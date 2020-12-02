---
title: Personalização da marca
seo-title: Personalização da marca
description: Personalize o ícone do aplicativo, o nome do aplicativo, as imagens de ativação e a página de logon para fornecer uma aparência específica da organização ao aplicativo AEM Forms.
seo-description: Personalize o ícone do aplicativo, o nome do aplicativo, as imagens de ativação e a página de logon para fornecer uma aparência específica da organização ao aplicativo AEM Forms.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---


# Personalização da marca {#branding-customization}

Você pode personalizar o ícone do aplicativo, o nome do aplicativo, as imagens de ativação e a página de logon para fornecer uma aparência distinta específica da organização ao aplicativo AEM Forms. Por exemplo, você pode alterar as imagens para usar logotipos de sua organização. O aplicativo AEM Forms oferece suporte às seguintes personalizações:

* Personalização de ícones de aplicativos e imagens de inicialização
* Personalização do nome do aplicativo
* Personalização de imagens na página de login
* Personalizar o logotipo no menu do aplicativo

## Personalização de ícones e imagens de ativação {#customizing-icon-and-launch-images}

Execute as seguintes etapas para personalizar o ícone do aplicativo padrão e a imagem de inicialização do aplicativo AEM Forms:

>[!NOTE]
>
>Para todos os ícones e imagens, use o formato PNG não entrelaçado.

### Para personalizar ícones e imagens de ativação {#to-customize-icon-and-launch-images}

#### Para iOS {#for-ios}

1. Abra o projeto `Capture.xcodeproj` no Xcode.
1. (***Para personalizar o ícone***) Na visualização do navegador do Capture, navegue até **[!UICONTROL Capture > Capture > Supporting Files > Capture-info.plist]**. Clique na lista suspensa ao lado dos arquivos de Ícone. Especifique o nome do arquivo de ícone (.png) e faça upload do arquivo em **[!UICONTROL Capturar > Capturar > Recursos > ícones]**. As dimensões atualmente suportadas são: 29 x 29, 50 x 50, 58 x 58, 72 x 72, 100 x 100 e 144 x 144.
1. (***Para personalizar imagens de ativação***) Certifique-se de que os nomes de arquivo das suas imagens são:

   * Para retrato: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Para paisagem: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Carregue-os no projeto Capture para substituir os arquivos existentes no projeto.

   >[!NOTE]
   >
   >Verifique se o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

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
   >Verifique se o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

1. Recrie o aplicativo AEM Forms.

### Para Windows {#for-windows}

1. Substitua os ícones no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Substitua a imagem do iniciador no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Verifique se o nome e a resolução da imagem correspondem à imagem que você substituiu no projeto.

1. Recrie o aplicativo AEM Forms.

## Personalizar o nome do aplicativo {#customize-the-app-name}

### Para iOS {#for-ios-1}

1. Abra o projeto `Capture.xcodeproj` no Xcode.
1. Na visualização do navegador Capture, navegue até **[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**.

   Atualize o valor do atributo `CFBundleDisplayName` para um nome que você deseja exibir para o aplicativo.

1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

   Para obter detalhes sobre como criar o aplicativo para iOS, consulte [Configure o projeto Xcode e crie o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Para Android {#for-android-1}

1. Abra o seguinte Xml em qualquer editor de texto ou Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Atualize o valor da chave `app_name`.
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre como criar o aplicativo para Android, consulte [Configure o projeto do Eclipse e crie o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Para Windows {#for-windows-1}

1. Abra o seguinte Xml em qualquer editor de texto:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Atualize o valor na tag `<name>...</name>`.
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre como criar o aplicativo para Windows, consulte [Configure o projeto do Visual Studio e crie o aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalização de imagens na página de logon {#customizing-images-on-the-login-page}

A página de logon do aplicativo AEM Forms tem imagens de logotipo e plano de fundo. O logotipo está localizado acima da caixa de diálogo de logon e a imagem de fundo está localizada abaixo da caixa de diálogo de logon. Execute as seguintes etapas para personalizar a imagem padrão na página de logon:

**Antes de você iniciar**

Verifique se você tem as seguintes imagens:

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
   <td><p>1280 x 989 pixels</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Para personalizar imagens na página de logon usando o Xcode**

1. Abra o projeto `Capture.xcodeproj` no Xcode.

1. Navegue até a pasta `www/wsmobile/images`.
1. Para alterar o logotipo, substitua o arquivo padrão `LC-logo.png` pelo arquivo personalizado `LC-logo.png`.
1. Para alterar o plano de fundo, substitua o arquivo padrão `Landing_bg.jpeg` pelo arquivo personalizado `Landing_bg.jpeg`.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Abra o projeto do Android no Eclipse.

1. Navegue até a pasta `assets/www/wsmobile/images`.
1. Para alterar o logotipo, substitua o arquivo padrão `LC-logo.png` pelo arquivo personalizado `LC-logo.png`.
1. Para alterar o plano de fundo, substitua o arquivo padrão `Landing_bg.jpeg` pelo arquivo personalizado `Landing_bg.jpeg`.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de logon usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Abra o projeto `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta `MWSWindows\www\wsmobile\images`.
1. Para alterar o logotipo, substitua o arquivo padrão `LC-logo.png` pelo arquivo personalizado `LC-logo.png`.
1. Para alterar o plano de fundo, substitua o arquivo padrão `Landing_bg.jpeg` pelo arquivo personalizado `Landing_bg.jpeg`.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.

## Personalizar o logotipo no menu do aplicativo {#customizing_images_on_the_login_page-1}

Depois de fazer logon no aplicativo AEM Forms e tocar no botão de menu, você poderá ver o logotipo acima do menu. Execute as seguintes etapas para personalizar o logotipo padrão:

**Antes de você iniciar**

Verifique se você tem a seguinte imagem:

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

1. Abra o projeto `Capture.xcodeproj` no Xcode.

1. Navegue até a pasta `www/wsmobile/images`.
1. Para alterar o logotipo, substitua o arquivo padrão `aem_icon.png` pelo arquivo personalizado `aem_icon.png`.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Abra o projeto do Android no Eclipse.

1. Navegue até a pasta `assets/www/wsmobile/images`.
1. Para alterar o logotipo, substitua o arquivo padrão `aem_icon.png` pelo arquivo personalizado `aem_icon.png`.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de logon usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Abra o projeto `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta `MWSWindows\www\wsmobile\images`.
1. Para alterar o logotipo, substitua o arquivo padrão `aem_icon.png` pelo arquivo personalizado `aem_icon.png`.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.
