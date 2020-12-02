---
title: Desenvolvimento de aplicativos com CLI PhoneGap
seo-title: Desenvolvimento de aplicativos com CLI PhoneGap
description: Siga esta página para saber mais sobre o desenvolvimento de aplicativos com CLI PhoneGap.
seo-description: Siga esta página para saber mais sobre o desenvolvimento de aplicativos com CLI PhoneGap.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Desenvolvimento de aplicativos com o PhoneGap CLI{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

A qualquer momento, como desenvolvedor, você pode executar seu aplicativo em um dispositivo ou em um emulador, desde que tenha configurado seu ambiente de desenvolvimento.

Para executar os seguintes exemplos, você precisará de um sistema que execute o OSx (Mac) com Xcode ou de um sistema Mac/Win/Linux com o Android SDK instalado.

## Bootstrap do ambiente de desenvolvimento {#bootstrap-your-development-environment}

[Configurar CLI do PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

Para iOS: Para desenvolver para iPhones e iPads, você precisa do Xcode IDE da Apple.

* Baixe-o gratuitamente [here](https://developer.apple.com/xcode/downloads/).
* [Guia da plataforma PhoneGap iOS](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Para Android: Para desenvolver para iPhones e iPads, você precisa do Android Stuido IDE do Google.

* Baixe-o gratuitamente [here](https://developer.android.com/sdk/index.html).
* [Guia da plataforma PhoneGap Android](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## Baixar a Fonte {#download-the-source}

Depois de inicializar com êxito seu ambiente de desenvolvimento, baixe a fonte do bloco AEM App Build:

* Clique no ícone suspenso PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Clique em Baixar fonte.
* Selecione a fonte desejada no modal Download Source.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>A fonte de desenvolvimento contém o estado mais recente do seu aplicativo, ao mesmo tempo que inclui alterações não preparadas. Use a fonte de armazenamento temporário para criar candidatos de lançamento para enviar aos fornecedores da app store.
>
>Se você nunca preparar seu aplicativo, selecionar a opção Armazenamento temporário acionará o fluxo de trabalho de armazenamento temporário (dica: isso será exibido como um aplicativo de preparo no aplicativo PhoneGap Enterprise Viewer disponível na AppStore e no Google PlayStore).

* Clique em Baixar e salve o ZIP em seu computador.
* Extraia o arquivo zip baixado para a área de trabalho.

## Criar e carregar o aplicativo (da origem) {#build-and-load-the-app-from-source}

A CLI do PhoneGap pode criar um projeto de plataforma, compilar a fonte e implantar o aplicativo em um único comando.

>[!NOTE]
>
>Você pode executar todas essas etapas separadamente, consulte [PhoneGap CLI docs](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. Verifique se você instalou a CLI PhoneGap, consulte acima.
1. Em uma janela de console (ou terminal), navegue até o diretório raiz da origem extraída.
1. Digite o seguinte comando:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>Se tiver problemas neste momento, volte ao básico para solucionar problemas -
>
>1. Criar uma nova pasta (teste mkdir)
>1. Navegar nesta nova pasta (teste cd)
>1. Executar &#39;phonegap criar helloWorld&#39;
>1. Navegue até helloWorld (cd helloWorld)
>1. Execute &#39;phonegap run android (ou substitua o Android por ios como acima).
>1. O Emulador abrirá a execução do aplicativo PhoneGap recém-criado, dizendo &quot;Pronto para dispositivo&quot; se a ponte JavaScript para nativo estiver operacional.

>
>
Isso verificará se o ambiente de desenvolvimento PhoneGap CLI está ativo e funcionando corretamente.

## Depurar Javascripts com Safari e IOS debug {#debug-javascripts-with-safari-and-ios-debug}

Você pode depurar JavaScripts de seu aplicativo usando as ferramentas de desenvolvedor do Safari, da mesma forma que faria com um aplicativo da Web.

## Ativar ferramentas para desenvolvedores do Safari {#enable-safari-developer-tools}

Para ativar as ferramentas do desenvolvedor:

* Abrir preferências do Safari

   * Clique em Safari na barra de menus
   * Clique em Preferências

* Clique em Avançado na janela Preferência

![chlimage_1-47](assets/chlimage_1-47.png)

* Marque &quot;Mostrar menu Revelação na barra de menus&quot;
* Fechar a janela Preferência

## Connect Safari para iOS {#connect-safari-to-ios}

Você pode conectar o Safari a um dispositivo iOS ou emulador.

* Em uma janela do console, navegue até o diretório raiz da fonte extraída.
* Digite o seguinte comando para iniciar o aplicativo no dispositivo ou emulador.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Abrir o Safari
* Clique em Desenvolver na barra de menus
* Selecione o submenu Simulador do iOS
* Clique em home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Depurar JavaScript com o Inspetor da Web do Safari {#debug-javascript-with-safari-s-web-inspector}

Você pode definir pontos de interrupção em qualquer lugar na sua origem. Quando você interage com seu emulador ou dispositivo, a execução do aplicativo será interrompida nesses pontos de interrupção. Você pode percorrer a execução e inspecionar os valores em variáveis.

* Clique em Recursos na janela Inspetor de Web
* Navegue pela árvore de origem e clique no arquivo de origem desejado
* Clique no número da linha adjacente para adicionar um ponto de interrupção
* Interagir com o dispositivo ou emulador

![chlimage_1-49](assets/chlimage_1-49.png)

* Use os botões de controle para continuar a execução, passe o mouse sobre, passe para dentro e saia dos métodos:

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Para ver os valores das variáveis, no método atual, passe o mouse sobre ele.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre o Desenvolvimento de aplicativos com CLI PhoneGap, consulte [Acessar recursos do dispositivo](/help/mobile/phonegap-access-device-features.md).
