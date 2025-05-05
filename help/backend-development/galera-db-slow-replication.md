---
title: Saiba como encontrar consultas lentas em logs de consulta lenta do mysql e por que o método de design de replicação do Galera DB pode ser o motivo
description: O Galera DB tem um método de design que faz com que a replicação de dados em bancos de dados secundários demore mais do que o principal. Saiba como localizar esses eventos no log de consulta lenta do mysql e o motivo pelo qual você vê entradas nos logs de consulta lenta e talvez como evitá-los no futuro.
kt: 13635
doc-type: video
activity: use
last-substantial-update: 2023-7-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Architect, Developer
level: Intermediate
exl-id: 4a8a2df1-8cac-4bd9-851f-0eaae011b76c
source-git-commit: 598bff1fd2cefdc449d5ae3431401aec1e796313
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Saiba mais sobre a replicação do Galera DB e consultas lentas do MySQL relacionadas

Os clusters Galera ajudam no desempenho e na escalabilidade. Ao considerar bancos de dados secundários, é importante entender como a replicação de dados ocorre é diferente do que no principal. O banco de dados principal pode executar operações em massa. Quando a replicação ocorre para todos os bancos de dados secundários, eles executam ações uma de cada vez. Por exemplo, se você tiver 67.000.000 itens em uma exclusão, nos bancos de dados secundários, cada um acontece um de cada vez. Ao revisar os logs de consulta lenta do Mysql, você acha que essa ação pode levar muito tempo. Como os bancos de dados secundários estão executando tudo um de cada vez, o é um motivo para que as coisas não estejam sincronizadas e os impactos no desempenho possam ser detectados.

Como solução, se possível, coloque suas grandes operações em lote para ajudar os bancos de dados secundários a manter a sincronização com o principal. Ao fazer coisas em lote, permite que as ações sejam executadas em tempo hábil e os impactos no desempenho são mantidos no mínimo.

## Para quem é este vídeo?

- Arquitetos
- Desenvolvedores
- DevOps

## Conteúdo de vídeo

- Replicação de galera para o banco de dados secundário
- Saiba mais sobre o controle de fluxo
- Localizando números de thread em logs de consulta lenta do mysql
- Execuções em massa ocorrem somente no principal. As replicações ocorrem uma de cada vez
- Adicione em lote suas grandes confirmações para ajudar a replicação a acompanhar o principal

>[!VIDEO](https://video.tv.adobe.com/v/3423544?learn=on&captions=por_br)

## Recursos úteis

- [Cluster Galera](https://galeracluster.com/)
