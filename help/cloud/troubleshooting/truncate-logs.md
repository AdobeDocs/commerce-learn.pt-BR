---
title: Truncar logs
description: Saiba como fazer a triagem de uma implantação com falha devido a um disco rígido cheio truncando arquivos de log grandes.
feature: Cloud, Site Management
topic: Commerce, Development
role: Architect, Developer
level: Beginner, Intermediate
doc-type: Technical Video
duration: 206
last-substantial-update: 2025-3-25
jira: KT-17595
source-git-commit: b90aa9eb8759391a16dfb29ca25b0d2d271956ed
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Truncar logs

Saiba como fazer a triagem e uma implantação com falha devido a um disco rígido completo. Saiba como encontrar e quais comandos podem ser executados para liberar espaço no ambiente da Adobe Commerce Cloud.

Se você acha que precisa desses arquivos de log, pode `rsync` ou usar outros métodos para obter uma cópia disponível do servidor antes de truncá-los.

## Para quem é este vídeo

- Desenvolvedores e profissionais de TI
- Administradores do sistema

## Conteúdo de vídeo

- Diagnosticar e resolver uma implantação com falha
- Onde alguns arquivos de log grandes comuns são encontrados
- Método rápido para truncar um arquivo de log

>[!VIDEO](https://video.tv.adobe.com/v/3454572?learn=on)


## Comandos usados no vídeo

Para verificar o espaço no disco rígido `df -h`. Preste atenção na linha dev/mapper/xxxx

```SHELL
df -h

Filesystem                              Size  Used Avail Use% Mounted on
/dev/loop217                           1016M 1016M     0 100% /
none                                    492K  4.0K  488K   1% /dev
fake-sysfs                              120G     0  120G   0% /sys
tmpfs                                   120G     0  120G   0% /sys/fs/cgroup
tmpfs                                   384M     0  384M   0% /dev/shm
tmpfs                                    50M  460K   50M   1% /run
tmpfs                                   5.0M     0  5.0M   0% /run/lock
/dev/loop236                            144M  144M     0 100% /app
/dev/mapper/hyjh5nlaoabqtxxnh4opgjqzpu  4.9G  4.9G     0 100% /mnt
/dev/loop14                             8.0G  403M  7.6G   5% /tmp
/dev/mapper/platform-lxc                5.0T   69G  4.7T   2% /run/shared
```


Exibir os arquivos e seus tamanhos em formato legível por humanos, como kb, mb e gb, usando o comando `ls -lah`

```SHELL
ls -lah

total 4.7G
drwxr-xr-x 2 web web 4.0K Jul 16  2024 .
drwxr-xr-x 6 web web 4.0K Jan 10  2024 ..
-rw-rw-r-- 1 web web 487K Jul  5  2024 cache.log
-rw-r--r-- 1 web web 1.2K Jul 16  2024 cloud.error.log
-rw-r--r-- 1 web web 328K Mar 25 14:09 cloud.log
-rw-rw-r-- 1 web web 2.4G Jul  5  2024 cron.log
-rw-rw-r-- 1 web web  363 Dec  6  2023 debug.log
-rw-rw-r-- 1 web web  15K Jan 10  2024 indexation.log
-rw-r--r-- 1 web web 229K Jan 10  2024 install_upgrade.log
-rw-r--r-- 1 web web 2.9K Jul 16  2024 patch.log
-rw-rw-r-- 1 web web 2.4G Mar 25 15:36 support_report.log
-rw-rw-r-- 1 web web  516 Dec  6  2023 system.log
```

## Exemplos para o registro truncado

Depois de enviar para o projeto e ambiente corretos, altere para o diretório `var/log`. Em seguida, você pode truncar um arquivo com algo semelhante a `> some-log-file.log`

```BASH
> support_report.log 
> cron.log 
```

## Documentação relacionada

- [Notificações de integridade](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/integrations/health-notifications){target="_blank"}
