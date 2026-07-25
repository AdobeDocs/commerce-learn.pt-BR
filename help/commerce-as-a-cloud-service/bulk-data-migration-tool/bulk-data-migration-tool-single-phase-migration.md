---
title: Ferramenta de migração de dados em massa - Migração de fase única
description: Saiba como executar uma migração de fase única com a Ferramenta de migração de dados em massa para execuções tranquilas e ambientes em que a origem pode permanecer ativa durante a extração.
role: Developer
level: Intermediate
doc-type: Technical Video
topic: Migration
feature: Data Import/Export
duration: 737
last-substantial-update: 2026-07-24T00:00:00Z
jira: KT-22139
source-git-commit: 838387ffddbd8bee3ef3ec22694818eb2de5fe2d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Executar uma migração de fase única com a Ferramenta de migração de dados em massa

Execute uma migração de fase única quando o ambiente de origem puder permanecer ativo durante a extração — ideal para execuções secas e ambientes de desenvolvimento ou sandbox. Se você precisar de uma origem congelada, como uma transferência de produção em que novos pedidos não podem ser recebidos no meio da migração, assista ao vídeo de migração em fases nesta série.

## Para quem é este vídeo?

* Arquiteto de soluções
* Engenheiro de DevOps
* Desenvolvedor de backend

## Conteúdo de vídeo

* Compilar a imagem do Docker com `bin console build` — só execute novamente se o Docker for alterado.
* Para iniciar o gerenciador de contêineres CLI do CDMS, execute `bin console start` e abra um shell no contêiner uma vez para baixar suas dependências.
* Para executar o pipeline de dez etapas completo, execute `bin console migration`: verifique a configuração, inicialize o ambiente, abra túneis PaaS, execute testes de integração, registre-se no CDMS, analise o esquema de destino, gere dados de teste, extraia dados de origem, carregue no ACCS, verifique as somas de verificação, limpe e resuma.
* Verifique o relatório de resumo da migração — a etapa 8 (verificação da integridade dos dados) registra falhas sem interromper o pipeline, de modo que uma execução concluída não garanta uma verificação limpa.
* Esse comando monofásico é um pipeline completo e independente — não o use como uma etapa no fluxo de trabalho do modo de manutenção (migração em fases), que tem seus próprios comandos dedicados.

>[!VIDEO](https://video.tv.adobe.com/v/3496320?captions=por_br&learn=on)
