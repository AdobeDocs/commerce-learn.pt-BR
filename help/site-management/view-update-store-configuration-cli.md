---
title: Exibir e definir as configurações do administrador usando a linha de comando
description: Saiba como visualizar e definir configurações do administrador usando a linha de comando.
feature: Configuration,Console,System
topic: Administration,Commerce
role: Developer
level: Beginner
doc-type: Technical Video
duration: 510
last-substantial-update: 2024-01-31T00:00:00.000Z
jira: KT-14877
exl-id: 6cecba51-8d39-46f5-9864-80126d8ca3da
TQID: https://experienceleague.adobe.com/W0kaFd-DJAPA1kFO0hWaBZXsSarojbt5Hnv3QkW85hA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 168
ht-degree: 0%

---

# Exibir e definir as configurações do administrador usando a linha de comando

Uma demonstração de como visualizar, definir e encontrar valores de configuração com a Commerce CLI. Entenda onde os valores são salvos e também de onde vêm os valores padrão.

## Para quem é este vídeo?

* Desenvolvedores do Adobe Commerce

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3439975?captions=por_br&learn=on)

## Alguns comandos usados no tutorial

Altere a configuração de segurança de senha para recomendado:

`$ php bin/magento config:set admin/security/password_is_forced 0`

Mostrar o endereço de email para a funcionalidade de cópia automática de ordem de venda

`$ php bin/magento config:show sales_email/order/copy_to`

Mostrar o resultado vazio de uma configuração que tenha um valor no administrador

`php bin/magento config:show trans_email/ident_sales/email`

## Consultas Mysql usadas no tutorial

```
SELECT * FROM core_config_data WHERE path = 'sales_email/order/copy_to';

SELECT * FROM core_config_data WHERE path = 'sales_email/order_comment/copy_to';

SELECT * FROM core_config_data WHERE path = 'trans_email/ident_sales/email';
```

## Onde encontrar o email de vendas padrão

Como encontrar o valor de configuração definido em algum lugar na base de código?
`grep -rnw vendor/magento/ -e 'sales@example.com'`

Para exibir uma página no terminal e mostrar os números de linha `cat -n vendor/magento/module-email/etc/config.xml`

## Recursos adicionais

* [Ferramenta de linha de comando](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html?lang=pt-BR){target="_blank"}
* [Configurar a segurança do administrador](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html?lang=pt-BR){target="_blank"}
