---
title: O arquivo .env
description: Saiba mais sobre os tipos de arquivos no arquivo .env para este aplicativo de amostra
landing-page-description: Saiba mais sobre o Adobe Developer App Builder usado com o Adobe Commerce e quais tipos de conteúdo são usados no arquivo .env
kt: 12423
doc-type: tutorial
audience: all
last-substantial-update: 2023-3-13
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 934fcdd1-ee61-4914-89ce-f6f04b1bc763
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# Gerar e configurar o arquivo .env {#env-file}

O `.env` é um arquivo especial que não faz parte do módulo de amostra, mas é importante para uso no aplicativo Adobe Developer App Builder. Esse arquivo contém segredos e outras informações. Evite confirmar esse arquivo em qualquer repositório de código.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce com experiência limitada usando o Adobe App Builder que desejam aprender sobre o arquivo `.env`.

## Conteúdo de vídeo

* Introdução ao arquivo .env e sua finalidade
* Como gerar o arquivo .env
* Como anexar o arquivo para adicionar novos segredos
* Evite confirmar este arquivo porque ele contém informações confidenciais

>[!VIDEO](https://video.tv.adobe.com/v/3416593?quality=12&learn=on)

## Amostra de código

```bash
# Specify your secrets here
# The .env file must not be committed to source control
## Adobe I/O Runtime credentials
AIO_runtime_auth=abcd1234-aaa-bbb-ccc-12345:Abcdd12345asdfadsfadsfee2323232323232
AIO_runtime_namespace=12345-someworkspace-stage
AIO_runtime_apihost=https://adobeioruntime.net
## Adobe I/O Console service account credentials (JWT) Api Key
SERVICE_API_KEY=

# You can include some commerce OAUTH credentials too, our sample module will use this
#COMMERCE_BASE_URL=https://somecommercewebsite.com/
#COMMERCE_CONSUMER_KEY=abcebdme5bvafnemk0mdeeiyfq123
#COMMERCE_CONSUMER_SECRET=ffff86sqws3pss5hhuofiqgq4t04rrr11
#COMMERCE_ACCESS_TOKEN=gdddfccronj098r4m04zyq773s5o64
#COMMERCE_ACCESS_TOKEN_SECRET=ggg7nb19jhr5gi9jzfan9ggzipe8yrus
```

Você pode ver esses valores estáticos sendo usados no módulo de exemplo no arquivo `actions/commerce.index.js`.

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
