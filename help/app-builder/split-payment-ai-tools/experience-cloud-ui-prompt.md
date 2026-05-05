---
title: 'POC de pagamento dividido: prompt da IA de extensão da interface do usuário do Experience Cloud'
description: 'Saiba como usar esse prompt opcional para incorporar o pagamento dividido no Commerce Admin: interface do usuário do SDK, IMS, OAuth, aceitar e recusar e o script de simulação.'
feature: App Builder, Admin Workspace, Extensibility, Paas, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 192
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 629bbb6fe26f128e346d85c857111c2f8dbb6d76
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# POC de pagamento dividido: prompt da IA de extensão da interface do usuário do Experience Cloud

Esta é a etapa opcional que incorpora um painel de ordens de pagamento divididas no Experience Cloud (Admin Shell) do **[!UICONTROL Adobe Commerce]** usando o padrão `commerce-checkout-starter-kit` e `commerce-backend-ui-1`. O [painel de demonstração](./orchestrator-prompt.md) autônomo do App Builder Orchestrator cobre o mesmo fluxo de aceitação e recusa sem a integração do shell do administrador.

## Como usar este prompt

Copie tudo de **PROMPT START** para **End of prompt** no Cursor ou Claude. Execute o prompt no diretório `commerce-checkout-starter-kit/`.

## Antes de executar

* Este caminho precisa de credenciais de **IMS**, além dos valores de OAuth (consulte [POC de pagamento dividido: referência de variáveis de ambiente](./env-reference.md) para as variáveis `commerce-checkout-starter-kit`).
* Conclua a POC [Dividir pagamento: prompt da IA do App Builder orchestrator](./orchestrator-prompt.md) primeiro se desejar que o mesmo comportamento de `payment-accept` e `payment-decline` seja comparado; a extensão da interface reutiliza essa lógica com nomes de ambiente `COMMERCE_INTEGRATION_*`.


## O prompt

**INÍCIO DA SOLICITAÇÃO**


Você está gerando a extensão do SDK da interface do Administrador `commerce-backend-ui-1` para a PoC de pagamento dividido. Esta extensão incorpora um painel de ordens de pagamento parceladas ao Adobe Commerce Admin Shell usando os padrões `@adobe/aio-app-dev-toolkit` e `@adobe/commerce-backend-ui-1` do Kit Inicial do Commerce Checkout.

**Projeto base:** `commerce-checkout-starter-kit/`
**Diretório de extensão:** `commerce-checkout-starter-kit/commerce-backend-ui-1/`


### O que esta extensão oferece

1. **Painel de grade de ordem do administrador** — um item de menu personalizado no Commerce Admin Shell que lista ordens de pagamento divididas com `split_cash_status = 'pending'`
2. **Visualização detalhada do pedido** — mostra a divisão de pagamento (valor do pagamento à vista, valor do crédito da loja, status) ao lado do pedido
3. **Ações Aceitar/Recusar** — botões que chamam as ações do App Builder `payment-accept` e `payment-decline` via OAuth 1.0a


### Estrutura de arquivo a ser gerada

```
commerce-checkout-starter-kit/commerce-backend-ui-1/
├── ext.config.yaml
├── README.md
├── .env.simulation.example
├── actions/
│   ├── utils.js
│   ├── commerce/
│   │   └── index.js           ← IMS-based Commerce REST (order listing)
│   ├── payment-accept/
│   │   ├── commerce-client.js ← OAuth 1.0a (accept/decline)
│   │   └── index.js
│   ├── payment-decline/
│   │   └── index.js
│   └── registration/
│       └── index.js
├── scripts/
│   ├── README.md
│   └── simulate-split-payment.mjs
└── web-src/
    ├── index.html
    ├── package.json
    ├── .parcelrc
    └── src/
        ├── index.jsx
        ├── index.css
        ├── utils.js
        ├── exc-runtime.js
        ├── config.json
        ├── constants/
        │   └── extension.js
        ├── components/
        │   ├── App.jsx
        │   ├── ExtensionRegistration.jsx
        │   ├── MainPage.jsx
        │   ├── SplitPaymentDashboard.jsx
        │   └── SplitPaymentOrderDetail.jsx
        └── hooks/
            └── useSplitPaymentOrders.js
```


### Ações de backend

**`actions/commerce/index.js`** — Commerce REST autenticado pelo IMS
* Usa o token IMS fornecido pelo contexto SDK da interface do administrador para chamar o Commerce REST
* Obtém a lista de ordens com o filtro `split_cash_status`
* Retorna a lista de pedidos como JSON

**`actions/payment-accept/commerce-client.js`** — Cliente OAuth 1.0a
* Mesma implementação que `split-payment-orchestrator/actions/payment-orchestrator/commerce-client.js`
* Usa `COMMERCE_INTEGRATION_*` variáveis de ambiente com prefixo (para diferenciar das credenciais IMS)

**`actions/payment-accept/index.js`** — Aceitar ação
* Mesma lógica que `split-payment-orchestrator/actions/payment-accept/index.js`
* Chamadas `POST /V1/split-payment/orders/:orderId/cash-received` via OAuth 1.0a

**`actions/payment-decline/index.js`** — Recusar ação
* Chamadas `POST /V1/split-payment/orders/:orderId/cash-decline`

**`actions/registration/index.js`** — Registro SDK da interface do usuário do administrador
* Registra a extensão com o Admin Shell do Commerce
* Adiciona um item de menu em Pedidos para o painel de pagamento dividido


### Componentes de front-end do React

**`SplitPaymentDashboard.jsx`**
* Lista as ordens de pagamento com divisão pendentes em uma tabela do estilo Espectro
* Colunas: Número da Ordem (increment_id), Data, Cliente, Caixa Devido, Crédito da Loja, Status
* Botões Aceitar e Recusar por linha
* Chama ações de back-end por meio de `web-src/src/utils.js` auxiliares de busca
* Mostra estados de carregamento/erro; atualiza após a conclusão da ação

**`SplitPaymentOrderDetail.jsx`**
* Mostra detalhes do pagamento dividido para um único pedido
* Exibe: quantia de caixa, quantia de crédito de armazenamento, split_cash_status atual

**`useSplitPaymentOrders.js`** — Gancho React
* Obtém ordens de pagamento parceladas de `actions/commerce/index.js`
* Retorna `{ orders, loading, error, refresh }`


### Script de simulação

**`scripts/simulate-split-payment.mjs`**

Um script ESM Node.js para testar chamadas REST do Commerce diretamente (sem passar pelo App Builder). Usa a mesma assinatura OAuth 1.0a das ações do App Builder.

Comandos:
* `node simulate-split-payment.mjs help` — mostrar uso
* `node simulate-split-payment.mjs list` — listar pedidos recentes com dados de pagamento dividido
* `node simulate-split-payment.mjs show <orderId>` — mostrar campos de pagamento dividido para um pedido específico (entity_id)
* `node simulate-split-payment.mjs accept <orderId>` — chamar ponto de extremidade `cash-received`
* `node simulate-split-payment.mjs decline <orderId>` — chamar ponto de extremidade `cash-decline`

Lê credenciais de `commerce-backend-ui-1/.env.simulation` (copiar de `.env.simulation.example`).

**`.env.simulation.example`:**

```dotenv
COMMERCE_BASE_URL=https://your-store.example.com
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```


### `ext.config.yaml`

Configurar a extensão com:
* O tipo de extensão `commerce-backend-ui-1`
* As quatro ações de back-end (`commerce`, `payment-accept`, `payment-decline`, `registration`)
* `require-adobe-auth: true` para todas as ações exceto `registration`
* Associações de entrada do ambiente para credenciais `COMMERCE_INTEGRATION_*`


### Após gerar os arquivos

```bash
cd commerce-checkout-starter-kit
npm install
cp .env.dist .env
# Fill in IMS credentials and COMMERCE_INTEGRATION_* credentials
aio app deploy
```

### Fim da solicitação


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
