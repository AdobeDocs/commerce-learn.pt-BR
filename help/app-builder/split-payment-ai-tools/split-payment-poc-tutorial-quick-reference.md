---
title: 'POC de pagamento dividido: referência rápida do tutorial'
description: 'Saiba mais sobre o mapa de arquivos POC de pagamento dividido: qual página do Experience League corresponde a cada prompt da IA, ordem de seção sugerida e notas do autor para o check-out da Luma.'
feature: App Builder, Extensibility, Paas, REST, Eventing
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Tutorial
duration: 398
jira: KT-20902
last-substantial-update: 2026-04-27T00:00:00Z
source-git-commit: 1e2c7e0e6d0f2d174b88406ce3fb7c787676ecee
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# POC de pagamento dividido: referência rápida do tutorial

Esta página resume como é organizada a série de tutoriais de prova de conceito de pagamento fracionado. Ele mapeia cada arquivo de prompt de origem numerado para sua página publicada do Experience League, lista uma ordem de seção sugerida para os leitores e coleta notas para os autores e mantenedores.


## Referência arquivo a arquivo

### [Criar uma POC de pagamento dividido: Ferramentas de IA e App Builder](create-a-split-payment-poc-app-builder-and-ai-tools.md)

**Rótulo do Source:** `00_TUTORIAL_OVERVIEW.md` (visão geral conceitual; a série publicada abre com esta página.)

**Finalidade:** Introdução e orientação para o tutorial.

**Por que é necessário:** oferece aos desenvolvedores o &quot;por que&quot; antes do &quot;como&quot;. Explica o que eles vão construir, quem é o público-alvo e criticamente — o que eles devem personalizar se o site for diferente de uma instalação limpa da Luma. Also serves as the table of contents for the rest of the series.

**Uso do tutorial:** Abrindo seção. Define o contexto antes de qualquer etapa técnica.


### [POC de pagamento dividido: decisões de arquitetura e design](split-payment-poc-architecture-and-decisions.md)


**Propósito:** explicação detalhada de cada decisão arquitetônica na PoC.

**Why it&#39;s needed:** The single most common point of confusion when working with this PoC is understanding *why* something is in PHP versus App Builder. Sem esse contexto, os desenvolvedores tentam mover itens que não podem ser movidos (como a aplicação de crédito da loja) e falham. This document pre-empts those failures with clear reasoning.

**Principais tópicos abordados:**

* The &quot;what must stay in PHP&quot; rule and why
* O padrão de dupla imposição de limite
* Por que o aplicativo de crédito de armazenamento não pode ser assíncrono
* Os cinco casos de borda do Commerce tratados por plug-ins
* O fluxo de dados do atributo de extensão a partir da finalização → citação → ordem → Evento de E/S → App Builder

**Uso do tutorial:** seção &quot;Arquitetura&quot; ou &quot;Como funciona&quot;. Pode ser ignorado por desenvolvedores experientes do Commerce, mas é essencial para os recém-chegados do App Builder.


### [POC de pagamento dividido: pré-requisitos e configuração de ambiente](split-payment-poc-prerequisites-and-setup.md)


**Finalidade:** Conclua a lista de verificação de pré-impressão antes que qualquer código seja gravado ou que os prompts sejam executados.

**Por que é necessário:** a fase de instalação tem a maior taxa de falha nos tutoriais. Este documento garante que o administrador do Commerce esteja configurado corretamente (título CQO exato, crédito de armazenamento ativado, cliente de teste tem saldo, integração criada), que o projeto do App Builder tenha Eventos de E/S e que o provedor de eventos do Commerce esteja conectado, e que o ambiente local tenha as versões certas.

**Itens de ênfase:**

* O título de pagamento à vista deve ser exatamente `Cash` (crítico — a JavaScript faz a correspondência de cadeias de caracteres)
* A integração do Commerce deve ser *ativada* (não apenas salva) para que as credenciais OAuth funcionem
* `entity_id` versus `increment_id` explicado aqui para evitar confusão em toda parte

**Uso do tutorial:** &quot;Pré-requisitos&quot; ou seção &quot;Introdução&quot;. Deve ser concluído interativamente — não apenas lido.


### [POC de pagamento dividido: referência de variáveis de ambiente](split-payment-poc-env-reference.md)


**Propósito:** Todas as variáveis de ambiente para todos os três componentes em um único local.

**Por que é necessário:** as mesmas quatro credenciais do OAuth aparecem em três arquivos diferentes com nomes de variáveis diferentes (`COMMERCE_*` versus `COMMERCE_INTEGRATION_*`). Ter uma única referência impede a depuração &quot;por que isso não está funcionando&quot;, em que um conjunto de credenciais tem um erro de digitação.

**Componentes abrangidos:**

* `split-payment-orchestrator/.env`
* `commerce-checkout-starter-kit/.env` (IMS + OAuth)
* `commerce-backend-ui-1/.env.simulation`

**Uso do tutorial:** Barra lateral de referência ou seção &quot;Configuração&quot;. Também usado como um complemento para os prompts de build.


### [POC de pagamento dividido: prompt de IA do módulo Commerce](split-payment-poc-commerce-module-prompt.md)


**Propósito:** Prompt completo de IA independente para gerar todo o módulo PHP `Client_SplitPayment`.

**Por que é necessário:** este é o artefato de compilação primário da IA para o lado do PHP. Ele é escrito para que um desenvolvedor sem experiência em PHP possa entregá-lo ao Cursor (com Claude) e obter um módulo de trabalho. Cada arquivo é especificado, cada contrato comportamental é definido, as notas de implementação críticas são incluídas e os comandos para habilitar o módulo posteriormente são fornecidos.

**Cobertura:**

* Estrutura de arquivo completa (mais de 30 arquivos)
* Esquema de banco de dados, atributos de extensão, endpoints REST, configuração de eventos de E/S
* Todas as classes PHP com especificações comportamentais completas (não apenas assinaturas)
* Especificações do componente de check-out KnockoutJS
* Os cinco plug-ins de casos de borda com explicações sobre por que cada existe
* Chamadas de personalização para temas que não são do Luma

**Uso do tutorial:** seção &quot;Criar o módulo Commerce&quot;. O prompt em si é o artefato — os desenvolvedores o copiam em sua ferramenta de IA e a executam.


### [POC de pagamento dividido: prompt da IA do App Builder orchestrator](split-payment-poc-app-builder-orchestrator-prompt.md)


**Propósito:** Concluir prompt de IA independente para gerar o aplicativo do App Builder `split-payment-orchestrator`.

**Por que é necessário:** as quatro ações do App Builder (`payment-orchestrator`, `payment-accept`, `payment-decline`, `demo-dashboard`) são o núcleo da história &quot;o que saiu do PHP&quot;. Esse prompt gera todos eles com especificações comportamentais completas, estrutura `app.config.yaml` correta e a configuração de registro do evento.

**Cobertura:**

* `app.config.yaml` com todas as quatro ações e o registro do Evento de E/S
* `commerce-client.js` cliente compartilhado OAuth 1.0a
* Todas as quatro ações com especificações lógicas completas
* O stub `store-credit.js` obsoleto (com a explicação de *por que* não é usado — isso é pedagogicamente importante)
* O painel de demonstração com renderização do HTML, filtragem de pedidos e segurança
* `.env.example` com todas as variáveis

**Uso do tutorial:** seção &quot;Criar o aplicativo do App Builder&quot;. Companheiro para o prompt do módulo Commerce.


### [POC de pagamento dividido: prompt da IA de extensão da interface do Experience Cloud](split-payment-poc-experience-cloud-ui-prompt.md)


**Propósito:** Prompt de IA para gerar a extensão opcional SDK da interface do usuário do administrador do Experience Cloud.

**Por que é necessário:** O painel de demonstração no prompt do orquestrador é intencionalmente áspero; é uma prova de conceito, não uma produção. Esta seção mostra aos desenvolvedores a próxima etapa: incorporar o painel de pagamento dividido ao Commerce Admin Shell usando a interface de usuário de administração do SDK. Ele estava faltando inteiramente dos prompts originais.

**Cobertura:**

* `ext.config.yaml` para a extensão SDK da interface do usuário do administrador
* Componentes do React para o painel de pedidos e detalhes do pedido
* Ações de back-end que usam autenticação IMS para listagem e OAuth para aceitação/recusa
* O script de simulação (também usado para teste)

**Uso do tutorial:** seção opcional &quot;Indo além&quot; ou &quot;Caminho de produção&quot;. Pode ser ignorado se o tutorial se concentrar somente na PoC.


### [POC de pagamento dividido: guia de teste e verificação](split-payment-poc-testing-and-verification.md)


**Propósito:** guia de teste passo a passo que cobre cada componente na ordem de verificação correta.

**Por que é necessário:** construir os componentes é metade do trabalho. Os desenvolvedores precisam de um caminho de verificação claro, que comece no nível mais baixo (colunas de banco de dados, pontos de extremidade REST) e vá para o fluxo completo. Os prompts originais tinham uma lista de verificação de configuração, mas nenhum fluxo de teste explícito.

**Cobertura:**

* Verificação de instalação do módulo Commerce
* Verificação da configuração do administrador
* Testes de fumaça do ponto final REST (comandos curl)
* Apresentação da interface de check-out (incluindo casos de validação)
* Teste de proteção de limite
* Teste de posicionamento de pedido completo
* Uso do script de simulação para aceitar e recusar
* Uso do painel de demonstração
* Inspeção do log de ação do App Builder
* Dez modos de falha comuns com correções específicas

**Uso do tutorial:** seção &quot;Teste&quot; ou &quot;Verificação&quot;. Também é importante como referência para a solução de problemas.


### [POC de pagamento dividido: próximas etapas após a prova de conceito](split-payment-poc-next-steps.md)


**Propósito:** Roteiro para transformar a POC em padrões prontos para produção.

**Por que é necessário:** um tutorial PoC corre o risco de deixar os desenvolvedores com um &quot;e agora?&quot; sentimento. Este documento mapeia os avanços naturais da demonstração à produção: substituição do painel de demonstração por uma extensão do Experience Cloud, conexão de um ERP real, adição de uma API Mesh, expansão do fluxo de trabalho do App Builder e lista de verificação de implantação de produção.

**Conteúdo da chave:**

* Diagrama de evolução da arquitetura (PoC → Fase 2 → Fase 3)
* Padrão de integração de ERP (o que muda, o que permanece o mesmo)
* Padrão do agente de malha da API
* Lista de verificação de implantação de produção
* Links de referência de chave

**Uso do tutorial:** seção de fechamento &quot;Próximas etapas&quot;. Também útil como iniciador de conversação para definir o escopo de um projeto real.


## Seções de tutorial sugeridas

Com base nesses arquivos, uma estrutura típica para leitores é:

| Seção Tutorial | Página do Experience League |
| --- | --- |
| Introdução e objetivos de aprendizagem | [Criar uma POC de pagamento dividido: Ferramentas de IA e App Builder](create-a-split-payment-poc-app-builder-and-ai-tools.md) |
| Demonstração completa (vídeo) | [Criar POC de pagamento dividido: demonstração completa do App Builder](create-a-split-payment-poc-app-builder-and-ai-tools-full-demo.md) |
| Arquitetura: o que vive onde | [POC de pagamento dividido: decisões de arquitetura e design](split-payment-poc-architecture-and-decisions.md) |
| Pré-requisitos e configuração | [POC de pagamento dividido: pré-requisitos e configuração de ambiente](split-payment-poc-prerequisites-and-setup.md) |
| Variáveis de ambiente | [POC de pagamento dividido: referência de variáveis de ambiente](split-payment-poc-env-reference.md) |
| Etapa 1: criar o módulo Commerce | [POC de pagamento dividido: prompt de IA do módulo Commerce](split-payment-poc-commerce-module-prompt.md) |
| Etapa 2: criar o App Builder orchestrator | [POC de pagamento dividido: prompt da IA do App Builder orchestrator](split-payment-poc-app-builder-orchestrator-prompt.md) |
| Etapa 3: testar o fluxo de ponta a ponta | [POC de pagamento dividido: guia de teste e verificação](split-payment-poc-testing-and-verification.md) |
| Etapa 4 (opcional): extensão da interface do usuário do administrador | [POC de pagamento dividido: prompt da IA de extensão da interface do Experience Cloud](split-payment-poc-experience-cloud-ui-prompt.md) |
| Próximas etapas e caminho de produção | [POC de pagamento dividido: próximas etapas após a prova de conceito](split-payment-poc-next-steps.md) |


## Observações importantes para autores tutoriais

**Na premissa do tema Luma:** Cada prompt de compilação gera um código para uma instalação limpa do Luma. O tutorial deve indicar isso claramente na parte superior — os desenvolvedores com check-outs personalizados precisarão adaptar os caminhos de injeção do `LayoutProcessorPlugin` e possivelmente a configuração RequireJS. A introdução da série e os prompts de build incluem chamadas de personalização para isso.

**No módulo PHP:** o tutorial explicitamente não fornece o código PHP como um download de copiar e colar. O prompt de IA *gera*. Isso é intencional — ensina o padrão de uso da IA para criar extensões do Commerce, não apenas copiar e colar chapas padrão. No entanto, o código gerado quando solicitado em um ambiente limpo deve corresponder exatamente ao código de trabalho no `app/code/Client/SplitPayment/`.

**No limite de $100:** Este é um valor PoC embutido em código. O tutorial deve observar que as lojas reais desejarão configurar isso por meio da configuração de administração do Commerce, em vez de uma constante de tempo de compilação.

**Dependência de crédito da loja:** O fluxo de pagamento dividido conforme compilado requer `Magento_CustomerBalance` (o módulo de crédito da loja nativa).


{{$include /help/_includes/split-payment-ai-tools-related-links.md}}
