---
title: Criar uma regra de preço do carrinho
description: Saiba como criar regras de preço do carrinho que aplicam descontos no carrinho de compras com base em um conjunto de condições.
doc-type: feature video
audience: all
role: Admin, User
activity: use
exl-id: ae8cab73-8a8b-4266-8205-b7397633e9bf
source-git-commit: 3ee6eae696d33ce792beabdf91c584e039ab3b54
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Criar uma regra de preço do carrinho

As regras de preço do carrinho aplicam descontos a itens no carrinho de compras, com base em um conjunto de condições. O desconto pode ser aplicado automaticamente quando as condições são atendidas, ou quando o cliente insere um código de cupom válido. Quando aplicado, o desconto é exibido no carrinho sob o subtotal. Uma regra de preço do carrinho pode ser usada conforme necessário para uma temporada ou promoção alterando seu status e intervalo de datas.

## Para quem é este vídeo?

- Comerciantes de eCommerce
- Gestores do site

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/343835?quality=12&learn=on)

## Problemas de exibição de preços

Há alguns cenários exclusivos que exigem que cada item de linha exiba seu desconto fornecido, mas os valores podem não corresponder exatamente. O motivo é quando um desconto de regra de preço do carrinho é aplicado a vários produtos, mas os valores não são divididos uniformemente em duas casas decimais.

>[!BEGINSHADEBOX]

Regra de preço do carrinho = desconto de 10% aplicado a 2 produtos na condição do carrinho para que a regra de preço entre em vigor: o total de itens no carrinho é 2. As ações aplicam a porcentagem do desconto do preço do produto e essa quantia de desconto é 10

2 itens são adicionados ao carrinho, cada um é de US$ 19,95

Para obter a quantia de desconto, multiplique o tempo de preço do produto 0.1

19,95 x 0,1 = 1,995

Esse é o problema, temos 3 casas decimais, em vez de duas. Converter isso em dólares agora é um problema

>[!ENDSHADEBOX]

### A solução

Pensando no proprietário do site, que é a única pessoa afetada por esse problema, foi determinado que mostrar cada item solicitado com o desconto fornecido em dólares era o mais apropriado. Para garantir que todo o valor do pedido seja calculado corretamente, foi decidido arredondar o primeiro item e os outros soltarem o terceiro decimal. Revise este cenário:

>[!BEGINSHADEBOX]

Mesmo desconto de 10% que a regra de carrinho acima na verdade Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve receber US$ 1,995 em descontos Produto 1 - 19,95 x 0,1 = 1,995 2 - 19,95 x 0,1 = 1,995

Um total geral de 3,99 é fornecido como um desconto ao cliente

Ao exibir os itens de linha para o proprietário da loja no administrador, precisamos ajustar o primeiro item e arredondar para 2.000. Os segundos itens que soltamos o terceiro Produto decimal 1 = 2.00 Produto 2 = 1.99

O desconto total dos dois produtos agora, quando somados, corresponde ao desconto real fornecido a um cliente.
>[!ENDSHADEBOX]

Esta é uma captura de tela como ela mostraria no administrador para um pedido que tem este cenário:

![Exibição de administrador mostrando itens ordenados com valores diferentes](../assets/commerce-admin-cart-price-rule-values-different.png)

### Outras soluções potenciais e por que não foram utilizadas

>[!BEGINSHADEBOX]

Mesmo desconto de 10% que a regra de carrinho acima na verdade Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve receber US$ 1,995 em descontos, no entanto, se apenas os arredondarmos, ele mostrará muito desconto.

Produto 1 - 19,95 x 0,1 = 1,995 Produto 2 - 19,95 x 0,1 = 1,995

Converter para arredondar todos os itens Produto 1 O novo valor é 2.00 Produto 2 O novo valor é 2.00

Na verdade, um total geral de 3,99 foi fornecido como um desconto ao cliente, no entanto, se formos arredondados, isso mostraria que foram dados 4,00 dólares, o que está incorreto.

2.00 + 2.00 = $4.00

>[!ENDSHADEBOX]

Problema semelhante se a terceira casa decimal fosse solta para todos os itens, ele mostraria muito pouco desconto fornecido.

>[!BEGINSHADEBOX]

Mesmo desconto de 10% que a regra de carrinho acima na verdade Adicione 2 produtos ao carrinho que são 19,95

Cada produto deve receber US$ 1,995 em descontos, no entanto, se apenas soltarmos o terceiro decimal, isso acontece: Produto 1 - 19,95 x 0,1 = 1,995 Produto 2 - 19,95 x 0,1 = 1,995

Converter para soltar a terceira casa decimal para todos os itens Produto 1 Novo valor é 1,99 Produto 2 Novo valor é 1,99

Na verdade, um total geral de 3,99 foi fornecido como um desconto ao cliente, no entanto, se soltarmos o terceiro decimal, isso mostraria que US$ 3,98 foi fornecido, e isso está incorreto.

1.99 + 1.99 = $3.98

>[!ENDSHADEBOX]


## Recursos adicionais

- [Criar uma regra de preço do carrinho - [!DNL Commerce] Guia de comercialização e promoção](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create.html)
- [Códigos de cupom - [!DNL Commerce] Guia de comercialização e promoção](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon.html)
