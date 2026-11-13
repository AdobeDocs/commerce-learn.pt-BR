---
title: Commerce combinável com Adobe
description: Saiba mais sobre o comércio combinável com opções de plataforma do Adobe, vitrines do Edge Delivery Services, API Mesh, App Builder e ferramentas de MCP de desenvolvimento do Commerce.
feature: API Mesh, App Builder, Saas
topic: Architecture, Commerce, Development, Headless, Integrations, Performance, Personalization
role: Admin, Developer, User
level: Intermediate
doc-type: Tutorial
duration: 307
last-substantial-update: 2026-11-13
jira: KT-15730
exl-id: 4d811a2f-8488-4de7-babd-449aced42e3a
TQID: 'https://experienceleague.adobe.com/NG-US7zLBgzV425mheo3oQ9Z6gnzAr6aRCLNjHVU0aM'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
autotag-review: '2026-11-13T20:04:10.194Z'
source-git-commit: 3a52f4de8c63f08418f4fa44833a7bf7eb90175b
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%
---
# Comércio combinável

O comércio combinável é uma abordagem arquitetônica que combina recursos comerciais por meio de APIs. Você pode selecionar e integrar componentes de experiências da loja, gerenciamento de catálogos, descoberta de produtos, finalização e outras necessidades comerciais, em vez de exigir que todos os recursos venham de um aplicativo totalmente integrado.

O comércio headless separa a camada de apresentação da loja do back-end de comércio. O comércio combinável se baseia nessa separação, permitindo que as equipes escolham quais recursos manter juntos e quais integrar de forma independente. Uma loja headless não faz com que cada componente de backend seja substituído independentemente.

A Adobe apóia essa abordagem por meio de opções de plataforma comercial, tecnologia de vitrine e ferramentas de integração e desenvolvimento. Os MCPs de desenvolvimento do Adobe Commerce as a Cloud Service (ACCS), Adobe Commerce Optimizer (ACO), Edge Delivery Services, API Mesh, App Builder e Commerce atendem a diferentes objetivos. Eles não são produtos intercambiáveis ou uma pilha combinada necessária.

## Benefícios e compensações

Uma abordagem combinável pode ajudá-lo a:

* **Adapte a experiência do cliente**: escolha componentes de vitrine e integre serviços que atendam às suas necessidades comerciais.
* **Modernizar incrementalmente:** substitua os recursos selecionados ao reter outros sistemas e seus dados.
* **Dimensione e evolva independentemente:** crie integrações e extensões para que suas alterações não exijam uma versão de todo o aplicativo de comércio.
* **Reutilizar recursos de comércio**: use recursos e APIs de plataforma compatíveis, em vez de reconstruir todas as funções empresariais.

Esses benefícios dependem da implementação. Avalie a maturidade técnica, os custos de entrega, o licenciamento, a segurança e a privacidade dos dados. Defina a propriedade para contratos de API, sincronização de dados, autenticação, desempenho e falhas entre serviços. Uma arquitetura mais modular também pode aumentar a integração e a complexidade operacional.

## Opções de arquitetura do Adobe Commerce

Comece decidindo se você precisa de uma plataforma de comércio gerenciada ou se deseja modernizar as experiências do cliente em torno de um back-end transacional existente.

Para ver uma comparação de vídeos, consulte [opções de comércio disponíveis da Adobe](./adobes-available-commerce-options.md).

### Adobe Commerce as a Cloud Service

O Adobe Commerce as a Cloud Service é uma plataforma de comércio SaaS gerenciada. A Adobe gerencia o aplicativo principal, a infraestrutura e as atualizações. Sua arquitetura inclui o Commerce Foundation, recursos de loja headless, serviços de merchandising e ferramentas de desenvolvedor.

Use essa opção ao avaliar uma base de comércio gerenciado com pontos de extensão compatíveis. Para uma lógica de negócios personalizada, planeje a extensibilidade fora do processo suportada, em vez de assumir que as extensões existentes do PHP possam ser implantadas inalteradas. O ACCS não é compatível com vitrines Luma; inclua a migração de vitrines no seu plano de implementação, quando aplicável.

Consulte a [visão geral do Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview).

### Adobe Commerce Optimizer

O Adobe Commerce Optimizer oferece suporte ao gerenciamento de catálogos, à descoberta de produtos, à pesquisa, às recomendações e às experiências da loja, permitindo que você mantenha um back-end de comércio existente. Os dados do catálogo podem vir de fontes externas e um sistema de terceiros pode permanecer responsável pelo ciclo de vida do carrinho e do checkout.

Use essa opção quando a meta for a modernização voltada para o cliente e a substituição do back-end transacional não for necessária. Planeje explicitamente a assimilação de catálogos e as integrações de carrinho e check-out. ACCS e ACO são opções de arquitetura separadas, não uma pilha combinada necessária. Verifique o suporte de integração atual antes de selecionar os serviços para a implementação.

Consulte a [visão geral do Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview).

### Implantações existentes do Adobe Commerce

O Adobe Commerce na infraestrutura em nuvem e em implantações locais também pode adotar vitrines headless e integrações compatíveis baseadas em API de forma incremental. Dependendo da implantação, você pode manter uma loja existente ou adotar uma loja headless compatível. Manter os recursos de comércio existentes juntos pode reduzir o trabalho de integração e, ao mesmo tempo, permitir que serviços selecionados evoluam separadamente.

A disponibilidade de recursos, a compatibilidade de extensões, o licenciamento e os requisitos de configuração variam de acordo com a oferta e a versão. Compare as [plataformas e os serviços da Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce/information-center/explore-platforms-and-services/platform-and-services) antes de escolher uma arquitetura.

## Commerce Storefront ativado por Edge Delivery Services

A Commerce Storefront baseada na Edge Delivery Services fornece a experiência da loja e a camada de entrega de conteúdo. Sua arquitetura headless permite que as equipes desenvolvam o front-end independentemente da base de comércio. A criação baseada em documentos e a edição visual são compatíveis com atualizações de conteúdo, enquanto os componentes da loja usam APIs de comércio para recursos de compra.

Diferencie a interface da loja dos sistemas responsáveis por dados de catálogo, preços, operações do carrinho, check-out e pedidos. O Edge Delivery Services não substitui o back-end de comércio transacional. Identifique os serviços compatíveis e o caminho de integração para o back-end escolhido antes de implementar a loja.

Consulte a [documentação da Commerce Store](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Integração e extensibilidade

A API Mesh e o App Builder ajudam a conectar e estender os recursos de comércio sem exigir que cada personalização seja incorporada ao aplicativo principal de comércio.

### API Mesh

A API Mesh para Adobe Developer App Builder combina várias fontes de API do Adobe, privadas e de terceiros em um endpoint do GraphQL consultável. Use-a para compor dados para experiências de front-end e coordenar o acesso aos serviços existentes.

A composição da API não elimina a necessidade de definir contratos de API, autenticação, tratamento de erros ou propriedade da lógica de negócios transacional. Mantenha essas responsabilidades explícitas no design de integração.

Consulte a [visão geral da API Mesh](https://developer.adobe.com/graphql-mesh-gateway/).

### Adobe App Builder

O Adobe App Builder fornece uma plataforma para aplicativos que estendem as soluções da Adobe e são executados na infraestrutura da Adobe, incluindo o Adobe I/O Runtime. Você pode usá-lo para personalizações e integrações fora do processo com sistemas como CRMs, ERPs e PIMs.

Escolha pontos de extensão, eventos e webhooks compatíveis para a oferta do Commerce que você usa. Projete e teste o aplicativo separadamente do ciclo de vida da versão principal de comércio.

Consulte a [visão geral do App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/).

## MCPs e habilidades de desenvolvimento do Commerce

Os MCPs de desenvolvimento e as habilidades do Commerce dão suporte ao desenvolvimento assistido por IA de aplicativos e personalizações de vitrine da App Builder. Eles também podem ajudar a migrar extensões Adobe Commerce PHP existentes para aplicativos App Builder ao migrar para o ACCS.

Os servidores do protocolo de contexto de modelo (MCP) conectam clientes de codificação de IA compatíveis com ferramentas de desenvolvimento. As ferramentas do Adobe incluem o Commerce Developer MCP Server, o App Builder MCP Server e o Dropins AI Tools, juntamente com habilidades específicas do Commerce.

Os MCPs de desenvolvimento do Commerce são ferramentas de desenvolvimento, não serviços de entrega de vitrines, carrinho, finalização ou processamento de pedidos. Eles não tornam um aplicativo compatível com todas as ofertas do Commerce automaticamente. Revise as alterações geradas e teste-as no ambiente de destino.

Consulte [MCPs e habilidades de desenvolvimento do Commerce](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools).

## Planejar uma implementação combinável

1. Defina metas de negócios, experiências do cliente, requisitos de segurança e as habilidades disponíveis para sua equipe.
2. Escolha a plataforma de comércio e identifique quais sistemas existentes serão retidos ou substituídos.
3. Selecione uma loja compatível e defina os limites entre os serviços de apresentação, merchandising e transacionais.
4. Estabeleça a propriedade de dados e os contratos de API para informações de catálogo, preços, inventário, clientes, carrinhos, finalização e pedidos.
5. Planeje a autenticação, a sincronização de dados, o armazenamento em cache, o monitoramento e o tratamento de falhas em integrações.
6. Implemente de forma incremental e valide a funcionalidade, o desempenho e a segurança antes de cada versão.

Uma implementação combinável é bem-sucedida quando seus componentes atendem aos requisitos de negócios e funcionam juntos de forma confiável. Selecione os recursos necessários em vez de adicionar serviços apenas para tornar a arquitetura mais modular.

## Recursos relacionados

Explore estes tutoriais, vídeos, guias de implementação e a lista de reprodução para planejar sua arquitetura e criar integrações comerciais.

### Plataformas e vitrines do Commerce

* [Arquitetura do Adobe Commerce as a Cloud Service](../commerce-as-a-cloud-service/architecture.md)
* [Vitrines combináveis e arquitetura modular](../commerce-as-a-cloud-service/product-overview/composable-storefront-and-modular-architecture.md)
* [Visão geral do Adobe Commerce Optimizer](../adobe-commerce-optimizer/overview.md)
* [Por que existe o modelo de dados do catálogo de composição](../adobe-commerce-optimizer/composable-catalog-data-model/why-ccdm-exists.md)
* [Experiências do comprador com o Edge Delivery Services](../edge-delivery-services/shopper-experience.md)

### Integração e desenvolvimento

* [Extensibilidade fora do processo com o App Builder](../app-builder/foundations/introduction-to-app-builder.md)
* [Introdução à API Mesh](../api-mesh/getting-started-api-mesh.md)
* [Criar uma malha de API com várias fontes](../api-mesh/graphql-multiple-source.md)
* [Criar taxas de envio personalizadas com ferramentas de IA e MCP](../app-builder/custom-shipping-rates-ai-tools/ai-tools-starter-kit.md)

### Documentação de arquitetura e desenvolvimento

* [Migrar para o Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/migration/overview)
* [Integrações do Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/integrations-overview)
* [Introdução ao desenvolvimento da Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)
* [Práticas recomendadas para MCPs e habilidades de desenvolvimento do Commerce](https://developer.adobe.com/commerce/extensibility/developer-agent/best-practices)

### Lista de reprodução

* [Introdução à API Mesh usando o Adobe App Builder e o Adobe Commerce](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh)
