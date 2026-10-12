---
title: Instalar o plug-in da CLI e da API Mesh do Adobe I/O Runtime
description: Saiba como instalar a interface de linha de comando do Adobe I/O Runtime e o plug-in do API Mesh para começar a usar o API Mesh para Adobe Developer App Builder.
jira: KT-11801
doc-type: Tutorial
duration: 410
last-substantial-update: 2023-02-08T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 898a0918-0362-4fa4-9204-d770ff1a7e6f
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: ce84ce08-883f-4337-ae83-6bb1855ca732
    internal-label: API Mesh
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
  - id: 618ab558-d6ad-5352-99d6-d5702c6fdf80
    internal-label: Tools and External Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '182'
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
