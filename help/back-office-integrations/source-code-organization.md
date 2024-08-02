---
title: Saiba mais sobre o Commerce Integration Starter Kit com as principais pastas e scripts de automação explicados
description: Saiba mais sobre a organização do código-fonte no kit inicial de integração do Commerce. ​
landing-page-description: Explorar a organização do código Source em um kit inicial de integração do Commerce
kt: 15868
doc-type: video
duration: 420
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: f0c6e9262a2bf2de3144255de1fc78d6972b6d33
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# Organização do código Source para o Adobe Starter Kit

Saiba mais sobre a organização do código-fonte no kit inicial de integração do Adobe Commerce.&#x200B; Explore a estrutura do projeto, destacando as pastas principais como `actions` e `scripts` e seus respectivos conteúdos.&#x200B; A pasta &quot;ações&quot; contém subpastas como `ingestion` e `webhook` que contêm código essencial para manipulação e rastreamento de eventos. Você também aprenderá sobre as pastas `starter-kit-info` e `scripts`. A pasta `scripts` foca em scripts de automação como `commerce-event-subscribe` e `onboarding` que otimizam a configuração de eventos e a configuração de provedores no projeto.
&#x200B;
Explore a lógica por trás da estrutura do código-fonte, detalhando como as pastas `commerce` e `external` em cada pasta de entidade lidam com eventos originados de sistemas diferentes. O vídeo explica a função da pasta `consumer` em despachar eventos para a ação de tempo de execução apropriada do manipulador de eventos, garantindo um processamento contínuo. O vídeo também aborda o mecanismo de repetição implementado nas ações de tempo de execução para lidar com eventos de falha de maneira eficaz. &#x200B;Entenda a organização e a funcionalidade do código-fonte no kit inicial da Integração do Adobe Commerce, oferecendo informações valiosas sobre manipulação de eventos, scripts de automação e configurações.

## Público-alvo

* Desenvolvedores que desejam entender como o código-fonte é organizado em pastas chave como `actions` e `scripts`.
* Saiba mais sobre a pasta `actions` que contém subpastas como `ingestion` e ` webhook`, que contêm código essencial para manipular eventos e rastrear implantações.
* Desenvolvedores que desejam saber mais sobre a pasta `actions` que inclui pastas para entidades como `customer`, `order`, `product` e `stock`.

## Conteúdo de vídeo

* Entenda que as quatro pastas principais: `actions`, `scripts`, `test` e `utils`, com foco nas pastas `actions` e `scripts` durante a sessão. &#x200B;
* Saiba mais sobre a pasta `actions` e como ela contém subpastas cruciais como `ingestion` e `webhook`.
* Explore a pasta `actions` e o motivo de haver pastas específicas para entidades como `customer`, `order`, `product` e `stock`, cada uma contendo ações de tempo de execução estruturadas em pastas `commerce` e `external` para gerenciar eventos do Commerce e de sistemas de terceiros de maneira eficaz. &#x200B;
* Saiba mais sobre a importância de não alterar o código na pasta `starter-kit-info`, que contém uma ação de tempo de execução usada pelo Adobe para rastrear as implantações do projeto com base no kit inicial. &#x200B;
* Entenda a pasta `scripts` que contém scripts de automação como `commerce-event-subscribe` e `onboarding`, que automatizam a configuração de eventos, a configuração de provedores e a configuração do módulo Adobe I/O Events no Commerce. &#x200B;

  >[!VIDEO](https://video.tv.adobe.com/v/3431691?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}
