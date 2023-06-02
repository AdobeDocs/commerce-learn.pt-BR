---
title: Criar um módulo
description: Crie uma página que retorne json com um parâmetro.
topic: Development
kt: 5614
doc-type: video
activity: use
last-substantial-update: 2023-6-2
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: fb2cb5b844c4156802e8627e71fc18f8e7fa981d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Criar um módulo

O módulo é um elemento estrutural de [!DNL Commerce] - todo o sistema se baseia em módulos. Normalmente, a primeira etapa na criação de uma personalização é criar um módulo.

## Para quem é este vídeo?

- Desenvolvedores

## Etapas para adicionar um módulo

- Crie a pasta do módulo.
- Crie o arquivo etc/module.xml.
- Crie o arquivo registration.php.
- Execute a configuração bin/magento.
- Atualizar script para instalar o novo módulo.
- Verifique se o módulo está funcionando.

>[!VIDEO](https://video.tv.adobe.com/v/35792?learn=on)

### module.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Training_Sales">
        <sequence>
            <module name="Magento_Sales"/>
        </sequence>
    </module>
</config>
```

### registration.php

```PHP
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Training_Sales',
    __DIR__);
```

## Recursos úteis

- [Guia de referência de módulo](https://developer.adobe.com/commerce/php/module-reference/)
