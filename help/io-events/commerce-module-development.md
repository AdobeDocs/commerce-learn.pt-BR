---
title: Saiba como criar um módulo no Adobe Commerce para usar eventos.
description: Saiba como criar um módulo do Commerce para usar eventos.
landing-page-description: Saiba como criar um módulo do Adobe Commerce para usar eventos.
short-description: Saiba como criar um módulo do Adobe Commerce para usar eventos.
kt: 11891
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: e8103fe0-116a-499c-ae0a-3ad0511f44d0
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Desenvolvimento de módulo do Adobe Commerce

Saiba como registrar eventos, encontrar eventos compatíveis e usar um novo arquivo XML `io_events.xml` no desenvolvimento de módulo personalizado. O vídeo também mostrará aos desenvolvedores como encontrar eventos registrados que podem ser usados, bem como cancelar a inscrição de eventos que já podem estar definidos. Documentação adicional encontrada em [Instalar Eventos Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder que usam eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Registro de eventos no Commerce para uso no Adobe Developer App Builder
* Identificar eventos que podem ser registrados
* Saiba como registrar eventos em io_events.xml
* Saiba como registrar eventos nas instâncias do Commerce `app/etc/config.php`
* Saiba como cancelar a inscrição em um evento

>[!VIDEO](https://video.tv.adobe.com/v/3430650?quality=12&learn=on&captions=por_br)

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
