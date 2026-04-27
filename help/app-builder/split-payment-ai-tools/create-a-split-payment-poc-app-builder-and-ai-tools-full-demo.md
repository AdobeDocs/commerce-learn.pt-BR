---
title: 'Criar uma POC de pagamento dividido: demonstração completa do App Builder'
description: Saiba como o pagamento dividido, REST, E/S da App Builder e o operador aceitam/rejeitam o trabalho nesta demonstração do Luma, além de um total de pré-pedido configurável que pode bloquear o carrinho.
feature: App Builder, Paas, Payments
topic: App Builder, Commerce, Development, I/O Events, Integrations, Runtime
role: Developer, Leader, User
level: Intermediate
doc-type: Technical Video
duration: 955
jira: KT-20902
last-substantial-update: 2026-04-24T00:00:00Z
source-git-commit: b98e827d7017c59b0df4c459ea913d69a55f0d56
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---

# Criar uma POC de pagamento dividido: demonstração completa do App Builder

Esta é a apresentação completa da prova de conceito de pagamento dividido criada no Adobe Commerce e no Adobe App Builder. A demonstração pressupõe que você já tenha usado ferramentas de IA e um prompt para produzir a extensão do Commerce em andamento e o aplicativo do App Builder; este vídeo mostra o que acontece depois que o código é mesclado, implantado no Commerce na nuvem (Luma) e o projeto do App Builder está ativo.

Um comprador paga com parte em dinheiro e parte **[!UICONTROL Store Credit]**. A Commerce é proprietária da finalização síncrona e das APIs de que a loja precisa; a App Builder lida com orquestração, fluxos de trabalho de operador e consumidores de eventos de E/S. A implementação de referência usa um projeto Commerce (PaaS) e o checkout nativo do Luma, em vez de uma loja da Edge Delivery Services, que ainda é um caminho comum para muitos comerciantes. Se você usar o **Adobe Commerce as a Cloud Service** em uma topologia diferente, o código do App Builder permanecerá semelhante, mas o trabalho na loja e em andamento parecerão diferentes. Para locais, auto-hospedados e Commerce na nuvem no Luma, este vídeo mostra uma divisão prática entre o código em andamento e o App Builder para novas funcionalidades.

## Vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3484087?learn=on)

## Para quem é este vídeo?

* Arquitetos técnicos que planejam a extensibilidade do Commerce
* Desenvolvedores implementando checkout e integrações
* Equipes de implementação que precisam de uma divisão realista entre PHP e App Builder

## Configurar o cenário na loja

A conta de demonstração tem **[!UICONTROL Store Credit]** e você pode ver esse saldo na finalização. Adicione produtos até que o pedido total seja de aproximadamente US$ 80. Esse tamanho lhe dá espaço para mostrar tanto o caminho de aceitação bem sucedido e um caminho de declínio, semelhante a um declínio de cartão, sem a matemática lutando contra você.

**[!UICONTROL Split payment]** é oferecido apenas a clientes conectados, pois a sessão deve expor crédito de loja. O check-out de convidado não mostra a opção de divisão.

1. Na etapa **[!UICONTROL Payment]**, escolha o método cash (a demonstração renomeia **[!UICONTROL Cash on delivery]** como **Just Cash**).
1. Uma área de pagamento dividido é exibida sob o método de pagamento. O campo de caixa é preenchido previamente no total do pedido, e o componente lê **[!UICONTROL Store Credit]** da sessão.
1. Para um carrinho de ~$80, defina o dinheiro de **$50** e o crédito da loja de **$30**, de modo que o componente mostre $50 + $30 = $80.
1. Quando os valores forem válidos, faça o pedido.

A interface do usuário dispara uma chamada para uma nova API REST **[!UICONTROL Commerce]** para a divisão. A finalização permanece síncrona: o Commerce aplica crédito de loja, armazena linhas divididas no pedido e emite um evento de E/S que o App Builder consome posteriormente. A página de sucesso é imediata para o cliente.

## Revisar o pedido no administrador do Commerce

Em **[!UICONTROL Sales]** > **[!UICONTROL Orders]**, abra o novo pedido. A área **[!UICONTROL Payment information]** mostra a divisão, por exemplo, **$50** em dinheiro e **$30** crédito de loja. O status é **Pendente** quando o caixa ainda não foi coletado; o crédito de armazenamento já foi obtido quando o pedido foi criado.

**[!UICONTROL Comments]** pode incluir texto adicionado pelo App Builder. O **[!UICONTROL Payment orchestrator action]** no App Builder recebeu o evento de E/S, verificou os valores divididos e usou REST autenticado para anexar comentários. **[!UICONTROL Commerce]** trata isso como qualquer outra chamada REST e não precisa conhecer o gravador.

## Use o painel do operador do App Builder (ERP ou back office)

Uma experiência simples do HTML é executada como uma ação da Web **[!UICONTROL App Builder]** (não há **[!UICONTROL Admin]** para esta exibição). O painel chama a API REST **[!UICONTROL Commerce Order]** e filtra como **Pendente** para que você possa encontrar o trecho de pagamento à vista de $50.

Normalmente, você integra esse padrão a uma ferramenta de ERP ou fraude. São demonstradas duas ações:

* **Aceitar** — Confirma que o dinheiro foi recebido (em produção, geralmente uma postagem automática de uma caixa registradora ou sistema de armazenamento).
* **Rejeitar** — Simula uma fraude ou uma etapa de coleta com falha (em produção, geralmente automatizada a partir do seu serviço de riscos).

**Aceitar e concluir o pedido**

1. No aplicativo **[!UICONTROL App Builder]**, use **Aceitar** para confirmar o pagamento à vista.
1. O aplicativo chama um novo ponto de extremidade **[!UICONTROL Commerce]** que finaliza a linha de caixa. O fluxo principal de pedidos (faturamento e, nesta compilação, uma remessa automatizada) é executado com comportamento **[!UICONTROL Commerce]** nativo. Nenhum desse caminho requer um humano em **[!UICONTROL Admin]**; a orquestração e o ponto de extremidade vivem no App Builder.

Atualizar a mesma ordem em **[!UICONTROL Admin]**: o status muda para **Concluído** quando o pagamento à vista é aceito, com fatura e, onde o produto for entregável, uma remessa para encurtar o ciclo de vida completo na demonstração.

**Recusar e cancelar**

1. Abra uma ordem pré-criada que ainda esteja em cenário de declínio.
1. No aplicativo **[!UICONTROL App Builder]**, use **Recusar** para simular uma falha de fraude ou coleta.
1. Em **[!UICONTROL Admin]**, a ordem é **Cancelada**. O histórico mostra um status de caixa recusado, comentários explicam o resultado, o comprador não foi cobrado na linha de crédito da loja como se fosse uma venda final e a fatura de crédito da loja é anulada com o cancelamento. Um sistema de produção também notificaria o cliente e liberaria quaisquer retenções no inventário ou serviço.

## Limite total do pedido (validação antes da criação do pedido)

A configuração do App Builder ou do **[!UICONTROL Commerce]** pode oferecer suporte a regras de validação; essa compilação bloqueia pedidos acima de **$100** no valor do carrinho (um limite de demonstração que você pode alterar). Uma verificação de valor não é a regra de negócios mais comum — as verificações de inventário ou disponibilidade são mais típicas — mas mostra que a validação pode ser executada em **[!UICONTROL Payment]** em **[!UICONTROL Commerce]** antes da criação de um pedido, enquanto a App Builder ainda lida com a automação de acompanhamento.

1. Adicione produtos até que o total esteja acima de **$100**.
1. A divisão **[!UICONTROL UI]** ainda aparece; o resultado de limite excedido só aparece em **Colocar ordem**.
1. O comprador vê um erro genérico, como **Não foi possível processar o pagamento. Tente novamente ou contate o suporte.**
1. O **[!UICONTROL cart]** permanece inalterado e, portanto, o cliente pode diminuir o total, escolher outro método ou entrar em contato com o suporte.

Uma pontuação de risco, regra de região ou similar pode ser conectada aqui; **[!UICONTROL Commerce]** bloqueia o pedido, e **[!UICONTROL App Builder]** pode receber notificações e trabalhar com casos depois do fato.

## Commerce local, Commerce na nuvem e **Adobe Commerce as a Cloud Service**

A apresentação corresponde **[!UICONTROL Adobe Commerce]** em uma infraestrutura que você gerencia ou **[!UICONTROL Commerce in the cloud]** (PaaS) com uma loja tradicional. Para o **[!UICONTROL Adobe Commerce as a Cloud service]** (SaaS) com um front-end diferente e nenhum módulo em andamento nessa forma, as partes do App Builder são praticamente as mesmas, enquanto a loja e o trabalho de extensão seriam diferentes. Em todos os casos, o mesmo princípio é válido: deixe **[!UICONTROL Commerce]** fazer o que deve acontecer dentro da solicitação **[!UICONTROL Commerce]**, e use **[!UICONTROL App Builder]** para o resto da experiência.

## Recursos adicionais

* [Criar uma POC de pagamento dividido: Ferramentas de IA e App Builder](create-a-split-payment-poc-app-builder-and-ai-tools.md) — a introdução da série às metas e à arquitetura.
