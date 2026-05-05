---
title: 'POC de pagamento dividido: referência de variáveis de ambiente'
description: Saiba como mapear o Commerce OAuth, o URL básico, o limite de pagamento e as configurações de demonstração opcionais para os arquivos de orquestrador, extensão da interface do usuário e ambiente de simulação.
feature: App Builder, Configuration, Extensibility, Paas, REST, Security
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 115
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: d5f1e76c3a5127698f2933810fca218b79082571
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# POC de pagamento dividido: referência de variáveis de ambiente

As mesmas quatro credenciais do Commerce OAuth são usadas em cada componente. Em **[!UICONTROL Commerce Admin]**, crie um **[!UICONTROL Integration]** e reutilize os quatro valores em cada arquivo `.env` abaixo. (Consulte [POC de pagamento dividido: pré-requisitos e configuração de ambiente](./prerequisites-and-setup.md) para as etapas de ativação.)

## As quatro credenciais OAuth (usadas em todos os lugares)

| Variável | Onde obter |
| --- | --- |
| `COMMERCE_CONSUMER_KEY` | **[!UICONTROL Commerce Admin]** > **[!UICONTROL System]** > **[!UICONTROL Integrations]** > *[sua integração]* |
| `COMMERCE_CONSUMER_SECRET` | O mesmo que acima — os valores são mostrados somente na ativação |
| `COMMERCE_ACCESS_TOKEN` | Igual ao anterior |
| `COMMERCE_ACCESS_TOKEN_SECRET` | Igual ao anterior |


## App Builder orchestrator

### `split-payment-orchestrator/.env`

Copie de `.env.example` no diretório do orquestrador. Não confirme este arquivo.

```dotenv
# Commerce REST base URL — no trailing slash
COMMERCE_BASE_URL=https://your-store.example.com

# OAuth 1.0a integration credentials
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=

# Must match split_payment/general/threshold in Commerce config (default: 100)
# Both Commerce and App Builder fall back to 100 if this is missing, non-numeric, or ≤ 0
PAYMENT_THRESHOLD=100

LOG_LEVEL=info

# Demo dashboard: if set, requires ?secret=<value> in URL or x-demo-secret header
# Leave empty for private staging only (anyone with the URL can list/accept orders)
DEMO_UI_SECRET=

# Optional: override the base URL used in dashboard action links (useful behind proxies)
DEMO_UI_BASE_URL=
```


## Extensão da interface do usuário do Experience Cloud (commerce-checkout-starter-kit)

### `commerce-checkout-starter-kit/.env`

Este componente usa dois conjuntos de credenciais: IMS para listagem de pedidos com a interface do usuário SDK **[!UICONTROL Admin]** e OAuth 1.0a para ações de aceitação e recusa.

```dotenv
# IMS — used by CustomMenu/commerce-rest-api to list orders
# The Admin UI SDK provides the IMS token context; these set the Commerce base URL
COMMERCE_BASE_URL=https://your-store.example.com
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRETS=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_SCOPES=
OAUTH_IMS_ORG_ID=
AIO_CLI_ENV=stage

# OAuth 1.0a — same four credentials, COMMERCE_INTEGRATION_ prefix
COMMERCE_INTEGRATION_BASE_URL=https://your-store.example.com
COMMERCE_INTEGRATION_CONSUMER_KEY=
COMMERCE_INTEGRATION_CONSUMER_SECRET=
COMMERCE_INTEGRATION_ACCESS_TOKEN=
COMMERCE_INTEGRATION_ACCESS_TOKEN_SECRET=
```


## Script de simulação

### `commerce-backend-ui-1/.env.simulation`

Copiar de `.env.simulation.example` no mesmo diretório.

```dotenv
COMMERCE_BASE_URL=https://your-store.example.com
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```


## Notas

**`PAYMENT_THRESHOLD`** — Deve corresponder a `split_payment/general/threshold` na configuração do sistema **[!UICONTROL Commerce]**. Ambos os lados assumem o padrão `100` se o valor estiver ausente, não for numérico ou for menor ou igual a `0`. Se você alterar o limite em **[!UICONTROL Commerce]**, atualize o App Builder `.env` para corresponder.

**`DEMO_UI_SECRET`** — Opcional, mas recomendado para qualquer implantação que não seja localhost. Qualquer pessoa com o URL do painel pode listar pedidos e executar aceitar e recusar se estiver vazio. Para um ambiente de preparo real, defina um segredo compartilhado.

**`COMMERCE_BASE_URL`** — Nunca inclua uma barra à direita. O cliente Commerce REST anexa `/rest/V1/` automaticamente.

**`AIO_CLI_ENV`** — Definido como `stage` para o espaço de trabalho **[!UICONTROL Stage]**. Altere para `prod` ao implantar para **[!UICONTROL Production]**.


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
