---
title: POC de pagamento dividido — decisões de arquitetura e design
description: Saiba como o POC de pagamento dividido mapeia a finalização da sincronização com a Commerce e as etapas orientadas por E/S para a App Builder, com atributos de extensão, REST e cinco casos de borda de plug-in.
feature: App Builder, Eventing, Extensibility, Paas, Payments, REST
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, User
level: Intermediate
doc-type: Tutorial
duration: 293
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 1%

---

# POC de pagamento dividido: decisões de arquitetura e design

Esta página explica as escolhas arquitetônicas por trás da prova de conceito do pagamento dividido. Leia-o antes de usar os prompts de build desta série para entender como cada componente está estruturado e como adaptar os padrões no seu próprio projeto.

## Princípio fundamental

A prova de conceito não é sobre a implementação de pagamento dividido mais elegante. Trata-se de mostrar **como começar a mover a lógica do Commerce para o App Builder sem uma regravação big bang**.

A regra aplicada em todo o é:

> **Se algo precisar ser executado de forma síncrona no ciclo de solicitações do Commerce, ou precisar invocar APIs internas da Commerce que não tenham superfície externa limpa, ele permanecerá no PHP. Todo o resto é movido para o App Builder.**

## O que existe no Commerce (PHP) e por quê

### &#x200B;1. Aplicativo de crédito de armazenamento: `PlaceOrderPlugin`

O crédito de armazenamento é aplicado ao carrinho usando `Magento\CustomerBalance\Api\BalanceManagementInterface::apply()`. Este método só funciona em um carrinho **ativo**. O carrinho fica inativo no momento em que o pedido é feito. A App Builder recebe o evento de E/S *depois* de o pedido ser feito, portanto, não é possível aplicar crédito de loja da App Builder.

**A lição:** tudo o que precisar mudar o estado do carrinho antes de fazer pedidos deve ser executado no Commerce. Não há solução alternativa.

### &#x200B;2. Proteção de limite síncrona: `CheckoutPlugin`

A verificação de limite de pedido de $100 deve bloquear o cliente na etapa de pagamento, antes que ele selecione **[!UICONTROL Place Order]**. A resposta deve ser síncrona no ciclo de solicitação do Commerce. O App Builder é orientado por eventos e assíncrono, portanto, não pode retornar um erro imediato nesse momento.

O App Builder *also* valida o limite (como uma auditoria), mas a experiência do cliente depende da execução da verificação do Commerce primeiro.

### &#x200B;3. Pontos de extremidade REST personalizados: `webapi.xml` e `SplitPaymentManagement`

Os seguintes endpoints devem:

* Invocar `SplitInvoiceService` (faturas que usam o serviço de fatura interna da Commerce)
* Chamar `ShipOrder::execute()` (serviço de remessa interna da Commerce)
* Atualizar o estado e o status do pedido com a máquina de estado do pedido da Commerce

`/V1/split-payment/orders/:id/cash-received` e `/V1/split-payment/orders/:id/cash-decline`

Não há camada REST pública limpa para esse comportamento, portanto, o Commerce expõe os endpoints. O App Builder as chama de.

### &#x200B;4. Dividir os valores por cotação e por ordem: observadores e plugins

O Commerce precisa dos valores divididos (`split_store_credit_amount`, `split_cash_amount`, `split_cash_status`) no pedido, tanto para as respostas REST lidas pelo App Builder quanto para a exibição de pedido **[!UICONTROL Admin]**. Os valores são anexados com atributos de extensão e são copiados da citação para a ordem em um observador em `sales_model_service_quote_submit_before`.

## O que está no App Builder e por quê

### &#x200B;1. Processamento de pedido orientado por evento: `payment-orchestrator`

Depois que `sales_order_place_before` for acionado, a App Builder receberá o evento. Ele revalida o limite (como uma auditoria), registra um comentário de *dinheiro pendente* no pedido e atualiza o status do pedido. Nada disso requer PHP novo, apenas REST de volta para Commerce.

### &#x200B;2. Aceitação de dinheiro: `payment-accept`

Quando um ERP (ou um operador no painel) confirma que o dinheiro foi recebido, `payment-accept` chama `POST /V1/split-payment/orders/:id/cash-received`. A fatura, a remessa e o status do pedido são tratados no Commerce. O acionador é o App Builder.

### &#x200B;3. Recusa em dinheiro: `payment-decline`

`payment-decline` chama `POST /V1/split-payment/orders/:id/cash-decline` e o Commerce cancela o pedido. Mesmo padrão que a aceitação de caixa.

### &#x200B;4. Painel do operador: `demo-dashboard`

Um painel do HTML independente veiculado a partir de uma ação da Web do App Builder. Ele busca pedidos que estão aguardando dinheiro do Commerce REST e fornece **[!UICONTROL Accept]** / **[!UICONTROL Decline]** ações que chamam as ações do App Builder acima. O Commerce **[!UICONTROL Admin]** não é necessário.

## O limite: aplicado duas vezes de propósito

```text
Customer at checkout
        |
        v
[Commerce: CheckoutPlugin]     <- Synchronous, blocks immediately, user sees error
        |
        |  (if somehow bypassed: direct API call, and so on)
        v
[Order placed] -> I/O Event -> [App Builder: payment-orchestrator]
                                        |
                                        v
                              [evaluateThreshold()]  <- Async audit, records failure comment
```

**A Commerce é proprietária da proteção voltada para o usuário; a App Builder é proprietária da auditoria de pós-posicionamento.** Isso é intencional.

## O crédito da loja: por que ele fica no PHP

```text
What you might think would work (it does not):
  Order placed -> I/O Event -> App Builder -> PUT /V1/carts/:id/store-credit
  (Fails: cart is inactive after place order)

What actually works:
  AroundPlaceOrder plugin
  -> BalanceManagementInterface::apply($cartId, $amount)  <- cart is still active
  -> place order
  -> order placed
  -> I/O event: App Builder (store credit is already applied)
```

O arquivo `store-credit.js` no orquestrador documenta isso. É um stub no-op com comentários que explicam por que não é usado.

## Atributos de extensão: a cola

As quantidades divididas são movidas pelo sistema em atributos de extensão:

```text
Checkout JavaScript (Knockout)
    |  POST /V1/split-payment/set
    v
SplitPaymentSession (PHP session)
    |  AroundPlaceOrder reads the session
    v
CartInterface extension attributes
    |  `sales_model_service_quote_submit_before` observer
    v
OrderInterface extension attributes -> `sales_order` flat columns
    |  I/O event payload includes these fields
    v
App Builder `payment-orchestrator` reads the split amounts
```

## Modelo de dados

**`sales_order`colunas simples que este módulo adiciona**

| Coluna | Tipo | Finalidade |
| --- | --- | --- |
| `split_store_credit_amount` | flutuante | Crédito de armazenamento aplicado |
| `split_cash_amount` | flutuante | Valor do pagamento à vista devido |
| `split_cash_status` | varchar | `pending`, `received` ou `declined` |
| `split_sc_invoice_id` | int | ID da entidade da fatura de crédito de armazenamento |
| `split_cash_invoice_id` | int | ID da entidade da fatura de pagamento à vista |

**Atributos de extensão** (em `CartInterface`, `OrderInterface` e `OrderPaymentInterface`)

* `split_store_credit_amount` (flutuante)
* `split_cash_amount` (flutuante)
* `split_cash_status` (cadeia de caracteres)

## Campos de carga útil do evento de E/S

`observer.sales_order_place_before` está configurado em `io_events.xml` para incluir o seguinte no evento:

```xml
entity_id, quote_id, increment_id, subtotal,
split_store_credit_amount, split_cash_amount, split_cash_status
```

A App Builder usa `entity_id` como a ID do pedido e `split_store_credit_amount` e `split_cash_amount` para validação de limite.

## Os cinco casos de borda que a prova de conceito cobre

### 1. `CapCustomerBalanceCollectPlugin`

O coletor total **[!UICONTROL Customer balance]** nativo do Commerce pode aplicar em excesso (pode ver o saldo disponível completo, não o valor de divisão declarado pela sessão). Este plug-in limita a quantidade ao valor declarado na sessão.

### 2. `FixSplitPaymentGrandTotalPlugin`

Depois que o crédito de armazenamento é aplicado, a cotação **[!UICONTROL Grand Total]** pode cair somente para o valor de caixa. A JavaScript de check-out deve calcular o total do pedido para validação de divisão *antes* dessa alteração. O plug-in é executado após a coleta de totais e corrige a exibição, enquanto o JavaScript não confia em `grand_total` sozinho e reconstrói o valor a partir de segmentos de subtotal.

### 3. `FixInvoiceCustomerBalanceAfterTotalsPlugin`

Quando os totais da fatura são recuperados, o crédito da loja pode ser aplicado duas vezes. Este plug-in corrige `customer_balance_amount` nas faturas.

### 4. `SplitPaymentZeroTotalPlugin`

Depois que o crédito de armazenamento é aplicado, o carrinho **[!UICONTROL Grand Total]** pode ser de $0 (ordem de crédito de armazenamento completa). A verificação **[!UICONTROL Zero subtotal checkout]** da Commerce pode bloquear o COD nesse caso. Este plug-in permite o COD quando o valor do dinheiro da sessão é maior que 0.

### &#x200B;5. Lembrança de cotação antes de `BalanceManagementInterface::apply()`

`apply()` verifica o valor em relação ao **[!UICONTROL Grand Total]** atual. Se o total já for apenas a parte de caixa, `apply()` pode falhar ou atingir. `PlaceOrderPlugin` suspende temporariamente a correção de total geral enquanto o saldo é aplicado, usando um sinalizador de sessão (`beginBalanceApply` / `endBalanceApply`).


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
