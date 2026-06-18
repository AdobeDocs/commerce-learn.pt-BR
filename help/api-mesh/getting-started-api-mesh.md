---
title: Introdução à API Mesh
description: Saiba como usar a API Mesh no Adobe Commerce e no Adobe App Builder, incluindo a instalação do App Builder, o trabalho com projetos e a criação de um proxy reverso.
jira: KT-11802
doc-type: Tutorial
duration: 422
last-substantial-update: 2023-08-27T00:00:00Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Intermediate
exl-id: baae6dab-48a4-49a0-b6f6-61cbebe63d0f
source-git-commit: c73744d503de5023e5c001d0534200522db55b04
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Introdução à API Mesh

Se você nunca usou a API Mesh para Adobe Developer App Builder, a Adobe recomenda começar com este tutorial introdutório antes de prosseguir para os outros vídeos e tutoriais.

## O que é a API Mesh

A API Mesh combina várias fontes de dados para obter uma única resposta para que seu aplicativo consuma.

[Exibir a documentação completa da API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/){target="_blank"}

## Para quem é este vídeo?

* Qualquer desenvolvedor novo no API Mesh ou [!DNL Adobe Commerce] com experiência limitada usando o [Adobe I/O Runtime](https://developer.adobe.com/app-builder/docs/intro_and_overview/what-is-app-builder){target="_blank"} e o API Mesh.

## Conteúdo de vídeo

* Visão geral da API Mesh
* Links para a documentação complementar
* Caso de uso para fazer verificação de inventário em tempo real na finalização da compra
* Afastar os esforços de desenvolvimento e o uso de recursos do aplicativo de comércio

>[!VIDEO](https://video.tv.adobe.com/v/3417534?learn=on)

## Exemplo de casos de uso

Seu aplicativo do Commerce tem uma API REST e um terminal GraphQL. Por exemplo, use a API REST para aplicar preços especiais ou o terminal GraphQL para lidar com o status do inventário. Usando a API Mesh, você pode definir ambos os endpoints, recuperar as informações e retorná-las ao aplicativo solicitante como uma resposta.

## O que é um proxy reverso

Como desenvolvedor do Adobe App Builder e da API Mesh, não é necessário compreender a definição de um proxy reverso. No entanto, se você estiver interessado na funcionalidade geral, pois ela se refere ao Adobe App Builder, use os seguintes recursos:

* [O que é um proxy reverso](https://www.imperva.com/learn/performance/reverse-proxy/){target="_blank"}


{{$include /help/_includes/api-mesh-related-links.md}}
