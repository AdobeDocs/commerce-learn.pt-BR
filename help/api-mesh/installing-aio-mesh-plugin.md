---
title: Instalar Adobe Systems interface de linha de comando de e/s do tempo de execução e a malha de API plug-in
description: Discover como instalar Adobe Systems interface de linha de comando de e/s do tempo de execução e a malha de API plug-in
landing-page-description: Discover como usar Adobe Systems aplicativo Builder e instalar o Adobe Systems de tempo de execução de e/s com a malha de API plug-in.
short-description: Discover como usar Adobe Systems aplicativo Builder e instalar o Adobe Systems de tempo de execução de e/s com a malha de API plug-in.
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

# Instalação do Adobe Systems CLI de tempo de execução e/s e plug-in de malha

Antes de começar a usar a malha de API para Adobe Systems desenvolvedor aplicativo Builder, é necessário instalar a `aio` CLI e a malha de API plug-in.
Para obter instruções de instalação e pré-requisitos, visita a introdução ](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/) {target="_blank"} à malha [ de API página.

## Para quem é esse vídeo?

* Desenvolvedores novos na malha de API ou [!DNL Adobe Commerce] com experiência limitado usando [ Adobe Systems tempo de execução ](https://developer.adobe.com/runtime/docs/guides/overview/) {target="_blank"} de e/s e malha de API.

## Vídeo conteúdo

* Introdução à malha de API
* Instalação do Adobe Systems CLI de tempo de execução de I/O (interface de linha de comando)
* Instalação da malha de API plug-in

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## Instalação da CLI e da malha de `aio` API plug-in

Após instalar `node` e `npm` , execute o seguinte comando para instalar a `aio` CLI:

```bash
npm install -g @adobe/aio-cli
```

Quando a Adobe Systems CLI de tempo de execução de e/s estiver instalada, use o seguinte comando para instalar a malha de API plug-in:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
