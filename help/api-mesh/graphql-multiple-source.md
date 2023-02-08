---
title: Criar um GraphQL de várias origens para ser usado na malha da API
description: Descubra como usar várias fontes para a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre alguns erros comuns e como resolvê-los.
landing-page-description: Descubra como usar a malha de API no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre como criar uma solicitação que tem várias fontes e como resolver alguns erros comuns.
kt: 11804
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-8
source-git-commit: b6d501c5c852e1cc2cf1f05f91b5a9d96ac7d036
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Criar malha de API GraphQL de várias fontes

O vídeo ajuda um desenvolvedor a entender como criar um proxy reverso do GraphQL com várias fontes. Este vídeo mostra como compilar diferentes fontes, identificar erros e salvar alterações no git. Para obter amostras de código básicas usadas no vídeo, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1).

## Para quem é este vídeo?

* Qualquer pessoa que seja nova na malha da API
* Desenvolvedores interessados em usar várias fontes gráficas
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por grafql

## Conteúdo de vídeo

* Como o esquema da API de atributos personalizados complexos de uma segunda fonte pode substituir o esquema de origem padrão
* Modificar a configuração da malha da api para levar em conta o segundo schema de substituição
* Como solucionar erros que podem ocorrer no processo, como conflito de nomeação, disponibilidade de esquema e outra sintaxe de SDL
* Exemplo de erros comuns após tentativas de compilar schemas
* Reconstruir a malha da api após as edições
* Como salvar alterações no git após modificar a configuração do API Mesh

>[!VIDEO](https://video.tv.adobe.com/v/3414125)

## Criar o arquivo de configuração json

Para que o Adobe App Builder saiba mais sobre todas as suas fontes, defina-as em uma configuração JSON. Cada origem é um elemento em uma matriz e você pode ter um ou mais. Este é um exemplo de uma solicitação de várias fontes que são mescladas para formar uma única resposta.

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
        "name": "ERP",
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
