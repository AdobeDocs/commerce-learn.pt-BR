---
title: Conectar e executar consultas no banco de dados do Adobe Commerce
description: Saiba como se conectar ao Adobe Commerce na nuvem, criar um despejo de banco de dados limpo e executar consultas SQL usando a CLI da nuvem, uma GUI ou conexões diretas.
feature: Backend Development,Console,Cloud
topic: Commerce,Development
role: Developer
level: Intermediate, Experienced
doc-type: Technical Video
duration: 581
last-substantial-update: 2024-06-25
jira: KT-14910
exl-id: e740bbd0-5ec7-4272-89cb-0bed776eb149
TQID: https://experienceleague.adobe.com/9jR79l0ERhs4UsQ9da2juigSktpcVE5IsiBnk83gCzc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: add3e29f8841ca4ca99f4c40afc656f00e93ec36
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 0%

---

# Conectar e executar consultas no banco de dados do Adobe Commerce

Saiba como se conectar a um projeto do Adobe Commerce na nuvem, criar um despejo de banco de dados para uso externo e mascarar ou remover informações de identificação pessoal (PII). Acesse dados com um despejo local, uma GUI como MySQL Workbench ou TablePlus, ou a CLI `magento-cloud`.

## Conteúdo de vídeo

* Conecte-se a um projeto remoto da Adobe Commerce Cloud com uma ferramenta de gerenciamento de banco de dados, como MySQL Workbench ou TablePlus.
* Conecte-se ao projeto e execute o SQL a partir da linha de comando.

>[!VIDEO](https://video.tv.adobe.com/v/3430507?learn=on)

Você pode acessar os dados do Adobe Commerce do seu projeto na nuvem usando um dos seguintes métodos:

* Usar um despejo de BD local.
* Abra uma conexão DB com seu ambiente de nuvem remoto com um aplicativo, como o MySQL Workbench ou o TablePlus.
* Conecte-se diretamente ao ambiente de nuvem com a CLI do `magento-cloud` e execute comandos no servidor remoto.

Prefira um dump de banco de dados que você depurar para remover as informações do cliente. Remova os dados do cliente totalmente quando não precisar deles.

## Uso da ferramenta da CLI da Adobe Commerce Cloud

Você precisa da [CLI da Adobe Commerce Cloud](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) instalada para criar um despejo de banco de dados. No computador local, abra um diretório e execute o comando a seguir. Substitua `your-project-id` pela ID do seu projeto (similar a `asasdasd45q`). Substitua `your-environment-name` pelo nome do ambiente, como `master` ou `staging`.

`magento-cloud db:dump -p your-project-id -e your-environment-name`

Se não tiver certeza da ID do projeto ou do ambiente, você pode omiti-los no comando:

`magento-cloud db:dump`

A CLI solicita que você especifique o projeto e o ambiente corretos. O exemplo a seguir exibe essa caixa de diálogo. Este exemplo mostra vários projetos atribuídos à sua conta, mas você provavelmente terá apenas um projeto disponível.

Alterar para um diretório

```bash
cd ~/Downloads/db-tutorial 
```

Agora execute o comando para criar o dump do banco de dados

```bash
magento-cloud db:dump
```

Como você não especificou um projeto ou ambiente, a CLI do Adobe Commerce Cloud faz algumas perguntas. O exemplo a seguir mostra uma caixa de diálogo de exemplo.

```bash
Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Creating SQL dump file: /Users/<username>/Downloads/db-tutorial/abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
```

## Utilização das ferramentas Adobe Commerce ECE

Se você não tiver a ferramenta Adobe Commerce CLI, poderá `ssh` em seu projeto e executar o comando `vendor/bin/ece-tools db-dump` do `ece`:
Exemplo de resposta:

```bash
ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud

 __  __                   _          ___ _             _ 
|  \/  |__ _ __ _ ___ _ _| |_ ___   / __| |___ _  _ __| |
| |\/| / _` / _` / -_) ' \  _/ _ \ | (__| / _ \ || / _` |
|_|  |_\__,_\__, \___|_||_\__\___/  \___|_\___/\_,_\__,_|
            |___/                                        

 Welcome to Magento Cloud.

 This is environment remote-db-ecpefky
 of project abasrpikfw4123.

web@mymagento.0:~$ vendor/bin/ece-tools db-dump
The db-dump operation switches the site to maintenance mode, stops all active cron jobs and consumer queue processes, and disables cron jobs before starting the dump process.
Your site will not receive any traffic until the operation completes.
Do you wish to proceed with this process? (y/N)?y
[2024-02-13T19:01:45.130999+00:00] INFO: Starting backup.
[2024-02-13T19:01:45.155039+00:00] NOTICE: Enabling Maintenance mode
[2024-02-13T19:01:46.404427+00:00] INFO: Trying to kill running cron jobs and consumers processes
[2024-02-13T19:01:46.420149+00:00] INFO: Running Magento cron and consumers processes were not found.
[2024-02-13T19:01:46.420434+00:00] INFO: Waiting for lock on db dump.
[2024-02-13T19:01:46.420499+00:00] INFO: Start creation DB dump for main database...
[2024-02-13T19:01:50.697886+00:00] INFO: Finished DB dump for main database, it can be found here: /app/var/dump-main-1707850906.sql.gz
[2024-02-13T19:01:51.628328+00:00] NOTICE: Maintenance mode is disabled.
[2024-02-13T19:01:51.628419+00:00] INFO: Backup completed.
web@mymagento.0:~$ exit
logout
Connection to ssh.us-4.magento.cloud closed.
```

Use `SFTP` ou `rsync` para extrair o despejo do banco de dados para o ambiente local.

O exemplo a seguir usa `rsync` para enviar o arquivo para a pasta `~/Downloads/db-tutorial`.

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
```

A janela do terminal irá mostrar algumas informações, aqui está um exemplo de saída

```bash
rsync -avrp -e ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud:/app/var/dump-main-1707850906.sql.gz ~/Downloads/db-tutorial
receiving file list ... done
dump-main-1707850906.sql.gz

sent 38 bytes  received 2691041 bytes  358810.53 bytes/sec
total size is 2690241  speedup is 1.00
```

Exiba o conteúdo do arquivo para verificar se ele foi baixado com êxito.

```bash
ls -lah
total 29840
drwxr-xr-x    4 <username>  staff   128B Feb 13 13:02 .
drwx------@ 103 <username>   staff   3.2K Feb 13 12:52 ..
-rw-r--r--    1 <username>   staff    11M Feb 13 12:53 abasrpikfw4123--remote-db-ecpefky--mysql--main--dump.sql
-rw-r--r--    1 <username>   staff   2.6M Feb 13 13:01 dump-main-1707850906.sql.gz
```

Depois de obter os dados, certifique-se de limpá-los removendo ou mascarando os dados do cliente. O exemplo de script a seguir ajudará você a começar.

Esse exemplo transforma os dados do cliente em sequências de caracteres aleatórias, mas mantém todos os itens. Este exemplo contém algumas tabelas extras para demonstrar que as PII do cliente podem ser encontradas em tabelas de terceiros e em tabelas principais. Examine cuidadosamente os dados em cada tabela e máscara ou remova quaisquer dados do cliente.

Normalmente, o arquiteto ou desenvolvedor principal é a única pessoa responsável por mascarar e limpar despejos de banco de dados. Ter um desinfetante dedicado reduz a exposição dos dados brutos, o que reduz a oportunidade de violar as regras e normas de conformidade.

```sql
SET FOREIGN_KEY_CHECKS=0;
UPDATE customer_entity SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE email_contact SET email = REPLACE(email, SUBSTRING(email, LOCATE('@', email) +1), CONCAT(UUID(), '.com'));
UPDATE sales_invoice_grid SET customer_email = 'customer@example.com', customer_name  = 'Jack Smith';
UPDATE sales_order SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Smith', remote_ip = '127.0.0.1';
UPDATE sales_order_address SET region = 'Ohio', postcode = '12345-1234', lastname = 'Smith', street = '123 Main street', region_id = 44, city = 'Phoenix', telephone = NULL, firstname = 'Jane', company = NULL;
UPDATE sales_order_grid SET customer_email = 'customer@example.com', shipping_name = 'Jack', billing_name = 'Jack Smith', billing_address = '123 Main Street', shipping_address = '321 Pine Street', customer_name = 'Jane Smith';
UPDATE sales_shipment_grid SET customer_email = 'customer@example.com', customer_name = 'Jane Smith', billing_address = '123 Main street', billing_name = 'Jack Doe', shipping_name = 'Susie Smith';
UPDATE quote SET customer_email = 'customer@example.com', customer_firstname = 'Sally', customer_lastname = 'Jones', customer_dob = NULL, remote_ip = '127.0.0.1';
UPDATE quote_address SET email = 'customer@example.com', firstname = 'Jack', lastname = 'Smith', company = NULL, street = '123 Main st', city = 'AnyCity', region = 'Some State', region_id = 44, postcode = '12345-1234', telephone = NULL;
UPDATE magento_rma SET customer_custom_email = 'customer@example.com' WHERE customer_custom_email IS NOT NULL;
UPDATE customer_address_entity SET firstname = 'Jack', lastname = 'Smith', telephone = '909-555-1212', postcode = NULL,  region = NULL, street = '123 Main street', city = 'Anycity', company = NULL;
UPDATE customer_grid_flat SET name = 'Jane Doe', email = 'customer@example.com', dob = NULL, gender = NULL, taxvat = NULL, shipping_full = '', billing_full = '', billing_firstname = 'Jack', billing_lastname = 'Smith', billing_telephone = NULL, billing_postcode = NULL, billing_country_id = NULL, billing_region = NULL, billing_street = '123 Main street', billing_city = 'Anycity', billing_fax = NULL, billing_vat_id = NULL, billing_company = NULL;
UPDATE sales_creditmemo_grid SET billing_name = 'Sally', billing_address = '123 Main Street', customer_name = 'Jack Smith', customer_email = 'customer@example.com';
UPDATE magento_rma_grid SET customer_name = 'Jack Smith';
UPDATE newsletter_subscriber SET subscriber_email = 'customer@example.com';
UPDATE core_config_data SET value = '' WHERE path = 'orderexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'productexport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'trackingimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'stockimport/general/serial';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'remarketing/onescript/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/application_id';
UPDATE core_config_data SET value = '' WHERE path = 'algoliasearch_credentials/credentials/search_only_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_account_number';
UPDATE core_config_data SET value = '' WHERE path = 'tax/avatax/production_license_key';
UPDATE core_config_data SET value = '' WHERE path = 'design/head/includes';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/merchant_id';
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/public_key';     
UPDATE core_config_data SET value = '' WHERE path = 'payment/braintree/private_key';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_service_id';
UPDATE core_config_data SET value = '' WHERE path = 'system/full_page_cache/fastly/fastly_api_key';
UPDATE core_config_data SET value = '' WHERE path = 'google/analytics/container_id';  
UPDATE core_config_data SET value = '' WHERE path = 'analytics/general/token';
UPDATE vault_payment_token SET public_hash = UUID(), details = '{"type":"VI","maskedCC":"1111","expirationDate":"01\/2019"}';
TRUNCATE customer_log; 
TRUNCATE customer_visitor; 
TRUNCATE magento_logging_event;
TRUNCATE oauth_consumer;
TRUNCATE oauth_nonce;
TRUNCATE oauth_token;
TRUNCATE password_reset_request_event;
TRUNCATE acknowledgement;
TRUNCATE acknowledgement_report;
TRUNCATE avatax_log;
TRUNCATE avatax_queue;
TRUNCATE cron_schedule;
SET FOREIGN_KEY_CHECKS=1;
```

Como alternativa, você pode excluir os registros em vez de mascarar as informações, o que também torna o novo banco de dados menor. Depois que as PII são mascaradas ou removidas, os dados podem ser fornecidos com segurança a um colega de equipe para uso em seu ambiente local.

## Conexão remota do BD com um projeto da Adobe Commerce Cloud

Esse método permite a edição e a exclusão acidentais de dados em tempo real. Use-o com cuidado. Prefira um backup do banco de dados e uma revisão off-line quando possível. Às vezes, você precisa acessar os dados diretamente na Adobe Commerce Cloud; esse fluxo de trabalho ainda apresenta risco. As GUIs não adicionam prompts de confirmação, portanto, você pode alterar ou remover dados por engano.

Uma conexão de banco de dados remota é conveniente, mas arriscada. Você pode esquecer facilmente que está conectado à produção e excluir ou alterar dados. Você pode se conectar a uma réplica somente leitura, mas SQL pesado ainda afeta o site. A Adobe não recomenda conexões remotas de rotina com bancos de dados graváveis; use as etapas abaixo apenas quando entender os riscos.

Estabeleça um túnel SSH:

```bash
magento-cloud tunnel:open
```

Depois que o projeto é escolhido e o ambiente é escolhido, há saída do comando que é usada nas configurações da interface gráfica mysql.

```bash
magento-cloud tunnel:open

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
SSH tunnel opened to redis at: redis://127.0.0.1:30001
SSH tunnel opened to opensearch at: http://127.0.0.1:30002
SSH tunnel opened to rabbitmq at: amqp://guest:guest@127.0.0.1:30003

Logs are written to: /Users/<user>/.magento-cloud/tunnels.log

List tunnels with: magento-cloud tunnels
View tunnel details with: magento-cloud tunnel:info
Close tunnels with: magento-cloud tunnel:close

Save encoded tunnel details to the MAGENTO_CLOUD_RELATIONSHIPS variable using:
  export MAGENTO_CLOUD_RELATIONSHIPS="$(magento-cloud tunnel:info --encode)"
```

Estabeleça uma conexão usando uma interface gráfica MySQL com a opção de comando `SSH tunnel opened to database at`.

```bash
SSH tunnel opened to database at: mysql://user:@127.0.0.1:30000/main
```

Agora que você tem as informações certas, insira esses valores no Cloud Console.

Você pode encontrar o nome de host SSH e o nome de usuário nas credenciais da nuvem no Cloud Console.

![Adobe Commerce Cloud Console](./assets/cloud-ui-screenshot.png "Adobe Commerce Cloud Console")

Veja um exemplo: `ssh abasrpikfw4123-remote-db-ecpefky--mymagento@ssh.us-4.magento.cloud`
O nome de host SSH é tudo depois do sinal @: `ssh.us-4.magento.cloud` neste exemplo.
O nome de usuário SSH é tudo antes do sinal @: `abasrpikfw4123-remote-db-ecpefky--mymagento`

## Localizando valores para conexão com o banco de dados

Para acessar o banco de dados do MariaDB diretamente, use o SSH para fazer logon no ambiente de nuvem remoto e se conectar ao banco de dados.

1. Use o SSH para fazer logon no ambiente remoto.

   ```bash
   magento-cloud ssh
   ```

2. Recupere as credenciais de logon do MySQL das propriedades `database` e `type` na variável [$MAGENTO_CLOUD_RELATIONSHIPS](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/app/properties/properties#relationships).

   ```bash
   echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
   ```

   ou

   ```bash
   php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
   ```

   Na resposta, localize as informações do MySQL. Por exemplo:

   ```json
   "database" : [
      {
         "password" : "",
         "rel" : "mysql",
         "hostname" : "nnnnnnnn.mysql.service._.magentosite.cloud",
         "service" : "mysql",
         "host" : "database.internal",
         "ip" : "###.###.###.###",
         "port" : 3306,
         "path" : "main",
         "cluster" : "projectid-integration-id",
         "query" : {
            "is_master" : true
         },
         "type" : "mysql:10.3",
         "username" : "user",
         "scheme" : "mysql"
      }
   ],
   ```

Em seguida, use os valores de configuração na interface do MySQL. O exemplo a seguir usa o MySQL Workbench, mas qualquer aplicativo que suporte conexões MySQL terá campos semelhantes.

![Exemplo de conexão do MySQL Workbench](./assets/mysql-workbench-after-connecting.png "Exemplo de conexão do MySQL Workbench")

![Exemplo de conexão do TablePlus](./assets/tablesPlus-db-connection.png "Exemplo de conexão do TablePlus")

Após configurar a conexão, você pode usar uma GUI MySQL para executar consultas em um projeto remoto da Adobe Commerce Cloud.

## Conectando diretamente ao banco de dados do projeto na nuvem para executar o SQL

O método a seguir usa a CLI `magento-cloud` para se conectar diretamente ao banco de dados MySQL e executar o SQL para consultas mais rápidas. Se você precisar de uma cópia deste banco de dados, use um dos métodos alternativos para [criar um despejo de banco de dados](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud).

```bash
magento-cloud db:sql    

Enter a number to choose a project:
  [0] demo-ralbin (ral32nryq4123)
  [1] adobe-commerce-demo (abc123zzkipexnqo)
  [2] DX Tutorials - Commerce (abasrpikfw4123)
 > 2

Enter a number to choose an environment:
Default: master
  [0] master (type: production)
  [1] remote-db (type: development)
 > 1

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 273454
Server version: 10.6.15-MariaDB-1:10.6.15+maria~deb10-log mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

Por exemplo, você pode encontrar todos os registros da tabela `core_config_data` que contêm a palavra `secure` como parte da coluna `path`:

```sql
MariaDB [main]> SELECT * FROM core_config_data WHERE path LIKE '%secure%' \G;
*************************** 1. row ***************************
 config_id: 5
     scope: default
  scope_id: 0
      path: web/unsecure/base_url
     value: http://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 2. row ***************************
 config_id: 6
     scope: default
  scope_id: 0
      path: web/secure/base_url
     value: https://remote-db-ecpefky-abasrpikfw4123.us-4.magentosite.cloud/
updated_at: 2024-02-02 18:03:17
*************************** 3. row ***************************
 config_id: 8
     scope: default
  scope_id: 0
      path: web/secure/use_in_adminhtml
     value: 1
updated_at: 2023-04-26 19:43:58
3 rows in set (0.001 sec)

ERROR: No query specified

MariaDB [main]> 
```

## Recursos adicionais

* [CLI da Adobe Commerce Cloud](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)
* [Configurar o serviço MySQL](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/service/mysql)
* [Configurar uma conexão remota com o banco de dados MySQL](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/prerequisites/database-server/mysql-remote)
* [Criar despejo de banco de dados no Adobe Commerce na infraestrutura em nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/how-to/create-database-dump-on-cloud)
