---
title: Redefina o URI do administrador usando a CLI
description: Saiba como redefinir o URI do administrador na CLI do Adobe Commerce Cloud. Esse método é útil quando alterações no URL do administrador causam problemas de acesso.
feature: Admin Workspace, Console
topic: Administration, Commerce
role: Developer, User
level: Beginner
doc-type: Technical Video
duration: 144
last-substantial-update: 2024-10-14T00:00:00.000Z
jira: KT-16338
exl-id: dbc155d7-8ce9-4622-abfb-1d8077c3a975
TQID: https://experienceleague.adobe.com/OgyaTHVhQSRFApJPYwkzodSyAJcBjwk8kIrw4VBXltQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 107
ht-degree: 0%

---

# Redefina o URI do administrador usando a cli

Saiba como redefinir o URI do administrador usando o comando da cli do Adobe Commerce Cloud. Isso é útil se o URL do administrador tiver sido alterado, mas um erro tiver sido cometido e você não puder mais acessar o administrador.

>[!VIDEO](https://video.tv.adobe.com/v/3439697?captions=por_br&learn=on)

## Alguns comandos usados no tutorial

Altere a configuração para esperar um URL de caminho de administrador personalizado para 0:

`$ php bin/magento config:set admin/url/use_custom 0`

Altere a configuração do URL do caminho personalizado do administrador para 0

`$ php bin/magento config:set admin/url/use_custom_path 0`
