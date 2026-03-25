---
title: Criar um módulo
description: Crie e registre um módulo no Adobe Commerce, execute a configuração e adicione plug-ins que registrem no log PSR nos contextos da área de administração, loja e API REST.
jira: KT-5614
doc-type: Technical Video
duration: 1113
activity: use
last-substantial-update: 2026-03-23T00:00:00Z
feature: Configuration, System, Backend Development
topic: Commerce, Development
role: Admin, Developer
level: Beginner, Intermediate
exl-id: 941c04ee-54b8-4b81-b77d-fff5875927f0
source-git-commit: 1e67193c9b80c929ec391acef771562fb930cc67
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Criar um módulo

Um módulo é um elemento estrutural de [!DNL Commerce]—módulos formam o backbone do sistema. Normalmente, você inicia uma personalização criando um módulo.

## Para quem é este vídeo?

* Desenvolvedores de backend

## Etapas para adicionar um módulo

1. Crie a pasta do módulo.
2. Crie o arquivo `etc/module.xml`.
3. Crie o arquivo `registration.php`.
4. Execute `bin/magento setup:upgrade` para registrar e instalar o módulo.
5. Verifique se o módulo está funcionando.

>[!VIDEO](https://video.tv.adobe.com/v/35792?learn=on)

### O arquivo module.xml

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

### O arquivo registration.php

```php
<?php

use Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Training_Sales',
    __DIR__);
```

### Adicionar um plug-in

Em seguida, você adiciona funcionalidade ao módulo básico. Você usa plug-ins como ferramentas essenciais no desenvolvimento do Adobe Commerce. Este vídeo e tutorial mostram como criar um plug-in.

>[!VIDEO](https://video.tv.adobe.com/v/3420255?learn=on)

### Itens a lembrar para plug-ins

* Você declara todos os plug-ins em `di.xml`.
* Você dá a cada plug-in um nome exclusivo.
* Opcionalmente, você pode definir os atributos `disabled` e `sortOrder`.
* Você define o escopo do plug-in escolhendo qual pasta contém o arquivo `di.xml`.
* Você executa plug-ins antes, depois ou ao redor da chamada do método target.
* Evite `around` plug-ins. Eles tentam, mas geralmente representam a escolha errada e causam problemas de desempenho.

### Exemplos de código de plug-in

O tutorial usa as seguintes classes XML e PHP para adicionar um plug-in ao primeiro módulo.

### app/code/Training/Sales/etc/adminhtml/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A Plugin that executes when the admin user places an order -->
    <type name="Magento\Sales\Model\Order">
        <plugin name="admin-training-sales-add-logging" type="Training\Sales\Plugin\AdminAddLoggingAfterOrderPlacePlugin" disabled="false" sortOrder="0"/>
    </type>
</config>
```

### app/code/Training/Sales/etc/frontend/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A plugin that executes when a customer uses the LoginPost controller from the Luma frontend -->
    <type name="Magento\Customer\Controller\Account\LoginPost">
        <plugin name="training-customer-loginpost-plugin"
                type="Training\Sales\Plugin\CustomerLoginPostPlugin" sortOrder="20"/>
    </type>
</config>
```

### app/code/Training/Sales/etc/webapi_rest/di.xml

```xml
<?xml version="1.0" ?>
<!--
/**
 * Copyright &copy; Magento, Inc. All rights reserved.
 * See COPYING.txt for license details.
 */
-->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <!-- A plugin that executes when the REST API is used OR when the Luma frontend places an order -->
    <type name="Magento\Sales\Model\Order">
        <plugin name="rest-training-sales-add-logging" type="Training\Sales\Plugin\RestAddLoggingAfterOrderPlacePlugin"/>
    </type>
</config>
```

### app/code/Training/Sales/Plugin/AdminAddLoggingAfterOrderPlacePlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Magento\Sales\Model\Order;
use Psr\Log\LoggerInterface;

/**
 *
 */
class AdminAddLoggingAfterOrderPlacePlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @param LoggerInterface $logger
     */
    public function __construct(
        LoggerInterface $logger
    ) {
        $this->logger = $logger;
    }

    /**
     * Add log after an order is placed
     *
     * @param Order $subject
     * @param Order $result
     * @return Order
     */
    public function afterPlace(Order $subject, Order $result): Order
    {
        // Log this admin area order
        $this->logger->notice('An ADMIN User placed an Order - $' . $subject->getBaseTotalDue());
        return $result;
    }
}
```

### app/code/Training/Sales/Plugin/CustomerLoginPostPlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Psr\Log\LoggerInterface;
use Magento\Framework\App\RequestInterface;

/**
 * Introduces Context information for ActionInterface of Customer Action
 */
class CustomerLoginPostPlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @var RequestInterface
     */
    private RequestInterface $request;

    /**
     * @param LoggerInterface $logger
     * @param RequestInterface $request
     */
    public function __construct(LoggerInterface $logger, RequestInterface $request)
    {
        $this->logger = $logger;
        $this->request = $request;
    }

    /**
     * Simple example of a before Plugin on a public method in a Controller
     */
    public function beforeExecute()
    {
        $login = $this->request->getParam('login');
        $username = $login['username'];
        $this->logger->notice( "Login Post controller was used for " . $username );
    }
}
```

### app/code/Training/Sales/Plugin/RestAddLoggingAfterOrderPlacePlugin.php

```php
<?php

declare(strict_types=1);

namespace Training\Sales\Plugin;

use Magento\Sales\Model\Order;
use Psr\Log\LoggerInterface;

/**
 *
 */
class RestAddLoggingAfterOrderPlacePlugin
{

    /**
     * @var LoggerInterface
     */
    private LoggerInterface $logger;

    /**
     * @param LoggerInterface $logger
     */
    public function __construct(
        LoggerInterface $logger
    ) {
        $this->logger = $logger;
    }

    /**
     * Add log after an order is placed
     *
     * @param Order $subject
     * @param Order $result
     * @return Order
     */
    public function afterPlace(Order $subject, Order $result): Order
    {
        // Log this customer driven order
        $this->logger->notice('A Customer placed an Order for $' . $subject->getBaseTotalDue());
        return $result;
    }
}
```

## Recursos úteis

* [Guia de referência do módulo](https://developer.adobe.com/commerce/php/module-reference/){target="_blank"}
* [Plug-ins](https://developer.adobe.com/commerce/php/development/components/plugins/){target="_blank"}
