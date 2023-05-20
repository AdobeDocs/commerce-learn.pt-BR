---
title: Extensibilidade fora do processo para o Adobe Commerce
description: Saiba mais sobre o Construtor de aplicativos Adobe e por que ele é um aspecto importante da extensibilidade fora do processo.
landing-page-description: Saiba o que é o Construtor de aplicativos e como ele pode ajudar nas estratégias de desenvolvimento do Adobe Commerce.
short-description: Saiba o que é o Construtor de aplicativos e como ele pode ajudar nas estratégias de desenvolvimento do Adobe Commerce.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-02-16T00:00:00Z
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# Introdução ao App Builder

Historicamente, o desenvolvimento do Adobe Commerce tem usado extensibilidade no processo. O modelo em andamento exige que qualquer novo código seja compatível com atualizações, a versão PHP do servidor e muitos outros aplicativos e serviços essenciais do servidor que o Commerce usa. O Construtor de aplicativos da Adobe Developer usa extensibilidade fora do processo para evitar esses problemas de compatibilidade.

## Construtor de aplicativos para Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?quality=12&learn=on)

O Adobe Developer App Builder é uma plataforma de extensibilidade sem servidor para integrar e criar experiências personalizadas para estender soluções de Adobe, e agora está disponível para o Adobe Commerce. Com o App Builder, você pode criar aplicativos seguros e escalonáveis que estendem a funcionalidade nativa do Commerce e se integram a soluções de terceiros. Como desenvolvedor, agora você pode aproveitar a extensibilidade fora do processo com o Adobe Commerce, o que, por sua vez, fornece benefícios imediatos e de longo prazo.

O App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar aplicativos personalizados que se estendem [!DNL Adobe Commerce]. Como essa estrutura de extensibilidade é criada na infraestrutura do Adobe, os desenvolvedores podem criar microsserviços personalizados e estender e integrar [!DNL Adobe Commerce] em outras soluções Adobe e integrações de terceiros.

O App Builder fornece uma maneira de os clientes estenderem [!DNL Adobe Commerce] em vários casos de uso:

* extensibilidade do middleware - Conecte sistemas externos com aplicativos Adobe criando conectores personalizados ou aproveite um conjunto de integrações pré-construídas.
* extensibilidade dos principais serviços - amplie os principais recursos do aplicativo estendendo o comportamento padrão com recursos personalizados e lógica de negócios.
* extensibilidade da experiência do usuário - Estenda a experiência principal para atender aos requisitos dos negócios ou criar propriedades digitais, vitrines e aplicativos back-office específicos do cliente.

O Adobe Developer App Builder é uma solução baseada em nuvem, o que significa que é dimensionada automaticamente. Esse serviço também é distribuído globalmente para permitir o melhor desempenho, independentemente da sua localização geográfica.

## Por que você deve saber mais sobre o App Builder

Como o Adobe Commerce não é um produto totalmente SAAS, o código que você desenvolve pode adicionar problemas de complexidade e atualização. Ao usar extensibilidade fora do processo, como o App Builder, você pode fornecer funcionalidade personalizada e exclusiva à loja da Adobe Commerce sem exigir métodos no processo.

Outros benefícios incluem:

* Os recursos dissociados possibilitam um tempo de lançamento mais rápido.
* As atualizações agora são mais fáceis. Os recursos personalizados estão fora da base de código do Commerce, o que evita problemas de compatibilidade ao atualizar.
* Mover recursos e lógica para fora do Commerce libera recursos que normalmente são usados por métodos de desenvolvimento em andamento.

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, o Adobe Developer App Builder fornece uma plataforma de desenvolvimento comum, consistente e padronizada para a extensão de soluções da Adobe Cloud, como o Adobe Commerce, incluindo:

* Console do Adobe Developer usado para microsserviço personalizado e desenvolvimento de extensão. Crie e gerencie projetos enquanto acessa todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas de código aberto, SDKs e bibliotecas para criar extensões e integrações personalizadas. Use o Espectro de Reação (kit de ferramentas da interface do Adobe) para ter uma interface comum para todos os aplicativos Adobe.
* serviços como I/O Runtime para hospedar a infraestrutura na plataforma sem servidor Adobe e Eventos de I/O para integrações baseadas em eventos. O Adobe também oferece suporte pronto para armazenar dados e arquivos.
* Adobe Experience Cloud, onde você envia extensões e integrações para publicar na sua organização Experience Cloud. Os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder estarão disponíveis junto com outros aplicativos da Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](/help/assets/app-builder/app-builder-architecture.jpeg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte [Visão geral da arquitetura](https://developer.adobe.com/app-builder/docs/guides/){target="_blank"}.

## Extensão Sales Channel do Amazon {#amazon-sales-channel-extension}

>[!IMPORTANT]
>
>A extensão Amazon Sales Channel ainda está em desenvolvimento e não foi lançada oficialmente.  Esses vídeos e tutoriais têm como objetivo mostrar como usar o Construtor de aplicativos da Adobe Developer para um caso de uso prático.

Os tutoriais a seguir demonstram como conectar o Adobe Commerce ao Amazon Sales Channel usando uma extensão do Construtor de aplicativos.

* [visão geral técnica App Builder](../app-builder/app-builder-technical-overview.md)
* [estrutura de extensibilidade](../app-builder/extensibility-framework-commerce-eventing.md)
* [demonstração funcional do App Builder](../app-builder/app-builder-functional-demonstration.md)

## Introdução ao App Builder {#additional-resources}

Uma visão geral da estratégia de comércio combinável, que inclui a configuração inicial, pode ser encontrada lendo a seguinte publicação do blog:

[Como o App Builder ajuda a impulsionar a agilidade comercial para sua plataforma de comércio](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Para ajudar você a começar a usar o App Builder, o Adobe criou a seguinte documentação:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/getting_started/){target="_blank"}

## Continue aprendendo com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/overview/){target="_blank"}
* [Vídeos do Construtor de aplicativos](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Experimente um dos aplicativos de amostra {#appbuilder-codesamples}

Pronto para começar a desenvolver? O link a seguir contém aplicativos de exemplo para ajudar você a começar:

* [Laboratórios de código do App Builder no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

## Suporte {#support}

Para solicitações de suporte do desenvolvedor, use o [fórum do Experience League](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly){target="_blank"} para obter assistência.

{{$include /help/_includes/app-builder-related-links.md}}
