---
title: Execução a seco do Adobe Commerce Developer Agent App Builder
description: Saiba como criar, implantar e testar três casos de uso de extensibilidade do Commerce com o Adobe Commerce Developer Agent nesta simulação prática do App Builder.
feature: Extensibility, App Builder, Eventing, Configuration
topic: App Builder, Development, Integrations
role: Developer
level: Intermediate
doc-type: Tutorial
duration: 438
last-substantial-update: 2026-08-28T00:00:00Z
source-git-commit: 6ce75fe023cfb9c3be988787e8993db556cf3150
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---

# Execução a seco do Adobe Commerce Developer Agent App Builder

Uma apresentação prática para criar, implantar e testar casos de uso de extensibilidade do Commerce com o Adobe Commerce Developer Agent (CDA). Essa simulação abrange três casos de uso: um webhook de limite de quantidade do carrinho, uma retenção de pedido de alto valor e arquivamento orientado por eventos para pedidos suspensos, desde o blueprint até o teste funcional.

## Introdução

### Como relatar problemas e feedback

Durante todo o período de seca, você encontra bordas ásperas — o que é esperado ao trabalhar com um novo recurso. Capture e compartilhe quaisquer problemas com o contato do programa do Adobe usando o modelo de feedback fornecido durante a integração.

>[!TIP]
>
> Ao relatar um problema:
>
> * Inclua o `projectId` (visível na URL do navegador).
> * Inclua capturas de tela sempre que relevante.

### Pré-requisitos

**Contas e acesso**

* Pelo menos a função **Desenvolvedor** em sua Organização de IMS de Acesso Antecipado.
* Acesso de administrador a uma instância do Adobe Commerce as a Cloud Service (ACCS) nessa organização, disponível em experience.adobe.com em **Instâncias do Cloud Service**.
* Uma conta do GitHub.

**Ferramentas**

Uma loja Edge Delivery Services (EDS) é necessária para a validação funcional. Você precisará de:

* Node.js 22+
* CLI DO Adobe I/O: `npm install -g @adobe/aio-cli`
* Plug-in AIO CLI Commerce: `aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce`

Instale a placa-mãe da loja em uma pasta vazia, selecionando a instância ACCS quando solicitado:

```bash
aio commerce extensibility app-setup -s aem-boilerplate-commerce -n storefront
```

Iniciar a loja:

```bash
cd storefront
npm run start
```

## Abrir o Commerce Developer Agent

1. Navegue até o Commerce Developer Agent em experience.adobe.com, em **Developer Agent**.
1. Faça logon usando suas credenciais da Organização IMS de acesso antecipado.

## Caso de uso 1: webhook de unidades máximas do carrinho

Esse caso de uso valida os limites de quantidade do carrinho antes que um produto seja adicionado, usando um webhook síncrono do Commerce.

### Estágio de blueprint

Digite o prompt a seguir e clique em **Gerar blueprint**:

```text
Add a validation webhook that runs before a product is added to the cart.

Use the Commerce webhook method observer.sales_quote_item_save_before (type before) — do not use
observer.checkout_cart_product_add_before, observer.sales_quote_add_item, or any other event.

Calculate the total by summing all quote line quantities and the quantity of the current item.
If the same SKU already exists in the quote, exclude its existing quantity to avoid double-counting.

If the total is greater than the maximum allowed, block the add and show:
"You have reached the maximum amount of items."

The maximum allowed must be configurable in Commerce Admin as max_cart_units, with default 10.

Map payload fields using name and source properties:
- name: item.qty, source: data.item.qty
- name: item.sku, source: data.item.sku
- name: quote, source: context_checkout_session.get_quote[items.qty,items.sku]

Set required: true and fallback_error_message: "You have reached the maximum amount of items."
on the webhook config.

When blocking the add, do not use exceptionOperation, because it serializes exceptionClass as class.
Instead, manually return an exception operation response whose body includes type:
{
  "op": "exception",
  "message": "You have reached the maximum amount of items.",
  "type": "\\Magento\\Framework\\GraphQl\\Exception\\GraphQlInputException"
}
```

>[!NOTE]
>
> Procure estas coisas:
>
> * Um blueprint (v1) que captura os requisitos é criado.
> * São criadas tarefas para orientar a implementação.

Refine o blueprint inserindo detalhes na caixa de chat ou clicando em uma das pílulas acima da caixa de chat (*Desafiar hipóteses*, *Localizar lacunas de design* etc.). Quando estiver satisfeito, clique em **Aprovar plano** para prosseguir.

### Estágio de desenvolvimento

O agente faz a transição para o estágio Desenvolver e começa a provisionar o espaço de trabalho.

>[!NOTE]
>
> Procure esses arquivos no painel Explorer:
>
> * `app.commerce.config.ts`
> * `app.config.yaml`
> * `install.yaml`
> * `package-lock.json`
> * `package.json`

Depois de provisionado, o agente mostra uma lista de tarefas de implementação e começa a criar.

>[!NOTE]
>
> Procure estas coisas:
>
> * O código gerado corresponde aos requisitos.
> * A tela de streaming `Validate` mostra o progresso na validação do espaço de trabalho (`aio app build`).
> * O agente corrige automaticamente o código gerado se a validação falhar.

Depois de satisfeito com o código, clique na guia **Integrações** para avançar.

### Configurar integrações

**Conectar ou criar um espaço de trabalho do App Builder**

Para criar ou conectar um projeto do App Builder, siga as instruções na tela.

Se estiver se conectando a um espaço de trabalho existente, verifique se ele tem:

* O serviço `Runtime` foi adicionado.
* As seguintes APIs foram adicionadas: Adobe Commerce as a Cloud Service, API de gerenciamento de E/S, App Builder Data Services, Eventos de E/S, Adobe I/O Events para Adobe Commerce.

Ao criar um novo espaço de trabalho, adicione manualmente a API do **Adobe Commerce as a Cloud Service**.

>[!IMPORTANT]
>
> Depois de conectado a um projeto App Builder existente, expanda **Configuração Avançada** e cole o JSON do espaço de trabalho e clique em **Verificar novamente o status** para confirmar se todas as APIs necessárias estão instaladas.

Clique em **Avançar** para continuar.

**Conectar-se ao Commerce**

Selecione a instância do ACCS na lista ou insira a URL no campo **URL da Base REST do Commerce** e clique em **Conectar instância do Commerce**. Clique em **Avançar** para continuar.

**Conectar-se ao GitHub**

Conecte o espaço de trabalho a um repositório GitHub inserindo o URL do repositório e usando o aplicativo GitHub ou um token de acesso pessoal. Clique em **Avançar** para continuar.

**Configurar variáveis de ambiente**

Preencha todas as variáveis de ambiente exigidas pelo projeto.

### Implantar

Clique em **Desenvolver** para retornar ao estágio de desenvolvimento e solicitar que o agente implante no campo de prompt.

>[!NOTE]
>
> Procure uma mensagem &quot;Confirmar implantação&quot; mostrando a Organização, o Projeto, o Workspace e o namespace do Tempo de execução.

Confirme a implantação.

>[!NOTE]
>
> Procure por:
>
> * A tela de transmissão `Validate` mostrando o progresso da validação pré-implantação.
> * O agente corrigirá automaticamente o código se a validação falhar.
> * A tela de streaming `Deploy` mostrando o progresso da implantação (`aio app deploy`).
> * O agente fará a autocorreção do código se a implantação falhar.

### Associar o aplicativo no Gerenciamento de aplicativos

1. Navegue até o URL do administrador da instância do ACCS e faça logon.
1. Selecione **Aplicativos** no menu à esquerda e depois **Gerenciamento de Aplicativos**.
1. Clique em **+ Associar aplicativo** (canto superior direito).
1. Selecione o Projeto e a Workspace nos quais o CDA implantou e clique em **Associar**.

>[!NOTE]
>
> Procure um cartão que mostre o nome e a versão do aplicativo, bem como os recursos implementados (Configuração comercial, Webhooks, Eventos etc.).

### Instalar e configurar no Gerenciamento de aplicativos

1. Na linha do aplicativo, clique em **Instalar** e em **Fechar**.
1. Na mesma linha, clique em **Configurar** para preencher os valores de configuração comercial e em **Fechar**.

>[!NOTE]
>
> Procure um formulário mostrando cada campo de configuração especificado pelo blueprint, pré-preenchido com os padrões especificados.

### Teste funcional

1. Na configuração do aplicativo Gerenciamento de aplicativos, defina **Máximo de unidades do carrinho** como 3 (um valor baixo para um teste rápido).
1. Na loja, comece com um carrinho vazio.
1. Adicione produtos da Página de detalhes do produto (PDP) até que a quantidade total exceda 3 — a última adição falhará.
1. No PDP, você vê: *&quot;Você atingiu a quantidade máxima de itens.&quot;*
1. Abaixo do limite, as adições ainda têm êxito.

>[!NOTE]
>
> Na Página de listagem de produtos (PLP), uma adição bloqueada falha silenciosamente sem mensagem; esse é um comportamento de vitrine, não uma falha de webhook. Prefira o PDP para verificação.

## Caso de uso 2: retenção de ordem de alto valor e código de verificação

Volte para o estágio **Blueprint** para iniciar este caso de uso.

### Estágio de blueprint

Digite o prompt a seguir e clique em **Gerar blueprint**:

```text
Add a Commerce event priority subscription to `plugin.sales.api.order_management.place`.

Extract `entity_id` and `grand_total` from the Commerce event payload using event `fields` in `app.commerce.config.ts`.

Important: the runtime action receives a CloudEvents-shaped payload. For Commerce eventing extracted fields,
parse them from `params.data.value`, not directly from `params.data`. The handler must use:
- `params.data.value.entity_id`
- `params.data.value.grand_total`

When `grand_total` is greater than `order_hold_threshold`:
1. Generate a verification code locally.
2. Put the order on hold with state and status `holded`.
When putting the order on hold, save the verification code using `custom_attributes`, not `extension_attributes`.
The Commerce `POST V1/orders` payload should include:
{
  "entity": {
    "entity_id": <entity_id>,
    "state": "holded",
    "status": "holded",
    "custom_attributes": [
      {
        "attribute_code": "<hold_verification_attribute>",
        "value": "<verification_code>"
      }
    ]
  }
}
3. Save the verification code via a `POST V1/orders` Commerce REST API call.

Make these configurable in Commerce Admin:
- `order_hold_threshold`, default `500`
- `hold_verification_attribute`, default `lab_verification_code`

Validate inputs before use:
- `entity_id` must be a positive integer.
- `grand_total` must be a non-negative number.
```

>[!NOTE]
>
> Procure estas coisas:
>
> * Um blueprint (v2) que captura os requisitos é criado.
> * As tarefas do plano original são retidas.
> * Novas tarefas correspondentes aos novos requisitos foram adicionadas.

Refine o blueprint conforme necessário, em seguida, clique em **Aprovar plano** para prosseguir.

### Desenvolver, implantar, associar e instalar

Siga o mesmo processo usado no Caso de uso 1 para passar dos requisitos para um aplicativo instalado — não há necessidade de reconfigurar as integrações.

>[!IMPORTANT]
>
> Para retirar alterações em um aplicativo já associado, é necessário **Desassociar** e **Associar** novamente no Gerenciamento de Aplicativos.

### Teste funcional

1. Na configuração do aplicativo Gerenciamento de aplicativos, defina o **Limite de bloqueio de pedido (USD)** como 50 (fácil de exceder em um carrinho de teste).
1. Confirmar se o atributo personalizado da ordem existe (padrão `lab_verification_code`).
1. Faça um pedido com um total geral superior a US$ 50.
1. Aguarde aproximadamente 30 segundos (os eventos são assíncronos; a entrega não prioritária pode levar até ~59 s).
1. Em Commerce Admin → Vendas → Pedidos, abra o pedido. O status é **Em Espera** (`holded`); os atributos personalizados incluem `lab_verification_code` com um valor aleatório.
1. Opcional: coloque um pedido abaixo de US$ 50 primeiro — esse manipulador não o coloca em retenção.

## Caso de uso 3: arquivamento orientado por eventos para pedidos retidos

Volte para o estágio **Blueprint** para iniciar este caso de uso.

### Estágio de blueprint

Digite o prompt a seguir e clique em **Gerar blueprint**:

```text
When an order is saved with state holded, archive it to external storage and
record a reference that can be looked up later by order ID.

Add an event priority subscription on observer.sales_order_save_after, filtered to fire only when
state equals holded. From the event payload, extract:
- `entity_id`
- `payment.amount_ordered`
- `custom_attributes` (to read the `lab_verification_code` attribute set in Step 3)

The event handler must:
1. Persist the order details to the `held_orders` App Builder DB collection:
{
  "order_id": <entity_id>,
  "grand_total": <payment.amount_ordered>,
  "verification_code": <lab_verification_code>,
  "archived_at": <ISO timestamp>
}
2. Ensure the record can be looked up later by order ID.

The `held_orders` collection must exist before the handler runs:
- Provision persistent App Builder Database Storage in region `amer`.
- Create the collection during app installation.
- Create a unique index on `order_id` during installation.
- Drop the whole `held_orders` collection when the app is uninstalled.

Register the event handler separately from the existing cart validation webhook and high-value order hold action:
- runtime action: `order-archive/archive-held-order`
- non-web action
- `include-ims-credentials: true` on the archive action and the installation action

Follow the `commerce-app-storage` skill for DB auth, installation steps, and ext.config wiring.
Do not use custom IMS credential normalization or `Core.AuthClient.generateAccessToken`.
```

>[!NOTE]
>
> Procure estas coisas:
>
> * Um blueprint (v3) que captura os requisitos é criado.
> * As tarefas do plano original são retidas.
> * Novas tarefas correspondentes aos novos requisitos foram adicionadas.

Refine o blueprint conforme necessário, em seguida, clique em **Aprovar plano** para prosseguir.

### Desenvolver, implantar, associar e instalar

Siga o mesmo processo usado nos casos de uso anteriores para migrar dos requisitos para um aplicativo instalado — não há necessidade de reconfigurar as integrações.

>[!IMPORTANT]
>
> Para retirar alterações em um aplicativo já associado, é necessário **Desassociar** e **Associar** novamente no Gerenciamento de Aplicativos.

### Teste funcional

1. Verifique se o limite do Caso de uso 2 é baixo o suficiente para testes (por exemplo, US$ 50 na configuração do aplicativo).
1. Coloque um pedido acima desse limite para que o Caso de uso 2 o coloque em espera (~30 segundos).
1. Em Adobe Developer Console → Seu projeto → Estágio → Eventos, abra o registro para o evento de arquivamento em pedido retido (adicionado ou atualizado na instalação).
1. Confirme se um evento foi entregue a esse registro depois que o pedido foi movido para espera. Use o rastreamento ou monitoramento de eventos para o evento do Commerce vinculado a `order-archive/archive-held-order`.

>[!NOTE]
>
> Os eventos são assíncronos — aguarde até ~30-59 segundos após o pedido ser colocado em espera.

## Solução de problemas

Se o aplicativo gerado pelo CDA não estiver se comportando como esperado ou estiver produzindo erros, peça ao agente para solucionar os problemas no estágio de desenvolvimento.

>[!NOTE]
>
> A CDA não tem visibilidade sobre etapas que ocorrem fora dele. Associar, instalar, configurar e executar testes funcionais no Commerce Admin, no App Management ou na loja — não no CDA. Se um problema ocorrer em uma dessas áreas, o agente não poderá vê-lo, portanto, dê a ele o que está faltando:
>
> * O que você fez e onde (por exemplo, &quot;clicou em Instalar no Gerenciamento de aplicativos&quot;).
> * O que você esperava que acontecesse.
> * O que aconteceu.
> * O texto ou a mensagem de erro exato mostrada na tela.
> * Quaisquer erros relevantes no console do navegador ou nos registros de depuração do App Builder e do registro de eventos do Adobe Developer Console.

Quanto mais concreto for o relatório, melhor o agente poderá diagnosticar o problema.

## Etapas opcionais

**Baixar o código**

Para continuar refinando ou editando em seu IDE favorito, baixe o código gerado pelo CDA clicando no ícone de download na barra de ferramentas do explorador de estágio de desenvolvimento. Selecione uma pasta de destino, clique em **Salvar** e descompacte o pacote do espaço de trabalho.

>[!NOTE]
>
> Procure por:
>
> * Todos os arquivos exibidos no Gerenciador de estágio de desenvolvimento estão presentes na pasta descompactada.
> * Nenhum erro de &quot;compilação&quot; ao compilar o projeto com `aio app build`.

Para usar as mesmas habilidades do agente que o CDA usa, instale-as na pasta do projeto:

```bash
npx skills add adobe/aio-commerce-sdk --skill commerce-app-init -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-eventing -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-webhooks -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-business-config -y && \
npx skills add adobe/aio-commerce-sdk --skill commerce-app-storage -y && \
npx skills add adobe/skills --skill appbuilder-project-init -y
```

Em seguida, inicie o IDE ou CLI e comece a solicitar.

**Anexar contexto via arquivo ou link**

Em vez de solicitar diretamente nos estágios Blueprint ou Desenvolver, é possível anexar contexto usando um arquivo de texto ou um link:

1. Clique no ícone de anexo na caixa de diálogo.
1. Clique em **Adicionar Arquivo** para carregar um arquivo de texto local ou insira uma URL e clique em **Adicionar Link** para adicionar contexto via arquivo remoto.
1. Clique em **Concluído** e insira um aviso para chamar o agente.

>[!NOTE]
>
> Procure o agente incorporando o contexto de seus anexos em seu próximo turno.

## Problemas conhecidos e soluções alternativas

**O estágio de blueprint não gera tarefas**

Para desbloquear e continuar, mova o agente para gerar tarefas.

**Os botões para enviar e receber do GitHub não estão funcionais**

Em vez disso, baixe o arquivo ZIP do projeto no estágio Desenvolver.

{{$include /help/_includes/commerce-developer-agent-related-links.md}}

<!-- ## Additional resources -->

<!-- Link to related Experience League or Adobe Developer documentation. -->
