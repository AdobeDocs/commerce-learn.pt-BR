---
title: Adicionar uma tabela a um banco de dados
description: "[!DNL Commerce] O tem um mecanismo especial que permite criar tabelas de banco de dados, modificar tabelas existentes e até mesmo adicionar alguns dados a elas."
topic: Development
kt: 5613
doc-type: video
activity: use
exl-id: fb222752-5689-4f87-94cf-a61ed7005e6b
source-git-commit: e8d2631b31319701beb327f42fdf1372d9dad9b7
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Adicionar uma tabela a um banco de dados

>[!IMPORTANT]
>
>Isso não é mais recomendado, consulte https://developer.adobe.com/commerce/php/development/components/declarative-schema/


[!DNL Commerce] O tem um mecanismo especial que permite criar tabelas de banco de dados, modificar tabelas existentes e até mesmo adicionar alguns dados a elas, como dados de configuração, que devem ser adicionados quando um módulo é instalado. Esse mecanismo permite que essas alterações sejam transferíveis entre diferentes instalações.

Em vez de realizar operações SQL manuais repetidamente ao reinstalar o sistema, os desenvolvedores criam um script de instalação (ou atualização) que contém os dados. O script é executado sempre que um módulo é instalado.

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

- [Migrar scripts de instalação/atualização para esquema declarativo](https://developer.adobe.com/commerce/php/development/components/declarative-schema/migration-scripts/)
