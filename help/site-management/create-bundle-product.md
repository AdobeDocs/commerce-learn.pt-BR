---
title: Criar um produto do pacote
description: Saiba como criar um produto combinado usando a REST API e o administrador do Commerce.
kt: 14589
doc-type: video
audience: all
activity: use
last-substantial-update: 2024-1-8
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 5d688e6a-ae8c-4a55-b16c-5d3ae2d1bfd5
source-git-commit: 765bf4159892416e02ea1e9b8e4fa69e396d40af
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# Criar um produto do pacote

Um produto combinado é uma maneira de agrupar vários produtos em um produto principal. Esses produtos secundários podem ser um conjunto definido de produtos ou oferecer algumas variações que fornecem opções de configuração flexíveis para os clientes. Os tipos de produtos do pacote levam um pouco mais de tempo para serem configurados e você deve fazer um planejamento antes de configurá-los. No entanto, a oferta de pacotes de produtos melhora a experiência de compra, facilitando para os clientes a personalização de suas seleções de produtos.

Por exemplo, você pode oferecer um pacote de produtos chamado `Learning to surf` em sua loja na web. O pacote é o produto principal que serve como um contêiner dos produtos secundários atribuídos que especificam as opções disponíveis:

- Uma prancha de surf padrão
- Uma coleira típica de prancha de surf
- Barbatanas de prancha vermelha

Quando desejar flexibilidade adicional, é recomendável permitir várias opções de produtos derivados. Isso requer um uso mais complexo de opções e produtos derivados. Para expandir no exemplo anterior, as opções finais são:

- Uma prancha de surf padrão
- Uma coleira típica de prancha de surf
- Escolha da cor da barbatana:
   - Vermelho
   - Azul
   - Amarelo

Seja o pacote um grupo estático de produtos simples ou vários produtos com variações, as opções flexíveis de configuração tornam os tipos de produto agrupados uma ferramenta de merchandising exclusiva e poderosa para a loja da Adobe Commerce.

Antes de criar um pacote de produtos, verifique se todos os produtos simples a serem incluídos no pacote estão disponíveis no Adobe Commerce. Crie qualquer um que não exista.

Neste tutorial, saiba como criar um pacote de produtos usando a API REST e o administrador do Adobe Commerce.

Use a REST API para definir um produto de pacote:

1. Crie produtos simples para usar no produto do pacote.
1. Crie um produto agrupado e associe os produtos simples.
1. Obtenha o produto do pacote e todas as opções associadas.
1. Exclua uma opção de uma seção dos produtos do pacote.
1. Restaurar as opções de um produto do pacote.

Ao criar pacotes de produtos do administrador do Adobe Commerce, você pode criar os produtos simples primeiro ou usar a ferramenta automatizada para criar produtos simples usando um assistente.

## Para quem é este vídeo?

- Gerentes de sites
- Merchandisers de comércio eletrônico
- Novos desenvolvedores do Adobe Commerce que desejam aprender como criar pacotes de produtos no Adobe Commerce usando a REST API

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3454504?learn=on&captions=por_br)

## Criar produtos com REST

Os comandos a seguir criam todos os produtos necessários para definir o produto do pacote neste exemplo: cinco produtos simples e um produto do pacote que tem três opções.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

- Altere `"attribute-set": 4` para substituir `4` pela ID do conjunto de atributos de seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "10-ft-beginner-surfboard",
    "name": "10 Foot Beginner surfboard",
    "attribute_set_id": 4,
    "price": 100,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "8-ft-surboard-leash",
    "name": "8 Foot surboard leash",
    "attribute_set_id": 4,
    "price": 50,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "red-fins-and-fin-plugs",
    "name": "Red fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "blue-fins-and-fin-plugs",
    "name": "Blue fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "yellow-fins-and-fin-plugs",
    "name": "Yellow fins and fin plugs",
    "attribute_set_id": 4,
    "price": 15,
    "type_id": "simple",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      }
    }
  }
}
'
```

## Criar um pacote de produtos e atribuir os produtos simples como opções

Crie um produto do pacote enviando a solicitação POST a seguir.

Antes de enviar a solicitação, atualize o exemplo com os valores do seu ambiente.

- Altere `"attribute_set_id": 4,` e substitua `4` pela ID do conjunto de atributos de seu ambiente.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "beginner-surfboard",
    "name": "Beginner Surfboard",
    "attribute_set_id": 4,
    "status": 1,
    "visibility": 4,
    "type_id": "bundle",
    "extension_attributes": {
      "stock_item": {
        "qty": 100,
        "is_in_stock":true
      },
      "bundle_product_options": [
        {
          "option_id": 0,
          "position": 1,
          "sku": "surfboard-essentials",
          "title": "Beginners 10ft Surfboard",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "10-ft-beginner-surfboard",
              "option_id": 1,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 100,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 1,
          "position": 2,
          "sku": "surboard-leash",
          "title": "Surfboard leash",
          "type": "checkbox",
          "required": true,
          "product_links": [
            {
              "sku": "8-ft-surboard-leash",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 50,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        },
        {
          "option_id": 3,
          "position": 2,
          "sku": "surfboard-color",
          "title": "Choose a color for the fins and fin plugs",
          "type": "radio",
          "required": true,
          "product_links": [
            {
              "sku": "red-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 1,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "blue-fins-and-fin-plugs",
              "option_id": 2,
              "qty": 1,
              "position": 2,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            },
            {
              "sku": "yellow-fins-and-fin-plugs",
              "option_id": 3,
              "qty": 1,
              "position": 3,
              "is_default": false,
              "price": 0,
              "price_type": 0,
              "can_change_quantity": 0
            }
          ]
        }
      ]
    },
    "custom_attributes": [
      {
        "attribute_code": "price_view",
        "value": "0"
      }
    ]
  },
  "saveOptions": true
}
'
```

## Excluir uma opção de um produto do pacote

Remova um produto filho de um produto de pacote sem excluir o produto do catálogo, enviando a seguinte solicitação de DELETE usando cURL.

```bash
curl --location --request DELETE '{{your.url.here}}/rest/default/V1/bundle-products/beginner-surfboard/options/35/children/blue-fins-and-fin-plugs' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3'
```

## Restaurar opções do produto

Ao atualizar as opções de pacote de produtos, inclua todas as opções que deseja associar a este produto. Se o conjunto original de opções continha três produtos e um foi removido, inclua todas as três opções na solicitação POST para garantir que o pacote de produtos especifique todas as opções. Se você incluiu apenas a opção removida, o pacote de produtos atualizado incluirá apenas essa opção.

Localize a ID de opção revisando a resposta da criação do produto do pacote. Na resposta, o `option_id` é `35`.

```json
...
,
            {
                "option_id": 35,
                "title": "added back color options for fins and fin plugs",
                "required": true,
                "type": "radio",
                "position": 2,
                "sku": "beginner-surfboard",
                "product_links": [
                    {
                        "id": "77",
                        "sku": "red-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 1,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "78",
                        "sku": "blue-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 2,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    },
                    {
                        "id": "79",
                        "sku": "yellow-fins-and-fin-plugs",
                        "option_id": 35,
                        "qty": 1,
                        "position": 3,
                        "is_default": false,
                        "price": 15,
                        "price_type": null,
                        "can_change_quantity": 0
                    }
                ]
            }
...
```

Atualize o pacote de produtos para adicionar a opção que você removeu enviando a seguinte solicitação POST.

```bash
curl --location '{{your.url.here}}/rest/default/V1/bundle-products/options/add' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "option": {
    "option_id": 35,
    "title": "Choose a color for the fins and fin plugs",
    "required": true,
    "type": "radio",
    "position": 2,
    "sku": "beginner-surfboard",
    "product_links": [
      {
        "sku": "red-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 1,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "blue-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 2,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      },
      {
        "sku": "yellow-fins-and-fin-plugs",
        "option_id": 35,
        "qty": 1,
        "position": 3,
        "is_default": false,
        "price": 0,
        "price_type": null,
        "can_change_quantity": 0,
        "extension_attributes": {}
      }
    ],
    "extension_attributes": {}
  }
}'
```

## Recursos adicionais

- [Tutorial sobre a criação de um pacote de produtos](https://developer.adobe.com/commerce/webapi/rest/tutorials/bundle-product/){target="_blank"}
- [Produto do Pacote](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-bundle.html?lang=pt-BR){target="_blank"}
- [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [ReDoc do Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
