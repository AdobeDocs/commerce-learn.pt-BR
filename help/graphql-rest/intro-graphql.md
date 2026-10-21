---
title: Introdução ao GraphQL
description: Saiba como usar o GraphQL no Adobe Commerce e no [!DNL Magento Open Source]. Use chamadas GET e POST do GraphQL para Adobe Commerce e [!DNL Magento Open Source].
short-description: Saiba como usar chamadas GET e POST do GraphQL para Adobe Commerce e [!DNL Magento Open Source].
kt: 11524
doc-type: video
duration: 286
audience: all
last-substantial-update: 2023-10-12T00:00:00.000Z
feature: GraphQL
topic: Commerce, Architecture, Headless
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 7516911fc14bc80f327310b99a00f9cbff7c65c7
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 6%
---
# Introdução ao GraphQL

Esta é a parte 1 da série para GraphQL e Adobe Commerce. O GraphQL tornou-se rapidamente o padrão do setor para a forma como aplicativos avançados do lado do cliente se comunicam com um back-end. É um tópico cada vez mais relevante para desenvolvedores do Adobe Commerce, já que a plataforma continua a expandir seus recursos no domínio de implementações headless.

Se você é novo no GraphQL, esta seção o orienta para os conceitos e o uso básicos.

>[!VIDEO](https://video.tv.adobe.com/v/3443946?captions=por_br&learn=on)

## Vídeos e tutoriais relacionados ao GraphQL nesta série

* [Parte 2 GraphQL - Consultas](../graphql-rest/graphql-queries.md)
* [Parte 3 GraphQL - Mutações](../graphql-rest/graphql-mutations.md)
* [GraphQL Parte 4 - Esquema](../graphql-rest/graphql-schema.md)

## O que é o GraphQL?

O GraphQL é uma especificação para uma linguagem de consulta de API exclusiva e o tempo de execução que fornece dados em resposta a essa linguagem de consulta.

As APIs da Web tradicionais, como REST, têm funcionado bem para sistemas diferentes que transmitem dados de um lado para o outro, mas fornecem menos do que o desempenho máximo para experiências modernas de link de aplicativo, como Aplicativos Web progressivos. Em aplicativos como este, as camadas front-end e back-end do _mesmo_ aplicativo se comunicam por meio da API da Web. A abordagem regimentada de esquemas como REST muitas vezes não fornece a flexibilidade apropriada neste contexto, onde muitos tipos de dados precisam ser buscados rapidamente.

O GraphQL permite que um cliente descreva _exatamente_ os dados de que precisa. Em vez de exigir várias solicitações de rede para buscar vários tipos de dados, uma única solicitação pode consultar muitos tipos. E as respostas são mantidas em ordem, incluindo (em um formato que espelha intuitivamente o query) somente os tipos e campos que são solicitados.

O tempo de execução que implementa a especificação do GraphQL pode ser construído em qualquer idioma. Adobe Commerce e [!DNL Magento Open Source] usam o
[graphql-php](https://webonyx.github.io/graphql-php/){target="_blank"} implementação do PHP e constrói suas próprias camadas sobre ele.

[Exibir a documentação completa do GraphQL](https://graphql.org/learn){target="_blank"}

## Uso de um cliente do GraphQL

Você precisa de um cliente GraphQL GUI para testar amostras de código e tutoriais. Há várias opções:

* O [Altair](https://altairgraphql.dev/){target="_blank"} é um cliente excelente e completo criado especificamente para o GraphQL. O Adobe usa Altair em vídeos passo a passo.
* Se você não quiser instalar o aplicativo de desktop, também há extensões Altair executadas diretamente em seu
  [Chrome](https://chromewebstore.google.com/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox ou navegador [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"}.
* O [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} é uma implementação do GraphQL IDE da GraphQL Foundation. Essa não é uma ferramenta instalável, mas um pacote que você mesmo pode usar para criar a interface.
* Se você já conhece o [Postman](https://www.postman.com/){target="_blank"}, ele oferece um suporte adequado para consultas do GraphQL, embora não seja tão completo quanto um cliente dedicado do GraphQL.

No cliente do GraphQL, você deve enviar suas solicitações para o caminho de URL `/graphql` na sua instância do Adobe Commerce ou do [!DNL Magento Open Source]. Se preferir usar uma instância existente para seus testes, use a demonstração do tema Venia (exemplo de implementação do PWA Studio): `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}
