---
title: Por que o Composable Catalog Data Model (CCDM) Existe
description: Saiba como o CDM mantém um catálogo unificado enquanto as lojas recebem produtos, preços e regras filtrados usando visualizações de catálogo e Serviços de merchandising.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 259
last-substantial-update: 2026-05-15T00:00:00Z
jira: KT-18624
source-git-commit: 456f3cae8c45d137a195456692c2d11204126bb7
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Por que existe o modelo de dados do catálogo de composição

Equipes de comércio modernas geralmente vendem em **marcas**, **regiões**, **concessionárias** e **canais digitais**. Quando cada canal mantém sua própria cópia do catálogo, as equipes gastam mais tempo reconciliando SKUs, preços e disponibilidade do que melhorando a experiência do comprador. O **Adobe Composable Catalog Data Model (CCDM)** por trás de **Adobe Commerce Optimizer** foi criado para inverter esse padrão: **um catálogo unificado** em uma camada SaaS, com **exibições de catálogo** e **políticas** moldando o que cada vitrine ou integração tem permissão para ver.

## Para quem é este vídeo?

* Arquitetos e desenvolvedores de soluções da Commerce que são novos no Adobe Commerce Optimizer e precisam do contexto de negócios antes de configurar fontes, visualizações e políticas de catálogos

## Conteúdo de vídeo

* Por que os catálogos duplicados e específicos de canal criam risco operacional e inovação mais lenta
* Como a CCDM mantém os dados do produto unificados enquanto ainda suporta cenários de várias marcas e de várias regiões
* Como as exibições de catálogo atuam como as &quot;lentes&quot; entre um catálogo base compartilhado e uma loja ou público-alvo específico
* Como as APIs de serviços de merchandising consomem essas visualizações para que as experiências headless permaneçam alinhadas ao catálogo configurado

>[!VIDEO](https://video.tv.adobe.com/v/3491290?captions=por_br&learn=on)

## O desafio com catálogos em silos

Quando cada site de revendedor, loja regional ou propriedade de marca mantém **seu próprio banco de dados de catálogo**, vários problemas se agravam:

* **Duplicação** — a mesma SKU, descrição e mídia são inseridas várias vezes.
* **Deriva** — atualizações de preço, novos atributos ou itens descontinuados chegam a um canal, mas não a outros.
* **Inicializações mais lentas** — cada novo ponto de contato repete um trabalho pesado com dados em vez de reutilizar um único registro de produto.

O CCDM existe para que as informações do produto possam ficar em **um catálogo combinável** que outros sistemas enriquecem, enquanto as vitrines ainda recebem sortimentos e preços **apropriados para canal**.

## O que muda o modelo de dados do catálogo de composição

No Adobe Commerce Optimizer, os dados do produto são **assimilados em um catálogo base unificado** de uma ou mais **fontes de catálogo** (por exemplo, uma localidade como `en-US` ou sistemas upstream como um PIM ou ERP). Essa origem fornece os atributos e valores brutos.

**As exibições de catálogo** definem como os dados unificados são **organizados e expostos** para um contexto comercial: quais produtos passam por suas **políticas**, quais **catálogos** se aplicam e qual **fonte de catálogo** dá suporte à exibição. Os mesmos registros subjacentes podem, portanto, suportar **muitas projeções**, por exemplo, exibições separadas por revendedor, região ou marca, sem clonar todo o catálogo de cada site.

Essa separação—**de onde os dados vêm** (origem do catálogo) versus **como são apresentados** (exibição do catálogo) — é o motivo principal pelo qual as equipes adotam o CCDM em vez de manter catálogos paralelos por canal.

## Exibições de catálogo como lentes de vitrine

Conforme descrito em [Exibições de Catálogo para Serviços de Merchandising](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/catalog-view){target="_blank"}, uma exibição de catálogo se comporta como uma **lente**: os compradores só veem os produtos, os preços e as regras permitidos pela exibição, enquanto o **catálogo base** permanece o sistema compartilhado de registro. Esse modelo é emparelhado diretamente com os **Serviços de merchandising** para que os clientes da API passem a exibição correta (e os cabeçalhos relacionados) e recebam uma resposta consistente e orientada por políticas para cada experiência.

Para obter uma apresentação mais detalhada de como essas partes se encaixam em um fluxo de ponta a ponta, consulte a apresentação do desenvolvedor [Criar um catálogo combinável para sua loja](https://developer.adobe.com/commerce/services/optimizer/ccdm-use-case){target="_blank"}.

## Conteúdo relacionado

* [Saiba mais sobre Exibições de catálogo](./learn-about-the-ccdm-feature-catalog-views.md)
* [Exibições de catálogo para serviços de merchandising](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/catalog-view){target="_blank"}
* [Criar um catálogo combinável para sua loja](https://developer.adobe.com/commerce/services/optimizer/ccdm-use-case){target="_blank"}
* [Guia do [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview){target="_blank"}
* [Introdução à API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#make-your-first-request){target="_blank"}

