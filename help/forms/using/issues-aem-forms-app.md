---
title: Solução de problemas do aplicativo AEM Forms
description: Saiba mais sobre problemas comuns com o aplicativo AEM Forms e como solucioná-los.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
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
1. No [!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa] caixa de diálogo, ativar **Tornar Nomes de Arquivos Exclusivos**.

   Se **Tornar Nomes de Arquivos Exclusivos** estiver desativada, os usuários sofrerão perda de dados se tentarem enviar formulários adaptáveis com vários anexos.

1. Clique em **Salvar**.

## os rascunhos do formulário HTML5 enviados pelos usuários do espaço de trabalho não estão visíveis no portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Para formulários HTML5 ativados no aplicativo AEM Forms com **Salvar como rascunho** Perfil de renderização do HTML, os rascunhos salvos não estarão visíveis para os usuários do espaço de trabalho. Para exibir os rascunhos salvos de formulários do HTML5 enviados pelos usuários do espaço de trabalho no portal, execute as seguintes etapas:

1. Abra o CRXDE e faça logon com credenciais de administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. No caminho raiz do CRXDE, na Lista de controle de acesso em Controle de acesso, clique em **+**.
1. No **Adicionar nova entrada** clique no botão de pesquisa do grupo no campo Principal.
1. No campo Nome da caixa de diálogo Selecionar principal, digite `PERM_WORKSPACE_USER` e clique em **Pesquisar**.
1. Selecionar `PERM_WORKSPACE_USER` grupo na caixa de diálogo Selecionar principal e clique em **OK**.
1. No diálogo Adicionar nova entrada, `PERM_WORKSPACE_USER` O grupo é selecionado no campo Principal.

   Ativar `jcr:read` privilégios para o grupo de usuários.

1. Clique em **OK**.

## Falha ao carregar formulários HTML5 (não em cache) no aplicativo AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando o aplicativo AEM Forms é conectado a uma versão mais antiga do servidor AEM Forms, os formulários HTML5 não armazenados em cache não são carregados no aplicativo AEM Forms.

Execute as seguintes etapas para resolver o problema:

1. Na instância do autor, navegue até **Adobe Experience Manager > Ferramentas > Configurar serviço off-line do aplicativo do Workspace > Configurar agora**.
1. Entrada **Serviço Offline do Aplicativo Workspace** clique em **Cache de recursos manuais**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. No **Cache de recursos manuais** clique na guia **+** botão para adicionar um caminho CRX.
1. No **Adicionar um novo recurso** digite: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e clique em **Adicionar**.
1. Clique em **Salvar**.

## O AEM Forms não é sincronizado no Windows {#aem-forms-do-not-sync-on-windows}

No aplicativo AEM Forms no Windows, um formulário não é sincronizado com o servidor conectado se o caminho do formulário ou de qualquer um de seus recursos contiver mais de ou igual a 256 caracteres.

Modifique o caminho do formulário e seus recursos para reduzir o número de caracteres para menos de 256 caracteres.

## Versão do Gradle não suportada {#unsupported-version-of-gradle}

**Mensagem de erro:** O projeto está usando uma versão não suportada do Gradle.

A mensagem de erro é exibida ao criar o aplicativo AEM Forms no Android Studio. O problema ocorre devido a uma versão não compatível do Gradle com suporte no sistema.

**Resolução:** Clique em **Corrigir invólucro Gradle e reimportar projeto** para resolver o problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemas de compatibilidade do plug-in Gradle e Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Mensagem de erro:** As versões do plug-in Android Gradle e Gradle não são compatíveis.

A mensagem de erro é exibida ao selecionar **Criar APK** opção no **Build** na interface do usuário do Android Studio.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**Resolução:** Abertura **Scripts Gradle** > **gradle-wrapper.properties** arquivo e edite o **distributionUrl** propriedade.

Por exemplo, o console do Android Studio recomenda baixar a versão Gradle para 3.5. Editar a versão no **distributionUrl** de **gradle-wrapper.properties** arquivo.

Selecionar **Build** > **Criar APK** novamente para resolver o erro e gerar o arquivo .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
