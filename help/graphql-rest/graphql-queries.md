---
title: Realizar um query usando o GraphQL
description: Saiba como executar um query usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Esta é uma introdução ao GraphQL usando chamadas GET e POST.
landing-page-description: Saiba como executar um query usando o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Esta é uma introdução ao GraphQL usando chamadas GET e POST.
short-description: Learn how to perform a query using GraphQL on Adobe Commerce and [!DNL Magento Open Source]. This is an introduction to GraphQL using GET and POST calls.
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
exl-id: 443d711d-ec74-4e07-9357-fbbe0f774853
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 0%

---

# Consultas do GraphQL

Vamos mergulhar diretamente na sintaxe de consulta do GraphQL com um exemplo completo. (Lembre-se, você pode experimentar isso sozinho em https://venia.magento.com/graphql.)

Observe a seguinte consulta do GraphQL, que é detalhada por peça:

```graphql
{
    country (
        id: "US"
    ) {
        id
        full_name_english
    }

    categories(
        filters: {
            name: {
                match: "Tops"
            }
        }
    ) {
        items {
            name
            products(
                pageSize: 10,
                currentPage: 2
            ) {
                items {
                    sku
                }
            }
        }
    }
}
```

Uma resposta plausível de um servidor GraphQL para a consulta acima pode ser:

```json
{
  "data": {
    "country": {
      "id": "US",
      "full_name_english": "United States"
    },
    "categories": {
      "items": [
        {
          "name": "Tops",
          "products": {
            "items": [
              {
                "sku": "VSW06"
              },
              {
                "sku": "VT06"
              },
              {
                "sku": "VSW07"
              },
              {
                "sku": "VT07"
              },
              {
                "sku": "VSW08"
              },
              {
                "sku": "VT08"
              },
              {
                "sku": "VSW09"
              },
              {
                "sku": "VT09"
              },
              {
                "sku": "VSW10"
              },
              {
                "sku": "VT10"
              }
            ]
          }
        }
      ]
    }
  }
}
```

O exemplo acima depende do schema pronto para uso do GraphQL para Adobe Commerce, definido no servidor. Nesta solicitação, você consulta vários tipos de dados de uma só vez. O query expressa exatamente os campos desejados e os dados retornados são formatados de forma semelhante ao próprio query.

>[!NOTE]
>
>Os clientes do GraphQL ofuscam o formulário da solicitação HTTP real que está sendo enviada, mas isso é fácil de descobrir. Se você estiver usando um cliente com base em navegador, observe o [!UICONTROL Network] quando um query é enviado. Você vê que a solicitação contém um corpo bruto que consiste em &quot;query: `{string}`&quot;, onde `{string}` é simplesmente a sequência bruta de todo o query. Se a solicitação estiver sendo enviada como um GET, a consulta poderá ser codificada no parâmetro de sequência de consulta &quot;query&quot;. Ao contrário do REST, o tipo de solicitação HTTP não importa, somente o conteúdo da consulta.


## Consultando o que deseja

`country` e `categories` no exemplo representa dois &quot;queries&quot; diferentes para dois tipos diferentes de dados. Ao contrário de um paradigma de API tradicional como REST, que definiria endpoints separados e explícitos para cada tipo de dados. O GraphQL oferece a flexibilidade de consultar um único endpoint com uma expressão que pode buscar vários tipos de dados de uma só vez.

Da mesma forma, a query especifica exatamente os campos desejados para ambos `country` (`id` e `full_name_english`) e `categories` (`items`, que tem uma subseleção de campos) e os dados recebidos retroalimentam essa especificação de campo. Provavelmente, há muitos mais campos disponíveis para esses tipos de dados, mas você recupera apenas o que solicitou.


>[!NOTE]
>
>Você pode notar que o valor de retorno de `items` na verdade é um _array_ de valores, mas, no entanto, você está selecionando diretamente os subcampos para ele. Quando o tipo de campo é uma lista, o GraphQL entende implicitamente as subseleções a serem aplicadas a cada item na lista.

## Argumentos

Embora os campos que você deseja retornar sejam especificados nas chaves de cada tipo, os argumentos nomeados e os valores para eles são especificados entre parênteses após o nome do tipo. Os argumentos geralmente são opcionais e afetam a maneira como os resultados da consulta são filtrados, formatados ou transformados.

Você está transmitindo uma `id` argumento para `country`, especificando o país específico a ser consultado e um `filters` argumento para `categories`.

## Campos até o fim

Embora você possa ter tendência a pensar em `country` e `categories` como queries ou entidades separadas, a árvore inteira expressa em sua query na verdade consiste em apenas campos. A expressão de `products` é sintaticamente indiferente do de `categories`. Ambos são campos e não há diferença entre suas construções.

Qualquer gráfico de dados do GraphQL tem um único tipo de &quot;raiz&quot; (normalmente referenciado por `Query`) para iniciar a árvore, e os tipos frequentemente considerados como entidades são atribuídos a campos nessa raiz. Na verdade, a query de exemplo está fazendo uma consulta genérica para o tipo raiz e selecionando os campos `country` e `categories`. Em seguida, é possível selecionar subcampos desses campos e assim por diante, possivelmente com vários níveis de profundidade. Sempre que o tipo de retorno de um campo for complexo (por exemplo, um com seus próprios campos, em vez de um tipo escalar), continue a selecionar os campos desejados.

Esse conceito de campos aninhados também é o motivo pelo qual você pode enviar argumentos para `products` (`pageSize` e `currentPage`) da mesma forma que fez para o nível superior `categories` campo.

![Árvore de campos do GraphQL](../assets/graphql-field-tree.png)

## Variáveis

Vamos tentar uma consulta diferente:

```graphql
query getProducts(
    $search: String
) {
    products(
        search: $search
    ) {
        items {
            ...productDetails
            related_products {
                ...productDetails
            }
        }
    }
}

fragment productDetails on ProductInterface {
    sku
    name
}
```

A primeira coisa a observar é adicionar a palavra-chave `query` antes da chave de abertura do query, juntamente com um nome de operação (`getProducts`). O nome desta operação é arbitrário; não corresponde a nada no schema do servidor. Essa sintaxe foi adicionada para suportar a introdução de variáveis.

Na query anterior, os valores foram codificados para os argumentos dos campos diretamente, como strings ou números inteiros. A especificação do GraphQL, no entanto, tem suporte de primeira classe para separar a entrada do usuário da consulta principal usando variáveis.

Na nova query, você está usando parênteses antes da chave de abertura de todo o query para definir um `$search` (variáveis sempre usam a sintaxe de prefixo de cifrão). É essa variável que está sendo fornecida para a variável `search` argumento para `products`.

Quando um query contém variáveis, espera-se que a solicitação do GraphQL inclua um dicionário de valores codificados em JSON separado ao lado da própria query. Para a consulta acima, você pode enviar o seguinte JSON de valores de variável além do corpo da consulta:

```json
{
    "search": "VT01"
}
```

>[!NOTE]
>
>Se você estiver experimentando essas consultas com o site de exemplo Venia em vez de sua própria instância do Adobe Commerce, é provável que os resultados retornados estejam vazios para `related_products`.

Em qualquer cliente com reconhecimento de GraphQL que você esteja usando para teste (como Altair e GraphiQL), a interface do usuário suporta a inserção das variáveis JSON separadamente da consulta.

Da mesma forma que você viu que a solicitação HTTP real para um query GraphQL contém &quot;query: `{string}`&quot; em seu corpo, qualquer solicitação que contenha um dicionário de variáveis inclui simplesmente &quot;variáveis: `{json}`&quot; nesse mesmo corpo, onde `{json}` é a string JSON com os valores da variável.

O novo query também usa um _fragmento_ (`productDetails`) para reutilizar a mesma seleção de campo em vários lugares. [Leia mais sobre fragmentos](https://graphql.org/learn/queries/#fragments){target="_blank"} na documentação do GraphQL.

{{$include /help/_includes/graphql-rest-related-links.md}}
