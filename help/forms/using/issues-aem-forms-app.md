---
title: Solução de problemas do aplicativo AEM Forms
seo-title: Troubleshoot AEM Forms app
description: Saiba mais sobre problemas comuns com o aplicativo AEM Forms e como solucioná-los.
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# Solução de problemas do aplicativo AEM Forms {#troubleshoot-aem-forms-app}

Este artigo descreve as mensagens de erro que podem ser exibidas durante a criação do aplicativo AEM Forms e as etapas para resolvê-las.

As seções neste artigo incluem:

* [Perda de anexo para usuários do iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Os rascunhos de formulário HTML5 enviados por usuários do espaço de trabalho não estão visíveis no portal](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Falha ao carregar formulários do HTML5 (não armazenados em cache) no aplicativo AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms não sincroniza no Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versão não suportada do Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemas de compatibilidade do plug-in Gradle e Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perda de anexo para usuários do iOS {#attachment-loss-for-ios-users}

O aplicativo AEM Forms para iOS configurado para sincronização com AEM Forms no OSGi é compatível somente com anexos no nível do campo. Todos os anexos devem ter nomes exclusivos. Se vários anexos tiverem um nome idêntico, apenas um anexo será mantido e todos os outros com um nome idêntico serão perdidos. Execute as seguintes etapas para impedir que os usuários de dispositivos iOS sofram perda de dados:

1. No servidor conectado, navegue até **Adobe Experience Manager > Ferramentas > Operações > Console da Web**.
1. Localizar e clicar em **[!UICONTROL Configuração do canal Web de comunicação interativa e formulário adaptável]**.
1. No [!UICONTROL Configuração do canal Web de comunicação interativa e formulário adaptável] caixa de diálogo, habilitar **Tornar Nomes de Arquivos Exclusivos**.

   If **Tornar Nomes de Arquivos Exclusivos** estiver desativada, os usuários sofrerão perda de dados se tentarem enviar formulários adaptáveis com vários anexos.

1. Clique em **Salvar**.

## Os rascunhos de formulário HTML5 enviados por usuários do espaço de trabalho não estão visíveis no portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Para formulários do HTML5 ativados no aplicativo AEM Forms com **Salvar como rascunho** Perfil de renderização de HTML, os rascunhos salvos não ficam visíveis para os usuários do espaço de trabalho. Para exibir rascunhos salvos de formulários HTML5 enviados por usuários do espaço de trabalho no portal, execute as seguintes etapas:

1. Abra o CRXDE e faça logon com credenciais de administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. No caminho raiz do CRXDE, na Lista de Controle de Acesso em Controle de Acesso, clique em **+**.
1. No **Adicionar nova entrada** clique no botão de pesquisa do grupo no campo Principal.
1. No campo Nome da caixa de diálogo Selecionar principal, digite `PERM_WORKSPACE_USER` e clique em **Pesquisar**.
1. Selecionar `PERM_WORKSPACE_USER` na caixa de diálogo Selecionar principal e clique em **OK**.
1. Na caixa de diálogo Adicionar nova entrada , `PERM_WORKSPACE_USER` está selecionado no campo Principal.

   Habilitar `jcr:read` privilégios para o grupo de usuários.

1. Clique em **OK**.

## Falha ao carregar formulários do HTML5 (não armazenados em cache) no aplicativo AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Quando o aplicativo AEM Forms é conectado a uma versão mais antiga do servidor AEM Forms, os formulários HTML5 não armazenados em cache não são carregados no aplicativo AEM Forms.

Execute as seguintes etapas para resolver o problema:

1. Na instância do autor, navegue até **Adobe Experience Manager > Ferramentas > Configurar serviço offline do aplicativo do Workspace > Configurar agora**.
1. Em **Serviço offline de aplicativo do Workspace** página, clique em **Cache de Recursos Manual**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. No **Cache de Recursos Manual** clique no botão **+** para adicionar um caminho CRX.
1. No **Adicionar um novo recurso** campo, tipo: /etc.clientlibs/fd/xfaforms/I18N/en_US.js e clique em **Adicionar**.
1. Clique em **Salvar**.

## AEM Forms não sincroniza no Windows {#aem-forms-do-not-sync-on-windows}

No aplicativo AEM Forms no Windows, um formulário não é sincronizado com o servidor conectado se o caminho do formulário ou de seus recursos contiver mais ou igual a 256 caracteres.

Modifique o caminho do formulário e seus recursos para reduzir o número de caracteres para menos de 256 caracteres.

## Versão não suportada do Gradle {#unsupported-version-of-gradle}

**Mensagem de erro:** O projeto está usando uma versão não suportada do Gradle.

A mensagem de erro é exibida ao criar o aplicativo AEM Forms no Android Studio. O problema ocorre devido à versão não suportada do Gradle suportada no sistema.

**Resolução:** Clique em **Correção do wrapper de Gradle e reimportação do projeto** para resolver o problema.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problemas de compatibilidade do plug-in Gradle e Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Mensagem de erro:** As versões do plug-in e Gradle do Android não são compatíveis.

A mensagem de erro é exibida ao selecionar **Criar APK** da **Criar** na interface do usuário do Android Studio.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**Resolução:** Abrir **Scripts de Gradle** > **gradle-wrapper.properties** e edite o **distributionUrl** propriedade.

Por exemplo, o console do Android Studio recomenda o downgrade da versão do Gradle para 3.5. Edite a versão em **distributionUrl** de **gradle-wrapper.properties** arquivo.

Selecionar **Criar** > **Criar APK** novamente para resolver o erro e gerar o arquivo .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
