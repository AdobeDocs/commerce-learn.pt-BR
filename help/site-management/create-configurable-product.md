---
title: Create a configurable product
description: Learn how to create a configurable product using the REST API and the Commerce Admin.
kt: 14586
doc-type: video
duration: 1760
audience: all
activity: use
last-substantial-update: 2023-12-15T00:00:00.000Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 112bec9a-0f8e-4252-8c52-f486a5e663b5
TQID: https://experienceleague.adobe.com/XAvtOnOIycqQ4z-uztWuVzzv0--eVit-I-QDnl67ba8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 994
ht-degree: 0%

---

# Create a configurable product

A configurable product is a parent product of multiple simple products. Define a configurable product to require the buyer to make one or more choices to select a specific product variation. For example, if the product is a shirt, the buyer must choose the size and color options to select the shirt.

Although a configurable product uses more SKUs and may initially take a little longer to set up, it can save you time in the end. If you plan to grow your business, the configurable product type is a good choice for products with multiple options.

Before creating a configurable product, verify that all the simple products to include in the configurable product are available in Adobe Commerce. Create any that do not exist.

In this tutorial, learn how to create a configurable product using the REST API and the Adobe Commerce Admin.

Use the REST API to create a configurable product:

1. Get the attributes for an [attribute set](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-sets.html) to use the ID numbers for subsequent API calls.
1. Create simple products for use in the configurable product.
1. Create an empty configurable product and associate the simple products.
1. Set the product attributes for the configurable product.
1. Populate the empty configurable product with simple products.
1. Get the configurable product and all the attributes.
1. Get the assigned children products for the configurable product.
1. Delete the association of simple products to configurable products.

When creating configurable products from the Adobe Commerce Admin, you can either create the simple products first, or use the automated tool that creates new simple products for use using the wizard.

## Para quem é este vídeo?

* Gerentes de sites
* Merchandisers de comércio eletrônico
* Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos configuráveis no Adobe Commerce usando a REST API

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3426381?learn=on)

## Obter os atributos de cor usando cURL

Neste exemplo, o conjunto de atributos inteiro com todos os atributos individuais é retornado para o conjunto de atributos 10. Pode ser longo, centenas de linhas não são incomuns. Ao revisar a resposta, a ID do atributo para cor provavelmente estará no meio. Acelere a pesquisa desses valores usando grep ou outros métodos para pesquisar os resultados. Minha resposta estava próxima à linha 665 e está incluída no seguinte trecho da resposta JSON.

```json
...
{
        "attribute_id": 93,
        "attribute_code": "color",
        "frontend_input": "select",
        "entity_type_id": "4",
        "is_required": false,
        "options": [
            {
                "label": " ",
                "value": ""
            },
            {
                "label": "Red",
                "value": "13"
            },
            {
                "label": "Blue",
                "value": "14"
            },
            {
                "label": "Green",
                "value": "15"
            }
        ],
...
```


Para recuperar as IDs de atributo para definir seu produto configurável, atualize a parte `attribute-sets/10/attributes` da seguinte solicitação de cURL para substituir `10` pela ID do conjunto de atributos em seu ambiente. Essa solicitação usa o método GET.

```bash
curl --location '{{your.url.here}}rest/V1/products/attribute-sets/10/attributes' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Criar o primeiro produto simples usando o cURL

### Ajustar IDs de ambiente e detalhes do produto

Crie o primeiro produto simples usando a API para enviar a seguinte solicitação POST usando cURL.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

* Altere `"attribute-set": 10` para substituir `10` pela ID do conjunto de atributos de seu ambiente.
* Altere `"value": "13"` para substituir `13` pelo valor do seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-red",
    "name": "Kids Hawaiian Ukulele Red",
    "attribute_set_id": 10,
    "price": 12.50,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "10",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "13"
        }
    ]
  }
}
'
```

## Criar o segundo produto simples usando o cURL

Crie o segundo produto simples usando a API para enviar a seguinte solicitação POST usando cURL.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

* Altere `"attribute_set_id": 10,` e substitua `10` pela ID do conjunto de atributos de em seu ambiente.
* Altere `"value": "14"` e substitua `14` pelo valor do seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Blue",
    "name": "Kids Hawaiian Ukulele Blue",
    "attribute_set_id": 10,
    "price": 15,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "20",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "14"
        }
    ]
  }
}
'
```

## Criar o terceiro produto simples usando o cURL

Crie o terceiro produto simples enviando a seguinte solicitação POST usando o cURL.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

* Altere `"attribute_set_id": 10,` para substituir `10` pela ID do conjunto de atributos de seu ambiente.
* Altere `"value": "15"` e substitua `15` pelo valor do seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele-Green",
    "name": "Kids Hawaiian Ukulele Green",
    "attribute_set_id": 10,
    "price": 25,
    "status": 1,
    "visibility": 1,
    "type_id": "simple",
    "weight": "0.5",
    "extension_attributes": {
        "stock_item": {
            "qty": "30",
            "is_in_stock": true
        }
    },
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "15"
        }
    ]
  }
}
'
```

## Criar um produto configurável vazio usando o cURL

Crie um produto configurável vazio enviando a seguinte solicitação POST usando o cURL.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

* Altere `"attribute_set_id": 10,` e substitua `10` pela ID do conjunto de atributos de seu ambiente.
* Altere `"value": "93"` e substitua `93` pelo valor do seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "product": {
    "sku": "Kids-Hawaiian-Ukulele",
    "name": "Kids Hawaiian Ukulele",
    "attribute_set_id": 10,
    "status": 1,
    "visibility": 4,
    "type_id": "configurable",
    "weight": "0.5",
    "custom_attributes": [
        {
            "attribute_code": "color",
            "value": "93"
        }
    ]
  }
}'
```

## Definir as opções disponíveis para o produto configurável

Defina as opções disponíveis para o produto configurável, enviando a seguinte solicitação POST usando cURL.

Antes de enviar a solicitação, altere `"attribute_id": 93,` para substituir `93` pela ID de atributo do seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/options' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "option": {
    "attribute_id": "93",
    "label": "Color",
    "position": 0,
    "is_use_default": true,
    "values": [
      {
        "value_index": 9
      }
    ]
  }
}'
```

Se você esquecer de definir as opções do produto configurável (principal), receberá um erro ao tentar associar um produto secundário ao produto configurável. A mensagem de erro é semelhante ao seguinte exemplo:

`{"message":"The parent product doesn't have configurable product options.","trace":"#0 [internal function]: Magento\\ConfigurableProduct\\Model\\LinkManagement->addChild('Kids-Hawaiian-U...'}`

## Vincular o produto derivado ao configurável

Agora, você criou três produtos simples:

* `"Kids Hawaiian Ukulele Red"`,
* `"Kids-Hawaiian-Ukulele-Blue"`
* `"Kids-Hawaiian-Ukulele-Green"`

Adicione estes produtos simples como filhos do produto configurável, enviando a seguinte solicitação POST. Envie uma solicitação separada para cada produto.

Para cada solicitação, atualize o valor `childSKU` com o valor do produto filho que você está adicionando. O exemplo a seguir atribui o produto simples `kids-Hawaiian-Ukulele-red` ao produto configurável com o SKU `Kids-Hawaiian-Ukulele-red`.


```bash
curl --location '{{your.url.here}}rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/child' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=aff63a1634f6f1a773e7a4894bf1a55c' \
--data '{
  "childSku": "Kids-Hawaiian-Ukulele-red"
}
'
```

## Obter um produto configurável usando o cURL

Agora que você criou um produto configurável com três SKUs secundárias atribuídas. Você pode ver as IDs vinculadas dos produtos atribuídos enviando a seguinte solicitação do GET usando o cURL. Esta solicitação retorna informações detalhadas sobre o produto configurável.

```json
...
        "configurable_product_links": [
            155,
            157,
            156
        ]
...
```

O seguinte usa o método GET

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Kids-Hawaiian-Ukulele' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Obter o produto filho associado a um produto configurável

Retorne somente os filhos associados ao produto configurável enviando a seguinte solicitação do GET. A resposta incluirá todos os atributos do produto secundário, incluindo SKU e preço.

O seguinte usa o método GET

```bash
curl --location '{{your.url.here}}/rest/default/V1/configurable-products/kids-hawaiian-ukulele/children' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Excluir ou remover um produto filho do configurável pai

Você pode remover um produto filho de um produto configurável sem excluir o produto do catálogo enviando a seguinte solicitação do DELETE usando o cURL.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/configurable-products/Kids-Hawaiian-Ukulele/children/Kids-Hawaiian-Ukulele-Blue' \
--header 'Authorization: Bearer {{Your Bearer Token}}'
```

## Recursos adicionais

* [Criar um tutorial de produto configurável](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/){target="_blank"}
* [Produto configurável](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html){target="_blank"}
* [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
* [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
