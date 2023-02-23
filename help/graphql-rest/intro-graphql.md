---
title: Introdução ao GraphQL
description: Saiba como usar o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Usar chamadas de GET e POST para GraphQL para Adobe Commerce e [!DNL Magento Open Source].
landing-page-description: Saiba como usar o GraphQL no Adobe Commerce e [!DNL Magento Open Source]. Usar chamadas de GET e POST para GraphQL para Adobe Commerce e [!DNL Magento Open Source].
kt: 11524
doc-type: tutorial
audience: all
last-substantial-update: 2022-12-13T00:00:00Z
exl-id: 8ea823da-24a3-4627-885c-4b3279b9142c
source-git-commit: ef3dd7aaa409d9c1bc30d3d9c225966d8c1ace9e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Introdução ao GraphQL

A GraphQL tornou-se rapidamente o padrão do setor para o poder dos aplicativos do lado do cliente conversarem com um back-end. É um tópico cada vez mais relevante para os desenvolvedores do Adobe Commerce, à medida que a plataforma continua a expandir seus recursos no domínio de implementações sem periféricos.

Se você é novo no GraphQL, esta seção orienta você aos conceitos e ao uso básicos.

## O que é o GraphQL?

O GraphQL é uma especificação para um idioma exclusivo de consulta de API e o tempo de execução que fornece dados em resposta a esse idioma de consulta.

As APIs tradicionais da Web, como REST, serviram bem para sistemas diferentes transmitindo dados de um lado para o outro, mas forneceram menos do que o desempenho máximo para experiências modernas de link de aplicativo, como o Progressive Web Application. Em aplicativos como esse, as camadas de front-end e back-end da variável _same_ O aplicativo se comunica por meio da API da Web. A abordagem regimentada de esquemas como o REST frequentemente não proporciona a flexibilidade adequada neste contexto, onde muitos tipos de dados precisam ser buscados rapidamente.

O GraphQL permite que um cliente descreva de maneira expressiva _exatamente_ os dados de que necessita. Em vez de exigir várias solicitações de rede para buscar vários tipos de dados, uma única solicitação pode consultar vários tipos. E as respostas são mantidas inativas ao incluir (em um formato que reflete intuitivamente a query) somente os tipos e campos solicitados.

O tempo de execução que implementa a especificação do GraphQL pode ser criado em qualquer idioma. Adobe Commerce e [!DNL Magento Open Source] use o
[grafql-php](https://webonyx.github.io/graphql-php/){target="_blank"} A implementação do PHP e cria suas próprias camadas sobre ela.

[Exibir a documentação completa do GraphQL](https://graphql.org/learn){target="_blank"}

## Usar um cliente do GraphQL

Você precisa de um cliente GUI GraphQL para testar amostras de código e tutoriais. Há várias opções:

* [Altair](https://altairgraphql.dev/){target="_blank"} O é um cliente excelente e completo criado especificamente para a GraphQL. O Adobe usa o Altair em vídeos de apresentação.
* Se você não quiser instalar o aplicativo de desktop, também há extensões Altair que são executadas diretamente no seu
   [Cromo](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja){target="_blank"}, Firefox, or [Edge](https://microsoftedge.microsoft.com/addons/detail/altair-graphql-client/kpggioiimijgcalmnfnalgglgooonopa){target="_blank"} navegador.
* [GraphiQL](https://github.com/graphql/graphiql/tree/main/packages/graphiql){target="_blank"} O é uma implementação do GraphQL IDE da GraphQL Foundation. Esta não é uma ferramenta instalável, mas um pacote que você pode usar para criar a interface.
* Se já estiver familiarizado com [Postman](https://www.postman.com/){target="_blank"}, ele tem suporte adequado para consultas do GraphQL, embora não seja tão apresentado como um cliente GraphQL dedicado.

No cliente do GraphQL, você deve enviar suas solicitações para o caminho do URL `/graphql` na Adobe Commerce ou [!DNL Magento Open Source] instância. Se preferir usar uma instância existente para seus testes, você pode usar a demonstração do tema Venia (o exemplo de implementação do PWA Studio): `https://venia.magento.com/graphql`

{{$include /help/_includes/graphql-rest-related-links.md}}
