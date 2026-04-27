---
title: Otimização do Adobe Commerce com arquitetura de referência global de pacotes em massa
description: Saiba como configurar o Adobe Commerce usando a Arquitetura de referência global de pacotes em massa para um gerenciamento de código eficiente e controle de versão.
jira: KT-16726
doc-type: tutorial
duration: 391
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac63e31e-3047-410a-a6f9-a578b495bd8c
TQID: https://experienceleague.adobe.com/q4NzQxc7XJDB-TNv2pU7ghDr6bahliY6soUGPu7fhfg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 1188
ht-degree: 0%

---

# O padrão de arquitetura de referência global de pacotes em massa

{{only-for-on-prem-commerce-cloud}}

Este guia explica como configurar o Adobe Commerce com o padrão GRA (Global Reference Architecture) de pacotes em massa.

O padrão GRA de pacotes em massa envolve um único repositório Git para hospedar todas as personalizações comuns. Esse único repositório Git é exposto por meio do Composer como um único pacote de composição, que contém vários módulos do Adobe Commerce.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA de pacotes em massa](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

* Reutilização de código por meio de um repositório de código compartilhado
* Flexibilidade para instalar diferentes versões históricas do GRA em diferentes instâncias, permitindo versões em fases
* Flexibilidade para realizar backport e manter várias versões principais do GRA
* Suporte para o controle de versão semântico do GRA
* Simplicidade, os desenvolvedores não precisam de mais habilidades do que nos padrões comuns de desenvolvimento de uma única loja
* Não é necessária nenhuma ferramenta especial, infraestrutura complexa ou estratégia especial de ramificação
* A combinação de pacotes em uma versão é sempre desenvolvida e testada em conjunto

Desvantagens:

* Só é possível atualizar a GRA completa, incluindo todos os pacotes nela contidos.
* Nenhum suporte no pacote em massa GRA para pacotes do compositor além de módulos do Adobe Commerce, pacotes de idiomas e temas, portanto, não há metapackages, pacotes de componentes magento2, plug-ins e patches do Composer

## Configurar o Adobe Commerce com o padrão Split Git GRA

### A estrutura de diretório

O GRA de pacotes em massa instala todo o código reutilizável por meio dos repositórios do Composer. O código específico de uma única instância reside no repositório Git dessa instância. O código específico da instância não é reutilizado em outras instâncias do Adobe Commerce.

A estrutura de diretório final de uma instalação completa do Adobe Commerce com o padrão GRA de pacotes em massa é semelhante a:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    └── local/
```

Os diretórios `app/code`, `app/i18n` e `app/design` foram omitidos de propósito, porque o Composer não avalia o código nesses diretórios. Como resultado, as dependências declaradas nos pacotes não são instaladas automaticamente. O padrão GRA de Pacotes em Massa resolve esse problema instalando algum código personalizado em `packages/` e tratando esse diretório como um repositório de compositor. Pacotes de symlinks do compositor dentro de `packages/` para `vendor/`.

### Preparar os repositórios Git

Crie dois repositórios Git para o código GRA compartilhado e para a primeira loja. Comece com o repositório GRA, que tem a seguinte estrutura de arquivos:

O resultado é a seguinte estrutura de diretório:

```text
.
├── composer.json
└── src/
    ├── GraOne/
    │   ├── composer.json
    │   └── registration.php
    ├── GraTwo/
    │   ├── composer.json
    │   └── registration.php
    └── registration.php
```

Esta estrutura de diretório só menciona o arquivo composer.json e o arquivo registration.php dos módulos GraOne e GraTwo. Na realidade, há mais arquivos dentro desses módulos.

Execute estes comandos para iniciar o repositório Git:

```bash
mkdir gra-bulk-foundation
cd gra-bulk-foundation
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-foundation.git
vim composer.json # see code snippet below for contents
git add composer.json
git commit -m 'initialize GRA foundation repository'
git push -u origin main
```

O conteúdo do arquivo composer.json:

```json
{
    "name": "antonevers/gra-bulk-foundation",
    "description": "Shared code repository",
    "type": "library",
    "license": [
        "OSL-3.0",
        "AFL-3.0"
    ],
    "require": {},
    "autoload": {
        "files": [
            "src/registration.php"
        ],
        "psr-0": {
            "": "src/"
        }
    }
}
```

Altere o namespace do pacote composer.json para seu próprio namespace.

O conteúdo do arquivo src/registration.php:

```php
<?php

declare(strict_types=1);

$pathList[] = dirname(__DIR__) . '/src/*/*/registration.php';
foreach ($pathList as $path) {
    $files = glob($path, GLOB_NOSORT | GLOB_ERR);
    if ($files === false) {
        throw new RuntimeException('glob() returned error while searching in \'' . $path . '\'');
    }
    foreach ($files as $file) {
        require_once $file;
    }
}
```

O arquivo registration.php procura outros arquivos registration.php dentro dos módulos do Adobe Commerce e os executa.

Crie os dois módulos de exemplo usando o código em <https://github.com/AntonEvers/gra-bulk-foundation>. O Composer não avalia os arquivos composer.json nos módulos de amostra. Eles estão lá como um hábito. Se você decidir mover os módulos para outro lugar, os arquivos composer.json serão necessários novamente.

### Configurar o repositório de armazenamento

O repositório de implantação contém toda a instalação do Adobe Commerce, incluindo o código GRA. Crie o repositório de implantação:

```bash
mkdir gra-bulk-brand-x
cd gra-bulk-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-bulk-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Instale o Adobe Commerce com `bin/magento setup:install`. Instale os módulos de amostra de GRA no repositório de implantação com o Composer:

```bash
composer config repositories.gra-foundation vcs git@github.com:AntonEvers/gra-bulk-foundation.git
composer require antonevers/gra-bulk-foundation:@dev
bin/magento module:enable AntonEvers_GraOne AntonEvers_GraTwo
bin/magento test:gra-one
bin/magento test:gra-two
git add app/etc/config.php composer.json composer.lock
git commit -m 'install GRA foundation'
git push origin main
```

Esse último comando deve resultar na seguinte saída para provar que o módulo está instalado e funcionando:

```bash
GRA One module is installed successfully and working!
GRA Two module is installed successfully and working!
```

É possível criar vários pacotes em massa para organizar o código. Por exemplo, um pacote em massa de terceiros para código de terceiros que não está disponível por meio do Composer. Tudo o que você normalmente instalaria no `app/code` agora deve estar no diretório `src/` do pacote em massa. Uma exceção a essa regra é o código usado somente em uma única instância. Esses pacotes são chamados de locais.

### Instalar pacotes locais

O repositório de implantação hospeda pacotes locais. Eles não vivem no pacote em massa GRA. O local dos pacotes locais não é `app/code`, mas `packages/local`. Instruir o Composer a tratar esse diretório como um repositório:

```bash
composer config repositories.local path 'packages/local/*/*'
git add composer.json
git commit -m 'initialize local composer package storage'
git push origin main
```

Adicione o módulo de exemplo que está hospedado em <https://github.com/AntonEvers/module-example-local>:

```bash
mkdir -p packages/local
cd packages/local
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-local/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-local-main module-local
git add module-local
cd ../../..
composer require antonevers/module-local:@dev
bin/magento module:enable AntonEvers_Local
bin/magento test:local
```

Esse último comando deve resultar na seguinte saída para provar que o módulo está instalado e funcionando:

```bash
Local module is installed successfully and working!
```

Confirme o módulo local no repositório de marcas:

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

## Visão geral de locais de código

Somente se os terceiros não oferecerem instalação por meio de um repositório do Composer, você poderá armazenar módulos de terceiros no diretório `src/` do seu repositório de base ou em um pacote em massa dedicado de terceiros.

* **Adobe Commerce core**: disponível em repo.magento.com.
* **Módulos de terceiros**: disponíveis no Marketplace ou no repositório do Composer de um fornecedor.
* **Opção de fallback de módulos de terceiros**: armazenada em `src/` de um pacote em massa.
* **GRA foundation code**: armazenado em `src/` do pacote de base em massa.
* **Código local**: armazenado no diretório `packages/local` do repositório de implantação.

## Desenvolver um módulo GRA

Instale o pacote em massa a partir da origem para habilitar o Git no diretório do pacote em massa:

```bash
rm -r vendor/antonevers/gra-bulk-foundation
composer install --prefer-source
```

The bulk package has been checked out using Git. When you enter the `vendor/antonevers/gra-bulk-foundation` directory, you are also entering the gra-bulk-foundation Git repository. You can create, checkout and merge branches in this directory.

Add Composer dependencies to the composer.json file at the root of the GRA bulk package, which is the only file in the bulk package that Composer evaluates.

## Include third-party modules to the GRA bulk package

Add third-party packages in the require section of the composer.json at the root of the GRA foundation to add them to your GRA. That way, the packages are always installed in all your instances through composer.

## Deliver your code

To deliver code to the main branch, there are 2 paths. First the local modules, which are merged to the main branch. Run Composer update for those modules. Do not allow developers to update composer.lock in their ticket branches to reduce conflicts. Only update the composer.lock file in staging and production branches, which reduces the risk of conflicts.

Secondly, the GRA bulk packages, which are merged into the main branch of the GRA bulk repository. Then you can add a Git tag to the main branch, versioning the Composer package. Require your new version of the GRA bulk package in the composer.json of the deployment repository to install it.

## Branching strategy

This GRA pattern works with all branching strategies so long as you mirror the branching strategy of the deployment repositories in your GRA bulk repository. For releases, create a release branch with the same name in both repositories. For development, create a ticket branch in both repositories.

In ticket branches, you should almost never have to update the composer.lock file. Just check out the right branches in your development environment for both the store and the GRA foundation repository with Git. The exception is when you update requirements in the GRA foundation composer.json file. Upgrading the GRA foundation in the deployment repository is only done when building the release, or when building a QA branch.

## Code examples

Os exemplos de código deste artigo estão disponíveis como um conjunto de repositórios Git, que podem ser usados para testar a prova de conceito.

* Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-bulk-brand-x>
* O repositório de código GRA: <https://github.com/AntonEvers/gra-bulk-foundation>
* Um exemplo de módulo local: <https://github.com/AntonEvers/module-example-local>
