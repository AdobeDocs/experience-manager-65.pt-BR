---
title: Personalização da marca
description: Personalize o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e a página de logon para fornecer uma aparência distinta específica da organização para o aplicativo AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# Personalização da marca {#branding-customization}

É possível personalizar o ícone do aplicativo, o nome do aplicativo, as imagens de inicialização e a página de logon para fornecer uma aparência distinta e específica da organização para o aplicativo AEM Forms. Por exemplo, você pode alterar as imagens para usar logotipos da sua organização. O aplicativo AEM Forms é compatível com as seguintes personalizações:

* Personalização do ícone do aplicativo e imagens de inicialização
* Personalização do nome do aplicativo
* Personalização de imagens na página de logon
* Personalização do logotipo no menu do aplicativo

## Personalização de ícones e imagens de lançamentos {#customizing-icon-and-launch-images}

Execute as seguintes etapas para personalizar o ícone do aplicativo padrão e a imagem de inicialização do aplicativo AEM Forms:

>[!NOTE]
>
>Para todos os ícones e imagens, use o formato PNG não entrelaçado.

### Para personalizar imagens de ícones e inicializações {#to-customize-icon-and-launch-images}

#### Para iOS {#for-ios}

1. Abra o `Capture.xcodeproj` projeto no Xcode.
1. (***Para personalizar o ícone***) Na visualização do navegador da Captura, navegue até **[!UICONTROL Capturar > Capturar > Arquivos de suporte > Capture-info.plist]**. Clique na lista suspensa ao lado dos arquivos de ícone. Especifique o nome do arquivo de ícone (.png) e faça upload do arquivo em **[!UICONTROL Capturar > Capturar > Recursos > ícones]**. As dimensões compatíveis no momento são: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Para personalizar imagens do Launch***) Verifique se os nomes de arquivo das imagens são:

   * Para retrato: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Para paisagem: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Faça upload deles para o projeto Capture para substituir arquivos existentes no projeto.

   >[!NOTE]
   >
   >Verifique se o nome e a resolução da imagem correspondem à imagem substituída no projeto.

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
   >Verifique se o nome e a resolução da imagem correspondem à imagem substituída no projeto.

1. Recrie o aplicativo AEM Forms.

### Para Windows {#for-windows}

1. Substitua os ícones no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Substitua a imagem do iniciador no caminho:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Verifique se o nome e a resolução da imagem correspondem à imagem substituída no projeto.

1. Recrie o aplicativo AEM Forms.

## Personalizar o nome do aplicativo {#customize-the-app-name}

### Para iOS {#for-ios-1}

1. Abra o `Capture.xcodeproj` projeto no Xcode.
1. Na view do navegador Captura, navegue até **[!UICONTROL Capturar > Capturar > Arquivos de Suporte > InfoPlist.strings]**.

   Atualize o valor para o `CFBundleDisplayName` para um nome que deseja exibir para o aplicativo.

1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

   Para obter detalhes sobre a criação do aplicativo para iOS, consulte [Configurar o projeto Xcode e criar o aplicativo iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Para Android {#for-android-1}

1. Abra o seguinte Xml em qualquer texto ou editor de Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Atualizar o valor da chave `app_name`.
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre a criação do aplicativo para Android, consulte [Configurar o projeto Eclipse e criar o aplicativo Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Para Windows {#for-windows-1}

1. Abra o seguinte Xml em qualquer editor de texto:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Atualize o valor no `<name>...</name>` tag.
1. Recrie o aplicativo AEM Forms.

   Para obter detalhes sobre a criação do aplicativo para Windows, consulte [Configurar o projeto do Visual Studio e criar o aplicativo do Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalização de imagens na página de logon {#customizing-images-on-the-login-page}

A página de logon do aplicativo AEM Forms tem logotipo e imagens de fundo. O logotipo está localizado acima da caixa de diálogo de logon e a imagem de fundo está localizada abaixo da caixa de diálogo de logon. Execute as seguintes etapas para personalizar a imagem padrão na página de logon:

**Antes de começar**

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

1. Abra o `Capture.xcodeproj` projeto no Xcode.

1. Navegue até a `www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` arquivo com o personalizado `LC-logo.png` arquivo.
1. Para alterar o fundo, substitua o padrão `Landing_bg.jpeg` arquivo com o personalizado `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Abra o projeto Android no Eclipse.

1. Navegue até a `assets/www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` arquivo com o personalizado `LC-logo.png` arquivo.
1. Para alterar o fundo, substitua o padrão `Landing_bg.jpeg` arquivo com o personalizado `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de logon usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Abra o `MWSWindows.sln` projeto no Visual Studio.

1. Navegue até a `MWSWindows\www\wsmobile\images`pasta.
1. Para alterar o logotipo, substitua o padrão `LC-logo.png` arquivo com o personalizado `LC-logo.png` arquivo.
1. Para alterar o fundo, substitua o padrão `Landing_bg.jpeg` arquivo com o personalizado `Landing_bg.jpeg`arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.

## Personalização do logotipo no menu do aplicativo {#customizing_images_on_the_login_page-1}

Depois de fazer logon no aplicativo AEM Forms e selecionar o botão de menu, você pode ver o logotipo acima do menu. Execute as seguintes etapas para personalizar o logotipo padrão:

**Antes de começar**

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

1. Abra o `Capture.xcodeproj` projeto no Xcode.

1. Navegue até a `www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` arquivo com o personalizado `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo iOS ou no simulador iOS.

### Para personalizar imagens nas páginas de logon usando o Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Abra o projeto Android no Eclipse.

1. Navegue até a `assets/www/wsmobile/images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` arquivo com o personalizado `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Android.

### Para personalizar imagens nas páginas de logon usando o Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Abra o `MWSWindows.sln` projeto no Visual Studio.

1. Navegue até a `MWSWindows\www\wsmobile\images`pasta.
1. Para alterar o logotipo, substitua o padrão `aem_icon.png` arquivo com o personalizado `aem_icon.png` arquivo.
1. Crie e execute o aplicativo AEM Forms no dispositivo Windows.
