---
title: Instalação da interface de linha de comando do Adobe I/O Runtime e do plug-in de malha da API
description: Saiba como instalar a interface de linha de comando do Adobe I/O Runtime e o plug-in de malha da API
landing-page-description: Descubra como usar o Adobe App Builder e instalar o Adobe I/O Runtime com o plug-in de malha de API.
short-description: Descubra como usar o Adobe App Builder e instalar o Adobe I/O Runtime com o plug-in de malha de API.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Instalação do plug-in Adobe I/O Runtime CLI e Mesh

Antes de começar a usar a Mensagem de API para o Adobe Developer App Builder, é necessário instalar o `aio` CLI e o plug-in de malha da API.
Para obter instruções de instalação e pré-requisitos, visite a malha da API [Introdução](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} página.

## Para quem é este vídeo?

* Desenvolvedores novos na malha de API ou [!DNL Adobe Commerce] com experiência limitada [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} e a malha da API.

## Conteúdo de vídeo

* Introdução à malha da API
* Instalação da CLI do Adobe I/O Runtime (interface de linha de comando)
* Instalação do plug-in de malha da API

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## Instalar o `aio` Plug-in de malha de CLI e API

Depois de instalar `node` e `npm`, execute o seguinte comando para instalar o `aio` CLI:

```bash
npm install -g @adobe/aio-cli
```

Depois que a CLI do Adobe I/O Runtime estiver instalada, use o seguinte comando para instalar o plug-in da malha da API:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
