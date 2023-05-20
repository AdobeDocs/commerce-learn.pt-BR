---
title: Configurar Adobe Commerce
description: Saiba como configurar o Adobe Commerce para permitir que eventos sejam usados no Construtor de aplicativos do Adobe Developer.
landing-page-description: Saiba como configurar o Adobe Commerce para usar o mecanismo de evento para consumo pelo Construtor de aplicativos do Adobe Developer.
short-description: Saiba como configurar o Adobe Commerce para usar o mecanismo de evento para consumo pelo Construtor de aplicativos do Adobe Developer.
kt: 11889
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
exl-id: b8062042-2e90-4750-92ef-d55a76f2d842
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# Configurar Adobe Commerce

Saiba como configurar o Adobe Commerce para expor os eventos. Documentação adicional encontrada em [Instalar eventos do Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Construtor de aplicativos da Adobe Developer que usam eventos de E/S precisam criar um projeto do Construtor de aplicativos Adobe.

## Conteúdo de vídeo {#video-content}

* Configuração dos eventos de Adobe I/O no administrador de comércio
* Salvamento de uma chave privada no administrador do Commerce
* Salvamento do identificador exclusivo no administrador do Commerce
* Criar um provedor de eventos

>[!VIDEO](https://video.tv.adobe.com/v/3415799?quality=12&learn=on)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:create-event-provider --label "my_provider" --description "Provides out-of-process extensibility for Adobe Commerce"

bin/magento events:subscribe observer.catalog_product_save_after --fields=name --fields=price
```

{{$include /help/_includes/io-events-related-links.md}}
