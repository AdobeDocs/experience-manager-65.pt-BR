---
title: Criar o aplicativo AEM Forms Android
seo-title: Build the AEM Forms Android app
description: Etapas para configurar o projeto do Android Studio e criar o arquivo .apk para o aplicativo AEM Forms para Android
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 6%

---

# Criar o aplicativo AEM Forms Android {#build-the-aem-forms-android-app}

Execute as etapas a seguir na sequência recomendada para criar o aplicativo Android para AEM Forms.

1. [Baixe o pacote de código-fonte do aplicativo AEM Forms](#download-android-zip)
1. [Definir as variáveis de ambiente](#set-environment-variable-android)
1. [Criar aplicativo AEM Forms padrão](#set-up-the-xcode-project)

## Baixe o pacote de código-fonte do aplicativo AEM Forms {#download-android-zip}

O Pacote de código-fonte do aplicativo do AEM Forms se refere ao `adobe-lc-mobileworkspace-src-<version>.zip` arquivo. Este arquivo inclui o código-fonte necessário para criar um aplicativo AEM Forms personalizado. O arquivo está incluído na variável `adobe-aemfd-forms-app-src-pkg-<version>.zip`disponível na Distribuição de software.

Execute as etapas a seguir para baixar a variável `adobe-aemfd-forms-app-src-pkg-<version>.zip` arquivo:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Também é possível usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
1. Abra [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.
1. Para baixar o arquivo do código-fonte, abra **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** no seu navegador. O arquivo .zip do aplicativo Android é baixado no dispositivo.
1. Extraia o conteúdo do arquivo .zip para uma pasta no sistema de arquivos local. Por exemplo, *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

A imagem a seguir exibe a estrutura da variável `adobe-lc-mobileworkspace-src-<version>.zip\android`pasta.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Definir as variáveis de ambiente {#set-environment-variable-android}

Defina as seguintes variáveis de ambiente antes de iniciar o processo de criação para o aplicativo AEM Forms:

* Defina a variável de ambiente JAVA_HOME para o local do software JDK no sistema de arquivos local. Por exemplo, C:\Program Files\Java\jdk1.8.0_181
* Defina as `ANDROID_SDK_ROOT` variável de ambiente do sistema para o local do SDK para Android. Por exemplo, C:\Users\&amp;lt;nome de usuário>\AppData\Local\Android\Sdk
* Defina as `Path` variável de ambiente do sistema para incluir os locais das pastas de ferramentas e ferramentas da plataforma para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

Depois de salvar o adobe-lc-mobileworkspace-src-&lt;version>Arquivo .zip no sistema de arquivos local e defina as variáveis de ambiente, crie o aplicativo AEM Forms Android padrão usando qualquer uma das seguintes opções:

* [Criar aplicativo AEM Forms usando o Android Studio](#using-android-studio)
* [Gerar arquivo .apk usando o Android Studio](#generate-apk-android-studio)

### Criar aplicativo AEM Forms usando o Android Studio {#using-android-studio}

Execute as seguintes etapas para criar o aplicativo AEM Forms usando o Android Studio:

1. Inicie o aplicativo Android Studio no computador.
1. Clique em **Abra um projeto Android Studio existente**. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegar para *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   O **android** é exibida no painel esquerdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selecionar **android** no painel esquerdo e clique em **Executar** > **Executar &#39;android&#39;**.
1. Selecione o dispositivo Android na seção Dispositivos conectados da caixa de diálogo Selecionar destino de implantação e clique em OK.

   Depois de criar o ambiente de desenvolvimento com sucesso, você pode aplicar personalizações no aplicativo. Use os seguintes artigos para personalizar o aplicativo:

   * [Personalização da marca](/help/forms/using/branding-customization.md)
   * [Personalização de Tema](/help/forms/using/theme-customization.md)
   * [Personalização de Gesto](/help/forms/using/gesture-customization.md)

   Depois de aplicar as personalizações apropriadas ao seu aplicativo, você pode gerar o arquivo .apk para distribuição.

### Gerar arquivo .apk usando o Android Studio {#generate-apk-android-studio}

Execute as seguintes etapas para gerar o arquivo .apk usando o Android Studio:

1. Inicie o aplicativo Android Studio no computador.
1. Selecionar **Abra um projeto Android Studio existente**. Se a caixa de diálogo para abrir um projeto existente não for exibida automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegar para *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção android é exibida no painel esquerdo.

1. Selecionar **Criar** > **Criar APK** para gerar o arquivo .apk.

   Opcionalmente, Selecione **Criar** > **Gerar APK assinado** para gerar um [versão assinada](https://developer.android.com/studio/publish/app-signing) do arquivo .apk.

## Usar o Android Debug Bridge {#build-android-debug-bridge}

Depois que o arquivo .apk tiver sido gerado, execute o seguinte comando para instalar o aplicativo em um dispositivo Android usando o [Ponte de depuração do Android](https://developer.android.com/tools/help/adb.html).

**Usuários do Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuários do Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
