---
title: Arquitetura do Salesforce Commerce Cloud Connector
description: Saiba como o Salesforce Commerce Cloud Connector Starter Kit usa ações de tempo de execução e exportações delta do App Builder para sincronizar catálogos com o Adobe Commerce Optimizer.
feature: App Builder,Saas
topic: Administration,Commerce,Integrations
role: Developer
level: Beginner
doc-type: Technical Video
duration: 288
last-substantial-update: 2025-10-20T00:00:00.000Z
jira: KT-19014
exl-id: 1e0edcbb-5619-45c2-b06d-9133f23a634f
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 7516911fc14bc80f327310b99a00f9cbff7c65c7
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%
---
# Arquitetura do Salesforce Commerce Cloud starter kit

Saiba mais sobre a arquitetura e a funcionalidade do Commerce Optimizer Connector Starter Kit, que integra o Salesforce Commerce Cloud (SFCC) e o Adobe App Builder. O kit inicial é usado pelo Adobe Commerce Optimizer para simplificar a sincronização de catálogos para vitrines do Edge Delivery. Ele explica como um cartucho personalizado no SFCC detecta alterações no catálogo por meio de arquivos de exportação delta e as expõe por meio de APIs personalizadas. Essas alterações são consumidas pelas ações de tempo de execução do App Builder — síncronas e assíncronas — para executar sincronizações completas e delta, atualizações de metadados e sincronizações específicas do produto. O sistema também inclui ferramentas de validação para garantir a precisão da vitrine eletrônica e usa o gerenciamento de estado da App Builder para rastrear o status de sincronização e evitar conflitos.

## Para quem é este vídeo?

* Arquiteto de soluções Commerce
* Engenheiros técnicos de marketing
* Administradores da plataforma de comércio eletrônico

## Conteúdo de vídeo

* O cartucho SFCC personalizado e as APIs detectam alterações no catálogo por meio de exportações delta, permitindo a sincronização eficiente dos dados com o Adobe App Builder.
* As ações de tempo de execução do App Builder gerenciam sincronizações completas e delta, validação e rastreamento de estado para garantir atualizações precisas e sem conflitos no Commerce Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3476046?learn=on)

