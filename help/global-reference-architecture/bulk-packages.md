---
title: Otimização do Adobe Commerce com arquitetura de referência global de pacotes em massa
description: Saiba como configurar o Adobe Commerce usando a Arquitetura de referência global de pacotes em massa para um gerenciamento de código eficiente e controle de versão.
jira: KT-16726
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac63e31e-3047-410a-a6f9-a578b495bd8c
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 0%

---

# O padrão de arquitetura de referência global de pacotes em massa

Este guia explica como configurar o Adobe Commerce com o padrão GRA (Global Reference Architecture) de pacotes em massa.

O padrão GRA de pacotes em massa envolve um único repositório Git para hospedar todas as personalizações comuns. Esse único repositório Git é exposto por meio do Composer como um único pacote de composição, que contém vários módulos do Adobe Commerce.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA de pacotes em massa](/help/assets/global-reference-architecture/bulk-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

- Reutilização de código por meio de um repositório de código compartilhado
- Flexibilidade para instalar diferentes versões históricas do GRA em diferentes instâncias, permitindo versões em fases
- Flexibilidade para realizar backport e manter várias versões principais do GRA
- Suporte para o controle de versão semântico do GRA
- Simplicidade, os desenvolvedores não precisam de mais habilidades do que nos padrões comuns de desenvolvimento de uma única loja
- Não é necessária nenhuma ferramenta especial, infraestrutura complexa ou estratégia especial de ramificação
- A combinação de pacotes em uma versão é sempre desenvolvida e testada em conjunto

Desvantagens:

- Só é possível atualizar a GRA completa, incluindo todos os pacotes nela contidos.
- Nenhum suporte no pacote em massa GRA para pacotes do compositor além de módulos do Adobe Commerce, pacotes de idiomas e temas, portanto, não há metapackages, pacotes de componentes magento2, plug-ins e patches do Composer

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

- **Adobe Commerce core**: disponível em repo.magento.com.
- **Módulos de terceiros**: disponíveis no Marketplace ou no repositório do Composer de um fornecedor.
- **Opção de fallback de módulos de terceiros**: armazenada em `src/` de um pacote em massa.
- **GRA foundation code**: armazenado em `src/` do pacote de base em massa.
- **Código local**: armazenado no diretório `packages/local` do repositório de implantação.

## Desenvolver um módulo GRA

Instale o pacote em massa a partir da origem para habilitar o Git no diretório do pacote em massa:

```bash
rm -r vendor/antonevers/gra-bulk-foundation
composer install --prefer-source
```

O pacote em massa foi retirado usando o Git. Ao inserir o diretório `vendor/antonevers/gra-bulk-foundation`, você também está inserindo o repositório Git de base em massa. Você pode criar, fazer check-out e mesclar ramificações nesse diretório.

Adicione dependências do Composer ao arquivo composer.json na raiz do pacote em massa GRA, que é o único arquivo no pacote em massa que o Composer avalia.

## Incluir módulos de terceiros no pacote de GRA em massa

Adicione pacotes de terceiros na seção obrigatória do composer.json na raiz da base GRA para adicioná-los ao GRA. Dessa forma, os pacotes são sempre instalados em todas as instâncias por meio do Composer.

## Entregar o código

Para entregar o código à ramificação principal, há dois caminhos. Primeiro, os módulos locais, que são mesclados à ramificação principal. Execute a atualização do Composer para esses módulos. Não permita que os desenvolvedores atualizem composer.lock em suas ramificações de tíquete para reduzir conflitos. Atualize somente o arquivo composer.lock em ramificações de preparo e produção, o que reduz o risco de conflitos.

Em segundo lugar, os pacotes em massa de GRA, que são fundidos na ramificação principal do repositório em massa de GRA. Em seguida, você pode adicionar uma tag do Git à ramificação principal, criando uma versão do pacote do Composer. Exigir sua nova versão do pacote em massa GRA no composer.json do repositório de implantação para instalá-lo.

## Estratégia de ramificação

Esse padrão GRA funciona com todas as estratégias de ramificação, desde que você espelhe a estratégia de ramificação dos repositórios de implantação no seu repositório GRA em massa. Para versões do, crie uma ramificação de versão com o mesmo nome em ambos os repositórios. Para desenvolvimento, crie uma ramificação de ticket em ambos os repositórios.

Nas ramificações de tíquetes, quase nunca é necessário atualizar o arquivo composer.lock. Basta verificar as ramificações certas no ambiente de desenvolvimento para a loja e o repositório de base GRA com Git. A exceção é quando você atualiza os requisitos no arquivo composer.json do GRA Foundation. A atualização da base do GRA no repositório de implantação só é feita ao criar a versão ou ao criar uma ramificação de controle de qualidade.

## Exemplos de código

Os exemplos de código deste artigo estão disponíveis como um conjunto de repositórios Git, que podem ser usados para testar a prova de conceito.

- Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-bulk-brand-x>
- O repositório de código GRA: <https://github.com/AntonEvers/gra-bulk-foundation>
- Um exemplo de módulo local: <https://github.com/AntonEvers/module-example-local>
