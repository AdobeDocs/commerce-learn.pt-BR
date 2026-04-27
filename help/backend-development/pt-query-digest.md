---
title: Saiba como o Percona Toolkit pt-query-digest funciona e por que ele é usado
description: Analisar consultas MySQL de arquivos de log lentos, gerais e binários. Ele também pode analisar queries de "SHOW PROCESSLIST" e dados de protocolo MySQL de tcpdump.
kt: 13846
doc-type: video
duration: 510
activity: use
last-substantial-update: 2023-8-28
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
TQID: https://experienceleague.adobe.com/lh-fBjlhZO6W-K08KNb-KaG-N2slLZVpNOSg6LAp0n8
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 113
ht-degree: 0%

---

# Percona Toolkit pt-query-digest

Saiba por que você usa o pt-query-digest e alguns exemplos reais para ajudar a aprofundar o raciocínio.

## Para quem é este vídeo?

* Arquitetos
* Desenvolvedores
* DevOps

## Conteúdo de vídeo

* Saiba mais sobre o uso de pt-query-digest
* Saiba mais sobre os benefícios e as limitações deste recurso do Kit de ferramentas Percona
* Entenda os resultados e saiba quais possíveis etapas de desempenho devem ser consideradas

>[!VIDEO](https://video.tv.adobe.com/v/3423480?learn=on)

## Referências de código

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Recursos úteis

* [Percona Toolkit](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}
