---
title: Extensibilidade fora do processo para o Adobe Commerce
description: Saiba mais sobre o Construtor de aplicativos da Adobe e por que ele é um aspecto importante da extensibilidade fora do processo.
landing-page-description: Saiba o que é o Construtor de aplicativos e como ele pode ajudar com as estratégias de desenvolvimento do Adobe Commerce.
short-description: Saiba o que é o Construtor de aplicativos e como ele pode ajudar com as estratégias de desenvolvimento do Adobe Commerce.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-2-16
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Architect, Developer
level: Beginner, Intermediate
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: 241f99eaed68488b952e8ed76186499ca1a20417
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 6%

---

# Introdução ao App Builder

Historicamente, o desenvolvimento do Adobe Commerce tem usado extensibilidade no processo. O modelo em andamento requer que qualquer novo código seja compatível com as atualizações, a versão PHP do servidor e muitos outros aplicativos e serviços essenciais do servidor que o Commerce usa. O Adobe Developer App Builder usa extensibilidade fora do processo para evitar esses problemas de compatibilidade.

## App Builder para Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

O Adobe Developer App Builder é uma plataforma de extensibilidade sem servidor para integrar e criar experiências personalizadas para estender as soluções da Adobe, e agora está disponível para o Adobe Commerce. Com o App Builder, você pode criar aplicativos seguros e escalonáveis que estendem a funcionalidade nativa da Commerce e se integram a soluções de terceiros. Como desenvolvedor, agora você pode aproveitar a extensibilidade fora do processo com o Adobe Commerce, o que, por sua vez, fornece benefícios imediatos e de longo prazo.

A App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar aplicativos personalizados que estendam o [!DNL Adobe Commerce]. Como essa estrutura de extensibilidade é criada na infraestrutura da Adobe, os desenvolvedores podem criar microsserviços personalizados e estender e integrar o [!DNL Adobe Commerce] a outras soluções da Adobe e integrações de terceiros.

A App Builder fornece uma maneira para os clientes estenderem o [!DNL Adobe Commerce] em vários casos de uso:

* extensibilidade do middleware - conecte sistemas externos com aplicativos da Adobe criando conectores personalizados ou aproveite um conjunto de integrações pré-criadas.
* extensibilidade dos principais serviços - amplie os principais recursos do aplicativo estendendo o comportamento padrão com recursos personalizados e lógica de negócios.
* extensibilidade da experiência do usuário - Estenda a experiência principal para atender aos requisitos dos negócios ou criar propriedades digitais, vitrines e aplicativos back-office específicos do cliente.

O Adobe Developer App Builder é uma solução baseada em nuvem, o que significa que é dimensionada automaticamente. Esse serviço também é distribuído globalmente para permitir o melhor desempenho, independentemente da sua localização geográfica.

## Por que você deve saber mais sobre o App Builder

Como o Adobe Commerce não é um produto totalmente SAAS, o código que você desenvolve pode adicionar problemas de complexidade e atualização. Ao usar a extensibilidade fora do processo, como o App Builder, você pode fornecer funcionalidade personalizada e exclusiva à loja da Adobe Commerce sem exigir métodos no processo.

Outros benefícios incluem:

* Os recursos dissociados possibilitam um tempo de lançamento mais rápido.
* As atualizações agora são mais fáceis. Os recursos personalizados estão fora da base de código do Commerce, o que evita problemas de compatibilidade ao atualizar.
* Mover recursos e lógica para fora do Commerce libera recursos que normalmente são usados por métodos de desenvolvimento em andamento.

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, a Adobe Developer App Builder fornece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como o Adobe Commerce, incluindo:

* Adobe Developer Console usado para microsserviço personalizado e desenvolvimento de extensão. Crie e gerencie projetos enquanto acessa todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas de código aberto, SDKs e bibliotecas para criar extensões e integrações personalizadas. Use o React Spectrum (kit de ferramentas da interface do Adobe) para ter uma interface comum para todos os aplicativos da Adobe.
* serviços como I/O Runtime para hospedar a infraestrutura na plataforma sem servidor da Adobe e Eventos de I/O para integrações baseadas em eventos. A Adobe também oferece suporte pronto para armazenar dados e arquivos.
* Adobe Experience Cloud, onde você envia extensões e integrações para publicar na sua organização da Experience Cloud. Os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder estarão disponíveis junto com outros aplicativos da Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](/help/assets/app-builder/app-builder-architecture.jpeg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte a [Visão geral da arquitetura](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Introdução ao App Builder {#additional-resources}

Uma visão geral da estratégia de comércio combinável, que inclui a configuração inicial, pode ser encontrada lendo a seguinte publicação do blog:

[Como o App Builder ajuda a impulsionar a agilidade comercial para sua plataforma de comércio](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Para ajudar você a começar a usar o App Builder, a Adobe criou a seguinte documentação:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Continue aprendendo com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Experimente um dos aplicativos de amostra {#appbuilder-codesamples}

Pronto para começar a desenvolver? O link a seguir contém aplicativos de exemplo para ajudar você a começar:

* [App Builder Code Labs no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Suporte {#support}

Para solicitações de suporte ao desenvolvedor, use o [fórum do Experience League](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly){target="_blank"} para obter assistência.

{{$include /help/_includes/app-builder-related-links.md}}
