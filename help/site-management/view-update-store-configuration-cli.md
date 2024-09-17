---
title: Exibir e definir as configurações do administrador usando a linha de comando
description: Saiba como visualizar e definir configurações do administrador usando a linha de comando.
feature: Configuration,Console,System
topic: Administration,Commerce
role: Developer
level: Beginner
doc-type: Technical Video
duration: 462
last-substantial-update: 2024-01-31T00:00:00Z
jira: KT-14877
exl-id: 6cecba51-8d39-46f5-9864-80126d8ca3da
source-git-commit: d578c066f3e51827694c8bf85aa2324035a8b07b
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Exibir e definir as configurações do administrador usando a linha de comando

Uma demonstração de como visualizar, definir e encontrar valores de configuração com a Commerce CLI. Entenda onde os valores são salvos e também de onde vêm os valores padrão.

## Para quem é este vídeo?

- Desenvolvedores do Adobe Commerce

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3427123?&learn=on)

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

- [Ferramenta de Linha de Comando](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/config-cli.html){target="_blank"}
- [Configurar a segurança do administrador](https://experienceleague.adobe.com/docs/commerce-admin/systems/security/security-admin.html){target="_blank"}
