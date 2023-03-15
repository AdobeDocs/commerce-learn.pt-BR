---
title: Saiba como usar eventos condicionais no Adobe Commerce
description: Saiba como usar eventos condicionais a serem usados no Adobe Developer App Builder.
landing-page-description: Saiba como usar eventos condicionais do Adobe Commerce.
short-description: Learn how to use Adobe Commerce conditional events.
kt: 11890
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Eventos condicionais do Adobe Commerce

Saiba mais sobre eventos condicionais no Adobe Commerce que podem ser usados no Adobe Developer App Builder. Documentação adicional encontrada em [Instalar eventos do Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/conditional-events/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S e precisam criar um projeto do Adobe App Builder.

## Conteúdo de vídeo {#video-content}

* Saiba mais sobre eventos condicionais
* Saiba mais sobre o uso adequado do novo arquivo XML io_events.xml
* Saiba como configurar eventos condicionais
* Definição de regras para uso em eventos condicionais
* Saiba como registrar eventos nas instâncias de Comércio `app/etc/config.php`

>[!VIDEO](https://video.tv.adobe.com/v/3415806)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id

bin/magento events:subscribe plugin.magento.catalog.model.resource_model.product.save_low_stock --parent=plugin.magento.catalog.model.resource_model.product.save --fields=sku --fields=qty --fields=category_id --rules="qty|lessThan|20" --rules="category_id|in|3,4,5"

cat app/etc/config.php

bin/magento events:list

bin/magento events:list -v
```

{{$include /help/_includes/io-events-related-links.md}}
