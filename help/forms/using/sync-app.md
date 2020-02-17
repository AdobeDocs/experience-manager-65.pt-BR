---
title: Sincronizar o aplicativo
seo-title: Sincronizar o aplicativo
description: Sincronize o aplicativo AEM Forms em seu dispositivo móvel com o servidor AEM Forms.
seo-description: Sincronize o aplicativo AEM Forms em seu dispositivo móvel com o servidor AEM Forms.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Sincronizar o aplicativo{#synchronizing-the-app}

## Sincronizar o aplicativo {#synchronizing-the-app-1}

Os formulários no aplicativo são baixados do servidor de formulários AEM. Os formulários são baixados nas guias Tarefas e Formulários. Os rascunhos criados a partir de formulários são baixados na guia rascunhos e os rascunhos criados a partir de tarefas são baixados na guia tarefas. Para um formulário independente no servidor OSGi, os formulários e rascunhos são baixados nas guias Formulários e Rascunho, respectivamente.

Quando você preenche e envia um formulário, o formulário é carregado de volta ao servidor do AEM Forms instantaneamente se o aplicativo estiver online. Os formulários são obtidos do servidor quando o aplicativo é sincronizado. No entanto, os rascunhos são sincronizados com o servidor instantaneamente se o aplicativo estiver online.

Por padrão, quando você está online com o servidor do AEM Forms, seu aplicativo é sincronizado a cada 15 minutos. No entanto, você tem a opção de alterar a frequência de sincronização. Como alternativa, você pode sincronizar manualmente o aplicativo a qualquer momento.

**Para sincronizar o aplicativo manualmente**

Toque no botão Sincronizar aplicativo ![de](assets/sync-app.png) sincronização no canto inferior direito da tela inicial.

**Alteração da frequência de sincronização**

1. Para acessar a tela Setting (Configuração), toque no botão de menu no canto superior esquerdo da tela Home (Início) e, em seguida, toque em **Settings (Configurações)**.
1. Na tela Configurações, toque na guia Geral.

   ![Configuração de frequência de sincronização na janela Configurações gerais](assets/gen-settings-2.png)

1. Na opção Frequência de sincronização, toque no valor à direita de Frequência de sincronização.
1. Na lista suspensa, selecione a nova frequência de sincronização.

### Especificações técnicas {#technical-specifications}

* A lógica principal de enviar os dados do aplicativo offline para o servidor do AEM Forms está incluída em runtime/offline/util/offline.js.
* Na função .js, a chamada para a função processOfflineSubmitedSavedTasks(...) envia as tarefas salvas / enviadas ao servidor. Também lida com erros ou conflitos no processo de sincronização. Se o envio de uma tarefa falhar, a tarefa no aplicativo será marcada como com falha. Além disso, a tarefa permanece em sua Caixa de saída.
* As funções syncSubmitedTask() e syncSavedTask() executam operações em tarefas individuais.
* A chamada para a função processOfflineSubmitedSavedTasks() é iniciada pelo componente da lista de tarefas depois que um usuário seleciona para sincronizar o estado offline com o servidor ou uma sincronização automática pelo thread em segundo plano.

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
