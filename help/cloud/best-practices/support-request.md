---
title: Criar uma solicitação de suporte efetiva
description: Saiba mais sobre como criar um tíquete de suporte para maximizar a eficiência da solicitação.
feature: Best Practices, Customer Service, Support
topic: Commerce
role: Admin, Developer, User
level: Beginner, Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-08-23T00:00:00Z
jira: KT-15165
source-git-commit: b3ec1230e5efa198d71e1a5c0756a47666065117
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Solicitações de suporte eficazes

Ao criar um tíquete de suporte, é importante enviá-lo por meio dos canais apropriados, fornecer informações precisas e detalhadas sobre o problema, selecionar a organização e o motivo de contato corretos, escolher o produto e a versão apropriados, revisar artigos sugeridos para possíveis soluções, verificar todas as informações antes de enviar, acompanhar o progresso do tíquete e iniciar uma conversa com a equipe de suporte, marcar o tíquete como resolvido quando o problema for resolvido e abrir um tíquete de acompanhamento se for necessária mais assistência. &#x200B; Lembre-se de enviar o tíquete pelos canais apropriados, fornecer informações precisas e detalhadas, selecionar a organização correta e o motivo do contato, escolher o produto e a versão apropriados, revisar os artigos sugeridos, verificar novamente todas as informações antes de enviar, acompanhar o progresso do tíquete, conversar com a equipe de suporte, marcar o tíquete como resolvido quando o problema for resolvido e abrir um tíquete de acompanhamento, se necessário. &#x200B;

## Incluir logs ou capturas de tela

Há vários logs úteis, dependendo do problema em questão. Se possível, encontre uma seção do registro e inclua-a como parte da solicitação de suporte. Esse trecho do registro ajuda os engenheiros a entender os erros exibidos e agilizará o processo de triagem. Lembre-se de que cada servidor de aplicativos tem logs individuais, que são alimentados no New Relic como um agregado.  Isso significa que você pode pesquisar todos os erros em um local, em vez de ler os arquivos de log individuais de cada servidor de aplicativos. Como opção final, se houver uma entrada encontrada no New Relic, uma captura de tela também poderá ser usada como informação adicional e ajudar a acelerar o processo, mas é preferível ter uma instrução NRQL.

## Verifique se o fuso horário é referenciado

Garantir que, quando as pessoas contribuírem para um problema de suporte, lembrem-nas de esclarecer seu fuso horário ao se referirem a um incidente. A referência a um fuso horário garante que, quando a equipe de engenharia de suporte estiver pesquisando os logs e eventos, seja possível se concentrar nos intervalos de tempo que são realmente relevantes. Lembre-se de que alguém pode estar muitas horas à frente ou atrás dos tempos de registro do servidor.

## Descrever a triagem inicial realizada e as descobertas

Discutindo e documentando todas as etapas de triagem realizadas até o momento, os engenheiros de suporte validam as suposições iniciais. Se as etapas de triagem e os resultados de suporte forem fornecidos, o processo geral poderá ser agilizado. Isso também ajudará a reduzir a duplicação de esforços e, eventualmente, fornecerá uma maneira de documentar as descobertas com um nível de validação.

## Links para relatórios do New Relic ou fornecem instrução NRQL

Vários problemas do Adobe Commerce podem ser rastreados por meio do New Relic. Ao observar os painéis do New Relic ou as instruções NRQL personalizadas, você obtém informações sobre a origem de alguns problemas. Esses mesmos painéis e consultas personalizadas do New Relic são compartilháveis. Ao fornecer esses links no tíquete de suporte, os engenheiros podem ver exatamente o que é o repórter.

>[!MORELIKETHIS]
> 
> - [Guia do Usuário da Ajuda do Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"}
