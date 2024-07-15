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
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Configuração do scheduler de sincronização {#configuring-the-synchronization-scheduler}

Por padrão, o agendador de sincronização é executado a cada 3 minutos para sincronizar todos os ativos modificados e atualizados no repositório por meio do LiveCycle Workbench 11. Os aplicativos que contêm formulários e recursos ficam visíveis na interface do usuário do AEM Forms após a conclusão do processo de sincronização.

## Alterar intervalo do agendador de sincronização {#change-interval-of-the-synchronization-scheduler}

Execute as seguintes etapas para alterar o intervalo do scheduler de sincronização:

1. Faça logon no Gerenciador de configuração do AEM. A URL do Configuration Manager é `https://'[server]:[port]'/lc/system/console/configMgr`

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

Você pode criar novos aplicativos no designer do workflow (LiveCycle Workbench).

Se o aplicativo recém-criado e uma pasta em /content/dam/formsanddocuments tiverem um nome idêntico, um erro &quot;*Um ativo com o mesmo nome deste aplicativo já existe no nível raiz.* está registrado.

Para resolver o conflito, renomeie o aplicativo e sincronize manualmente os ativos.

![Conflitos na caixa de diálogo de sincronização de ativos](assets/sync-conflict.png)

**Figura:** *Conflitos na caixa de diálogo de sincronização de ativos*
