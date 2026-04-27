---
title: Learn how to install IO events for Adobe Commerce 2.4.5
description: Learn how to install modules needed for IO events in Adobe Commerce 2.4.5 for use in Adobe Developer App Builder
landing-page-description: Learn how to install several modules needed for Adobe Commerce 2.4.5 using composer.
short-description: Learn how to install several modules needed for Adobe Commerce 2.4.5 using composer.
kt: 11886
doc-type: tutorial
duration: 214
audience: all
last-substantial-update: 2023-02-22T00:00:00.000Z
badge: Adobe Commerce 2.4.5
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
TQID: https://experienceleague.adobe.com/vb-q-JXeM4KvkxzfDui1MaTOSBFXDVBwmpTeolUtKGw
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
source-wordcount: 190
ht-degree: 0%

---

# Adobe Commerce 2.4.5 Installation

Learn how to install several new modules in Adobe Commerce using Composer for version 2.4.5. This sets up the required modules to be used in the Adobe Commerce application. Documentação adicional encontrada em [Instalar o Adobe I/O Events para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Developers new to Adobe Commerce and Adobe Developer App Builder using I/O Events

## Conteúdo de vídeo {#video-content}

* Installation of required modules using composer
* Comandos a serem executados para hospedagem local
* Comandos a serem executados para a Adobe Commerce Cloud
* Edição do yaml da Adobe Commerce Cloud necessária

>[!VIDEO](https://video.tv.adobe.com/v/3415794?learn=on)

## Comandos úteis {#useful-commands}

Há vários comandos que diferem um pouco, dependendo se você está em um ambiente auto-hospedado ou usando a Adobe Commerce Cloud.

### Hospedagem no local {#on-premise}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce na nuvem {#adobe-commerce-cloud}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml`:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}
