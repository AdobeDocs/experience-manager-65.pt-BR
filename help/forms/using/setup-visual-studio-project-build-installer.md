---
title: Configurar o projeto do Visual Studio e criar o aplicativo do Windows
seo-title: Set up the Visual Studio project and build the Windows app
description: Saiba como configurar um projeto do Visual Studio para compilar o aplicativo para dispositivos móveis do AEM Forms Windows.
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# Configurar o projeto do Visual Studio e criar o aplicativo do Windows{#set-up-the-visual-studio-project-and-build-the-windows-app}

O AEM Forms fornece o código-fonte completo do aplicativo AEM Forms. A origem contém todos os componentes para criar um aplicativo de espaço de trabalho personalizado. O arquivo do código-fonte, `adobe-lc-mobileworkspace-src-<version>.zip`O faz parte da `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacote na Distribuição de software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para baixar o arquivo de código-fonte, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` no navegador.\
   O pacote de origem é baixado no dispositivo.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

A imagem a seguir exibe a estrutura de diretório do `windows` pasta na `src` pasta.

![win-dir](assets/win-dir.png)

## Configuração do ambiente {#setting-up-the-environment}

Para dispositivos Windows, é necessário:

* Microsoft Windows 8.1 ou Windows 10
* Microsoft Visual Studio 2015
* Ferramentas do Microsoft Visual Studio para Apache Cordova

## Configurando o Projeto do Visual Studio para o aplicativo AEM Forms {#setting-up-visual-studio-project-for-aem-forms-app}

Execute as seguintes etapas para configurar o projeto de aplicativo AEM Forms no Visual Studio.

1. Copie o `adobe-lc-mobileworkspace-src-<version>.zip` arquivar em `%HOMEPATH%\Projects` pasta no dispositivo Windows 8.1 ou Windows 10 com Visual Studio 2015 instalado e configurado.
1. Extraia o arquivo no `%HOMEPATH%\Projects\MobileWorkspace` diretório.
1. Navegue até a `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` diretório.
1. Abra o `CordovaApp.sln` usando o Visual Studio 2015 e prossiga para a criação do aplicativo AEM Forms.

## Criar aplicativo AEM Forms {#build-aem-forms-app}

Execute as seguintes etapas para criar e implantar o aplicativo AEM Forms.

>[!NOTE]
>
>Os dados armazenados no sistema de arquivos do Windows para o aplicativo AEM Forms não são criptografados. É recomendável usar uma ferramenta de terceiros, como a Criptografia de Unidade de Disco BitLocker do Windows, para criptografar dados de disco.

1. Na barra de ferramentas do Visual Studio Standard, selecione **Versão** na lista suspensa para modo de criação.

1. Selecione Windows-AnyCPU, Windows-x64 ou Windows-x86 com base em sua plataforma. Windows-AnyCPU é recomendado.
1. No Visual Studio Solution Explorer, clique com o botão direito no projeto **CordovaApp.Windows** e selecione **Loja > Criar AppPackages**.

   ![createapppackages](assets/createapppackages.png)

   O assistente Criar pacotes de aplicativos é exibido.

   O arquivo do instalador CordovaApp.Windows_3.0.2.0_anycpu.appx é criado no diretório platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test.

   Se você encontrar o erro `Retarget to windows 8.1 required`, clique com o botão direito no erro e, no menu pop-up, selecione **Redirecionar Para O Windows 8.1**.

   ![retarget-solution](assets/retarget-solution.png)

1. No assistente Criar Pacotes de Aplicativos, selecione clima ou não para carregar seu aplicativo na windows store e clique em **Próxima**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. Faça as alterações nos parâmetros, como a versão e o local de saída da build do aplicativo, conforme necessário.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. Depois que o projeto for criado, você poderá instalar o aplicativo usando:

   * Windows PowerShell
   * Visual Studio

   A variável `.appx` O pacote requer os seguintes itens para ser instalado com êxito:

   1. Biblioteca WinJS
   1. Verifique se o pacote vem com um certificado autoassinado ou com um certificado público assinado por uma autoridade confiável, como o VeriSign.
   1. Licença de desenvolvedor

   O diretório Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test contém os quatro componentes principais:

   1. `.appx` arquivo
   1. Certificado (Atualmente, é um certificado autoassinado pelo Apache Cordova)
   1. Pasta de dependências
   1. Arquivo do PowerShell (extensão .ps1)

## Implantação de um aplicativo usando o Windows PowerShell {#deploying-an-app-using-windows-powershell}

Há duas maneiras de instalar o aplicativo em um dispositivo Windows.

### Ao adquirir a licença de desenvolvedor {#by-acquiring-the-developer-license}

1. Clique com o botão direito do mouse no arquivo do PowerShell ( `Add-AppDevPackage.ps1)`e escolha **Executar com o PowerShell**.

1. A instalação solicita que você obtenha uma licença de desenvolvedor. Use as credenciais de conta da Microsoft para adquirir uma licença de desenvolvedor.\
   Esta licença é válida por 30 dias e você pode renová-la gratuitamente.
1. Quando você adquire a licença de desenvolvedor, a configuração instala o certificado autoassinado no sistema e o aplicativo é instalado com êxito.

### Ao usar dispositivos de propriedade empresarial {#by-using-enterprise-owned-devices}

Para dispositivos de propriedade corporativa que ingressaram no domínio da empresa, não é necessário adquirir uma licença de desenvolvedor.

Dispositivos de propriedade corporativa usam as edições Professional e Enterprise do Windows.

A Microsoft recomenda instalar um certificado público emitido por uma autoridade confiável, como o VeriSign.

Para implantar o aplicativo:

* Verifique se o dispositivo ingressou no domínio da empresa.
* Habilitar configuração de política de grupo.

**Para habilitar a configuração de diretiva de grupo:**

1. Em seu dispositivo, execute `gpedit.msc`.
1. Navegue até **Configuração do computador > Modelos administrativos > Componente do Windows > Implantação do pacote de aplicativos**.
1. Clique com o botão direito do mouse **Permitir que todos os aplicativos confiáveis sejam instalados**.
1. Clique em **Editar** e selecione **Ativado**.

1. Clique em **OK**.

Edite o script do PowerShell gerado pelo Visual Studio para impedi-lo de adquirir uma licença de desenvolvedor.

No script do PowerShell, defina a variável: `$NeedDeveloperLicense = $false`.

Para dispositivos que não ingressaram em um domínio, é necessário carregar manualmente a chave de ativação do produto. Você pode comprá-lo de um revendedor Windows.

Para o Windows 8.1 Home Edition, não há política de grupo, o carregamento lateral da empresa não é permitido e você não pode ingressá-lo com o domínio da empresa. Implante o aplicativo em um dispositivo Windows 8.1 Home Edition usando uma licença de desenvolvedor.

Para obter mais informações, clique em [aqui](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Implantando um aplicativo usando o Visual Studio {#deploying-an-app-using-visual-studio}

Para instalar o aplicativo no Windows usando o Visual Studio:

1. Conecte o dispositivo usando o depurador remoto.\
   Para obter mais informações, consulte [Executar aplicativos da Windows Store em um computador remoto](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Com seu aplicativo aberto no Visual Studio, escolha Windows-x64, Windows-x86 ou Windows-AnyCPU na lista Plataformas de Soluções e selecione **Computador Remoto**.
1. Seu aplicativo é implantado no computador remoto.
