---
title: Saiba como o Percona Toolkit pt-query-digest funciona e por que ele é usado
description: Analisar consultas MySQL de arquivos de log lentos, gerais e binários. Ele também pode analisar queries de "SHOW PROCESSLIST" e dados de protocolo MySQL de tcpdump.
kt: 13846
doc-type: video
activity: use
last-substantial-update: 2023-8-28
feature: Backend Development, Tools and External Services, Logs
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 77e91f1b-b3ae-4c6d-bb6d-4fd7ebbb0baf
source-git-commit: 598bff1fd2cefdc449d5ae3431401aec1e796313
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Percona Toolkit pt-query-digest

Saiba por que você usa o pt-query-digest e alguns exemplos reais para ajudar a aprofundar o raciocínio.

## Para quem é este vídeo?

- Arquitetos
- Desenvolvedores
- DevOps

## Conteúdo de vídeo

- Saiba mais sobre o uso de pt-query-digest
- Saiba mais sobre os benefícios e as limitações deste recurso do Kit de ferramentas Percona
- Entenda os resultados e saiba quais possíveis etapas de desempenho devem ser consideradas

>[!VIDEO](https://video.tv.adobe.com/v/3452299?learn=on&captions=por_br)

## Referências de código

```MYSQL
Be sure to change to match your logs and time frame

$ pt-query-digest mysql-slow.log.7 > mysql-slow.log.7.DIGEST
```

## Recursos úteis

- [Kit de Ferramentas Percona](https://docs.percona.com/percona-toolkit/pt-query-digest.html){target="_blank"}
- [Deadlocks no MySQL](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/database/deadlocks-in-mysql.html?lang=pt-BR){target="_blank"}
