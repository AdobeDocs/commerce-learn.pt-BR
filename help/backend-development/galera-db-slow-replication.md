---
title: Diagnosticar replicação do Galera DB em logs de consulta lenta do MySQL
description: Saiba como o design de replicação do Galera DB reduz a velocidade das sincronizações de bancos de dados secundários, como identificar esses eventos em logs de consulta lenta do MySQL e como minimizar o impacto.
doc-type: Technical Video
duration: 452
last-substantial-update: 2023-07-18
feature: Backend Development, Logs, Services
topic: Commerce, Development
role: Developer
level: Intermediate
jira: KT-13635
exl-id: 4a8a2df1-8cac-4bd9-851f-0eaae011b76c
TQID: https://experienceleague.adobe.com/NYapiIjnRv5RAS1glm8do16M4jUPmbgfVCs6ICQwbUc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: add3e29f8841ca4ca99f4c40afc656f00e93ec36
workflow-type: tm+mt
source-wordcount: 262
ht-degree: 0%

---

# Saiba mais sobre a replicação do Galera DB e consultas lentas do MySQL relacionadas

Os clusters Galera ajudam no desempenho e na escalabilidade. Ao considerar bancos de dados de réplica, é importante compreender que a forma como a replicação de dados ocorre é diferente da principal. O banco de dados principal pode executar operações em massa. Quando a replicação ocorre para todos os bancos de dados de réplica, eles realizam ações uma de cada vez. Por exemplo, se você tiver 67.000.000 itens em uma exclusão, nos bancos de dados de réplica cada um ocorrerá um de cada vez. Ao revisar os logs de consulta lenta do MySQL, você acha que essa ação pode levar muito tempo. O fato de os bancos de dados de réplica estarem executando operações sequencialmente é um motivo para que as coisas não estejam sincronizadas e é possível detectar impactos no desempenho.

Para ajudar os bancos de dados de réplica a manterem-se sincronizados com o banco de dados principal, faça um lote de grandes operações quando possível. Ao fazer coisas em lote, permite que as ações sejam executadas em tempo hábil e os impactos no desempenho são mantidos no mínimo.

## Público-alvo

* Arquitetos
* Desenvolvedores
* DevOps

## Conteúdo de vídeo

* Replicação de galera para banco de dados de réplica
* Saiba mais sobre o controle de fluxo
* Localizando números de thread em logs de consulta lenta do mysql
* Execuções em massa ocorrem somente no principal. As replicações ocorrem uma de cada vez
* Para ajudar a replicação a acompanhar o principal, faça o lote de grandes confirmações.

>[!VIDEO](https://video.tv.adobe.com/v/3423544?captions=por_br&learn=on)

## Recursos úteis

* [Cluster Galera](https://mariadb.com/products/enterprise/galera-cluster/)
