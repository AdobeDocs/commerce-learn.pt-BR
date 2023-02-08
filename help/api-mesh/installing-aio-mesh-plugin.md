---
title: Instalação da interface de linha de comando do Adobe Developer IO e do plug-in de malha da API
description: Saiba como instalar a interface de linha de comando do Adobe Developer IO e o plug-in de malha da API
landing-page-description: Descubra como usar o Adobe App Builder e instalar o Adobe Developer IO com o plug-in de malha de API.
kt: 11801
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Instalação do plug-in Adobe Developer IO e Mesh

Antes de começar, há algumas coisas que precisam ser configuradas. Primeiro, a configuração da interface da linha de comando do Adobe Developer IO. Em seguida, verifique se o plug-in de malha de API está configurado em cada ambiente.
Para obter instruções sobre como configurar seu ambiente local para executar o Nó, o nvm e instalar o Adobe Developer IO, certifique-se de visitar [Introdução ao GraphQL Mesh](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/).

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe App Builder ou [!DNL Magento Open Source] com experiência limitada com Adobe Developer IO e malha de API.

## Conteúdo de vídeo

* Introdução à malha da API
* Instalação da interface de linha de comando do Adobe Developer IO
* Adicionar o plug-in de malha de API à linha de comando da AIO

>[!VIDEO](https://video.tv.adobe.com/v/3414122/)

## Exemplo de comandos usando NPM e AIO

Instalar a interface da linha de comando do Adobe Developer é muito simples. Depois que o Nó estiver instalado, execute este comando `npm install -g @adobe/aio-cli`
Depois que a cli do Adobe Developer é instalada, é possível instalar o plug-in de malha. Execute este comando para fazer isso `aio plugins:install @adobe/aio-cli-plugin-api-mesh`

{{$include /help/_includes/api-mesh-related-links.md}}
