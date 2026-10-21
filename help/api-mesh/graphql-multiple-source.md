---
title: Criar um GraphQL de várias origens para ser usado na API Mesh
description: Descubra como usar várias fontes para a API Mesh no Adobe Commerce e [!DNL Adobe App Builder]. Saiba mais sobre alguns erros comuns e como resolvê-los.
jira: KT-21677
doc-type: Tutorial
duration: 381
last-substantial-update: 2023-02-08T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: d788a068-9d20-4db0-a0eb-fd897873253d
autotag-review: '2026-08-11T19:13:41.066Z'
TQID: 'https://experienceleague.adobe.com/O6ONn4NzMP-VqN0nsCoD-OPkZGMBelLWB-KNP1fZqmA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
subfeature_v2:
  - id: ce84ce08-883f-4337-ae83-6bb1855ca732
    internal-label: API Mesh
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
  - id: 618ab558-d6ad-5352-99d6-d5702c6fdf80
    internal-label: Tools and External Services
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7516911fc14bc80f327310b99a00f9cbff7c65c7
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%
---
# Criar uma malha com várias fontes

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com várias fontes na API Mesh para Adobe Developer App Builder. Este vídeo mostra como criar uma malha com várias fontes e identificar erros. Para obter mais detalhes e exemplos de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa nova na malha da API
* Desenvolvedores interessados em combinar várias fontes de API e GraphQL

## Conteúdo de vídeo

* Como usar [transformações](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/transforms/){target="_blank"} para modificar o esquema de origem padrão
* Como solucionar erros, como conflitos de nome, disponibilidade de esquema e outros problemas de sintaxe de esquema
* Atualização da malha com uma configuração modificada

>[!VIDEO](https://video.tv.adobe.com/v/3414125?learn=on)

## Criar o arquivo de configuração JSON

A API Mesh usa um arquivo de configuração JSON para definir os manipuladores de origem. O arquivo JSON contém uma matriz `sources` que contém as fontes da malha. Veja a seguir um exemplo de uma malha com várias origens.

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
