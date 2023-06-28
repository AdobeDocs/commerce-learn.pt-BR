---
title: Executar uma mutação usando o GraphQL
description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
landing-page-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
short-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Mutações

Qualquer especificação completa da API precisa oferecer a capacidade não apenas de consultar dados, mas também de criá-los e atualizá-los.

REST distingue entre solicitações que alteram dados e aquelas que não têm o tipo de solicitação ou &quot;verbo&quot; (GET vs. POST ou PUT).
Ao usar o GraphQL, as consultas de modificação de dados são diferenciadas pelo `mutation` que corresponde a um tipo de raiz diferente no esquema definido no servidor.

Observe este exemplo de mutação para adicionar um produto ao carrinho de um usuário. (Isso requer uma ID de carrinho gerada para a sessão do cliente conectada ou usando o `createEmptyCart` mutação.)

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

Você pode imaginar a mutação acima sendo enviada em uma solicitação junto com o seguinte dicionário de variáveis:

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

E, finalmente, você pode receber uma resposta como esta:

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

O principal ponto a ser observado sobre o exemplo acima é que, além do uso do `mutation` palavra-chave em vez de `query`, a sintaxe é idêntica a um query. Como consultas, a mutação inclui:

* Um nome de operação arbitrário (`doAddToCart`)
* Uma lista de variáveis (por exemplo, `$cartId`)
* Um campo inicial (`addProductsToCart`) com argumentos (por exemplo, `cartId`, defina como o valor de `$cartId`) entre parênteses
* Uma subseleção de campos entre chaves

A subseleção de campos permite definir com flexibilidade os campos que você deseja retornar (do tipo atribuído como o valor de retorno de `addProductsToCart` - `AddProductsToCartOutput`) após a conclusão da mutação.

Como explicado anteriormente, os campos definidos em um esquema do GraphQL começam em um tipo raiz para consultas (normalmente chamados de `Query`). Da mesma forma, existe outro tipo de raiz para mutações (normalmente referido como `Mutation`). `addProductsToCart` é um campo nesse tipo de raiz.

Algumas outras observações sobre o exemplo acima:

* A variável `!` sufixo de caractere `String` e `CartItemInput` indica que a variável é obrigatória.
* Os colchetes (`[]`) ao redor do `CartItemInput` tipo especificado para `$cartItems` indica uma lista desse tipo em vez de um único valor.

{{$include /help/_includes/graphql-rest-related-links.md}}
