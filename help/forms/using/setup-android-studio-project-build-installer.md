---
title: Configure o projeto de estúdio do Android e crie o aplicativo Android
seo-title: Configure o projeto de estúdio do Android e crie o aplicativo Android
description: Etapas para configurar o projeto do Android Studio e criar o instalador para o aplicativo AEM Forms
seo-description: Etapas para configurar o projeto do Android Studio e criar o instalador para o aplicativo AEM Forms
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Configure o projeto de estúdio do Android e crie o aplicativo Android {#set-up-the-android-studio-project-and-build-the-android-app}

Este artigo é para a criação do aplicativo AEM Forms 6.3.1.1 e versões posteriores. Para criar um aplicativo a partir do código-fonte do código-fonte do AEM Forms App 6.3, consulte [Configurar o projeto Eclipse e criar o aplicativo](/help/forms/using/setup-eclipse-project-build-installer.md)Android™.

O AEM Forms fornece o código fonte completo do aplicativo AEM Forms. A fonte contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo de código-fonte `adobe-lc-mobileworkspace-src-<version>.zip` é parte do `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacote de distribuição de software.

Para obter a fonte do aplicativo AEM Forms, execute as seguintes etapas:

1. Distribuição [de](https://experience.adobe.com/downloads)software aberta. Você precisa de um Adobe ID para fazer login na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]** :
   1. Selecione **[!UICONTROL Formulários]** na lista suspensa **[!UICONTROL Solução]** .
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos]** do EULA e toque em **[!UICONTROL Download]**.
1. Abra o Gerenciador [de](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Select the package and click **[!UICONTROL Install]**.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![Conteúdo extraído da origem compactada do Android™](assets/mws-content-1.png)

A imagem a seguir exibe a estrutura de diretório da `android`pasta na `src`pasta.

![Estrutura de diretório da pasta android em src](assets/android-folder.png)

## Criar aplicativo de AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Android™ Studio e fornecer uma identidade de assinatura:

   Faça logon em um computador que tenha o Android™ Studio instalado e configurado.

1. Copie o arquivo baixado `adobe-lc-mobileworkspace-src-<version>.zip` para:

   **Para usuários** MAC: `[User_Home]/Projects`

   **Para usuários** do Windows®: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >No Windows®, é recomendável manter o projeto android na unidade do sistema.

1. Extraia o arquivo no seguinte diretório:

   **Para usuários** MAC: `[User_Home]/Projects/[your-project]`

   **Para usuários** do Windows®: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >É recomendável manter o projeto do android extraído na unidade do sistema antes de importar o projeto para o Android Studio.

1. Inicie o Android™ Studio.

   **Para usuários** MAC: Atualize o `local.properties` arquivo presente na `[User_Home]/Projects/[your-project]/android` pasta e aponte a variável para a `sdk.dir` localização na `SDK` área de trabalho.

   **Para usuários** do Windows®: Atualize o `local.properties` arquivo presente na `%HOMEPATH%\Projects\[your-project]\android` pasta e aponte a variável para a `sdk.dir` localização na `SDK` área de trabalho.

1. Clique em **[!UICONTROL Concluir]** para criar o projeto.

   O projeto está disponível no ADT Project Explorer.

   ![projeto eclipse após a criação do aplicativo](assets/eclipsebuildmws.png)

1. No Android™ Studio, selecione **[!UICONTROL Importar projeto (Eclipse ADT, Gradle Etc.)]**.
1. No explorador de projetos, selecione o diretório raiz do projeto que deseja criar na caixa de texto Diretório **** raiz:

   **Para usuários do Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **Para usuários do Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Depois que o projeto é importado, um pop-up é exibido com a opção de atualizar o Gradle do plug-in Android™. Clique no botão apropriado, dependendo de seu requisito.

   ![dontremindmeagaincontutisproject](assets/dontremindmeagainforthisproject.png)

1. Após a criação gradle bem-sucedida, a seguinte tela é exibida. Conecte o dispositivo ou emulador apropriado ao sistema e clique em **[!UICONTROL Executar Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. O Android™ Studio exibe os dispositivos conectados e os emuladores disponíveis. Selecione o dispositivo no qual deseja executar o aplicativo e clique em **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Depois de criar o projeto, você pode escolher instalar o aplicativo usando o Android™ Debug Bridge ou o Android™ Studio.

### Usando a ponte de depuração Android™ {#andriod-debug-bridge}

Você pode instalar o aplicativo em um dispositivo Android™ por meio da [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) com o seguinte comando:

**Para usuários** MAC: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuários** do Windows®: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
