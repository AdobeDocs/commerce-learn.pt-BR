---
title: Criar uma malha de fonte única do GraphQL na malha da API
description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha que tenha uma fonte.
landing-page-description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha que tenha uma fonte.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: fba55cd605c4b17d87af5e8e2919bd400e6ebf55
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Criar uma malha com uma única fonte

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com uma única fonte na malha da API para o Adobe Developer App Builder. Para que esse exemplo básico funcione conforme o esperado, é necessário uma API acessível publicamente ou um terminal GraphQL. O vídeo também explica como criar um `mesh.json` para usar com sua instância do Commerce. Para obter mais detalhes e amostras de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Para quem é este vídeo?

* Qualquer novo na malha da API
* Desenvolvedores interessados em combinar várias fontes de GraphQL e API
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar pelo GraphQL

## Conteúdo de vídeo

* Uso da malha de API como proxy reverso
* Criação de uma malha a partir de um arquivo de configuração JSON
* Acesso ao endpoint recém-criado da GraphQL

>[!VIDEO](https://video.tv.adobe.com/v/3414124)

## Criar o arquivo de configuração json

A malha de API usa um arquivo de configuração JSON para definir seus manipuladores de origem. O arquivo JSON contém um `sources` matriz que contém as origens da sua malha. Este é um exemplo de malha com uma única fonte.

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
