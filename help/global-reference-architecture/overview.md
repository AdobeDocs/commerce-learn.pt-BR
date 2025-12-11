---
title: Otimização da reutilização do código com o Adobe Commerce
description: Saiba como otimizar a reutilização de código no Adobe Commerce com padrões de arquitetura de referência global, melhorando o desempenho e a conformidade em várias instâncias.
kt: 15773
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: 5475ade8-028c-4b24-a563-60dcda5ba93a
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 0%

---

# Técnicas de implementação da arquitetura de referência global

Há várias maneiras de otimizar a reutilização do código com o Adobe Commerce. Cada uma dessas quatro técnicas de implementação tem suas próprias vantagens. Os exemplos neste artigo são ordenados de simples a mais complexo. Escolha a estratégia que melhor se adapta ao seu projeto e ao futuro roteiro. A migração de uma estratégia para outra pode ser demorada.

## Quando usar a arquitetura de referência global

A arquitetura de referência global pode ser valiosa, dependendo do número de instâncias que você possui. Uma instância é uma instalação independente do Adobe Commerce usando seu próprio banco de dados. Conte o número de bancos de dados de produção para saber quantas instâncias você possui. Se você mantiver mais de uma instância ou se previr esse cenário no futuro, poderá se beneficiar da arquitetura de referência global. Quanto mais funcionalidades as instâncias compartilham, mais valor uma arquitetura de referência global agrega.

Em qualquer um desses cenários, é aconselhável explorar o uso de várias instâncias do Adobe Commerce.

1. **Proprietários de Repositório Diferentes**: se você mantiver o código para vários proprietários de repositórios, cada um com seu próprio repositório distinto, instâncias separadas poderão ser necessárias para manter seus requisitos individuais de maneira eficaz.
2. **Conformidade com as Regulamentações Nacionais**: certas regulamentações exigem que os dados do cliente sejam armazenados em regiões específicas. Nesses casos, instâncias separadas são essenciais para garantir a conformidade com essas regulamentações.
3. **Variações operacionais entre regiões geográficas**: operar em várias regiões pode significar diferentes agendamentos e requisitos de manutenção. O uso de instâncias separadas permite flexibilidade no gerenciamento eficiente dessas variações.
4. **Vendas de Flash de Alta Intensidade**: lojas que realizam vendas de flash em larga escala geralmente exigem desempenho otimizado de servidor. A infraestrutura dedicada fornecida por instâncias separadas garante o desempenho ideal durante esses períodos de alta demanda.
5. **Diferenças Significativas entre Marcas ou Países**: quando a diferença entre marcas ou países é grande, o uso de uma única instância resulta em um código que é usado apenas para algumas marcas ou países. Instâncias separadas podem melhorar o desempenho e a estabilidade, eliminando códigos desnecessários para marcas e países que não precisam deles.

## Padrões da arquitetura de referência global

Ao lado de &quot;nenhum padrão GRA&quot; há quatro estilos de padrões GRA.

![5 ícones de padrões GRA: sem GRA, split, bulk, split e monorepo.](/help/assets/global-reference-architecture/gra-patterns-horizontal.png){align="center"}

### Nenhum padrão GRA

![Um ícone que representa &quot;sem GRA&quot;](/help/assets/global-reference-architecture/no-gra.png){align="center"}

Quando um padrão GRA não é usado, cada instância do Adobe Commerce é um aplicativo exclusivo. Não há reutilização de código, exceto ao mover manualmente o código de uma instância para outra. Essas cópias sempre divergem. O esforço necessário para garantir que cada instância tenha as mesmas alterações, mas ainda funcione conforme o esperado, pode se tornar excessivo. Nesse cenário, três instâncias precisam de três vezes o esforço de manutenção de uma instância.

![Um diagrama que representa três armazenamentos, onde cada um é uma cópia do primeiro, com desenvolvimento único ocorrendo em todas as três cópias.](/help/assets/global-reference-architecture/no-gra-pattern-diagram.png){align="center"}

### O padrão Git GRA dividido

![Um ícone que representa o padrão GRA &quot;dividido&quot;](/help/assets/global-reference-architecture/split-git.png){align="center"}

Esse padrão consiste em repositórios Git para desenvolvimento e um repositório Git por instância. Cada arquivo na instância é mantido em um dos repositórios de desenvolvimento. Eles se unem como uma trança formando todo o GRA. Cada linha de código existe apenas em um único repositório de desenvolvimento e é instalada nas instâncias usando a técnica de encadeamento, resultando na reutilização do código.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA dividido](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"}

### O padrão GRA de pacotes em massa

![Um ícone que representa o padrão GRA &quot;em massa&quot;](/help/assets/global-reference-architecture/bulk-packages.png){align="center"}

Os módulos principais do Adobe Commerce e de terceiros são instalados diretamente pelos repositórios do Composer. Os repositórios Git podem ser usados como repositórios do Composer. Neste padrão, toda a base de código compartilhada do GRA é hospedada em um único ou alguns repositórios Git e instalada por meio do Composer. A principal característica é que vários módulos, pacotes de idiomas ou temas são hospedados em um único pacote de compositor, simplificando o desenvolvimento.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA de pacotes em massa](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"}

### Os pacotes separados padrão GRA

![Um ícone que representa o padrão GRA &quot;pacotes separados&quot;](/help/assets/global-reference-architecture/separate-packages.png){align="center"}

Cada módulo, pacote de idiomas ou tema do Adobe Commerce é instalado como um pacote de compositor separado. Cada personalização tem seu próprio repositório Git. Isso significa flexibilidade máxima na composição das instâncias e tem um gerenciamento de dependência confiável do Composer. Para otimização de desempenho, todos os pacotes são espelhados em um único repositório de compositor privado.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA de pacotes separados](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"}

### O padrão monorepo GRA

![Um ícone que representa o padrão GRA &quot;monorepo&quot;](/help/assets/global-reference-architecture/monorepo.png){align="center"}

Todo o desenvolvimento ocorre em um único repositório de código. A automação gera pacotes para novas versões e os publica em um repositório do compositor. O padrão combina a baixa sobrecarga de desenvolvimento da abordagem de pacotes em massa com a flexibilidade da abordagem de pacotes separados. O padrão monorepo também é ideal para executar testes funcionais automatizados.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA monorepo](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"}

## Escolha de um padrão GRA

A escolha de um padrão GRA é feita avaliando a complexidade do projeto, a necessidade de flexibilidade e a capacidade de adaptação da equipe de desenvolvimento.

Equipes com pouca experiência em Adobe Commerce têm um início simples. No entanto, se o projeto exigir um padrão GRA mais complexo devido às suas características, não comprometa.

Características comuns do projeto relacionadas a cada padrão:

1. **Nenhum padrão GRA**: instância única do Adobe Commerce sem planos de estender. Várias instâncias do Adobe Commerce com compatibilidade mínima entre elas.

2. **Padrão Git GRA dividido**: equipes que desejam evitar o Composer para suas personalizações. Na maioria dos casos, o padrão de pacotes em massa é um padrão preferencial para o Git dividido.

3. **Padrão GRA de pacote em massa**: base de código de personalização com alta interdependência. Todas as instâncias têm combinações muito semelhantes de pacotes personalizados. Nenhuma promoção ou rebaixamento frequentes de pacotes individuais. Equipes com pouca experiência em gerenciamento de código e que precisam de simplicidade.

4. **Padrão GRA de pacotes separados**: gerenciamento flexível do escopo de versão necessário. Há previsão de 50 ou menos pacotes personalizados para os próximos 5 anos. Potencialmente, camadas globais e regionais de código comum. Não há planos para migrar para um padrão Monorepo. A equipe é tecnicamente adepta e tem estrita adesão ao processo.

5. **Padrão GRA de Monorepo**: todas as características do padrão GRA de pacotes separados. Mais de 50 pacotes estão previstos para os próximos 5 anos. Necessidade de testes automatizados abrangentes. Suporte para ambientes efêmeros. Base de código complexa de escala corporativa que precisa ser dimensionada sem dimensionar o custo de manutenção a uma taxa igual.

### O custo de uma escolha errada

A migração de um padrão para outro é possível. O diagrama abaixo mostra o nível de impacto da mudança de um padrão para outro. As linhas verdes mostram baixo impacto, as linhas amarelas e âmbar mostram migrações moderadamente complexas a complexas.

![Um diagrama que mostra setas coloridas entre todos os 4 padrões de GRA, indicando o nível de dificuldade para mover de um para o outro.](/help/assets/global-reference-architecture/wrong-choice.png){align="center"}
