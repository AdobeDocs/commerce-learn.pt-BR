---
title: Saiba como criar um módulo no Adobe Commerce para usar eventos.
description: Saiba como criar um módulo do Commerce para usar eventos.
landing-page-description: Saiba como criar um módulo do Adobe Commerce para usar eventos.
short-description: Saiba como criar um módulo do Adobe Commerce para usar eventos.
kt: 11891
doc-type: tutorial
duration: 348
audience: all
last-substantial-update: 2023-02-21T00:00:00.000Z
feature: App Builder, Eventing, Backend Development
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: e8103fe0-116a-499c-ae0a-3ad0511f44d0
TQID: https://experienceleague.adobe.com/bRnOh6fnsyTY-21f81vIXV4-eeitLXQWsAbjg2rx-Is
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 0%

---

# Desenvolvimento de módulo do Adobe Commerce

Saiba como registrar eventos, encontrar eventos compatíveis e usar um novo arquivo XML `io_events.xml` no desenvolvimento de módulo personalizado. O vídeo também mostrará aos desenvolvedores como encontrar eventos registrados que podem ser usados, bem como cancelar a inscrição de eventos que já podem estar definidos. Documentação adicional encontrada em [Instalar o Adobe I/O Events para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder que usam eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Registro de eventos no Commerce para uso no Adobe Developer App Builder
* Identificar eventos que podem ser registrados
* Saiba como registrar eventos em io_events.xml
* Saiba como registrar eventos nas instâncias do Commerce `app/etc/config.php`
* Saiba como cancelar a inscrição em um evento

>[!VIDEO](https://video.tv.adobe.com/v/3430650?captions=por_br&learn=on)

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
