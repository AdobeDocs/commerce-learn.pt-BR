---
title: POC de pagamento dividido — prompt do App Builder orchestrator AI
description: Saiba como usar este prompt para criar o aplicativo split-payment-orchestrator. Eventos de E/S, orquestrador de pagamentos, ações da Web, painel de demonstração e implantação do aplicativo aio.
feature: App Builder, Configuration, Eventing, Extensibility, Paas, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 421
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# POC de pagamento dividido: prompt do App Builder orchestrator AI

Use esta página para copiar o prompt completo que gera o projeto **split-payment-orchestrator**: o **payment-orchestrator** consumidor de Eventos de E/S, **payment-accept** e **payment-deny** ações da Web, o **demo-dashboard** e o cliente REST da Commerce.

## Como usar este prompt

Copie tudo de **PROMPT START** para **End of prompt** no Cursor (com Claude) ou diretamente no Claude. Execute o prompt a partir do diretório `split-payment-orchestrator/` (a raiz do projeto App Builder).

## Antes de executar

* Concluir [POC de pagamento dividido: pré-requisitos e configuração de ambiente](./prerequisites-and-setup.md).
* Tenha seu arquivo [Split payment POC: environment variables reference](./env-reference.md) and `.env` pronto no projeto.


## O prompt

**INÍCIO DA SOLICITAÇÃO**


Você está gerando um aplicativo completo do Adobe App Builder para orquestrar pagamentos parcelados no Adobe Commerce. Esse aplicativo recebe Eventos de E/S da Commerce, processa decisões de pagamento dividido e retorna chamadas para a Commerce via REST.

**Projeto:** `split-payment-orchestrator`
**Tempo de execução:** Node.js 18
**Dependências de chave:** `@adobe/aio-sdk ^6.0.0`, `got ^11.8.6`, `oauth-1.0a ^2.2.6`

Gere todos os arquivos listados abaixo. O aplicativo deve funcionar com o Adobe I/O Runtime (`aio app deploy`).


### Estrutura de arquivo a ser gerada

```
split-payment-orchestrator/
├── package.json
├── app.config.yaml
├── .env.example
└── actions/
    ├── payment-orchestrator/
    │   ├── index.js         ← I/O Event entry point
    │   ├── commerce-client.js
    │   ├── threshold.js
    │   ├── cash-payment.js
    │   ├── order-update.js
    │   └── store-credit.js  ← Deprecated stub; kept for reference
    ├── payment-accept/
    │   └── index.js
    ├── payment-decline/
    │   └── index.js
    └── demo-dashboard/
        └── index.js
```


### `package.json`

```json
{
  "name": "split-payment-orchestrator",
  "version": "1.0.0",
  "private": true,
  "description": "Adobe App Builder action — split payment PoC orchestrator",
  "engines": { "node": ">=18" },
  "scripts": {
    "deploy": "NODE_OPTIONS=--disable-warning=DEP0040 aio app deploy",
    "aio": "NODE_OPTIONS=--disable-warning=DEP0040 aio"
  },
  "dependencies": {
    "@adobe/aio-sdk": "^6.0.0",
    "@adobe/exc-app": "^1.5.9",
    "got": "^11.8.6",
    "oauth-1.0a": "^2.2.6"
  }
}
```


### `app.config.yaml`

Defina quatro ações no pacote `split_payment_orchestrator`:

**`payment-orchestrator`**
* `web: "no"` (somente Gatilho de Evento de E/S — não pode ser chamado diretamente via HTTP)
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Entradas do ambiente: `LOG_LEVEL`, `COMMERCE_BASE_URL`, `COMMERCE_CONSUMER_KEY`, `COMMERCE_CONSUMER_SECRET`, `COMMERCE_ACCESS_TOKEN`, `COMMERCE_ACCESS_TOKEN_SECRET`, `PAYMENT_THRESHOLD`

**`payment-accept`**
* `web: "yes"` (Ação da Web HTTP — chamada pelo painel ou ERP)
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Mesmas entradas de credencial do Commerce (sem `PAYMENT_THRESHOLD`)

**`payment-decline`**
* `web: "yes"`
* `runtime: nodejs:18`
* `require-adobe-auth: true`, `final: true`
* Mesmas entradas de credencial do Commerce

**`demo-dashboard`**
* `web: "yes"`
* `runtime: nodejs:18`
* `require-adobe-auth: false` ← O painel está acessível publicamente (protegido apenas por `DEMO_UI_SECRET`, se estiver definido)
* Entradas: todas as credenciais do Commerce + `DEMO_UI_SECRET`, `DEMO_UI_BASE_URL`

**Registro de eventos** (em `events.registrations`):

```yaml
Split payment — sales order place before:
  description: Invokes payment-orchestrator when an order is about to be placed
  events_of_interest:
    - provider_metadata: dx_commerce_events
      event_codes:
        - com.adobe.commerce.observer.sales_order_place_before
  runtime_action: split_payment_orchestrator/payment-orchestrator
```


### `actions/payment-orchestrator/commerce-client.js`

Cliente REST OAuth 1.0a compartilhado para Adobe Commerce. Implementa:

**`createCommerceClient(params, logger)`** — retorna `{ request, baseUrl }`

* Lê `COMMERCE_BASE_URL`, `COMMERCE_CONSUMER_KEY`, `COMMERCE_CONSUMER_SECRET`, `COMMERCE_ACCESS_TOKEN`, `COMMERCE_ACCESS_TOKEN_SECRET` de `params`
* Gera se alguma credencial estiver ausente
* Usa `oauth-1.0a` com `HMAC-SHA256` (Node.js `crypto.createHmac`)
* Usa `got@11` (não `got@12+` — o projeto usa CJS) com `prefixUrl = ${baseUrl}/rest/V1/`
* Adiciona o cabeçalho `Authorization` através do gancho `beforeRequest`
* `request(method, path, options)` — normaliza o caminho (remove a entrelinha `/`), retorna `{ statusCode, body }`
* `throwHttpErrors: false` — nunca lança em 4xx/5xx; sempre retorna o código de status


### `actions/payment-orchestrator/threshold.js`

**`evaluateThreshold({ orderTotal, storeCreditAmount, cashAmount, params, logger })`** — retorna `{ pass: boolean, reason: string }`

Lógica:
1. Ler `params.PAYMENT_THRESHOLD`; analisar como flutuante; padrão: `100` se ausente, NaN ou ≤ 0
2. Se `orderTotal > threshold`: retornar `{ pass: false, reason: 'PAYMENT_THRESHOLD_EXCEEDED' }`
3. Se `Math.abs((storeCreditAmount + cashAmount) - orderTotal) > 0.02`: retornar `{ pass: false, reason: 'SPLIT_AMOUNT_MISMATCH' }`
4. Caso contrário: retornar `{ pass: true, reason: '' }`


### `actions/payment-orchestrator/cash-payment.js`

**`recordCashPending({ commerce, orderId, cashAmount, logger })`** — retorna `{ ok: boolean, error? }`

* Chama `POST orders/${orderId}/comments` com:

  ```json
  {
    "statusHistory": {
      "comment": "Cash payment of $X.XX pending. Awaiting admin confirmation.",
      "entity_name": "order",
      "parent_id": "<orderId>",
      "is_visible_on_front": true,
      "is_customer_notified": false,
      "status": "pending_payment"
    }
  }
  ```

* Retorna `{ ok: true }` em 2xx; caso contrário, retorna `{ ok: false, error: { code, message } }`
* Envolve try/catch; retorna o objeto de erro, nunca lança


### `actions/payment-orchestrator/order-update.js`

**`updateOrderAfterOrchestration({ commerce, orderId, success, detail, logger })`** — retorna `{ ok: boolean, error? }`

* Se `success`: postou um comentário de histórico `"Split payment orchestration completed. Order awaiting cash confirmation."`
* Se `!success`: postagens `"Payment could not be processed. Please try again or contact support."` — nunca inclua `detail` no comentário visível ao cliente; registre `detail` apenas internamente
* Retorna `{ ok: boolean, error? }` — nunca lança


### `actions/payment-orchestrator/store-credit.js`

**`applyStoreCredit({ commerce, cartId, amount, logger })`** — implementação no-op obsoleta

Inclua este arquivo com um aviso JSDoc `@deprecated` explicando:
> O orquestrador não aplica mais crédito de armazenamento via REST. O crédito de armazenamento é aplicado no check-out no módulo Commerce PHP (`PlaceOrderPlugin`) usando `BalanceManagementInterface::apply()`, que requer um carrinho ativo. Quando a App Builder recebe o evento de I/O, o carrinho fica inativo. Esse arquivo é mantido para referência ou para fluxos personalizados em que o crédito da loja é aplicado após o pedido.

Manter uma implementação em funcionamento (mesma forma que outros módulos) para que os desenvolvedores possam estudar o padrão, mas marcá-lo claramente como não usado no fluxo atual.


### `actions/payment-orchestrator/index.js`

Ponto de entrada do evento de E/S. Implementa `async function main(params)`.

**Extração de carga:**

Os Eventos do Adobe Commerce I/O podem fornecer a carga de várias formas. Extraia o objeto de valor da ordem verificando esses caminhos em ordem:
1. `params.__ow_body` (analisar cadeia de caracteres JSON se necessário) → `.event.data.value`
2. `params.data.value`
3. `params.value`
4. `params.body.event.data.value`
5. Voltar para o próprio `params`

**Extração de campo do valor:**
* `orderId = value.entity_id || value.id`
* `orderTotal = parseFloat(value.grand_total ?? value.base_grand_total ?? value.subtotal ?? '0')`
* Dividir valores de `value.extension_attributes` (verificar `extension_attributes` e `extensionAttributes`):
   * `storeCredit = parseFloat(ext.split_store_credit_amount ?? value.split_store_credit_amount ?? '0')`
   * `cash = parseFloat(ext.split_cash_amount ?? value.split_cash_amount ?? '0')`

**Fluxo:**
1. Extrair valor; se `orderId` estiver ausente, registrar erro e retornar `{ statusCode: 200, body: { ok: false, message: PUBLIC_ERROR } }`
2. Chamar `evaluateThreshold(...)` — se falhar, registrar e retornar a mesma resposta 200
3. Chamada `createCommerceClient(params, logger)` — se falhar, retornar o erro 200
4. Se `storeCredit > 0`, registrar que o crédito de armazenamento foi aplicado no check-out (nenhuma chamada REST é necessária)
5. Chamada `recordCashPending(...)` — se falhar, chama `updateOrderAfterOrchestration(..., success: false)` e retorna o erro 200
6. Ligar para `updateOrderAfterOrchestration(..., success: true)`
7. Retornar `{ statusCode: 200, body: { ok: true, message: 'processed' } }`

**Importante:** sempre retornar `statusCode: 200` — o I/O Runtime tentará novamente respostas não-200, o que pode causar processamento de pedido duplicado. Erros são relatados no corpo.

**`PUBLIC_ERROR`constante:** `"Payment could not be processed. Please try again or contact support."` — usada para todas as mensagens de erro direcionadas para o exterior.


### `actions/payment-accept/index.js`

Ação da Web HTTP. Chama `POST /V1/split-payment/orders/:orderId/cash-received`.

**Resolução da ID do pedido:** Verifique `params.orderId`, depois `params.payload.orderId`, depois `params.__ow_body` (JSON analisado). Retorna 400 se estiver faltando.

**Fluxo:**
1. Resolver `orderId`; retornar 400 se ausente
2. Init commerce client; retorna 500 se falhar
3. Chamar `POST split-payment/orders/${orderId}/cash-received` com corpo JSON vazio
4. Se 2xx: retornar `{ statusCode: 200, body: { ok: true, orderId, message: 'accepted' } }`
5. Em caso de erro: registrar e retornar `{ statusCode: 200, body: { ok: false, message: PUBLIC_ERROR } }`


### `actions/payment-decline/index.js`

Ação da Web HTTP. Mesmo padrão de `payment-accept`, mas chama `POST /V1/split-payment/orders/:orderId/cash-decline`.

Retornar `{ ok: true, orderId, message: 'declined' }` em caso de sucesso.


### `actions/demo-dashboard/index.js`

Painel de operador de demonstração independente. Serve um painel do HTML para listar ordens de caixa pendentes e acionar ações de aceitação/recusa. Essa é uma única ação da Web que atende à interface do usuário do HTML e a uma API JSON.

**Segurança:**
* Verificação `DEMO_UI_SECRET` opcional: se definida, requer `?secret=<value>` parâmetro de consulta ou cabeçalho `x-demo-secret` em todas as solicitações. Retorna 401 se ausente/incorreto.
* Registrar um aviso se `DEMO_UI_SECRET` não estiver definido (o painel está desprotegido)

**Roteamento (com base no método HTTP + caminho/corpo):**

A ação recebe todas as solicitações. Determinar intenção de:
* `params.__ow_method` (GET/POST) e `params.__ow_path` ou parâmetros de ação
* `GET` sem nenhuma ação → servir o painel do HTML
* `GET` com o parâmetro `action=list` → retornar a lista JSON de pedidos pendentes
* `POST` com `action=accept` e `orderId` → chame a lógica `payment-accept` (ou incorpore a chamada REST do Commerce)
* `POST` com `action=decline` e `orderId` → chame a lógica `payment-decline`

**Buscando pedidos pendentes:**
* Chamada `GET orders?searchCriteria[pageSize]=50` do Commerce REST
* Filtrar para ordens nas quais `extension_attributes.split_cash_status === 'pending'` E ordem não estão em um estado terminal (`complete`, `closed`, `canceled`, `cancelled`)
* Classificar primeiro mais recente na memória
* Retornar até 20 (configurável por meio do parâmetro `limit`)

**Painel do HTML:**
O painel é uma cadeia de caracteres do HTML retornada com `Content-Type: text/html`. Ele deve:
* Listar ordens de pagamento à vista pendentes em uma tabela: Nº da Ordem (increment_id), entity_id, nome do cliente, valor de pagamento à vista, valor de crédito de armazenamento, data
* Forneça os botões **Aceitar** e **Recusar** para cada ordem que chama o ponto de extremidade de API da própria ação
* Mostrar respostas de sucesso/erro em linha
* Incluir um botão de atualização
* Ser estilizado o suficiente para ser utilizável (o CSS mínimo é adequado; não há dependências externas de CDN para evitar problemas com o CORS no tempo de execução)
* Mostrar um banner de aviso se `DEMO_UI_SECRET` não estiver definido

**Erro ao exibir na interface do usuário:**
Quando uma chamada REST do Commerce falhar, inclua o status HTTP e uma breve descrição do corpo do erro do Commerce (limpar — retirar as tags do HTML, truncar para 500 caracteres). Não exponha as credenciais.

**Auxiliares de resposta:**

```javascript
function jsonResponse(statusCode, obj, extraHeaders = {}) { ... }
function htmlResponse(html) { ... }
```


### `.env.example`

```dotenv
# Commerce REST base URL — no trailing slash
COMMERCE_BASE_URL=

# OAuth 1.0a integration credentials (Admin → System → Integrations)
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=

# PoC threshold — must match split_payment/general/threshold in Commerce (default: 100)
PAYMENT_THRESHOLD=100

LOG_LEVEL=info

# Demo dashboard optional shared secret
DEMO_UI_SECRET=
DEMO_UI_BASE_URL=
```


### Implantar Comando

Após gerar todos os arquivos, no diretório `split-payment-orchestrator/`:

```bash
npm install
cp .env.example .env
# Edit .env with your credentials
aio app deploy
```

Após a implantação, observe as URLs de ação impressas por `aio app deploy`. A URL `demo-dashboard` é onde você acessa o painel do operador.


### Fim da solicitação


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
