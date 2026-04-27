---
title: Ferramenta de correção de qualidade
description: Saiba como usar a ferramenta de correção de qualidade ao diagnosticar um problema, encontrar uma solução e aplicar uma correção encontrada na lista existente de correções disponíveis.
feature: Cloud, Configuration, Logs, System, Tools and External Services
topic: Architecture, Commerce, Development
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Technical Video
duration: 903
last-substantial-update: 2024-07-17T00:00:00.000Z
jira: KT-15836
exl-id: 16710f27-1232-4c6a-aac3-9838308d1267
TQID: https://experienceleague.adobe.com/GpcJqSCn3XqLZtm-QdQ-ka9c-RdkG-C6Hd3FpXrh8-I
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 593
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

>[!VIDEO](https://video.tv.adobe.com/v/3431436?learn=on)

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

* [Pesquisa de ferramentas de correção de qualidade](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html?lang=pt-BR)
* [Notas de versão](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/quality-patches-tool/release-notes)
* [Github para patches](https://github.com/magento/quality-patches/blob/master/patches/os/)
* [Uso da ferramenta de correção de qualidade](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/quality-patches-tool/usage)
* [Vídeo técnico no QPT](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/tools/quality-patch-tool)
