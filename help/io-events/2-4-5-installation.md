---
title: Aprenda a instalar eventos IO para Adobe Systems Comércio 2.4.5
description: Aprenda a instalar os módulos necessários para eventos de e/s no Adobe Systems Comércio 2.4.5 para uso no Adobe Systems desenvolvedor aplicativo Builder
landing-page-description: Aprenda a instalar vários módulos necessários para Adobe Systems Comércio 2.4.5 usando o Composer.
short-description: Aprenda a instalar vários módulos necessários para Adobe Systems Comércio 2.4.5 usando o Composer.
kt: 11886
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-22T00:00:00Z
badge: Adobe Systems Comércio 2.4.5
exl-id: e0adfd85-5a3d-44ba-aab5-ecd7c61715cf
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Adobe Systems Comércio instalação do 2.4.5

Aprenda a instalar vários novos módulos no Adobe Systems Comércio usando o Composer para a versão 2.4.5. Isso configura os módulos necessários para serem usados no Adobe Systems Comércio aplicativo. Documentação adicional encontrada na [ instalação Adobe Systems eventos de e/s para Adobe Systems comércio ](https://developer.adobe.com/commerce/events/get-started/installation/) {target="_blank"} .

## Para quem é esse vídeo?

* Desenvolvedores novos no Adobe Systems Comércio e Adobe Systems desenvolvedor aplicativo Builder usando eventos de e/s

## Vídeo conteúdo {#video-content}

* Instalação dos módulos necessários usando o Composer
* Comandos a serem executados para hospedagem no local
* Comandos a serem executados para Adobe Commerce Cloud
* Adobe Commerce Cloud YAML necessário editar

>[!VIDEO](https://video.tv.adobe.com/v/3415794?quality=12&learn=on)

## Comandos úteis {#useful-commands}

Há vários comandos que diferem ligeiramente, dependendo se você estiver em um ambiente hospedada automaticamente ou usando Adobe Commerce Cloud.

### Hospedagem no local {#on-premise}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

bin/magento events:generate:module

bin/magento module:enable --all

bin/magento setup:upgrade && bin/magento setup:di:compile
```

### Adobe Systems Comércio na nuvem {#adobe-commerce-cloud}

```bash
composer require magento/commerce-eventing=^1.0 --no-update

composer update

composer info magento/ece-tools
```

Commerce Cloud `.magento.env.yaml` :

```yaml
stage:
  global:
    ENABLE_EVENTING: true
```

{{$include /help/_includes/io-events-related-links.md}}
