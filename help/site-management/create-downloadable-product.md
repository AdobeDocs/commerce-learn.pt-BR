---
title: Criar um produto para download
description: Saiba como criar um produto para download usando a REST API e o administrador do Adobe Commerce.
kt: 14464
doc-type: video
audience: all
activity: use
last-substantial-update: 2023-11-16T00:00:00Z
feature: Catalog Management, Admin Workspace, Backend Development, Integration, REST
topic: Commerce, Integrations, Content Management
role: Developer, User
level: Beginner
exl-id: 90753b8d-eca0-4868-b40e-9563d2b0e1e8
source-git-commit: eba043cd4169cd762653557bf9283b8d6a208ef0
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Criar um produto para download

Saiba como criar um produto para download usando a REST API e o administrador do Adobe Commerce.

## Para quem é este vídeo?

- Gerentes de sites
- Merchandisers de comércio eletrônico
- Novos desenvolvedores do Adobe Commerce que desejam aprender como criar produtos no Adobe Commerce usando a REST API

## Conteúdo de vídeo

>[!VIDEO](https://video.tv.adobe.com/v/3425753?learn=on)

## Domínios baixáveis permitidos

Você deve especificar quais domínios têm permissão para downloads. Os domínios são adicionados ao `env.php` arquivo por meio da linha de comando. A variável `env.php` o arquivo detalha os domínios permitidos para conter conteúdo baixável. Ocorre um erro se um produto para download for criado usando a API REST _antes_  o `php.env` O arquivo foi atualizado:

```bash
{
    "message": "Link URL's domain is not in list of downloadable_domains in env.php."
}
```

Para definir o domínio, conecte-se ao servidor: `bin/magento downloadable:domains:add www.example.com`

Depois que estiver concluído, a variável `env.php` é modificado dentro do _downloadable_domains_ matriz.

```php
    'downloadable_domains' => [
        'www.example.com'
    ],
```

Agora que o domínio foi adicionado à variável `env.php`, você pode criar um produto para download no Administrador do Adobe Commerce ou usando a API REST.

Consulte [Referência de configuração](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains) para saber mais.

>[!IMPORTANT]
>Em algumas versões do Adobe Commerce, você pode receber o seguinte erro quando um produto é editado no administrador do Adobe Commerce. O produto é criado usando a REST API, mas o download vinculado tem uma `null` preço.

`Deprecated Functionality: number_format(): Passing null to parameter #1 ($num) of type float is deprecated in /app/vendor/magento/module-downloadable/Ui/DataProvider/Product/Form/Modifier/Data/Links.php on line 228`.

Para corrigir esse erro, use a API do link de atualização: `POST V1/products/{sku}/downloadable-links.`

Consulte a [Atualizar um link de download de produto usando cURL](#update-downloadable-links) para obter mais informações.

## Criar um produto para download usando cURL (download do servidor remoto)

Este exemplo mostra como criar um produto para download usando cURL quando o arquivo para download não estiver no mesmo servidor. Esse caso de uso é típico se o arquivo for armazenado em um bucket do S3 ou outro gerenciador de ativos digitais.

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01' \
--data '{
  "product": {
    "sku": "POSTMAN-download-product-1",
    "name": "POSTMAN download product-1",
    "attribute_set_id": 4,
    "price": 9.9,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        
        "downloadable_product_links": [
            {
                "title": "My url link",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "url",
                "link_url": "{{location.url.where.file.exists}}/some-file.zip",
                "sample_type": "url",
                "sample_url": "{{location.url.where.file.exists}}/sample-file.zip"
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}
'
```

## Criar um produto para download usando o cURL (download do servidor de aplicativos Commerce)

Este exemplo demonstra como usar o cURL para criar um produto para download do Adobe Commerce Admin quando o arquivo é armazenado no mesmo servidor que o aplicativo do Adobe Commerce.

Nesse caso de uso, quando o administrador que gerencia o catálogo escolher `upload file`, o arquivo é transferido para o `pub/media/downloadable/files/links/` diretório.  A automação cria e move os arquivos para seus respectivos locais com base no seguinte padrão:

- Cada arquivo carregado é armazenado em uma pasta com base nos dois primeiros caracteres do nome do arquivo.
- Quando o upload é iniciado, o aplicativo do Commerce cria ou usa pastas existentes para transferir o arquivo.
- Ao baixar o arquivo, a variável `link_file` seção do caminho usa a parte do caminho anexada ao `pub/media/downloadable/files/links/` diretório.

Por exemplo, se o arquivo carregado for nomeado como `download-example.zip`:

- O arquivo é carregado no caminho `pub/media/downloadable/files/links/d/o/`.
Os subdiretórios `/d` e `/d/o` são criadas se não existirem.

- O caminho final para o arquivo é `/pub/media/downloadable/files/links/d/o/download-example.zip`.

- A variável `link_url` o valor deste exemplo é `d/o/download-example.zip`

```bash
curl --location '{{your.url.here}}/rest/default/V1/products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=571f5ebe48857569cd56bde5d65f83a2; private_content_version=9f3286b427812be6aec0b04cae33ba35' \
--data '{
  "product": {
    "sku": "sample-local-download-file",
    "name": "A downloadable product with locally hosted download file",
    "attribute_set_id": 4,
    "price": 33,
    "status": 1,
    "visibility": 4,
    "type_id": "downloadable",
    "extension_attributes": {
        "website_ids": [
            1
        ],
        "downloadable_product_links": [
            {
                "title": "an api version of already upload file",
                "sort_order": 1,
                "is_shareable": 1,
                "price": 0,
                "number_of_downloads": 0,
                "link_type": "file",
                "link_file": "/d/o/downloadable-file-demo-file-upload.zip",
                "sample_type": null
            }
        ],
        "downloadable_product_samples": []
    },
    "product_links": [],
    "options": [],
    "media_gallery_entries": [],
    "tier_prices": []
  }
}'
```

## Obter um produto usando o curl

```bash
curl --location '{{your.url.here}}/rest/default/V1/products/POSTMAN-download-product-1' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=b78cae2338f12d846d233d4e9486607e; private_content_version=564dde2976849891583a9a649073f01e'
```

## Atualizar o produto usando o Postman {#update-downloadable-links}

Usar o endpoint `rest/all/V1/products/{sku}/downloadable-links`
A variável `SKU` é a ID do produto gerada quando o produto foi criado. Por exemplo, na amostra de código abaixo, é o número 39, mas certifique-se de que esteja atualizado para usar a ID do seu site. Isso atualiza os links dos produtos baixáveis.

```json
{
  "link": {
    "id": 39,
    "title": "My swagger update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}
```

## Atualizar um link de download de produto usando CURL

Ao atualizar um link de download de produto usando cURL, o URL inclui a SKU do produto que está sendo atualizado.  No código de exemplo a seguir, o SKU é `abcd12345`. Ao enviar o comando, altere o valor para corresponder ao SKU do produto que deseja atualizar.

```bash
curl --location '{{your.url.here}}/rest/all/V1/products/abcd12345/downloadable-links' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{Your Bearer Token}}' \
--header 'Cookie: PHPSESSID=fa5d76f4568982adf369f758e8cb9544; private_content_version=564dde2976849891583a9a649073f01e' \
--data '{
  "link": {
    "id": {{The ID of the download link for example 39}},
    "title": "My update",
    "sort_order": 0,
    "is_shareable": 0,
    "price": 0,
    "number_of_downloads": 0,
    "link_type": "url",
    "link_file": "{{your.url.here}}/some-file.zip",
    "link_url": "{{your.url.here}}/some-file.zip",
    "link_file_content": {
      "file_data": "{{your.url.here}}/some-file.zip",
      "extension_attributes": {}
    }
  },
  "isGlobalScopeContent": true
}'
```

## Recursos adicionais

- [Tipo de produto baixável](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-downloadable.html){target="_blank"}
- [Guia de configuração de domínios baixáveis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/files/config-reference-envphp.html#downloadable_domains){target="_blank"}
- [Tutoriais do Adobe Developer REST](https://developer.adobe.com/commerce/webapi/rest/tutorials/prerequisite-tasks/){target="_blank"}
- [ReDoc Adobe Commerce REST](https://adobe-commerce.redoc.ly/2.4.6-admin/tag/products#operation/PostV1Products){target="_blank"}
