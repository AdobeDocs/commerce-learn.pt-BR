---
title: Learn about catalog import options that come native with Adobe Commerce
description: Learn how a few of the native options for importing your catalog to your Adobe Commerce store.
kt: 13634
doc-type: tutorial
duration: 211
audience: all
activity: use
last-substantial-update: 2023-8-15
feature: Backend Development, Data Import/Export, REST
topic: Commerce, Administration, Content Management
role: Admin, User
level: Beginner, Intermediate
exl-id: 18713a44-df39-4b94-91ce-c7efeb4ce2b3
TQID: https://experienceleague.adobe.com/-JG7blrxImSXjA2DP9soZfsicISW0hkP2zJeWdMpVBU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 898
ht-degree: 0%

---

# Options for importing a catalog

There are a few native methods for importing a catalog into Adobe Commerce. Each method has its own reasoning for usage along with pros and cons that must be considered.

Choose from one of the options below to learn more.

>[!BEGINTABS]

>[!TAB Manual]

## Creating the products manually {#manual-import}

If you have a limited catalog and updates are infrequent, creating them manually might be the best option. It requires time to enter each product and some limited training to how to use the Commerce Admin. Manual catalog management is not the right option for most stores, but in certain situations, it may make sense. To see additional documentation for this process, visit [Create a product](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html){target="_blank"}. Do not forget, you can use more than one method to manage your catalog, however once automation is used, manual edits must be limited. Automated updates have the opportunity to overwrite any changes performed manually, and therefore cause confusion. Once the integration with Adobe Commerce to manage the catalog is using automation and APIs, it is advised to restrict management of the catalog from the admin through [user roles and permissions](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html){target="_blank"}.

### When to consider this approach

* Very small catalog, for example fewer than 50 products
* Updates are infrequent
* You have all the product details, images, videos, and you do not want to take the time to learn how to convert the data to CSV
* You want to include adding images and videos when creating the products
* Your team is `not` familiar with APIs and how OAUTH works

>[!TAB Admin CSV]

## Admin CSV import tool {#admin-csv}

This tool allows a store owner to import a catalog using a CSV right from the commerce admin.
[Import Data from Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}

Pros:
Uploading a CSV from the admin is a straight forward approach to catalog management. It allows for faster catalog product updates to a moderately sized catalog.

Cons:

* Slow
* Maximum upload file sized defined on server and may not be easily adjusted by a store owner.
* Requires admin access and someone to perform the action, automation is limited
* Schedule imports are limited to 1x a day max
* The images and videos associated must be uploaded separately

### When to consider this approach

* Catalog size is moderate
* Updates are not more than once a day
* you have some access to server configurations in case that you must increase max file upload size
* Your team is `not` familiar with APIs and how OAUTH works

>[!TAB Bulk REST API]

## Bulk REST API {#bulk-rest-api}

The bulk REST API allows for automation and more frequent updates. This API is faster than using the admin upload of CSV.
[Bulk endpoints documentation](https://developer.adobe.com/commerce/webapi/rest/use-rest/bulk-endpoints/){target="_blank"}

Vantagens:
A capacidade de importar grandes conjuntos de dados que não estejam no formato CSV.

Desvantagens:

* As imagens e os vídeos associados devem ser carregados separadamente
* Pode ser limitado por restrições de largura de banda no provedor de hospedagem

### Quando considerar esta abordagem

* Catálogo de qualquer tamanho
* As atualizações são frequentes; mais de 1x por dia é aceitável
* O tempo de importação é importante, mas não é crítico, e um pequeno atraso no processamento dos dados de importação é aceitável
* Os dados não são estruturados em formato CSV e você não é capaz de transformá-los usando automação

>[!TAB API REST ASSÍNCRONA]

## API REST ASSÍNCRONA {#async-rest-api}

Um ponto de extremidade da Web assíncrono intercepta mensagens em uma API da Web e as grava na fila de mensagens. Cada vez que o sistema aceita essa solicitação de API, ele gera um identificador UUID. O Adobe Commerce inclui essa UUID quando adiciona a mensagem à fila. Em seguida, um consumidor lê as mensagens da fila e as executa uma a uma.
[Documentação assíncrona de pontos de extremidade da Web](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/){target="_blank"}

Vantagens:

* Importação de dados rápida
* O escopo de armazenamento é suportado ou você pode especificar `all` para executar a operação em todos os armazenamentos existentes

Desvantagens:

* Não há suporte para solicitações GET

### Quando considerar esta abordagem

* As importações são frequentes
* Nenhum problema com um pequeno atraso a partir do momento em que são enviadas por meio da API e processadas a partir da fila de mensagens.


>[!TAB API REST CSV]

## API REST CSV {#csv-rest-api}

Essa opção de API permite importações extremamente rápidas em comparação a todas as outras opções nativas.

[Importar API CSV de dados REST](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
Vantagens:

* Método mais rápido para processar os dados recebidos
* Pode ser executado várias vezes ao dia
* Os dados podem ser compactados usando gzip em solicitações grandes para evitar limites de tamanho de solicitação HTTP.

Desvantagens:

* As imagens e os vídeos associados devem ser carregados separadamente
* Os dados precisam estar em um formato CSV

### Quando considerar esta abordagem

* Catálogo de qualquer tamanho
* As atualizações são frequentes; mais de 1x por dia é aceitável
* O tempo geral para importar é importante
* Os dados já estão no formato CSV ou podem ser facilmente transformados com a automação

>[!ENDTABS]

## Recursos adicionais

* [Importar dados usando o novo CSV REST](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}
* [Importar documentação principal de dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/import/data-import.html){target="_blank"}
* [Notas de versão do Adobe Commerce versão 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/adobe-commerce/2-4-6.html){target="_blank"}
* [Usuários, funções e permissões](../site-management/users-roles-permissions.md){target="_blank"}
