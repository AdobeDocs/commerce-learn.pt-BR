---
title: Visão geral da arquitetura do aplicativo Salesforce Commerce cloud connector
description: Saiba mais sobre a arquitetura do Salesforce Commerce Cloud com o Adobe Commerce Optimizer.
feature: App Builder,Saas
topic: Administration,Commerce,Integrations
role: Architect, Developer
level: Beginner
doc-type: Technical Video
duration: 0
last-substantial-update: 2025-10-20T00:00:00Z
jira: KT-19014
source-git-commit: 54a1a8e62e86f8ae3456bb41a1b0450134f26b71
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Saiba mais sobre a arquitetura do Salesforce Commerce Cloud Starter Kit

Saiba mais sobre a arquitetura e a funcionalidade do Commerce Optimizer Connector Starter Kit, que integra o Salesforce Commerce Cloud (SFCC) e o Adobe App Builder. O kit inicial é usado pelo Adobe Commerce Optimizer para simplificar a sincronização de catálogos para vitrines do Edge Delivery. Ele explica como um cartucho personalizado no SFCC detecta alterações no catálogo por meio de arquivos de exportação delta e as expõe por meio de APIs personalizadas. Essas alterações são consumidas pelas ações de tempo de execução do App Builder — síncronas e assíncronas — para executar sincronizações completas e delta, atualizações de metadados e sincronizações específicas do produto. O sistema também inclui ferramentas de validação para garantir a precisão da vitrine eletrônica e usa o gerenciamento de estado da App Builder para rastrear o status de sincronização e evitar conflitos.

## Para quem é este vídeo?

* Arquiteto de soluções Commerce
* Engenheiros técnicos de marketing
* Administradores da plataforma de comércio eletrônico

## Conteúdo de vídeo

* O cartucho SFCC personalizado e as APIs detectam alterações no catálogo por meio de exportações delta, permitindo a sincronização eficiente dos dados com o Adobe App Builder.
* As ações de tempo de execução do App Builder gerenciam sincronizações completas e delta, validação e rastreamento de estado para garantir atualizações precisas e sem conflitos no Commerce Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3476056?captions=por_br&learn=on)
