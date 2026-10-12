---
title: O Adobe Commerce Developer Agent migra o código existente
description: Use a Ferramenta de avaliação de migração com o Agente de desenvolvedor da Adobe Commerce para determinar o escopo e recriar um módulo herdado como uma extensão testada do App Builder.
feature: Extensibility
topic: App Builder
role: Developer
level: Beginner
doc-type: Technical Video
duration: 350
last-substantial-update: 2026-08-28T00:00:00.000Z
jira: KT-22478
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%
---
# O Adobe Commerce Developer Agent migra o código existente

Nem todos os projetos começam com uma configuração vazia. Este exemplo migra uma extensão existente para o App Builder, migrando da Plataforma PaaS para o Adobe Commerce as a Cloud Service, usando a Ferramenta de avaliação de migração para alimentar o Agente do desenvolvedor.

## Para quem é este vídeo?

* Desenvolvedores do Commerce
* Arquitetos de soluções
* Engenheiros de back-end

## Conteúdo de vídeo

* Verificação de uma instância existente do Commerce com a Ferramenta de avaliação de migração — classificações de complexidade, impacto por módulo, sinais de risco e uma recomendação de reconstrução, refatoração, substituição ou remoção
* Analisar a avaliação de um módulo de alto impacto, incluindo seus ganchos, arquivos e um resumo de finalidade em linguagem simples que funciona como um prompt pronto
* Enviando a avaliação diretamente para o Agente do desenvolvedor sem cópia manual
* Para focalizar a primeira passagem em recursos específicos, responda às perguntas de escopo do agente
* Geração de um blueprint de webhooks síncronos que substituem a lógica herdada mais arriscada por um diagrama de arquitetura
* Criar a implementação com um arquivo de teste correspondente gravado com cada manipulador

>[!VIDEO](https://video.tv.adobe.com/v/3502483)

{{$include /help/_includes/commerce-developer-agent-related-links.md}}

## Recursos adicionais

* [Visão geral do Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/)
* [Desenvolvimento da avaliação da migração com o Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/assessment-development)
