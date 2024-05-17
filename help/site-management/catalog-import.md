---
title: Saiba mais sobre as opções de importação de catálogo que vêm nativas com o Adobe Commerce
description: Saiba mais sobre algumas das opções nativas para importar seu catálogo para a loja da Adobe Commerce.
kt: 13634
doc-type: tutorial
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
exl-id: 18713a44-df39-4b94-91ce-c7efeb4ce2b3
source-git-commit: b0fe49352b00a68554e662327cd66983c30d8285
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Opções de importação de um catálogo

Existem alguns métodos nativos para importar um catálogo para o Adobe Commerce. Cada método tem seu próprio raciocínio para uso, juntamente com prós e contras que devem ser considerados.

Escolha uma das opções abaixo para saber mais.

>[!BEGINTABS]

>[!TAB Manual]

## Criação manual dos produtos {#manual-import}

Se você tiver um catálogo limitado e as atualizações forem pouco frequentes, criá-las manualmente pode ser a melhor opção. É necessário tempo para entrar em cada produto e algum treinamento limitado sobre como usar o administrador do Commerce. O gerenciamento manual de catálogos não é a opção correta para a maioria das lojas, mas, em determinadas situações, pode fazer sentido. Para ver a documentação adicional para esse processo, visite [Criar um produto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html){target="_blank"}. Não se esqueça: você pode usar mais de um método para gerenciar o catálogo. No entanto, uma vez que a automação for usada, as edições manuais deverão ser limitadas. As atualizações automatizadas têm a oportunidade de substituir qualquer alteração executada manualmente e, portanto, causar confusão. Quando a integração com o Adobe Commerce para gerenciar o catálogo estiver usando automação e APIs, é recomendável restringir o gerenciamento do catálogo do administrador até [funções e permissões do usuário](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html){target="_blank"}.

### Quando considerar esta abordagem

- Catálogo muito pequeno, por exemplo, menos de 50 produtos
- Atualizações pouco frequentes
- Você tem todos os detalhes do produto, imagens, vídeos e não quer dedicar tempo para saber como converter os dados em CSV
- Você deseja incluir a adição de imagens e vídeos ao criar os produtos
- Sua equipe está `not` familiarizado com APIs e como o OAUTH funciona

>[!TAB CSV de administrador]

## Ferramenta de importação de CSV do administrador {#admin-csv}

Essa ferramenta permite que o proprietário de uma loja importe um catálogo usando um direito CSV do administrador de comércio.
[Importar dados do administrador do Commerce](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}

Vantagens: fazer upload de um CSV do administrador é uma abordagem direta para o gerenciamento de catálogos. Ele permite atualizações mais rápidas de produtos de catálogo para um catálogo de tamanho moderado.

Desvantagens:

- Lento
- O tamanho máximo do arquivo para upload está definido no servidor e pode não ser facilmente ajustado pelo proprietário da loja.
- Requer acesso de administrador e alguém para executar a ação, a automação é limitada
- As importações programadas são limitadas a no máximo 1x por dia
- As imagens e os vídeos associados devem ser carregados separadamente

### Quando considerar esta abordagem

- O tamanho do catálogo é moderado
- As atualizações não são feitas mais de uma vez ao dia
- você tem acesso às configurações do servidor caso precise aumentar o tamanho máximo de upload de arquivo
- Sua equipe está `not` familiarizado com APIs e como o OAUTH funciona

>[!TAB API REST em massa]

## API REST em massa {#bulk-rest-api}

A API REST em massa permite automação e atualizações mais frequentes. Essa API é mais rápida do que usar o upload de administrador do CSV.
[Documentação de pontos de extremidade em massa](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Vantagens: a capacidade de importar grandes conjuntos de dados que não estejam no formato CSV.

Desvantagens:

- As imagens e os vídeos associados devem ser carregados separadamente
- Pode ser limitado por restrições de largura de banda no provedor de hospedagem

### Quando considerar esta abordagem

- Catálogo de qualquer tamanho
- As atualizações são frequentes; mais de 1x por dia é aceitável
- O tempo de importação é importante, mas não é crítico, e um pequeno atraso no processamento dos dados de importação é aceitável
- Os dados não são estruturados em formato CSV e você não é capaz de transformá-los usando automação

>[!TAB API REST ASSÍNCRONA]

## API REST ASSÍNCRONA {#async-rest-api}

Um ponto de extremidade da Web assíncrono intercepta mensagens em uma API da Web e as grava na fila de mensagens. Cada vez que o sistema aceita essa solicitação de API, ele gera um identificador UUID. O Adobe Commerce inclui essa UUID quando adiciona a mensagem à fila. Em seguida, um consumidor lê as mensagens da fila e as executa uma a uma.
[Documentação de endpoints assíncronos da Web](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Vantagens:

- Importação de dados rápida
- O escopo de armazenamento é compatível ou você pode especificar `all` para executar a operação em todos os armazenamentos existentes

Desvantagens:

- Não há suporte para solicitações GET

### Quando considerar esta abordagem

- As importações são frequentes
- Nenhum problema com um pequeno atraso a partir do momento em que são enviadas por meio da API e processadas a partir da fila de mensagens.


>[!TAB API REST CSV]

## API REST CSV {#csv-rest-api}

Essa opção de API permite importações extremamente rápidas em comparação a todas as outras opções nativas.

[Importar API CSV REST de dados](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Vantagens:

- Método mais rápido para processar os dados recebidos
- Pode ser executado várias vezes ao dia
- Os dados podem ser compactados usando gzip em solicitações grandes para evitar limites de tamanho de solicitação HTTP.

Desvantagens:

- As imagens e os vídeos associados devem ser carregados separadamente
- Os dados precisam estar em um formato CSV

### Quando considerar esta abordagem

- Catálogo de qualquer tamanho
- As atualizações são frequentes; mais de 1x por dia é aceitável
- O tempo geral para importar é importante
- Os dados já estão no formato CSV ou podem ser facilmente transformados com a automação

>[!ENDTABS]

## Recursos adicionais

- [Importar dados usando o novo CSV REST](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
- [Importar documentação principal de dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}
- [Notas de versão do Adobe Commerce versão 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html){target="_blank"}
- [Usuários, funções e permissões](../site-management/users-roles-permissions.md){target="_blank"}
