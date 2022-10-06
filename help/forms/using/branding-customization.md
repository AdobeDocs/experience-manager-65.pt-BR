---
title: Personalização da marca
seo-title: Branding Customization
description: Personalize o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e a página de logon para fornecer uma aparência distinta e específica da organização ao aplicativo AEM Forms.
seo-description: Customize the application icon, application name, launch images, and login page to provide a distinct organization-specific look and feel to AEM Forms app.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# Personalização da marca {#branding-customization}

Você pode personalizar o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e a página de logon para fornecer uma aparência distinta específica da organização ao aplicativo AEM Forms. Por exemplo, você pode alterar as imagens para usar logotipos de sua organização. O aplicativo AEM Forms é compatível com as seguintes personalizações:

* Personalização do ícone do aplicativo e imagens de inicialização
* Personalização do nome do aplicativo
* Personalização de imagens na página de logon
* Personalização do logotipo no menu do aplicativo

## Personalização de ícones e imagens de lançamento {#customizing-icon-and-launch-images}

Execute as seguintes etapas para personalizar o ícone do aplicativo padrão e a imagem de inicialização do aplicativo AEM Forms:

>[!NOTE]
>
>Para todos os ícones e imagens, use o formato PNG não entrelaçado.

### Personalização de ícones e imagens de lançamento {#to-customize-icon-and-launch-images}

#### Para iOS {#for-ios}

1. Abra o `Capture.xcodeproj` projeto no Xcode.
1. (***Para ícone personalizado***) Na exibição do navegador de Captura, navegue até **[!UICONTROL Captura > Captura > Arquivos de suporte > Capture-info.plist]**. Clique na lista suspensa ao lado dos arquivos de Ícone . Especifique o nome do arquivo de ícone (.png) e faça upload do arquivo em **[!UICONTROL Captura > Captura > Recursos > ícones]**. As dimensões atualmente compatíveis são: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Para personalizar imagens de lançamento***) Verifique se os nomes de arquivo das imagens são:

   * Para retrato: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Para paisagem: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Faça o upload para o projeto Capture para substituir arquivos existentes no projeto.

   >[!NOTE]
   >
   >Certifique-se de que o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

#### Para Android {#for-android}

1. Nomeie os arquivos de ícone do aplicativo como:

   `ic_launcher.png`

1. Coloque os arquivos de ícone correspondentes nos seguintes diretórios:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Certifique-se de que o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

1. Recrie o aplicativo AEM Forms.

### Para Windows {#for-windows}

1. Substitua os ícones no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Substitua a imagem do iniciador no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Certifique-se de que o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

1. Recrie o aplicativo AEM Forms.

## Personalizar o nome do aplicativo {#customize-the-app-name}

### Para iOS {#for-ios-1}

1. Abra o `Capture.xcodeproj` projeto no Xcode.
1. Na exibição do navegador de Captura, navegue até **[!UICONTROL Captura > Captura > Arquivos de suporte > InfoPlist.strings]**.

   Atualize o valor da variável `CFBundleDisplayName` a um nome que você deseja exibir para o aplicativo.

1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

   Para obter detalhes sobre como criar o aplicativo para iOS, consulte [Configurar o projeto Xcode e criar o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Para Android {#for-android-1}

1. Abra o seguinte Xml em qualquer editor de texto ou Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Atualizar o valor da chave `app_name`.
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre como criar o aplicativo para Android, consulte [Configure o projeto do Eclipse e crie o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Para Windows {#for-windows-1}

1. Abra o seguinte Xml em qualquer editor de texto:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Atualize o valor no `<name>...</name>` .
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre como criar o aplicativo para Windows, consulte [Configurar o projeto do Visual Studio e criar o aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalização de imagens na página de logon {#customizing-images-on-the-login-page}

A página de logon do aplicativo AEM Forms tem imagens de logotipo e plano de fundo. O logotipo está localizado acima da caixa de diálogo de logon e a imagem de fundo está localizada abaixo da caixa de diálogo de logon. Execute as seguintes etapas para personalizar a imagem padrão na página de logon:

**Antes de você iniciar**

Certifique-se de ter as seguintes imagens:

<table>
 <tbody>
  <tr>
   <th><p>Descrição</p> </th>
   <th><p>Tamanho</p> </th>
   <th><p>Nome de arquivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 pixels</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Imagem de plano de fundo (Retrato)</p> </td>
   <td><p>1280 x 989 pixel</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Para personalizar imagens na página de logon usando o Xcode**

1. Abra o `Capture.xcodeproj` projeto no Xcode.

1. Navegue até o `www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` com o `LC-logo.png` arquivo.
1. Para alterar o plano de fundo, substitua o padrão `Landing_bg.jpeg` com o `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Abra o projeto do Android no Eclipse.

1. Navegue até o `assets/www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` com o `LC-logo.png` arquivo.
1. Para alterar o plano de fundo, substitua o padrão `Landing_bg.jpeg` com o `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de login usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Abra o `MWSWindows.sln` projeto no Visual Studio.

1. Navegue até o `MWSWindows\www\wsmobile\images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` com o `LC-logo.png` arquivo.
1. Para alterar o plano de fundo, substitua o padrão `Landing_bg.jpeg` com o `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.

## Personalização do logotipo no menu do aplicativo {#customizing_images_on_the_login_page-1}

Depois de fazer logon no aplicativo AEM Forms e tocar no botão do menu, você poderá ver o logotipo acima do menu. Execute as seguintes etapas para personalizar o logotipo padrão:

**Antes de você iniciar**

Certifique-se de ter a seguinte imagem:

<table>
 <tbody>
  <tr>
   <th><p>Descrição</p> </th>
   <th><p>Tamanho</p> </th>
   <th><p>Nome de arquivo</p> </th>
  </tr>
  <tr>
   <td><p>Logotipo</p> </td>
   <td><p>72 x 72 pixels</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Para personalizar imagens na página de logon usando o Xcode**

1. Abra o `Capture.xcodeproj` projeto no Xcode.

1. Navegue até o `www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` com o `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Abra o projeto do Android no Eclipse.

1. Navegue até o `assets/www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` com o `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de login usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Abra o `MWSWindows.sln` projeto no Visual Studio.

1. Navegue até o `MWSWindows\www\wsmobile\images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` com o `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.
