---
title: Saiba como criar um módulo no Adobe Commerce para usar eventos.
description: Saiba como criar o módulo Commerce para usar eventos.
landing-page-description: Saiba como criar um módulo Adobe Commerce para usar eventos.
kt: 11891
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: f1295c93652a9a2ae40a82009a8eb6895f59b909
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# Desenvolvimento do módulo Adobe Commerce

Saiba como registrar eventos, encontrar eventos compatíveis e usar um novo arquivo XML `io_events.xml` no desenvolvimento do módulo personalizado. O vídeo também mostrará aos desenvolvedores como encontrar eventos registrados que possam ser usados, bem como cancelar a assinatura de quaisquer eventos que já tenham sido definidos. Documentação adicional encontrada em [Instalar eventos do Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Registro de eventos no Commerce para uso no Adobe Developer App Builder
* Identificar eventos que podem ser registrados
* Saiba como registrar eventos em io_events.xml
* Saiba como registrar eventos nas instâncias de Comércio `app/etc/config.php`
* Saiba como cancelar a assinatura de um evento

>[!VIDEO](https://video.tv.adobe.com/v/3415802)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:list:all Magento_Catalog

bin/magento events:info plugin.magento.catalog.api.category_repository.save

bin/magento events:subscribe observer.catalog_category_save_after --fields=entity_id --fields=parent_id

cat app/etc/config.php

bin/magento events:unsubscribe observer.catalog_category_save_after

bin/magento events:list
```

{{$include /help/_includes/io-events-related-links.md}}
