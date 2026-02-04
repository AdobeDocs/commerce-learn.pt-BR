---
title: Explorar novas APIs REST do cliente
description: Descubra como usar as novas APIs REST do cliente no Adobe Commerce Cloud Service. Ideal para arquitetos e desenvolvedores.
feature: REST, Customers, Saas
topic: Development, Integrations
role: Architect, Developer
level: Beginner
doc-type: Tutorial
duration: 225
last-substantial-update: 2026-01-27T00:00:00Z
jira: KT-20160
source-git-commit: ad2cfb4b38d739b03e0c2fff8bcd88d77d6e4b12
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# API REST do cliente

Saiba como usar as novas APIs REST do cliente no Adobe Commerce as a Cloud Service. Este tutorial é perfeito para arquitetos e desenvolvedores que buscam integrar e otimizar as soluções de API de maneira eficaz.

## Para quem é este vídeo?

* Desenvolvedores de back-end responsáveis por criar integrações com o Adobe Commerce
* Arquitetos técnicos projetando workflows de gerenciamento de clientes para implementações de comércio headless

## Conteúdo de vídeo

* Autentique com o Adobe IMS usando credenciais de servidor para servidor para obter um token de acesso para solicitações de API
* Use o formato correto de endpoint da API REST para o Commerce as a Cloud Service
* Crie e atualize contas de clientes de forma programática usando solicitações POST e PUT com cargas JSON adequadas

>[!VIDEO](https://video.tv.adobe.com/v/3479361/?learn=on&enablevpops)

## Amostras de código

Antes de iniciar, colete todos os valores necessários do [Experience Cloud](https://experience.adobe.com) e do [Adobe Developer Console](https://developer.adobe.com/console). Ter esses valores prontos garante um processo de configuração tranquilo.

>[!NOTE]
>
>Verifique se você está trabalhando na organização correta. A seleção de sua organização afeta quais instâncias e ambientes estão visíveis no Experience Cloud e na Developer Console.

### Detalhes da instância - experience.adobe.com

Os detalhes da instância contêm informações como ID da instância, endpoints do GraphQL e credenciais.

### Detalhes do desenvolvedor - https://developer.adobe.com/console/

O Developer Console é onde você gerencia as credenciais da API, incluindo IDs do cliente, segredos do cliente e tokens de acesso. Você também pode criar novos tipos de credenciais, como autenticação de Servidor para Servidor ou de Aplicativo Nativo.

## Pré-requisitos

| Item | Valor | Onde é este valor |
|--- |--- |--- |
| ID da instância | `<instance_id>` | experience.adobe.com |
| Endpoint REST | `<rest_endpoint>` | experience.adobe.com |
| ID do cliente | `<client_id>` | developer.adobe.com/console |
| Segredo do cliente | `<client_secret>` | developer.adobe.com/console |


## Etapa 1: Obter Token de Acesso (Autenticação de Servidor para Servidor)

>[!IMPORTANT]
>
> As variáveis mostradas neste exemplo não são válidas. Use o &lt;client_id> e o &lt;client_secret> das credenciais do projeto.

```bash
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=client_credentials&client_id=<client_id>&client_secret=<client_secret>&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles'
```

**Exemplo de resposta:**

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIs...",
  "token_type": "bearer",
  "expires_in": 86399
}
```

## Etapa 2: Criar um Cliente

>[!IMPORTANT]
>
> O URL fornecido nesta amostra não é válido. Use seu URL base REST. Troque &#39;&lt;rest_endpoint>&#39; por seu URL. É semelhante a este `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123`.
>
> Esse endpoint não tem /rest/ como parte do URL. Incluir isso leva a um erro.

**Ponto de extremidade:** `POST /V1/customers`

```bash
curl -X POST \
  "<rest_endpoint>/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }'
```

**Resposta:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:15",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "store_id": 1,
  "website_id": 1,
  "addresses": [],
  "disable_auto_group_change": 0
}
```

## Etapa 3: Atualizar um Cliente

>[!IMPORTANT]
>
> O URL fornecido nesta amostra não é válido. Use seu URL base REST. Troque &#39;&lt;rest_endpoint>&#39; por seu URL. É semelhante a este `https://na1-sandbox.api.commerce.adobe.com/AbCYab34cdEfGHiJ27123`.

O número `5` no exemplo a seguir é a ID do cliente criado anteriormente usando o POST `"id": 5,`. Certifique-se de alterar `5` para qualquer ID retornada em sua solicitação.

**Ponto de extremidade:** `PUT /V1/customers/{customerId}`

```bash
curl -X PUT \
  "<rest_endpoint>/V1/customers/5" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <ACCESS_TOKEN>" \
  -d '{
    "customer": {
      "id": 5,
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe-Updated"
    }
  }'
```

**Resposta:**

```json
{
  "id": 5,
  "group_id": 1,
  "created_at": "2026-01-23 20:40:15",
  "updated_at": "2026-01-23 20:40:30",
  "created_in": "Default Store View",
  "email": "john.doe@example.com",
  "firstname": "John",
  "lastname": "Doe-Updated",
  "store_id": 1,
  "website_id": 1,
  "addresses": []
}
```

## Script completo (all-in-one)

>[!IMPORTANT]
>
> As variáveis mostradas neste exemplo não são válidas. Use a ID do cliente e o segredo do cliente das credenciais do projeto. Use seu URL base REST. Troque &#39;&lt;rest_endpoint>&#39; pela URL do ponto de extremidade REST de experience.adobe.com. É semelhante a este `https://na1-sandbox.api.commerce.adobe.com/AbCDefGHiJ1234567`.

```bash
#!/bin/bash

# Configuration be sure to update these with your projects unique values
CLIENT_ID="<client_id>"
CLIENT_SECRET="<client_secret>"
REST_ENDPOINT="<rest_endpoint>"

# Step 1: Get Access Token
echo "Getting access token..."
ACCESS_TOKEN=$(curl -s -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d "grant_type=client_credentials&client_id=${CLIENT_ID}&client_secret=${CLIENT_SECRET}&scope=openid,AdobeID,email,additional_info.projectedProductContext,profile,commerce.aco.ingestion,commerce.accs,org.read,additional_info.roles" | jq -r '.access_token')

echo "Token obtained: ${ACCESS_TOKEN:0:50}..."

# Step 2: Create Customer
echo ""
echo "Creating customer..."
CREATE_RESPONSE=$(curl -s -X POST \
  "${REST_ENDPOINT}/V1/customers" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d '{
    "customer": {
      "email": "john.doe@example.com",
      "firstname": "John",
      "lastname": "Doe",
      "store_id": 1,
      "website_id": 1
    },
    "password": "TempPa55word!"
  }')

echo "Create Response:"
echo "$CREATE_RESPONSE" | jq .

# Extract customer ID
CUSTOMER_ID=$(echo "$CREATE_RESPONSE" | jq -r '.id')
echo "Customer ID: $CUSTOMER_ID"

# Step 3: Update Customer
echo ""
echo "Updating customer..."
curl -s -X PUT \
  "${REST_ENDPOINT}/V1/customers/${CUSTOMER_ID}" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ${ACCESS_TOKEN}" \
  -d "{
    \"customer\": {
      \"id\": ${CUSTOMER_ID},
      \"email\": \"john.doe@example.com\",
      \"firstname\": \"john\",
      \"lastname\": \"Doe-Updated\"
    }
  }" | jq .
```

## Observações importantes sobre este tutorial

1. **Caminho da URL**: Usar `https://<server>.api.commerce.adobe.com/<tenant-id>/V1/customers` — **NÃO** `https://<host>/rest/<store-view-code>/V1/customers`
1. **Autenticação**: este tutorial usou Servidor a Servidor (tipo de concessão `client_credentials`)
1. **Escopo Necessário**: `commerce.accs`
1. **Expiração do token**: 86.400 segundos (24 horas)

## Referências

* [Notas de versão do Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/commerce/cloud-service/release-notes)
* [Referência da API REST SaaS](https://developer.adobe.com/commerce/webapi/reference/rest/saas/)
* [Guia de Autenticação do Usuário](https://developer.adobe.com/commerce/webapi/rest/authentication/user/)
