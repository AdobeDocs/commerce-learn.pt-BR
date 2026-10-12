---
title: Ferramenta de migração de dados em massa - Migração multifásica
description: Saiba como executar uma migração multifásica com a Ferramenta de migração de dados em massa usando o modo de manutenção quando a origem precisar permanecer congelada durante a transferência de produção.
feature: Data Import/Export
topic: Migration
role: Developer
doc-type: Technical Video
duration: 211
last-substantial-update: 2026-07-27T00:00:00.000Z
jira: KT-22157
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%
---

# Executar uma migração de várias fases com a Ferramenta de migração de dados em massa

Execute uma migração de várias fases quando o ambiente de origem precisar ser congelado durante a extração — ideal para cutovers de produção em que novos pedidos não podem surgir no meio da migração. Ele usa o modo de manutenção e tem cinco fases que devem ser executadas em ordem. Se a fonte puder permanecer ativa, assista ao vídeo da migração de fase única desta série.

## Para quem é este vídeo?

* Arquiteto de soluções
* Engenheiro de DevOps
* Desenvolvedor de backend

## Conteúdo de vídeo

* Uma distinção importante antes de iniciar: `bin/console` comandos executados na própria ferramenta de migração; `bin/magento maintenance` comandos executados no servidor Commerce de origem. A ferramenta não ativa ou desativa o modo de manutenção para você — essa é uma etapa manual.
* A fase um é executada enquanto a origem ainda está ativa — o `bin console migration:before-maintenance` verifica a configuração, inicializa o ambiente, conecta-se ao CDMS, registra a migração, executa testes funcionais e cria dados de teste sintético. Não ative o modo de manutenção até que esta fase seja concluída.
* A fase três é a extração de um ambiente congelado — `bin/console migration:during-maintenance` reabre túneis PaaS, se necessário, extrai da origem, limpa exibições de preparo, carrega no destino ACCS, executa a verificação e limpa dados de teste no destino.

>[!VIDEO](https://video.tv.adobe.com/v/3496417?captions=por_br&learn=on)
