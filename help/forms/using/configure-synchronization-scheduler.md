---
title: Configuração do scheduler de sincronização
description: Saiba como migrar e sincronizar ativos, configurar o agendador de sincronização e usar pastas para organizar ativos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Configuração do scheduler de sincronização {#configuring-the-synchronization-scheduler}

Por padrão, o agendador de sincronização é executado a cada 3 minutos para sincronizar todos os ativos modificados e atualizados no repositório por meio do LiveCycle Workbench 11. Os aplicativos que contêm formulários e recursos ficam visíveis na interface do usuário do AEM Forms após a conclusão do processo de sincronização.

## Alterar intervalo do agendador de sincronização {#change-interval-of-the-synchronization-scheduler}

Execute as seguintes etapas para alterar o intervalo do scheduler de sincronização:

1. Faça logon no Gerenciador de configuração do AEM. O URL do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Localize e abra o **FormsManagerConfiguration** pacote.

1. Especifique um novo valor para a variável **Frequência do Agendador de Sincronização** opção.

   A unidade da frequência é minutos. Por exemplo, para configurar o scheduler para ser executado a cada 60 minutos, especifique 60.

## Sincronização de ativos {#synchronizing-assets}

Você pode usar o **Sincronizar ativos do repositório** opção para sincronizar manualmente os ativos. Execute as seguintes etapas para sincronizar manualmente os ativos:

1. Faça logon no AEM Forms. O URL padrão é `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interface do usuário do AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *Interface do usuário do AEM Forms*

1. Clique em ![aem6forms_sync](assets/aem6forms_sync.png) na barra de ferramentas. Se você não tiver nenhum ativo no último caminho configurado, abra a caixa de diálogo como mostrado abaixo. Clique em **Início** para iniciar a sincronização.

   ![Caixa de diálogo Sincronização](assets/migrate-and-syncronize.png)

   **Figura:** *Caixa de diálogo Sincronização*

## Solução de problemas de erro de sincronização {#troubleshooting-synchronization-error}

Você pode criar novos aplicativos no designer do workflow (LiveCycle Workbench).

Se o aplicativo recém-criado e uma pasta em /content/dam/formsanddocuments tiverem um nome idêntico, um erro &quot;*Um ativo com o mesmo nome deste aplicativo já existe no nível raiz.*&quot; está registrado.

Para resolver o conflito, renomeie o aplicativo e sincronize manualmente os ativos.

![Conflitos na caixa de diálogo de sincronização de ativos](assets/sync-conflict.png)

**Figura:** *Conflitos na caixa de diálogo de sincronização de ativos*
