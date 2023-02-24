---
title: Saiba como instalar eventos de E/S para o Adobe Commerce 2.4.6
description: Saiba como instalar módulos necessários para eventos de E/S no Adobe Commerce 2.4.6 para uso no Adobe Developer App Builder
landing-page-description: Saiba como instalar vários módulos necessários para o Adobe Commerce 2.4.6.
kt: 11887
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: "Adobe Commerce 2.4.6"
source-git-commit: 4f73e2a6852d545d9b30b03158b6d8a35e3eba49
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Instalação do Adobe Commerce 2.4.6

Saiba como instalar vários novos módulos no Adobe Commerce usando o Composer para a versão 2.4.6. Documentação adicional encontrada em [Instalar eventos do Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce e no Adobe Developer App Builder usando Eventos de E/S.

## Conteúdo de vídeo {#video-content}

* Comandos para execução na hospedagem local
* Comandos para executar o Adobe Commerce Cloud
* Edição necessária do Adobe Commerce Cloud Yaml

>[!VIDEO](https://video.tv.adobe.com/v/3415795)

## Comandos úteis {#useful-commands}

Há vários comandos que diferem um pouco, dependendo se você está em um ambiente auto-hospedado ou usando o Adobe Commerce Cloud.

### Hospedagem local {#on-premise}

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