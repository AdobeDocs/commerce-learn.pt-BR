---
title: O arquivo app.config.yaml
description: Saiba mais sobre os tipos de arquivos no arquivo app.config.yaml para este aplicativo de exemplo.
landing-page-description: Saiba mais sobre o Adobe Developer App Builder usado com o Adobe Commerce e quais tipos de arquivos estão no app.config.yaml.
kt: 12426
doc-type: tutorial
audience: all
last-substantial-update: 2023-03-13T00:00:00Z
source-git-commit: e0371a8cefab0141318daa0e1be42bfbb9e5b608
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Descrição e uso do arquivo app.config.yaml {#app-config-yaml}

Esse arquivo determina a configuração do aplicativo.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce com experiência limitada com o Adobe App Builder que estão aprendendo sobre o `app.config.yaml` no aplicativo de amostra.

## Conteúdo de vídeo

* O `app.config.yaml` arquivo discutido
* Como as definições estão vinculadas a outras `.js` arquivos

>[!VIDEO](https://video.tv.adobe.com/v/3416592)

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

Você pode ver esses valores estáticos sendo usados no módulo de amostra no arquivo `actions/commerce.index.js`

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