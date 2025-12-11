---
title: Diagnosticar e corrigir alguns erros comuns do Commerce Cloud
description: Resolva dois erros comuns de projeto da Adobe Cloud que impedem o carregamento do site.
feature: Cloud, Site Management
topic: Commerce, Development
old-role: Architect, Developer
role: Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 260
last-substantial-update: 2024-10-30T00:00:00Z
jira: KT-16419
exl-id: 4c21b6a6-783a-422f-9071-3534ed68e8be
source-git-commit: afe0ac1781bcfc55ba0e631f492092fd1bf603fc
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# O serviço de diagnóstico e correção não está disponível e ocorreu um erro

Saiba como triar e resolver dois erros comuns vistos em projetos da Adobe Commerce Cloud.  Entenda como e por que esses erros ocorrem e quais são as etapas recomendadas para resolvê-los.

## Para quem é este vídeo

- Desenvolvedores e profissionais de TI
- Administradores do sistema

## Conteúdo de vídeo

- Diagnosticar e resolver problemas de armazenamento:
- Gerenciar modo de manutenção
- Dicas eficientes de solução de problemas

>[!VIDEO](https://video.tv.adobe.com/v/3435766?learn=on)


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
