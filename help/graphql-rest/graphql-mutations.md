---
title: Executar uma mutação usando o GraphQL
description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
landing-page-description: Obtenha uma introdução sobre como executar uma mutação usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Execute sua primeira mutação usando chamadas de POST.
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

# Infecções e infestações

Qualquer especificação completa da API precisa oferecer a capacidade não apenas de consultar dados, mas também de criá-los e atualizá-los.

O REST faz a distinção entre solicitações que alteram dados e aquelas que não têm o tipo de solicitação ou &quot;verbo&quot; (GET vs. POST ou PUT).
Ao usar o GraphQL, as consultas de modificação de dados são diferenciadas pela variável `mutation` palavra-chave que corresponde a um tipo raiz diferente no schema definido no servidor.

Observe este exemplo de mutação para adicionar um produto ao carrinho de um usuário. (Isso requer uma ID de carrinho que foi gerada para a sessão do cliente conectado ou que usa a variável `createEmptyCart` mutação.)

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

E finalmente, você pode receber uma resposta como esta:

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

O principal ponto a ser observado sobre o exemplo acima é que, além do uso da variável `mutation` palavra-chave em vez de `query`, a sintaxe é idêntica a um query. Como queries, a mutação inclui:

* Um nome de operação arbitrário (`doAddToCart`)
* Uma lista de variáveis (por exemplo, `$cartId`)
* Um campo inicial (`addProductsToCart`) com argumentos (por exemplo, `cartId`, defina como o valor de `$cartId`) entre parênteses
* Uma subseleção de campos em chaves

A subseleção de campos permite definir de forma flexível os campos que você gostaria de retornar (do tipo atribuído como o valor de retorno de `addProductsToCart` - `AddProductsToCartOutput`) após a conclusão da mutação.

Como explicado anteriormente, os campos definidos em um esquema GraphQL começam em um tipo raiz de consultas (normalmente chamado de `Query`). Da mesma forma, existe outro tipo de raiz para as mutações (normalmente referidas como `Mutation`). `addProductsToCart` é um campo nesse tipo raiz.

Algumas outras observações sobre o exemplo acima:

* O `!` sufixo de caractere `String` e `CartItemInput` indica que a variável é obrigatória.
* Os colchetes (`[]`) em torno da `CartItemInput` tipo especificado para `$cartItems` indica uma lista desse tipo em vez de um único valor.

{{$include /help/_includes/graphql-rest-related-links.md}}
