---
title: 'POC de pagamento dividido: próximas etapas após a prova de conceito'
description: Saiba como mover a POC de pagamento dividido para produção. Interface do usuário do Experience Cloud, ganchos de ERP, malha de API, escopo do PHP, fluxos de trabalho do App Builder e lista de verificação de implantação.
feature: App Builder, API Mesh, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 269
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 8dfbf2694378aae76c91afa11bfee7d93077d8ba
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# POC de pagamento dividido: próximas etapas após a prova de conceito

O painel de demonstração e o script de simulação que você criou neste tutorial são intencionalmente ásperos. Eles existem para provar o padrão. Esta página descreve um caminho prático, da prova de conceito ao desenvolvimento de App Builder no estilo de produção.


## Etapa 1 — Substituir o painel de demonstração por uma extensão da interface do usuário do Experience Cloud

A ação da Web `demo-dashboard` serve o HTML de uma cadeia de caracteres dentro de uma função Node.js. Funciona, mas não é o padrão de produção.

A substituição adequada é a extensão `commerce-backend-ui-1` no `commerce-checkout-starter-kit` — um aplicativo React incorporado no Commerce Admin Shell por meio da interface do usuário SDK do Adobe Admin. Consulte [POC de pagamento dividido: prompt da IA de extensão da interface do usuário do Experience Cloud](./experience-cloud-ui-prompt.md) para o prompt de geração.

**O que muda:**
* Os operadores fazem logon por meio do Commerce Admin Shell (autenticação IMS em vez de um segredo compartilhado)
* A lista de pedidos usa o contexto do token IMS — sem necessidade de um segredo de demonstração
* As ações Aceitar/Recusar têm escopo para a identidade IMS do operador
* A interface do usuário é incorporada ao administrador do Commerce no URL que os administradores do Commerce já conhecem

**O que permanece o mesmo:**
* As ações do App Builder `payment-accept` e `payment-decline` permanecem inalteradas
* Os endpoints REST do Commerce permanecem inalterados
* O módulo PHP não é alterado


## Etapa 2 — conectar um ERP real

O fluxo de aceitação/recusa nesta PoC é orientado por um clique humano em um botão. Na produção, isso é orientado por seu ERP, CRM ou processador de pagamento.

**O padrão de integração:**
1. Seu sistema ERP captura dinheiro e chama `POST /payment-accept` (o URL da ação da Web do App Builder) com `{ orderId: <entity_id> }`
2. O App Builder valida a chamada (bearer token ou chave de API — adicione middleware de autenticação a `payment-accept`)
3. O App Builder chama o Commerce REST `cash-received`
4. O Commerce fatura e envia a ordem

Não são necessárias alterações no PHP. A superfície REST já está lá. A ação do App Builder só precisa de um chamador seguro em vez de um botão de painel.

**Opções de autenticação para o chamador ERP:**
* A Adobe I/O Runtime oferece suporte a `require-adobe-auth: true` para tokens IMS (se o ERP puder obter um token IMS)
* Para sistemas que não sejam da Adobe: adicione uma verificação simples de chave de API na ação `payment-accept` (compare um cabeçalho com um segredo armazenado no ambiente da ação)


## Etapa 3 — Adicionar a malha de API como uma camada do Broker

Atualmente, o App Builder chama o Commerce REST diretamente com credenciais OAuth 1.0a. Para implantações maiores, a API em malha do Adobe fornece uma camada de gateway gerenciada entre o App Builder e o Commerce.

**Vantagens:**
* Gerenciamento centralizado de credenciais — O API Mesh contém as credenciais do Commerce; o App Builder chama o API Mesh
* Solicitar transformação — mapear cargas do App Builder para formas REST do Commerce sem alterar a ação do App Builder
* Limitação de taxa e cache — proteja o Commerce contra tráfego de eventos de alto volume

**O padrão:**
* Substituir `createCommerceClient(params, logger)` chamadas por chamadas para o ponto de extremidade da API Mesh
* A API Mesh lida com a assinatura OAuth em relação ao Commerce


## Etapa 4 — Reduzir a Pegada PHP

O módulo PHP atual lida com cinco itens que devem permanecer em andamento (consulte [POC de pagamento dividido: decisões de arquitetura e design](./architecture-and-decisions.md)). À medida que a superfície da API do Adobe Commerce amadurece, alguns deles podem se tornar móveis:

**Potencialmente móvel no futuro:**
* A API REST de crédito da loja está evoluindo — as versões futuras podem oferecer suporte à aplicação de crédito pós-pedido ou a carrinhos inativos
* À medida que mais operações do Commerce se tornam assíncronas, o protetor de limite pode ser movido para um resolvedor de malha de API de pré-ordem

**Não móvel (restrições de arquitetura):**
* A manipulação de aspas antes de `placeOrder()` sempre exigirá um código em andamento, a menos que a Commerce exponha um gancho limpo por meio de um ponto de extensão API-first
* Os endpoints REST (`/V1/split-payment/*`) são específicos para esse recurso; eles residem no Commerce porque chamam os serviços internos da Commerce


## Etapa 5 — adicionar mais fluxo de trabalho ao App Builder

A PoC atual faz uma coisa: escuta a disposição do pedido e, em seguida, habilita a aceitação/recusa. Extensões naturais:

**Pontuação de fraude antes de aceitar:**
Em `payment-orchestrator`, depois de registrar dinheiro pendente, chame uma API de pontuação de fraude antes que o resultado da orquestração seja considerado final. Se a pontuação estiver acima de um limite, recuse automaticamente em vez de aguardar a ação do operador.

**Emails de notificação:**
Quando `payment-accept` tiver êxito, acione um email (via Adobe Campaign, SendGrid ou qualquer API HTTPS) notificando o cliente que seu pagamento em dinheiro foi confirmado.

**Prêmios de pontos de fidelidade:**
Depois que o dinheiro for confirmado, chame uma API de fidelidade para atribuir pontos. Isto é App Builder puro — não é necessário PHP.

**Manipulação de tempo limite:**
Adicione uma ação agendada do App Builder (usando `cron` em `app.config.yaml`) que verifica pedidos com `split_cash_status = 'pending'` mais de X dias e os recusa automaticamente.


## Etapa 6 — implantação para produção

A POC está configurada para o espaço de trabalho `Stage`. Movendo para produção:

```bash
# Switch to production workspace
aio app use
# Select Production workspace

# Update .env for production
# (same credentials, but production Commerce base URL)

# Deploy
aio app deploy
```

**Lista de verificação para prontidão de produção:**
* [ Conjunto ] `DEMO_UI_SECRET` (ou painel de demonstração substituído pela interface do Experience Cloud)
* [ ] `LOG_LEVEL=warn` ou `error` em produção (não `debug`)
* [ ] `PAYMENT_THRESHOLD` corresponde à configuração de produção do Commerce
* [ As credenciais de Integração do Commerce ] em `.env` são para uma integração de produção dedicada (não de preparo)
* [ ] incluo na lista de permissões de IP do Fastly atualizado com os IPs de saída de produção do App Builder (Commerce Cloud)
* [ ] Registro de evento de E/S confirmado no espaço de trabalho de produção


## Diagrama de Evolução da Arquitetura

```
PoC (this tutorial)
┌─────────────────────────────────────────────────┐
│  Commerce                 App Builder            │
│  ┌─────────────┐         ┌──────────────────┐   │
│  │  PHP Module │◄────────│ payment-orchestr │   │
│  │  REST API   │────────►│ payment-accept   │   │
│  │  Checkout UI│         │ payment-decline  │   │
│  └─────────────┘         │ demo-dashboard   │   │
└─────────────────────────────────────────────────┘

Phase 2: Experience Cloud UI
┌─────────────────────────────────────────────────┐
│  Commerce                 App Builder            │
│  ┌─────────────┐         ┌──────────────────┐   │
│  │  PHP Module │◄────────│ payment-orchestr │   │
│  │  REST API   │────────►│ payment-accept   │   │
│  │  Checkout UI│         │ payment-decline  │   │
│  │             │         │ Admin UI ext.    │   │
│  └─────────────┘         └──────────────────┘   │
└─────────────────────────────────────────────────┘

Phase 3: Real ERP + API Mesh
┌──────────────────────────────────────────────────────────┐
│  ERP  ──►  App Builder  ──►  API Mesh  ──►  Commerce     │
│            (orchestrator)   (gateway)    (PHP module      │
│            (accept)                      REST surface)    │
└──────────────────────────────────────────────────────────┘
```


## Referências principais

* [Documentação do Adobe App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Adobe I/O Events para Commerce](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"}
* [Kit inicial do Commerce Checkout](https://github.com/adobe/commerce-checkout-starter-kit){target="_blank"}
* [SDK da interface do administrador do Adobe](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}
* [Adobe API Mesh](https://developer.adobe.com/graphql-mesh-gateway/){target="_blank"}
* [Adobe I/O Runtime (OpenWhisk)](https://developer.adobe.com/runtime/docs/){target="_blank"}



{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
