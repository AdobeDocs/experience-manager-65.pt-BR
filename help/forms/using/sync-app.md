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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Sincronização do aplicativo{#synchronizing-the-app}

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
* No .js, a chamada para a função processOfflineSubmittedSavedTasks(...) envia as tarefas salvas/enviadas para o servidor. Também lida com erros ou conflitos no processo de sincronização. Se o envio de uma tarefa falhar, a tarefa no aplicativo será marcada como com falha. Além disso, a tarefa permanece na Caixa de saída.
* As funções syncSubmittedTask() e syncSavedTask() executam operações em tarefas individuais.
* A chamada para a função processOfflineSubmittedSavedTasks() é iniciada pelo componente de lista de tarefas depois que um usuário seleciona sincronizar o estado offline para o servidor ou uma sincronização automática pelo thread em segundo plano.
