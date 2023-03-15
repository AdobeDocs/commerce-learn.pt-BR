---
title: Instalação da interface de linha de comando do Adobe I/O Runtime e do plug-in de malha da API
description: Saiba como instalar a interface de linha de comando do Adobe I/O Runtime e o plug-in de malha da API
landing-page-description: Descubra como usar o Adobe App Builder e instalar o Adobe I/O Runtime com o plug-in de malha de API.
short-description: Discover how to use Adobe App Builder and install the Adobe I/O Runtime with API Mesh plugin.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: 67d21ca23cdccc87cdeed4a08a3ebb48e5bd1030
workflow-type: tm+mt
source-wordcount: '177'
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

>[!VIDEO](https://video.tv.adobe.com/v/3414122/)

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
