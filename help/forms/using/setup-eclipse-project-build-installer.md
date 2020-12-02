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
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# Crie o aplicativo AEM Forms Android {#build-the-aem-forms-android-app}

Execute as seguintes etapas na sequência recomendada para criar o aplicativo Android para AEM Forms.

1. [Download do pacote de código-fonte do aplicativo AEM Forms](#download-android-zip)
1. [Definir as variáveis de ambiente](#set-environment-variable-android)
1. [Criar aplicativo AEM Forms padrão](#set-up-the-xcode-project)

## Baixe o pacote de código-fonte do aplicativo AEM Forms {#download-android-zip}

O Pacote de código-fonte do aplicativo AEM Forms se refere ao arquivo `adobe-lc-mobileworkspace-src-<version>.zip`. Este arquivo inclui o código fonte necessário para criar um aplicativo AEM Forms personalizado. O arquivo está incluído no pacote `adobe-aemfd-forms-app-src-pkg-<version>.zip`disponível na Distribuição de software.

Execute as seguintes etapas para baixar o arquivo `adobe-aemfd-forms-app-src-pkg-<version>.zip`:

1. Abra [Distribuição de software](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solution]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Download]**.
1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.
1. Para baixar o arquivo de código-fonte, abra **https://&lt;servidor>:&lt;porta>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;versão>.zip** no seu navegador. O arquivo .zip do aplicativo Android é baixado em seu dispositivo.
1. Extraia o conteúdo do arquivo .zip para uma pasta no sistema de arquivos local. Por exemplo, *C:\&lt;Estrutura da pasta>\adobe-lc-mobileworkspace-src-2.4.20*

A imagem a seguir exibe a estrutura da pasta `adobe-lc-mobileworkspace-src-<version>.zip\android`.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Defina as variáveis de ambiente {#set-environment-variable-android}

Defina as seguintes variáveis de ambiente antes de iniciar o processo de criação para o aplicativo AEM Forms:

* Defina a variável de ambiente JAVA_HOME para o local do software JDK no sistema de arquivos local. Por exemplo, C:\Program Files\Java\jdk1.8.0_181
* Defina a variável de ambiente do sistema `ANDROID_SDK_ROOT` como o local do SDK para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Defina a variável de ambiente do sistema `Path` para incluir os locais de pastas de ferramentas e ferramentas da plataforma para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

Depois de salvar o arquivo adobe-lc-mobileworkspace-src-&lt;versão>.zip no sistema de arquivos local e definir as variáveis do ambiente, crie um aplicativo AEM Forms Android padrão usando qualquer uma das seguintes opções:

* [Criar aplicativo AEM Forms usando o Android Studio](#using-android-studio)
* [Gerar arquivo .apk usando o Android Studio](#generate-apk-android-studio)

### Criar aplicativo AEM Forms usando o Android Studio {#using-android-studio}

Execute as seguintes etapas para criar um aplicativo AEM Forms usando o Android Studio:

1. Inicie o aplicativo Android Studio em seu computador.
1. Clique em **Abrir um projeto do Android Studio** existente. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção **android** é exibida no painel esquerdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selecione **android** no painel esquerdo e clique em **Executar** > **Executar &#39;android&#39;**.
1. Selecione o dispositivo Android na seção Dispositivos conectados na caixa de diálogo Selecionar Público alvo de implantação e clique em OK.

   Depois de criar o ambiente de desenvolvimento com êxito, você pode aplicar personalizações no aplicativo. Use os seguintes artigos para personalizar o aplicativo:

   * [Personalização da marca](/help/forms/using/branding-customization.md)
   * [Personalização do tema](/help/forms/using/theme-customization.md)
   * [Personalização do gesto](/help/forms/using/gesture-customization.md)

   Depois de aplicar as personalizações apropriadas ao aplicativo, você pode gerar o arquivo .apk para distribuição.

### Gerar arquivo .apk usando o Android Studio {#generate-apk-android-studio}

Execute as seguintes etapas para gerar o arquivo .apk usando o Android Studio:

1. Inicie o aplicativo Android Studio em seu computador.
1. Selecione **Abrir um projeto do Android Studio** existente. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção android é exibida no painel esquerdo.

1. Selecione **Build** > **Criar APK** para gerar o arquivo .apk.

   Como opção, selecione **Build** > **Gerar APK assinado** para gerar uma [versão assinada](https://developer.android.com/studio/publish/app-signing) do arquivo .apk.

## Usar a ponte de depuração do Android {#build-android-debug-bridge}

Depois que o arquivo .apk for gerado, execute o seguinte comando para instalar o aplicativo em um dispositivo Android usando a [Ponte de depuração do Android](https://developer.android.com/tools/help/adb.html).

**Usuários do Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuários do MAC:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
