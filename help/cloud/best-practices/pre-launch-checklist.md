---
title: Lista de verificação de pré-lançamento do Adobe Commerce Cloud
description: Saiba mais sobre a lista de verificação de pré-lançamento do Adobe Commerce Cloud.
feature: Cloud
topic: Commerce, Architecture, Development
role: Architect, Developer
level: Intermediate
doc-type: Tutorial
duration: 0
last-substantial-update: 2024-04-17T00:00:00Z
jira: KT-15180
kt: 15180
source-git-commit: 7cc6ee2906e5f223575d98f0f1b6f4bdf4c936d0
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 0%

---


# Lista de verificação de pré-lançamento do Commerce Cloud

Veja a seguir um resumo da Adobe Commerce [Documentação de lançamento do site](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}.

Essa lista de verificação tem como objetivo ajudar no planejamento e na execução de um lançamento bem-sucedido do site do Adobe Commerce Cloud. Colabore com o integrador de sistemas da Adobe Commerce Cloud para garantir que todas as tarefas de configuração e itens da lista de verificação sejam concluídas e verificadas. Se encontrar dificuldades com algum item da lista de verificação ou tiver dúvidas, entre em contato com o Consultor técnico ou engenheiro de sucesso do cliente designado. Se sua conta não tiver um CTA/CSE atribuído, você poderá criar um tíquete de suporte para obter assistência.

Se você tiver um CTA/CSE atribuído à conta, entre em contato com ele e com o Gerente de conta pelo menos quatro semanas antes de iniciar o novo site do Adobe Commerce Cloud para notificá-los sobre o **intenção** para iniciar.

- Algumas verificações são destacadas com [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}
- Colabore com seu desenvolvedor ou parceiro de integração de sistema para alinhar-se à abordagem de implementação.

>[!IMPORTANT]
> Você aceita [responsabilidade](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} para quaisquer efeitos adversos e riscos associados ao cronograma de lançamento da produção e à estabilidade contínua do site, se você não usar e concluir essa lista de verificação.

## 1. Pré-ativação

1. Revise a documentação sobre como testar e ativar [Documentação de lançamento do site](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Assegurar uma _&quot;plano de preparação para ativação&quot;_ O está totalmente preparado com seu parceiro ou integrador de sistemas, incorporando todos os itens de ação necessários. Lembre-se, embora a lista de verificação de pré-lançamento enfatize as práticas recomendadas do Adobe, ela _**não**_ substituir a necessidade de seu próprio plano de preparação para ativação.

2. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}[Guia do usuário](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. UAT (User Acceptance Testing, teste de aceitação do usuário) realizado pelo usuário final/comerciante, incluindo operações de back-end.
4. A equipe do integrador de sistemas executou UAT completo no preparo e na produção. Consulte a [Documentação do Experience League](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Confirmar a implantação e o teste de código em ambientes de preparo e produção ([Leia mais](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/staging-and-production){target="_blank"}).
6. O cluster de produção foi aumentado permanentemente para a linha de base diária contratada. Fale com o CTA/CSE atribuído para obter mais detalhes ou gere um tíquete de suporte.

## 2. Configurações atuais

1. Atualize o Adobe Commerce e pacotes/serviços relacionados para o [versão mais recente](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Analisar as configurações e os serviços atuais com seu SI/parceiro e [seguir as práticas recomendadas](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Revise o MySQL/Arquivos compartilhados [uso do disco](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/storage/manage-disk-space){target="_blank"}

## 3. Configurações do Fastly

1. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}[Cache de página inteira](https://developer.adobe.com/commerce/frontend-core/guide/caching/){target="_blank"} or [GraphQL caching](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Read the [Fastly set up guide](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly){target="_blank"}.
2. Use o método GET para consultas do GraphQL em sites PWA/Headless, quando aplicável.

   >[!NOTE]
   > Somente as consultas enviadas com uma operação HTTP GET podem ser armazenadas em cache (se aplicável). [as consultas de POST não podem ser armazenadas em cache](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Certifique-se de que a Otimização de imagem do Fastly esteja ativada ([Consulte Otimização rápida de imagens](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Verifique se o local correto da blindagem está configurado ([Configurar cache, back-end e blindagem de origem](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Firewall de Aplicativo Web (**WAF**) está funcionando. (Consulte [Solução de problemas de solicitações bloqueadas](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/fastly-waf-service){target="_blank"}, se houver, e limitações)
6. Atualizar o Fastly [&quot;Parâmetros de URL ignorados&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} no painel de administração para aprimorar o desempenho do cache.

   >[!NOTE]
   > Na configuração do Fastly em _Admin > Lojas > Configurações > Sistema > Cache de página inteira > Configuração rápida > Configuração avançada > Parâmetros de URL ignorados (Global)_, você pode encontrar uma lista de parâmetros separada por vírgulas que o Fastly deve ignorar ao pesquisar por páginas em cache. Certifique-se de recarregar o VCL depois de modificar esta lista

## 4. DNS e SSL

1. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}_(Envie um tíquete de suporte com antecedência para qualquer domínio adicionado ou alterado)_
2. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}[este artigo](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} para obter mais informações.
3. Atualizar DNS [TTL (Tempo de vida útil)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist#to-update-dns-configuration-for-site-launch){target="_blank"} para o mínimo possível, para a ativação.
4. Ativar o Sendgrid SPF e o DKIM

   >[!NOTE]
   > Adicione os registros CNAME do SendGrid de cada domínio à configuração do DNS. Ler [Serviço de email SendGrid](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"} para ver como alterar os domínios de remetente e muito mais.

## 5. Configurações de banco de dados

A Adobe Commerce Cloud emprega um cluster MariaDB Galera como banco de dados para os ambientes de preparo e produção. Os clusters Galera são fundamentais para melhorar o desempenho e a escalabilidade. Para obter insights sobre as práticas e restrições ideais das replicações de clusters Galera, consulte os artigos a seguir.

- [Práticas recomendadas de configurações do MySQL](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
- Alertas gerenciados no Adobe Commerce: [Alertas do MariaDB](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
- Práticas recomendadas para [configuração do banco de dados](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
- Análise profunda para [Replicação de clusters de galera e controle de fluxo.](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/backend-development/galera-db-slow-replication){target="_blank"}

1. [Conexão subordinada do MYSQL](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} O é recomendado para melhorar o desempenho durante cargas altas de banco de dados.
2. Verifique se o formato da linha de todas as tabelas do banco de dados está definido como [DINÂMICO em vez de COMPACTO](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} (Isso é especialmente verdadeiro para migrações no local para a nuvem).
3. Alterar o mecanismo de armazenamento do banco de dados de [MyISAM para InnoDB](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} para todas as tabelas.
4. Analise e otimize com bastante antecedência as tabelas de bancos de dados que excedam 1 GB.
5. As informações do esquema do banco de dados estão atuais e atualizadas. (Consulte [este guia](https://mariadb.com/kb/en/engine-independent-table-statistics/#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## 6. Implantações

1. Revise o estado ideal da Implantação de conteúdo estático (SCD) para reduzir o tempo de manutenção durante implantações no ambiente de produção. Revisão [Estratégias de implantação de conteúdo estático (SCD)](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/static-content){target="_blank"} and [Store configuration management](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/store-settings){target="_blank"} guia.
2. Revise as configurações de minificação para HTML, JavaScript e CSS. (Isso não se aplica aos sites PWA/Headless).
3. Confirme se a utilização das variáveis de nuvem a seguir está alinhada às finalidades pretendidas. ([SCD_MATRIX](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} and [SKIP_SCD](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## 7. Teste e solução de problemas

1. Teste os emails transacionais de saída. Leia mais sobre [Adobe Commerce Cloud - Funcionalidade SendGrid Mail](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}
3. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}

   >[!NOTE]
   > A [testes de carga e tensão servem o propósito](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} identificar gargalos e descobrir problemas de desempenho no aplicativo. Ele desempenha um papel crucial no gerenciamento das expectativas em relação ao tamanho do cluster e na determinação dos ajustes de dimensionamento necessários para atender aos requisitos de negócios de maneira eficaz.

   >[!IMPORTANT]
   > **_AVISO:_** Ao preparar um teste de carga, por favor_ **_não_** enviar emails de transação em tempo real (até mesmo para endereços fictícios). Enviar emails durante o teste pode fazer com que o projeto atinja o limite de envio padrão (12k) configurado para o SendGrid antes do lançamento.
   > 
   > - Como desativar a comunicação por email:
   >   Ir para _Armazenamento > Configuração > Avançado > Sistema > Configurações de envio de email_.

4. Realizar testes de penetração de segurança na instância de produção como parte da [modelo de segurança de responsabilidade compartilhada](https://business.adobe.com/products/magento/secure-ecommerce.html){target="_blank"}. Para conformidade com PCI (Payment Card Industry, setor de cartões de pagamento), o site personalizado requer teste de penetração.

## 8. Outras configurações

1. Alternar indexação para _&quot;atualização programada_&quot;, exceto o **_customer_grid_** que permanece em &quot;SALVAR&quot; (consulte [Modos de indexação](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Você está usando mecanismos de pesquisa ou extensões de terceiros?
3. Confirme que [As configurações de SEO (Otimização do mecanismo de pesquisa) estão configuradas corretamente](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} para permitir que indexadores/crawlers verifiquem o site, se relevante.
4. Adicionar redirecionamentos e rotas (consulte [Configurar rotas](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   >Adicione redirecionamentos e rotas ao arquivo route.yaml no ambiente de Integração e verifique a configuração nesse ambiente antes de implantar em Preparo e Produção.

       &quot;http://{all}/&quot;:
       tipo: upstream
       upstream: &quot;mymagento:http&quot;
       
       &quot;http://{all}/&quot;:
       tipo: upstream
       upstream: &quot;mymagento:http&quot;
   
5. Verifique se o XDebug está desativado, se estiver ativado durante o desenvolvimento (consulte [Configurar Xdebug](https://developer.adobe.com/commerce/cloud-tools/docker/test/configure-xdebug/){target="_blank"}).
6. Verifique se o op-cache e outras configurações foram atualizadas com precisão no arquivo php.ini ([consulte esta amostra](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Assine a [**Página de status do Adobe Commerce**](https://status.adobe.com/cloud/experience_cloud#/){target="_blank"}.
8. Assinar o New Relic &quot;[Alertas gerenciados para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-for-magento-commerce){target="_blank"}" notification channels to monitor the given performance metrics ([read more](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## 9. Segurança

1. Configurar a verificação de segurança do Adobe Commerce

   >[!NOTE]
   > [O Adobe Commerce Security Scan é uma ferramenta útil](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-scan){target="_blank"} que ajuda a descobrir versões de software desatualizadas, configurações incorretas e possíveis malwares no site. Inscreva-se, programe-o para ser executado com frequência e certifique-se de que os emails sejam enviados ao contato de segurança técnica correto.
   > 
   > Conclua esta tarefa durante UAT. Se você usar a opção de varreduras periódicas, certifique-se de programar as varreduras em momentos de baixa demanda. Consulte a [Verificação de segurança](https://account.magento.com/scanner/index/dashboard/){target="_blank"} página na conta do Adobe Commerce. É necessário fazer logon em uma conta da Adobe Commerce para acessar a Verificação de segurança.

2. Altere as configurações padrão para o Administrador do Adobe Commerce.
3. Altere a senha do administrador (consulte [Configuração da segurança do administrador](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Alterar o URL do administrador (consulte [Uso de um URL de administração personalizado](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Remova os usuários que não estão mais no projeto (consulte [Criar e gerenciar usuários](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access){target="_blank"}).
6. As senhas para administradores são configuradas (consulte [Requisitos de senha de administrador](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Configure a autenticação de dois fatores (consulte [Autenticação de dois fatores](https://developer.adobe.com/commerce/testing/functional-testing-framework/two-factor-authentication/){target="_blank"}).

## 10. Ativar

Quando chegar o momento da transferência, execute as seguintes etapas (para obter mais informações, consulte [Configurações de DNS](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}):

1. Acesse o serviço DNS e atualize os registros A e CNAME para cada um dos domínios e nomes de host:
   1. Adicionar um registro CNAME para _&lt;&lt;www.yourdomain.com>>_, apontando para **prod.magentocloud.map.fastly.net**
   2. Estabeleça quatro registros A para _&lt;&lt;yourdomain.com>>_, indicando:\
      151.101.1.124\
      151.101.65.124\
      151.101.129.124\
      151.101.193.124
2. Alterar o URL de base do Adobe Commerce para _&lt;&lt;www.yourdomain.com>>_
3. Aguarde o tempo de TTL passar e reinicie o navegador da Web.
4. Teste o site.

### Se você tiver um problema bloqueando a ativação:

Se você encontrar problemas que o impeçam de iniciar durante a transferência, o método mais rápido para obter suporte adequado e em tempo hábil é utilizar o suporte técnico e abrir um tíquete com o motivo &quot;Não é possível iniciar minha loja&quot; e ligar para um número de suporte de linha direta (consulte [a lista de números de linha direta Adobe Commerce P1 (Prioridade 1)](https://support.magento.com/hc/en-us/articles/360042536151){target="_blank"}):

- Chamada Gratuita dos EUA: (+1) 877 282 7436 (direto para a linha direta Adobe Commerce P1)
- Chamada Gratuita dos EUA: (+1) 800 685 3620 (No primeiro menu, pressione 7 para obter a linha direta Adobe Commerce P1)
- Local EUA: (+1) 408 537 8777

## 11. Pós-ativação

Quando o site estiver ativo, envie um email para o CTA (Customer Technical Advisory, Consultoria técnica do cliente), o CSE (Customer Success Engineer, Engenheiro de sucesso do cliente) e o AM (Account Manager, Gerente de conta) atribuídos. No entanto, se você não tiver um gerente de conta atribuído ao projeto, poderá criar um tíquete de suporte solicitando que o monitoramento de Alto SLA seja ativado depois que o site for ativado. O CTA/CSE executa as seguintes tarefas assim que o site é verificado para ser iniciado com o Fastly ativado e o armazenamento em cache:

- Marque o cluster como ativo e crie um tíquete de suporte para ativar o monitoramento de SLAs (Contratos de nível de serviço) altos.
- Ativar verificações PKingdom para monitoramento do tempo de atividade.

>[!MORELIKETHIS]
> 
> - [Visão geral da prontidão do Launch - Manual de implementação](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/launch/overview){target="_blank"}
> - [Lista de verificação do Launch - Guia do usuário](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/launch/checklist){target="_blank"}
> - [Lista de verificação do Pré-lançamento - Guia do administrador do Gerenciador de sites/Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> - [Modelo de segurança de responsabilidade compartilhada](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}
