---
title: Saiba como o Adobe cria comércio combinável
description: Saiba mais sobre o comércio combinável, priorizando uma abordagem de API e implementando uma arquitetura modular e orientada a serviços.
feature: App Builder, Saas
topic: Architecture, Commerce, Development, Headless, Integrations, Performance, Personalization
role: Admin, Architect, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-06-27T00:00:00Z
jira: KT-15730
thumbnail: KT-15730.jpeg
source-git-commit: d3d4338568b04d36c8dff3ada423a04b33dae061
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---


# Saiba como o Adobe cria comércio combinável

Saiba mais sobre o investimento da Adobe Commerce em ferramentas de desenvolvimento combináveis e personalização baseada em IA para aprimorar a experiência de comércio eletrônico.

## O que é comércio combinável

O comércio combinável é uma abordagem arquitetônica no comércio eletrônico que envolve a dissociação da camada de apresentação front-end da funcionalidade de comércio back-end. &#x200B; Ele permite que as empresas selecionem e combinem os melhores componentes ou módulos para criar uma solução personalizada. Essa abordagem envolve dividir a plataforma monolítica tradicional de comércio eletrônico em serviços ou microsserviços menores e independentes que podem ser compostos em conjunto. O comércio combinável oferece benefícios como flexibilidade, escalabilidade, personalização, agilidade e a possibilidade de integrações mais fáceis com outros sistemas e tecnologias. &#x200B; O Adobe Commerce fornece vários recursos e ferramentas para apoiar os comerciantes na adoção e implementação do comércio combinável. O Adobe Commerce oferece uma metodologia de comércio combinável e experiências de front-end híbridas headless e não headless. Com a extensibilidade fora do processo em mente, o Adobe oferece a API Mesh para integração de vários serviços e o Adobe App Builder para criação de microsserviços personalizados. &#x200B;

## Por que o comércio combinável é importante?

Entender o comércio combinável é importante para empresas e indivíduos envolvidos no setor de comércio eletrônico por vários motivos. &#x200B; Ele oferece flexibilidade e personalização, escalabilidade e agilidade, recursos de integração, prova de obsolescência e capacitação de desenvolvedores. O comércio combinável permite que as empresas adaptem e evoluam suas plataformas de comércio eletrônico, dimensionem e expandam suas operações. Alguns benefícios mais impressionantes incluem a capacidade de integração com outros sistemas e tecnologias, acompanhar a evolução das expectativas dos clientes e aproveitar a experiência dos desenvolvedores. &#x200B; Ele ajuda as empresas a navegar no cenário de comércio eletrônico em evolução, tomar decisões conscientes e aproveitar os benefícios dos recursos de flexibilidade, escalabilidade, personalização, agilidade e integração. Além disso, conhecer o comércio combinável é importante para o crescimento dos negócios, a personalização, a agilidade e a inovação, a eficiência de custos, a integração e a flexibilidade, além de ser inovador. &#x200B; Ele permite que as empresas se adaptem rapidamente a novos recursos e respondam a condições de mercado em constante mudança, criem soluções altamente personalizadas. Há mais benefícios que incluem a capacidade de inovar rapidamente, reduzir os custos de desenvolvimento e manutenção e integrar-se a serviços e sistemas de terceiros. &#x200B; Em geral, entender o comércio combinável permite que as empresas tomem decisões informadas, otimizem a arquitetura e a estratégia de comércio eletrônico e impulsionem o crescimento e o sucesso no mercado digital. &#x200B;

## Como as empresas podem se beneficiar do comércio combinável

As empresas podem se beneficiar do comércio combinável de várias maneiras:

Flexibilidade e personalização: o comércio combinável permite que as empresas selecionem e combinem os melhores componentes ou microsserviços para criar uma solução de comércio eletrônico personalizada que atenda às suas necessidades específicas. &#x200B; Ele permite que as empresas personalizem suas plataformas para fornecer experiências exclusivas aos clientes, implementar funcionalidades especializadas e diferenciar-se no mercado. &#x200B;

Escalabilidade e agilidade: com uma arquitetura combinável, as empresas podem dimensionar diferentes componentes de sua plataforma de comércio eletrônico independentemente. &#x200B; Isso significa que eles podem alocar recursos e dimensionar funcionalidades específicas com base na demanda, garantindo desempenho ideal e economia. O comércio combinável também permite práticas ágeis de desenvolvimento, permitindo que as equipes trabalhem em diferentes componentes simultaneamente e implantem alterações de maneira independente, resultando em um encurtamento do tempo de entrada no mercado. &#x200B;

Recursos de integração: o comércio combinável facilita a integração perfeita com sistemas, serviços e tecnologias de terceiros. &#x200B; As empresas podem conectar facilmente sua plataforma de comércio eletrônico com várias ferramentas, como gateways de pagamento, sistemas ERP, sistemas CRM, plataformas de automação de marketing e muito mais. &#x200B; Esse recurso de integração permite que as empresas aproveitem as melhores soluções do setor e criem um ecossistema unificado que melhore a eficiência operacional e a experiência do cliente.

Prova de futuro: o comércio combinável oferece às empresas a flexibilidade de adaptar e desenvolver sua plataforma de comércio eletrônico à medida que a tecnologia e as tendências de mercado mudam. &#x200B; Ele permite que as empresas adicionem ou substituam facilmente componentes, integrem novas tecnologias e permaneçam à frente da concorrência. Esse recurso inovador garante que as empresas possam inovar continuamente e atender às crescentes expectativas dos clientes.

Capacitação do desenvolvedor: o comércio combinável capacita os desenvolvedores, fornecendo-lhes a flexibilidade para trabalhar com diferentes tecnologias, linguagens e estruturas. &#x200B; Ele permite que os desenvolvedores se concentrem em componentes ou microsserviços específicos, permitindo a especialização e o conhecimento. Essa capacitação leva ao aumento da produtividade do desenvolvedor, ciclos de desenvolvimento mais rápidos e à capacidade de aproveitar as ferramentas e as tecnologias mais recentes.

Em geral, o comércio combinável permite que as empresas criem uma plataforma de comércio eletrônico altamente flexível, escalável e personalizável que pode se adaptar às necessidades comerciais em constante mudança, fornecer experiências excepcionais para os clientes e impulsionar o crescimento e o sucesso no mercado digital. &#x200B;

## Quais recursos o Adobe Commerce tem para o comércio combinável?

O Adobe Commerce fornece vários recursos para apoiar os comerciantes na adoção e implementação do comércio combinável:

Metodologia do Commerce combinável: o Adobe Commerce oferece uma metodologia de comércio combinável que orienta os comerciantes a entender e implementar os princípios da arquitetura combinável. &#x200B; Essa metodologia ajuda as empresas a aproveitar os benefícios da flexibilidade, escalabilidade e personalização, considerando fatores como complexidade, maturidade técnica e tamanho do projeto.

Funcionalidade repleta de recursos: a Adobe Commerce fornece um conjunto abrangente de recursos acessíveis por meio do GraphQLAPI. &#x200B; Essa funcionalidade repleta de recursos permite que os comerciantes minimizem o número de fornecedores necessários em sua pilha de comércio, reduzindo os desafios de tempo para comercialização. &#x200B; Ele permite que as empresas iniciem mais rápido, mantendo a flexibilidade para compor e integrar serviços ou recursos adicionais de terceiros à medida que sua pilha de comércio evolui. &#x200B;

Experiências de front-end híbridas: o Adobe Commerce oferece suporte a experiências de front-end headless e não headless no mesmo ecossistema. &#x200B; Essa flexibilidade permite que os comerciantes escolham a abordagem de arquitetura mais adequada para cada caso de uso de front-end específico. &#x200B; Ela permite uma transição gradual para uma arquitetura headless e combinável, sem a necessidade de uma migração simultânea de todo o sistema.

API Mesh: o Adobe Commerce API Mesh simplifica a integração de vários microsserviços, ferramentas de terceiros e aplicativos em um endpoint de API unificado para desenvolvedores de front-end. &#x200B; Ele permite que os desenvolvedores combinem várias fontes de dados em um único endpoint do GraphQL, reduzindo a complexidade e simplificando o desenvolvimento e a manutenção de novos recursos e experiências.

Adobe App Builder: o Adobe App Builder é uma plataforma de extensibilidade sem servidor que permite aos comerciantes criar microsserviços personalizados, criar experiências personalizadas e estender soluções Adobe. &#x200B; Com o App Builder, os comerciantes podem criar aplicativos seguros e escalonáveis que ampliam a funcionalidade nativa da Adobe Commerce e integram-se a soluções de terceiros. &#x200B; Isso elimina a necessidade de os comerciantes criarem e manterem sua própria infraestrutura para personalizações e microsserviços, reduzindo a complexidade e o custo total de propriedade. &#x200B;

Esses recursos fornecidos pela Adobe Commerce simplificam a adoção e a implementação do comércio combinável, permitindo que os comerciantes aproveitem os benefícios de flexibilidade, escalabilidade, personalização e recursos de integração enquanto reduzem a complexidade e o esforço de desenvolvimento. &#x200B;

## Pensamentos finais

O comércio combinável é uma abordagem arquitetônica no comércio eletrônico que envolve a dissociação da camada de apresentação front-end da funcionalidade de comércio back-end. &#x200B; Estas são as principais lições aprendidas sobre o comércio combinável:

Arquitetura: o comércio combinável segue uma arquitetura modular e dissociada, permitindo que as empresas selecionem e combinem os melhores componentes ou microsserviços para criar uma solução personalizada. &#x200B; Essa arquitetura oferece flexibilidade, escalabilidade e agilidade.

Benefícios: o comércio combinável oferece vários benefícios, incluindo flexibilidade e personalização, escalabilidade e agilidade, recursos de integração, prova de obsolescência e capacitação do desenvolvedor. &#x200B; Ele permite que as empresas se adaptem, dimensionem, integrem, inovem e aproveitem a experiência do desenvolvedor.

Considerações: ao considerar o comércio combinável, fatores como complexidade, maturidade técnica interna, tamanho e estrutura do projeto, personalização versus padronização, custo total de propriedade e segurança e privacidade de dados devem ser cuidadosamente avaliados. &#x200B;

Adobe Commerce: o Adobe Commerce fornece recursos e ferramentas para apoiar os comerciantes na adoção e implementação do comércio combinável. &#x200B; Isso inclui uma metodologia de comércio combinável, funcionalidade repleta de recursos, experiências de front-end híbridas, API Mesh para integração e Adobe App Builder para microsserviços personalizados. &#x200B;

Impacto nos negócios: o comércio combinável permite que as empresas criem uma plataforma de comércio eletrônico altamente flexível, escalável e personalizável. &#x200B; Ele permite que eles ofereçam experiências exclusivas para o cliente, dimensionem com base na demanda, integrem-se a outros sistemas, tornem suas operações possíveis e aproveitem a experiência do desenvolvedor.

Entender o comércio combinável é crucial para que as empresas do setor de comércio eletrônico permaneçam competitivas, se adaptem às condições de mercado em constante mudança e ofereçam experiências excepcionais para o cliente. &#x200B; Ao adotar o comércio combinável, as empresas podem aproveitar os benefícios dos recursos de flexibilidade, escalabilidade, personalização, agilidade e integração, impulsionando o crescimento e o sucesso no mercado digital. &#x200B;
