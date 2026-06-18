---
title: Configurar, implantar e personalizar um Webhook de assimilação
description: Saiba como configurar, implantar e personalizar um webhook de assimilação para conectar o Adobe Commerce a um sistema de back office de terceiros e lidar com a tradução de eventos.
doc-type: Technical Video
duration: 697
last-substantial-update: 2024-07-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Developer
level: Intermediate
jira: KT-15870
exl-id: f2654873-256e-4c1b-abed-8bfbc4db3fbb
TQID: https://experienceleague.adobe.com/nUXdrsjzeD939jOjZS8ywPV3OeOaxpZCmeuveACtYrY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 9568f37b026d0e659e8092282cb923c7ecde58ac
workflow-type: tm+mt
source-wordcount: 412
ht-degree: 0%

---

# Configurar, implantar e personalizar um webhook de assimilação

Saiba mais sobre a configuração e personalização de um webhook de assimilação para integrar o Commerce com um sistema de back office de terceiros.&#x200B; Este vídeo explica como o webhook pode resolver limitações na comunicação de eventos entre sistemas, fornecendo um terminal disponível publicamente para adaptar mensagens do sistema de terceiros à API de evento do Adobe IO. O processo envolve a configuração do webhook no arquivo `actions.config.yaml`, sua habilitação no arquivo `app.config.yaml` e sua implantação para garantir a funcionalidade adequada.

O vídeo aborda as etapas para modificar o código do webhook para traduzir eventos de terceiros em formatos compatíveis com os tipos de evento inscritos da integração. Ele discute a adição de um arquivo `event-mapping.json` para facilitar essa tradução e enfatiza a importância de reimplantar a ação de tempo de execução após fazer alterações.&#x200B; O vídeo também destaca a importância de validar e transformar cargas de evento recebidas para alinhar-se ao esquema esperado, garantindo um processamento bem-sucedido e a integração com a API do Commerce para criar clientes.

## Público-alvo

* Desenvolvedores que desejam configurar um webhook de assimilação
* Qualquer pessoa que quiser personalizar o código para tradução de eventos
* Desenvolvedores e arquitetos que desejam entender a importância da autenticação e do gerenciamento de conteúdo

## Conteúdo de vídeo

* Configuração e implantação: o vídeo enfatiza a importância de configurar o webhook de assimilação no arquivo `actions.config.yaml` e habilitá-lo no arquivo `app.config.yaml`. Ele também destaca a necessidade de reimplantar o projeto depois de fazer alterações para garantir que o webhook funcione corretamente.
* Personalização para compatibilidade: é fundamental personalizar o código do webhook para traduzir eventos de terceiros em formatos que se alinhem aos tipos de evento inscritos da integração. &#x200B; Essa personalização garante uma comunicação perfeita entre os sistemas e o processamento bem-sucedido de eventos.
* Implementação de autenticação: as empresas são responsáveis por implementar mecanismos de autenticação adequados às suas necessidades para evitar solicitações não autorizadas ao usar o webhook de assimilação. Essa etapa é essencial para manter a segurança e a integridade da integração.
* Validação e transformação de carga útil: validar e transformar cargas de evento recebidas para corresponder ao esquema esperado é essencial para o processamento e a integração bem-sucedidos com a API do Commerce. &#x200B; Ao cortar e mapear campos adequadamente, a integração pode operar com eficiência com os dados necessários.

>[!VIDEO](https://video.tv.adobe.com/v/3431694?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Amostras de código

* [Webhook de assimilação personalizada](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/customize-ingestion-webhook)
* [Adicionar programador de assimilação](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler)
