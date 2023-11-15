---
title: Criar um produto virtual
description: Saiba como criar um produto virtual usando a REST API e o administrador do Commerce.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-15T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 225faceffefc31a6205f689933210510dba235d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Criar um produto virtual

Saiba como criar um produto virtual usando a REST API e o administrador do Adobe Commerce.

## Para quem é este vídeo?

- Gerentes de sites
- Merchandisers de comércio eletrônico
- Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos no Adobe Commerce usando a REST API.

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3425723?learn=on)

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

- [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
