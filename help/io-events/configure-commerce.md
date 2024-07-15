---
title: Configurar Adobe Commerce
description: Saiba como configurar o Adobe Commerce para permitir que eventos sejam usados no Adobe Developer App Builder.
landing-page-description: Saiba como configurar o Adobe Commerce para usar o mecanismo de evento para consumo do Adobe Developer App Builder.
short-description: Saiba como configurar o Adobe Commerce para usar o mecanismo de evento para consumo do Adobe Developer App Builder.
kt: 11889
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-21T00:00:00Z
feature: App Builder, Configuration, Backend Development
topic: Commerce, Architecture
role: Architect, Developer, User
level: Beginner, Intermediate
exl-id: b8062042-2e90-4750-92ef-d55a76f2d842
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Configurar Adobe Commerce

Saiba como configurar o Adobe Commerce para expor os eventos. Documentação adicional encontrada em [Instalar Eventos Adobe I/O para Adobe Commerce](https://developer.adobe.com/commerce/events/get-started/installation/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce e no Adobe Developer App Builder que usam eventos de E/S e precisam criar um projeto Adobe App Builder.

## Conteúdo de vídeo {#video-content}

* Configuração dos eventos de Adobe I/O no administrador do Commerce
* Salvamento de uma chave privada no administrador do Commerce
* Salvar o identificador exclusivo no administrador do Commerce
* Criar um provedor de eventos

>[!VIDEO](https://video.tv.adobe.com/v/3415799?quality=12&learn=on)

## Comandos úteis {#useful-commands}

```bash
bin/magento events:create-event-provider --label "my_provider" --description "Provides out-of-process extensibility for Adobe Commerce"

bin/magento events:subscribe observer.catalog_product_save_after --fields=name --fields=price
```

{{$include /help/_includes/io-events-related-links.md}}
