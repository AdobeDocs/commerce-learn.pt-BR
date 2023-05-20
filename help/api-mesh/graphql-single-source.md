---
title: Criar uma malha de origem única do GraphQL na malha de API
description: Discover como usar a malha de API no Adobe Systems Comércio e  [!DNL Adobe App Builder] . Aprenda a criar uma malha com uma fonte.
landing-page-description: Discover como usar a malha de API no Adobe Systems Comércio e  [!DNL Adobe App Builder] . Aprenda a criar uma malha com uma fonte.
short-description: Discover como usar a malha de API no Adobe Systems Comércio e  [!DNL Adobe App Builder] . Aprenda a criar uma malha com uma fonte.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Criar uma malha com uma única fonte

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com uma única fonte na malha de API para Adobe Systems desenvolvedor aplicativo Builder. Para que esse exemplo básico funcione como esperado, você precisa de uma API acessível publicamente ou uma GraphQL Endpoint. O vídeo também explica como criar um arquivo simples `mesh.json` para usar com o Comércio instância. Para obter mais detalhes e amostras de código, visita [ criar uma malha ](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1) {target="_blank"} .

## Para quem é esse vídeo?

* Qualquer um novo na malha de API
* Desenvolvedores interessados em combinar vários GraphQL e fontes de API
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por GraphQL

## Vídeo conteúdo

* Uso da malha de API como um proxy reverso
* Criação de uma malha a partir de um arquivo de configuração JSON
* Acesso ao ponto de extremidade GraphQL recém-criado

>[!VIDEO](https://video.tv.adobe.com/v/3414124?quality=12&learn=on)

## Criar o arquivo de configuração JSON

A malha de API usa um arquivo de configuração JSON para definir seus manipuladores de origem. O arquivo JSON contém uma `sources` matriz que contém as fontes da sua malha. Aqui está um exemplo de uma malha com uma única fonte.

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
