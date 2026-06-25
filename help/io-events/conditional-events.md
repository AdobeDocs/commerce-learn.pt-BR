---
title: Saiba como usar eventos condicionais no Adobe Commerce
description: Saiba como usar eventos condicionais no Adobe Developer App Builder.
landing-page-description: Saiba como usar eventos condicionais do Adobe Commerce.
short-description: Saiba como usar eventos condicionais do Adobe Commerce.
kt: 11890
doc-type: tutorial
duration: 421
audience: all
last-substantial-update: 2023-02-21T00:00:00.000Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 03787aa3-051b-4a35-b2e8-ecf6762b5eb4
TQID: https://experienceleague.adobe.com/GuN9--5xQaBnbFvQrkGuqMcDMMe-1tVGPk-hvqs4-UY
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 456f3cae8c45d137a195456692c2d11204126bb7
workflow-type: tm+mt
source-wordcount: 144
ht-degree: 0%

---

# Eventos condicionais do Adobe Commerce

Saiba mais sobre eventos condicionais no Adobe Commerce que podem ser usados no Adobe Developer App Builder. Documentação adicional encontrada em [Instalar o Adobe I/O Events para Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/conditional-events/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S e precisam criar um projeto do Adobe App Builder.

## Conteúdo de vídeo {#video-content}

* Saiba mais sobre eventos condicionais
* Saiba mais sobre o uso adequado do novo arquivo XML io_events.xml
* Saiba como configurar eventos condicionais
* Definição de regras para uso em eventos condicionais
* Saiba como registrar eventos nas instâncias do Commerce `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3415806?learn=on)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}

