---
title: Usar a funcionalidade nativa de um mecanismo de repetição
description: Aproveite o mecanismo de repetição do Adobe I/O Events para aplicativos resilientes, incluindo condições de repetição e indicadores visuais.
landing-page-description: Entenda e utilize o mecanismo de repetição integrado do Adobe I/O Events para aprimorar a resiliência dos aplicativos e gerenciar as ativações de eventos com eficiência.
kt: 15872
doc-type: video
duration: 314
audience: all
last-substantial-update: 2024-7-31
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer
level: Intermediate
exl-id: 412060b3-76ae-4c27-bf96-8eb2a0f0d0e8
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Aproveitar o mecanismo de repetição do Adobe I/O Events para resiliência de aplicativos

O vídeo descreve um guia abrangente sobre como aproveitar o mecanismo de repetição integrado do Adobe I/O Events para melhorar a resiliência dos aplicativos. Saiba como códigos de status de resposta HTTP específicos acionam novas tentativas de evento. O Adobe I/O Events emprega estratégias de recuo exponenciais e fixas para tentativas, com intervalos que aumentam de um minuto a 15 minutos. A documentação também detalha como os indicadores de repetição são exibidos no console do desenvolvedor, com dicas visuais como ícones de aviso e setas circulares que indicam eventos de falha e de repetição, respectivamente.

Saiba como o mecanismo de repetição funciona no contexto das ações de tempo de execução &quot;consumidor&quot; e determine se um evento é repetido. As respostas bem-sucedidas são indicadas com um código de status 200, enquanto as respostas de erro incluem um objeto de erro com um atributo &quot;statusCode&quot;. A ação de tempo de execução &quot;consumidor&quot; determina o código de resposta HTTP a ser retornado com base nos resultados de processamento downstream, garantindo um tratamento eficiente de eventos e eventuais ativações bem-sucedidas.

## Público-alvo

* Desenvolvedores que desejam entender os códigos de status de resposta HTTP específicos que acionam novas tentativas de evento.
* Equipes que desejam aprender sobre as estratégias de retrocesso exponencial e fixo empregadas pelo Adobe I/O Events para tentativas.
* Desenvolvedores que desejam entender como os indicadores visuais no console do desenvolvedor representam eventos com falha e repetidos.

## Doente de vídeo

* O Adobe I/O Events tem um mecanismo de repetição integrado e pronto para uso que repete automaticamente as ativações de eventos com base em códigos de status de resposta HTTP específicos.
* O mecanismo de repetição implementado pelo Adobe I/O Events envolve estratégias de retrocesso exponenciais e fixas.
* Indicadores visuais no console do desenvolvedor, como ícones de aviso para eventos com falha e ícones de seta circulares para eventos repetidos.
* As ações de tempo de execução &quot;consumidor&quot; desempenham um papel crucial na determinação dos códigos de status de resposta HTTP apropriados para a manipulação de eventos.

>[!VIDEO](https://video.tv.adobe.com/v/3431695?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}

## Documentação relacionada

* [O Webhook não pode manipular um evento](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-unable-to-handle-a-specific-event-but-handles-all-other-events-gracefully)
* [Webhook desativado e marcado como instável](https://developer.adobe.com/events/docs/support/faq/#what-happens-if-my-webhook-is-down-why-is-my-event-registration-marked-as-unstable)
