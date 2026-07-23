---
title: Ferramenta de migração de dados em massa - Credenciais do Target
description: Saiba como definir os URLs da instância de destino, as credenciais do Adobe IMS e as configurações do CDMS no arquivo .env antes de executar a ferramenta Migração de dados em massa.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 226
last-substantial-update: 2026-07-21T00:00:00Z
jira: KT-22107
source-git-commit: b3c029f7c1080550900cbc5838478cd7a4137a20
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Configurar credenciais de destino para a Ferramenta de Migração de Dados em Massa

Defina as URLs da instância de destino, as credenciais do Adobe IMS e as configurações do CDMS no arquivo `.env` antes de executar a Ferramenta de migração de dados em massa. Verifique se o URL do Adobe IMS, o URL de destino e o host CDMS correspondem à mesma camada de ambiente — preparo ou produção.

## Para quem é este vídeo?

* Arquiteto de soluções
* Engenheiro de DevOps
* Desenvolvedor de backend

## Conteúdo de vídeo

* Defina as URLs REST e GraphQL da instância de destino e a ID do locatário de destino no arquivo `.env`, usando valores do painel de informações da instância em experience.adobe.com.
* Defina o URL do Adobe IMS para corresponder à camada (preparo ou produção) e à região do ambiente.
* Recupere a ID de cliente do Adobe IMS e o segredo do cliente do **Projeto** > **Servidor para servidor OAuth** na Adobe Developer Console.
* Copie a ID da organização de destino e defina as configurações de host, porta e servidor local do CDMS para corresponder ao seu ambiente.

>[!VIDEO](https://video.tv.adobe.com/v/3496171?captions=por_br&learn=on)
