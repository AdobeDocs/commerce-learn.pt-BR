---
title: Usar o Fastly para negar acesso a um site inteiro
description: Restringir o acesso ao site do Adobe Commerce com ACLs do Fastly Edge e um VCL Personalizado
feature: Cloud, Configuration, Site Management, System
topic: Administration,Commerce,Development, Security
role: Admin, Developer, User
level: Intermediate, Experienced
doc-type: Technical Video
duration: 200
last-substantial-update: 2025-07-11T00:00:00Z
jira: KT-18494
source-git-commit: 810d1a17e9fe564e8450b091bbeb5574d7d76075
workflow-type: tm+mt
source-wordcount: '130'
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

>[!VIDEO](https://video.tv.adobe.com/v/3464779/?learn=on&enablevpops)

## Amostra de código

Este é um exemplo do VCL usado

```BASH
if ( !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
```

## Documentação relacionada

* [Detectando endereço IP mal-intencionado](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/tools/new-relic/malicious-ip)
* [VCL personalizado para solicitações de permissão](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-allowlist)
* [VCL personalizado para solicitações de bloqueio](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking)