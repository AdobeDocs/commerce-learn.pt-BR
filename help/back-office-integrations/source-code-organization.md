---
title: Organização do código Source no kit inicial do Commerce
description: Saiba mais sobre a organização do código-fonte no kit inicial de integração do Commerce, incluindo pastas principais como ações e scripts, scripts de automação e manipulação de eventos.
doc-type: Technical Video
duration: 534
last-substantial-update: 2024-07-30T00:00:00.000Z
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Developer
level: Intermediate
jira: KT-15868
exl-id: 678f4d2b-c57e-4afb-a535-1048a88bc3b1
TQID: 'https://experienceleague.adobe.com/P6-sK18TcpC91YXJcXohIvzmii3N66ZKh3nZha-RYQY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: b48dbafb-4193-5648-b9d9-bf96e9c9a411
    internal-label: Backend Development
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%
---
# Organização do código Source para o Adobe Starter Kit

Saiba mais sobre a organização do código-fonte no kit inicial da Integração do Adobe Commerce.&#x200B; Explore a estrutura do projeto, destacando as principais pastas, como `actions` e `scripts`, e seus respectivos conteúdos.&#x200B; A pasta &quot;ações&quot; contém subpastas, como `ingestion` e `webhook`, que contêm código essencial para a manipulação e o rastreamento de eventos. Você também aprenderá sobre as pastas `starter-kit-info` e `scripts`. A pasta `scripts` foca em scripts de automação como `commerce-event-subscribe` e `onboarding` que otimizam a configuração de eventos e a configuração de provedores no projeto.
&#x200B;
Explore a lógica por trás da estrutura do código-fonte, detalhando como as pastas `commerce` e `external` em cada pasta de entidade lidam com eventos originados de sistemas diferentes. O vídeo explica a função da pasta `consumer` em despachar eventos para a ação de tempo de execução apropriada do manipulador de eventos, garantindo um processamento contínuo. O vídeo também aborda o mecanismo de repetição implementado nas ações de tempo de execução para lidar com eventos de falha de maneira eficaz. &#x200B;Entenda a organização e a funcionalidade do código-fonte no kit inicial da Integração do Adobe Commerce, oferecendo insights valiosos sobre manipulação de eventos, scripts de automação e configurações.

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
