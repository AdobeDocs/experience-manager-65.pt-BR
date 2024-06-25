---
title: Etapas genéricas para personalização do espaço de trabalho do AEM Forms
description: Introdução à personalização da interface do usuário do espaço de trabalho do Adobe Experience Manager Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Etapas genéricas para personalização do espaço de trabalho do AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

As etapas genéricas para executar qualquer personalização são:

1. Faça logon no CRXDE Lite acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Criar um `sling:Folder` pasta nomeada `ws` em `/apps`, se não existir. Para criar um `sling:Folder` , clique com o botão direito do mouse na `apps` e selecione **[!UICONTROL Criar]** > **[!UICONTROL Criar nó]**. Especifique o nome como `ws`, selecione tipo como `sling:Folder`e clique em **[!UICONTROL OK]**. Clique em **[!UICONTROL Salvar tudo]**.
1. Navegue até `/apps/ws`e navegue até o **[!UICONTROL Controle de acesso]** guia.
1. Selecione o **[!UICONTROL Repositório]** opção. No **[!UICONTROL Controle de acesso]** clique em **[!UICONTROL +]** para adicionar uma entrada. Clique em **[!UICONTROL +]** novamente.
1. Pesquise e selecione o **PERM_WORKSPACE_USER** Principal.

   ![Selecione PRINCIPAL PERM_WORKSPACE_USER como parte das etapas genéricas para personalizar o HTML Workspace](assets/perm_workspace_user.png)

1. Conceder `jcr:read` ao responsável principal.
1. Clique em **[!UICONTROL Salvar tudo]**.
1. Copie o `GET.jsp`, `index`, e `html.jsp` arquivos do `/libs/ws` pasta para a `/apps/ws` pasta.
1. Copie o `/libs/ws/locales` pasta na `/apps/ws` pasta. Clique em **[!UICONTROL Salvar tudo]**.
1. Atualize as referências e os caminhos relativos no `GET.jsp` conforme mostrado abaixo e clique em **[!UICONTROL Salvar tudo]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Faça o seguinte para personalizações de CSS:

   1. Navegue até a `/apps/ws` e crie uma pasta chamada `css`.

   1. No `css` , crie um arquivo chamado `newStyle.css`.

   1. Abertura `/apps/ws/html`.jsp e alterar de

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   para

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Coloque a entrada do arquivo CSS definido pelo usuário após a entrada de style.css, como mostrado acima.

1. No arquivo /apps/ws/html.jsp, altere de

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   para

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Faça o seguinte:

   1. Crie uma pasta chamada `js` em `/apps/ws`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Crie uma pasta chamada `libs` em `/apps/ws/js`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copiar `/libs/ws/js/libs/jqueryui` pasta para `/apps/ws/js/libs`. Clique em **[!UICONTROL Salvar tudo]**.

1. Faça o seguinte para personalizações de HTML:

   1. Em `/apps/ws/js`, crie uma pasta chamada `runtime`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Em `/apps/ws/js/runtime`, crie uma pasta chamada `templates`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copiar `/libs/ws/js/main.js` para `/apps/ws/js/main.js`.

   1. Copiar /libs/ws/js/registry.js para `/apps/ws/js/registry.js`.

1. Clique em **[!UICONTROL Salvar tudo]**, limpar o cache e atualizar o espaço de trabalho do AEM Forms.

   Acessar o URL `https://'[server]:[port]'/lc/ws` e faça logon com credenciais de administrador/senha. O navegador redireciona para `https://'[server]:[port]'/lc/apps/ws/index.html`.
