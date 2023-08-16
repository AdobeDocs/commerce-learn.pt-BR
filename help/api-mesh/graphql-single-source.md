---
title: Criar uma malha de origem única do GraphQL na malha de API
description: Descubra como usar a API de malha no Adobe Commerce e no [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
landing-page-description: Descubra como usar a API de malha no Adobe Commerce e no [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
short-description: Descubra como usar a API de malha no Adobe Commerce e no [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com uma fonte.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: 404d2708a6d540d6fb19a33afb20726356cd8000
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%

---

# Criar uma malha com uma única fonte

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com uma única fonte na API Mesh para o Construtor de aplicativos do Adobe Developer. Para que esse exemplo básico funcione conforme o esperado, é necessário ter uma API ou um terminal GraphQL acessível publicamente. O vídeo também explica como criar uma `mesh.json` arquivo a ser usado com sua instância do Commerce. Para obter mais detalhes e exemplos de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa nova na malha da API
* Desenvolvedores interessados em combinar várias fontes do GraphQL e da API
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por GraphQL

## Conteúdo de vídeo

* Uso da API Mesh como um proxy reverso
* Criação de uma malha a partir de um arquivo de configuração JSON
* Acesso ao endpoint do GraphQL recém-criado

>[!VIDEO](https://video.tv.adobe.com/v/3414124?quality=12&learn=on)

## Criar o arquivo de configuração json

A API Mesh usa um arquivo de configuração JSON para definir os manipuladores de origem. O arquivo JSON contém um `sources` matriz que contém as fontes da malha. Este é um exemplo de uma malha com uma única fonte.

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
