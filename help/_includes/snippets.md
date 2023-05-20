---
title: Banners de edição
description: Elementos visuais reutilizados para anotar recursos ou páginas que se aplicam a uma edição específica
source-git-commit: 8c7c64ddff456815b0a1649f497e917da8b8fca0
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Banners de edição

## Recurso somente EE {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Recurso do Adobe Commerce" src="../assets/adobe-logo.svg" width="20" height="20" /> Recurso exclusivo somente no Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">Saiba mais</a>)</td></tr>
</table>

## Recurso somente B2B {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Recurso do Adobe Commerce" src="../assets/b2b.svg" width="20" height="20" /> Recurso exclusivo disponível somente com o <a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">B2B para Adobe Commerce</a></td></tr>
</table>

## 400 problemas {#avoid-400-error}

>[!CAUTION]
>
>Ao executar chamadas de API, verifique se algum tipo de searchCriteria é usado. Você também pode considerar o uso de paginação. Se o resultado do Adobe Commerce for muito grande, a capacidade do Construtor de aplicativos do Adobe Developer poderá ser atendida e causar um encerramento inesperado do arquivo. O resultado é uma resposta malformada como um erro 400.\
> Por exemplo, suponha que haja uma necessidade de solicitar todos os produtos atuais da Adobe Commerce. O URL resultante seria semelhante a `{{base_url}}rest/V1/products?searchCriteria=all`. Dependendo do tamanho do catálogo retornado, o json pode ser muito grande para o Construtor de aplicativos consumir. Use a paginação e faça algumas solicitações para evitar `Response is not valid 'message/http'.`
