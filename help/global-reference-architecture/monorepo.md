---
title: Global Reference Architecture Monorepo
description: Learn how to use the monorepo approach for global reference architecture to establish a scalable and resilient commerce experience
jira: KT-16728
doc-type: tutorial
duration: 441
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Experienced
exl-id: ebdc13cf-c452-4728-af00-c3ea1149c2fa
TQID: https://experienceleague.adobe.com/22ayPTG7ZgpcWr5l53Ide2sZeGTN-9P0jept0ZQ6njQ
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 1418
ht-degree: 0%

---

# Monorepo Global Reference Architecture pattern

{{only-for-on-prem-commerce-cloud}}

This guide explains how to set up Adobe Commerce with the Monorepo Global Reference Architecture (GRA) Pattern.

The Monorepo GRA pattern involves a single Git repository to host all common customizations. This single Git repository is exposed through Composer as a separate composer packages.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA monorepo](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

* Ideal for functional testing
* Reutilização de código por meio de repositórios de código compartilhados
* Flexibilidade total na instalação de pacotes, cada pacote de GRA pode ser atualizado, rebaixado ou ter backport individualmente
* Suporte completo para controle de versão semântico
* Não é necessária nenhuma ferramenta especial, infraestrutura complexa ou estratégia especial de ramificação
* Suporte para todos os tipos de encapsulamento que o Composer suporta
* Ideal for ephemeral environments, which are optional, but for high volume delivery teams they are very useful

Desvantagens:

* Possível implantar combinações de pacotes que não foram desenvolvidos na mesma configuração; necessidade de procedimentos de teste rigorosos
* The monorepo GRA pattern can be complex at the start. Assign a lead that helps the team work with the system

## Configurar o Adobe Commerce com o padrão GRA de pacotes separados

### A estrutura de diretório

The final directory structure of a full Adobe Commerce installation with the Separate Packages GRA pattern has this directory structure:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── packages/
│   └── ...
├── composer.json
└── composer.lock
```

A production Git repository has this directory structucture:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

The difference is that the production instances install from Composer, where the monorepo holds its own copy of every package inside the packages directory.

### Prepare a production repository

Crie um repositório para a primeira instância do Adobe Commerce, que representa uma loja da Web para a Marca X.

```bash
mkdir gra-monorepo-brand-x
cd gra-monorepo-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Instale o Adobe Commerce com `bin/magento setup:install`. Commit the resulting `app/etc/config.php` and the composer files. Composer manages anything else so nothing else should be in Git.

### Prepare the monorepo repository

The monorepo repository starts with the same steps.

```bash
mkdir gra-monorepo 
cd gra-monorepo
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
```

Install Adobe Commerce with `bin/magento setup:install`, commit and push.

```bash
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo.git 
git add composer.json composer.lock app/etc/config.php
git commit -m 'initialize monorepo GRA development repository'
git push -u origin main
```

### Prepare for monorepo development

For monorepo development, make the following changes to your composer.json file:

1. Change the name and description of the package so that it is clear that this package is your monorepo package.
1. Delete the version attribute from composer.json, because the version is managed using Git tags for this repository.
1. Replace the require section with a meta package which is created later.
1. Change minimum stability to dev.
1. Add a path type repository that points to `packages/*/*` to host monorepo packages, including branch aliases for each package it contains
1. Add a branch alias for the project itself

The following Git diff shows the difference between a clean Adobe Commerce install and the changes mentioned above:

```diff
@@ -1,6 +1,6 @@
 {
-    "name": "magento/project-enterprise-edition",
-    "description": "eCommerce Platform for Growth (Enterprise Edition)",
+    "name": "antonevers/gra-monorepo",
+    "description": "Monorepo repository for Global Reference Architecture development",
     "type": "project",
     "license": [
         "proprietary"
@@ -15,11 +15,8 @@
         "preferred-install": "dist",
         "sort-packages": true
     },
-    "version": "2.4.7-p3",
     "require": {
-        "magento/product-enterprise-edition": "2.4.7-p3",
-        "magento/composer-dependency-version-audit-plugin": "~0.1",
-        "magento/composer-root-update-plugin": "^2.0.4"
+        "antonevers/gra-meta-brand-x": "self.version"
     },
     "autoload": {
         "exclude-from-classmap": [
@@ -69,16 +66,33 @@
             "Magento\\Tools\\Sanity\\": "dev/build/publication/sanity/Magento/Tools/Sanity/"
         }
     },
-    "minimum-stability": "stable",
+    "minimum-stability": "dev",
     "prefer-stable": true,
     "repositories": [
         {
+            "type": "path",
+            "url": "packages/*/*",
+            "options": {
+                "versions": {
+                    "antonevers/gra-meta-brand-x": "1.4.x-dev",
+                    "antonevers/gra-meta-foundation": "1.4.x-dev",
+                    "antonevers/gra-component-foundation": "1.4.x-dev",
+                    "antonevers/module-gra": "1.4.x-dev",
+                    "antonevers/module-3rdparty": "1.4.x-dev",
+                    "antonevers/module-local": "1.4.x-dev"
+                }
+            }
+        },
+        {
             "type": "composer",
             "url": "https://repo.magento.com/"
         }
     ],
     "extra": {
-        "magento-force": "override"
+        "magento-force": "override",
+        "branch-alias": {
+            "dev-main": "1.4.x-dev"
+        }
     }
 }
```

### Usar metapackages

Baixe o código de exemplo de [AntonEvers/gra-meta-foundation](https://github.com/AntonEvers/gra-meta-foundation) no GitHub para obter os metapackages e os módulos de amostra usados neste exemplo.

Os metapackages de compositor agrupam vários pacotes de compositor em um único pacote. Quando um metapackage é necessário, todos os pacotes que ele agrupa são instalados automaticamente por meio da seção Composer require do metapackage.

Neste exemplo, há dois metapackages:

1. **antonevers/gra-meta-brand-x**: um metapackage que contém tudo o que compõe &quot;Marca X&quot;
1. **antonevers/gra-meta-foundation**: um metapackage que contém tudo o que está sempre instalado em qualquer marca

O metapackage da marca requer o metapackage de base. Quando o metapackage da marca é necessário, o metapackage de base também é necessário automaticamente. Consulte os dois arquivos composer.json dos metapackages para ver como eles se relacionam:

antonevers/gra-meta-brand-x:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-meta-foundation": "^1.4",
        "antonevers/module-local": "^1.4"
    }
}
```

antonevers/gra-meta-foundation:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {
        "antonevers/gra-component-foundation": "^1.4",
        "antonevers/module-gra": "^1.4",
        "antonevers/module-3rdparty": "^1.4",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "^2.0.4",
        "magento/product-enterprise-edition": "2.4.7-p3"
    }
}
```

Os metapackages são uma boa maneira de organizar o código que pertence a nós. Use metapackages para definir grupos de pacotes que sejam regionais, globais, específicos da marca ou qualquer agrupamento que faça sentido para você. Se você mantiver várias instalações do Adobe Commerce, o empacotamento será uma maneira segura e versátil de definir o contexto em que um pacote é esperado.

Existem metapackages no monorepo dentro do diretório `packages`. Lá, a estrutura de diretório de `vendor` é espelhada:

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       │   └── composer.json
│       └── gra-meta-foundation
│           └── composer.json
├── composer.json
└── composer.lock
```

### Adicionar e desenvolver módulos

Existem módulos no monorepo no diretório `packages`. Dessa forma, o Composer pode encontrá-los no repositório de tipo de caminho.

Baixe o código de exemplo de [AntonEvers/gra-meta-foundation](https://github.com/AntonEvers/gra-meta-foundation) no GitHub para obter os metapackages e os módulos de amostra usados neste exemplo.

```text
.
├── packages/
│   └── antonevers
│       ├── gra-meta-brand-x
│       ├── gra-meta-foundation
│       ├── module-3rdparty
│       ├── module-gra
│       └── module-local
├── composer.json
└── composer.lock
```

Você pode ter vários namespaces dentro do diretório `packages`, se necessário.

O desenvolvimento ocorre no diretório packages. Os symlinks para os pacotes dentro do diretório `packages` são criados no diretório `vendor` depois que você executa `composer update`. Dessa forma, o código se torna parte da instalação do Adobe Commerce.

Run `bin/magento module:enable --all` or for only specific modules to enable the modules that were added.

By now you should have a working Adobe Commerce installation with the three sample modules installed and working. You can validate if the modules are installed and working by running the commands:

```bash
bin/magento test:gra
bin/magento test:3rdparty
bin/magento test:local
```

### Achieve automated package creation

There are multiple options to achieve automated package creation. Some options are:

1. [Private Packagist](https://packagist.com/)
1. [Simplyfy Monorepo Builder](https://github.com/symplify/monorepo-builder)
1. Build your own solution

[Private Packagist](https://packagist.com/) automates recognizing packages in the Git monorepo and exposes them through Composer. It is compatible with Adobe Commerce, fast, low-maintenance and error-prone, which is why this guide focuses on the Private Packagist option.

It is beyond the scope of this guide to explain how to set up Private Packagist, please see the [docs](https://packagist.com/docs).

There is the possibility to turn a package into a monorepo once you have set up organization syncing and your Git repositories are automatically syncing to Private Packagist.

First, go to the packages tab and find the monorepo:

![Private Packagist screen shot with the monorepo package visible in the packages screen](/help/assets/global-reference-architecture/packagist-packages-before-multi-package.png){align="center"}

Click on the monorepo package and click &quot;Edit&quot; in the details screen, which takes you to the following page:

![Private Packagist screen shot with the monorepo package edit page](/help/assets/global-reference-architecture/packagist-packages-edit.png)

Underneath the first input field, there is a link saying: Create a multi-package repository. Click this link.

![Private Packagist screen shot with the multi-package configuration](/help/assets/global-reference-architecture/packagist-packages-multi-package.png)

Define the location where composer packages can be found inside your monorepo. In the example, the location is `packages/**/composer.json`. Change the location to limit or broaden where Private Packagist searches for packages to extract.

A guia Pacotes mostrará todos os pacotes encontrados após salvar, e o monorepo em si não estará mais visível como um pacote do Composer:

![Captura de tela de Packagist Particular com todos os pacotes monorepo visíveis na tela de pacotes](/help/assets/global-reference-architecture/packagist-packages-after-multi-package.png)

Uma versão é criada no Composer para cada pacote dentro do monorepo, para cada tag ou ramificação criada no monorepo no Git.

## Instalar os pacotes no ambiente de produção

Siga as instruções de Private Packagist para adicionar Private Packagist como um repositório do compositor. O Packagist privado pode e deve ser usado como um espelho para todos os repositórios Composer e repositórios Git, incluindo packagist.org. Dessa forma, as credenciais não precisam ser compartilhadas com desenvolvedores e você tem controle total sobre cada pacote. Este exemplo não segue essa prática recomendada, pois exporia a base de código do Adobe Commerce publicamente.

Baixe a [Marca GRA Monorepo X](https://github.com/AntonEvers/gra-monorepo-brand-x) do GitHub para ver um exemplo de uma loja de produção.

No armazenamento de produção, não há diretório `packages`, e todos os pacotes são instalados pelo Composer. O único pacote necessário é:

```json
    "require": {
        "antonevers/gra-meta-brand-x": "^1.0"
    },
```

No entanto, todo o Adobe Commerce e toda a GRA é instalada por meio dos requisitos desse metapackage.

## Controle de versão

Todos os pacotes no monorepo recebem a mesma versão que o monorepo em si. Pense nisso como a publicação de novas versões de todo o aplicativo. No entanto, durante a produção, é possível instalar uma combinação de pacotes de diferentes versões do monorepo.

## Ambientes efêmeros

Se você usar ambientes efêmeros ou planeja usá-los, o monorepo é uma excelente escolha. Cada versão e ramificação do monorepo contém todos os arquivos de módulo Adobe Commerce, de terceiros e personalizados. Com uma instalação completa em cada ramificação, é possível executar todos os tipos de teste, incluindo testes funcionais. Com outras configurações de GRA, como os pacotes separados ou pacotes em massa GRA, primeiro seria necessário criar um ambiente de trabalho do Adobe Commerce antes de poder executar testes funcionais. Da perspectiva do DevOps, o monorepo o torna muito mais simples.

## Exemplos de código

Os exemplos de código deste artigo foram combinados em um conjunto de repositórios Git, que podem ser usados para reproduzir com a prova de conceito.

* Um exemplo de repositório monorepo: <https://github.com/AntonEvers/gra-monorepo>
* Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-monorepo-brand-x>
