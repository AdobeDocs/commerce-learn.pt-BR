---
title: Instalar o plug-in da CLI e da API Mesh do Adobe I/O Runtime
description: Saiba como instalar a interface de linha de comando do Adobe I/O Runtime e o plug-in do API Mesh para começar a usar o API Mesh para Adobe Developer App Builder.
jira: KT-11801
doc-type: Tutorial
duration: 410
last-substantial-update: 2023-02-08T00:00:00Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
source-git-commit: c73744d503de5023e5c001d0534200522db55b04
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Instalação do plug-in do Adobe I/O Runtime CLI e do Mesh

Antes de começar a usar o API Mesh para Adobe Developer App Builder, você precisa instalar o `aio` CLI e o plug-in do API Mesh.
Para obter instruções de instalação e pré-requisitos, visite a página API Mesh [Introdução](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/){target="_blank"}.

## Para quem é este vídeo?

* Desenvolvedores novatos no API Mesh ou [!DNL Adobe Commerce] com experiência limitada usando o [Adobe I/O Runtime](https://developer.adobe.com/app-builder/docs/intro_and_overview/what-is-app-builder){target="_blank"} e o API Mesh.

## Conteúdo de vídeo

* Introdução à API Mesh
* Instalando a CLI (interface de linha de comando) do Adobe I/O Runtime
* Instalação do plug-in do API Mesh

>[!VIDEO](https://video.tv.adobe.com/v/3414122?learn=on)

## Instalando o plug-in da CLI e da API Mesh do `aio`

Para instalar a CLI do `aio`, execute o seguinte comando após instalar o `node` e o `npm`:

```bash
npm install -g @adobe/aio-cli
```

Depois que a CLI do Adobe I/O Runtime estiver instalada, use o seguinte comando para instalar o plug-in do API Mesh:

```bash
aio plugins:install @adobe/aio-cli-plugin-api-mesh
```

{{$include /help/_includes/api-mesh-related-links.md}}
