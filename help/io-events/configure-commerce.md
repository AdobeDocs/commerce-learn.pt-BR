---
title: Configurar o Adobe Commerce
description: Saiba como configurar o Adobe Commerce para permitir que os eventos sejam usados no Adobe Developer App Builder.
landing-page-description: Saiba como configurar o Adobe Commerce para usar o mecanismo de evento para consumo pelo Adobe Developer App Builder.
kt: 11889
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
source-git-commit: fe59ed078ac0fa410b9f0a7a62719a279f73390c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Configurar o Adobe Commerce

Saiba como configurar o Adobe Commerce para expor os eventos. Documentação adicional encontrada em [Instalar eventos do Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce e no Adobe Developer App Builder usando eventos de E/S e precisam criar um projeto do Adobe App Builder.

## Conteúdo de vídeo {#video-content}

* Configuração dos eventos do Adobe I/O no administrador do Commerce
* Salvar uma chave privada no administrador do Commerce
* Como salvar o identificador exclusivo no administrador do Commerce
* Criar um provedor de eventos

>[!VIDEO](https://video.tv.adobe.com/v/3415799)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:create-event-provider --label "my_provider" --description "Provides out-of-process extensibility for Adobe Commerce"

bin/magento events:subscribe observer.catalog_product_save_after --fields=name --fields=price
```

{{$include /help/_includes/io-events-related-links.md}}
