---
title: Arquitetura de referência global Monorepo
description: Saiba como usar a abordagem monorepo para arquitetura de referência global para estabelecer uma experiência de comércio escalável e resiliente
jira: KT-16728
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Experienced
exl-id: ebdc13cf-c452-4728-af00-c3ea1149c2fa
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 0%

---

# Padrão de arquitetura de referência global Monorepo

Este guia explica como configurar o Adobe Commerce com o padrão Monorepo Global Reference Architecture (GRA).

O padrão Monorepo GRA envolve um único repositório Git para hospedar todas as personalizações comuns. Esse único repositório Git é exposto por meio do Composer como um pacote de compositor separado.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA monorepo](/help/assets/global-reference-architecture/monorepo-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

- Ideal para testes funcionais
- Reutilização de código por meio de repositórios de código compartilhados
- Flexibilidade total na instalação de pacotes, cada pacote de GRA pode ser atualizado, rebaixado ou ter backport individualmente
- Suporte completo para controle de versão semântico
- Não é necessária nenhuma ferramenta especial, infraestrutura complexa ou estratégia especial de ramificação
- Suporte para todos os tipos de encapsulamento que o Composer suporta
- Ideal para ambientes efêmeros, que são opcionais, mas para equipes de entrega de alto volume, eles são muito úteis

Desvantagens:

- Possível implantar combinações de pacotes que não foram desenvolvidos na mesma configuração; necessidade de procedimentos de teste rigorosos
- O padrão de monorepo GRA pode ser complexo no início. Atribuir um cliente potencial que ajude a equipe a trabalhar com o sistema

## Configurar o Adobe Commerce com o padrão GRA de pacotes separados

### A estrutura de diretório

A estrutura de diretório final de uma instalação completa do Adobe Commerce com o padrão GRA de pacotes separados tem esta estrutura de diretório:

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

Um repositório Git de produção tem esta estrutura de diretório:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

A diferença é que as instâncias de produção são instaladas no Composer, onde o monorepo mantém sua própria cópia de cada pacote dentro do diretório de pacotes.

### Preparar um repositório de produção

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

Instale o Adobe Commerce com `bin/magento setup:install`. Confirmar os arquivos resultantes `app/etc/config.php` e o compositor. O compositor gerencia qualquer outra coisa para que nada mais esteja no Git.

### Preparar o repositório do monorepo

O repositório do monorepo começa com as mesmas etapas.

```bash
mkdir gra-monorepo 
cd gra-monorepo
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
```

Instalar o Adobe Commerce com `bin/magento setup:install`, confirmar e enviar.

```bash
git init
git remote add origin git@github.com:AntonEvers/gra-monorepo.git 
git add composer.json composer.lock app/etc/config.php
git commit -m 'initialize monorepo GRA development repository'
git push -u origin main
```

### Prepare-se para o desenvolvimento do monorepo

Para o desenvolvimento do monorepo, faça as seguintes alterações no arquivo composer.json:

1. Altere o nome e a descrição do pacote para que fique claro que este pacote é o seu pacote monorepo.
1. Exclua o atributo de versão do composer.json, pois a versão é gerenciada usando as tags Git para este repositório.
1. Substitua a seção necessária por um meta pacote que será criado posteriormente.
1. Alterar estabilidade mínima para desenvolvimento.
1. Adicione um repositório de tipo de caminho que aponte para `packages/*/*` para hospedar pacotes monorepo, incluindo aliases de ramificação para cada pacote que ele contém
1. Adicionar um alias de ramificação para o próprio projeto

O seguinte diff do Git mostra a diferença entre uma instalação limpa do Adobe Commerce e as alterações mencionadas acima:

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

Execute `bin/magento module:enable --all` ou apenas para módulos específicos para habilitar os módulos que foram adicionados.

Agora você deve ter uma instalação do Adobe Commerce em funcionamento com os três módulos de amostra instalados e em funcionamento. Você pode validar se os módulos estão instalados e funcionando executando os comandos:

```bash
bin/magento test:gra
bin/magento test:3rdparty
bin/magento test:local
```

### Obter criação automatizada de pacotes

Há várias opções para obter a criação automática de pacotes. Algumas opções são:

1. [Packagist Particular](https://packagist.com/)
1. [Simplesmente Monorepo Builder](https://github.com/symplify/monorepo-builder)
1. Crie sua própria solução

[Private Packagist](https://packagist.com/) automatiza o reconhecimento de pacotes no monorepo do Git e os expõe por meio do Composer. Ele é compatível com o Adobe Commerce, rápido, de baixa manutenção e sujeito a erros, e é por isso que este guia se concentra na opção Private Packagist.

Está além do escopo deste guia para explicar como configurar o Private Packagist, consulte os [documentos](https://packagist.com/docs).

Há a possibilidade de transformar um pacote em um monorepo depois de configurar a sincronização da organização e seus repositórios Git estiverem sincronizando automaticamente com o Private Packagist.

Primeiro, vá para a guia packages e localize o monorepo:

![Captura de tela de Packagist Particular com o pacote monorepo visível na tela de pacotes](/help/assets/global-reference-architecture/packagist-packages-before-multi-package.png){align="center"}

Clique no pacote monorepo e clique em &quot;Editar&quot; na tela de detalhes, que leva à seguinte página:

![Captura de tela do Packagist Particular com a página de edição do pacote monorepo](/help/assets/global-reference-architecture/packagist-packages-edit.png)

Abaixo do primeiro campo de entrada, há um link que diz: Create a multi-package repository (Criar um repositório de vários pacotes). Clique neste link.

![Captura de tela do Packagist Particular com a configuração de vários pacotes](/help/assets/global-reference-architecture/packagist-packages-multi-package.png)

Defina o local onde os pacotes do compositor podem ser encontrados dentro do monorepo. No exemplo, o local é `packages/**/composer.json`. Altere o local para limitar ou ampliar onde o Agente de pacote privado procura pacotes para extrair.

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

- Um exemplo de repositório monorepo: <https://github.com/AntonEvers/gra-monorepo>
- Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-monorepo-brand-x>
