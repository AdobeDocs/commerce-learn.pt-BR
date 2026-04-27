---
title: Lista de verificação de pré-lançamento do Adobe Commerce Cloud
description: Saiba mais sobre a lista de verificação de pré-lançamento da Adobe Commerce Cloud e como trabalhá-la com seu integrador antes da ativação.
feature: Cloud
topic: Commerce, Architecture, Development
role: Admin, Developer, User
level: Intermediate
doc-type: Tutorial
duration: 451
last-substantial-update: 2024-04-17T00:00:00.000Z
jira: KT-15180
exl-id: c6adb2c2-f194-4a3d-9290-e0837ef062ae
TQID: https://experienceleague.adobe.com/czbb8zkX55fzgKiZthAj4whBCF-IL2bEox0M7rDr9oE
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: b599f79ad41b9552cea6ff41062eb4ef75f183bb
workflow-type: tm+mt
source-wordcount: 2365
ht-degree: 0%

---

# Lista de verificação de pré-lançamento

Esta página resume a [Documentação de inicialização do site](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/launch/overview){target="_blank"} do Adobe Commerce.

Essa lista de verificação tem como objetivo ajudar no planejamento e na execução de um lançamento bem-sucedido do site da Adobe Commerce Cloud. Colabore com o integrador de sistemas da Adobe Commerce Cloud para garantir que todas as tarefas de configuração e itens da lista de verificação sejam concluídos e verificados. Se encontrar dificuldades com algum item da lista de verificação ou tiver dúvidas, entre em contato com o Consultor técnico ou engenheiro de sucesso do cliente designado. Se sua conta não tiver um CTA/CSE atribuído, você poderá criar um tíquete de suporte para obter assistência.

Se você tiver um CTA/CSE atribuído à conta, entre em contato com ele e com o Gerente de conta pelo menos 4 semanas antes de iniciar o novo site da Adobe Commerce Cloud para notificá-lo de sua **intenção** de iniciar o.

* Algumas verificações são destacadas com [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"}, pois elas podem bloquear sua ativação, se não forem revisadas com cuidado.
* Colabore com seu desenvolvedor ou parceiro de integração de sistema para que sua abordagem de implementação permaneça alinhada.

>[!IMPORTANT]
> Você aceita a [responsabilidade](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"} por quaisquer efeitos adversos e riscos associados ao cronograma de lançamento da produção e à estabilidade contínua do site, se não conseguir usar e concluir esta lista de verificação.

## &#x200B;1. Pré-ativação

1. Revise a documentação sobre testes e ativação da [Documentação de inicialização do site](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/launch/overview){target="_blank"}

   >[!NOTE]
   >Certifique-se de que um _&quot;plano de preparação para ativação&quot;_ abrangente esteja totalmente preparado com seu parceiro ou integrador de sistema, incorporando todos os itens de ação necessários. Lembre-se, embora a lista de verificação de pré-lançamento enfatize as práticas recomendadas da Adobe, ela _&#x200B;**não**&#x200B;_ substitui a necessidade de seu próprio plano de preparação para ativação.

2. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} Revise as Recomendações e as Informações do SWAT (Support Insights) ([Guia do Usuário](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/site-wide-analysis-tool/intro){target="_blank"})
3. Confirmar se usuários finais e comerciantes concluíram o UAT (User Acceptance Testing, teste de aceitação do usuário), incluindo operações de backend.
4. Confirme se a equipe do integrador de sistemas executou UAT completo no preparo e na produção. Consulte a [Documentação do Experience League](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/test/staging-and-production){target="_blank"}.
5. Confirme a implantação e o teste de código em ambientes de preparo e produção ([Leia mais](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/test/staging-and-production){target="_blank"}).
6. Confirme se o cluster de produção foi redimensionado permanentemente para a linha de base diária contratada. Fale com o CTA/CSE atribuído para obter mais detalhes ou gere um tíquete de suporte.

## &#x200B;2. Configurações atuais

1. Atualize o Adobe Commerce e os pacotes/serviços relacionados para a [última versão](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/notes/overview){target="_blank"}
2. Revise as configurações e os serviços atuais com seu SI/parceiro, e [siga as práticas recomendadas](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/planning/catalog-management){target="_blank"}.
3. Revise o MySQL/Arquivos compartilhados [uso do disco](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/storage/manage-disk-space){target="_blank"}

## &#x200B;3. Configurações do Fastly

1. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} Verifique se o cache está funcionando ([Cache de Página Inteira](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/cache-management){target="_blank"} ou [cache do GraphQL](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}). Leia o [Guia de configuração do Fastly](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/fastly){target="_blank"}.
2. Use o método do GET para consultas do GraphQL em sites do PWA/Headless, quando aplicável.

   >[!NOTE]
   > Somente as consultas enviadas com uma operação HTTP GET podem ser armazenadas em cache (se aplicável). [Não é possível armazenar consultas POST em cache](https://developer.adobe.com/commerce/webapi/graphql/usage/caching/){target="_blank"}.

3. Certifique-se de que a Otimização de imagem do Fastly esteja habilitada ([Consulte Otimização de Imagem do Fastly](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/fastly-image-optimization){target="_blank"})
4. Verifique se o local de blindagem correto está configurado ([Configurar cache, infraestruturas e blindagem de origem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/setup-fastly/fastly-custom-cache-configuration){target="_blank"}).
5. Confirme se o Firewall do Aplicativo Web (**WAF**) está funcionando. (Consulte [Solução de problemas de solicitações bloqueadas](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/fastly-waf-service){target="_blank"}, se houver, e limitações.)
6. Atualize a lista Fastly [&quot;Parâmetros de URL ignorados&quot;](https://github.com/iancassidyweb/magento2/commit/68fdecfcd26c957382b8d68b64887e0a83298524){target="_blank"} no painel de administração para aprimorar o desempenho do cache.

   >[!NOTE]
   > Na configuração do Fastly em _Admin > Lojas > Configurações > Sistema > Cache de Página Inteira > Configuração do Fastly > Configuração Avançada > Parâmetros de URL Ignorados (Global)_, você pode encontrar uma lista de parâmetros separados por vírgulas que o Fastly deve ignorar ao pesquisar por páginas em cache. Recarregue o VCL depois de modificar essa lista.

## &#x200B;4. DNS e SSL

1. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} Confirme se todos os nomes de domínio necessários foram solicitados. _(Envie um tíquete de suporte com antecedência para qualquer domínio adicionado ou alterado.)_
2. O certificado SSL (TLS) [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} foi aplicado ao(s) domínio(s). Leia [este artigo](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/how-to/ssl-tls-certificates-for-magento-commerce-cloud-faq){target="_blank"} para obter mais informações.
3. Atualize o valor DNS [TTL (Time to Live)](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"} com o mínimo possível para a ativação.
4. Ative o SendGrid SPF e o DKIM.

   >[!NOTE]
   > Adicione os registros CNAME do SendGrid de cada domínio à configuração do DNS. Leia o [serviço de email SendGrid](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/sendgrid){target="_blank"} para ver como alterar os domínios de remetente e muito mais.

## &#x200B;5. Configurações do banco de dados

A Adobe Commerce Cloud emprega um cluster MariaDB Galera como banco de dados para os ambientes de preparo e produção. Os clusters Galera são fundamentais para melhorar o desempenho e a escalabilidade. Para obter insights sobre as práticas e restrições ideais das replicações de clusters Galera, consulte os artigos a seguir.

* [Práticas recomendadas de configurações do MySQL](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration){target="_blank"}
* Alertas gerenciados no Adobe Commerce: [alertas do MariaDB](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-on-magento-commerce-mariadb-alerts){target="_blank"}
* Práticas recomendadas para [configuração de banco de dados](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud){target="_blank"}
* [Replicação de cluster de galera e controle de fluxo](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/extensibility/backend-development/galera-db-slow-replication){target="_blank"} (análise mais profunda)

1. [Conexão subordinada do MySQL](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/planning/mysql-configuration#slave-connections){target="_blank"} recomendada para melhor desempenho durante cargas altas de banco de dados.
2. Verifique se o formato de linha de todas as tabelas do banco de dados está definido como [DYNAMIC em vez de COMPACT](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/maintenance/mariadb-upgrade#convert-database-table-storage-format){target="_blank"} (isso é especialmente verdadeiro para migrações no local para a nuvem).
3. Altere o mecanismo de armazenamento do banco de dados de [MyISAM para InnoDB](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/planning/database-on-cloud#convert-all-myisam-tables-to-innodb){target="_blank"} para todas as tabelas.
4. Revise e otimize as tabelas do banco de dados que excedem 1 GB de tamanho com bastante antecedência.
5. As informações do esquema do banco de dados estão atuais e atualizadas. (Consulte [este guia](https://mariadb.com/docs/server/ha-and-performance/optimization-and-tuning/query-optimizations/statistics-for-optimizing-queries/engine-independent-table-statistics#collecting-statistics-with-the-analyze-table-statement){target="_blank"}).

## &#x200B;6. Implantações

1. Revise o estado ideal da Implantação de conteúdo estático (SCD) para reduzir o tempo de manutenção durante implantações no ambiente de produção. Revise o guia [Estratégias de implantação de conteúdo estático](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/deploy/static-content){target="_blank"} e [Gerenciamento de configuração de repositório](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure-store/store-settings){target="_blank"}.
2. Revise as configurações de minificação para HTML, JavaScript e CSS. (Isso não se aplica a sites do PWA/Headless).
3. Confirme se a utilização das variáveis de nuvem a seguir está alinhada às finalidades pretendidas. ([SCD_MATRIX](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-build#scd_matrix){target="_blank"}, [SCD_ON_DEMAND](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-global#scd_on_demand){target="_blank"} e [SKIP_SCD](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/env/stage/variables-deploy#skip_scd){target="_blank"})

## &#x200B;7. Teste e solução de problemas

1. Teste os emails transacionais de saída. Leia mais sobre [Adobe Commerce Cloud - Funcionalidade SendGrid Mail](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/sendgrid){target="_blank"}.
2. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} Confirme se não há bloqueadores relacionados à Adobe a serem iniciados.
3. [!BADGE Bloqueador]{type=caution tooltip="Bloqueador potencial"} Execute testes de carga e tensão na instância de Produção antes de entrar em funcionamento e compartilhar resultados com o CTA/CSE atribuído.

   >[!NOTE]
   > Um [teste de carga e estresse serve o objetivo](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/test/guidance#:~:text=A%20load%20test%20can%20help,Scan%20Tool%20for%20your%20sites.){target="_blank"} de identificar gargalos e descobrir problemas de desempenho no aplicativo. Ele desempenha um papel crucial no gerenciamento das expectativas em relação ao tamanho do cluster e na determinação dos ajustes de dimensionamento necessários para atender aos requisitos de negócios de maneira eficaz.

   >[!IMPORTANT]
   > **_WARNING:_** Ao preparar um teste de carga, **não** envia emails de transações ativas (mesmo para endereços fictícios). Enviar emails durante o teste pode fazer com que o projeto atinja o limite de envio padrão (12k) configurado para o SendGrid antes do lançamento.
   > 
   > * Como desativar a comunicação por email:
   >   Vá para _Armazenamento > Configuração > Avançado > Sistema > Configurações de Envio de Email_.

4. Realizar testes de inserção de segurança na instância de produção como parte do [modelo de segurança de responsabilidade compartilhada](https://business.adobe.com/br/products/commerce.html){target="_blank"}. Para conformidade com PCI (Payment Card Industry, setor de cartões de pagamento), o site personalizado requer teste de penetração.

## &#x200B;8. Outras configurações

1. Alternar a indexação para _&quot;atualização na agenda_&quot;, exceto a **_grade_cliente_**, que permanece em &quot;SALVAR&quot; (consulte [Modos de indexação](https://developer.adobe.com/commerce/php/development/components/indexing/#indexing-modes){target="_blank"}).
2. Documente todos os mecanismos de pesquisa ou extensões de terceiros em uso.
3. Confirme se as configurações de [SEO (Otimização do Mecanismo de Pesquisa) estão configuradas corretamente](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/seo/seo-overview){target="_blank"} para permitir que indexadores/rastreadores verifiquem o site, se relevante.
4. Adicionar redirecionamentos e rotas (consulte [Configurar rotas](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure/routes/routes-yaml){target="_blank"})

   >[!NOTE]
   > Adicione redirecionamentos e rotas ao arquivo route.yaml no ambiente de Integração e verifique a configuração nesse ambiente antes de implantar em Preparo e Produção.

   Exemplo do fragmento `routes.yaml`:

   ```yaml
           "http://{all}/":
               type: upstream
               upstream: "mymagento:http"
   
           "http://{all}/":
               type: upstream
               upstream: "mymagento:http"
   ```

5. Verifique se o Xdebug está desabilitado caso tenha sido habilitado durante o desenvolvimento (consulte [Configurar Xdebug para Commerce na Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/test/debug){target="_blank"}).
6. Verifique se o OPcache e outras configurações foram atualizados com precisão no arquivo php.ini ([consulte esta amostra](https://github.com/magento/magento-cloud/blob/master/php.ini#L41){target="_blank"}).
7. Assine a [**página de status do Adobe Commerce**](https://status.adobe.com/pt-br/cloud/experience_cloud#/){target="_blank"}.
8. Inscreva-se nos canais de notificação &quot;[Alertas Gerenciados do New Relic para Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/managed-alerts-for-adobe-commerce/managed-alerts-for-magento-commerce){target="_blank"}&quot; para monitorar as métricas de desempenho fornecidas ([leia mais](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/monitor/new-relic/new-relic-service){target="_blank"}).

## &#x200B;9. Segurança

1. Configure a Verificação de segurança do Adobe Commerce.

   >[!NOTE]
   > [O Adobe Commerce Security Scan é uma ferramenta útil](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security-scan){target="_blank"} que ajuda a descobrir versões de software desatualizadas, configurações incorretas e malware em potencial no site. Inscreva-se, programe-o para ser executado com frequência e certifique-se de que os emails sejam enviados ao contato de segurança técnica correto.
   > 
   > Conclua esta tarefa durante UAT. Se você usar a opção de varreduras periódicas, certifique-se de programar as varreduras em momentos de baixa demanda. Depois de entrar na sua conta da Adobe Commerce, abra a ferramenta Verificação de Segurança na sua conta (consulte [Verificação de segurança](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security-scan){target="_blank"} para acesso e uso).

2. Altere as configurações padrão para o Administrador do Adobe Commerce.
3. Altere a senha do administrador (consulte [Configurando a Segurança do Administrador](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
4. Alterar a URL do administrador (consulte [Usando uma URL de Administrador personalizada](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/site-store/store-urls#use-a-custom-admin-url){target="_blank"}).
5. Remova os usuários que não estão mais no projeto (consulte [Criar e gerenciar usuários](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/user-access){target="_blank"}).
6. Confirme se as senhas do administrador atendem aos requisitos (consulte [Requisitos de Senha do Administrador](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security-admin){target="_blank"}).
7. Configure a autenticação de dois fatores (consulte [Autenticação de dois fatores (Admin)](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security-admin#two-factor-authentication){target="_blank"}).

## 10. Go Live

Quando for a hora de transferir, execute as seguintes etapas (para obter mais informações, consulte [Configurações de DNS](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"}):

1. Acesse o serviço DNS e atualize os registros A e CNAME para cada um dos domínios e nomes de host:
   1. Adicione um registro CNAME para _&lt;&lt;www.yourdomain.com>_, apontando para **prod.magentocloud.map.fastly.net**
   2. Set four A records for _&lt;&lt;yourdomain.com>>_, pointing at:\
      151.101.1.124\
      151.101.65.124\
      151.101.129.124\
      151.101.193.124
2. Change the Adobe Commerce Base URL to _&lt;&lt;www.yourdomain.com>>_
3. Wait for the TTL time to pass, then restart the web browser.
4. Test the website.

### If you have an issue blocking the go-live:

If you encounter any problems preventing you from launching during the cutover, the fastest way to get timely support is to use the help desk and open a ticket with the reason &quot;Unable to launch my store&quot;, and call a hotline support number (see [Adobe Commerce P1 notification hotline](https://experienceleague.adobe.com/pt-br/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-p1-notification-hotline){target="_blank"} for current numbers and procedures):

* US Toll Free: (+1) 877 282 7436 (direct to Adobe Commerce P1 hotline)
* US Toll Free: (+1) 800 685 3620 (At first menu, press 7 for Adobe Commerce P1 hotline)
* US Local: (+1) 408 537 8777

## &#x200B;11. Pós-ativação

Once the site is live, email the assigned CTA (Customer Technical Advisor), CSE (Customer Success Engineer), and AM (Account Manager). However, if you do not have an account manager assigned to the project, you can create a support ticket asking for High SLA monitoring to be enabled once the site has gone live. The CTA/CSE performs the following tasks as soon as the site is verified to be launched with Fastly enabled and caching:

* Tag the cluster as live and create a support ticket to activate High SLA (Service Level Agreements) monitoring.
* Activate New Relic Synthetics for uptime monitoring.

>[!MORELIKETHIS]
> 
> * [Launch Readiness Overview - Implementation Playbook](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/best-practices/launch/overview){target="_blank"}
> * [Launch Checklist - User Guide](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/launch/checklist){target="_blank"}
> * [Prelaunch Checklist - Site Manager/Commerce Admin&#39;s Guide](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/start/setup/prelaunch-checklist){target="_blank"}
> * [Shared responsibility security model](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/security-and-compliance/shared-responsibility){target="_blank"}
