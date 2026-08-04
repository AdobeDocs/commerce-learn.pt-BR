---
title: Extensibilidade fora do processo para o Adobe Commerce
description: Saiba mais sobre o Adobe Developer App Builder e como a extensibilidade fora do processo permite criar extensões seguras e escaláveis do Commerce sem preocupações de compatibilidade no processo.
jira: KT-11433
doc-type: Tutorial
duration: 300
last-substantial-update: 2023-02-16T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner
exl-id: 94f8d82a-4a95-46ea-8eed-edf9bed5760c
TQID: https://experienceleague.adobe.com/c3dl6gZ7Jtje5rZCB9HrwmCbFrcu8bllL0z0B9cl5Jg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 63ac13d8c5a97ee81dcdd1f3785a9875aaf2a4db
workflow-type: tm+mt
source-wordcount: 761
ht-degree: 0%

---

# Introdução ao App Builder

Historicamente, o desenvolvimento do Adobe Commerce tem usado extensibilidade no processo. O modelo em andamento requer que qualquer novo código seja compatível com as atualizações, a versão PHP do servidor e muitos outros aplicativos e serviços essenciais do servidor que o Commerce usa. O Adobe Developer App Builder usa extensibilidade fora do processo para evitar esses problemas de compatibilidade.

## App Builder para Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?learn=on)

O Adobe Developer App Builder é uma plataforma de extensibilidade sem servidor para integrar e criar experiências personalizadas para estender as soluções da Adobe, e agora está disponível para o Adobe Commerce. Com o App Builder, você pode criar aplicativos seguros e escalonáveis que estendem a funcionalidade nativa da Commerce e se integram a soluções de terceiros. Como desenvolvedor, agora você pode aproveitar a extensibilidade fora do processo com o Adobe Commerce, o que, por sua vez, fornece benefícios imediatos e de longo prazo.

A App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar aplicativos personalizados que estendam o [!DNL Adobe Commerce]. Como essa estrutura de extensibilidade é criada na infraestrutura da Adobe, os desenvolvedores podem criar microsserviços personalizados e estender e integrar o [!DNL Adobe Commerce] a outras soluções da Adobe e integrações de terceiros.

A App Builder fornece uma maneira para os clientes estenderem o [!DNL Adobe Commerce] em vários casos de uso:

* extensibilidade do middleware - conecte sistemas externos com aplicativos da Adobe criando conectores personalizados ou aproveite um conjunto de integrações pré-criadas.
* extensibilidade dos principais serviços - amplie os principais recursos do aplicativo estendendo o comportamento padrão com recursos personalizados e lógica de negócios.
* extensibilidade da experiência do usuário - Para dar suporte às necessidades dos negócios ou criar propriedades digitais, vitrines e aplicativos back-office específicos do cliente, estenda a experiência principal.

O Adobe Developer App Builder é uma solução baseada em nuvem, o que significa que é dimensionada automaticamente. Esse serviço também é distribuído globalmente para permitir o melhor desempenho, independentemente da sua localização geográfica.

## Por que saber mais sobre o App Builder

Como o Adobe Commerce não é um produto totalmente SAAS, o código que você desenvolve pode adicionar considerações de complexidade e atualização. Ao usar a extensibilidade fora do processo, como o App Builder, você pode fornecer funcionalidade personalizada e exclusiva à loja da Adobe Commerce sem exigir métodos no processo.

Outros benefícios incluem:

* Os recursos dissociados possibilitam um tempo de lançamento mais rápido.
* As atualizações agora são mais fáceis. Os recursos personalizados estão fora da base de código do Commerce, o que evita problemas de compatibilidade ao atualizar.
* Mover recursos e lógica para fora do Commerce libera recursos que os métodos de desenvolvimento em andamento normalmente usam.

## Arquitetura {#architecture}

Em vez de uma solução pré-configurada, o Adobe Developer App Builder fornece uma plataforma de desenvolvimento comum, consistente e padronizada para estender as soluções da Adobe Cloud, como o Adobe Commerce, incluindo:

* Adobe Developer Console usado para microsserviço personalizado e desenvolvimento de extensão. Crie e gerencie projetos enquanto acessa todas as ferramentas e APIs necessárias para criar plug-ins e integrações.
* Ferramentas de código aberto, SDKs e bibliotecas para criar extensões e integrações personalizadas. Use o React Spectrum (kit de ferramentas da interface do Adobe) para ter uma interface comum para todos os aplicativos da Adobe.
* serviços como I/O Runtime para hospedar a infraestrutura na plataforma sem servidor da Adobe e Eventos de I/O para integrações baseadas em eventos. A Adobe também oferece suporte pré-configurado para armazenar dados e arquivos.
* A Adobe Experience Cloud, onde você envia extensões e integrações para publicar na sua organização da Experience Cloud. Os administradores do sistema podem revisar, gerenciar e aprovar essas extensões. Depois de publicadas, suas ferramentas e extensões personalizadas do App Builder estarão disponíveis junto com outros aplicativos da Adobe Experience Cloud.

O diagrama a seguir ilustra como um aplicativo padrão criado no App Builder usa essas funcionalidades:

![Arquitetura](/help/assets/app-builder/app-builder-architecture.jpeg)

Para obter mais detalhes sobre a arquitetura do App Builder, consulte a [Visão geral da arquitetura](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview){target="_blank"}.

## Introdução ao App Builder {#additional-resources}

Uma visão geral da estratégia de comércio combinável que inclui a configuração inicial pode ser encontrada lendo a seguinte publicação do blog:

[Como o App Builder ajuda a impulsionar a agilidade comercial para sua plataforma de comércio](https://business.adobe.com/blog/how-to/how-app-builder-helps-you-implement-a-composable-commerce-strategy){target="_blank"}

Para ajudar você a começar a usar o App Builder, a Adobe criou a seguinte documentação:

* [Introdução ao App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app){target="_blank"}

## Continue aprendendo com a documentação {#appbuilder-documentation}

O App Builder fornece vídeos e documentação para desenvolvedores, incluindo guias e documentação de referência para ajudar a desenvolver seus próprios aplicativos personalizados:

* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview){target="_blank"}
* [Vídeos do App Builder](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o){target="_blank"}

## Experimente um dos aplicativos de amostra {#appbuilder-codesamples}

Pronto para começar a desenvolver? O link a seguir contém aplicativos de exemplo para ajudar você a começar:

* [App Builder Code Labs no site da Adobe Developer](https://developer.adobe.com/app-builder/docs/resources/){target="_blank"}

{{$include /help/_includes/app-builder-related-links.md}}
