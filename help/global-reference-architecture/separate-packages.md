---
title: Arquitetura de referência global de pacotes separados
description: Otimizar o Adobe Commerce com pacotes separados GRA. Conheça a configuração, os benefícios e as práticas recomendadas para o gerenciamento flexível e com controle de versão de pacotes.
jira: KT-16727
doc-type: tutorial
audience: all
last-substantial-update: 2025-1-6
feature: Best Practices, Configuration, Install
topic: Architecture, Commerce, Development
badge: label="Contribuição de Tony Evers, arquiteto técnico sênior, Adobe" type="Informative" url="https://www.linkedin.com/in/evers-tony/" tooltip="Contribuição de Tony Evers"
role: Architect, Developer, User, Leader
level: Beginner, Intermediate
exl-id: cbddc4a3-602f-4208-85cd-b906d2b81f8b
source-git-commit: e0b11bbcfff830badf471206ead59fc48dd14b7c
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 0%

---

# O padrão de arquitetura de referência global de pacotes separados

Este guia explica como configurar o Adobe Commerce com o padrão GRA (Global Reference Architecture) de pacotes separados.

O padrão GRA de pacotes separados envolve um repositório Git para cada pacote comum e um repositório Git para cada instância do Adobe Commerce. Pacotes comuns são expostos por meio do Composer com um repositório de compositor privado.

Esse padrão de arquitetura de referência global é completamente baseado no Composer e foi projetado para obter o máximo benefício de todos os recursos do Composer.

![Um diagrama que mostra onde o código está armazenado em um padrão GRA de Pacotes Separados](/help/assets/global-reference-architecture/separate-packages-gra-pattern-diagram.png){align="center"}

## Vantagens e desvantagens deste padrão

Vantagens

- Reutilização de código por meio de repositórios de código compartilhados
- Flexibilidade total na instalação de pacotes, cada pacote de GRA pode ser atualizado, rebaixado ou ter backport individualmente
- Suporte completo para controle de versão semântico
- Não é necessária nenhuma ferramenta especial, infraestrutura complexa ou estratégia especial de ramificação
- Suporte para todos os tipos de encapsulamento que o Composer suporta

Desvantagens:

- O desenvolvimento dentro deste padrão GRA é ligeiramente mais difícil no início, há uma pequena curva de aprendizagem
- Possível implantar combinações de pacotes que não foram desenvolvidos na mesma configuração; necessidade de procedimentos de teste rigorosos

## Configurar o Adobe Commerce com o padrão GRA de pacotes separados

### A estrutura de diretório

A estrutura de diretório final de uma instalação completa do Adobe Commerce com o padrão GRA de pacotes separados é semelhante a:

```text
.
├── app/
│   └── etc/
│       └── config.php
├── composer.json
└── composer.lock
```

Os diretórios `app/code`, `app/i18n` e `app/design` foram omitidos na finalidade. A GRA Pacotes separados instala cada pacote do Composer. Mesmo que o pacote seja instalado somente em uma única instância do Adobe Commerce.

### Preparar o repositório de armazenamento

Crie um repositório para a primeira instância do Adobe Commerce, que representa uma loja da Web para a Marca X.

```bash
mkdir gra-separate-brand-x
cd gra-separate-brand-x
composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .
git init
git remote add origin git@github.com:AntonEvers/gra-separate-brand-x.git 
git add composer.json composer.lock
git commit -m 'initialize Brand X repository'
git push -u origin main
```

Instale o Adobe Commerce com `bin/magento setup:install`. Confirme o `app/etc/config.php` resultante.

### Criar repositórios de packages

Cada pacote neste padrão de arquitetura de referência global tem seu próprio repositório Git. Abaixo estão exemplos de pacotes que contêm módulos Adobe Commerce representando um módulo GRA, um módulo de terceiros e um módulo local.

- <https://github.com/AntonEvers/module-example-gra>
- <https://github.com/AntonEvers/module-example-3rdparty>
- <https://github.com/AntonEvers/module-example-local>

Use os exemplos para criar seus próprios pacotes.

### Criar repositórios de metapackage

Metapackages controlam o escopo da base de código comum GRA neste padrão GRA. Eles definem o que está na base: qual combinação de versões de pacote é sempre instalada em conjunto. Um exemplo:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0",
        "magento/composer-dependency-version-audit-plugin": "~0.1",
        "magento/composer-root-update-plugin": "~2.0",
        "magento/product-enterprise-edition": "2.4.6-p3"
    }
}
```

O trecho acima é o composer.json de um metapackage. Porque os metapackages contêm apenas um arquivo composer.json e nenhum outro código. O código acima também é o metapackage completo. Hospede-o em um repositório Git e você tem um repositório instalável do metapackage composer. Ele requer um módulo GRA de exemplo e um módulo de terceiros, bem como o núcleo do Adobe Commerce. Também requer o gra-component-foundation, que será explicado no próximo capítulo.

Os metapackages são uma maneira de agrupar pacotes sem criar dependências entre eles. Assim, mesmo quando não há dependência técnica entre os pacotes, com um metapackage você pode fazer com que eles sejam instalados juntos. Se você precisar desse metapackage no projeto, qualquer pacote ou metapackage exigido pelo metapackage será instalado. Portanto, se você criar um projeto de compositor em branco e precisar apenas desse pacote, o Composer instalará o Adobe Commerce e o GRA e o módulo de terceiros.

Dessa forma, você pode garantir que cada armazenamento contenha o mesmo conjunto de pacotes fundamentais.

Você pode definir de forma semelhante um metapackage que define store x. Ele requer o metapackage de fundação, exigindo a fundação GRA completa, além de um módulo local:

```json
{
    "name": "antonevers/gra-meta-brand-x",
    "type": "metapackage",
    "require": {
        "antonevers/gra-meta-foundation": "~1.0",
        "antonevers/module-local": "~1.0"
    }
}
```

O metapackage Brand-X é opcional. Você também pode pular o metapackage da marca e exigir essas dependências diretamente no projeto do Composer da loja. A vantagem de criar um metappackage para módulos locais é que você não tem ramificações de recursos e solicitações de pull de recursos no repositório Git da loja, somente nos repositórios de packages. É uma medida de segurança. Além disso, você pode optar por aplicar o controle de versão semântico nos repositórios de packages e usar diferentes tags Git em seu projeto principal, por exemplo, para rastrear releases nomeadas. Depende de você.

### Arquivos de base GRA fora do diretório do fornecedor

Às vezes, é necessário armazenar arquivos fora do diretório do fornecedor. Como `.gitignore`, arquivos que vão para o diretório `dev/` ou arquivos de verificação de domínio. O tipo de pacote do componente magento2 foi projetado para essa finalidade. Olhe para <https://github.com/AntonEvers/gra-component-foundation>.

```json
{
    "name": "antonevers/gra-component-foundation",
    "type": "magento2-component",
    "require": {
        "magento/magento-composer-installer": "*"
    },
    "extra": {
        "map": [
            [
                "src/gitignore",
                ".gitignore"
            ]
        ]
    }
}
```

Este pacote tem o componente tipo magento2 e contém um diretório src que hospeda arquivos copiados para o diretório raiz do Adobe Commerce. O mapeamento neste arquivo copia `/src/gitignore` para `/.gitignore` no projeto Composer principal.

Dessa forma, você também pode tornar arquivos fora do diretório de fornecedores parte da sua base GRA.

### Desenvolver um módulo de base de GRA

O desenvolvimento ocorre dentro do diretório de fornecedor. Peça ao Composer para instalar seus pacotes de base a partir da origem. Ao fazer isso, o verifica os pacotes do Git em vez de instalá-los de um arquivo baixado.

```bash
rm -r vendor/antonevers/*
composer install --prefer-source
```

Com este comando, foi feito o check-out dos pacotes no namespace antonevers usando o Git. Ao entrar no diretório vendor/antonevers/module-gra, você também estará inserindo o repositório Git module-gra. Agora é possível criar, finalizar e mesclar ramificações no local e desenvolver dessa maneira, diretamente do diretório do fornecedor.

### Incluir módulos de terceiros na base de GRA

Adicione pacotes de terceiros ao metapackage GRA. Se o código de terceiros não estiver disponível para ser instalado a partir de um repositório do Composer, crie um pacote para ele. Crie um repositório Git, adicione o conteúdo dos pacotes (tudo o que estaria em app/code/Vendor/Package) e verifique se há um arquivo composer.json válido na raiz do repositório. Agora você pode instalar esse pacote através do Composer.

## Configurar um repositório privado do Composer

Um repositório privado não é obrigatório na arquitetura de referência global. Ele agiliza as implantações e a instalação, reduz a configuração do repositório no composer.json e aumenta a segurança. As credenciais para outros repositórios do Composer e o marketplace do Adobe Commerce são armazenadas em seu repositório privado. Não há mais credenciais confidenciais agrupadas com o código ou nos computadores dos desenvolvedores.

Além disso, alguns repositórios privados oferecem funcionalidades adicionais, como notificações por email quando uma de suas lojas contém uma vulnerabilidade de segurança em uma de suas dependências.

O problema de lentidão é o que ocorre quando você tem vários repositórios VCS no composer.json. Cada repositório do Composer precisa ser lido ao fazer atualizações e ter 50 repositórios para 50 pacotes tem pelo menos 50 vezes a sobrecarga de apenas um único repositório do Composer.

![Um diagrama que mostra onde ocorre a lentidão quando um repositório do compositor está ausente](/help/assets/global-reference-architecture/separate-packages-without-mirror-diagram.png){align="center"}

Inclua um espelho do Composer na forma de um repositório privado do Composer. O espelho contém uma cópia de todos os pacotes de outros repositórios do Composer, bem como de todos os pacotes hospedados no Git. Com um repositório privado do Composer, você também obtém controle de acesso refinado.

Com a sincronização do Git, um repositório privado do Composer detecta automaticamente novos pacotes nos repositórios Git, bem como novas versões de pacotes existentes.

Você pode hospedar seu próprio repositório privado com o Satis: <https://composer.github.io/satis/>. Veja um exemplo de repositório público em <https://antonevers.github.io/gra-composer-repository/>. Esse repositório é usado como o repositório do compositor nos exemplos de código. São necessárias medidas adicionais para tornar privado um repositório Satis.

Há soluções que você pode configurar e esquecer: Private Packagist <https://packagist.com/>, que é feito pelas mesmas pessoas que escreveram o Composer ou JFrog Artifactory <https://jfrog.com/artifactory/>.

## Código de entrega

Com metapackages, há 3 etapas para fornecer código.

1. Mesclar alterações em pacotes e criar versões dos pacotes alterados.
2. (Opcional, somente se novos pacotes forem adicionados) Exigir os novos pacotes em metapackages e criar a versão dos metapackages.
3. (Opcional, somente se novos pacotes forem adicionados) Exigir os novos metapackages no Adobe Commerce e implantar.

O escopo de implantação é controlado com versões de pacote. A criação de uma versão estável de um pacote significa que ele está pronto para a implantação de produção.

Para criar uma nova versão, execute a atualização do Composer no projeto Composer principal, que contém a instalação de armazenamento completo. Todas as versões mais recentes dos pacotes são instaladas.

## Controle de versão

Controle de versão em pacotes separados GRA é um sinônimo de módulos de marcação no Git. As tags Git criam versões numeradas dos seus pacotes que o Composer instala.
A abordagem de controle de versão correta permite que seus pacotes fluam automaticamente e, ao mesmo tempo, permaneçam seguros.

Dois exemplos:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "1.1.4",
        "antonevers/module-gra": "1.0.0",
        "antonevers/module-3rdparty": "1.3.89"
    }
}
```

Este exemplo mostra uma definição estrita de dependências. 3 pacotes são necessários nas versões exatas. A atualização do Composer com este metapackage na sua instalação não faz nada. Ele sempre instala esses três pacotes nessas versões exatas, mesmo se uma versão mais recente estiver disponível.

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.0",
        "antonevers/module-gra": "~1.0",
        "antonevers/module-3rdparty": "~1.0"
    }
}
```

Este exemplo mostra uma definição ampla de dependências. Com `~1.0`, qualquer versão desses pacotes poderá ser instalada se forem maiores ou iguais a `1.0.0` e menores que `2.0.0`, com preferência pela versão mais alta disponível. Você pode saber mais sobre como definir dependências de versão em <https://getcomposer.org/doc/articles/versions.md>:

> O operador ~ é melhor explicado pelo exemplo: `~1.2` é equivalente a `>=1.2 <2.0.0`, enquanto `~1.2.3` é equivalente a `>=1.2.3 <1.3.0`.

Assim que você lançar uma nova versão de qualquer um dos pacotes mencionados, ela será instalada automaticamente com a atualização do Composer.

Aplicar controle de versão semântico. Você pode aprender tudo sobre o controle de versão semântico em <https://semver.org/>. Especialmente, as Perguntas frequentes são obrigatórias. Com o controle de versão semântico, os números em &quot;1.0.0&quot; são chamados de MAJOR.MINOR.PATCH. As versões secundárias e de patch de um pacote devem ser introduzidas com segurança, sem quebrar o aplicativo.
Você pode incluir patches automaticamente e escolher atualizações secundárias manualmente. Esteja ciente de que isso custa despesas gerais adicionais ao selecionar cada pequena alteração manualmente:

```json
{
    "name": "antonevers/gra-meta-foundation",
    "type": "metapackage",
    "require": {
        "antonevers/gra-component-foundation": "~1.1.0",
        "antonevers/module-gra": "~1.0.0",
        "antonevers/module-3rdparty": "~1.3.0"
    }
}
```

É claro que tudo isso só funciona se você aplicar o controle de versão semântico de forma consistente, sempre. E não apenas em metapackages, mas os requisitos de seus pacotes regulares também devem definir dependências livremente. Se você tiver uma dependência estrita no sistema, esse pacote será limitado à definição estrita.

Encontre essas dependências estritas digitando composer depends \&lt;nome do pacote\>. Consulte <https://getcomposer.org/doc/03-cli.md#depends-why> para obter mais informações.

## Estratégia de ramificação

É possível usar várias estratégias de ramificação para suportar esse padrão de estratégia de referência global, desde que a ramificação principal seja a única ramificação na qual você cria a versão dos seus pacotes. Se você analisar a versão em várias ramificações, isso apresenta o risco de perder aleatoriamente a funcionalidade entre as versões. Criar apenas versões estáveis na ramificação principal.

Criar ramificações de recursos somente nos repositórios de packages. Não nos repositórios de instalação da loja. Permaneça capaz de introduzir qualquer alteração na sua loja apenas usando o Composer. Evite a necessidade de mesclagens Git no repositório de implantação.

Tipos de ramificação comuns em estratégias e repositórios de ramificação nos quais devem existir:

**Ramificações de recursos**: existem em seus repositórios de pacotes, em nenhum outro lugar.

**Ramificações de versão**: são criadas em qualquer repositório: pacotes, metapackages, repositórios de instalação de armazenamento. Ao planejar uma versão, agrupe as alterações nas ramificações de lançamento dos pacotes antes de fazer o controle de versão. Suponha que você esteja preparando uma versão com o nome de código &quot;Unicórnio&quot;. Você pode criar uma ramificação de unicórnio de versão em pacotes com alterações. Mescle qualquer coisa nele e exija &quot;dev-release-unicorn as 1.4.0&quot; em seu metapackage. Saiba mais sobre aliases para ver o que está acontecendo lá: <https://getcomposer.org/doc/articles/aliases.md>.

**Ramificações de controle de qualidade/desenvolvimento**: semelhante às ramificações de lançamento.

**Ramificação principal**: deve existir em todos os repositórios e sempre deve ser a ramificação que representa um estado de produção ou pronto para produção. A ramificação principal é onde você marca o código para versões de lançamento.
Escolha uma estratégia de ramificação com pouca sobrecarga de manutenção. Por exemplo, mesclar a ramificação principal de volta às ramificações de controle de qualidade, UAT, versão ou desenvolvimento após uma versão de hotfix é uma tarefa de manutenção de sobrecarga. Quanto mais packages, mais repositórios e mais tarefas de overhead repetitivas.

Use uma ferramenta como mixu/gr para executar operações de rotina em vários repositórios Git em um lote: <https://github.com/mixu/gr>

## Nomeação de convenções

Com o padrão GRA de Pacotes Separados, os pacotes fazem parte da base GRA se o metapackage de base os exigir. Adicione ou remova pacotes do metapackage para movê-los para dentro e para fora da base.

Os metapackages oferecem flexibilidade ao escopo de instalação dos pacotes. É extremamente importante que os nomes dos pacotes não contenham palavras relacionadas ao uso pretendido do pacote. O nome antonevers/module-gra-store-locator pode se tornar confuso quando você decide retirar esse pacote da base GRA. Evite o escopo (GRA, fundação, local). Evite a região (EMEA, Espanha, Global). Definitivamente, evite o nome do armazenamento para o qual um pacote é criado. Escolha nomes que se relacionam apenas à funcionalidade que é adicionada no pacote. Dessa forma, você pode reutilizá-los em qualquer lugar que desejar, também em cenários futuros imprevistos. O nome antonevers/module-store-locator seria excelente.

Verifique se os pacotes relacionados são exibidos juntos nas visões gerais. Crie nomes de genéricos para específicos. Então, antonevers/module-b2b-tax-free ao invés de antonevers/tax-free-module-b2b.

## Exemplos de código

Os exemplos de código desta publicação do blog foram combinados em um conjunto de repositórios Git, que podem ser usados para reproduzir com a prova de conceito.

- Um exemplo de armazenamento de produção: <https://github.com/AntonEvers/gra-separate-brand-x>
- Um exemplo de módulo de base: <https://github.com/AntonEvers/module-example-gra>
- Um exemplo de módulo de terceiros: <https://github.com/AntonEvers/module-example-3rdparty>
- Um exemplo de módulo local: <https://github.com/AntonEvers/module-example-local>
- Um exemplo de metapackage de fundação: <https://github.com/AntonEvers/gra-meta-foundation>
- Um exemplo de metapackage local (opcional): <https://github.com/AntonEvers/gra-meta-brand-x>
- Um exemplo de repositório do Composer: <https://github.com/AntonEvers/gra-composer-repository>
