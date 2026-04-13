---
title: O arquivo app.config.yaml
description: Saiba mais sobre os tipos de arquivos no arquivo app.config.yaml para este aplicativo de amostra.
jira: KT-12929
doc-type: Tutorial
duration: 136
last-substantial-update: 2023-03-13T00:00:00Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
exl-id: ff5f1811-ca93-494e-8e5c-a5e0c7bb673d
source-git-commit: 82c30f9cce110c2315822fe236c06a6fc33d54bf
workflow-type: tm+mt
source-wordcount: '86'
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
