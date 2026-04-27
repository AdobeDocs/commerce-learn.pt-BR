---
title: 'Criar uma POC de pagamento dividido: ferramentas do App Builder e da IA'
description: Saiba mais sobre uma prova de conceito de pagamento dividido com o App Builder e o Commerce PaaS, incluindo metas, arquitetura e o que esta primeira sessão aborda.
feature: App Builder, Paas, Payments
topic: App Builder, Commerce, Development, Integrations
role: Developer, Leader, User
level: Intermediate
doc-type: Technical Video
duration: 259
jira: KT-20791
source-git-commit: 47b35088f2d3139d58791a2f7d327159db8f2175
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# Criar uma POC de pagamento dividido: ferramentas do App Builder e da IA

Este é o primeiro de um conjunto de tutoriais que apresentam o uso do desenvolvimento assistido por IA para ajudar você a criar uma prova de conceito de pagamento dividido. Você trabalha com o Adobe App Builder e o Adobe Commerce na nuvem (PaaS) ou no local, passando de uma visão geral nesta sessão para os tutoriais práticos que se seguem. Espere metas, arquitetura de alto nível e um roteiro para o que o restante da série aborda.

## Vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3483938?captions=por_br&learn=on)

## Detalhes importantes


Este tutorial elimina a lacuna entre onde a maioria das equipes do Adobe Commerce está hoje — no PHP — e onde a Adobe deseja que elas vão: lógica de negócios orientada por eventos e sem servidor rodando fora do Commerce no Adobe App Builder. Ele faz isso através de um recurso real e funcional em vez de um exemplo de brinquedo.

### O que você realmente vai construir

Um sistema de pagamento dividido em que os clientes pagam usando uma combinação de Dinheiro na Entrega e Crédito da Loja. Depois que o pedido é feito, um operador (ou sistema ERP) confirma ou recusa o pagamento em dinheiro por meio de um painel independente — sem nunca abrir o Commerce Admin. Todo o fluxo de trabalho de aceitação/recusa é executado no App Builder.
A lição de arquitetura (este é o principal ensino)
O tutorial demonstra uma estrutura de decisão deliberada e repetível:

O que deve ficar no PHP: qualquer coisa que seja executada de forma síncrona no ciclo de solicitação do Commerce ou que chame APIs internas da Commerce sem superfície externa limpa
O que muda para o App Builder: tudo o mais — processamento de eventos, fluxo de trabalho do operador, integrações externas e ferramentas voltadas para o operador

Isso não é &quot;mover tudo para o App Builder&quot;. É um ponto de partida prático e honesto para equipes que precisam começar a transição sem precisar reescrever.

### Por que o código PHP não está incluído

A abordagem de prompt da IA é melhor do que o código de amostra para esse caso de uso, pois o prompt captura os contratos comportamentais e o raciocínio arquitetônico que o código de amostra sozinho não pode transmitir. Um desenvolvedor que executa o prompt e lê a saída entende por que o código é formado da maneira que é, não apenas sua aparência.

### O que está incluído

Código completo do aplicativo do App Builder (consistente em todos os projetos — use-o diretamente ou como referência)
Um conjunto completo de prompts de IA numerados, criados para o Cursor e o Claude, abrangendo o módulo do Commerce, o orquestrador do App Builder, o painel do operador, os testes e o caminho para a produção
Um script de simulação para testar o fluxo de aceitação/recusa em um site Commerce ativo sem precisar de um ERP real
Documentação da arquitetura explicando cada decisão

### Para quem isto é

Desenvolvedores no Adobe Commerce no local ou no Commerce Cloud que estão iniciando sua primeira integração real com o App Builder. Não para a implantação totalmente headless da API — especificamente para equipes na transição, executando uma loja tradicional, que desejam ver como descarregar a lógica de negócios real para o App Builder sem abandonar o investimento existente no PHP.

### Texto Explicativo de Pré-requisitos

Adobe Commerce 2.4.5 ou posterior, acesso a uma organização da Adobe Developer Console com um projeto do App Builder e eventos de E/S ativados. Um tema limpo do Luma é presumido para a interface do usuário de check-out — os temas personalizados exigirão o ajuste do prompt antes da execução.

### Pensamentos finais

Este deve ser considerado um debate de nível inicial sobre o desenvolvimento assistido por IA. Este tutorial é uma demonstração do uso das ferramentas de IA em um fluxo de trabalho de desenvolvimento do Commerce, não apenas um tutorial sobre pagamentos divididos.
