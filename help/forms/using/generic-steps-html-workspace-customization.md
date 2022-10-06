---
title: Etapas genéricas para personalização do espaço de trabalho do AEM Forms
seo-title: Generic steps for AEM Forms workspace customization
description: Como começar a personalizar a interface do usuário do AEM Forms workspace.
seo-description: How to get started customizing AEM Forms workspace user interface.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
exl-id: 45e50b47-1b36-4937-9e1a-cc7bfb953861
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Etapas genéricas para personalização do espaço de trabalho do AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

As etapas genéricas para executar qualquer personalização são:

1. Faça logon no CRXDE Lite acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Crie um `sling:Folder` nome da pasta `ws` at `/apps`, se não existir. Para criar um `sling:Folder` , clique com o botão direito do mouse no `apps` e selecione **[!UICONTROL Criar]** > **[!UICONTROL Criar nó]**. Especifique o nome como `ws`, selecione tipo como `sling:Folder` e clique em **[!UICONTROL OK]**. Clique em **[!UICONTROL Salvar tudo]**.
1. Navegue até `/apps/ws`e navegue até o **[!UICONTROL Controle de acesso]** guia .
1. Selecione o **[!UICONTROL Repositório]** opção. No **[!UICONTROL Controle de acesso]** listar, clique em **[!UICONTROL +]** para adicionar uma nova entrada. Clique em **[!UICONTROL +]** novamente.
1. Pesquise e selecione o **PERM_WORKSPACE_USER** Principal.

   ![Selecione PERM_WORKSPACE_USER principal como parte das etapas genéricas para personalizar o HTML Workspace](assets/perm_workspace_user.png)

1. Dar `jcr:read` privilégio do diretor.
1. Clique em **[!UICONTROL Salvar tudo]**.
1. Copie o `GET.jsp`, `index`e `html.jsp` arquivos da `/libs/ws` para `/apps/ws` pasta.
1. Copie o `/libs/ws/locales` na pasta `/apps/ws` pasta. Clique em **[!UICONTROL Salvar tudo]**.
1. Atualize as referências e os caminhos relativos na `GET.jsp` como mostrado abaixo e clique em **[!UICONTROL Salvar tudo]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Faça o seguinte para personalizações de CSS:

   1. Navegue até o `/apps/ws` e crie uma nova pasta chamada `css`.

   1. No `css` criar um novo arquivo chamado `newStyle.css`.

   1. Abrir `/apps/ws/html`.jsp e alterar de

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
   >Coloque a entrada do arquivo CSS definido pelo usuário após a entrada de style.css, conforme mostrado acima.

1. No arquivo /apps/ws/html.jsp, altere de

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   para

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Faça o seguinte:

   1. Crie uma pasta chamada `js` at `/apps/ws`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Crie uma pasta chamada `libs` at `/apps/ws/js`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copiar `/libs/ws/js/libs/jqueryui` pasta para `/apps/ws/js/libs`. Clique em **[!UICONTROL Salvar tudo]**.

1. Faça o seguinte para personalizações de HTML:

   1. Em `/apps/ws/js`, crie uma pasta chamada `runtime`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Em `/apps/ws/js/runtime`, crie uma pasta chamada `templates`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copiar `/libs/ws/js/main.js` para `/apps/ws/js/main.js`.

   1. Copiar /libs/ws/js/registry.js para `/apps/ws/js/registry.js`.

1. Clique em **[!UICONTROL Salvar tudo]**, limpe o cache e atualize o espaço de trabalho do AEM Forms.

   Acessar o URL `https://'[server]:[port]'/lc/ws` e faça logon com credenciais de administrador/senha. O navegador redireciona para `https://'[server]:[port]'/lc/apps/ws/index.html`.
