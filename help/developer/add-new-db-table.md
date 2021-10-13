---
title: Adicionar uma tabela a um banco de dados
description: '[!DNL Commerce] O tem um mecanismo especial que permite criar tabelas de banco de dados, modificar as existentes e até mesmo adicionar alguns dados a elas.'
topic: Development
kt: 5613
doc-type: video
activity: use
exl-id: fb222752-5689-4f87-94cf-a61ed7005e6b
source-git-commit: 1eb2cd22f9bded77032ad0ed43c3f2ca84879a69
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Adicionar uma tabela a um banco de dados

[!DNL Commerce] O tem um mecanismo especial que permite criar tabelas de banco de dados, modificar as existentes e até mesmo adicionar alguns dados a elas, como dados de configuração, que devem ser adicionados quando um módulo é instalado. Este mecanismo permite que essas alterações sejam transferíveis entre diferentes instalações.

Em vez de realizar operações manuais do SQL repetidamente ao reinstalar o sistema, os desenvolvedores criam um script de instalação (ou atualização) que contém os dados. O script é executado sempre que um módulo é instalado.

## Para quem é este vídeo?

- Desenvolvedores

## Conteúdo de vídeo

- Criar um módulo
- Criar script InstallSchema
- Criar script InstallData
- Adicionar novo módulo e verificar se uma tabela com dados foi criada
- Criar um script UpgradeSchema
- Criar um script UpgradeData
- Execute scripts de atualização e verifique se a tabela foi alterada

>[!VIDEO](https://video.tv.adobe.com/v/35791?quality=12&learn=on)

## Recursos úteis

- [Comandos de migração](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/declarative-schema/migration-commands.html)
