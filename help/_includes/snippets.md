---
title: Banners de edição
description: Elementos visuais reutilizados para observar o recurso ou as páginas que se aplicam a uma edição específica
source-git-commit: 8c7c64ddff456815b0a1649f497e917da8b8fca0
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Banners de edição

## Apenas recurso EE {#ee-feature}

<table style="border:1px solid red">
<tr><td><img alt="Recurso do Adobe Commerce" src="../assets/adobe-logo.svg" width="20" height="20" /> Recurso exclusivo somente no Adobe Commerce (<a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">Saiba mais</a>)</td></tr>
</table>

## Recurso somente B2B {#b2b-feature}

<table style="border:1px solid green">
<tr><td><img alt="Recurso do Adobe Commerce" src="../assets/b2b.svg" width="20" height="20" /> Recurso exclusivo disponível somente com <a href="https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html#product-editions">B2B para Adobe Commerce</a></td></tr>
</table>

## 400 problemas {#avoid-400-error}

>[!CAUTION]
>
>Ao executar chamadas de API, verifique se um tipo de searchCriteria é usado. Você também pode considerar o uso da paginação. Se o resultado do Adobe Commerce for muito grande, a capacidade do Adobe Developer App Builder poderá ser atendida e causar um fim inesperado ao arquivo. O resultado é um resultado de resposta malformada como um erro 400.\
> Por exemplo, suponha que haja uma necessidade de solicitar todos os produtos atuais do Adobe Commerce. O URL resultante seria semelhante `{{base_url}}rest/V1/products?searchCriteria=all`. Dependendo do tamanho do catálogo retornado, o json pode ser muito grande para ser consumido pelo App Builder. Em vez disso, use a paginação e faça algumas solicitações para evitar `Response is not valid 'message/http'.`
