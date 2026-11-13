---
title: Ferramenta de Migração de Dados em Massa - Credenciais do BD
description: Saiba como configurar a conexão do banco de dados de origem em seu arquivo .my.cnf usando a Magento Cloud CLI ou uma ID de projeto antes de executar a ferramenta de migração.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 161
last-substantial-update: 2026-07-21
jira: KT-22105
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 8d1fc3f2db752369487199175fb99a4e9db34b19
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
