---
title: Configurar o projeto do Android&trade; studio e criar o aplicativo do Android&trade;
description: Etapas para configurar o projeto Android&trade; Studio e criar o instalador do aplicativo Adobe Experience Manager (AEM) Forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---

# Configure o projeto Android™ studio e crie o aplicativo Android™ {#set-up-the-android-studio-project-and-build-the-android-app}

Este artigo é para a criação do aplicativo AEM Forms 6.3.1.1 e versões posteriores. Para criar um aplicativo a partir do código-fonte do Aplicativo AEM Forms 6.3, consulte [Configurar o projeto Eclipse e criar o aplicativo Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

A AEM Forms fornece o código-fonte completo do aplicativo AEM Forms. A origem contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo morto de código-fonte, `adobe-lc-mobileworkspace-src-<version>.zip`, é parte do pacote `adobe-aemfd-forms-app-src-pkg-<version>.zip` na Distribuição de Software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecione **[!UICONTROL Adobe Experience Manager]**, disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solução]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Downloads de Pesquisa]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abra o [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar Pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

A imagem a seguir exibe o conteúdo extraído de `adobe-lc-mobileworkspace-src-<version>.zip`.

![Conteúdo extraído da origem Android™ compactada](assets/mws-content-1.png)

A imagem a seguir exibe a estrutura de diretório da pasta `android` na pasta `src`.

![Estrutura de diretório da pasta android em src](assets/android-folder.png)

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Android™ Studio e fornecer uma identidade de assinatura:

   Faça logon em um computador que tenha o Android™ Studio instalado e configurado.

1. Copiar o arquivo morto `adobe-lc-mobileworkspace-src-<version>.zip` baixado em:

   **Para usuários do Mac**: `[User_Home]/Projects`

   **Para usuários do Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >No Windows®, é recomendável manter o projeto Android™ na unidade do sistema.

1. Extraia o arquivo no seguinte diretório:

   **Para usuários do Mac**: `[User_Home]/Projects/[your-project]`

   **Para usuários do Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >É recomendável manter o projeto Android extraído na unidade do sistema antes de importar o projeto para o Android™ Studio.

1. Inicie o Android™ Studio.

   **Para usuários do Mac**: atualize o arquivo `local.properties` presente na pasta `[User_Home]/Projects/[your-project]/android` e aponte a variável `sdk.dir` para o local `SDK` na sua área de trabalho.

   **Para usuários do Windows®**: atualize o arquivo `local.properties` presente na pasta `%HOMEPATH%\Projects\[your-project]\android` e aponte a variável `sdk.dir` para o local `SDK` em sua área de trabalho.

1. Clique em **[!UICONTROL Concluir]** para compilar o projeto.

   O projeto está disponível no ADT Project Explorer.

   ![projeto do eclipse após a compilação do aplicativo](assets/eclipsebuildmws.png)

1. No Android™ Studio, selecione **[!UICONTROL Importar Projeto (Eclipse ADT, Gradle, Etc.)]**.
1. No explorador do projeto, selecione o diretório raiz do projeto que você deseja compilar na caixa de texto **Diretório raiz**:

   **Para usuários do Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **Para usuários do Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Depois que o projeto for importado, um pop-up será exibido com a opção para atualizar o plug-in Gradle do Android™. Clique no botão apropriado, dependendo de sua necessidade.

   ![dontremindmeagainfroisproject](assets/dontremindmeagainforthisproject.png)

1. Após a criação bem-sucedida do gradle, a tela a seguir é exibida. Conecte o dispositivo ou emulador apropriado ao sistema e clique em **[!UICONTROL Executar o Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. O Android™ Studio exibe os dispositivos conectados e os emuladores disponíveis. Selecione o dispositivo no qual deseja executar o aplicativo e clique em **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Depois de criar o projeto, você pode optar por instalar o aplicativo usando o Android™ Debug Bridge ou o Android™ Studio.

### Uso do Android™ Debug Bridge {#andriod-debug-bridge}

Você pode instalar o aplicativo em um dispositivo Android™ por meio do [Android™ Debug Bridge](https://developer.android.com/tools/adb) com o seguinte comando:

**Para usuários do Mac**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuários do Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
