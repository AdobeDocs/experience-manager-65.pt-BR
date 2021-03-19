---
title: Configurar o agendador de sincronização
seo-title: Configurar o agendador de sincronização
description: Saiba como migrar e sincronizar ativos, configurar o agendador de sincronização e usar pastas para organizar ativos.
seo-description: Saiba como migrar e sincronizar ativos, configurar o agendador de sincronização e usar pastas para organizar ativos.
uuid: b2c89feb-2947-418a-b343-4c01e453602b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 8c8b1998-eab4-4230-b24f-5e96883ba599
docset: aem65
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Configurar o agendador de sincronização {#configuring-the-synchronization-scheduler}

Por padrão, o agendador de sincronização é executado após cada 3 minutos para sincronizar todos os ativos modificados e atualizados no repositório por meio do LiveCycle Workbench 11. Os aplicativos que contêm formulários e recursos ficam visíveis na interface do usuário do AEM Forms após a conclusão do processo de sincronização.

## Alterar intervalo do agendador de sincronização {#change-interval-of-the-synchronization-scheduler}

Execute as seguintes etapas para alterar o intervalo do agendador de sincronização:

1. Faça logon no AEM Configuration Manager. O URL do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Localize e abra o pacote **FormsManagerConfiguration**.

1. Especifique um novo valor para a opção **Frequência do Agendador de Sincronização**.

   A unidade da frequência é minutos. Por exemplo, para configurar o scheduler para ser executado após cada 60 minutos, especifique 60.

## Sincronizar ativos {#synchronizing-assets}

Você pode usar a opção **Sincronizar ativos do repositório** para sincronizar manualmente os ativos. Execute as seguintes etapas para sincronizar manualmente os ativos:

1. Faça logon no AEM Forms. O URL padrão é `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interface do usuário do AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *Interface do usuário do AEM Forms*

1. Clique no ícone ![aem6forms_sync](assets/aem6forms_sync.png) na barra de ferramentas. Se você não tiver ativos no caminho configurado pela última vez, a caixa de diálogo será exibida abaixo. Clique em **Start** para iniciar a sincronização.

   ![Caixa de diálogo Sincronização](assets/migrate-and-syncronize.png)

   **Figura: Caixa de diálogo** *Sincronização*

## Resolução de problemas do erro de sincronização {#troubleshooting-synchronization-error}

Você pode criar novos aplicativos no designer de workflow (LiveCycle Workbench).

Se o aplicativo recém-criado e uma pasta em /content/dam/formsanddocuments tiver um nome idêntico, um erro &quot;*Um ativo com o mesmo nome desse aplicativo já existe no nível raiz.*&quot; está registrado.

Para resolver o conflito, renomeie o aplicativo e sincronize manualmente os ativos.

![Conflitos na caixa de diálogo sincronização de ativos](assets/sync-conflict.png)

**Figura:** *Conflitos na caixa de diálogo de sincronização de ativos*
