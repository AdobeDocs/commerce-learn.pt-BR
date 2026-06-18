---
title: POC de pagamento dividido — prompt do Commerce Module AI
description: Saiba como usar esse prompt para gerar Client_SplitPayment. REST, plug-ins, check-out do JavaScript, eventos de E/S e comandos enable, compile e deploy.
feature: App Builder, Backend Development, Eventing, Extensibility, Paas, REST, Orders
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 503
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# POC de pagamento dividido: prompt do Commerce Module AI

Use esta página para copiar o prompt completo que gera o módulo em andamento `Client_SplitPayment`: REST, manipulação de sessão, **[!UICONTROL Checkout]** e exibição **[!UICONTROL Admin]** para a prova de conceito do pagamento dividido. O fluxo de trabalho do operador permanece no App Builder.

## Como usar este prompt

Copie tudo de **PROMPT START** para **End of prompt** no Cursor (com Claude) ou diretamente no Claude. Execute-o a partir da raiz do seu projeto Commerce ou de um diretório em que a IA possa criar arquivos.

## Personalizar antes de executar

* Substitua `Client` pelo nome real do fornecedor.
* Altere `SplitPayment` se quiser um nome de módulo diferente.
* Se o site usar um tema personalizado, os caminhos XML do layout e RequireJS poderão precisar de alterações.
* Se o método **[!UICONTROL Cash on delivery]** usar um código diferente de `cashondelivery`, atualize `payment-method-helper.js`.


## O prompt

**INÍCIO DA SOLICITAÇÃO**

Você está gerando um módulo em andamento completo e pronto para produção do Adobe Commerce 2.4.5+ para um recurso de pagamento dividido. Este módulo é o adaptador PHP fino que expõe a superfície REST correta e anexa os dados corretos nos momentos certos no ciclo de vida do Commerce. Toda a lógica do fluxo de trabalho do operador reside no Adobe App Builder (não neste módulo).

**Identidade do módulo:**
* Fornecedor: `Client`
* Módulo: `SplitPayment`
* Nome completo: `Client_SplitPayment`
* Namespace: `Client\SplitPayment`
* Localização: `app/code/Client/SplitPayment/`
* Dependências: `Magento_Checkout`, `Magento_CustomerBalance`, `Magento_Sales`, `Magento_Quote`, `Magento_WebApi`, `Magento_AdobeCommerceEventsClient`

Gere cada arquivo listado na estrutura de arquivo abaixo. Não omita nenhum arquivo. Use `declare(strict_types=1)` em todos os arquivos PHP.


### Estrutura de arquivo a ser gerada

```
app/code/Client/SplitPayment/
├── registration.php
├── composer.json
├── Api/
│   ├── Data/SplitPaymentInterface.php
│   └── SplitPaymentManagementInterface.php
├── Block/
│   └── Order/SplitPaymentInfo.php
├── Controller/
│   └── Checkout/StoreCreditBalance.php
├── etc/
│   ├── acl.xml
│   ├── config.xml
│   ├── db_schema.xml
│   ├── db_schema_whitelist.json
│   ├── di.xml
│   ├── events.xml
│   ├── extension_attributes.xml
│   ├── io_events.xml
│   ├── module.xml
│   ├── webapi.xml
│   └── frontend/
│       └── routes.xml
├── Model/
│   ├── SplitPaymentData.php
│   ├── SplitPaymentManagement.php
│   ├── Service/
│   │   └── SplitInvoiceService.php
│   └── Session/
│       └── SplitPaymentSession.php
├── Observer/
│   ├── AutoInvoiceStoreCreditOnOrderPlace.php
│   └── CopySplitPaymentToOrder.php
├── Plugin/
│   ├── CheckoutPlugin.php
│   ├── OrderRepositoryPlugin.php
│   ├── PlaceOrderPlugin.php
│   ├── Adminhtml/
│   │   └── OrderPaymentPlugin.php
│   ├── Checkout/
│   │   └── LayoutProcessorPlugin.php
│   ├── CustomerBalance/
│   │   └── CapCustomerBalanceCollectPlugin.php
│   ├── Payment/
│   │   ├── Block/
│   │   │   └── AdminSplitPaymentTitlePlugin.php
│   │   └── Checks/
│   │       └── SplitPaymentZeroTotalPlugin.php
│   ├── Quote/
│   │   └── FixSplitPaymentGrandTotalPlugin.php
│   └── Sales/
│       └── FixInvoiceCustomerBalanceAfterTotalsPlugin.php
├── Setup/
│   └── Patch/
│       └── Data/
│           └── AddSplitPaymentOrderAttribute.php
└── view/
    └── frontend/
        ├── requirejs-config.js
        ├── layout/
        │   └── sales_order_view.xml
        ├── templates/
        │   └── order/
        │       └── split-payment-info.phtml
        └── web/
            ├── js/
            │   ├── model/
            │   │   └── payment-method-helper.js
            │   └── view/
            │       └── payment/
            │           ├── cashondelivery-method.js
            │           └── split-payment.js
            └── template/
                └── payment/
                    ├── cashondelivery.html
                    └── split-payment.html
```


### Especificações comportamentais

#### &#x200B;1. Esquema de Banco de Dados (`etc/db_schema.xml`)

Adicionar estas colunas a `sales_order` (recurso: `sales`):

| Coluna | Tipo | Anulável | Comentário |
|---|---|---|---|
| `split_store_credit_amount` | decimal(12,4) | sim | Parte de crédito da loja |
| `split_cash_amount` | decimal(12,4) | sim | Parte do pagamento à vista devida |
| `split_cash_status` | varchar(32) | sim | `pending` / `received` / `declined` |
| `split_sc_invoice_id` | int unsigned | sim | ID da entidade da fatura de crédito de armazenamento |
| `split_cash_invoice_id` | int unsigned | sim | ID da entidade da fatura de pagamento à vista |

Gere também o `db_schema_whitelist.json` para essas colunas.

#### &#x200B;2. Atributos de Extensão (`etc/extension_attributes.xml`)

Adicionar `split_store_credit_amount` (flutuante), `split_cash_amount` (flutuante), `split_cash_status` (cadeia de caracteres) a:
* `Magento\Quote\Api\Data\CartInterface`
* `Magento\Sales\Api\Data\OrderInterface`
* `Magento\Sales\Api\Data\OrderPaymentInterface`

#### &#x200B;3. Pontos de Extremidade REST (`etc/webapi.xml`)

```xml
POST /V1/split-payment/set              → anonymous (session-scoped)
POST /V1/split-payment/orders/:orderId/cash-received  → Magento_Sales::actions
POST /V1/split-payment/orders/:orderId/cash-decline   → Magento_Sales::cancel
```

Todos os três mapeiam para `Client\SplitPayment\Api\SplitPaymentManagementInterface`.

#### &#x200B;4. Eventos de E/S (`etc/io_events.xml`)

Inscrever-se em `observer.sales_order_place_before` e incluir campos:
`entity_id`, `quote_id`, `increment_id`, `subtotal`, `split_store_credit_amount`, `split_cash_amount`, `split_cash_status`

#### &#x200B;5. `SplitPaymentSession` — Wrapper de Sessões

Armazena valores divididos declarados na sessão de finalização. Deve expor:
* `setAmounts(float $storeCredit, float $cash): void`
* `getAmounts(): array` — retorna `['store_credit' => float, 'cash' => float]`
* `clear(): void`
* `beginBalanceApply(): void` — define um sinalizador que suprime o plug-in de correção de total geral durante a aplicação de crédito de armazenamento
* `endBalanceApply(): void`
* `isBalanceApplyInProgress(): bool`

#### &#x200B;6. `SplitPaymentManagement` — Controlador REST

**`setSplitPayment(float $storeCreditAmount, float $cashAmount, ?string $cartId = null): bool`**
* Valida se o carrinho pertence à sessão atual (comparando IDs de cotações numéricas e mascaradas)
* Armazena valores em `SplitPaymentSession`
* Retorna `true` em caso de sucesso; lança `LocalizedException` com mensagem genérica em caso de falha

**`markCashReceived(int $orderId): bool`**
* Carrega a ordem por `entity_id`
* Valida `split_cash_status === 'pending'`
* Define o status para `received`, estado para `processing`
* Adiciona um comentário de histórico: `"Cash payment of $X.XX received."`
* Chamadas `SplitInvoiceService::createCashPortionInvoice($orderId)`
* Adiciona um comentário com a ID de incremento da fatura à vista
* Chama `createShipmentIfPossible($orderId)` — cria uma remessa usando `ShipOrder::execute()` se houver itens entregáveis
* Retorna `true`; lança `LocalizedException` genérico em qualquer erro

**`markCashDeclined(int $orderId): bool`**
* Carrega a ordem
* Valida `split_cash_status === 'pending'`
* Valida `$order->canCancel()`
* Define o status para `declined`, adiciona o comentário: `"Cash payment declined (simulated fraud check)."`
* Salvar pedido
* Chamadas `OrderManagement::cancel($orderId)`
* Retorna `true`; lança `LocalizedException` genérico em caso de falha

#### &#x200B;7. `PlaceOrderPlugin` — aroundPlaceOrder em `QuoteManagement`

Este é o plug-in mais importante. Executa `aroundPlaceOrder`:

1. Carregar a cotação; se não estiver ativo, chamar `$proceed()` imediatamente
2. Ler `SplitPaymentSession::getAmounts()`
3. Se `customer_balance_amount_used > 0` estiver na citação, chamar `BalanceManagementInterface::remove($cartId)` (identificador `LocalizedException` — registrar e relançar como mensagem genérica)
4. Chamada `recollectQuoteForBalanceOperation()` — carrega aspas, chama `collectTotals()`, salva (em `beginBalanceApply()` / `endBalanceApply()` para suprimir o plug-in de correção de total geral)
5. Se `$storeCredit > 0`, chamar `BalanceManagementInterface::apply($cartId, $storeCredit)` (falha do identificador)
6. Recarregar cotação; definir atributos de extensão: `split_store_credit_amount`, `split_cash_amount`, `split_cash_status = 'pending'`
7. Salvar `payment->additional_information['client_split_payment']` como `['store_credit' => x, 'cash' => y]`
8. Salvar cotação
9. Chamar `$proceed()`, capturar ID da ordem
10. Ligar para `SplitPaymentSession::clear()`
11. ID da ordem de devolução

#### &#x200B;8. `CopySplitPaymentToOrder` — Observador em `sales_model_service_quote_submit_before`

Lê valores divididos de sessão → pagamento additional_information → atributos de extensão de cotação (nessa ordem de prioridade). Grava `split_store_credit_amount`, `split_cash_amount`, `split_cash_status = 'pending'` no objeto de ordem.

#### &#x200B;9. `AutoInvoiceStoreCreditOnOrderPlace` — Observador em `sales_order_place_after`

Após o posicionamento do pedido, se o pedido tiver um valor de crédito de armazenamento (`split_store_credit_amount > 0`), chame `SplitInvoiceService::createStoreCreditPortionInvoice($orderId)` para faturar imediatamente a parte de crédito de armazenamento.

#### 10. `SplitInvoiceService`

**`createStoreCreditPortionInvoice(int $orderId): ?int`**
Cria uma fatura somente para a parte de crédito da loja. Define `customer_balance_amount` na fatura para o valor de crédito da loja. Registra e salva a fatura. Retorna a ID de entidade da fatura ou nulo na falha (log; não relançar).

**`createCashPortionInvoice(int $orderId): ?int`**
Cria uma fatura para a porção de caixa (os itens/valores restantes da ordem não cobertos pela fatura SC). Registra e salva. Retorna a ID da entidade ou nulo em caso de falha.

#### &#x200B;11. `CheckoutPlugin` — em `PaymentInformationManagement`

Plug-in em `Magento\Checkout\Model\PaymentInformationManagement::savePaymentInformationAndPlaceOrder`. Antes de continuar:
* Carregar a cotação da sessão de finalização
* Obter o limite configurado: `Magento\Framework\App\Config\ScopeConfigInterface::getValue('split_payment/general/threshold')`, padrão `100`
* Se `$quote->getGrandTotal() > $threshold`, lançar `LocalizedException('Payment could not be processed. Please try again or contact support.')`

#### &#x200B;12. `CapCustomerBalanceCollectPlugin` — em `Customerbalance` total

Depois que a coleta de saldo total do cliente nativo for executada, limite de `customer_balance_amount_used` a `SplitPaymentSession::getAmounts()['store_credit']`. Isso evita que o Commerce aplique em excesso o saldo completo do cliente quando ele declarar uma parte menor de crédito da loja.

#### &#x200B;13. `FixSplitPaymentGrandTotalPlugin` — em `Quote\Address\Total\Grand`

Após a coleta do total geral: se existir uma sessão de pagamento parcelado e `isBalanceApplyInProgress()` for falso, defina o total geral da cotação para o valor em dinheiro da sessão. Isso faz com que a interface do usuário de check-out mostre apenas o que está vencido em dinheiro.

#### &#x200B;14. `FixInvoiceCustomerBalanceAfterTotalsPlugin` — em `Sales\Model\Order\Invoice`

Depois que os totais da fatura forem coletados, se a ordem associada da fatura tiver um `split_sc_invoice_id`, corrija o `customer_balance_amount` na fatura para evitar a aplicação dupla de crédito de loja.

#### &#x200B;15. `SplitPaymentZeroTotalPlugin` — em `Payment\Model\Checks\ZeroTotal`

Permitir pagamento de CQO quando `SplitPaymentSession::getAmounts()['cash'] > 0`, mesmo que o total geral da cotação seja $0 (porque o crédito da loja cobre a ordem inteira).

#### &#x200B;16. `LayoutProcessorPlugin` — em `Checkout\Block\Checkout\LayoutProcessor`

Depois que o layout for processado:
* Insira o componente `Client_SplitPayment/js/view/payment/split-payment` nos filhos `additional` do componente do método de pagamento `cashondelivery` em `components.checkout.children.steps.children.billing-step.children.payment.children.renders.children.offline-payments.children.cashondelivery.children.additional`
* Remover o componente da interface de usuário de crédito de loja nativa (`customerBalance`, `useStoreCredit`) da etapa de pagamento — o componente de pagamento dividido possui a exibição/aplicativo de crédito de loja

#### &#x200B;17. `OrderRepositoryPlugin` — em `OrderRepositoryInterface`

Depois de `get()` e `getList()`, hidratar os atributos de extensão do pedido das `sales_order` colunas simples (`split_store_credit_amount`, `split_cash_amount`, `split_cash_status`).

#### &#x200B;18. `AdminSplitPaymentTitlePlugin` — em `Payment\Block\Info`

Depois de `getTitle()` retornar, se o método de pagamento for `cashondelivery` e a ordem tiver um pagamento dividido, anexe `" (Split: Cash $X.XX + Store Credit $Y.YY)"` ao título.

#### &#x200B;19. `OrderPaymentPlugin` — em `Sales\Block\Adminhtml\Order\Payment`

Em `_beforeToHtml` ou via afterToHtml, anexe os detalhes do pagamento dividido (valor do pagamento à vista, valor do crédito da loja, status) ao bloco de pagamento HTML na exibição de ordem do Administrador do Commerce.

#### &#x200B;20. Controlador de Saldo de Crédito da Loja

`Controller/Checkout/StoreCreditBalance.php` — rota: `GET /splitpayment/checkout/storecreditbalance`

Retorna JSON: `{"balance": float, "logged_in": bool}`. Se o cliente não estiver conectado, retorna `{"balance": 0, "logged_in": false}`. Saldo de leitura de `Magento\CustomerBalance\Model\Balance`.

Registrar a rota de front-end em `etc/frontend/routes.xml` com `frontName="splitpayment"`.

#### &#x200B;21. Componente KnockoutJS de Check-out — `split-payment.js`

Um `uiComponent` que:
* Detecta quando o método de pagamento `cashondelivery` é selecionado (`quote.paymentMethod.subscribe`)
* Carrega o saldo de crédito da loja do cliente via `GET /splitpayment/checkout/storecreditbalance`
* Preenche previamente o campo de valor em dinheiro com o total completo do pedido (calculado a partir de `total_segments` excluindo `grand_total` e `customerbalance` — nunca usa `grand_total` diretamente, pois pode ser definido para o restante em dinheiro)
* À medida que o cliente altera a entrada do valor de caixa: calcula o crédito de armazenamento necessário = total do pedido - caixa; valida; lança em `POST /V1/split-payment/set`
* Mostra mensagens de validação para: dinheiro > total do pedido, crédito de armazenamento insuficiente, não conectado
* Mostra uma mensagem de sucesso quando uma divisão válida é inserida: `"The remaining $X.XX will automatically be applied from your store credit."`
* Redefine quando outro método de pagamento é selecionado (lança `{storeCreditAmount: 0, cashAmount: 0}` para limpar a sessão)

#### 22. `cashondelivery-method.js`

Estende `Magento_OfflinePayments/js/view/payment/offline-payments`. Usa `payment-method-helper.js` para detectar o código do método de pagamento à vista. Registra o componente `split-payment` em sua região `additional`.

#### 23. `payment-method-helper.js`

Utilitário retornando `getCashMethodCode()` — verifica `window.checkoutConfig.paymentMethods` para `cashondelivery`; retorna para `checkmo` se necessário.

#### &#x200B;24. `cashondelivery.html` Modelo

Modelo CQO padrão, mas inclui a região `<!-- ko foreach: getRegion('additional') -->` para que o componente filho do pagamento dividido possa ser renderizado.

#### &#x200B;25. `split-payment.html` Modelo

Modelo KnockoutJS para os campos de pagamento dividido:
* Exibição do saldo de crédito da loja disponível
* Entrada de valor de caixa (número, etapa 0,01)
* Exibição da parte de crédito da loja (somente leitura)
* Aplicar automaticamente a mensagem de crédito da loja (exibida quando a divisão é válida e o crédito da loja > 0)
* Mensagem de erro de validação

#### 26. `requirejs-config.js`

Mapas:
* `Client_SplitPayment/js/view/payment/split-payment` → o componente
* `Client_SplitPayment/js/view/payment/cashondelivery-method` → a substituição do COD
* `Client_SplitPayment/js/model/payment-method-helper` → o auxiliar

#### 27. `etc/config.xml`

Valores padrão de configuração do sistema:

```xml
<split_payment>
  <general>
    <threshold>100</threshold>
    <enabled>1</enabled>
  </general>
</split_payment>
```


### Notas de implementação críticas

**O aplicativo de crédito de armazenamento deve usar `BalanceManagementInterface`, não a manipulação de modelo direta.** `BalanceManagementInterface::apply()` manipula atentamente a sessão, a validação e o recálculo do carrinho.

**`PlaceOrderPlugin`deve usar `aroundPlaceOrder` (não `beforePlaceOrder`).** O crédito da loja deve ser aplicado enquanto o carrinho ainda está ativo, e isso deve ser garantido antes que `$proceed()` seja chamado.

**O padrão de sinalizador de sessão para `beginBalanceApply` / `endBalanceApply` é crítico.** Sem ele, `FixSplitPaymentGrandTotalPlugin` é executado durante `collectTotals()` dentro da operação de saldo e define o total geral como o restante do caixa, fazendo com que `BalanceManagementInterface::apply()` falhe ou limite o crédito.

**Nunca exponha detalhes de erros internos ao cliente.** Todos os blocos `catch` que superam para respostas REST devem lançar `LocalizedException('Payment could not be processed. Please try again or contact support.')`.

**`entity_id`é a ID numérica do banco de dados.** As chamadas REST do App Builder sempre usam `entity_id`, não `increment_id`.

**`SplitInvoiceService`deve capturar e registrar erros em vez de propagá-los.** A falha na criação da fatura não deve cancelar um pedido já feito — registre a falha e deixe que o administrador a manipule manualmente.


### Após gerar os arquivos

Execute estes comandos na raiz do projeto Commerce:

```bash
bin/magento module:enable Client_SplitPayment
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento setup:static-content:deploy -f
bin/magento cache:flush
```

### Fim da solicitação


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
