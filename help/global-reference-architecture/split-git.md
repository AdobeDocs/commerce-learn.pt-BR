---
title: Configuração do Adobe Commerce com a arquitetura de referência global Split Git
description: Saiba como configurar o Adobe Commerce usando a arquitetura de referência global Split do Git para um gerenciamento de código eficiente e uma implantação simplificada. ​
kt: 16725
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
topic: Architecture, Commerce, Development
old-role: Architect, Developer
role: Developer, User, Leader
level: Beginner, Intermediate
exl-id: ac544f77-8f5f-4ad1-92b2-bdf323100c13
source-git-commit: 79d57d2c04c42a8dc23b5735e72e841b7e51cc63
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%

---

# O padrão de arquitetura de referência global do Git Split

{{only-for-on-prem-commerce-cloud}}

Este guia explica como configurar o Adobe Commerce com o padrão Split Git Global Reference Architecture (GRA).

O padrão Git GRA dividido envolve dois repositórios Git para desenvolvimento e um repositório Git por instância do Adobe Commerce. Nos exemplos, presume-se que cada instância represente uma marca única.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA dividido](/help/assets/global-reference-architecture/split-git-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

- Reutilização de código por meio de um repositório de código compartilhado
- Padrão GRA simples, adequado mesmo para equipes com conhecimento Composer limitado
- Além de módulos, temas e pacotes de idiomas do Adobe Commerce, é possível instalar qualquer tipo de pacote do Composer por meio desse modelo, incluindo composer-plugin, composer-metapackage, magento2-component e patches
- Possível liberar em fases, planejando liberações para regiões em suas próprias janelas de manutenção
- Suporte para tags Git para fins administrativos, não para controle de implantação
- Garantir que a combinação de pacotes em uma implantação de produção seja desenvolvida e testada nessa configuração exata

Desvantagens:

- Sem flexibilidade adicional em comparação com outros padrões de GRA
- Não é possível atualizar ou fazer downgrade de módulos individuais por instância, sempre atualizar ou fazer downgrade da GRA como um todo
- Na maioria dos casos, o padrão de pacotes em massa é um melhor ajuste, pois é igualmente simples, mas mais convencional

## Configurar o Adobe Commerce com o padrão Split Git GRA

### A estrutura de diretório

O padrão Split Git GRA tem dois tipos de repositórios: repositórios de desenvolvimento e repositórios de instalação. Os repositórios de desenvolvimento contêm apenas parte de uma instalação completa do Adobe Commerce. Os repositórios de instalação contêm a instalação completa do Adobe Commerce e são usados para implantação, mas não para desenvolvimento.

A estrutura de diretório final de uma instalação completa do Adobe Commerce com o padrão Split Git GRA é semelhante a:

```text
.
├── .gitignore
├── app/
│   └── etc/
│       └── config.php
├── composer.json
├── composer.lock
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

Os diretórios `app/code`, `app/i18n` e `app/design` foram omitidos de propósito, porque o Composer não avalia o código nesses diretórios. Como resultado, as dependências declaradas nos pacotes não são instaladas automaticamente. O padrão Split Git GRA resolve esse problema instalando todo o código personalizado em `packages/` e tratando esse diretório como um repositório de compositor. Pacotes de symlinks do compositor dentro de `packages/` para `vendor/`.

### Preparar os repositórios Git

Criar 3 repositórios Git para:

1. Uma instância do Adobe Commerce
2. Código de terceiros que não está instalado por meio do Composer
3. Suas personalizações no formato de módulos, temas, pacotes de idiomas e assim por diante; seu GRA

Neste guia, os seguintes nomes são usados para esses repositórios:

1. gra-split-brand-x
2. gra-split-3rdparty
3. gra-split-gra

Todos os repositórios no padrão Split Git GRA são mesclados em um. Para que o Git permita a mesclagem de vários repositórios, todos os três repositórios precisam de um histórico compartilhado. Crie um projeto Git com uma única confirmação e envie-o para todos os controles remotos.

```bash
mkdir gra-split-brand-x
cd gra-split-brand-x
git init
git remote add origin git@github.com:AntonEvers/gra-split-brand-x.git
git remote add 3rdparty git@github.com:AntonEvers/gra-split-3rdparty.git
git remote add gra git@github.com:AntonEvers/gra-split-gra.git
touch .gitkeep
git add .gitkeep
git commit -m 'initialize repository'
git push -u origin main
git push 3rdparty main
git push gra main
```

Enviar o arquivo temporário `.gitkeep` para todos os controles remotos cria a mesma confirmação inicial com o mesmo hash de confirmação, criando um histórico compartilhado. Cada alteração criada em um local remoto pode ser mesclada com as outras.

Daqui, os repositórios divergem. O repositório gra-split-brand-x contém código específico da marca. O repositório gra-split-3rd-party contém somente código de terceiros. O repositório gra-split-gra contém somente a base de arquitetura de referência global, que consiste em todo o código personalizado.

Instale o Adobe Commerce no repositório gra-split-brand-x.

```bash
composer create-project --no-install --repository-url=https://repo.magento.com/ magento/project-enterprise-edition temp
mv temp/composer.json ./
rmdir temp
git add composer.json
git commit -m 'install Adobe Commerce'
git push origin main
```

Crie confirmações iniciais nos repositórios gra-split-3rd e gra-split-gra. A maneira mais fácil é verificando esses repositórios em diretórios separados.

```bash
cd ..
git clone git@github.com:AntonEvers/gra-split-3rdparty.git
git clone git@github.com:AntonEvers/gra-split-gra.git
cd gra-split-3rdparty
mkdir -p packages/3rdparty
touch packages/3rdparty/.gitkeep
git add packages/3rdparty/.gitkeep
git commit -m 'initialize 3rd party package storage'
git push origin main
cd ../gra-split-gra
mkdir -p packages/gra
touch packages/gra/.gitkeep
git add packages/gra/.gitkeep
git commit -m 'initialize GRA package storage'
git push origin main
```

Esses dois repositórios armazenam packages de terceiros e packages GRA. Pode haver um código exclusivo para cada instância do Adobe Commerce. Crie um local para armazenar esses pacotes locais no repositório gra-split-brand-x.

```bash
cd ../gra-split-brand-x
mkdir -p packages/local
touch packages/local/.gitkeep
git add packages/local/.gitkeep
git commit -m 'initialize local package storage'
git push origin main
```

### Onde armazenar diferentes tipos de código

O Adobe Commerce é um aplicativo do Composer. A maneira preferida de instalar é sempre por meio de repositórios do Composer. Somente se um fornecedor de módulo não oferecer instalação por meio de um repositório do Composer, você poderá armazenar módulos de terceiros no repositório de terceiros. O local preferencial para o código personalizado é o repositório GRA. Quando um módulo é usado somente por uma instância específica, ele se torna código local.

Resumindo:

- **Adobe Commerce**: armazenado em um repositório do Composer.
- **Módulos de terceiros**: armazenados em um repositório do Composer.
- **Opção de fallback de módulos de terceiros**: armazenada no repositório Git gra-split-3rd-party.
- **Código de base do GRA**: armazenado no repositório Git gra-split-gra.
- **Código local**: armazenado no repositório Git gra-split-brand-x.

### Conectar armazenamento de pacote ao Composer

O Composer pode tratar o diretório de pacotes como um repositório do composer. Informe o Composer sobre o local dos pacotes dentro do diretório de pacotes.

```json
"repositories": [
  {"type": "path", "url": "packages/local/*/*"},
  {"type": "path", "url": "packages/gra/*/*"},
  {"type": "path", "url": "packages/3rdparty/*/*"},
  {"type": "composer", "url": "https://repo.magento.com"}
]
```

O Composer procura arquivos composer.json em dois níveis nos três diretórios de armazenamento. Crie subdiretórios dentro dos três diretórios de armazenamento de código exatamente como eles apareceriam no diretório `vendor/`.

Por exemplo: se um pacote é normalmente instalado em `vendor/example-corp/module-example/`, então você o armazena em `packages/3rdparty/example-corp/module-example/`. O compositor vincula o pacote a `vendor/example-corp/module-example/` quando você precisar.

Use o namespace e o nome do pacote do compositor como a estrutura de diretório. Por exemplo: um módulo que tradicionalmente existe no `app/code/MyCorp/MyCustomization/` tem o nome `my-corp/module-my-customization` no composer.json. Armazenar este pacote em `packages/gra/my-corp/module-my-customization`.

### Incluir novos packages nos repositórios de instância

Mescle pacotes de dispositivos remotos de terceiros e do GRA no repositório gra-split-brand-x.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
git push origin main
```

O resultado é a seguinte estrutura de diretório:

```text
.
├── composer.json
└── packages/
    ├── 3rdparty/
    ├── gra/
    └── local/
```

As alterações no repositório de base de terceiros e do GRA são mescladas aos repositórios de marcas. Dessa forma, o código de terceiros e do GRA são mantidos somente em um local. Mova as alterações para as marcas com uma mesclagem Git.

A Adobe Commerce não reconhece automaticamente novos módulos. Executar o composer requer a adição de um novo pacote após uma mesclagem. Execute a atualização do composer toda vez que atualizar um de seus pacotes após uma mesclagem.

### Instalar módulos de exemplo

Como prova de conceito, instale módulos de exemplo para ver como o padrão GRA funciona.

Execute `composer install` e `bin/magento install` antes de seguir em frente.

Há 3 módulos de teste para o no GitHub:

1. [exemplo-módulo-local](https://github.com/AntonEvers/module-example-local)
2. [módulo-exemplo-gra](https://github.com/AntonEvers/module-example-gra)
3. [module-example-3rdparty](https://github.com/AntonEvers/module-example-3rdparty)

### Instalar um módulo local

Adicionar um módulo ao pool de códigos local é simples. Baixe e extraia o módulo. Exigir com o Composer. Habilite-o com `bin/magento` e confirme os arquivos no repositório de marcas.

```bash
cd gra-split-brand-x
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

Se você vir a saída acima, é possível confirmá-la com segurança no repositório da marca.

```bash
git add packages/local/antonevers/module-local app/etc/config.php composer.json composer.lock 
git commit -m 'add local module'
git push origin main
```

### Instalar e desenvolver um módulo de base GRA

Adicionar um módulo ao repositório GRA é diferente de instalar módulos locais. Por padrão, as confirmações são adicionadas à origem/principal, que é o repositório gra-split-brand-x. As alterações nos módulos GRA devem ser enviadas para o repositório gra-split-gra e mescladas ao repositório gra-split-brand-x posteriormente.

### Criar um ambiente de desenvolvimento

Crie um ambiente de desenvolvimento com uma combinação de todos os conjuntos de códigos em um único local. Você pode enviar o código para o repositório local, GRA e de terceiros individualmente por meio de links simbólicos. Comece criando um novo diretório de desenvolvimento ao lado da sua marca, do GRA e de diretórios de repositório de terceiros.

```text
.
├── gra-development    # <---
├── gra-split-3rdparty
├── gra-split-brand-x
└── gra-split-gra
```

```bash
cd ..
mkdir gra-development
cd gra-development
cp ../gra-split-brand-x/composer.json ../gra-split-brand-x/composer.lock .
mkdir packages
ln -s ../../gra-split-brand-x/packages/local/ packages/
ln -s ../../gra-split-3rdparty/packages/3rdparty/ packages/
ln -s ../../gra-split-gra/packages/gra/ packages/
```

O resultado é a seguinte estrutura de diretório:

```text
.
├── packages/
│ ├── 3rdparty -> ../../gra-split-3rdparty/packages/3rdparty/
│ ├── gra -> ../../gra-split-gra/packages/gra/
│ └── local -> ../../gra-split-brand-x/packages/local/
├── composer.lock
└── composer.json
```

Execute `composer install` e `bin/magento install` no diretório gra-development.

Agora é possível confirmar as alterações diretamente dos diretórios `packages/3rdparty`, `packages/gra` e `package/local`. O Git confirma as alterações no repositório Git ao qual os diretórios estão vinculados. É importante que o comando git commit seja executado no diretório `packages/3rdparty`, `packages/gra` ou `package/local`. Não execute o git commit na raiz do projeto.

### Instalar módulos de exemplo

Instale os módulos de exemplo de terceiros e GRA nos diretórios de pacotes.

```bash
cd packages/gra
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-gra/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-gra-main module-gra
git add module-gra
 
cd ../../3rdparty
mkdir antonevers
cd antonevers
curl -OL https://github.com/AntonEvers/module-example-3rdparty/archive/refs/heads/main.zip
unzip main.zip
rm main.zip
mv module-example-3rdparty-main module-3rdparty
git add module-3rdparty
 
cd ../../..
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
bin/magento test:gra
bin/magento test:3rdparty
```

Esse último comando deve resultar na seguinte saída para provar que o módulo está instalado e funcionando:

```bash
GRA module is installed successfully and working!
3rd party module is installed successfully and working!
```

Se você vir a saída acima, é possível confirmá-la com segurança no repositório da marca. Execute `git remote -v` para verificar se você está confirmando para o controle remoto correto.

```bash
cd packages/gra
git remote -v 
origin git@github.com:AntonEvers/gra-split-gra.git (fetch)
origin git@github.com:AntonEvers/gra-split-gra.git (push)
git add antonevers/module-gra
git commit -m 'add GRA module'
git push origin main
 
cd ../3rdparty
git remote -v 
origin git@github.com:AntonEvers/gra-split-3rdparty.git (fetch)
origin git@github.com:AntonEvers/gra-split-3rdparty.git (push)
git add antonevers/module-3rdparty
git commit -m 'add third-party module'
git push origin main
```

### Entregar código às instâncias

Mescle os repositórios GRA e de terceiros com o repositório gra-split-brand-x para entregar o código a uma instância do Adobe Commerce. Execute `composer require`, `bin/magento module:enable` e confirme o resultado.

```bash
cd gra-split-brand-x
git fetch - all
git merge gra/main 3rdparty/main
composer require antonevers/module-gra:@dev antonevers/module-3rdparty:@dev
bin/magento module:enable AntonEvers_Gra AntonEvers_ThirdParty
git add app/etc/config.php composer.lock composer.json
git commit -m 'install GRA and third-party modules'
git push origin main
```

## Estratégia de ramificação

Esse padrão GRA funciona com todas as estratégias de ramificação, se você espelhar a estratégia de ramificação dos repositórios de loja em seus repositórios de terceiros e GRA. Para versões do, crie uma ramificação de versão com o mesmo nome nos três repositórios. Mescle as ramificações de versão juntas no repositório de armazenamento durante a preparação da versão.

Às vezes, você tem uma ramificação de tíquete que requer o código local e de terceiros ou o código GRA para ser alterado. Nesse caso, as ramificações de ticket precisam ser criadas em todos os repositórios relacionados.

Nunca mescle confirmações de terceiros e do GRA no repositório da marca dentro das ramificações de tíquete. Em vez disso, verifique as ramificações certas no ambiente de desenvolvimento para cada pool de códigos. A mesclagem no repositório de marcas só é feita ao compor a versão ou ao compor uma ramificação de controle de qualidade.

## Exemplos de código

Os exemplos de código deste artigo estão disponíveis como um conjunto de repositórios Git, que podem ser usados para testar a prova de conceito.

- Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-split-brand-x>
- O repositório de código de terceiros: <https://github.com/AntonEvers/gra-split-3rdparty>
- O repositório de código GRA: <https://github.com/AntonEvers/gra-split-gra>
- Um exemplo de módulo local: <https://github.com/AntonEvers/module-example-local>
- Um exemplo de módulo GRA: <https://github.com/AntonEvers/module-example-gra>
- Um exemplo de módulo de terceiros: <https://github.com/AntonEvers/module-example-3rdparty>
