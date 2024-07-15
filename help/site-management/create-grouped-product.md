---
title: Criar um produto agrupado
description: Saiba como criar um produto agrupado usando a REST API e o administrador do Commerce.
kt: 14585
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-30T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 3ad7125b-ef6d-4ea0-9fa7-8fc9eb399ec1
source-git-commit: 76a67af957b0d8c1eb64ad42f92412f338650d4b
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Criar um produto agrupado

Um produto agrupado consiste em produtos simples independentes que são apresentados como um grupo. Você pode oferecer variações de um único produto ou agrupá-las por temporada ou tema. Antes de criar um produto agrupado, verifique se todos os produtos simples que serão incluídos no grupo estão disponíveis no Adobe Commerce e crie os que não existem.

Neste tutorial, você aprenderá a criar um produto agrupado usando a API REST e o Administrador do Adobe Commerce.

Use a REST API para criar um produto de grupo na página Admin:

1. Criar um produto agrupado vazio.
1. Criar produtos simples para usar no produto agrupado.
1. Preencha o produto agrupado vazio com produtos simples.
1. Crie um produto agrupado vazio e associe os produtos simples.

   Quando você associa produtos simples ao produto agrupado, o atributo de ordem de classificação (`position`) na carga é usado pelo front-end para exibir os produtos associados na ordem desejada. Se o atributo `position` não for especificado, os produtos serão exibidos na ordem de adição ao produto agrupado.

Ao criar produtos agrupados do Administrador do Adobe Commerce, crie os produtos simples primeiro. Quando estiver pronto para criar o produto agrupado, associe os produtos simples atribuindo-os ao produto agrupado em um lote.

## Para quem é este vídeo?

- Gerentes de sites
- Merchandisers de comércio eletrônico
- Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos agrupados no Adobe Commerce usando a REST API.

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3425920?learn=on)

## Configuração do produto agrupado

Neste exemplo, há três produtos simples (criados primeiro) e um produto agrupado. Dois produtos simples são associados ao produto agrupado e o terceiro produto simples é adicionado ao produto agrupado.

## Criar o primeiro produto simples usando o cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-one",
    "name": "Simple product one",
    "attribute_set_id": 4,
    "price": 1.11,
    "type_id": "simple"
  }
}
```

## Criar o segundo produto simples usando o cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-two",
    "name": "Simple Product two",
    "attribute_set_id": 4,
    "price": 2.22,
    "type_id": "simple"
  }
}
```

## Criar o terceiro produto simples usando o cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "product-sku-three",
    "name": "Simple product three",
    "attribute_set_id": 4,
    "price": 3.33,
    "type_id": "simple"
  }
}
```

## Criar um produto agrupado vazio usando o cURL

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "product":{
        "sku":"my-new-grouped-product",
        "name":"This is my New Grouped Product",
        "attribute_set_id":4,
        "type_id":"grouped",
        "visibility":4
    }
}
'
```

## Adicionar o primeiro e o segundo produtos simples ao produto agrupado

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=28a020734488eef2600f8d5c7f302b53; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
    "items":[
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-one",
            "linked_product_type":"simple",
            "position":1,
            "extension_attributes":{
            "qty":1
            }
        },
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
    ]
}
'
```

## Adicionar o terceiro produto simples ao produto agrupado existente

Inclua o número da posição apropriada (qualquer coisa exceto `1` ou `2`), que são usados para os dois primeiros produtos originalmente associados ao produto agrupado. Para este exemplo, a posição é `4`.

```bash
curl --location --request PUT '{{your.url.here}}/rest/default/V1/products/my-new-grouped-product/links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2' \
--data '{
    "entity":{
        "sku":"my-new-grouped-product",
        "link_type":"associated",
        "linked_product_sku":"product-sku-three",
        "linked_product_type":"simple",
        "position":4,
        "extension_attributes":{
            "qty":1
        }
    }
}

'
```

## Excluir um produto simples de um produto agrupado

Para [excluir um produto simples](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/) de um produto agrupado, use: `DELETE /V1/products/{sku}/links/{type}/{linkedProductSku}`.

Para descobrir o que usar como `{type}`, use xdebug para capturar a solicitação e avaliar os $linkTypes: `related`, `crosssell`, `uupsell` e `associated`.
![Tipos de link de produto agrupados - texto alternativo](/help/assets/site-management/catalog/grouped-types.png "Tipos de link de produto agrupados capturados durante a sessão xdebug")

Ao vincular os produtos simples ao produto agrupado, a carga continha algumas seções semelhantes a:

```bash
        {
            "sku":"my-new-grouped-product",
            "link_type":"associated",
            "linked_product_sku":"product-sku-two",
            "linked_product_type":"simple",
            "position":2,
            "extension_attributes":{
            "qty":1
            }
        }
```

Na carga, o valor `link_type` `associated` fornece o valor `{type}` necessário na solicitação DELETE. A URL da solicitação será semelhante a `/V1/products/my-new-grouped-product/links/associated/product-sku-three`.

Consulte a solicitação de cURL para excluir o produto simples com o SKU `product-sku-three` do produto agrupado com o SKU `my-new-grouped-product`:

```bash
curl --location --request DELETE '{{your.url.here}}rest/default/V1/products/my-new-grouped-product/links/associated/product-sku-three' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=9e61396705e9c17423eca2bdf2deefb2'
```

## Obter um produto agrupado usando o cURL

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-grouped-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Recursos adicionais

- [Criar e gerenciar produtos agrupados](https://developer.adobe.com/commerce/webapi/rest/tutorials/grouped-product/){target="_blank"}
- [Produto agrupado](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-grouped.html){target="_blank"}
- [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [ReDoc do Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
