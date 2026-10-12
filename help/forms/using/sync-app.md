---
title: Sincronização do aplicativo
description: Sincronize o aplicativo AEM Forms no dispositivo móvel com o servidor do AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%
---
# Sincronização do aplicativo{#synchronizing-the-app}

>[!NOTE]
>
>O aplicativo AEM Forms está obsoleto no momento. Para perguntas ou ajuda, contate [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

## Sincronização do aplicativo {#synchronizing-the-app-1}

Os formulários no aplicativo são baixados do servidor do AEM Forms. Os formulários são baixados nas guias Tarefas e Forms. Os rascunhos criados em formulários são baixados na guia rascunhos, e os rascunhos criados em tarefas são baixados na guia tarefas. Para um formulário independente no servidor OSGi, os formulários e rascunhos são baixados nas guias Forms e Rascunho, respectivamente.

Quando você preenche e envia um formulário, ele é carregado de volta ao servidor do AEM Forms instantaneamente, se o aplicativo estiver online. Os formulários são obtidos do servidor quando o aplicativo é sincronizado. Os rascunhos, no entanto, são sincronizados com o servidor instantaneamente se o aplicativo estiver online.

Quando você está online com o servidor do AEM Forms, por padrão, seu aplicativo é sincronizado a cada 15 minutos. No entanto, você tem a opção de alterar a frequência de sincronização. Como alternativa, você pode sincronizar manualmente o aplicativo a qualquer momento.

**Para sincronizar o aplicativo manualmente**

Selecione o botão Sincronizar ![sync-app](assets/sync-app.png) no canto inferior direito da tela inicial.

**Para alterar a frequência de sincronização**

1. Para ir para a tela Configuração, selecione o botão de menu no canto superior esquerdo da tela inicial e selecione **Configurações**.
1. Na tela Settings, selecione a guia General.

   ![Configuração de frequência de sincronização na janela Configurações Gerais](assets/gen-settings-2.png)

1. Na opção Sync frequency, selecione o valor à direita de Sync frequency.
1. Na lista suspensa, selecione a nova frequência de sincronização.

### Especificações técnicas {#technical-specifications}

* A lógica principal de enviar os dados do aplicativo offline para o servidor do AEM Forms está incluída em runtime/offline/util/offline.js.
* No .js, a chamada para processOfflineSubmittedSavedTasks(...) envia as tarefas salvas/enviadas para o servidor. Também lida com erros ou conflitos no processo de sincronização. Se o envio de uma tarefa falhar, a tarefa no aplicativo será marcada como com falha. Além disso, a tarefa permanece na Caixa de saída.
* As funções syncSubmittedTask() e syncSavedTask() executam operações em tarefas individuais.
* A chamada para a função processOfflineSubmittedSavedTasks() é iniciada pelo componente de lista de tarefas depois que um usuário seleciona sincronizar o estado offline para o servidor ou uma sincronização automática pelo thread em segundo plano.
