---
title: O arquivo .env
description: Saiba como gerar e configurar o arquivo .env para seu aplicativo do Adobe Developer App Builder, incluindo o gerenciamento de segredos e a prevenção de confirmações acidentais no controle de origem.
jira: KT-21681
doc-type: Tutorial
duration: 177
last-substantial-update: 2023-03-13T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
exl-id: 934fcdd1-ee61-4914-89ce-f6f04b1bc763
TQID: https://experienceleague.adobe.com/Sup5quVNU60RYmkCJaYGgLq2gHCpCvaIKEFLH2MAifQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: e03f0a058d1a08b1a67fd278c1b6127566a370ac
workflow-type: tm+mt
source-wordcount: 147
ht-degree: 0%

---

# Gerar e configurar o arquivo .env {#env-file}

O `.env` é um arquivo especial que não faz parte do módulo de amostra, mas é importante para uso no aplicativo Adobe Developer App Builder. Esse arquivo contém segredos e outras informações. Evite confirmar esse arquivo em qualquer repositório de código.

## Para quem é este vídeo?

* Desenvolvedores novatos no Adobe Commerce com experiência limitada usando o Adobe App Builder que desejam aprender sobre o arquivo `.env`.

## Conteúdo de vídeo

* Introdução ao arquivo .env e sua finalidade
* Como gerar o arquivo .env
* Para adicionar novos segredos, anexe o arquivo
* Evite confirmar este arquivo porque ele contém informações confidenciais

>[!VIDEO](https://video.tv.adobe.com/v/3416593?learn=on)

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
