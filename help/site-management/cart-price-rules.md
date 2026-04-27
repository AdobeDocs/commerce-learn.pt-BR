---
title: Criar regras de preço do carrinho
description: Saiba como criar regras de preço do carrinho que aplicam descontos no carrinho de compras quando as condições definidas são atendidas.
doc-type: Tutorial
last-substantial-update: 2022-12-28T00:00:00.000Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: User
level: Beginner
duration: 353
jira: KT-17148
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
TQID: https://experienceleague.adobe.com/2gmoGQBVz2foQwnGJRlXzWF-OkNGZtiJkQWy0F-0utg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 701
ht-degree: 0%

---

# Criar regras de preço do carrinho

As regras de preço do carrinho aplicam descontos aos itens do carrinho de compras com base nas condições definidas. O desconto pode ser aplicado automaticamente quando as condições forem atendidas ou quando o cliente inserir um código de cupom válido. O desconto aparece no carrinho sob o subtotal. Você pode ativar ou desativar uma regra para uma temporada ou promoção alterando seu status e intervalo de datas.

## Para quem é este vídeo?

* Profissionais de marketing de comércio eletrônico
* Gerentes de sites

## Conteúdo de vídeo

* Crie regras de preço do carrinho e códigos de cupom opcionais.
* Veja como os descontos são exibidos no carrinho e para promoções.

>[!VIDEO](https://video.tv.adobe.com/v/343835?learn=on)

## Problemas de exibição de preços

Em alguns casos, cada item de linha deve mostrar o desconto aplicado, mas os valores exibidos podem não corresponder exatamente. Isso acontece quando uma regra de preço do carrinho aplica um desconto em vários produtos e a divisão não é dividida uniformemente em duas casas decimais.

>[!BEGINSHADEBOX]

Regra de preço do carrinho = desconto de 10% aplicado a 2 produtos no carrinho
Condição para a regra de preço entrar em vigor: o total de itens no carrinho é 2
As ações aplicam o percentual de desconto do preço do produto e esse valor de desconto é 10

Dois itens são adicionados ao carrinho, cada um custa US$ 19,95

Para obter o valor do desconto, multiplique o preço do produto vezes 0,1

19,95 x 0,1 = 1,995

Essa é a questão, temos 3 casas decimais, em vez de duas. Converter isso em dólares agora é um problema

>[!ENDSHADEBOX]

### A solução

Para o comerciante no Administrador, a abordagem mais clara é mostrar cada linha solicitada com seu desconto em dólares. Para manter o total do pedido correto, arredonde o primeiro item de linha para cima e solte o terceiro decimal nos itens de linha restantes. Analise este cenário:

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor
Adicione 2 produtos ao carrinho com 19,95

Cada produto deve receber US$ 1.995 em descontos
Produto 1 - 19,95 x 0,1 = 1,995
2 - 19,95 x 0,1 = 1,995

Um total geral de 3,99 é fornecido como um desconto para o cliente

Ao exibir os itens de linha para o proprietário da loja no administrador,
precisamos ajustar o primeiro item e arredondá-lo para 2.000. Para o segundo item, solte o terceiro decimal.
Produto 1 = 2,00
Produto 2 = 1,99

O desconto total dos dois produtos agora quando somados corresponde ao desconto real fornecido a um cliente.
>[!ENDSHADEBOX]

Esta é uma captura de tela, como mostraria o administrador para um pedido que tem este cenário:

![Modo de exibição de administrador mostrando itens ordenados com valores diferentes](../assets/commerce-admin-cart-price-rule-values-different.png)

### Outras soluções possíveis e por que elas não foram usadas

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor
Adicione 2 produtos ao carrinho com 19,95

Cada produto deve receber US$ 1.995 em descontos,
no entanto, se os juntarmos, isso mostra desconto demais.

Produto 1 - 19,95 x 0,1 = 1,995
Produto 2 - 19,95 x 0,1 = 1,995

Converter para arredondar todos os itens
Produto 1 O novo valor é 2,00
O novo valor do Produto 2 é 2,00

Um total geral de 3,99 foi efetivamente fornecido como um desconto para o cliente,
no entanto, se juntarmos tudo, isso mostraria que foram dados US$ 4,00, e isso é incorreto.

2.00 + 2.00 = $4.00

>[!ENDSHADEBOX]

Problema semelhante se a terceira casa decimal fosse descartada para todos os itens, mostraria muito pouco desconto fornecido.

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor
Adicione 2 produtos ao carrinho com 19,95

Cada produto deve receber US$ 1.995 em descontos. No entanto, se apenas descermos o terceiro decimal, isso acontece:
Produto 1 - 19,95 x 0,1 = 1,995
Produto 2 - 19,95 x 0,1 = 1,995

Converter para eliminar o terceiro decimal para todos os itens
Produto 1 O novo valor é 1,99
O novo valor do Produto 2 é 1,99

Um total geral de 3,99 foi efetivamente fornecido como um desconto para o cliente,
no entanto, se descermos o terceiro decimal, isso mostraria que $3,98 foi dado, e isso está incorreto.

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]

## Recursos adicionais

* [Criar uma regra de preço do carrinho - [!DNL Commerce] Guia de merchandising e promoções](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html){target="_blank"}
* [Códigos de cupom - [!DNL Commerce] Guia de merchandising e promoções](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html){target="_blank"}
