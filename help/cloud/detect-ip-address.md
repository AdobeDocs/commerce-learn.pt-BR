---
title: Detectar endereços IP
description: Saiba como detectar endereços IP para ambientes da Adobe Commerce Cloud para aprimorar a segurança e simplificar a comunicação com o servidor
feature: Cloud, Configuration
topic: Commerce, Development, Integrations
role: Developer
level: Beginner
doc-type: Technical Video
duration: 0
last-substantial-update: 2025-04-07T00:00:00Z
jira: KT-17553
exl-id: beb0a6e1-e6b1-4ec0-976c-77a22a27e8a2
source-git-commit: 3acec65129773a8ba94eb52c53d15d7633440717
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# Detectar endereços IP de ambientes diferentes

Saiba como detectar endereços IP para diferentes ambientes em um projeto da Adobe Commerce Cloud. Ao usar uma série de comandos, incluindo Adobe Commerce CLI, sed, xargs, dig, grep e sort -u, os usuários podem identificar endereços IP para ambientes de desenvolvimento, preparo e produção.

## Para quem é este vídeo?

* Desenvolvedores: querendo entender como coletar os endereços IP do projeto da Adobe Commerce Cloud.
* Equipes de desenvolvimento e segurança que precisam restringir o acesso a sistemas de terceiros ou back-end

## Conteúdo de vídeo {#video-content}

* Saiba como descobrir o endereço IP de qualquer ambiente na Adobe Commerce Cloud.

>[!VIDEO](https://video.tv.adobe.com/v/3457493/?learn=on)

## Comando para obter o endereço IP

Observe que você precisa usar a ID do projeto e o nome do ambiente em vez das informações de espaço reservado.  Também pode ser necessário alterar o `{1..3}` para corresponder ao número de nós no cluster da Adobe Commerce Cloud, mas 3 é mais comum.

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1 | sed 's/.\.c\.(.)/\1/;s/.$//' | xargs -I% dig +short {1..3}."%" | grep '^\d' | sort -u
```

## CLI da Adobe Commerce Cloud

```bash
magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1
```

A ferramenta da CLI da magento-cloud foi projetada para ajudar desenvolvedores e administradores de sistema a gerenciar projetos e ambientes da Adobe Commerce Cloud com eficiência. Ele estende a funcionalidade do Cloud Console, permitindo que os usuários executem tarefas de rotina e executem automação localmente. Os principais recursos incluem gerenciamento de ambientes de integração, check-out e mesclagem de ambientes, listagem de variáveis e uso de SSH para conexão com ambientes remotos. A ferramenta simplifica os fluxos de trabalho permitindo que os comandos sejam executados diretamente da estação de trabalho local, aprimorando o processo geral de desenvolvimento e implantação.

Nesta seção inicial do código de exemplo, `magento-cloud environment:url -p InsertYourProjectID -e UseYourEnvironmentName --pipe -1`, ele está solicitando a URL para o ambiente. O valor retornado se parece com algo como este `http://integration-1ajmyuq-mk7xr7zmslfg.us-4.magentosite.cloud/`. De vez em quando se parece mais com este `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/`.  Este primeiro comando é bastante simples, e agora é hora de seguir para o próximo comando.

Para obter mais informações, leia a [Visão geral da CLI da nuvem](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview){target="_blank"}

## Usando `sed` para pesquisar e substituir

```bash
sed 's/.\.c\.(.)/\1/;s/.$//'
```

O comando `sed` no UNIX®Linux® significa Editor de Fluxo. Ele é usado para executar transformações básicas de texto em um fluxo de entrada (um arquivo ou entrada de um pipeline). Usos comuns incluem pesquisa, localização e substituição, inserção e exclusão de texto. O comando `sed` processa o texto linha por linha e aplica as operações especificadas, tornando-o uma ferramenta poderosa para manipulação de texto e scripts.

Como mencionado anteriormente, normalmente há dois tipos de URLs retornados da cli do `magento-cloud`. Há uma variação que contém `.com.c.c` no meio. Essa variante é a que precisa ser manipulada. Se esta estrutura for detectada, ela exigirá a remoção de tudo, desde o início da URL até `.com.c.c`.  Em seguida, o que resta é apenas a última parte da URL. Um exemplo de URL se parece com `http://mcprod.russell.dummycachetest.com.c.abcikdxbg789.ent.magento.cloud/`.  Quando este padrão é detectado, o objetivo é manter tudo após `.c.`.  Neste código de exemplo fornecido, `sed 's/.\.c\.(.)/\1/'` é usado para coletar esta parte e ignorar o restante do valor retornado original. A parte restante da URL é semelhante a `abcikdxbg789.ent.magento.cloud/`.\
Há dois comandos sendo executados em `sed`. Eles são separados por ponto e vírgula. A segunda parte do meu comando `sed` `;s/.$//'` é remover qualquer barra à direita, se elas existirem, para limpar essa URL para parecer com `abcikdxbg789.ent.magento.cloud`.  Nesse ponto, o URL foi limpo e está pronto para o próximo comando.

## Xargs com &#39;dig&#39;

```bash
xargs -I% dig +short {1..3}."%"
```

O comando `xargs` no UNIX®Linux® é usado para criar e executar linhas de comando a partir da entrada padrão. Ele pega a entrada de um pipe ou arquivo e a converte em argumentos para outro comando. É particularmente útil para lidar com um grande número de argumentos que excedem o limite do shell. O comando `xargs` pode ser usado para executar operações como mover, copiar ou excluir arquivos. Ele permite um processamento em lote eficiente, transmitindo vários argumentos para comandos em uma única execução.

O comando `dig`, abreviação de Domain Information Groper, é uma ferramenta de administração de rede usada para consultar servidores DNS (Domain Name System). Ajuda a recuperar informações sobre registros DNS, como registros A, AAAA, MX e CNAME. O comando `dig` é normalmente usado para solucionar problemas de DNS, verificar configurações de DNS e coletar informações detalhadas sobre nomes de domínio e seus endereços IP associados. Usando várias opções e sinalizadores, os usuários podem personalizar a saída para exibir detalhes específicos ou um resumo conciso.

O uso do `xargs` com `dig` o torna complicado, mas é necessário. O objetivo é pegar esse URL limpo e salvá-lo.  Depois que a URL é salva como variável, ela é inserida no comando `dig`.

O comando `dig` foi criado para coletar informações de DNS. Para reduzir a quantidade de dados retornada, o argumento `+short` é usado. Ao usar `dig` combinado com `+short`, endereços IP e, às vezes, cadeias de caracteres são retornados.

Nessa parte do comando, `xargs` salvará a URL `abcikdxbg789.ent.magento.cloud` e a inserirá no próximo comando `dig`. A técnica de salvar a URL combinada com a iteração facilita sua utilização com o comando `dig`. Lembre-se de que meu código de amostra é uma maneira de atingir a meta. Sinta-se à vontade para modificar coisas de acordo com suas necessidades e expectativas.

Nesse ponto, o URL está pronto. Em seguida, vamos ver como é possível verificar cada servidor no cluster. Para a Adobe Commerce Cloud, cada servidor no cluster tem um número. O identificador do servidor é um prefixo do URL que acabou de ser limpo e está pronto para uso. Uma maneira rápida e fácil de fazer check-out dos servidores é usando o `{1..3}`. Usando `{1..3}` que notifica o comando `dig` para ser executado 3 vezes. Veja a seguir uma representação do que acontece se você assistir à execução em tempo real.

```bash
dig +short 1.<projectid>.ent.magento.cloud
dig +short 2.<projectid>.ent.magento.cloud
dig +short 3.<projectid>.ent.magento.cloud
```

Para melhor ilustração, este exemplo de URL sendo usado por `dig` seria semelhante a:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
```

Se `{1..3}` foi modificado para ser `{1..6}`, então seria assim:

```bash
dig +short 1.aabcikdxbg789.ent.magento.cloud
dig +short 2.abcikdxbg789.ent.magento.cloud
dig +short 3.abcikdxbg789.ent.magento.cloud
dig +short 4.aabcikdxbg789.ent.magento.cloud
dig +short 5.abcikdxbg789.ent.magento.cloud
dig +short 6.abcikdxbg789.ent.magento.cloud
```

## O comando `grep`

Algumas vezes uma cadeia de caracteres é retornada como parte do resultado de `dig`. Para essa finalidade, o objetivo é somente endereços IP e eles são compostos de números com pontos. Para garantir que a saída final contenha apenas números, é possível ajustar o comando. Quando concluída, a sintaxe final é ` grep '^\d'`.  Ao adicionar `'^\d'`, o comando `grep` só mantém números e desconsidera qualquer outra coisa.

## O comando `sort`

Ao usar `sort -u`, ele remove todas as duplicatas da lista de IPs. As duplicatas só acontecem ao observar os níveis de desenvolvimento.

Esses ambientes de nível inferior são multilocatários e compartilham servidores subjacentes com muitos outros projetos. Os ambientes de desenvolvimento são servidores únicos e nunca um cluster. Portanto, quando o comando dig está em loop em cada iteração, ele retorna o mesmo IP várias vezes. Assim, ao usar o comando `sort -u`, todos os IPs duplicados são removidos e somente endereços IP exclusivos permanecem.



## Documentação relacionada

* [Endereços IP Regionais](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/regional-ip-addresses|https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/regional-ip-addresses){target="_blank"}
