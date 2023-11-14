---
title: Criar um produto simples
description: Saiba como criar um produto simples usando a REST API e o administrador do Commerce.
kt: 14446
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-13T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
source-git-commit: 9f5d0e83995d12b5884c53fc8bcb0e9d1913768e
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Criar um produto simples

Saiba como criar um produto simples usando a REST API e o administrador de comércio.

## Para quem é este vídeo?

- Gerentes de sites
- Merchandisers de comércio eletrônico
- Novos desenvolvedores do Adobe Commerce que precisam aprender a usar o REST para criar um produto no Adobe Commerce

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3425650?learn=on)

## Amostra de código curl para criar um produto

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=a42da0096288718c9556f77549c6305f; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "product": {
    "sku": "some-product-sku",
    "name": "My curl created product test",
    "attribute_set_id": 4,
    "price": 222,
    "type_id": "simple"
  }
}
```

## Amostra de código de ondulação para obter um produto

```bash
curl --location '{{your.url.here}}rest/default/V1/products/some-product-sku' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: private_content_version=3b797a6cc3c5c71f2193109fb9838b12'
```

## Recursos adicionais

- [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
