---
title: Criar uma regra de preço do carrinho
description: Saiba como criar regras de preço do carrinho que aplicam descontos no carrinho com base em um conjunto de condições.
doc-type: feature video
audience: all
activity: use
last-substantial-update: 2022-12-28T00:00:00Z
feature: Configuration, System, Customers, Shopping Cart
topic: Commerce, Administration
role: Admin, Leader, User
level: Beginner, Intermediate
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: 273119420a7051b1833d9b796bdce36e17d893c7
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Criar uma regra de preço do carrinho

As regras de preço do carrinho aplicam descontos aos itens do carrinho de compras, com base em um conjunto de condições. O desconto pode ser aplicado automaticamente quando as condições forem atendidas ou quando o cliente inserir um código de cupom válido. Quando aplicado, o desconto é exibido no carrinho abaixo do subtotal. Uma regra de preço do carrinho pode ser usada conforme necessário para uma temporada ou promoção, alterando seu status e intervalo de datas.

## Para quem é este vídeo?

- Profissionais de marketing de comércio eletrônico
- Gerentes de sites

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/343835?quality=12&learn=on)

## Problemas de exibição de preços

Há alguns cenários exclusivos que exigem que cada item de linha exiba seu desconto fornecido, mas os valores podem não corresponder exatamente. O motivo é quando um desconto de regra de preço do carrinho é aplicado a vários produtos, mas os valores não são divididos uniformemente em duas casas decimais.

>[!BEGINSHADEBOX]

Regra de Preço do Carrinho = Desconto de 10% aplicado a 2 produtos no carrinho Condição para a regra de preço entrar em vigor: o total de itens no carrinho é 2 Ações aplicam percentual de desconto de preço do produto e a quantia de desconto é 10

Dois itens são adicionados ao carrinho, cada um custa US$ 19,95

Para obter o valor do desconto, multiplique o preço do produto vezes 0,1

19,95 x 0,1 = 1,995

Essa é a questão, temos 3 casas decimais, em vez de duas. Converter isso em dólares agora é um problema

>[!ENDSHADEBOX]

### A solução

Pensando no proprietário do site, que é a única pessoa afetada por esse problema, foi determinado que mostrar cada item solicitado com o desconto fornecido em dólares era o mais apropriado. Para garantir que todo o valor do pedido fosse calculado corretamente, decidiu-se arredondar o primeiro item e os outros baixariam a terceira casa decimal. Analise este cenário:

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve receber US$ 1,995 em descontos Produto 1 - 19,95 x 0,1 = 1,995 2 - 19,95 x 0,1 = 1,995

Um total geral de 3,99 é fornecido como um desconto para o cliente

Ao exibir os itens de linha para o proprietário da loja no administrador, precisamos ajustar o primeiro item e arredondá-lo para 2.000. Os segundos itens são eliminados na terceira casa decimal Produto 1 = 2,00 Produto 2 = 1,99

O desconto total dos dois produtos agora quando somados correspondem ao desconto real fornecido a um cliente.
>[!ENDSHADEBOX]

Esta é uma captura de tela, como mostraria o administrador para um pedido que tem este cenário:

![Exibição do administrador mostrando itens solicitados com valores diferentes](../assets/commerce-admin-cart-price-rule-values-different.png)

### Outras soluções possíveis e por que elas não foram usadas

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve obter $1.995 em descontos, no entanto, se nós apenas reuni-los, mostra muito desconto.

Produto 1 - 19,95 x 0,1 = 1,995 Produto 2 - 19,95 x 0,1 = 1,995

Converter para arredondar todos os itens Produto 1 O novo valor é 2,00 Produto 2 O novo valor é 2,00

Um total geral de 3,99 foi realmente fornecido como um desconto para o cliente, no entanto, se arredondarmos para cima, mostraria que $4,00 foi dado, e isso é incorreto.

2.00 + 2.00 = $4.00

>[!ENDSHADEBOX]

Problema semelhante se a terceira casa decimal fosse descartada para todos os itens, mostraria muito pouco desconto fornecido.

>[!BEGINSHADEBOX]

Mesmo desconto de 10% como acima da regra do carrinho em vigor Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve receber US$ 1,995 em descontos. No entanto, se apenas descermos o terceiro decimal, isso acontece: Produto 1 - 19,95 x 0,1 = 1,995 Produto 2 - 19,95 x 0,1 = 1,995

Converta para soltar o terceiro decimal para todos os itens Produto 1 O novo valor é 1,99 Produto 2 O novo valor é 1,99

Um total geral de 3,99 foi fornecido como um desconto para o cliente, no entanto, se descermos a terceira casa decimal, isso mostraria que US$ 3,98 foi fornecido, e isso está incorreto.

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]


## Recursos adicionais

- [Criar uma regra de preço do carrinho - [!DNL Commerce] Guia de merchandising e promoções](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html)
- [Códigos de cupom - [!DNL Commerce] Guia de merchandising e promoções](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html)
