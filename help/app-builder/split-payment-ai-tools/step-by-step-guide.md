---
title: Guia de implementação passo a passo da POC de pagamento dividido
description: Saiba como implementar a POC de pagamento dividido para depois que a configuração for concluída, cobrindo módulo, ambientes, orquestrador, verificação e interface opcional.
feature: App Builder, Eventing, Extensibility
topic: Commerce, Architecture, App Builder, Development
role: Developer
level: Intermediate
doc-type: Tutorial
duration: 480
jira: KT-20902
last-substantial-update: 2026-04-30T00:00:00Z
source-git-commit: 27811c05f066c95a60ac309472d6488295fb2c96
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# Guia de implementação passo a passo da POC de pagamento dividido

Esta página é a lista de verificação de implementação. Ele pressupõe que você já assistiu à [visão geral](./overview.md) e à [demonstração completa](./full-demo.md), e que o site da Commerce e o projeto do App Builder estão prontos. As páginas de tutorial individuais contêm detalhes completos sobre cada tópico abaixo. Use esta página para saber o que fazer e em que ordem.

## Antes de começar

Confirme todos os itens a seguir antes de executar qualquer prompt ou comando. A página [pré-requisitos e configuração](./prerequisites-and-setup.md) aborda detalhadamente cada item.

**Commerce Side**

* [ ] Adobe Commerce 2.4.5 ou posterior
* [ ] evento de E/S habilitado e implantado (somente Commerce Cloud — requer `ENABLE_EVENTING: true` em `.magento.env.yaml`)
* [ ] **Pagamento na Entrega** habilitado no Administrador com seu título definido exatamente como `Cash`
* [ ] Crédito da loja habilitado no Administrador
* [ ] O cliente de teste tem pelo menos US$ 50 de crédito de loja
* [ ] Integração do Commerce criada, ativada e todos os quatro valores OAuth salvos com segurança

**App Builder Side**

* [ ] Projeto do App Builder existe no Adobe Developer Console
* [ ] serviço Adobe I/O Events adicionado ao espaço de trabalho
* [ ] Commerce conectado como um provedor de eventos
* [ ] `aio login` concluído; espaço de trabalho correto selecionado com `aio app use`
* [ ] Node.js 18 ou posterior instalado; `aio` CLI instalado (`npm install -g @adobe/aio-cli`)

Se algo acima estiver ausente, pare aqui e conclua primeiro.

## Fase 1 — criação do módulo Commerce

**O que isso faz:** Gera o módulo PHP `Client_SplitPayment` que lida com a interface do usuário de check-out, a aplicação de crédito de armazenamento, os pontos de extremidade REST e a assinatura do evento de E/S. Este é o adaptador thin no Commerce — todo o workflow do operador permanece no App Builder.

### Etapa 1.1 — Personalizar o prompt do projeto

Abra a página [prompt do Commerce module AI](./commerce-module-prompt.md) e observe o seguinte antes de copiar o prompt:

* Substituir `Client` pelo nome real do fornecedor no prompt
* Substitua `SplitPayment` se quiser um nome de módulo diferente
* Se o tema não for Luma, talvez seja necessário ajustar o caminho de injeção `LayoutProcessorPlugin` e os mapeamentos RequireJS
* Se o seu método de Pagamento à Vista usa um código diferente de `cashondelivery`, atualize `payment-method-helper.js`

### Etapa 1.2 — Executar o prompt

Copie o prompt completo de **PROMPT START** para **End of prompt** e cole-o no Cursor (com Claude) ou diretamente no Claude. Execute-o a partir da raiz do seu projeto do Commerce para que a IA possa criar arquivos em `app/code/`.

### Etapa 1.3 — Ativar e instalar o módulo

Execute estes comandos na raiz do projeto do Commerce:

```bash
bin/magento module:enable Client_SplitPayment
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento setup:static-content:deploy -f
bin/magento cache:flush
```

### Etapa 1.4 — Verificar se o módulo está instalado corretamente

```bash
# Confirm the module is active
bin/magento module:status Client_SplitPayment

# Confirm the split_ columns were added to sales_order
mysql -u <user> -p <dbname> -e "DESCRIBE sales_order;" | grep split
```

Você deve ver cinco colunas: `split_store_credit_amount`, `split_cash_amount`, `split_cash_status`, `split_sc_invoice_id` e `split_cash_invoice_id`.

Em seguida, confirme em um navegador que os campos de pagamento dividido aparecem no check-out quando um cliente conectado com crédito da loja seleciona **Caixa** como o método de pagamento.

## Fase 2 — Configurar variáveis de ambiente

**O que isso faz:** prepara os arquivos de credencial usados pelo App Builder Orchestrator, pelo script de simulação e (opcionalmente) pela extensão da interface do usuário do Experience Cloud. Os mesmos quatro valores OAuth da sua integração do Commerce são usados em cada arquivo `.env`.

Consulte a [referência das variáveis de ambiente](./env-reference.md) para obter a lista completa de variáveis por componente.

### Etapa 2.1 — Criar o orquestrador `.env`

No diretório `split-payment-orchestrator/`:

```bash
cp .env.example .env
```

Preencher todos os valores:

| Variável | Onde obter |
|---|---|
| `COMMERCE_BASE_URL` | O URL da sua loja — sem barra à direita |
| `COMMERCE_CONSUMER_KEY` | Administração do Commerce > Sistema > Integrações |
| `COMMERCE_CONSUMER_SECRET` | Igual — exibido somente na ativação |
| `COMMERCE_ACCESS_TOKEN` | Igual |
| `COMMERCE_ACCESS_TOKEN_SECRET` | Igual |
| `PAYMENT_THRESHOLD` | Deve corresponder a `split_payment/general/threshold` no Commerce (padrão: `100`) |
| `DEMO_UI_SECRET` | Opcional — se definido, exigido como `?secret=` no URL do painel |

### Etapa 2.2 — Criar o script de simulação `.env`

```bash
cp commerce-backend-ui-1/.env.simulation.example commerce-backend-ui-1/.env.simulation
```

Preencha `COMMERCE_BASE_URL` e os quatro valores de OAuth (as mesmas credenciais que as acima).

## Fase 3 — criação do App Builder Orchestrator

**O que isso faz:** Gera o projeto do App Builder `split-payment-orchestrator`: o consumidor de Eventos de E/S `payment-orchestrator`, as ações da Web `payment-accept` e `payment-decline` e a interface do operador `demo-dashboard`.

### Etapa 3.1 — Executar o prompt do orquestrador

Abra a página [prompt do App Builder orchestrator AI](./orchestrator-prompt.md). Copie o prompt completo e execute-o no diretório `split-payment-orchestrator/`.

### Etapa 3.2 — Instalar dependências e implantar

```bash
cd split-payment-orchestrator
npm install
# Confirm .env is filled in (from Phase 2, Step 2.1)
aio app deploy
```

Após a implantação, `aio app deploy` imprime as URLs de ação. Anote a URL `demo-dashboard` — você precisa dela na Fase 4.

### Etapa 3.3 — Confirmar o registro do evento

No Adobe Developer Console, abra o espaço de trabalho de projetos do App Builder. Em **Eventos**, confirme se o registro de `Split payment — sales order place before` existe e está associado à ação `payment-orchestrator`.

## Fase 4 — Ensaio do caudal completo

Siga as etapas de verificação em ordem. O [guia de teste e verificação](./testing-and-verification.md) tem os comandos curl completos, o uso do script de simulação e a referência de solução de problemas para cada etapa abaixo.

### Etapa 4.1 — Verificar se os endpoints REST são roteáveis

```bash
# Expect 401, not 404 — the endpoint exists but requires auth
curl -X POST https://your-store.example.com/rest/V1/split-payment/orders/1/cash-received
```

### Etapa 4.2 — testar a interface do usuário de check-out

1. Faça logon na loja como cliente de teste (aquele com crédito de loja)
2. Adicionar um produto ao carrinho com um total inferior a US$ 100 após o envio e o imposto
3. Na etapa de pagamento, selecione **Caixa**
4. Confirme se os campos de pagamento parcelado aparecem: saldo exibido, caixa pré-preenchido, crédito de armazenamento a US$ 0
5. Reduza o valor de caixa e confirme se a parte de crédito da loja foi atualizada corretamente

### Passo 4.3 - Testar o protetor de limiar

Adicione produtos que totalizam mais de US$ 100, prossiga para o checkout, selecione Dinheiro e tente fazer o pedido. O erro `"Payment could not be processed. Please try again or contact support."` deve aparecer.

### Etapa 4.4 — Colocar uma ordem de pagamento dividido de teste

Crie um carrinho com menos de US$ 100, insira uma divisão de crédito em dinheiro/loja e faça o pedido. No Commerce Admin, confirme:

* O status do pedido é `pending_payment`
* Dois comentários do App Builder estão visíveis no pedido:
   1. `"Cash payment of $X.XX pending. Awaiting admin confirmation."`
   2. `"Split payment orchestration completed. Order awaiting cash confirmation."`

Se nenhum comentário do App Builder for exibido, verifique os logs com `aio app logs` antes de continuar.

### Etapa 4.5 — Aceitação do teste por meio do script de simulação

```bash
# Find your order's entity_id
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs list

# Accept the payment
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs accept <entity_id>
```

No Commerce Admin, confirme:

* Status do pedido alterado para `processing`
* Comentário do histórico: `"Cash payment of $X.XX received."`
* NFF em dinheiro visível na guia NFFs
* Entrega visível na guia Entregas (se aplicável)

### Etapa 4.6 — Declínio do ensaio através de script de simulação

Coloque outra ordem de teste e, em seguida:

```bash
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs decline <entity_id>
```

O status da confirmação do pedido é `canceled` e `split_cash_status` é `declined`.

### Etapa 4.7 — Testar o painel de demonstração

Abra o URL do painel na Etapa 3.2. Com um pedido pendente no sistema:

1. Confirmar se o pedido aparece na lista pendente
2. Clique em **Aceitar** e confirme se a ordem foi movida para `processing` no Commerce
3. Faça um novo pedido, retorne ao painel e clique em **Recusar** — confirmar cancelamento

## Fase 5 (opcional) — Adicionar a extensão da interface do usuário do Experience Cloud

Esta fase incorpora o painel do operador ao shell Commerce Admin em vez de usar o `demo-dashboard` independente. Ignore esta fase se o painel independente atender às suas necessidades.

### Etapa 5.1 — revisão dos pré-requisitos

A extensão da interface do usuário do Experience Cloud requer credenciais IMS, além dos valores de integração OAuth. Leia a página [Prompt da IA de extensão da interface do usuário do Experience Cloud](./experience-cloud-ui-prompt.md) antes de executar o prompt, prestando atenção ao `OAUTH_CLIENT_ID` e às variáveis IMS relacionadas.

### Etapa 5.2 — Executar o prompt de extensão da interface

Copie o prompt completo de **PROMPT START** para **End of prompt** e execute-o no diretório `commerce-checkout-starter-kit/`.

### Etapa 5.3 — Implantação

```bash
cd commerce-checkout-starter-kit
npm install
cp .env.dist .env
# Fill in IMS credentials and COMMERCE_INTEGRATION_* credentials
aio app deploy
```

## Referência rápida de solução de problemas

| Sintoma | Primeira coisa a verificar |
|---|---|
| Os campos de pagamento dividido não aparecem no check-out | Erros RequireJS no console do navegador; também execute `bin/magento cache:flush` |
| `"Payment could not be processed"` na ordem do local | `PlaceOrderPlugin` ou `BalanceManagementInterface` — adicionar log de depuração temporário em `PlaceOrderPlugin` |
| Nenhum comentário do App Builder no pedido | Execute `aio app logs` para ver se o evento foi acionado e o que a ação retornou |
| `403` do Commerce REST no App Builder | Fastly IP incluir na lista de permissões — teste com o script de simulação primeiro; se isso funcionar, o problema será o bloqueio de IP de saída |
| `"The signature is invalid"` do Commerce | Confirmar se `COMMERCE_BASE_URL` não tem nenhuma barra à direita; confirmar se a integração está ativada |
| Os pedidos não aparecem no painel de demonstração | Verifique se `extension_attributes.split_cash_status` aparece em uma resposta direta de `GET /rest/V1/orders` |

Para obter detalhes completos sobre a solução de problemas, consulte o [guia de teste e verificação](./testing-and-verification.md#common-issues-and-fixes).

{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
