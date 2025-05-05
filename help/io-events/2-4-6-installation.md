---
title: Saiba como instalar eventos de IO para o Adobe Commerce 2.4.6
description: Saiba como instalar módulos necessários para eventos de E/S no Adobe Commerce 2.4.6 para uso no Adobe Developer App Builder
landing-page-description: Saiba como instalar vários módulos necessários para o Adobe Commerce 2.4.6.
short-description: Saiba como instalar vários módulos necessários para o Adobe Commerce 2.4.6.
kt: 11887
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: Adobe Commerce 2.4.6
feature: App Builder, Eventing
topic: Commerce, Architecture
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 41b31ed8-04c5-4d50-aaff-abc3718b5957
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Instalação do Adobe Commerce 2.4.6

Saiba como instalar vários módulos novos no Adobe Commerce usando o Composer para versão 2.4.6. Documentação adicional encontrada em [Instalar Eventos Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Comandos a serem executados para hospedagem local
* Comandos a serem executados para o Adobe Commerce Cloud
* Edição do yaml Adobe Commerce Cloud necessária

>[!VIDEO](https://video.tv.adobe.com/v/3430640?quality=12&learn=on&captions=por_br)

## Comandos úteis {#useful-commands}

Há vários comandos que diferem um pouco, dependendo se você está em um ambiente auto-hospedado ou usando o Adobe Commerce Cloud.

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
