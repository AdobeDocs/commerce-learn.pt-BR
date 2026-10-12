---
title: Diagnosticar e corrigir alguns erros comuns do Commerce Cloud
description: Resolva dois erros comuns de projeto da Adobe Cloud que impedem o carregamento do site.
feature: Cloud, Site Management
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 297
last-substantial-update: 2024-10-30T00:00:00.000Z
jira: KT-16419
exl-id: 4c21b6a6-783a-422f-9071-3534ed68e8be
TQID: 'https://experienceleague.adobe.com/-mN2UoNU6uKjUoHmZT59LgT4o7p4d4O2Zl1BR3x8y-8'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 938d2364-5176-55ec-80f1-9415253e5e51
    internal-label: Site Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: 71835f0240311d4b26ec8e0d9bbdf005f9887579
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%
---
# O serviço de diagnóstico e correção não está disponível e ocorreu um erro

Saiba como triar e resolver dois erros comuns vistos em projetos da Adobe Commerce Cloud.  Entenda como e por que esses erros ocorrem e quais são as etapas recomendadas para resolvê-los.

## Para quem é este vídeo

* Desenvolvedores e profissionais de TI
* Administradores do sistema

## Conteúdo de vídeo

* Diagnosticar e resolver problemas de armazenamento:
* Gerenciar modo de manutenção
* Dicas eficientes de solução de problemas

>[!VIDEO](https://video.tv.adobe.com/v/3447698?captions=por_br&learn=on)


## Comandos usados no vídeo

Localize as 5 últimas linhas do log de exceções mencionado na mensagem de resposta.

```SHELL
 tail -n 5 ~/var/log/exception.log
```

Para verificar o espaço no disco rígido. Preste atenção na linha dev/mapper/xxxx

```SHELL
df -h
```

Vamos encontrar os 15 maiores arquivos

```SHELL
find -type f -exec du -Sh {} + | sort -rh | head -n 15
```

Exibir o status do modo de manutenção

```SHELL
php bin/magento maintenance:status
```

Desabilitar o modo de manutenção

```SHELL
php bin/magento maintenance:disable 
```
