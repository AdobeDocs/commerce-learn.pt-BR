---
title: Criar uma malha de origem única do GraphQL na malha de API
description: Saiba como usar a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
landing-page-description: Saiba como usar a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
short-description: Saiba como usar a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Criar uma malha com uma única fonte

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com uma única fonte na API Mesh para Adobe Developer App Builder. Para que esse exemplo básico funcione conforme o esperado, é necessário ter uma API ou um terminal GraphQL acessível publicamente. O vídeo também explica como criar um arquivo `mesh.json` simples para usar com sua instância do Commerce. Para obter mais detalhes e exemplos de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa nova na malha da API
* Desenvolvedores interessados em combinar várias fontes do GraphQL e da API
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por GraphQL

## Conteúdo de vídeo

* Uso da API Mesh como um proxy reverso
* Criação de uma malha a partir de um arquivo de configuração JSON
* Acesso ao endpoint do GraphQL recém-criado

>[!VIDEO](https://video.tv.adobe.com/v/3430823?captions=por_br&quality=12&learn=on)

## Criar o arquivo de configuração json

A API Mesh usa um arquivo de configuração JSON para definir os manipuladores de origem. O arquivo JSON contém uma matriz `sources` que contém as fontes da malha. Este é um exemplo de uma malha com uma única fonte.

```json
{
"meshConfig": {
    "sources": [
      {
        "name": "Commerce",
        "handler": {
          "graphql": {
            "endpoint": "https://venia.magento.com/graphql/"
          }
        }
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}
