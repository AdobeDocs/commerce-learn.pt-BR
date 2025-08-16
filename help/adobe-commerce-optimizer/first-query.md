---
title: Como consultar dados
description: Saiba como consultar dados de uma instância do Adobe Commerce Optimizer.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 182
last-substantial-update: 2025-08-13T00:00:00Z
jira: KT-18548
source-git-commit: c598e46f7119ebdb1575e41c65d6285109fd9af9
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Consultar dados do Adobe Commerce Optimizer

Saiba como consultar dados usando o GraphQL em uma instância do Adobe Commerce Optimizer.

## Para quem é este vídeo?

* Arquiteto e desenvolvedores de soluções da Commerce

## Conteúdo de vídeo

* Consultar dados usando o GraphQL
* Usar jq para facilitar a leitura do json

>[!VIDEO](https://video.tv.adobe.com/v/3470805?learn=on&enablevpops&captions=por_br)

## Amostras de código

Certifique-se de trocar valores como `{{insert-your-graphql-endpoint-url}}`, `{{insert-your-ac-source-locale}}` e `{{your-search-query-string}}` com os valores necessários na sua consulta.

Exemplo básico de consulta

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-Source-Locale: {{insert-your-ac-source-locale}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}'
```

Exemplo básico de consulta usando `jq` para criar uma impressão digital da saída

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-Source-Locale: {{insert-your-ac-source-locale}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}' | jq .
```

## Conteúdo relacionado

* [Introdução à API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
* [[!DNL Adobe Commerce Optimizer] Guia](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview){target="_blank"}
