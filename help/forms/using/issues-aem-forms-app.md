---
title: Solução de problemas do aplicativo AEM Forms
description: Saiba mais sobre problemas comuns com o aplicativo AEM Forms e como solucioná-los.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Solução de problemas do aplicativo AEM Forms {#troubleshoot-aem-forms-app}

Este artigo descreve as mensagens de erro que podem ser exibidas ao criar o aplicativo AEM Forms e as etapas para resolvê-las.

As seções neste artigo incluem:

* [Perda de anexos para usuários do iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [os rascunhos do formulário HTML5 enviados pelos usuários do espaço de trabalho não estão visíveis no portal](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Falha ao carregar formulários HTML5 (não em cache) no aplicativo AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [O AEM Forms não é sincronizado no Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versão do Gradle não suportada](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemas de compatibilidade do plug-in Gradle e Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perda de anexos para usuários do iOS {#attachment-loss-for-ios-users}

O aplicativo AEM Forms para iOS configurado para sincronização com o AEM Forms no OSGi é compatível somente com anexos em nível de campo. Todos os anexos devem ter nomes exclusivos. Se vários anexos tiverem nomes idênticos, apenas um anexo será mantido e todos os outros com nomes idênticos serão perdidos. Execute as seguintes etapas para impedir que os usuários em dispositivos iOS sofram perda de dados:

1. No servidor conectado, navegue até **Adobe Experience Manager > Ferramentas > Operações > Console da Web**.
1. Localize e clique em **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]**.
1. Na caixa de diálogo [!UICONTROL Configuração do Canal da Web de Formulário Adaptável e Comunicação Interativa], habilite **Tornar os Nomes de Arquivos Exclusivos**.

   Se a configuração **Tornar os Nomes de Arquivos Exclusivos** estiver desabilitada, os usuários sofrerão perda de dados se tentarem enviar formulários adaptáveis com vários anexos.

1. Clique em **Salvar**.

## os rascunhos do formulário HTML5 enviados pelos usuários do espaço de trabalho não estão visíveis no portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Para formulários HTML5 habilitados no aplicativo AEM Forms com **Salvar como rascunho** Perfil de Renderização de HTML, os rascunhos salvos não ficam visíveis para usuários do espaço de trabalho. Para exibir os rascunhos salvos de formulários do HTML5 enviados pelos usuários do espaço de trabalho no portal, execute as seguintes etapas:

1. Abra o CRXDE e faça logon com credenciais de administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. No caminho raiz do CRXDE, na Lista de Controle de Acesso, em Controle de Acesso, clique em **+**.
1. Na caixa de diálogo **Adicionar nova entrada**, clique no botão de pesquisa de grupo no campo Principal.
1. No campo Nome da caixa de diálogo Selecionar Entidade, digite `PERM_WORKSPACE_USER` e clique em **Pesquisar**.
1. Selecione o grupo `PERM_WORKSPACE_USER` na caixa de diálogo Selecionar Entidade e clique em **OK**.
1. Na caixa de diálogo Adicionar nova entrada, o grupo `PERM_WORKSPACE_USER` é selecionado no campo Principal.

   Habilitar privilégios de `jcr:read` para o grupo de usuários.

1. Clique em **OK**.

## Falha ao carregar formulários HTML5 (não em cache) no aplicativo AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando o aplicativo AEM Forms é conectado a uma versão mais antiga do servidor AEM Forms, os formulários HTML5 não armazenados em cache não são carregados no aplicativo AEM Forms.

Execute as seguintes etapas para resolver o problema:

1. Na instância do autor, navegue até **Adobe Experience Manager > Ferramentas > Configurar serviço offline do aplicativo Workspace > Configurar agora**.
1. Na página **Serviço Offline do Aplicativo Workspace**, clique em **Cache de Recursos Manual**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Na guia **Cache de Recursos Manual**, clique no botão **+** para adicionar um caminho CRX.
1. No campo **Adicionar Novo Recurso**, digite: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e clique em **Adicionar**.
1. Clique em **Salvar**.

## O AEM Forms não é sincronizado no Windows {#aem-forms-do-not-sync-on-windows}

No aplicativo AEM Forms no Windows, um formulário não é sincronizado com o servidor conectado se o caminho do formulário ou de qualquer um de seus recursos contiver mais de ou igual a 256 caracteres.

Modifique o caminho do formulário e seus recursos para reduzir o número de caracteres para menos de 256 caracteres.

## Versão do Gradle não suportada {#unsupported-version-of-gradle}

**Mensagem de erro:** o projeto está usando uma versão sem suporte do Gradle.

A mensagem de erro é exibida ao criar o aplicativo AEM Forms no Android Studio. O problema ocorre devido a uma versão não compatível do Gradle com suporte no sistema.

**Solução:** clique em **Corrigir Gradle wrapper e reimportar projeto** para resolver o problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemas de compatibilidade do plug-in Gradle e Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Mensagem de Erro:** As versões do plug-in e do Gradle do Android não são compatíveis.

A mensagem de erro é exibida ao selecionar a opção **Build APK** no menu **Build** da interface do usuário do Android Studio.

![compatibilidade_de_plug-in_de_gradle](assets/gradle_plugin_compatibility.png)

**Solução:** Abra o arquivo **Gradle Scripts** > **gradle-wrapper.properties** e edite a propriedade **distributionUrl**.

Por exemplo, o console do Android Studio recomenda baixar a versão Gradle para 3.5. Edite a versão em **distributionUrl** de **arquivo gradle-wrapper.properties**.

Selecione **Build** > **Build APK** novamente para resolver o erro e gerar o arquivo .apk.

![propriedades_do_wrapper_de_gradle](assets/gradle_wrapper_properties.png)
