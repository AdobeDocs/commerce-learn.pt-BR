---
title: Saiba mais sobre políticas do CCDM no Modelo de dados de catálogo combinável
description: Saiba como as políticas ESTÁTICAS e DE ACIONAMENTO no Modelo de dados do catálogo combinável do Adobe controlam a visibilidade do produto em visualizações de catálogo sem reconstruir o catálogo.
feature: Saas, Storefront
topic: Commerce
role: Developer
level: Beginner
doc-type: Tutorial
duration: 349
last-substantial-update: 2026-05-21T00:00:00Z
jira: KT-21258
source-git-commit: 456f3cae8c45d137a195456692c2d11204126bb7
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Políticas no modelo de dados do catálogo combinável do Adobe

Se uma **exibição de catálogo** for a lente que molda o que os compradores veem de um catálogo base unificado, as **políticas** serão o que é feito dessa lente. Este tutorial explica o que é uma política, como as políticas **STATIC** e **TRIGGER** funcionam juntas no cenário de demonstração **Automóveis Carvelo** e por que a atualização de uma política entra em vigor imediatamente, sem reconstruir o catálogo.

## Para quem é este vídeo?

* Arquitetos e desenvolvedores de soluções da Commerce que configuram exibições de catálogo e regras de merchandising no Adobe Commerce Optimizer

## Conteúdo de vídeo

* Políticas como filtros de acesso a dados nos atributos do produto
* Como várias políticas se combinam na visualização do catálogo do Celport (marcas e categorias de peça)
* Políticas ESTÁTICAS para regras de negócios permanentes
* Políticas de ACIONAMENTO ativadas por cabeçalhos de solicitação de API (por exemplo `AC-Policy-Brand`)
* Atualização de políticas em operações diárias sem reconstrução de catálogo

>[!VIDEO](https://video.tv.adobe.com/v/3491429?captions=por_br&learn=on)

Uma **política** é um **filtro de acesso a dados**. Ele inspeciona os atributos do produto e aplica regras que determinam quais produtos uma exibição de catálogo pode expor. As políticas ficam na parte superior do catálogo de composição compartilhado — elas não duplicam os dados do catálogo.

## Políticas ESTÁTICAS

Uma política **STATIC** é **always on**. Ela impõe regras de negócios permanentes, independentemente do comportamento do comprador ou do estado da sessão.

No cenário do Celport, as regras STATIC incluem:

* A Celport venderá somente as marcas **Bolt** e **Cruz**.
* Celport só mostrará **freios** e **suspensão** partes.

Estas regras nunca desligam. As políticas STATIC são o local onde residem **contratos de licenciamento**, **restrições territoriais** e **permissões de marca**. Defina-as uma vez e o Adobe Commerce Optimizer as aplicará automaticamente em cada solicitação.

## políticas DE ACIONAMENTO

Às vezes, as políticas com uma origem de valor de **TRIGGER** são chamadas de **políticas exclusivas**. A exibição de catálogo executa essa política **somente quando o gatilho é especificado** no cabeçalho da chamada de API.

Por exemplo, uma loja EDS (Serviços de Entrega de Experiência) pode oferecer uma lista suspensa com **Todas as Marcas**, **Aurora**, **Bolt** e **Cruz**:

* Na exibição da página inicial, nada está selecionado, portanto, nenhum cabeçalho de marca extra é enviado.
* Quando o comprador seleciona **Parafuso**, a API subjacente define o cabeçalho `AC-Policy-Brand` como `Bolt`.
* Quando o comprador seleciona **Cruz**, o mesmo cabeçalho é definido como `Cruz`.

A exibição de catálogo aplica a política TRIGGER somente quando esse cabeçalho está presente, o que oferece suporte à filtragem interativa sem alterar as regras ESTÁTICAS permanentes.

## STATIC e TRIGGER juntos

As políticas **STATIC** lidam com regras permanentes. As políticas **TRIGGER** manipulam as interativas. Usados juntos em uma única exibição de catálogo, eles fornecem **conformidade** e **flexibilidade**—limites de sortimento fixos, além de refinamento orientado pelo comprador.

## Atualizar políticas sem recriar o catálogo

Para operações diárias, as alterações nas políticas são imediatas. Suponha que o contrato de licenciamento da Celport agora permita **pneus**, bem como freios e suspensão:

1. Abra a política relevante.
1. Adicionar **camadas** à lista de valores.
1. Salve.

Esta alteração está **ativa imediatamente**. Não há tempo de espera, reimplantação ou recriação de catálogo. A próxima solicitação para a loja Celport reflete a atualização.

As políticas são filtros leves em um **catálogo compartilhado**, não regras transformadas em cópias de catálogo separadas. **Alterar a regra, não os dados.**

## Conteúdo relacionado

* [Por que existe o modelo de dados do catálogo de composição](./why-ccdm-exists.md)
* [Saiba mais sobre Exibições de catálogo](./learn-about-the-ccdm-feature-catalog-views.md)
* [Exibições de catálogo para serviços de merchandising](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/catalog-view){target="_blank"}
* [Guia do [!DNL Adobe Commerce Optimizer]](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview){target="_blank"}
* [Introdução à API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#make-your-first-request){target="_blank"}

