---
title: Criar uma solicitação de fonte única do GraphQL para ser usada na malha da API
description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma solicitação que tem uma fonte.
landing-page-description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma solicitação que tem uma fonte.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Criar malha de API do GraphQL de origem única

O vídeo ajuda um desenvolvedor a entender como criar um proxy reverso do GraphQL e tem uma única fonte. Lembre-se de que, para que o GraphQL Mesh funcione conforme o esperado, é necessário um URL acessível publicamente com um esquema GraphQL válido. O vídeo também explica como configurar seu json inicial para uso com seu site de comércio. Para obter amostras de código básicas usadas no vídeo, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Para quem é este vídeo?

* Qualquer pessoa que seja nova na malha da API
* Desenvolvedores interessados em usar várias fontes gráficas
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por grafql

## Conteúdo de vídeo

* Uso da API como proxy reverso
* Configuração JSON com a interface de linha de comando do Adobe Developer
* Acesso ao endpoint recém-criado da GraphQL

>[!VIDEO](https://video.tv.adobe.com/v/3414124)

## Criar o arquivo de configuração json

Para que o Adobe App Builder saiba mais sobre todas as suas fontes, defina-as em uma configuração JSON. Cada origem é um elemento em uma matriz e você pode ter um ou mais. Veja um exemplo de uma única fonte

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
