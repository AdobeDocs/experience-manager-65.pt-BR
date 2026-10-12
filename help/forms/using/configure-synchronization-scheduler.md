---
title: Configuração do scheduler de sincronização
description: Saiba como migrar e sincronizar ativos, configurar o agendador de sincronização e usar pastas para organizar ativos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
solution: Experience Manager, Experience Manager Forms
feature: Workbench,Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 36ac8e9c-5c7a-56d8-af5e-39399fd7b101
    internal-label: Workbench
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%
---
# Configuração do scheduler de sincronização {#configuring-the-synchronization-scheduler}

Por padrão, o agendador de sincronização é executado a cada 3 minutos para sincronizar todos os ativos modificados e atualizados no repositório por meio do LiveCycle Workbench 11. Os aplicativos que contêm formulários e recursos ficam visíveis na interface do usuário do AEM Forms após a conclusão do processo de sincronização.

## Alterar intervalo do agendador de sincronização {#change-interval-of-the-synchronization-scheduler}

Execute as seguintes etapas para alterar o intervalo do scheduler de sincronização:

1. Faça logon no AEM Configuration Manager. A URL do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`

1. Localize e abra o pacote **FormsManagerConfiguration**.

1. Especifique um novo valor para a opção **Frequência do Agendador de Sincronização**.

   A unidade da frequência é minutos. Por exemplo, para configurar o scheduler para ser executado a cada 60 minutos, especifique 60.

## Sincronização de ativos {#synchronizing-assets}

Você pode usar a opção **Sincronizar Assets do Repositório** para sincronizar manualmente os ativos. Execute as seguintes etapas para sincronizar manualmente os ativos:

1. Faça logon no AEM Forms. A URL padrão é `https://'[server]:[port]'/lc/aem/forms/`.

   ![Interface de usuário do AEM Forms](assets/aem_forms_ui.png)

   **Figura:** *Interface do usuário do AEM Forms*

1. Clique no ícone ![aem6forms_sync](assets/aem6forms_sync.png) na barra de ferramentas. Se você não tiver nenhum ativo no último caminho configurado, abra a caixa de diálogo como mostrado abaixo. Clique em **Iniciar** para iniciar a sincronização.

   ![Caixa de diálogo de sincronização](assets/migrate-and-syncronize.png)

   **Figura:** *Caixa de diálogo de sincronização*

## Solução de problemas de erro de sincronização {#troubleshooting-synchronization-error}

Você pode criar novos aplicativos no designer de workflow (LiveCycle Workbench).

Se o aplicativo recém-criado e uma pasta em /content/dam/formsanddocuments tiverem nomes idênticos, um erro &quot;*Um ativo com o mesmo nome deste aplicativo já existe no nível raiz.*&quot; está registrado.

Para resolver o conflito, renomeie o aplicativo e sincronize manualmente os ativos.

![Conflitos na caixa de diálogo de sincronização de ativos](assets/sync-conflict.png)

**Figura:** *Conflitos na caixa de diálogo de sincronização de ativos*
