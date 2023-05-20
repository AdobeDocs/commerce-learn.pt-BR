---
title: Executar uma mutação usando GraphQL
description: Obtenha uma introdução sobre como executar uma mutação usando GraphQL no Adobe Systems Comércio e  [!DNL Magento Open Source] . Execute sua primeira mutação usando chamadas de POST.
landing-page-description: Obtenha uma introdução sobre como executar uma mutação usando GraphQL no Adobe Systems Comércio e  [!DNL Magento Open Source] . Execute sua primeira mutação usando chamadas de POST.
short-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Mutações

Qualquer especificação completa de API precisa oferta a capacidade de query dados, mas também sua criação e atualização.

O REST distingue entre solicitações que alteram dados e aquelas que não têm o tipo solicitação ou &quot;verbo&quot; (GET versus POST ou PUT).
Ao usar o GraphQL, as consultas de modificação de dados são diferenciadas pelo palavra-chave que corresponde a `mutation` um outro
tipo de raiz no schema definido no servidor.

Look neste exemplo de mutação para adicionar um produto à carrinho do usuário. (Isso requer uma ID de carrinho que foi gerada
para a sessão do cliente conectado ou usando a `createEmptyCart` mutação.)

```graphql
mutation doAddToCart(
    $cartId: String!,
    $cartItems: [CartItemInput!]!
) {
    addProductsToCart(
        cartId: $cartId
        cartItems: $cartItems
    ) {
        cart {
            total_quantity
            prices {
                grand_total {
                    value
                }
            }
        }
    }
}
```

Você pode imaginar que a mutação acima está sendo enviada em um solicitação juntamente com o seguinte dicionário de variáveis:

```json
{
  "cartId": "{cart-id}",
  "cartItems": [
    {
      "quantity": 1,
      "sku": "VT01-RN-XS"
    }
  ]
}
```

E, finalmente, você pode receber uma resposta curtir:

```json
{
  "data": {
    "addProductsToCart": {
      "cart": {
        "total_quantity": 1,
        "prices": {
          "grand_total": {
            "value": 35.2
          }
        }
      }
    }
  }
}
```

O chefe a observar que, sobre o exemplo acima, é que, além do uso do `mutation` palavra-chave em vez de `query` ,
a sintaxe é idêntica a uma query. Como as consultas, a mutação inclui:

* Um nome de operação arbitrário (`doAddToCart`)
* Uma lista de variáveis (por exemplo, `$cartId`)
* Um campo inicial ( `addProductsToCart` ) com argumentos (por exemplo, `cartId` definido como o valor de `$cartId` ) entre parênteses
* Uma subseleção de campos em chaves

A Subseleção de campos permite definir com flexibilidade os campos que você curtir retornado (do tipo atribuído como
valor de retorno de `addProductsToCart` - `AddProductsToCartOutput` ) após a conclusão da mutação.

Conforme explicado anteriormente, os campos definidos em um GraphQL schema start em um tipo de raiz para consultas (geralmente chamadas `Query` de a). Da mesma forma
Há outro tipo de raiz para mutações (normalmente conhecido como `Mutation` ). `addProductsToCart` é um campo
nesse tipo de raiz.

Algumas outras observações sobre o exemplo acima:

* O sufixo `String` de `!` caractere e `CartItemInput` indica que a variável é necessária.
* Os colchetes ( `[]` ) em torno do `CartItemInput` tipo especificado para `$cartItems` indicar um lista
desse tipo em vez de um único valor.

{{$include /help/_includes/graphql-rest-related-links.md}}
