---
title: A pasta de teste
description: Saiba mais sobre os tipos de arquivos na pasta de teste para este aplicativo de amostra.
landing-page-description: Saiba mais sobre o Adobe Developer App Builder usado com o Adobe Commerce e quais tipos de arquivos estão localizados na pasta de teste.
kt: 12424
doc-type: tutorial
audience: all
last-substantial-update: 2023-03-10T00:00:00Z
source-git-commit: e0371a8cefab0141318daa0e1be42bfbb9e5b608
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Saiba mais sobre a pasta de teste {#test-folder}

O `test` A pasta deste aplicativo de amostra contém um único arquivo JavaScript, que é usado ao executar testes de unidade no aplicativo.

Este é um exemplo simples e pode ser expandido para criar testes abrangentes para seus aplicativos específicos.

## Para quem é este vídeo?

* Desenvolvedores novos no Adobe Commerce com experiência limitada usando o Adobe App Builder que desejam aprender mais sobre o `test` pasta.

## Conteúdo de vídeo

* Por que usar a variável `test` pasta?
* Breve explicação do ficheiro de ensaio da unidade e dos seus componentes
* Introdução ao teste completo

>[!VIDEO](https://video.tv.adobe.com/v/3416662)

## Amostras de código

test/utils.test.js

```javascript
/* 
* <license header>
*/

const utils = require('./../actions/utils.js')

test('interface', () => {
  expect(typeof utils.errorResponse).toBe('function')
  expect(typeof utils.stringParameters).toBe('function')
  expect(typeof utils.checkMissingRequestInputs).toBe('function')
  expect(typeof utils.getBearerToken).toBe('function')
})

describe('errorResponse', () => {
  test('(400, errorMessage)', () => {
    const res = utils.errorResponse(400, 'errorMessage')
    expect(res).toEqual({
      error: {
        statusCode: 400,
        body: { error: 'errorMessage' }
      }
    })
  })

  test('(400, errorMessage, logger)', () => {
    const logger = {
      info: jest.fn()
    }
    const res = utils.errorResponse(400, 'errorMessage', logger)
    expect(logger.info).toHaveBeenCalledWith('400: errorMessage')
    expect(res).toEqual({
      error: {
        statusCode: 400,
        body: { error: 'errorMessage' }
      }
    })
  })
})

describe('stringParameters', () => {
  test('no auth header', () => {
    const params = {
      a: 1, b: 2, __ow_headers: { 'x-api-key': 'fake-api-key' }
    }
    expect(utils.stringParameters(params)).toEqual(JSON.stringify(params))
  })
  test('with auth header', () => {
    const params = {
      a: 1, b: 2, __ow_headers: { 'x-api-key': 'fake-api-key', authorization: 'secret' }
    }
    expect(utils.stringParameters(params)).toEqual(expect.stringContaining('"authorization":"<hidden>"'))
    expect(utils.stringParameters(params)).not.toEqual(expect.stringContaining('secret'))
  })
})

describe('checkMissingRequestInputs', () => {
  test('({ a: 1, b: 2 }, [a])', () => {
    expect(utils.checkMissingRequestInputs({ a: 1, b: 2 }, ['a'])).toEqual(null)
  })
  test('({ a: 1 }, [a, b])', () => {
    expect(utils.checkMissingRequestInputs({ a: 1 }, ['a', 'b'])).toEqual('missing parameter(s) \'b\'')
  })
  test('({ a: { b: { c: 1 } }, f: { g: 2 } }, [a.b.c, f.g.h.i])', () => {
    expect(utils.checkMissingRequestInputs({ a: { b: { c: 1 } }, f: { g: 2 } }, ['a.b.c', 'f.g.h.i'])).toEqual('missing parameter(s) \'f.g.h.i\'')
  })
  test('({ a: { b: { c: 1 } }, f: { g: 2 } }, [a.b.c, f.g.h])', () => {
    expect(utils.checkMissingRequestInputs({ a: { b: { c: 1 } }, f: { g: 2 } }, ['a.b.c', 'f'])).toEqual(null)
  })
  test('({ a: 1, __ow_headers: { h: 1, i: 2 } }, undefined, [h])', () => {
    expect(utils.checkMissingRequestInputs({ a: 1, __ow_headers: { h: 1, i: 2 } }, undefined, ['h'])).toEqual(null)
  })
  test('({ a: 1, __ow_headers: { f: 2 } }, [a], [h, i])', () => {
    expect(utils.checkMissingRequestInputs({ a: 1, __ow_headers: { f: 2 } }, ['a'], ['h', 'i'])).toEqual('missing header(s) \'h,i\'')
  })
  test('({ c: 1, __ow_headers: { f: 2 } }, [a, b], [h, i])', () => {
    expect(utils.checkMissingRequestInputs({ c: 1 }, ['a', 'b'], ['h', 'i'])).toEqual('missing header(s) \'h,i\' and missing parameter(s) \'a,b\'')
  })
  test('({ a: 0 }, [a])', () => {
    expect(utils.checkMissingRequestInputs({ a: 0 }, ['a'])).toEqual(null)
  })
  test('({ a: null }, [a])', () => {
    expect(utils.checkMissingRequestInputs({ a: null }, ['a'])).toEqual(null)
  })
  test('({ a: \'\' }, [a])', () => {
    expect(utils.checkMissingRequestInputs({ a: '' }, ['a'])).toEqual('missing parameter(s) \'a\'')
  })
  test('({ a: undefined }, [a])', () => {
    expect(utils.checkMissingRequestInputs({ a: undefined }, ['a'])).toEqual('missing parameter(s) \'a\'')
  })
})

describe('getBearerToken', () => {
  test('({})', () => {
    expect(utils.getBearerToken({})).toEqual(undefined)
  })
  test('({ authorization: Bearer fake, __ow_headers: {} })', () => {
    expect(utils.getBearerToken({ authorization: 'Bearer fake', __ow_headers: {} })).toEqual(undefined)
  })
  test('({ authorization: Bearer fake, __ow_headers: { authorization: fake } })', () => {
    expect(utils.getBearerToken({ authorization: 'Bearer fake', __ow_headers: { authorization: 'fake' } })).toEqual(undefined)
  })
  test('({ __ow_headers: { authorization: Bearerfake} })', () => {
    expect(utils.getBearerToken({ __ow_headers: { authorization: 'Bearerfake' } })).toEqual(undefined)
  })
  test('({ __ow_headers: { authorization: Bearer fake} })', () => {
    expect(utils.getBearerToken({ __ow_headers: { authorization: 'Bearer fake' } })).toEqual('fake')
  })
  test('({ __ow_headers: { authorization: Bearer fake Bearer fake} })', () => {
    expect(utils.getBearerToken({ __ow_headers: { authorization: 'Bearer fake Bearer fake' } })).toEqual('fake Bearer fake')
  })
})
```

{{$include /help/_includes/app-builder-first-app-related-links.md}}