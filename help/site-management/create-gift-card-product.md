---
title: Criar um produto de cartão-presente
description: Saiba como criar um produto de cartão-presente usando a REST API e o administrador do Commerce.
kt: 14587
doc-type: video
audience: all
activity: use
last-substantial-update: 2024-2-1
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
duration: 815
exl-id: c18fd80e-1a25-4346-a8c5-3b5449d49965
TQID: 'https://experienceleague.adobe.com/wGq8KFBDMlY5wW02ZVuV0ZCVquAlXNxxWQioXVba8Kk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: bb2df8be-afdd-4818-b6b5-95ca1dd3bc3a
    internal-label: Admin workspace
  - id: e0ca0e7a-9738-48d1-b98b-615468ab4aaf
    internal-label: REST API
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%
---
# Criar um produto de cartão-presente

Saiba como criar um produto de cartão-presente usando a REST API e o administrador do Adobe Commerce.

## Para quem é este vídeo?

* Gerentes de sites
* Merchandisers de comércio eletrônico
* Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos no Adobe Commerce usando a REST API.

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3427128?learn=on)

## Criar um cartão-presente com uma carga simples

O exemplo de solicitação a seguir mostra a carga para criar um cartão-presente como o mostrado no vídeo. Essa carga menor substitui as configurações padrão para um subconjunto dos atributos disponíveis. Os atributos restantes não incluídos na carga permanecem definidos com os valores padrão.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=83b55460e3ab1bf903fab59dfedc81c6; private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "giftcard21",
    "name": "giftcard21",
    "attribute_set_id": {{Your Attribute Set ID}},
    "price": 0,
    "status": 1,
    "visibility": 4,
    "type_id": "giftcard",
    "weight": 1,
    "extension_attributes": {
      "website_ids": [
        1
      ],
      "stock_item": {
        "qty": 1000,
        "is_in_stock": true
      },
      "giftcard_amounts": [
        {
          "attribute_id": {{Your attribute ID for giftcard_amounts},
          "website_id": 0,
          "value": 10,
          "website_value": null
        },
        {
          "attribute_id": {{Your attribute ID for giftcard_amounts},
          "website_id": 0,
          "value": 20,
          "website_value": null
        }
      ]
    },
    "custom_attributes": [
    
      {
        "attribute_code": "gift_message_available",
        "value": "2"
      },
      {
        "attribute_code": "is_redeemable",
        "value": "1"
      },
      {
        "attribute_code": "required_options",
        "value": "1"
      },
      {
        "attribute_code": "use_config_is_redeemable",
        "value": "1"
      },
      {
        "attribute_code": "has_options",
        "value": "1"
      },
      {
        "attribute_code": "allow_message",
        "value": "1"
      },
      {
        "attribute_code": "giftcard_type",
        "value": "1"
      },
      {
        "attribute_code": "giftcard_amounts",
        "value": [
          {
            "website_id": "0",
            "value": "10.0000",
            "attribute_id": "{{Your attribute ID for giftcard_amounts}",
            "website_value": 10
          },
          {
            "website_id": "0",
            "value": "20.0000",
            "attribute_id": "{{Your attribute ID for giftcard_amounts}",
            "website_value": 20
          }
        ]
      },
      {
        "attribute_code": "allow_open_amount",
        "value": "1"
      },
      {
        "attribute_code": "open_amount_min",
        "value": "10.000000"
      },
      {
        "attribute_code": "open_amount_max",
        "value": "100.000000"
      },
      {
        "attribute_code": "is_returnable",
        "value": "2"
      }
    ]
  }
}'
```

## Criar um cartão-presente com carga total

O exemplo a seguir mostra a solicitação POST para criar um vale-presente com carga total. A carga inclui todos os atributos que podem ser configurados quando você cria um cartão-presente. Se você usar essa amostra de código, personalize a configuração atualizando os valores padrão para cada atributo, conforme necessário, antes de enviar a solicitação.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=83b55460e3ab1bf903fab59dfedc81c6; private_content_version=41d94540f5bd8b691017a850bc3b82b3' \
--data '{
  "product": {
    "sku": "giftcard22",
    "name": "giftcard22",
    "attribute_set_id": {{Your Attribute Set ID}},
    "price": 0,
    "status": 1,
    "visibility": 4,
    "type_id": "giftcard",
    "created_at": "2024-01-24 20:54:54",
    "updated_at": "2024-01-24 20:54:54",
    "weight": 1,
    "extension_attributes": {
      "website_ids": [
        1
      ],
      "stock_item": {
        "qty": 1000,
        "is_in_stock": true,
        "is_qty_decimal": false,
        "show_default_notification_message": false,
        "use_config_min_qty": true,
        "min_qty": 0,
        "use_config_min_sale_qty": 1,
        "min_sale_qty": 1,
        "use_config_max_sale_qty": true,
        "max_sale_qty": 10000,
        "use_config_backorders": true,
        "backorders": 0,
        "use_config_notify_stock_qty": true,
        "notify_stock_qty": 1,
        "use_config_qty_increments": true,
        "qty_increments": 0,
        "use_config_enable_qty_inc": true,
        "enable_qty_increments": false,
        "use_config_manage_stock": true,
        "manage_stock": true,
        "low_stock_date": null,
        "is_decimal_divided": false,
        "stock_status_changed_auto": 0
      },
      "giftcard_amounts": [
        {
          "attribute_id": {{Your attribute ID for giftcard_amounts},
          "website_id": 0,
          "value": 10,
          "website_value": null
        },
        {
          "attribute_id": {{Your attribute ID for giftcard_amounts},
          "website_id": 0,
          "value": 20,
          "website_value": null
        }
      ]
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": [],
    "custom_attributes": [
      {
        "attribute_code": "options_container",
        "value": "container2"
      },
      {
        "attribute_code": "url_key",
        "value": "giftcard22"
      },
      {
        "attribute_code": "gift_message_available",
        "value": "2"
      },
      {
        "attribute_code": "is_redeemable",
        "value": "1"
      },
      {
        "attribute_code": "required_options",
        "value": "1"
      },
      {
        "attribute_code": "use_config_is_redeemable",
        "value": "1"
      },
      {
        "attribute_code": "has_options",
        "value": "1"
      },
      {
        "attribute_code": "lifetime",
        "value": "0"
      },
      {
        "attribute_code": "use_config_lifetime",
        "value": "1"
      },
      {
        "attribute_code": "email_template",
        "value": "giftcard_email_template"
      },
      {
        "attribute_code": "use_config_email_template",
        "value": "1"
      },
      {
        "attribute_code": "allow_message",
        "value": "1"
      },
      {
        "attribute_code": "meta_title",
        "value": "giftcard22"
      },
      {
        "attribute_code": "use_config_allow_message",
        "value": "1"
      },
      {
        "attribute_code": "gift_wrapping_available",
        "value": "2"
      },
      {
        "attribute_code": "meta_keyword",
        "value": "giftcard22"
      },
      {
        "attribute_code": "giftcard_type",
        "value": "1"
      },
      {
        "attribute_code": "giftcard_amounts",
        "value": [
          {
            "website_id": "0",
            "value": "10.0000",
            "attribute_id": "{{Your attribute ID for giftcard_amounts}",
            "website_value": 10
          },
          {
            "website_id": "0",
            "value": "20.0000",
            "attribute_id": "{{Your attribute ID for giftcard_amounts}",
            "website_value": 20
          }
        ]
      },
      {
        "attribute_code": "allow_open_amount",
        "value": "1"
      },
      {
        "attribute_code": "open_amount_min",
        "value": "10.000000"
      },
      {
        "attribute_code": "open_amount_max",
        "value": "100.000000"
      },
      {
        "attribute_code": "meta_description",
        "value": "giftcard22"
      },
      {
        "attribute_code": "is_returnable",
        "value": "2"
      }
    ]
  }
}'
```

## Recursos adicionais

* [Criar um produto de cartão-presente do administrador do Commerce](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-gift-card-create.html){target="_blank"}
* [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
* [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
