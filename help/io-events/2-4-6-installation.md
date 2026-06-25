---
title: Saiba como instalar eventos de IO para o Adobe Commerce 2.4.6
description: Saiba como instalar módulos necessários para eventos de E/S no Adobe Commerce 2.4.6 para uso no Adobe Developer App Builder
landing-page-description: Saiba como instalar vários módulos necessários para o Adobe Commerce 2.4.6.
short-description: Saiba como instalar vários módulos necessários para o Adobe Commerce 2.4.6.
kt: 11887
doc-type: tutorial
duration: 167
audience: all
last-substantial-update: 2023-02-22T00:00:00.000Z
badge: Adobe Commerce 2.4.6
feature: App Builder, Eventing
topic: Commerce, Architecture
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 41b31ed8-04c5-4d50-aaff-abc3718b5957
TQID: https://experienceleague.adobe.com/19IVX54xo-RAJAOuXNIABdy11ExmBRAbWugi4eZ0cF0
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
source-git-commit: 456f3cae8c45d137a195456692c2d11204126bb7
workflow-type: tm+mt
source-wordcount: 166
ht-degree: 0%

---

# Instalação do Adobe Commerce 2.4.6

Saiba como instalar vários módulos novos no Adobe Commerce usando o Composer para versão 2.4.6. Documentação adicional encontrada em [Instalar o Adobe I/O Events para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Comandos a serem executados para hospedagem local
* Comandos a serem executados para a Adobe Commerce Cloud
* Edição do yaml da Adobe Commerce Cloud necessária

>[!VIDEO](https://video.tv.adobe.com/v/3415795?learn=on)

## Comandos úteis {#useful-commands}

Há vários comandos que diferem um pouco, dependendo se você está em um ambiente auto-hospedado ou usando a Adobe Commerce Cloud.

### Hospedagem no local {#on-premise}

```bash
bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Commerce na nuvem {#adobe-commerce-cloud}

```bash
composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml`:

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}

