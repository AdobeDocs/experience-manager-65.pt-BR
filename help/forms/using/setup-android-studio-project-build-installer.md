---
title: Configure o projeto de estúdio do Android e crie o aplicativo Android
seo-title: Set up the Android studio project and build the Android app
description: Etapas para configurar o projeto do Android Studio e criar o instalador do aplicativo AEM Forms
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 7%

---

# Configure o projeto de estúdio do Android e crie o aplicativo Android {#set-up-the-android-studio-project-and-build-the-android-app}

Este artigo é para criar o aplicativo AEM Forms 6.3.1.1 e versões posteriores. Para criar um aplicativo a partir do código-fonte do código-fonte do AEM Forms App 6.3, consulte [Configure o projeto Eclipse e crie o aplicativo Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

O AEM Forms fornece o código fonte completo do aplicativo AEM Forms. A fonte contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo de código-fonte, `adobe-lc-mobileworkspace-src-<version>.zip` faz parte do `adobe-aemfd-forms-app-src-pkg-<version>.zip` na Distribuição de software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Também é possível usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
1. Abra [Gerenciador de pacotes](https://docs.adobe.com/content/help/pt-BR/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![Conteúdo extraído da fonte compactada Android™](assets/mws-content-1.png)

A imagem a seguir exibe a estrutura de diretório do `android`na pasta `src`pasta.

![Estrutura de diretório da pasta android no src](assets/android-folder.png)

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Android™ Studio e fornecer uma identidade de assinatura:

   Faça logon em uma máquina que tenha o Android™ Studio instalado e configurado.

1. Copie o arquivo baixado `adobe-lc-mobileworkspace-src-<version>.zip` arquivar em:

   **Para usuários do MAC**: `[User_Home]/Projects`

   **Para usuários do Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >No Windows®, é recomendável manter o projeto android na unidade do sistema.

1. Extraia o arquivo no seguinte diretório:

   **Para usuários do MAC**: `[User_Home]/Projects/[your-project]`

   **Para usuários do Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >É recomendável manter o projeto android extraído na unidade do sistema antes de importar o projeto para o Android Studio.

1. Inicie o Android™ Studio.

   **Para usuários do MAC**: Atualize o `local.properties` arquivo presente no `[User_Home]/Projects/[your-project]/android` e aponte a `sdk.dir` para `SDK` na área de trabalho.

   **Para usuários do Windows®**: Atualize o `local.properties` arquivo presente no `%HOMEPATH%\Projects\[your-project]\android` e aponte a `sdk.dir` para `SDK` na área de trabalho.

1. Clique em **[!UICONTROL Concluir]** para criar o projeto.

   O projeto está disponível no Gerenciador de projetos ADT.

   ![projeto do eclipse após criar o aplicativo](assets/eclipsebuildmws.png)

1. No Android™ Studio, selecione **[!UICONTROL Importar Projeto (Eclipse ADT, Gradle Etc.)]**.
1. No explorador de projetos, selecione o diretório raiz do projeto que deseja criar no **Diretório raiz** caixa de texto:

   **Para usuários do Mac:** [User_Home]/Projetos/MobileWorkspace/src/android

   **Para usuários do Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Depois que o projeto é importado, um pop-up é exibido com a opção de atualizar o Gradle do plug-in Android™. Clique no botão apropriado dependendo de sua necessidade.

   ![dontremindmeagainforisproject](assets/dontremindmeagainforthisproject.png)

1. Após a criação bem-sucedida do gradle, a tela a seguir é exibida. Conecte o dispositivo ou emulador apropriado ao sistema e clique em **[!UICONTROL Execute o Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. O Android™ Studio exibe os dispositivos conectados e os emuladores disponíveis. Selecione o dispositivo no qual deseja executar o aplicativo e clique em **OK**.

   ![dispositivo conectado](assets/connecteddevice.png)

Depois de criar o projeto, você pode optar por instalar o aplicativo usando o Android™ Debug Bridge ou o Android™ Studio.

### Uso do Android™ Debug Bridge {#andriod-debug-bridge}

Você pode instalar o aplicativo em um dispositivo Android™ através do [Ponte de depuração Android™](https://developer.android.com/tools/help/adb.html) com o seguinte comando:

**Para usuários do MAC**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuários do Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
