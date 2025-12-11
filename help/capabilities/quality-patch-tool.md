---
title: Ferramenta de correção de qualidade
description: Saiba como usar a ferramenta de correção de qualidade ao diagnosticar um problema, encontrar uma solução e aplicar uma correção encontrada na lista existente de correções disponíveis.
feature: Cloud, Configuration, Logs, System, Tools and External Services
topic: Architecture, Commerce, Development
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Technical Video
duration: 771
last-substantial-update: 2024-07-17T00:00:00Z
jira: KT-15836
exl-id: 16710f27-1232-4c6a-aac3-9838308d1267
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Ferramenta de correção de qualidade

Saiba como usar a ferramenta de correção de qualidade ao diagnosticar um problema, encontrar uma solução e aplicar uma correção encontrada na lista existente de correções disponíveis.

## O que você vai aprender

Saiba como fazer a triagem de um problema e usar algumas técnicas básicas para encontrar um patch de qualidade para aplicar uma correção.

## Público-alvo

* Desenvolvedores aprendendo como encontrar problemas e aproveitar essa ferramenta para aplicar patches GIT para problemas conhecidos

## Conteúdo de vídeo

A Ferramenta de correção de qualidade é um utilitário de linha de comando para Adobe Commerce e Magento Open Source. Veja o que ele permite que você faça:

* Exibir informações gerais sobre os patches de qualidade mais recentes.
* Aplique patches de qualidade à sua instalação.
* Reverter patches aplicados, se necessário

Esses patches são desenvolvidos por desenvolvedores da Adobe na comunidade da Magento Open Source para melhorar a estabilidade e o desempenho. Lembre-se de que isso não é recomendado para aplicar um grande número de patches, pois pode complicar atualizações futuras.

>[!VIDEO](https://video.tv.adobe.com/v/3454073?captions=por_br&learn=on)

## Por que usar a ferramenta de correção de qualidade

Talvez você queira usar a Ferramenta de correções de qualidade para o Adobe Commerce ou Magento Open Source se estiver procurando:

Melhorar a estabilidade e o desempenho: os patches de qualidade resolvem problemas, melhoram a segurança e otimizam a sua instalação.
Mantenha-se atualizado: a aplicação de patches garante que seu sistema esteja atualizado e protegido.
Reverter alterações: se um patch causar problemas inesperados, você poderá revertê-lo usando a ferramenta. Lembre-se de que ele é mais adequado para aplicar um número limitado de patches, evitando complicar atualizações futuras.  

## Limitações ou preocupações com o uso da ferramenta de correção de qualidade

Embora a Ferramenta de correção de qualidade ofereça benefícios, há algumas considerações a serem levadas em conta:

* Compatibilidade: verifique se os patches são compatíveis com sua versão específica do Adobe Commerce ou Magento Open Source.
* Teste: sempre teste patches em um ambiente de preparo antes de aplicá-los à produção. Problemas inesperados podem surgir.
* Dependências de Patch: Alguns patches podem depender de outros. Esteja ciente de qualquer pré-requisito.
* Personalizações: se você tiver feito alterações no código personalizado, os patches podem entrar em conflito. Revise as alterações com cuidado.
* Backup: faça backup da instalação antes de aplicar patches para evitar perda de dados.

Embora a Ferramenta de correção de qualidade seja útil para aplicar um número limitado de correções, ela não é recomendada para manipular um grande volume de correções. A aplicação de muitos patches pode complicar atualizações e manutenção futuras. Se você tiver vários patches para aplicar, considere abordagens alternativas ou consulte um especialista da Magento. 

## Resumo

A Ferramenta de correção de qualidade permite que plataformas de comércio eletrônico melhorem a estabilidade e a segurança aplicando correções. Esses patches resolvem problemas, melhoram o desempenho e otimizam o sistema. Manter sua instalação atualizada garante proteção contra vulnerabilidades.

Antes de aplicar patches, é crucial testá-los em um ambiente de preparo. Garanta a compatibilidade com sua versão específica do Adobe Commerce ou Magento Open Source. Alguns patches podem ter dependências, portanto, analise os pré-requisitos cuidadosamente.

 Faça backup da instalação antes de aplicar patches para evitar perda de dados. Se você tiver feito alterações no código personalizado, esteja ciente de que os patches podem entrar em conflito. Siga as práticas recomendadas e monitore o impacto de cada patch.

## Artigos e vídeos relacionados

* [Pesquisa de Ferramentas de Correção de Qualidade](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=pt-BR)
* [Notas de versão](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/quality-patches-tool/release-notes)
* [Github para patches](https://github.com/magento/quality-patches/blob/master/patches/os/)
* [Uso da ferramenta de correção de qualidade](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/quality-patches-tool/usage)
* [Vídeo técnico no QPT](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/tools/quality-patch-tool)
