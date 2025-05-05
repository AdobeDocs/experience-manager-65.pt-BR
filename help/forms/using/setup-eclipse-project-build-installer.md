---
title: Criar o aplicativo AEM Forms Android
description: Etapas para configurar o projeto do Android Studio e criar o arquivo .apk para o aplicativo AEM Forms para o Android
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Criar o aplicativo AEM Forms Android {#build-the-aem-forms-android-app}

Para criar o aplicativo Android para AEM Forms, execute as seguintes etapas na sequência recomendada.

1. [Baixe o pacote de código do AEM Forms App Source](#download-android-zip)
1. [Definir as variáveis de ambiente](#set-environment-variable-android)
1. [Criar um aplicativo AEM Forms padrão](#set-up-the-xcode-project)

## Baixe o pacote de código do AEM Forms App Source {#download-android-zip}

O Pacote de Códigos Source do Aplicativo AEM Forms se refere ao arquivo `adobe-lc-mobileworkspace-src-<version>.zip`. Este arquivo inclui o código-fonte necessário para criar um aplicativo AEM Forms personalizado. O arquivo está incluído no pacote `adobe-aemfd-forms-app-src-pkg-<version>.zip` disponível na Distribuição de Software.

Para baixar o arquivo `adobe-aemfd-forms-app-src-pkg-<version>.zip`, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecione **[!UICONTROL Adobe Experience Manager]**, disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solução]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Downloads de Pesquisa]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abra o [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Carregar Pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.
1. Para baixar o arquivo de código-fonte, abra **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** no navegador. O arquivo .zip do aplicativo Android é baixado no dispositivo.
1. Extraia o conteúdo do arquivo .zip para uma pasta no sistema de arquivos local. Por exemplo, *C:\&lt;Estrutura de Pastas>\adobe-lc-mobileworkspace-src-2.4.20*

A imagem a seguir exibe a estrutura da pasta `adobe-lc-mobileworkspace-src-<version>.zip\android`.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Definir as variáveis de ambiente {#set-environment-variable-android}

Defina as seguintes variáveis de ambiente antes de iniciar o processo de compilação para o aplicativo AEM Forms:

* Defina a variável de ambiente JAVA_HOME para o local do software JDK no sistema de arquivos local. Por exemplo, C:\Program Files\Java\jdk1.8.0_181
* Defina a variável de ambiente do sistema `ANDROID_SDK_ROOT` como o local do SDK para o Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Defina a variável de ambiente do sistema `Path` para incluir os locais da pasta de ferramentas e ferramentas da plataforma do Android. Por exemplo, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools e C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Criar um aplicativo AEM Forms padrão {#set-up-the-xcode-project}

Depois de salvar o arquivo adobe-lc-mobileworkspace-src-&lt;version>.zip no sistema de arquivos local e definir as variáveis de ambiente, crie um aplicativo AEM Forms Android padrão usando uma das seguintes opções:

* [Criar aplicativo AEM Forms usando o Android Studio](#using-android-studio)
* [Gerar arquivo .apk usando o Android Studio](#generate-apk-android-studio)

### Criar aplicativo AEM Forms usando o Android Studio {#using-android-studio}

Para criar um aplicativo AEM Forms usando o Android Studio, execute as seguintes etapas:

1. Inicie o aplicativo Android Studio no computador.
1. Clique em **Abrir um projeto existente do Android Studio**. Se a caixa de diálogo para abrir um projeto existente não aparecer automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção **android** é exibida no painel esquerdo.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selecione **android** no painel esquerdo e clique em **Executar** > **Executar &#39;android&#39;**.
1. Selecione o dispositivo Android na seção Dispositivos conectados da caixa de diálogo Selecionar destino de implantação e clique em OK.

   Depois de criar o ambiente de desenvolvimento com sucesso, você pode aplicar personalizações no aplicativo. Use os seguintes artigos para personalizar o aplicativo:

   * [Personalização da marca](/help/forms/using/branding-customization.md)
   * [Personalização de tema](/help/forms/using/theme-customization.md)
   * [Personalização de gesto](/help/forms/using/gesture-customization.md)

   Depois de aplicar as personalizações apropriadas ao seu aplicativo, você pode gerar o arquivo .apk para distribuição.

### Gerar arquivo .apk usando o Android Studio {#generate-apk-android-studio}

Para gerar o arquivo .apk usando o Android Studio, faça o seguinte:

1. Inicie o aplicativo Android Studio no computador.
1. Selecione **Abrir um projeto existente do Android Studio**. Se a caixa de diálogo para abrir um projeto existente não aparecer automaticamente, selecione **Arquivo** > **Abrir**.
1. Navegue até *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* no sistema de arquivos local e clique em **OK**.

   A opção android é exibida no painel esquerdo.

1. Para gerar o arquivo .apk, selecione **Build** > **Build APK**.

   Opcionalmente, selecione **Build** > **Generate Signed APK** para gerar uma [versão assinada](https://developer.android.com/studio/publish/app-signing) do arquivo .apk.

## Usar o Android Debug Bridge {#build-android-debug-bridge}

Depois que o arquivo .apk for gerado, execute o seguinte comando para instalar o aplicativo em um dispositivo Android usando o [Android Debug Bridge](https://developer.android.com/tools/adb).

**Usuários do Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Usuários do Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
