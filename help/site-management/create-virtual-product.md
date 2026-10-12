---
title: Criar um produto virtual
description: Saiba como criar um produto virtual usando a REST API e o administrador do Commerce.
kt: 14464
doc-type: video
duration: 213
audience: all
activity: use
last-substantial-update: 2023-11-15T00:00:00.000Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 5149b6b4-5fbf-467a-a412-6dce7188bcb9
TQID: 'https://experienceleague.adobe.com/OktfC13mVgaoxyfKlZYH6HPDoCqP-m07pz5VEQ4cssM'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
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
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%
---
# Criar um produto virtual

Saiba como criar um produto virtual usando a REST API e o administrador do Adobe Commerce.

## Para quem é este vídeo?

* Gerentes de sites
* Merchandisers de comércio eletrônico
* Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos no Adobe Commerce usando a REST API.

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3444869?captions=por_br&learn=on)

## Criar um produto virtual usando curl

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "postman-rest-virtual-product-test",
    "name": "POSTMAN virtual product test",
    "attribute_set_id": 4,
    "price": 44,
    "type_id": "virtual"
  }
}
'
```

## Obter um produto usando o curl

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/Admin-created-virtual-product' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=2cd97649bcf4ee5b45b23f8eb940e3a0; private_content_version=564dde2976849891583a9a649073f01e'
```

## Recursos adicionais

* [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
* [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
