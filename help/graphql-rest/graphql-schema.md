---
title: Idioma do esquema com o GraphQL
description: Saiba mais sobre o esquema envolvido com o GraphQL. Leia uma descrição do esquema, juntamente com alguns padrões interessantes e maneiras de ler o esquema.
landing-page-description: Esta é uma introdução ao GraphQL. Compreender o esquema e como interpretar alguns dos elementos
short-description: Esta é uma introdução ao GraphQL. Compreender o esquema e como interpretar alguns dos elementos
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
feature: GraphQL
topic: Commerce, Architecture, Headless
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 6b59db07-b99e-47ae-9ccb-d4904afc8251
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Idioma do esquema

As consultas e mutações usadas dependem de um gráfico de dados específico que está sendo implementado no servidor, que o tempo de execução do GraphQL consome e usa para resolver a consulta. A especificação do GraphQL define uma linguagem agnóstica para expressar os tipos e relações do gráfico de dados.

Este é um schema do tipo abreviado que aceita as consultas e mutações que você viu até agora:

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

Você pode se aprofundar em [a documentação do GraphQL](https://graphql.org/learn/schema/){target="_blank"} para saber mais sobre os detalhes do sistema do tipo, incluindo a sintaxe para alguns conceitos não representados aqui. O exemplo acima, no entanto, é autoexplicativo. (Além disso, observe como a sintaxe é semelhante à sintaxe de consulta.) A definição de um schema GraphQL é simplesmente uma questão de expressar os argumentos e campos disponíveis de um determinado tipo, juntamente com os tipos desses campos. Cada tipo de campo complexo deve ter uma definição e assim por diante, por meio da árvore, até que você chegue a tipos escalares simples como `String`.

A variável `input` declaração é, em todos os aspectos, como uma `type` mas define um tipo que pode ser usado como entrada para um argumento. Observe também que `interface` declaração. Isto serve a uma função mais ou menos igual a interfaces no PHP. Outros tipos são herdados dessa interface.

A sintaxe `[CartItemInput!]!` parece complicado, mas é bastante intuitivo no final. A variável `!` _dentro_ o colchete declara que todos os valores na matriz devem ser não nulos, enquanto o _fora_ declara que o valor da matriz em si deve ser não nulo (por exemplo, uma matriz vazia).

>[!NOTE]
>
>A lógica de como os dados são buscados e formatados de acordo com um esquema e como essa lógica é mapeada para tipos específicos depende da implementação do tempo de execução do GraphQL. As implementações, no entanto, devem seguir um fluxo conceitual que faça sentido à luz de uma compreensão sobre campos aninhados: uma operação de resolução associada à raiz `Query` ou `Mutation` é executado, que examina cada campo especificado na solicitação. Para cada campo que é resolvido para um tipo complexo, uma resolução semelhante é feita para esse tipo e assim por diante, até que tudo tenha sido resolvido em valores escalares.

{{$include /help/_includes/graphql-rest-related-links.md}}
