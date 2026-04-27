---
title: Out-of-process extensibility for Adobe Commerce
description: Saiba mais sobre o Adobe App Builder e por que ele é um aspecto importante da extensibilidade fora do processo.
jira: KT-11433
doc-type: Tutorial
duration: 322
last-substantial-update: 2023-02-16T00:00:00.000Z
feature: API Mesh, App Builder, Extensibility, Tools and External Services, Backend Development
topic: App Builder, I/O Events, Developer Console, Commerce, Development, Integrations
role: Developer
level: Beginner, Intermediate
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
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 777
ht-degree: 2%

---

# Introduction to App Builder

Historically, Adobe Commerce development has used in-process extensibility. The in-process model requires any new code to be compatible with upgrades, the server&#39;s PHP version, and many other essential server applications and services that Commerce uses. Adobe Developer App Builder uses out-of-process extensibility to avoid these compatibility issues.

## App Builder for Adobe Commerce {#app-builder}

>[!VIDEO](https://video.tv.adobe.com/v/3412839?learn=on)

Adobe Developer App Builder is a serverless extensibility platform for integrating and creating custom experiences to extend Adobe solutions, and it&#39;s now available for Adobe Commerce. With App Builder, you can build secure and scalable apps that extend Commerce-native functionality and integrate with third-party solutions. As a developer, you can now take advantage of out-of-process extensibility with Adobe Commerce and that in turn provides immediate and long-term benefits.

App Builder provides a unified third-party extensibility framework for integrating and creating custom applications that extend [!DNL Adobe Commerce]. Since this extensibility framework is built on Adobe&#39;s infrastructure, developers can build custom microservices, and extend and integrate [!DNL Adobe Commerce] across other Adobe solutions and third-party integrations.

App Builder provides a way for customers to extend [!DNL Adobe Commerce] in various use cases:

* middleware extensibility - Connect external systems with Adobe applications by building custom connectors or take advantage of a suite of pre-built integrations.
* core services extensibility - Extend core application capabilities by extending the default behavior with custom features and business logic.
* user experience extensibility - Extend core experience to support business requirements or build customer-specific digital properties, storefronts, and back-office applications.

Adobe Developer App Builder is a cloud-based solution, which means that it automatically scales. This service is also globally distributed to allow the best performance regardless of your geographic location.

## Why should you learn more about App Builder

Since Adobe Commerce is not a fully SAAS product, the code you develop can add complexity and upgrade issues. By using out-of-process extensibility, such as App Builder, you can provide custom, unique functionality to your Adobe Commerce store without requiring in-process methods.

Other benefits include:

* Decoupled features allow for faster time to launch.
* Upgrades are now easier. Os recursos personalizados estão fora da base de código do Commerce, o que evita problemas de compatibilidade ao atualizar.
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
