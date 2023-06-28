---
title: Instalação da interface de linha de comando do Adobe I/O Runtime e do plug-in do API Mesh
description: Saiba como instalar a interface de linha de comando do Adobe I/O Runtime e o plug-in da API Mesh
landing-page-description: Saiba como usar o Construtor de aplicativos Adobe e instalar o Adobe I/O Runtime com o plug-in de malha de API.
short-description: Saiba como usar o Construtor de aplicativos Adobe e instalar o Adobe I/O Runtime com o plug-in de malha de API.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Instalação do plug-in do Adobe I/O Runtime CLI e do Mesh

Antes de começar a usar a API Mesh para o Construtor de aplicativos do Adobe Developer, é necessário instalar o `aio` CLI e o plug-in da API Mesh.
Para obter instruções de instalação e pré-requisitos, visite a API Mesh [Introdução](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/){target="_blank"} página.

## Para quem é este vídeo?

* Desenvolvedores novatos na API Mesh ou [!DNL Adobe Commerce] com experiência limitada usando [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/overview/){target="_blank"} e API Mesh.

## Conteúdo de vídeo

* Introdução à API Mesh
* Instalando a CLI (interface de linha de comando) do Adobe I/O Runtime
* Instalação do plug-in do API Mesh

>[!VIDEO](https://video.tv.adobe.com/v/3414122?quality=12&learn=on)

## Instalação do `aio` Plug-in CLI e API Mesh

Após a instalação `node` e `npm`, execute o seguinte comando para instalar o `aio` CLI:

```bash
npm install -g @adobe/aio-cli
```

Depois que a CLI do Adobe I/O Runtime estiver instalada, use o seguinte comando para instalar o plug-in do API Mesh:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
