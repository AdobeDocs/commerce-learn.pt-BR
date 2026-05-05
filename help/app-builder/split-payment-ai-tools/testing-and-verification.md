---
title: 'POC de pagamento dividido: guia de teste e verificação'
description: Saiba como verificar a POC de pagamento fracionado. Instalação do Commerce, REST, check-out, limite, aceitação e recusa da simulação, painel de demonstração e logs do App Builder.
feature: App Builder, Configuration, Extensibility, Paas, Payments, REST, Orders
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 359
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 8dfbf2694378aae76c91afa11bfee7d93077d8ba
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# POC de pagamento dividido: guia de teste e verificação

Este guia orienta você na verificação de que cada componente funciona corretamente, na ordem em que devem ser testados. Comece de baixo (módulo Commerce) e trabalhe acima (App Builder).


## Etapa 1 — Verificar a instalação do módulo Commerce

Após executar `bin/magento setup:upgrade` e `bin/magento setup:di:compile`:

```bash
# Confirm module is enabled
bin/magento module:status Client_SplitPayment

# Confirm db_schema columns were added
bin/magento doctrine:schema:validate
# or check directly:
mysql -u <user> -p <dbname> -e "DESCRIBE sales_order;" | grep split
```

Saída esperada: quatro colunas começando com `split_` visíveis em `sales_order`.


## Etapa 2 — Verificar a configuração de administração do Commerce

No Commerce Admin:
1. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Sales]** > **[!UICONTROL Payment Methods]** — confirmar se **[!UICONTROL Cash On Delivery]** está habilitado com o título `Cash`
2. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Customers]** > **[!UICONTROL Customer Configuration]** > **[!UICONTROL Store Credit Options]** — confirmação habilitada
3. Confirme se o cliente de teste tem crédito de loja: **[!UICONTROL Customers]** > **[!UICONTROL All Customers]** > *[cliente]* > **[!UICONTROL Store Credit]**


## Etapa 3 — Verificar se os pontos de extremidade REST estão acessíveis

Use curl para confirmar a resposta dos endpoints (eles rejeitarão solicitações não autorizadas, mas um 401 confirma que foram roteados corretamente):

```bash
# Should return 401 (not 404) — endpoint exists but requires auth
curl -X POST https://your-store.example.com/rest/V1/split-payment/orders/1/cash-received

# Should return 200 or session-based response — anonymous endpoint
curl -X POST https://your-store.example.com/rest/V1/split-payment/set \
  -H "Content-Type: application/json" \
  -d '{"storeCreditAmount": 0, "cashAmount": 0}'
```


## Etapa 4 — testar a interface do usuário de check-out

1. Faça logon na loja como cliente de teste (que tem crédito na loja)
2. Adicionar um produto ao carrinho (total abaixo de US$ 100 após o envio + imposto)
3. Prosseguir para o check-out
4. Na etapa de pagamento, selecione **Dinheiro** (ou Dinheiro na Entrega)
5. Verifique se os campos de pagamento parcelado são exibidos:
   * Seu saldo de crédito de loja mostrado
   * Campo de valor do pagamento à vista pré-preenchido com o total do pedido
   * O campo &quot;Armazenar crédito para este pedido&quot; mostra US$ 0,00 (já que dinheiro = total completo do pedido)
6. Reduzir o valor do caixa (por exemplo, insira $10 para uma ordem de $50)
7. Verifique se a parte de crédito da loja está atualizada para US$ 40,00
8. Verifique se a mensagem é exibida: `"The remaining $40.00 will automatically be applied from your store credit."`

**Validação de teste:**
* Inserir um valor de pagamento à vista maior que o total da ordem → mensagem de erro
* Insira um valor de caixa que exija mais crédito de armazenamento do que o disponível → mensagem de erro
* Inserir caixa = 0 → erro (ou armazenar crédito cobre toda a ordem)


## Etapa 5 — Testar proteção de limiar

1. Adicionar produtos totalizando mais de US$ 100 (subtotal + envio + imposto > US$ 100)
2. Prossiga para o check-out, selecione **Caixa**
3. Tentar colocar o pedido
4. Verifique se a mensagem de erro aparece: `"Payment could not be processed. Please try again or contact support."`
5. Verifique se o carrinho está preservado (o cliente ainda pode ajustar o carrinho e tentar novamente)


## Etapa 6 — Colocar uma Ordem de Pagamento de Divisão de Teste

1. Criar um carrinho abaixo de US$ 100 (conectado ao cliente com crédito da loja)
2. Selecionar Caixa no check-out
3. Insira um valor de caixa menor que o total da ordem (por exemplo, US$ 10 de uma ordem de US$ 45)
4. Confirmar se a mensagem de crédito da loja é exibida
5. Clique em **Fazer pedido**

Após o envio do pedido, verifique no Commerce Admin:
* A ordem está no status `pending_payment`
* O pedido tem dois comentários de histórico:
   1. `"Cash payment of $X.XX pending. Awaiting admin confirmation."` (do App Builder `payment-orchestrator`)
   2. `"Split payment orchestration completed. Order awaiting cash confirmation."` (do App Builder)
* Os valores do pagamento parcelado estão visíveis no bloco de pagamento da ordem

> **Se nenhum comentário do App Builder for exibido:** Verifique os logs de ação do App Builder com `aio app logs`. O evento pode não ter sido acionado ou a ação pode ter um erro.


## Etapa 7 — Testar aceitação por meio do script de simulação

O script de simulação é a maneira mais rápida de testar o fluxo de aceitação/recusa sem a interface completa do operador.

```bash
cd commerce-checkout-starter-kit
cp commerce-backend-ui-1/.env.simulation.example commerce-backend-ui-1/.env.simulation
# Edit .env.simulation with your credentials

# List recent orders (find your test order entity_id)
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs list

# Show split payment fields for a specific order
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs show 42

# Accept the cash payment
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs accept 42
```

Depois de aceitar, verifique na exibição da ordem do administrador do Commerce:
* O status do pedido é `processing`
* Comentário do histórico: `"Cash payment of $X.XX received."`
* NFF de caixa criada (visível na guia NFFs)
* Entrega criada (visível na guia Entregas, se aplicável)
* Comentário do histórico: `"Split payment: cash portion invoiced #XXXXXXXX."`
* Comentário do histórico: `"Split payment: shipment created after cash was accepted (App Builder / API)."`


## Etapa 8 — Rejeição do teste por meio do script de simulação

Coloque outra ordem de teste (mesma configuração da Etapa 6) e:

```bash
node commerce-backend-ui-1/scripts/simulate-split-payment.mjs decline <orderId>
```

Depois de recusar, verifique no Commerce Admin:
* O status do pedido é `canceled`
* Comentário do histórico: `"Cash payment declined (simulated fraud check)."`
* `split_cash_status` = `declined`


## Etapa 9 — testar o painel de demonstração

Depois de implantar o `split-payment-orchestrator`, `aio app deploy` imprime as URLs de ação.

Abra a URL `demo-dashboard` em um navegador:

```
https://[runtime-host]/api/v1/web/split_payment_orchestrator/demo-dashboard
```

Se `DEMO_UI_SECRET` estiver definido:

```
https://[runtime-host]/api/v1/web/split_payment_orchestrator/demo-dashboard?secret=<your-secret>
```

Com um pedido pendente:
1. O painel deve mostrar a ordem na lista pendente
2. Clique em **Aceitar** → a ordem deve ser movida para `processing` no Commerce
3. Faça outro pedido; clique em **Recusar** → a ordem deve ser `canceled` no Commerce


## Etapa 10 — Testar logs de ação do App Builder

```bash
# Follow logs in real-time
aio app logs --tail

# Or view last invocations
aio runtime activation list --limit 10
aio runtime activation logs <activation-id>
```

Para o `payment-orchestrator`, procure por:

```
[INFO] Split payment orchestration finished { orderId: '42' }
```

Para `payment-accept` ou `payment-decline`:

```
[INFO] Cash payment accepted on Commerce via REST { orderId: '42' }
```


## Problemas comuns e correções

### &quot;A assinatura é inválida&quot; do Commerce OAuth

**Causa:** Desvio de relógio entre o tempo de execução do App Builder e o Commerce ou um erro de assinatura OAuth.

**Correção:**
* Confirmar se `COMMERCE_BASE_URL` não tem barra à direita
* Confirme se as quatro credenciais do OAuth são para uma integração _ativada_
* Testar com o script de simulação primeiro — se o script funcionar, mas o App Builder não, é provável que uma variável env não esteja carregada (verifique se há variáveis env ausentes na saída `aio app deploy`)

### Campos de pagamento dividido não aparecem no check-out

**Causa:** os caminhos de injeção de LayoutProcessorPlugin não correspondem ao layout de check-out.

**Correção:**
* Verifique o console do navegador em busca de erros RequireJS ao carregar `Client_SplitPayment/js/view/payment/split-payment`
* Verificação `bin/magento setup:static-content:deploy` concluída com êxito
* Liberar cache: `bin/magento cache:flush`
* Se o tema tiver um check-out personalizado, o caminho `LayoutProcessorPlugin` para inserir o componente pode precisar de ajuste

### O crédito da loja não está sendo aplicado / &quot;O pagamento não pôde ser processado&quot; na ordem de colocação

**Causa:** Geralmente, um dos plug-ins de caso de borda não está funcionando corretamente.

**Verificar:**
1. `SplitPaymentSession` está retornando os valores corretos? Adicionar log de depuração temporário em `PlaceOrderPlugin`
2. `FixSplitPaymentGrandTotalPlugin` está em execução e afetando o total da cotação antes que `BalanceManagementInterface::apply()` seja chamado? O sinalizador `beginBalanceApply()` deve suprimi-lo.
3. O módulo de saldo do cliente está ativado no Commerce?

### A ação do App Builder recebe o evento, mas orderId está ausente

**Causa:** a lista de campos `io_events.xml` não inclui `entity_id` ou a forma de carga do evento foi alterada.

**Correção:**
* Confirmar se `io_events.xml` inclui `entity_id` na lista de campos
* Na ação, registre `JSON.stringify(params)` temporariamente para ver a forma de carga completa
* Verifique se a função `extractValue()` está encontrando o nível de aninhamento correto

### Os pedidos não são exibidos no painel de demonstração

**Causa:** os critérios de pesquisa REST do Commerce `orders` não retornam pedidos ou o campo `split_cash_status` não está na resposta REST.

**Correção:**
* Confirmar se `OrderRepositoryPlugin` está carregando atributos de extensão corretamente
* Testar diretamente: `GET /rest/V1/orders?searchCriteria[pageSize]=5` e verificar se `extension_attributes.split_cash_status` aparece na resposta
* Verifique se `extension_attributes.xml` está declarando corretamente o atributo `split_cash_status` em `OrderInterface`


## Lista de verificação de verificação

* [ ] `split_*` colunas visíveis na tabela `sales_order`
* [ ] pontos de extremidade REST retornam 401 (não 404) quando chamados sem autenticação
* [ ] A interface do usuário para pagamento dividido é renderizada no check-out quando Dinheiro está selecionado
* [ ] As mensagens de validação funcionam (pagamento a maior, crédito insuficiente)
* [ ] A proteção de limite bloqueia pedidos > US$ 100
* [ ] O pedido feito tem o status `pending_payment` e comentários do App Builder
* [ ] `simulate-split-payment.mjs list` mostra a ordem de teste com valores divididos
* [ ] `simulate-split-payment.mjs accept <id>` move a ordem para `processing` com fatura e remessa
* [ ] `simulate-split-payment.mjs decline <id>` cancela o pedido
* [ O painel de demonstração ] lista pedidos pendentes e aceita/recusa o trabalho da interface do usuário


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
