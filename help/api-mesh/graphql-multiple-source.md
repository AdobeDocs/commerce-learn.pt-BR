---
title: Criar um GraphQL de várias origens para ser usado na API Mesh
description: Descubra como usar várias fontes para a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre alguns erros comuns e como resolvê-los.
landing-page-description: Saiba como usar a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com várias fontes e como resolver alguns erros comuns.
short-description: Saiba como usar a API Mesh no Adobe Commerce e  [!DNL Adobe App Builder]. Saiba mais sobre como criar uma malha com várias fontes e como resolver alguns erros comuns.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Criar uma malha com várias fontes

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com várias fontes na API Mesh para Adobe Developer App Builder. Este vídeo mostra como criar uma malha com várias fontes e identificar erros. Para obter mais detalhes e exemplos de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa nova na malha da API
* Desenvolvedores interessados em combinar várias fontes de API e GraphQL

## Conteúdo de vídeo

* Como usar [transformações](https://developer.adobe.com/graphql-mesh-gateway/gateway/transforms/){target="_blank"} para modificar o esquema de origem padrão
* Como solucionar erros, como conflitos de nome, disponibilidade de esquema e outros problemas de sintaxe de esquema
* Atualização da malha com uma configuração modificada

>[!VIDEO](https://video.tv.adobe.com/v/3430765?captions=por_br&quality=12&learn=on)

## Criar o arquivo de configuração json

A API Mesh usa um arquivo de configuração JSON para definir os manipuladores de origem. O arquivo JSON contém uma matriz `sources` que contém as fontes da malha. Este é um exemplo de uma malha com múltiplas fontes.

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
