---
title: Criar o aplicativo AEM Forms Android
description: Etapas para configurar o projeto do Android Studio e criar o arquivo .apk para o aplicativo AEM Forms para Android
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Criar o aplicativo AEM Forms Android {#build-the-aem-forms-android-app}

Para criar o aplicativo Android para AEM Forms, execute as seguintes etapas na sequência recomendada.

1. [Baixe o pacote do código-fonte do aplicativo AEM Forms](#download-android-zip)
1. [Definir as variáveis de ambiente](#set-environment-variable-android)
1. [Criar um aplicativo AEM Forms padrão](#set-up-the-xcode-project)

## Baixe o pacote do código-fonte do aplicativo AEM Forms {#download-android-zip}

O pacote do Código fonte do aplicativo AEM Forms se refere ao `adobe-lc-mobileworkspace-src-<version>.zip` arquivo. Este arquivo inclui o código-fonte necessário para criar um aplicativo AEM Forms personalizado. O arquivo está incluído na variável `adobe-aemfd-forms-app-src-pkg-<version>.zip`disponível na Distribuição de software.

Para baixar o `adobe-aemfd-forms-app-src-pkg-<version>.zip` execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.
1. Para baixar o arquivo de código-fonte, abra **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** no navegador. O arquivo .zip do aplicativo Android foi baixado em seu dispositivo.
1. Extraia o conteúdo do arquivo .zip para uma pasta no sistema de arquivos local. Por exemplo, *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

A imagem a seguir mostra a estrutura do `adobe-lc-mobileworkspace-src-<version>.zip\android`pasta.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Definir as variáveis de ambiente {#set-environment-variable-android}

Defina as seguintes variáveis de ambiente antes de iniciar o processo de compilação para o aplicativo AEM Forms:

* Defina a variável de ambiente JAVA_HOME para o local do software JDK no sistema de arquivos local. Por exemplo, C:\Program Files\Java\jdk1.8.0_181
* Defina o `ANDROID_SDK_ROOT` variável de ambiente do sistema ao local do SDK para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Defina o `Path` Variável de ambiente do sistema para incluir os locais das pastas de ferramentas e ferramentas da plataforma para Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools e C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Criar um aplicativo AEM Forms padrão {#set-up-the-xcode-project}

Depois de salvar adobe-lc-mobileworkspace-src-&lt;version>.zip no sistema de arquivos local e defina as variáveis de ambiente, crie um aplicativo padrão do AEM Forms Android usando uma das seguintes opções:

* [Criar aplicativo AEM Forms usando o Android Studio](#using-android-studio)
* [Gerar arquivo .apk usando o Android Studio](#generate-apk-android-studio)

### Criar aplicativo AEM Forms usando o Android Studio {#using-android-studio}

Para criar um aplicativo AEM Forms usando o Android Studio, execute as seguintes etapas:

1. Inicie o aplicativo Android Studio no computador.
1. Clique em **Abrir um projeto Android Studio existente**. Se a caixa de diálogo para abrir um projeto existente não aparecer automaticamente, selecione **Arquivo** > **Abertura**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A variável **android** será exibida no painel esquerdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selecionar **android** no painel esquerdo e clique em **Executar** > **Executar &#39;android&#39;**.
1. Selecione o dispositivo Android na seção Dispositivos conectados da caixa de diálogo Selecionar destino de implantação e clique em OK.

   Depois de criar o ambiente de desenvolvimento com sucesso, você pode aplicar personalizações no aplicativo. Use os seguintes artigos para personalizar o aplicativo:

   * [Personalização da marca](/help/forms/using/branding-customization.md)
   * [Personalização de tema](/help/forms/using/theme-customization.md)
   * [Personalização de gesto](/help/forms/using/gesture-customization.md)

   Depois de aplicar as personalizações apropriadas ao seu aplicativo, você pode gerar o arquivo .apk para distribuição.

### Gerar arquivo .apk usando o Android Studio {#generate-apk-android-studio}

Para gerar o arquivo .apk usando o Android Studio, faça o seguinte:

1. Inicie o aplicativo Android Studio no computador.
1. Selecionar **Abrir um projeto Android Studio existente**. Se a caixa de diálogo para abrir um projeto existente não aparecer automaticamente, selecione **Arquivo** > **Abertura**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção android é exibida no painel esquerdo.

1. Para gerar o arquivo .apk, selecione **Build** > **Criar APK**.

   Opcionalmente, selecione **Build** > **Gerar APK assinado** para gerar um [versão assinada](https://developer.android.com/studio/publish/app-signing) do arquivo .apk.

## Usar o Android Debug Bridge {#build-android-debug-bridge}

Depois que o arquivo .apk for gerado, execute o seguinte comando para instalar o aplicativo em um dispositivo Android usando o [Android Debug Bridge](https://developer.android.com/tools/adb).

**Usuários do Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuários do Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
