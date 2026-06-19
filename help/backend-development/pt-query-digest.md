---
title: Analisar consultas MySQL com o Percona Toolkit pt-query-digest
description: Saiba como usar pt-query-digest para analisar consultas MySQL de arquivos de log lentos, gerais e binários, SHOW PROCESSLIST e dados de protocolo MySQL de tcpdump.
doc-type: Technical Video
duration: 506
last-substantial-update: 2023-08-28
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
role: Developer
level: Intermediate
jira: KT-13846
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
TQID: https://experienceleague.adobe.com/lh-fBjlhZO6W-K08KNb-KaG-N2slLZVpNOSg6LAp0n8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: add3e29f8841ca4ca99f4c40afc656f00e93ec36
workflow-type: tm+mt
source-wordcount: 105
ht-degree: 0%

---

# Percona Toolkit pt-query-digest

Saiba por que usar pt-query-digest e alguns exemplos práticos para ajudar a melhorar a análise.

## Público-alvo

* Arquitetos
* Desenvolvedores
* DevOps

## Conteúdo de vídeo

* Saiba mais sobre o uso de pt-query-digest
* Saiba mais sobre os benefícios e as limitações deste recurso do Kit de ferramentas Percona
* Entenda os resultados e saiba quais possíveis etapas de desempenho devem ser consideradas

>[!VIDEO](https://video.tv.adobe.com/v/3452299?captions=por_br&learn=on)

## Referências de código

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Recursos úteis

* [Percona Toolkit](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}
