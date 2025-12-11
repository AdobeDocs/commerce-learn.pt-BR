---
title: Executar uma mutação usando o GraphQL
description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
landing-page-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
short-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e  [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas POST.
kt: 13938
doc-type: video
audience: all
last-substantial-update: 2023-10-12T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 6b82ffda-925f-4a81-8ca5-49a2b8ab4929
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '404'
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
a sintaxe é idêntica a um query. Como consultas, a mutação inclui:

* Um nome de operação arbitrário (`doAddToCart`)
* Uma lista de variáveis (por exemplo, `$cartId`)
* Um campo inicial (`addProductsToCart`) com argumentos (por exemplo, `cartId`, definido como o valor de `$cartId`) entre parênteses
* Uma subseleção de campos entre chaves

A subseleção de campos permite definir com flexibilidade os campos que você deseja retornar (do tipo atribuído como
valor de retorno de `addProductsToCart` - `AddProductsToCartOutput`) após a conclusão da mutação.

Como explicado anteriormente, os campos definidos em um esquema do GraphQL começam em um tipo raiz para consultas (normalmente chamados de `Query`). Da mesma forma,
outro tipo de raiz existe para mutações (normalmente referido como `Mutation`). `addProductsToCart` é um campo
nesse tipo de raiz.

Algumas outras observações sobre o exemplo acima:

* O caractere `!` com os sufixos `String` e `CartItemInput` indica que a variável é obrigatória.
* Os colchetes (`[]`) ao redor do tipo `CartItemInput` especificado para `$cartItems` indicam uma lista
desse tipo em vez de um valor único.

{{$include /help/_includes/graphql-rest-related-links.md}}
