---
title: Configurar, implantar e personalizar um Webhook de assimilação
description: Saiba como configurar e personalizar um webhook de assimilação para facilitar a comunicação entre o Commerce e um sistema de back office de terceiros.
landing-page-description: Saiba como usar o Commerce Integration Starter Kit para integrar o Commerce a um sistema de back-office de terceiros usando um webhook de assimilação.
kt: 15870
doc-type: video
duration: 593
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: 45c018813ed8d5487e1491e09afc34e2de39c5b2
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Configurar, implantar e personalizar um webhook de assimilação

Saiba mais sobre a configuração e personalização de um webhook de assimilação para integrar o Commerce a um sistema de back office de terceiros&#x200B; Este vídeo explica como o webhook pode lidar com limitações na comunicação de eventos entre sistemas, fornecendo um endpoint disponível publicamente para adaptar mensagens do sistema de terceiros para a API de evento do Adobe IO. O processo envolve a configuração do webhook no arquivo `actions.config.yaml`, sua habilitação no arquivo `app.config.yaml` e sua implantação para garantir a funcionalidade adequada.

O vídeo aborda as etapas para modificar o código do webhook para traduzir eventos de terceiros em formatos compatíveis com os tipos de evento inscritos da integração. Ele discute a adição de um arquivo `event-mapping.json` para facilitar essa tradução e enfatiza a importância de reimplantar a ação de tempo de execução depois de fazer alterações&#x200B; O vídeo também destaca a importância de validar e transformar cargas de evento recebidas para alinhar-se ao esquema esperado, garantindo o processamento e a integração bem-sucedidos com a API do Commerce para criar clientes.

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
* [Adicionar agendador de assimilação](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit/add-ingestion-scheduler)
