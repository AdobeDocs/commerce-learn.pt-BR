---
title: Saiba como instalar eventos de IO para o Adobe Commerce 2.4.5
description: Saiba como instalar módulos necessários para eventos de E/S no Adobe Commerce 2.4.5 para uso no Adobe Developer App Builder
jira: KT-11886
doc-type: Tutorial
duration: 179
last-substantial-update: 2023-02-22
badge: Adobe Commerce 2.4.5
feature: App Builder, Eventing
topic: Commerce, Architecture
role: Developer
level: Beginner, Intermediate
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
TQID: https://experienceleague.adobe.com/vb-q-JXeM4KvkxzfDui1MaTOSBFXDVBwmpTeolUtKGw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 9f50b87d13f48b239d814783eb2c56319946cb29
workflow-type: tm+mt
source-wordcount: 164
ht-degree: 0%

---

# Instalação do Adobe Commerce 2.4.5

Saiba como instalar vários módulos novos no Adobe Commerce usando o Composer para versão 2.4.5. Isso configura os módulos necessários a serem usados no aplicativo do Adobe Commerce. Documentação adicional encontrada em [Instalar o Adobe I/O Events para Adobe Commerce](https://developer.adobe.com/commerce/extensibility/events/installation){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S

## Conteúdo de vídeo {#video-content}

* Instalação dos módulos necessários usando o compositor
* Comandos a serem executados para hospedagem local
* Comandos a serem executados para a Adobe Commerce Cloud
* Edição do yaml da Adobe Commerce Cloud necessária

>[!VIDEO](https://video.tv.adobe.com/v/3415794?learn=on)

## Comandos disponíveis {#useful-commands}

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

