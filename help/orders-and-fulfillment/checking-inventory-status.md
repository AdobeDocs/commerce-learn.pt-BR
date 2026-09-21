---
title: 'Verificações de status do estoque: desenvolvimento e desempenho'
description: Saiba como avaliar se as verificações de inventário em tempo real são necessárias no Adobe Commerce e analise as considerações de desenvolvimento e desempenho da sua loja.
feature: Best Practices, Inventory
topic: Development, Performance
role: Developer
level: Intermediate, Experienced
doc-type: Tutorial
duration: 496
last-substantial-update: 2024-05-09
jira: KT-15462
exl-id: bd2be562-5738-4398-8afb-2faeb0ba6b83
TQID: https://experienceleague.adobe.com/IfBm4JSpLXViUNTHo7amAL6GIYJsC4O-rdITtbqJV24
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: b01a71b7-d17a-42b2-a9ac-af4b8d9d2ef5
    internal-label: 2FA
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: fcf0f5116ba75bd618f4ed80591ecc96132cdb45
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 0%
---
# O status do estoque verifica as considerações de desenvolvimento e desempenho

A precisão com o inventário é uma consideração importante. Há alguns recursos nativos que podem ajudar a garantir que esse risco seja o mais baixo possível, como pedidos pendentes e definição do limite de estoque. Ambos os tópicos podem ser lidos na [Adobe Experience League](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/configuration/backorders) para obter mais explicações.

Há projetos e casos de uso em que as verificações de status do estoque em tempo real são solicitadas para uma loja da Adobe Commerce. Este tutorial fornece o insight para lidar com essa conversa com considerações de desenvolvimento e desempenho.

## Validar se esta solicitação é necessária

Prepare-se para discutir a solicitação com o máximo de informações possível. A coisa mais importante a fazer é verificar se a funcionalidade nativa não é aceitável para este projeto. Encontre o motivo por trás dessa solicitação para validar que os recursos nativos do Adobe Commerce não atendem a essa solicitação.

Outra consideração é o custo para desenvolver, testar e manter esse recurso. A opinião de uma parte interessada não faz necessariamente de algo um requisito. Há custos associados à validação de inventário fora da funcionalidade principal do Adobe Commerce. Esses custos vêm na forma de débito técnico, mais testes e validação, bem como documentação de uso e documentos de suporte para sua arquitetura.

## Determine o que é uma cadência de atualização de inventário aceitável

Tente considerar as verificações de inventário e como isso é realizado em três abordagens. Cada uma tem vantagens e limitações. Elas também aumentam a complexidade e exigem mais testes e ideias para o tratamento de erros. Lembre-se de que, quando decidir implementar uma solução personalizada, haverá mais responsabilidades e considerações. Os exemplos incluem um processo de fallback, monitoramento, teste e solução de problemas, que pertencem à equipe de desenvolvimento. Alguns bons itens a serem incluídos são nova documentação de suporte, treinamento e monitoramento para garantir que a equipe de desenvolvimento possa dar suporte a todo o recurso. Um efeito colateral é que a equipe de desenvolvimento é proprietária do processo e não aproveita mais a funcionalidade nativa fornecida pelo aplicativo principal do Adobe Commerce. O suporte da Adobe não pode ajudar com esse nível de personalização.

A primeira abordagem é usar a funcionalidade nativa. Usar a funcionalidade nativa é a menor quantidade de risco e tem muitos benefícios. Seguir essa abordagem significa que você pode confiar em toda a documentação e nos tutoriais existentes fornecidos pela Adobe Commerce para o uso do recurso. Há muitos aspectos no gerenciamento de inventário; portanto, use o que vem com o aplicativo como a primeira consideração. No entanto, há casos de uso em que os dados encontrados no comércio no momento do pedido não são precisos. Um exemplo de como os dados não são sincronizados é que as vendas são permitidas fora do aplicativo do Adobe Commerce diretamente no sistema do Order Management. Um motivo é que, para garantir que os níveis precisos de inventário sejam representados no Adobe Commerce, é necessário algum tipo de integração para manter as informações do Adobe Commerce o mais precisas possível. Se a venda em excesso não for aceitável, adicionar um limite de falta de estoque será um bom método para interromper a venda de itens antes que você chegue a zero. A funcionalidade de sincronização nativa do Adobe Commerce é de no máximo 1 vez por dia. Essa frequência é suficiente para alguns casos de uso, no entanto, não é frequente o suficiente para outros. Leia [Importação e exportação agendadas](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-scheduled-import-export) para obter informações detalhadas.

A segunda abordagem é `near real-time`. O tempo quase real ainda usa a funcionalidade nativa. No entanto, isso inclui trabalho extra para fornecer uma integração que alimenta o comércio com frequência para atualizar seu inventário em um cronograma. Por exemplo, a cada hora. Essa opção requer reflexão sobre como uma integração funciona, mas usar a &quot;api em massa&quot; e fazer com que algum middleware faça a transformação dos dados e os envie para o comércio é uma ótima abordagem. Considere usar o Adobe App Builder ou plataformas semelhantes para realizar a maior parte do trabalho e enviar as informações para o Adobe Commerce com mais frequência.

A terceira abordagem e a mais complexa com a maior quantidade de risco e responsabilidade são as verificações de inventário em tempo real em uma API externa ou fonte de dados. Fazer uma verificação de inventário em tempo real para um sistema externo é arriscado e tem vários outros elementos que precisam ser considerados. Veja um pequeno conjunto de outras coisas que precisam ser avaliadas:

* O sistema externo pode aceitar solicitações REST ou GraphQL
* Há limites para o endpoint, como X número de solicitações por minuto que não coincidem com o tráfego do site?
* O que acontece com o tempo de resposta sob carga
* O que acontece quando os tempos de resposta são longos? Você encerra isso automaticamente e usa uma opção de fallback, como o inventário nativo.
* Que tipo de monitoramento está disponível para garantir que as solicitações de API estejam dentro dos limites de tolerância

## Considerações para gerenciamento de inventário não nativo

Mantenha as personalizações o mais não complexas possível.
Quão uniforme pode ser a organização do inventário, é 1 SKU e a quantidade total de estoque disponível OU há outros atributos que precisam ser considerados.

Se as informações de inventário forem razoavelmente planas, por exemplo, um SKU e a quantidade total disponível, as opções de tempo quase real serão expandidas. O conceito de tempo quase real significa que há uma operação em segundo plano que coleta o inventário da origem e preenche um mecanismo de armazenamento a ser usado para responder à solicitação. Para isso, você pode usar coisas como Redis, Mongo ou outros bancos de dados não relacionais. Essas opções são rápidas e funcionam perfeitamente para pares de chave/valor. Se os dados forem um pouco mais complexos, será necessário usar um banco de dados de relação, dentro ou fora do aplicativo de comércio. Ao descarregar isso do banco de dados de comércio, você mantém o aplicativo principal de comércio isolado dessas transações. Outro conjunto de benefícios está salvando a I/O do aplicativo comercial, CPU, RAM e outros do uso. Para salvar recursos dos servidores de aplicativos da Adobe Commerce, aproveite as novas APIs para extrair os dados do armazenamento externo. Esse processo requer um middleware para ajudar a transformar quaisquer dados. Em seguida, verifique se o aplicativo de chamada pode obter o resultado conforme esperado. Ao usar o Adobe App Builder com a malha de API, os dados podem ser transformados e retornados corretamente formatados.

Usar o Adobe App Builder com a malha de API também é uma ótima opção quando há várias fontes de inventário.


## Mover a lógica de execução para fora do processo

A Adobe Developer App Builder fornece uma estrutura unificada de extensibilidade de terceiros para integrar e criar experiências personalizadas para estender as soluções da Adobe. O Adobe Commerce pode usar o Adobe Developer App Builder. Essa abordagem é um excelente caso de uso para estender alguma funcionalidade que normalmente ocorre no aplicativo principal e movê-la para fora do site. A remoção da funcionalidade do aplicativo do Commerce reduz o número de módulos e a complexidade do aplicativo do Commerce. Por sua vez, um número menor de personalizações em andamento reduz a complexidade de atualização e manutenção.

Para obter inspiração sobre como essa tarefa é realizada, a equipe da Adobe criou uma documentação que é uma grande fonte de inspiração e fornece amostras de código de trabalho. Quando um comprador adiciona um produto ao carrinho, um sistema de gerenciamento de estoque de terceiros verifica se o item está em estoque. Em caso afirmativo, permita que o produto seja adicionado. Caso contrário, exiba uma mensagem de erro. Para obter amostras de código e mais informações, vá para [Casos de uso do Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/use-cases/#add-product-to-cart).

## Quando fazer verificações de inventário

Quando verificar se o inventário ainda está disponível é da responsabilidade da parte interessada do negócio, o arquiteto de software com algumas informações de outras partes interessadas principais. Alguns momentos apropriados incluem ao adicionar um item ao carrinho e ao inserir o fluxo de trabalho de check-out. Quaisquer outros eventos adicionam carregamento aos sistemas de backend quando não é necessário. Lembre-se de que o objetivo é capturar um problema de inventário somente quando é fundamental. Considere cuidadosamente outras verificações que afetam a meta geral para verificações de status do inventário e somente as permita se as partes interessadas estiverem cientes do risco potencial de carga extra.

## Pesquisar a origem do inventário

É necessária uma investigação abrangente da origem do inventário externo. Os itens que devem ser avaliados são as opções de API disponíveis, suporte para GraphQL e tempos de resposta esperados. Se a fonte de inventário tiver uma largura de banda de conexão limitada ou nunca tiver sido projetada para ser usada em uma solicitação em tempo real, a capacidade de uso será excluída e o arquiteto precisará considerar o tempo quase real. Se os tempos de solicitação da API excederem os parâmetros definidos, isso exclui a possibilidade de ser uma opção viável. Um exemplo desse comportamento são as respostas da api, que são de 200 ms para solicitações únicas, mas chegam a 500 a 900 ms com carga moderada. Essa situação fica pior com mais carga e impede que chamadas de inventário em tempo real estejam disponíveis.

Certifique-se de testar os tempos de resposta da api com solicitações simples, bem como com um alto volume semelhante ao tráfego esperado no site ativo. Lembre-se de testar todas as áreas do comércio ao mesmo tempo para simular cenários do mundo real. Se ocorrerem chamadas de inventário em tempo real nas páginas do produto, no carrinho e durante a finalização da compra, o teste de carga deverá simular tudo isso simultaneamente para simular o comportamento real do cliente.

## Opções de fallback

Se a origem do inventário estiver inativa e o monitoramento estiver disponível, é recomendado usar o recurso nativo do Adobe Commerce. No entanto, com o monitoramento adequado, a experiência do cliente pode mudar dinamicamente para refletir a perda de verificações de inventário em tempo real. Isso significa que uma venda ou evento é cancelado antecipadamente ou removido da exibição para evitar venda excessiva. Discuta o plano de fallback com o proprietário do armazenamento para que todos entendam o processo automático que ocorre se a origem do inventário ficar inativa.

## Conclusão

A decisão de fazer verificações de inventário em tempo real é significativa. Garantir que o proprietário do site, a equipe de desenvolvimento e outros sejam totalmente instruídos e cientes de todos os ganhos e possíveis armadilhas repousem no líder ou arquiteto do desenvolvedor. Fornecer um plano elaborado que cubra os motivos e um processo de fallback é a chave para o sucesso.

As verificações de inventário em tempo real podem ser realizadas, mas exigem pesquisa e reflexão em torno de testes e validação durante o ciclo de controle de qualidade. Garantir que o teste de carga e os testes automatizados completos ajudem a garantir que todos os possíveis problemas sejam detectados e triados.

Se o monitoramento detectar chamadas com falha ou tempos de resposta lentos, execute ações para manter o site on-line e minimizar a irritação do cliente. As opções de fallback variam desde usar a funcionalidade nativa até desabilitar promoções, notificar a equipe de desenvolvimento ou redirecionar solicitações para um sistema de back-end secundário. A forma como o mecanismo de fallback é implementado deve ser planejada com o mesmo cuidado da integração real, pois todos os sistemas apresentam problemas em algum momento. Qualquer coisa automatizada ou que exija ação manual deve ser claramente documentada.
