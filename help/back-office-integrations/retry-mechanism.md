---
title: Usar a funcionalidade nativa de um mecanismo de repetição
description: Saiba como usar o mecanismo de repetição do Adobe I/O Events para criar aplicativos resilientes, cobrindo condições de repetição, estratégias de retirada e indicadores visuais.
doc-type: Technical Video
duration: 402
last-substantial-update: 2024-07-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Developer
level: Intermediate
jira: KT-15872
exl-id: 412060b3-76ae-4c27-bf96-8eb2a0f0d0e8
TQID: https://experienceleague.adobe.com/hrzcmSY8cAke4LBLRtqfkP8-t6jP4KMoMc7iL3WPRng
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 9568f37b026d0e659e8092282cb923c7ecde58ac
workflow-type: tm+mt
source-wordcount: 382
ht-degree: 0%

---

# Usar o mecanismo de repetição do Adobe I/O Events para resiliência de aplicativos

O vídeo descreve um guia abrangente sobre como aproveitar o mecanismo de repetição integrado do Adobe I/O Events para melhorar a resiliência dos aplicativos. Saiba como códigos de status de resposta HTTP específicos acionam novas tentativas de evento. O Adobe I/O Events emprega estratégias de recuo exponenciais e fixas para tentativas, com intervalos que aumentam de um minuto a 15 minutos. A documentação também detalha como os indicadores de repetição são exibidos no console do desenvolvedor, com dicas visuais como ícones de aviso e setas circulares que indicam eventos de falha e de repetição, respectivamente.

Saiba como o mecanismo de repetição funciona no contexto das ações de tempo de execução &quot;consumidor&quot; e determine se um evento é repetido. As respostas bem-sucedidas são indicadas com um código de status 200, enquanto as respostas de erro incluem um objeto de erro com um atributo &quot;statusCode&quot;. A ação de tempo de execução &quot;consumidor&quot; determina o código de resposta HTTP a ser retornado com base nos resultados de processamento downstream, garantindo um tratamento eficiente de eventos e eventuais ativações bem-sucedidas.

## Público-alvo

* Desenvolvedores que desejam entender os códigos de status de resposta HTTP específicos que acionam novas tentativas de evento.
* Equipes que desejam aprender sobre as estratégias de retrocesso exponencial e fixo empregadas pelo Adobe I/O Events para tentativas.
* Desenvolvedores que desejam entender como os indicadores visuais no console do desenvolvedor representam eventos com falha e repetidos.

## Conteúdo de vídeo

* O Adobe I/O Events tem um mecanismo de repetição integrado e pronto para uso que repete automaticamente as ativações de eventos com base em códigos de status de resposta HTTP específicos.
* O mecanismo de repetição implementado pelo Adobe I/O Events envolve estratégias de retrocesso exponenciais e fixas.
* Indicadores visuais no console do desenvolvedor, como ícones de aviso para eventos com falha e ícones de seta circulares para eventos repetidos.
* As ações de tempo de execução &quot;consumidor&quot; desempenham um papel crucial na determinação dos códigos de status de resposta HTTP apropriados para a manipulação de eventos.

>[!VIDEO](https://video.tv.adobe.com/v/3449078?captions=por_br&learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Documentação relacionada

* [O Webhook não pode manipular um evento](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [Webhook inativo e marcado como instável](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)
