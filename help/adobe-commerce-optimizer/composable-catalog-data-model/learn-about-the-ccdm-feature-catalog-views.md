---
title: Saiba mais sobre Exibições de catálogo no Modelo de dados de catálogo combinável
description: Saiba como as visualizações de catálogo no Adobe Composable Catalog Data Model (CCDM) mapeiam um catálogo base para cada loja com produtos, preços e regras distintos.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 297
last-substantial-update: 2026-05-15T00:00:00Z
jira: KT-21132
source-git-commit: 96a1356a399fa5cdca9d9befd7c14ebad1b0162f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Exibições de catálogo no Modelo de dados do catálogo combinável do Adobe

As exibições de catálogo mostram como você atende cada público-alvo de forma diferente de um único catálogo combinável. Este tutorial explica o que é uma exibição de catálogo, como a Adobe Commerce Optimizer a aplica a um comprador e por que uma ID de exibição exclusiva é a âncora para produtos, preços e regras, usando o cenário de demonstração **Automóveis Carvelo**.

## Para quem é este vídeo?

* Arquitetos e desenvolvedores de soluções da Commerce que modelam catálogos de várias marcas ou de vários revendedores na Adobe Commerce Optimizer

## Conteúdo de vídeo

* O cenário Carvelo Automobiles (marcas, concessionárias e contratos)
* O que é uma visualização de catálogo e a metáfora da &quot;lente&quot; sobre um catálogo de base unificado
* Como uma loja usa uma exibição de catálogo para filtrar produtos e preços (por exemplo, Celport)
* IDs exclusivas de visualização de catálogo e o valor comercial de uma única fonte da verdade

>[!VIDEO](https://video.tv.adobe.com/v/3491261?learn=on)

## Cenário: Carvelo Automobiles

A **Carvelo Automobiles** é uma empresa fictícia de autopeças usada com frequência em demonstrações, documentação e tutoriais da Adobe Commerce. A Carvelo vende peças em três marcas —**Aurora**, **Bolt** e **Cruz** — por meio de três concessionárias:

* **Arkbridge** pertence à West Coast Inc.
* **Kingsbluff** e **Celport** pertencem à East Coast Inc.

Cada concessionária tem seu próprio acordo sobre quais produtos está autorizada a vender. Isso cria uma configuração realmente complexa e ainda pode ser executada a partir de **um único catálogo base** de cerca de seis milhões de SKUs. O recurso que torna isso possível é uma **exibição de catálogo**.

## O que é uma exibição de catálogo?

Uma **exibição de catálogo** é uma exibição configurada do catálogo para um contexto comercial específico. Pense nisso como uma **lente**. Seu catálogo básico unificado fica no meio, mantendo cada SKU para cada marca. Cada concessionária recebe sua própria lente - sua própria visualização de catálogo.

No exemplo:

* A lente **Arkbridge** pode mostrar todas as três marcas: Aurora, Bolt e Cruz.
* A lente **Celport** mostra apenas um subconjunto de partes de Parafuso e Cruz.

Cada exibição de catálogo também pode controlar **preços**. Os **dados do catálogo subjacente não são alterados**. Somente os aspectos visualizáveis (classificação, preço e regras) são alterados para esse contexto.

## Como o Commerce Optimizer aplica uma exibição de catálogo

Quando um comprador visita a loja **Celport**, a Adobe Commerce Optimizer usa a **exibição do catálogo do Celport** para determinar exatamente quais produtos, preços e regras se aplicam. O comprador só vê o que as lentes permitem.

Outros produtos ainda podem existir no catálogo — por exemplo, pneus Aurora, motores Bolt ou baterias Cruz — mas a loja da **Celport nunca os expõe** se a exibição do catálogo não permitir.

## ID de visualização do catálogo e valor comercial

Toda exibição do catálogo tem uma **ID exclusiva**. Essa ID é o que conecta a loja à configuração do catálogo. Você o define uma vez na configuração da loja e o comportamento de downstream o segue: os produtos certos, os preços certos e as regras certas.

Em vez de manter catálogos separados para cada revendedor ou marca — e mantê-los sincronizados — você mantém o catálogo combinável **one**. As exibições de catálogo mostram **muitas experiências de vitrine diferentes** dessa **única fonte da verdade**.

## Conteúdo relacionado

* [Guia do [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview){target="_blank"}
* [Introdução à API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/#make-your-first-request){target="_blank"}
