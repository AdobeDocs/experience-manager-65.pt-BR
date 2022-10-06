---
title: Aplicação de fluxos de trabalho a páginas
seo-title: Applying Workflows to Pages
description: Fluxos de trabalho podem ser iniciados no console Sites ou, ao editar uma página, no Sidekick.
seo-description: Workflows can be started from either the Websites console or, when editing a page, from Sidekick.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
exl-id: d8b604c5-a6da-47c4-9422-b519e224c7ca
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 85%

---

# Aplicação de fluxos de trabalho a páginas{#applying-workflows-to-pages}

Ao aplicar o fluxo de trabalho, você especifica as seguintes informações:

* O fluxo de trabalho a ser aplicado.

   É possível aplicar qualquer fluxo de trabalho (ao qual você tenha acesso, conforme atribuído pelo administrador do AEM).
* Opcionalmente:

   * Um comentário que forneça informações sobre por que você iniciou o fluxo de trabalho.
   * Um título que ajude a identificar a instância de fluxo de trabalho na Caixa de entrada de um usuário.

>[!NOTE]
>
>Os administradores do AEM podem iniciar fluxos de trabalho usando [vários outros métodos](/help/sites-administering/workflows-starting.md).

## Aplicação de fluxos de trabalho {#applying-workflows}

Fluxos de trabalho podem ser iniciados no console Sites ou, ao editar uma página, no Sidekick.

O **Status** na coluna **Sites** O console indica se um fluxo de trabalho foi aplicado a uma página:

![workflowstatus](assets/workflowstatus.png)

### Início de um fluxo de trabalho no console Sites {#starting-a-workflow-from-the-websites-console}

1. Abra o console Sites. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. Na árvore Sites, selecione o pai da página à qual você deseja aplicar o fluxo de trabalho.
1. Na lista de páginas, selecione a página e clique em Fluxo de trabalho.
1. Na caixa de diálogo Iniciar fluxo de trabalho, selecione o fluxo de trabalho que será aplicado. Opcionalmente, insira um comentário e um título. Em seguida, clique em Iniciar.

### Início de um fluxo de trabalho usando o Sidekick {#starting-a-workflow-using-sidekick}

1. Abra o console Sites.
1. Abra a página necessária.
1. Selecione a guia Fluxo de trabalho no Sidekick.
1. Expanda o **Fluxo de trabalho** , permitindo que você selecione o **Fluxo de trabalho** e, opcionalmente, insira **Título do fluxo de trabalho** e **Comentário**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. Clique em **Iniciar fluxo de trabalho** para iniciar uma nova instância de fluxo de trabalho com as propriedades configuradas e a página atual como carga útil. Agora, o fluxo de trabalho está em execução.
