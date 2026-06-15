---
title: Como consultar dados
description: Saiba como consultar dados de produto do Adobe Commerce Optimizer usando o GraphQL, incluindo como formatar respostas JSON com variáveis de consulta jq e de pesquisa de estrutura.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 204
last-substantial-update: 2025-08-13
jira: KT-18548
exl-id: bad3d926-2952-4bac-b685-adb16f009f8d
TQID: https://experienceleague.adobe.com/IxrS6rwleWgU0-jtwu4hUavQuZesbQ6h5z7zVZR2xCo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: bfe282e4f1ef04985cffb109bce90bc05a70fda0
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 0%

---

# Consultar dados do Adobe Commerce Optimizer

Saiba como consultar dados usando o GraphQL em uma instância do Adobe Commerce Optimizer.

## Para quem é este vídeo?

* Arquiteto e desenvolvedores de soluções da Commerce

## Conteúdo de vídeo

* Consultar dados usando o GraphQL
* Usar jq para facilitar a leitura do json

>[!VIDEO](https://video.tv.adobe.com/v/3470805?captions=por_br&learn=on)

## Amostras de código

Certifique-se de trocar valores como `{{insert-your-graphql-endpoint-url}}`, `{{insert-your-ac-view-id}}` e `{{your-search-query-string}}` com os valores necessários na sua consulta.

Exemplo básico de consulta

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}'
```

Exemplo básico de consulta usando `jq` para criar uma impressão digital da saída

```bash
curl '{{insert-your-graphql-endpoint-url}}' \
-H 'Content-Type: application/json' \
-H 'AC-View-ID: {{insert-your-ac-view-id}}' \
-d '{"query": "query ProductSearch($search: String!) { productSearch( phrase: $search, page_size: 10, current_page: 2) { items { productView { sku name description shortDescription images { url } ... on SimpleProductView { attributes { label name value } price { regular { amount { value currency } } roles } } } } } }", "variables": { "search": "{{your-search-query-string}}"}}' | jq .
```

## Conteúdo relacionado

* [Introdução à API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#make-your-first-request){target="_blank"}
* [Guia do [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview){target="_blank"}
