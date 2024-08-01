---
title: Integração da última milha no kit inicial de integração do Commerce.
description: Integração do último quilômetro no Commerce, destacando os ganchos de extensibilidade como validação, transformação, pré-processamento, envio e pós-processamento.​
landing-page-description: Saiba mais sobre a estrutura e as funções dos ganchos de extensibilidade na integração de última milha para sistemas Commerce.
kt: 15869
doc-type: video
duration: 465
audience: all
last-substantial-update: 2024-7-30
feature: Best Practices, Backend Development, Integration
topic: Architecture, Commerce, Development
role: Architect, Developer
level: Intermediate
source-git-commit: aed143b96f13a413f85fc461e11f358b4c657015
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Integração do último quilômetro usando o Adobe Starter Kit

Saiba mais sobre os itens a serem considerados ao iniciar a integração de última milha com o Adobe Commerce, com foco no uso de ganchos de extensibilidade para melhorar a conectividade com sistemas de terceiros. Este vídeo descreve uma abordagem estruturada em que vários ganchos, como validação, transformação, pré-processamento, envio e pós-processamento, garantem o fluxo de dados e a sincronização do sistema perfeitos. Cada gancho tem um propósito distinto, incluindo:

* Validação de dados de entrada em relação a esquemas
* Transformando objetos de dados entre sistemas
* Realização de cálculos antes do envio de informações relevantes
* Envio dos dados para o sistema de destino

É importante manter arquivos JavaScript separados para cada bloco para manter a integridade da lógica de negócios e facilitar atualizações futuras da estrutura, garantindo uma configuração de integração robusta e adaptável.

Saiba mais sobre a importância das atividades de pós-processamento por meio do gancho pós-processo, que permite que os usuários executem ações adicionais após a sincronização de dados, como adicionar comentários a pedidos ou armazenar IDs externas. O vídeo inclui práticas recomendadas como encapsular solicitações de API em bibliotecas específicas para simplificar conexões com sistemas de terceiros. Você também aprenderá casos de uso típicos para cada gancho e orientações sobre como lidar com diferentes cenários.

## Público-alvo

* Desenvolvedores que desejam conhecer a estrutura e a funcionalidade dos ganchos de extensibilidade e como esses ganchos podem melhorar a conectividade com sistemas de terceiros.
* Desenvolvedores que desejam conhecer os casos de uso típicos e as práticas recomendadas associadas a cada gancho de extensibilidade, como validação, transformação, pré-processamento, envio e pós-processamento, para facilitar o fluxo de dados contínuo, a sincronização do sistema e a manutenção eficiente da configuração de integração. &#x200B;

## Conteúdo de vídeo

* Saiba mais sobre a estrutura das ações invocadas na integração de última milha.
* Entenda os casos de uso típicos no gancho de validação, incluindo a validação de dados de entrada em relação a esquemas e a omissão de eventos específicos com base em determinados critérios. &#x200B;
* Saiba mais sobre a função do gancho de transformação na transformação de objetos de dados entre os sistemas de origem e destino.
* Saiba mais sobre o significado do gancho de envio para facilitar o envio de dados reais para o sistema de destino.

>[!VIDEO](https://video.tv.adobe.com/v/3431692?learn=on)

{{$include /help/_includes/starter-kit-related-links.md}}
