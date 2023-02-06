---
title: Extensibilidade fora do processo para Adobe Commerce
description: Saiba mais sobre o Adobe App Builder e por que ele é um aspecto importante da extensibilidade fora do processo.
landing-page-description: Saiba o que é o App Builder e como ele pode ajudar com as estratégias de desenvolvimento do Adobe Commerce.
kt: 11433
doc-type: tutorial
audience: all
last-substantial-update: 2023-01-24T00:00:00Z
source-git-commit: 336581ac6b695d8b847d88daadeb3784ece97ae7
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---


# Introdução ao App Builder

Historicamente, o desenvolvimento do Adobe Commerce tem usado a extensibilidade no processo. O modelo em andamento requer que qualquer novo código seja compatível com as atualizações, a versão PHP do servidor e muitos outros aplicativos e serviços essenciais do servidor que o Commerce usa. O Adobe Developer App Builder usa extensibilidade fora de processo para evitar esses problemas de compatibilidade.

## App Builder para Adobe Commerce {#project-firefly}

>[!VIDEO](https://video.tv.adobe.com/v/3412839)

O Adobe Developer App Builder é uma plataforma de extensibilidade sem servidor para integrar e criar experiências personalizadas para estender soluções do Adobe, e agora está disponível para a Adobe Commerce. Com o App Builder, você pode criar aplicativos seguros e escaláveis que estendem a funcionalidade nativa de comércio e se integram a soluções de terceiros. Como desenvolvedor, agora você pode aproveitar as vantagens da extensibilidade fora do processo com o Adobe Commerce e que, por sua vez, oferece benefícios imediatos e de longo prazo.

O App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar aplicativos personalizados que se estendem [!DNL Adobe Commerce]. Como a estrutura de extensibilidade é criada nessa infraestrutura Adobe, os desenvolvedores podem criar microsserviços personalizados e estender a integração [!DNL Adobe Commerce] em outras soluções de Adobe e integrações de terceiros.

O App Builder oferece uma maneira de os clientes estenderem [!DNL Adobe Commerce] em vários casos de uso:

* extensibilidade middleware - conecte sistemas externos a aplicativos Adobe criando conectores personalizados ou aproveite um conjunto de integrações pré-criadas.
* extensibilidade de serviços principais - estenda os principais recursos do aplicativo ao estender o comportamento padrão com recursos personalizados e lógica comercial.
* extensibilidade da experiência do usuário - estenda a experiência principal para atender aos requisitos dos negócios ou crie propriedades digitais específicas do cliente, vitrines e aplicativos de back-office.

O App Builder (anteriormente conhecido como Project Firefly) é uma solução baseada em nuvem, o que significa que é dimensionada automaticamente. Esse serviço também é distribuído globalmente para permitir o melhor desempenho independentemente da localização geográfica.

## Por que você deve saber mais sobre o App Builder

Como o Adobe Commerce não é um produto SAAS completo, o código desenvolvido pode adicionar complexidade e problemas de atualização. Ao usar extensibilidade fora do processo, como o App Builder, você pode fornecer funcionalidade personalizada e exclusiva à sua loja da Adobe Commerce sem precisar de métodos em andamento.

Outros benefícios incluem:

* Os recursos dissociados permitem uma inicialização mais rápida.
* As atualizações agora são mais fáceis. Os recursos personalizados estão fora da base de código do Commerce, o que impede problemas de compatibilidade ao atualizar.
* Mover recursos e lógicas para fora do Commerce libera recursos que são normalmente usados por métodos de desenvolvimento em andamento.

## Arquitetura {#architecture}

Em vez de uma solução pronta para uso, o Adobe Developer App Builder oferece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como o Adobe Commerce, incluindo:

* Console do Adobe Developer usado para microsserviço personalizado e desenvolvimento de extensão. Crie e gerencie projetos enquanto acessa todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas, SDKs e bibliotecas de código aberto para criar extensões e integrações personalizadas. Use o React Spectrum (Adobe UI toolkit) para ter uma interface comum para todos os aplicativos de Adobe.
* serviços como I/O Runtime para hospedar a infraestrutura na plataforma sem servidor Adobe e Eventos de E/S para integrações baseadas em eventos. O Adobe também oferece suporte pronto para o armazenamento de dados e arquivos.
* Adobe Experience Cloud, onde você envia extensões e integrações para publicar em sua organização do Experience Cloud. Os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder estarão disponíveis junto com outros aplicativos Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](/help/assets/app-builder/firefly-architecture.jpeg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte a [Visão geral da arquitetura](https://developer.adobe.com/app-builder/docs/guides/).

## Extensão Sales Channel do Amazon {#amazon-sales-channel-extension}

Os seguintes tutoriais demonstram como se conectar ao Adobe Commerce ao Amazon Sales Channel usando uma extensão do App Builder.

* [visão geral técnica do App Builder](../app-builder/app-builder-technical-overview.md)
* [estrutura de extensibilidade](../app-builder/extensibility-framework-commerce-eventing.md)
* [demonstração funcional App Builder](../app-builder/app-builder-functional-demonstration.md)

## Introdução ao App Builder {#additional-resources}

Para ajudar você a começar a usar o App Builder, o Adobe criou a seguinte documentação:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/getting_started/)

## Continuar o aprendizado com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/overview/)
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Experimente um dos aplicativos de exemplo {#appbuilder-codesamples}

Pronto para começar a desenvolver? O link a seguir contém aplicativos de exemplo para ajudar você a começar:

* [Laboratórios de código do App Builder no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/)

## Suporte {#support}

Para solicitações de suporte do desenvolvedor, use o [Experience League forum](https://experienceleaguecommunities.adobe.com/t5/app-builder/ct-p/project-firefly) para obter assistência.
