---
title: Executar uma mutação usando o GraphQL
description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
landing-page-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
short-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
kt: 13938
doc-type: video
duration: 268
audience: all
last-substantial-update: 2023-10-12T00:00:00.000Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
TQID: https://experienceleague.adobe.com/DyzC0YLv2eWrfSAUZb-32cMAePHjurmp1RyynMbsa7Q
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 0%

---

# Mutações

Esta é a parte 3 da série para GraphQL e Adobe Commerce. Mutações são a capacidade de salvar, atualizar e retornar valores usando o GraphQL.


>[!VIDEO](https://video.tv.adobe.com/v/3424121?learn=on)

## Vídeos e tutoriais relacionados ao GraphQL nesta série

* [Parte 1 GraphQL - Introdução](../graphql-rest/intro-graphql.md)
* [Parte 2 GraphQL - Consultas](../graphql-rest/graphql-queries.md)
* [GraphQL Parte 4 - Esquema](../graphql-rest/graphql-schema.md)

## Exemplo de mutação

Qualquer especificação completa da API precisa oferecer a capacidade não apenas de consultar dados, mas também de criá-los e atualizá-los.

REST distingue entre solicitações que alteram dados e aquelas que não têm o tipo de solicitação ou &quot;verbo&quot; (GET vs. POST ou PUT).
Ao usar o GraphQL, as consultas de modificação de dados são diferenciadas pela palavra-chave `mutation` que corresponde a uma
tipo raiz no esquema definido no servidor.

Observe este exemplo de mutação para adicionar um produto ao carrinho de um usuário. (Isso requer uma ID de carrinho gerada
para a sessão do cliente conectado ou usando a mutação `createEmptyCart`.)

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

O principal a ser observado sobre o exemplo acima é que, além do uso da palavra-chave `mutation` em vez de `query`,
the syntax is identical to a query. Like queries, the mutation includes:

* An arbitrary operation name (`doAddToCart`)
* A list of variables (for example, `$cartId`)
* An initial field (`addProductsToCart`) with arguments (for example, `cartId`, set to the value of `$cartId`) in parentheses
* A subselection of fields in braces

The fields subselection allows you to flexibly define the fields you would like returned (from the type assigned as the
return value of `addProductsToCart` - `AddProductsToCartOutput`) after the mutation is completed.

As explained previously, fields defined in a GraphQL schema start on a root type for queries (typically referred to as a `Query`). Similarly,
another root type exists for mutations (typically referred to as `Mutation`). `addProductsToCart` is a field
on that root type.

A few other notes about the above example:

* The `!` character suffixing `String` and `CartItemInput` indicates that the variable is required.
* The square brackets (`[]`) around the `CartItemInput` type specified for `$cartItems` indicate a list
of that type rather than a single value.

{{$include /help/_includes/graphql-rest-related-links.md}}
