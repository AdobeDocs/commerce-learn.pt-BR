---
title: Criar uma malha de origem única do GraphQL na malha de API
description: Saiba como usar a API Mesh no Adobe Commerce e no Adobe App Builder. Descubra como criar uma malha com uma única fonte de GraphQL e acessar o novo terminal.
jira: KT-11804
doc-type: Tutorial
duration: 485
last-substantial-update: 2023-02-08T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 9a78457a-1539-49c0-ac69-4bbfc6786137
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
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
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%
---
# Criar uma malha com uma única fonte

Este vídeo ajuda os desenvolvedores a entender como criar uma malha com uma única fonte na API Mesh para Adobe Developer App Builder. Para que esse exemplo básico funcione, é necessário ter uma API ou um terminal GraphQL acessível publicamente. O vídeo também explica como criar um arquivo `mesh.json` simples para usar com sua instância do Commerce. Para obter mais detalhes e exemplos de código, visite [Criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh){target="_blank"}.

## Para quem é este vídeo?

* Qualquer pessoa nova na malha da API
* Desenvolvedores interessados em combinar várias fontes do GraphQL e da API
* Qualquer pessoa que precise saber como filtrar a guia de rede e filtrar por GraphQL

## Conteúdo de vídeo

* Uso da API Mesh como um proxy reverso
* Criação de uma malha a partir de um arquivo de configuração JSON
* Acesso ao endpoint do GraphQL recém-criado

>[!VIDEO](https://video.tv.adobe.com/v/3414124?learn=on)

## Criar o arquivo de configuração JSON

A API Mesh usa um arquivo de configuração JSON para definir os manipuladores de origem. O arquivo JSON contém uma matriz `sources` que contém as fontes da malha. Veja a seguir um exemplo de uma malha com uma única fonte.

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
