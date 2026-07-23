---
title: O arquivo app.config.yaml
description: Saiba como o arquivo app.config.yaml determina a configuração do aplicativo e como suas definições são vinculadas aos arquivos do JavaScript no aplicativo de amostra do Adobe Developer App Builder.
jira: KT-12929
doc-type: Tutorial
duration: 136
last-substantial-update: 2023-03-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
exl-id: ff5f1811-ca93-494e-8e5c-a5e0c7bb673d
TQID: https://experienceleague.adobe.com/iK4PPaI2-vxQK32DMfkMRZMgNYpLExMbNge2lXIJzLg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 3f243b43695e65d63cb25142ec5a886ce390d502
workflow-type: tm+mt
source-wordcount: 96
ht-degree: 0%

---

# Descrição e uso do arquivo app.config.yaml {#app-config-yaml}

Esse arquivo determina a configuração do aplicativo.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce com experiência limitada no Adobe App Builder que estão aprendendo sobre o `app.config.yaml` no aplicativo de amostra.

## Conteúdo de vídeo

* O arquivo `app.config.yaml` foi discutido
* Como as definições estão vinculadas a outros arquivos do `.js`

>[!VIDEO](https://video.tv.adobe.com/v/3430848?captions=por_br&learn=on)

## Amostra de código

```bash
# Specify your secrets here
# This file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can also include commerce OAuth credentials, our sample module will use the following example credentials:
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Você pode ver esses valores estáticos sendo usados no módulo de exemplo no arquivo `actions/commerce.index.js`

```javascript
        const oauth = getCommerceOauthClient(
            {
                url: params.COMMERCE_BASE_URL,
                consumerKey: params.COMMERCE_CONSUMER_KEY,
                consumerSecret: params.COMMERCE_CONSUMER_SECRET,
                accessToken: params.COMMERCE_ACCESS_TOKEN,
                accessTokenSecret: params.COMMERCE_ACCESS_TOKEN_SECRET
            },
            logger
        )
```

{{$include /help/_includes/app-builder-first-app-related-links.md}}

