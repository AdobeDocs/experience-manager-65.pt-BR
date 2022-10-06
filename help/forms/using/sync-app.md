---
title: Sincronização do aplicativo
seo-title: Synchronizing the app
description: Sincronize o aplicativo AEM Forms em seu dispositivo móvel com o servidor AEM Forms.
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# Sincronização do aplicativo{#synchronizing-the-app}

## Sincronização do aplicativo {#synchronizing-the-app-1}

Os formulários no seu aplicativo são baixados do servidor do AEM Forms. Os formulários são baixados nas guias Tarefas e Forms . Os rascunhos criados a partir de formulários são baixados na guia rascunhos e os rascunhos criados a partir de tarefas são baixados na guia tarefas . Para um formulário independente no servidor OSGi, os formulários e rascunhos são baixados nas guias Forms e Rascunho , respectivamente.

Quando você preenche e envia um formulário, o formulário é carregado de volta ao servidor da AEM Forms instantaneamente se o aplicativo estiver online. Os formulários são buscados no servidor quando o aplicativo é sincronizado. Os rascunhos, no entanto, são sincronizados instantaneamente com o servidor se o aplicativo estiver online.

Por padrão, quando você está online com o servidor do AEM Forms, seu aplicativo é sincronizado a cada 15 minutos. No entanto, você tem a opção de alterar a frequência de sincronização. Como alternativa, você pode sincronizar manualmente o aplicativo a qualquer momento.

**Para sincronizar o aplicativo manualmente**

Toque no botão Sincronizar ![sync-app](assets/sync-app.png) no canto inferior direito da tela inicial.

**Para alterar a frequência de sincronização**

1. Para ir para a tela Definição, toque no botão de menu no canto superior esquerdo do ecrã inicial e toque em **Configurações**.
1. Na tela Configurações , toque na guia Geral .

   ![Configuração de frequência de sincronização na janela Configurações gerais](assets/gen-settings-2.png)

1. Na opção Sync frequency , toque no valor à direita de Sync frequency .
1. Na lista suspensa, selecione a nova frequência de sincronização.

### Especificações técnicas {#technical-specifications}

* A lógica principal de enviar os dados do aplicativo offline para o servidor do AEM Forms está incluída em runtime/offline/util/offline.js.
* No .js, a chamada para a função processOfflineSubmitedSavedTasks(..) envia as tarefas salvas / enviadas ao servidor. Ele também lida com erros ou conflitos no processo de sincronização. Se o envio de uma tarefa falhar, a tarefa no aplicativo será marcada como falha. Além disso, a tarefa permanece em sua Caixa de saída.
* As funções syncSubmitedTask() e syncSavedTask() executam operações em tarefas individuais.
* A chamada para a função processOfflineSubmitedSavedTasks() é iniciada pelo componente de lista de tarefas depois que um usuário seleciona para sincronizar o estado offline com o servidor ou uma sincronização automática pelo thread em segundo plano.
