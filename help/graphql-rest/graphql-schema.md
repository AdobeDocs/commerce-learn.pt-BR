---
title: Linguagem de esquema com o GraphQL
description: Saiba mais sobre o schema envolvido com o GraphQL. Leia uma descrição do schema, juntamente com alguns padrões interessantes e maneiras de ler o schema.
landing-page-description: Esta é uma introdução ao GraphQL. Noções básicas sobre o schema e como interpretar alguns dos elementos
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: ef3dd7aaa409d9c1bc30d3d9c225966d8c1ace9e
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Idioma do esquema

As consultas e mutações com as quais trabalhamos dependem de um gráfico de dados específico sendo implementado no servidor, que o tempo de execução do GraphQL consome e usa para resolver a consulta. A especificação do GraphQL define uma linguagem agnóstica para expressar os tipos e as relações do seu gráfico de dados.

Este é um schema do tipo abreviado que suporta as consultas e mutações que você já viu:

```graphql
input FilterMatchTypeInput {
  match: String
}

type Money {
  value: Float
}

type Country {
  id: String
  full_name_english: String
}

interface ProductInterface {
  sku: String
  name: String
  related_products: [ProductInterface]
}

type CategoryFilterInput {
  name: FilterMatchTypeInput
}

type CategoryProducts {
  items: [ProductInterface]
}

type CategoryTree {
  name: String
  products(pageSize: Int, currentPage: Int): CategoryProducts
}

type CategoryResult {
  items: [CategoryTree]
}

type Products {
  items: [ProductInterface]
}

type Query {
  country (id: String): Country
  categories (filters: CategoryFilterInput): CategoryResult
  products (search: String): Products
}

input CartItemInput {
  sku: String!
  quantity: Float!
}

type CartPrices {
  grand_total: Money
}

type Cart {
  prices: CartPrices
  total_quantity: Float!
}

type AddProductsToCartOutput {
  cart: Cart!
}

type Mutation {
  addProductsToCart(cartId: String!, cartItems: [CartItemInput!]!): AddProductsToCartOutput
}
```

Você pode se aprofundar em [a documentação do GraphQL](https://graphql.org/learn/schema/){target="_blank"} para saber mais sobre os detalhes do tipo de sistema, incluindo sintaxe para alguns conceitos não representados aqui. No entanto, o exemplo acima é autoexplicativo. (Além disso, observe como a sintaxe é semelhante à sintaxe de consulta.) A definição de um schema GraphQL é simplesmente uma questão de expressar os argumentos e campos disponíveis de um determinado tipo, juntamente com os tipos desses campos. Cada tipo de campo complexo deve ter uma definição, e assim por diante, por meio da árvore, até chegar a tipos escalares simples como `String`.

O `input` declaração é, em todos os aspectos, como uma `type` mas define um tipo que pode ser usado como entrada para um argumento. Observe também a `interface` declaração. Isso serve uma função mais ou menos a mesma que interfaces no PHP. Outros tipos herdam dessa interface.

A sintaxe `[CartItemInput!]!` parece complicado, mas é bastante intuitivo no final. O `!` _inside_ o colchete declara que cada valor na matriz deve ser não nulo, enquanto o outro _outside_ declara que o próprio valor da matriz deve ser não nulo (por exemplo, uma matriz vazia).

>[!NOTE]
>
>A lógica de como os dados são buscados e formatados de acordo com um esquema e como essa lógica é mapeada para tipos específicos depende da implementação do tempo de execução do GraphQL. No entanto, as implementações devem seguir um fluxo conceitual que faça sentido à luz da compreensão de campos aninhados: Uma operação de resolução associada à raiz `Query` ou `Mutation` é executado, que examina cada campo especificado na solicitação. Para cada campo que é resolvido para um tipo complexo, uma resolução semelhante é feita para esse tipo e assim por diante, até que tudo tenha sido resolvido em valores escalares.

{{$include /help/_includes/graphql-rest-related-links.md}}
