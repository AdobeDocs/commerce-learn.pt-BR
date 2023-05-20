---
title: A pasta Web-src
description: Saiba mais sobre os tipos de arquivos na pasta Web-src e os arquivos e pastas aninhados desta amostra aplicativo.
landing-page-description: Saiba mais sobre Adobe Systems desenvolvedor aplicativo Builder usado com Adobe Systems Comércio e quais tipos de arquivos estão localizados na pasta Web-src.
kt: 12425
doc-type: tutorial
audience: all
last-substantial-update: 2023-03-13T00:00:00Z
exl-id: 67bbb464-1c2e-493e-9d7f-1051dfeec4ee
source-git-commit: edb98cf6544954d741c43beb39f4056326c7d26b
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Discover o objetivo da pasta Web-src {#web-src-folder}

A pasta Web-src para este aplicativo de amostra contém muitos arquivos e pastas do JavaScript. Essa pasta é usada para aplicativos com uma interface usuário. Nem todos os aplicativos usam esse recurso. Por exemplo, uma integração Comércio com um sistema de gerenciamento de inventário externo pode não exigir uma interface e um código front-end.

## Para quem é esse vídeo?

* Os desenvolvedores novos no Adobe Systems Comércio com experiência limitada usando o Adobe Systems aplicativo Builder que estão aprendendo sobre a `web-src` pasta e seu conteúdo.

## Vídeo conteúdo

* Qual é o principal objetivo `web-src` da pasta?
* Geralmente arquivos e pastas incluídos
* Como a `web-src` pasta e o conteúdo dentro são usados na aplicativo de amostra

>[!VIDEO](https://video.tv.adobe.com/v/3416665?quality=12&learn=on)

## Amostras de Code

Web-src/src/Components/Orders. js

```javascript
/*
 * Copyright 2023 Adobe
 * All Rights Reserved.
 *
 * NOTICE: All information contained herein is, and remains
 * the property of Adobe and its suppliers, if any. The intellectual
 * and technical concepts contained herein are proprietary to Adobe
 * and its suppliers and are protected by all applicable intellectual
 * property laws, including trade secret and copyright laws.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe.
 */
import {
    Content,
    Heading,
    IllustratedMessage,
    TableView,
    TableHeader,
    TableBody,
    Column,
    Row,
    Cell,
    View,
    Flex,
    ProgressCircle
} from '@adobe/react-spectrum'
import {useCommerceOrders} from '../hooks/useCommerceOrders'

export const Orders = props => {

    const {isLoadingCommerceOrders, commerceOrders} = useCommerceOrders(props)

    const ordersColumns = [
        {name: 'Order Id', uid: 'increment_id'},
        {name: 'Status', uid: 'status'},
        {name: 'Store Name', uid: 'store_name'},
        {name: 'Total Item Count', uid: 'total_item_count'},
        {name: 'Total Quantity', uid: 'total_qty_ordered'},
        {name: 'Total Due', uid: 'total_due'},
        {name: 'Tax', uid: 'tax_amount'},
        {name: 'Created At', uid: 'created_at'}
    ]

    function renderEmptyState() {
        return (
            <IllustratedMessage>
                <Content>No data available</Content>
            </IllustratedMessage>
        )
    }

    return (

        <View>
            {isLoadingCommerceOrders ? (
                <Flex alignItems="center" justifyContent="center" height="100vh">
                    <ProgressCircle size="L" aria-label="Loading…" isIndeterminate/>
                </Flex>
            ) : (
                <View margin={10}>
                    <Heading level={1}>Fetched orders from Adobe Commerce</Heading>
                    <TableView
                        overflowMode="wrap"
                        aria-label="orders table"
                        flex
                        renderEmptyState={renderEmptyState}
                        height="static-size-1000"
                    >
                        <TableHeader columns={ordersColumns}>
                            {column => <Column key={column.uid}>{column.name}</Column>}
                        </TableHeader>
                        <TableBody items={commerceOrders}>
                            {order => (
                                <Row key={order['increment_id']}>{columnKey => <Cell>{order[columnKey]}</Cell>}</Row>
                            )}
                        </TableBody>
                    </TableView>
                </View>
            )}
        </View>
    )
}
```

Web-src/src/ganchos/useCommerceOrders. js

{{avoid-400-error}}

No exemplo abaixo, a amostra de código está `not` limitando o solicitação. Para evitar um erro 400, reduza o tamanho da resposta usando `searchCriteria` .

`?searchCriteria[filter_groups][0][filters][0][field]=created_at&searchCriteria[filter_groups][0][filters][0][value]=2022-12-01&searchCriteria[filter_groups][0][filters][0][condition_type]=gt`

```javascript {line-numbers="true" start-line="1" highlight="25"}
/*
 * Copyright 2023 Adobe
 * All Rights Reserved.
 *
 * NOTICE: All information contained herein is, and remains
 * the property of Adobe and its suppliers, if any. The intellectual
 * and technical concepts contained herein are proprietary to Adobe
 * and its suppliers and are protected by all applicable intellectual
 * property laws, including trade secret and copyright laws.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe.
 */
import { useEffect, useState } from 'react'
import { callAction } from '../utils'

export const useCommerceOrders = props => {
    const [isLoadingCommerceOrders, setIsLoadingCommerceOrders] = useState(true)
    const [commerceOrders, setCommerceOrders] = useState([])

    const fetchCommerceOrders = async () => {
        const commerceOrdersResponse = await callAction(
            props,
            'commerce-rest-get',
            'orders?searchCriteria=all'
        )
        setCommerceOrders(commerceOrdersResponse.error ? [] : commerceOrdersResponse.items)
    }

    useEffect(() => {
        fetchCommerceOrders().then(() => setIsLoadingCommerceOrders(false))
    }, [])

    return { isLoadingCommerceOrders, commerceOrders }
}
```

{{$include /help/_includes/app-builder-first-app-related-links.md}}
