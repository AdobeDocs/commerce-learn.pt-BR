---
title: POC de pagamento dividido — pré-requisitos e configuração do ambiente
description: Saiba como configurar o Commerce, o Admin para COD e armazenar crédito, integração OAuth, Eventos de E/S, App Builder e aio CLI antes dos prompts de build do pagamento dividido.
feature: App Builder, Configuration, Eventing, Extensibility, Paas, Payments, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 262
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# POC de pagamento dividido: pré-requisitos e configuração de ambiente

Conclua todas as etapas deste tutorial antes de executar qualquer um dos prompts de construção. A falta de uma única etapa é o motivo mais comum para o fluxo ser interrompido no meio do tutorial.

## &#x200B;1. Requisitos do Adobe Commerce

* Adobe Commerce **2.4.5 ou posterior** (local ou Commerce Cloud)
* Acesso Git ao projeto Commerce (você adiciona um módulo em `app/code/`)
* Acesso a **[!UICONTROL Commerce Admin]**

### Somente Commerce Cloud: habilitar eventos de E/S

Adicione o seguinte a `.magento.env.yaml` e implante antes de adicionar o módulo:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

> **Aviso:** esta implantação deve ser concluída com êxito para que a dependência do módulo de Eventos de E/S possa ser resolvida.


## &#x200B;2. Configuração de administração do Commerce

Faça essas etapas antes de qualquer outra coisa. O checkout do JavaScript depende das correspondências exatas da string.

### 2-A. Habilitar Pagamento na Entrega com o título exato

**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Payment Methods]** > **[!UICONTROL Cash On Delivery Payment]**

* **[!UICONTROL Enabled]**: **Sim**
* **[!UICONTROL Title]**: **`Cash`** (esta cadeia de caracteres exata é a que o JavaScript de check-out corresponde)

> **Observação:** se sua loja usar uma implementação ou um título diferente para pagamento na entrega (COD), ajuste `payment-method-helper.js` no módulo Commerce.

### 2-B. Habilitar crédito da loja

**[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Store Credit Options]**

* **[!UICONTROL Enable Store Credit Functionality]**: **Sim**

### 2-C. Adicionar crédito da loja ao cliente de teste

**[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > *[seu cliente de teste]* > **[!UICONTROL Store Credit]** > **[!UICONTROL Update Balance]**

Adicione pelo menos **$50** ao crédito da loja. Você testará com um pedido abaixo de US$ 100 no total.

### 2-D Criar a integração do Commerce

**[!UICONTROL System]** > **[!UICONTROL Integrations]** > **[!UICONTROL Add New Integration]**

* **[!UICONTROL Name]**: `Split Payment App Builder` (ou qualquer nome que você preferir)
* Na guia **[!UICONTROL API]**, conceda no mínimo:
   * `Magento_Sales::actions` (obrigatório para o ponto de extremidade `cash-received`)
   * `Magento_Sales::cancel` (obrigatório para o ponto de extremidade `cash-decline`)
   * Gerenciamento de cotas ou carrinhos (completo ou um subconjunto relevante)
   * **[!UICONTROL Customer balance]** (completo ou um subconjunto relevante)

Selecione **[!UICONTROL Save]**, depois **[!UICONTROL Activate]**.

**Copie todos os quatro valores; eles são mostrados apenas uma vez:**

| Valor | Variável de ambiente |
| --- | --- |
| Chave do consumidor | `COMMERCE_CONSUMER_KEY` |
| Segredo do consumidor | `COMMERCE_CONSUMER_SECRET` |
| Token de acesso | `COMMERCE_ACCESS_TOKEN` |
| Senha do token de acesso | `COMMERCE_ACCESS_TOKEN_SECRET` |

Armazene esses valores com segurança. Você precisa deles em cada arquivo do App Builder `.env`.


## &#x200B;3. ADOBE DEVELOPER CONSOLE e APP BUILDER

* Acesso a uma organização da Adobe Developer Console
* Um **projeto App Builder** (novo ou um que você reutilize)
* Um espaço de trabalho configurado; os prompts presumem **[!UICONTROL Stage]**
* **[!UICONTROL Adobe I/O Events]** adicionado como um serviço ao espaço de trabalho
* **Commerce** conectado como provedor de eventos do espaço de trabalho

O código de evento usado na prova de conceito é: `com.adobe.commerce.observer.sales_order_place_before`

Se você não tiver conectado o Commerce como um provedor de eventos, consulte [Configurar o Commerce para emitir eventos para o Adobe I/O](https://developer.adobe.com/commerce/extensibility/events/configure-commerce/){target="_blank"} no guia de Extensibilidade do Commerce.


## &#x200B;4. Ambiente de desenvolvimento local

```bash
# Required versions
node --version    # 18.x or later
npm --version     # any recent version

# Adobe I/O CLI
npm install -g @adobe/aio-cli

# Authenticate
aio login

# Select your project and workspace
aio app use
# Confirm the org, project, and workspace shown are correct
```


## &#x200B;5. Dois diretórios de projeto a conhecer

Este tutorial usa duas raízes de diretório separadas. Mantenha-os separados.

**raiz do projeto Commerce** (seu repositório Git Magento):

```text
<commerce-root>/
└── app/code/Client/SplitPayment/   ← Module goes here
```

**Raiz do projeto do App Builder** (a pasta `split-payment-orchestrator` do pacote de origem ou um novo projeto que você cria):

```text
split-payment-orchestrator/
├── app.config.yaml
├── package.json
├── .env                            ← Copy from .env.example, then fill in
└── actions/
```


## &#x200B;6. entity_id comparada com increment_id

> **Sempre usar `entity_id` (a ID do banco de dados numérico), não `increment_id` (por exemplo `000000042`), em chamadas REST.**

Localizar `entity_id` da URL do pedido **[!UICONTROL Commerce Admin]**:

```text
/admin/sales/order/view/order_id/42/   →   entity_id = 42
```

Ou no script de simulação:

```bash
node scripts/simulate-split-payment.mjs show 42
```


## &#x200B;7. O limite de $100

A interface de usuário de pagamento dividido e a proteção de limite direcionam pedidos **$100.00 ou menos**. O fluxo se comporta da seguinte maneira:

* **A partir de US$ 100:** a interface de pagamento parcelado aparece; o cliente pode definir uma divisão de crédito de depósito com caixa
* **Acima de $100:** `CheckoutPlugin` lança um erro na etapa de pagamento

Para testar, crie um carrinho cujo subtotal, remessa e imposto sejam **menores ou iguais a US$ 100** (por exemplo, um produto abaixo de US$ 90, portanto, remessa e imposto ainda se encaixam no limite).

O limite é armazenado em:

* Configuração do Commerce: `split_payment/general/threshold` (padrão `100` em `etc/config.xml`)
* Ambiente do App Builder: `PAYMENT_THRESHOLD=100` (deve corresponder ao Commerce)


## &#x200B;8. Fastly (somente Commerce Cloud)

As ações do App Builder chamam o Commerce em REST (`/rest/V1/split-payment/orders/...`). Se o seu projeto do Commerce Cloud usar o Fastly com incluir na lista de permissões de IP, os endereços IP de saída em tempo de execução do App Builder deverão ser.

**Como verificar:** Execute primeiro o script de simulação (curl direto com assinatura OAuth). Se isso funcionar, mas a ação do App Builder retornar `403`, o Fastly provavelmente está bloqueando a solicitação.

Use a documentação atual do Adobe para intervalos de IP de saída do App Builder e adicione-os à sua configuração do Fastly, conforme necessário.


## Lista de verificação de verificação

Antes de iniciar os prompts de build, confirme o seguinte:

* [ A versão do Commerce ] é 2.4.5 ou posterior
* [ ] evento de E/S habilitado (Commerce Cloud) e implantado
* [ ] Pagamento na entrega habilitado com o título definido exatamente como `Cash`
* [ ] Crédito da loja habilitado
* [ ] O cliente de teste tem pelo menos US$ 50 de crédito de loja
* [ ] A integração do Commerce é criada e ativada, e todos os quatro valores OAuth são salvos
* [ ] O projeto do App Builder tem o serviço de Eventos de E/S e o provedor de eventos do Commerce configurados
* [ ] `aio login` está concluído e o espaço de trabalho correto está selecionado com `aio app use`
* [ ] Node.js 18 ou posterior está instalado e a CLI do `aio` está instalada
* [ ] `.env` arquivos são preparados por [POC de pagamento dividido: referência de variáveis de ambiente](./env-reference.md) (e seu pacote de origem, se você usar um)


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
