---
title: Redefina o URI do administrador usando a CLI
description: Saiba como redefinir o URI do administrador na CLI do Adobe Commerce Cloud. Esse método é útil quando alterações no URL do administrador causam problemas de acesso.
feature: Admin Workspace, Console
topic: Administration, Commerce
role: Developer, User
level: Beginner
doc-type: Technical Video
duration: 123
last-substantial-update: 2024-10-14T00:00:00Z
jira: KT-16338
exl-id: dbc155d7-8ce9-4622-abfb-1d8077c3a975
source-git-commit: 25ee35b730cc6265665a87c9c37d24e88c41b60e
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Redefina o URI do administrador usando a cli

Saiba como redefinir o URI do administrador usando o comando da cli do Adobe Commerce Cloud. Isso é útil se o URL do administrador tiver sido alterado, mas um erro tiver sido cometido e você não puder mais acessar o administrador.

>[!VIDEO](https://video.tv.adobe.com/v/3435066/?learn=on)

## Alguns comandos usados no tutorial

Altere a configuração para esperar um URL de caminho de administrador personalizado para 0:

`$ php bin/magento config:set admin/url/use_custom 0`

Altere a configuração do URL do caminho personalizado do administrador para 0

`$ php bin/magento config:set admin/url/use_custom_path 0`
