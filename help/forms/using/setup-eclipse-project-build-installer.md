---
title: Criar o aplicativo AEM Forms Android
seo-title: Criar o aplicativo AEM Forms Android
description: Etapas para configurar o projeto do Android Studio e criar o arquivo .apk para o aplicativo AEM Forms para Android
seo-description: Etapas para configurar o projeto do Android Studio e criar o arquivo .apk para o aplicativo AEM Forms para Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Criar o aplicativo AEM Forms Android {#build-the-aem-forms-android-app}

Execute as seguintes etapas na sequência recomendada para criar o aplicativo Android para formulários AEM.

1. [Baixar o pacote de código-fonte do aplicativo AEM Forms](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-277929160)
1. [Definir as variáveis de ambiente](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-111803610)
1. [Criar aplicativo AEM Forms padrão](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-heading-0)

## Baixar o pacote de código-fonte do aplicativo AEM Forms {#download-android-zip}

O pacote de código-fonte do aplicativo AEM Forms refere-se ao `adobe-lc-mobileworkspace-src-<version>.zip` arquivo. Este arquivo inclui o código fonte necessário para criar um aplicativo AEM Forms personalizado. O arquivo está incluído no `adobe-aemfd-forms-app-src-pkg-<version>.zip`pacote disponível no compartilhamento do pacote.

Execute as seguintes etapas para baixar o `adobe-aemfd-forms-app-src-pkg-<version>.zip` arquivo:

1. Faça logon na instância do autor do servidor [](http://localhost:4502/) AEM como um administrador e abra o compartilhamento [](http://localhost:4502/crx/packageshare)de pacote. Você precisa de uma ID da Adobe para fazer logon no compartilhamento de pacote.
1. Em Compartilhamento [de pacote do](http://localhost:4502/crx/packageshare/login.html)AEM, pesquise `adobe-aemfd-forms-app-src-pkg-<version>.zip`, clique no pacote aplicável ao seu sistema operacional e clique em **Download**. Leia e aceite o contrato de licença e clique em **OK**. Os start de download. Após o download, a palavra **Download** é exibida ao lado do pacote.
1. Depois que o download for concluído, clique em **Download**. Você é redirecionado para o gerenciador de pacotes. No gerenciador de pacotes, pesquise o pacote baixado e clique em **Instalar**.
1. Para baixar o arquivo de código-fonte, abra **https://&lt;servidor>:&lt;porta>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;versão>.zip** em seu navegador. O arquivo .zip do aplicativo Android é baixado em seu dispositivo.
1. Extraia o conteúdo do arquivo .zip para uma pasta no sistema de arquivos local. Por exemplo, *C:\&amp;lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

A imagem a seguir exibe a estrutura da `adobe-lc-mobileworkspace-src-<version>.zip\android`pasta.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Definir as variáveis de ambiente {#set-environment-variable-android}

Defina as seguintes variáveis de ambiente antes de iniciar o processo de criação para o aplicativo AEM Forms:

* Defina a variável de ambiente JAVA_HOME para o local do software JDK no sistema de arquivos local. Por exemplo, C:\Program Files\Java\jdk1.8.0_181
* Defina a variável de ambiente do `ANDROID_SDK_ROOT` sistema para o local do SDK para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Defina a variável de ambiente do `Path` sistema para incluir os locais de pastas de ferramentas de plataforma para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

Depois de salvar o arquivo adobe-lc-mobileworkspace-src-&lt;versão>.zip no sistema de arquivos local e definir as variáveis do ambiente, crie um aplicativo AEM Forms Android padrão usando qualquer uma das seguintes opções:

* [Criar aplicativo AEM Forms usando o Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-1347434739)
* [Gerar arquivo .apk usando o Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-0)

### Criar aplicativo AEM Forms usando o Android Studio {#using-android-studio}

Execute as seguintes etapas para criar um aplicativo AEM Forms usando o Android Studio:

1. Inicie o aplicativo Android Studio em seu computador.
1. Clique em **Abrir um projeto** Android Studio existente. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;versão>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção **android** é exibida no painel esquerdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selecione **Android** no painel esquerdo e clique em **Executar** > **Executar &#39;android&#39;**.
1. Selecione o dispositivo Android na seção Dispositivos conectados na caixa de diálogo Selecionar Público alvo de implantação e clique em OK.

   Depois de criar o ambiente de desenvolvimento com êxito, você pode aplicar personalizações no aplicativo. Use os seguintes artigos para personalizar o aplicativo:

   * [Personalização da marca](/help/forms/using/branding-customization.md)
   * [Personalização do tema](/help/forms/using/theme-customization.md)
   * [Personalização do gesto](/help/forms/using/gesture-customization.md)
   Depois de aplicar as personalizações apropriadas ao aplicativo, você pode gerar o arquivo .apk para distribuição.

### Gerar arquivo .apk usando o Android Studio {#generate-apk-android-studio}

Execute as seguintes etapas para gerar o arquivo .apk usando o Android Studio:

1. Inicie o aplicativo Android Studio em seu computador.
1. Selecione **Abrir um projeto** Android Studio existente. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;versão>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção android é exibida no painel esquerdo.

1. Selecione **Criar** > **Criar APK** para gerar o arquivo .apk.

   Como opção, selecione **Criar** > **Gerar APK** assinado para gerar uma versão [](https://developer.android.com/studio/publish/app-signing) assinada do arquivo .apk.

## Usar a ponte de depuração do Android {#build-android-debug-bridge}

Depois que o arquivo .apk for gerado, execute o seguinte comando para instalar o aplicativo em um dispositivo Android usando a Ponte [de Depuração do](https://developer.android.com/tools/help/adb.html)Android.

**Usuários do Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuários do MAC:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
