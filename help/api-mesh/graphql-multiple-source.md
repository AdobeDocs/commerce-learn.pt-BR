---
title: Criar um GraphQL de várias origens para ser usado na malha da API
description: Descubra como usar várias fontes para a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre alguns erros comuns e como resolvê-los.
landing-page-description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha que tenha várias fontes e como resolver alguns erros comuns.
short-description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha que tenha várias fontes e como resolver alguns erros comuns.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Criar uma malha com várias fontes

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com várias fontes na malha da API para o Adobe Developer App Builder. Este vídeo mostra como criar uma malha com várias fontes e identificar erros. Para obter mais detalhes e amostras de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa que seja nova na malha da API
* Desenvolvedores interessados em combinar várias fontes de API e GraphQL

## Conteúdo de vídeo

* Como utilizar [transformações](https://developer.adobe.com/graphql-mesh-gateway/gateway/transforms/){target="_blank"} para modificar o schema de origem padrão
* Como solucionar erros, como conflitos de nome, disponibilidade de esquema e outros problemas de sintaxe de esquema
* Atualizar sua malha com uma configuração modificada

>[!VIDEO](https://video.tv.adobe.com/v/3414125?quality=12&learn=on)

## Criar o arquivo de configuração json

A malha de API usa um arquivo de configuração JSON para definir seus manipuladores de origem. O arquivo JSON contém um `sources` matriz que contém as origens da sua malha. Este é um exemplo de uma malha com várias fontes.

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
      },
      {
        "name": "Example",
        "handler": {
          "graphql": {
            "endpoint": "https://www.example.com/graphql/"
          }
        }
      }
    ]
  }
}
```

{{$include /help/_includes/api-mesh-related-links.md}}
