---
title: Usar o Fastly para negar acesso a um site inteiro
description: Restringir o acesso ao site do Adobe Commerce com ACLs do Fastly Edge e um VCL Personalizado
feature: Cloud, Configuration, Site Management, System
topic: Administration,Commerce,Development, Security
role: Admin, Developer, User
level: Intermediate, Experienced
doc-type: Technical Video
duration: 231
last-substantial-update: 2025-07-11T00:00:00.000Z
jira: KT-18494
exl-id: 121e7a2f-f9fd-4cd1-b2be-48a12b538008
TQID: 'https://experienceleague.adobe.com/OQlPdH-rAoSoPK1-zemp5OODX6pKWV-dW1C88KVRE6I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 938d2364-5176-55ec-80f1-9415253e5e51
    internal-label: Site Management
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Experienced
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%
---
# Usar o Fastly para negar o acesso a um site inteiro

Saiba como restringir o acesso ao seu site da Adobe Commerce Cloud usando ACLs do Fastly Edge e trechos personalizados de VCL. Este guia passo a passo ajuda a proteger seu ambiente de pré-lançamento, permitindo somente endereços IP específicos, garantindo que seu site de desenvolvimento permaneça privado.

## O que você vai aprender

Restringir o acesso ao site do Adobe Commerce com ACLs do Fastly Edge e VCL Personalizado | Ambientes Seguros De Pré-Lançamento

## Para quem é este vídeo?

* Engenheiro de DevOps
* Desenvolvedor do Adobe Commerce
* Engenheiro de confiabilidade do site

>[!VIDEO](https://video.tv.adobe.com/v/3464784?captions=por_br&learn=on)

## Amostra de código

Este é um exemplo do VCL usado

```BASH
if ( !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
```

## Documentação relacionada

* [Detecção de endereço IP mal-intencionado](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/tools/new-relic/malicious-ip)
* [VCL personalizado para permitir solicitações](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist)
* [VCL personalizado para solicitações de bloqueio](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking)
