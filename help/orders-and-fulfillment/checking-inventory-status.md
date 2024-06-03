---
title: O status do estoque verifica as considerações de desenvolvimento e desempenho
description: Saiba mais sobre algumas ideias e considerações para fazer verificações de status do inventário para o Adobe Commerce.
feature: Best Practices, Inventory
topic: Development, Performance
role: Architect, Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-05-09T00:00:00Z
jira: KT-15462
source-git-commit: e171d0a0b6272db5e9ca88992a73395af57072ed
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---


# O status do estoque verifica as considerações de desenvolvimento e desempenho

A precisão com o inventário é uma consideração muito importante. Há alguns recursos nativos que podem ajudar a garantir que esse risco seja o mais baixo possível, como pedidos pendentes e definição do limite de estoque. Ambos os tópicos podem ser lidos em [Experience League](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/backorders) para obter mais explicações.

Há projetos e casos de uso em que as verificações de status do estoque em tempo real são solicitadas para uma loja da Adobe Commerce. Este tutorial fornece informações para lidar com essa conversa com considerações de desenvolvimento e desempenho.

## Validar se esta solicitação é absolutamente necessária

Prepare-se para se envolver com a conversa com o máximo de informações possível. A coisa mais importante a fazer é verificar se a funcionalidade nativa não é aceitável para este projeto. Encontre o motivo por trás dessa solicitação para validar que os recursos nativos do Adobe Commerce não atendem a essa solicitação.

Outra consideração é o custo para desenvolver, testar e manter esse recurso. Só porque algumas partes interessadas acham que é necessário, não significa que seja um requisito. Há custos associados à validação de inventário fora da funcionalidade principal do Adobe Commerce. Esses custos representam dívidas técnicas, mais testes e validações, bem como documentação de uso e documentos de suporte para sua arquitetura.

## Determine o que é uma cadência de atualização de inventário aceitável

Tente considerar as verificações de inventário e como isso é realizado em três abordagens. Cada uma tem vantagens e limitações. Elas também aumentam a complexidade e exigem mais testes e ideias para o tratamento de erros. Lembre-se de quando decidir seguir um roteiro personalizado, haverá mais responsabilidades e considerações. Alguns exemplos incluem um processo de fallback, a equipe de desenvolvimento deve seguir os passos do monitoramento, do teste e da solução de problemas. Alguns bons itens a serem incluídos são nova documentação de suporte, treinamento e monitoramento para garantir que a equipe de desenvolvimento possa dar suporte a todo o recurso. Um efeito colateral adicional é que a equipe de desenvolvimento é totalmente proprietária do processo e não está mais aproveitando a funcionalidade nativa fornecida pelo aplicativo principal do Adobe Commerce. O suporte para Adobe não pode ajudar com esse nível de personalização.

A primeira abordagem é usar a funcionalidade nativa. Usar a funcionalidade nativa é a menor quantidade de risco e tem muitos benefícios. Seguir essa abordagem significa que você pode confiar em toda a documentação e nos tutoriais existentes fornecidos pela Adobe Commerce para o uso do recurso. Há muitos aspectos no gerenciamento de inventário, portanto, o uso do que vem com o aplicativo deve ser a primeira consideração. No entanto, há casos de uso em que os dados encontrados no comércio no momento do pedido podem não ser completamente precisos. Um exemplo de como as coisas podem ficar fora de sincronia é que as vendas são permitidas fora do aplicativo do Adobe Commerce diretamente no sistema de gerenciamento de pedidos. Um motivo é que, para garantir que os níveis precisos de inventário sejam representados no Adobe Commerce, seria necessário algum tipo de integração para manter as informações do Adobe Commerce o mais precisas possível. Se a venda em excesso não for aceitável, adicionar um limite de falta de estoque será um bom método para interromper a venda de itens antes que você chegue a zero. A funcionalidade de sincronização nativa do Adobe Commerce é de no máximo 1 vez por dia. Isso é suficiente para alguns casos de uso, mas pode não ser frequente o suficiente para outros. Leia [Importação e exportação programadas](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) para obter informações mais detalhadas.

A segunda abordagem seria `near real-time`. O tempo quase real ainda usa a funcionalidade nativa. No entanto, isso inclui trabalho extra para fornecer uma integração que alimenta o comércio com frequência para atualizar seu inventário em um cronograma. Por exemplo, a cada hora. Essa opção precisa de reflexão sobre como uma integração pode funcionar, mas usar a &quot;api em massa&quot; e fazer com que algum middleware faça a transformação dos dados e os envie para o comércio é uma ótima abordagem. Considere o uso do Construtor de aplicativos Adobe ou de plataformas semelhantes para realizar a maior parte do trabalho e enviar as informações para a Adobe Commerce com mais frequência.

A terceira abordagem e a mais complexa com a maior quantidade de risco e responsabilidade são as verificações de inventário em tempo real em uma API externa ou fonte de dados. Fazer uma verificação de inventário em tempo real para um sistema externo é arriscado e tem vários outros elementos que precisam ser considerados. Veja um pequeno conjunto de outras coisas que precisam ser avaliadas:

* O sistema externo pode aceitar solicitações REST ou GraphQL
* há limites para o endpoint, como X número de solicitações por minuto que podem não coincidir com o tráfego do site
* O que acontece com o tempo de resposta sob carga
* O que acontece quando os tempos de resposta são longos? Você encerra isso automaticamente e usa uma opção de fallback, como o inventário nativo.
* Que tipo de monitoramento está disponível para garantir que as solicitações de API estejam dentro dos limites de tolerância

## Considerações ao considerar o gerenciamento de inventário não nativo

Mantenha as personalizações o mais não complexas possível.
Quão uniforme pode ser a organização do inventário, é apenas 1 SKU e a quantidade total de estoque disponível OU há outros atributos que precisam ser considerados.

Se as informações de inventário forem razoavelmente planas, por exemplo, um SKU e a quantidade total disponível, as opções de tempo quase real serão expandidas. O conceito de tempo quase real significa que há uma operação em segundo plano que coleta o inventário da origem e preenche um mecanismo de armazenamento a ser usado para responder à solicitação. Para isso, você pode usar coisas como Redis, Mongo ou outros bancos de dados não relacionais. Essas opções são excelentes, pois são muito rápidas e funcionam perfeitamente para pares de chave/valor. Se os dados forem um pouco mais complexos, será necessário usar um banco de dados de relação, dentro ou fora do aplicativo de comércio. Ao descarregar isso do banco de dados de comércio, você mantém o aplicativo principal de comércio isolado dessas transações. Outro conjunto de benefícios está salvando a I/O do aplicativo comercial, CPU, RAM e outros do uso. Em vez de usar os recursos dos servidores de aplicativos da Adobe Commerce, aproveite as novas APIs para extrair os dados do armazenamento externo.  Isso provavelmente precisará de um middleware para ajudar a transformar quaisquer dados. Em seguida, verifique se o aplicativo de chamada pode obter o resultado conforme esperado. Ao usar o Construtor de aplicativos de Adobe com malha de API, os dados podem ser transformados e retornados corretamente formatados.

O uso do Construtor de aplicativos de Adobe com malha de API também é uma ótima opção quando há várias fontes de inventário.


## Mover a lógica de execução para um local fora do processo

O Construtor de aplicativos da Adobe Developer fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar experiências personalizadas para estender soluções de Adobe. A Adobe Commerce pode usar o Construtor de aplicativos da Adobe Developer. Esse seria um excelente caso de uso para estender algumas funcionalidades que normalmente ocorrem no aplicativo principal e movê-las para fora do local. A remoção da funcionalidade do aplicativo do Commerce reduz o número de módulos e a complexidade do aplicativo do Commerce. Por sua vez, um número menor de personalizações em andamento reduz a complexidade de atualização e manutenção.

Para inspiração sobre como isso pode ser feito, a equipe do Adobe criou uma documentação que pode ser uma grande fonte de inspiração e fornecer amostras de código de trabalho. Quando um comprador adiciona um produto ao carrinho, um sistema de gerenciamento de estoque de terceiros verifica se o item está em estoque. Em caso afirmativo, permita que o produto seja adicionado. Caso contrário, exiba uma mensagem de erro.  Para obter amostras de código e mais informações, acesse [Casos de uso do Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Quando fazer verificações de inventário

Quando verificar se o inventário ainda está disponível, a decisão final caberá ao acionista comercial, o arquiteto de software com alguma informação de outros participantes importantes. Alguns momentos apropriados incluem ao adicionar um item ao carrinho e ao inserir o fluxo de trabalho de check-out. Quaisquer outros eventos simplesmente adicionarão carga aos sistemas de backend quando isso não for necessário. Lembre-se de que o objetivo é capturar um problema de inventário somente quando é fundamental. Outras verificações podem ser agradáveis, mas se elas podem afetar a meta geral para verificações de status do estoque, elas devem ser cuidadosamente consideradas e permitidas somente se as partes interessadas da empresa ou outras pessoas estiverem cientes do risco potencial de carga extra nos sistemas de back-end.

## Pesquisar como a origem do estoque

É necessária uma investigação abrangente da origem do inventário externo. Os itens que devem ser avaliados são as opções de API disponíveis, suporte para GraphQL e tempos de resposta esperados. Se a fonte de inventário tiver uma largura de banda de conexão limitada ou nunca tiver sido projetada para ser usada em uma solicitação em tempo real, a capacidade de uso será excluída e o arquiteto precisará considerar o tempo quase real.  Se os tempos de solicitação da API excederem os parâmetros definidos, isso também excluirá que seja uma opção viável.  Um exemplo disso são as respostas de api de 200 MS® para uma solicitação por vez, mas elevam para 500 a 900 MS® com carga moderada.  Isso provavelmente só pioraria com mais carga e impediria que chamadas de inventário em tempo real ficassem disponíveis.

Certifique-se de testar os tempos de resposta da api com solicitações simples, bem como com um alto volume semelhante ao tráfego esperado no site ativo. Lembre-se de testar todas as áreas do comércio ao mesmo tempo para simular cenários do mundo real. Se a expectativa for uma chamada de inventário em tempo real deve ocorrer nas páginas do produto, ao visualizar e editar um carrinho e durante o check-out, o teste de carga precisa simular todos esses itens ao mesmo tempo para simular o comportamento real do cliente e a expectativa de uma loja.

## Opções de fallback

SE a origem do inventário estiver inativa e o monitoramento estiver disponível, é recomendado usar o recurso nativo do Adobe Commerce. No entanto, com o monitoramento adequado, a experiência do cliente pode mudar dinamicamente para refletir a perda de verificações de inventário em tempo real. Isso pode significar que uma venda ou evento é cancelado antecipadamente ou removido da exibição para evitar venda excessiva. A expectativa sobre o que fazer quando a origem do inventário estiver inativa por qualquer motivo precisa ser considerada e discutida com o proprietário da loja para que todos estejam cientes de qualquer processo automático que assuma essa circunstância infeliz.

## Conclusão

A decisão de fazer verificações de inventário em tempo real é significativa. Garantir que o proprietário do site, a equipe de desenvolvimento e outros sejam totalmente instruídos e cientes de todos os ganhos e possíveis armadilhas repousem no líder ou arquiteto do desenvolvedor. Fornecer um plano elaborado que cubra os motivos e um processo de fallback é a chave para o sucesso.

As verificações de inventário em tempo real podem ser realizadas, mas exigem pesquisa e reflexão em torno de testes e validação durante o ciclo de controle de qualidade. Garantir que o teste de carga e os testes automatizados completos ajudem a garantir que todos os possíveis problemas sejam detectados e triados.

Ao considerar quais ações executar se o monitoramento detectar uma tendência de chamadas com falha para o sistema externo ou se os tempos de resposta estiverem acima dos limites aceitáveis, o site permanecerá online e oferecerá a menor quantidade de irritação para os clientes. As opções de fallback podem ser tão simples quanto desativar as verificações do inventário externo e usar a funcionalidade nativa, ou podem ser tão avançadas quanto desativar uma promoção, notificar a equipe de desenvolvimento sobre os problemas de escalonamento ou até mesmo talvez redirecionar solicitações para um segundo ou terceiro sistema de backend, se disponível. A forma como o mecanismo de fallback é exercido deve ser considerada apenas como a implementação real, pois cada integração tem problemas em algum momento. Qualquer coisa automatizada ou que exija ação manual deve ser claramente documentada.
