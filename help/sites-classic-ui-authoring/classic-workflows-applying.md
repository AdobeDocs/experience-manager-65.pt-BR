---
title: Aplicação de fluxos de trabalho a páginas
description: Os fluxos de trabalho podem ser iniciados no console Sites ou, ao editar uma página, no Sidekick.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 14%
---
# Aplicação de fluxos de trabalho a páginas{#applying-workflows-to-pages}

Ao aplicar o fluxo de trabalho, especifique as seguintes informações:

* O fluxo de trabalho a ser aplicado.

  É possível aplicar qualquer fluxo de trabalho (ao qual você tenha acesso, conforme atribuído pelo administrador do AEM).
* Opcionalmente:

  * Um comentário que fornece informações sobre por que você iniciou o fluxo de trabalho.
  * Um título que ajuda a identificar a instância do fluxo de trabalho na Caixa de entrada de um usuário.

>[!NOTE]
>
>Os administradores do AEM podem iniciar fluxos de trabalho usando [vários outros métodos](/help/sites-administering/workflows-starting.md).

## Aplicação de fluxos de trabalho {#applying-workflows}

Os fluxos de trabalho podem ser iniciados no console Sites ou, ao editar uma página, no Sidekick.

A coluna **Status** no console **Sites** indica se um fluxo de trabalho foi aplicado a uma página:

![status do fluxo de trabalho](assets/workflowstatus.png)

### Iniciar um fluxo de trabalho a partir do console Sites {#starting-a-workflow-from-the-websites-console}

1. Abra o console Sites. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. Na árvore Sites, selecione a página principal à qual deseja aplicar o fluxo de trabalho.
1. Na lista da página, selecione a página e clique em Fluxo de trabalho.
1. Na caixa de diálogo Iniciar fluxo de trabalho, selecione o fluxo de trabalho a ser aplicado. Opcionalmente, insira um comentário e um título. Em seguida, clique em Start.

### Iniciar um fluxo de trabalho usando o Sidekick {#starting-a-workflow-using-sidekick}

1. Abra o console Sites.
1. Abra a página desejada.
1. Selecione a guia Fluxo de trabalho no Sidekick.
1. Expanda a caixa de diálogo **Fluxo de Trabalho**, que permite selecionar o **Fluxo de Trabalho** e, opcionalmente, inserir o **Título do Fluxo de Trabalho** e o **Comentário**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. Clique em **Iniciar Fluxo de Trabalho** para iniciar uma nova instância de fluxo de trabalho com as propriedades que você configurou e a página atual como carga. Agora, o workflow está em execução.
