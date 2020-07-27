---
title: Etapas genéricas para personalização da área de trabalho do AEM Forms
seo-title: Etapas genéricas para personalização da área de trabalho do AEM Forms
description: Como começar a personalizar a interface do usuário do espaço de trabalho do AEM Forms.
seo-description: Como começar a personalizar a interface do usuário do espaço de trabalho do AEM Forms.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---


# Etapas genéricas para personalização da área de trabalho do AEM Forms{#generic-steps-for-aem-forms-workspace-customization}

As etapas genéricas para executar qualquer personalização são:

1. Faça logon no CRXDE Lite acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Crie uma pasta com o nome `ws`em `/apps`, se ela não existir. Clique em **[!UICONTROL Salvar tudo]**.
1. Navegue até `/apps/ws`a guia **[!UICONTROL Controle de acesso]** e navegue até ela.
1. Na lista do **[!UICONTROL Controle de acesso]** , clique em **[!UICONTROL +]** para adicionar uma nova entrada. Clique **[!UICONTROL +]** novamente.
1. Pesquise e selecione o Principal **PERM_WORKSPACE_USER** .

   ![Selecione o principal PERM_WORKSPACE_USER como parte das etapas genéricas para personalizar a área de trabalho HTML](assets/perm_workspace_user.png)

1. Dê `jcr:read` privilégio ao diretor.
1. Clique em **[!UICONTROL Salvar tudo]**.
1. Copie os arquivos `GET.jsp` e `html.jsp`arquivos da `/libs/ws`pasta para a `/apps/ws` pasta.
1. Copie a `/libs/ws/locales` pasta na `/apps/ws` pasta. Clique em **[!UICONTROL Salvar tudo]**.
1. Atualize as referências e os caminhos relativos no `GET.jsp` arquivo, como mostrado abaixo, e clique em **[!UICONTROL Salvar tudo]**.

   ```jsp
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Faça o seguinte para personalizações de CSS:

   1. Navegue até a `/apps/ws` pasta e crie uma nova pasta chamada `css`.

   1. Na pasta da `css`pasta, crie um novo arquivo chamado `newStyle.css`.

   1. Abrir `/apps/ws/html`.jsp e alterar de

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   para

   ```css
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Coloque a entrada do arquivo CSS definido pelo usuário após a entrada de newStyle.css, como mostrado acima.

1. No arquivo /apps/ws/html.jsp, altere de

   ```css
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   para

   ```css
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Faça o seguinte:

   1. Crie uma pasta com o nome `js`em `/apps/ws`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Crie uma pasta com o nome `libs`em `/apps/ws/js`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Crie uma pasta com o nome `jqueryui`em `/apps/ws/js/libs`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copie `/libs/ws/js/libs/jqueryui/jquery.ui.datepicker-ja.js` para `/apps/ws/js/libs/jqueryui`. Clique em **[!UICONTROL Salvar tudo]**.

1. Faça o seguinte para personalizações de HTML:

   1. Em `/apps/ws/js`, crie uma pasta chamada `runtime`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Em `/apps/ws/js/runtime`, crie uma pasta chamada `templates`. Clique em **[!UICONTROL Salvar tudo]**.

   1. Copie `/libs/ws/js/main.js` para `/apps/ws/js/main.js`.

   1. Copie /libs/ws/js/registry.js para `/apps/ws/js/registry.js`.

1. Clique em **[!UICONTROL Salvar tudo]**, limpar o cache e atualizar o espaço de trabalho do AEM Forms.

   Acesse o URL `https://'[server]:[port]'/lc/ws` e faça logon com as credenciais de administrador/senha. O navegador é redirecionado para `https://'[server]:[port]'/lc/apps/ws/index.html`.
