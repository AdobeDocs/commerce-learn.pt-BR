---
title: Criar um módulo
description: Crie uma página que retorne json com um parâmetro.
topic: Development
kt: 5602
doc-type: video
activity: use
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: 32d1366758fa6453a48570cfd08d10a93559a974
workflow-type: tm+mt
source-wordcount: '94'
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
