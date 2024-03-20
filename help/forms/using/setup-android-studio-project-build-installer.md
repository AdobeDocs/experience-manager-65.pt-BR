---
title: Configurar o projeto do Android&trade; studio e criar o aplicativo Android&trade;
description: Etapas para configurar o projeto Android&trade; Studio e criar o instalador para o aplicativo Forms do Adobe Experience Manager (AEM)
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---

# Configure o projeto do Android™ Studio e crie o aplicativo Android™ {#set-up-the-android-studio-project-and-build-the-android-app}

Este artigo é para a criação do aplicativo AEM Forms 6.3.1.1 e versões posteriores. Para criar um aplicativo a partir do código-fonte do Aplicativo AEM Forms 6.3, consulte [Configurar o projeto Eclipse e criar o aplicativo Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

A AEM Forms fornece o código-fonte completo do aplicativo AEM Forms. A origem contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo do código-fonte, `adobe-lc-mobileworkspace-src-<version>.zip` O faz parte da `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacote na Distribuição de software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![Conteúdo extraído da origem Android™ compactada](assets/mws-content-1.png)

A imagem a seguir exibe a estrutura de diretório do `android`pasta na `src`pasta.

![Estrutura de diretório da pasta do android em src](assets/android-folder.png)

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Android™ Studio e fornecer uma identidade de assinatura:

   Faça logon em um computador com Android™ Studio instalado e configurado.

1. Copie o baixado `adobe-lc-mobileworkspace-src-<version>.zip` arquivar em:

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
   >É recomendável manter o projeto extraído do Android na unidade do sistema antes de importar o projeto para o Android™ Studio.

1. Inicie o Android™ Studio.

   **Para usuários do Mac**: atualize o `local.properties` arquivo presente no `[User_Home]/Projects/[your-project]/android` e aponte a `sdk.dir` variável para `SDK` em sua área de trabalho.

   **Para usuários do Windows®**: atualize o `local.properties` arquivo presente no `%HOMEPATH%\Projects\[your-project]\android` e aponte a `sdk.dir` variável para `SDK` em sua área de trabalho.

1. Clique em **[!UICONTROL Concluir]** para construir o projeto.

   O projeto está disponível no ADT Project Explorer.

   ![projeto do eclipse após a criação do aplicativo](assets/eclipsebuildmws.png)

1. No Android™ Studio, selecione **[!UICONTROL Importar projeto (Eclipse ADT, Gradle, Etc.)]**.
1. No explorador do projeto, selecione o diretório raiz do projeto que você deseja construir na **Diretório raiz** caixa de texto:

   **Para usuários do Mac:** [Início_Usuário]/Projects/MobileWorkspace/src/android

   **Para usuários do Windows®:** %CAMINHOCAMINHO%\Projects\MobileWorkspace\src\android

1. Depois que o projeto for importado, um pop-up será exibido com a opção para atualizar o plug-in do Android™ Gradle. Clique no botão apropriado, dependendo de sua necessidade.

   ![dontremindmeagainforisproject](assets/dontremindmeagainforthisproject.png)

1. Após a criação bem-sucedida do gradle, a tela a seguir é exibida. Conecte o dispositivo ou emulador apropriado ao sistema e clique em **[!UICONTROL Executar Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. O Android™ Studio exibe os dispositivos conectados e os emuladores disponíveis. Selecione o dispositivo no qual deseja executar o aplicativo e clique em **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Depois de criar o projeto, você pode optar por instalar o aplicativo usando o Android™ Debug Bridge ou o Android™ Studio.

### Utilização do Android™ Debug Bridge {#andriod-debug-bridge}

É possível instalar o aplicativo em um dispositivo Android™ por meio da [Ponte de depuração Android™](https://developer.android.com/tools/adb) com o seguinte comando:

**Para usuários do Mac**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Para usuários do Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
