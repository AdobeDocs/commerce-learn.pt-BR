---
title: Diagnosticar e corrigir alguns erros comuns de Commerce Cloud
description: Resolva dois erros comuns no projeto da Adobe Cloud que impedem o carregamento do site.
feature: Cloud, Site Management
topic: Commerce, Development
role: Architect, Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 260
last-substantial-update: 2024-10-30T00:00:00Z
jira: KT-16419
source-git-commit: 27c1715dd42853013181d9c729549a5a32bc2af0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# O serviço de diagnóstico e correção não está disponível e ocorreu um erro

Saiba como triar e resolver dois erros comuns vistos em projetos do Adobe Commerce Cloud.  Entenda como e por que esses erros ocorrem e quais são as etapas recomendadas para resolvê-los.

## Para quem é este vídeo

- Desenvolvedores e profissionais de TI
- Administradores do sistema

## Conteúdo de vídeo

- Diagnosticar e resolver problemas de armazenamento:
- Gerenciar modo de manutenção
- Dicas eficientes de solução de problemas

>[!VIDEO](https://video.tv.adobe.com/v/3447698?learn=on&captions=por_br)


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
