---
title: Ferramenta de Migração de Dados em Massa - Credenciais do BD
description: Saiba como configurar a conexão do banco de dados de origem em seu arquivo .my.cnf usando a Magento Cloud CLI ou uma ID de projeto antes de executar a ferramenta de migração.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 161
last-substantial-update: 2026-07-21T00:00:00Z
jira: KT-22105
source-git-commit: 0dcb41e9138a36528f10333b0b5a9a9b2a39ed40
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Configurar credenciais de banco de dados para a Ferramenta de Migração de Dados em Massa

Configure a conexão de banco de dados de origem no arquivo `.my.cnf` antes de executar a Ferramenta de Migração de Dados em Massa. As etapas diferem dependendo se o ambiente de origem está no local ou no Adobe Commerce as a Cloud Service (PaaS).

## Para quem é este vídeo?

* Arquiteto de soluções
* Engenheiro de DevOps
* Desenvolvedor de backend

## Conteúdo de vídeo

* Copie `.my.cnf.example` para `.my.cnf` e crie uma nova seção chamada para sua conexão de origem.
* Defina a ID do projeto em `.my.cnf` se a origem for Adobe Commerce as a Cloud Service (PaaS).
* Use os comandos de túnel da CLI da Magento Cloud para obter os valores de host, usuário, senha, porta e banco de dados.
* Confirme a conectividade de host e porta antes de executar a ferramenta, se a origem estiver no local.

>[!VIDEO](https://video.tv.adobe.com/v/3496152?learn=on)
