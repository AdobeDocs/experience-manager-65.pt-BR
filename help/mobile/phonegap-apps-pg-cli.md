---
title: Desenvolvimento de aplicativos com a CLI do PhoneGap
seo-title: Developing Apps with PhoneGap CLI
description: Siga esta página para saber mais sobre como desenvolver aplicativos com a CLI do PhoneGap.
seo-description: Follow this page to learn about developing apps with PhoneGap CLI.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Desenvolvimento de aplicativos com a CLI do PhoneGap{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A qualquer momento, como desenvolvedor, você pode executar o aplicativo em um dispositivo ou em um emulador, desde que tenha configurado o ambiente de desenvolvimento.

Para executar os exemplos a seguir, será necessário um sistema que execute OSx (Mac) com Xcode ou um sistema Mac/Win/Linux com o Android SDK instalado.

## Bootstrap do ambiente de desenvolvimento {#bootstrap-your-development-environment}

[Configurar CLI do PhoneGap](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

Para iOS: para desenvolver iPhones e iPads, é necessário o Xcode IDE da Apple.

* Baixe gratuitamente [aqui](https://developer.apple.com/xcode/downloads/).
* [Guia da plataforma PhoneGap iOS](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Para Android: para desenvolver iPhones e iPads, é necessário o Android Studio IDE da Google.

* Baixe gratuitamente [aqui](https://developer.android.com/sdk/index.html).
* [Guia da plataforma PhoneGap Android](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## Baixar a Origem {#download-the-source}

Depois de inicializar seu ambiente de desenvolvimento com êxito, baixe a origem do Bloco de build do aplicativo AEM:

* Clique na divisa suspensa do bloco PhoneGap Build.

![chlimage_1-45](assets/chlimage_1-45.png)

* Clique em Baixar origem.
* Selecione a origem desejada no modal Origem de download.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>A fonte de desenvolvimento contém o estado mais recente do aplicativo, enquanto inclui alterações não preparadas. Use a fonte de Preparo para criar candidatos a lançamento para enviar a fornecedores da loja de aplicativos.
>
>Se você nunca preparar seu aplicativo, selecionar Preparo acionará o fluxo de trabalho de preparo (dica: isso será exibido como um aplicativo preparado no aplicativo Visualizador Corporativo do PhoneGap, disponível na AppStore e na Google PlayStore).

* Clique em Baixar e salve o ZIP no computador.
* Extraia o arquivo zip baixado para o espaço de trabalho.

## Criar e carregar o aplicativo (da origem) {#build-and-load-the-app-from-source}

A CLI do PhoneGap pode criar um projeto de plataforma, compilar o código-fonte e implantar o aplicativo em um único comando.

>[!NOTE]
>
>É possível executar todas essas etapas separadamente, consulte [Documentos CLI do PhoneGap](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. Certifique-se de ter instalado a CLI do PhoneGap; veja acima.
1. Em uma janela de console (ou terminal), navegue até o diretório raiz da origem extraída.
1. Digite o seguinte comando:

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>Se você tiver problemas neste momento, volte aos conceitos básicos para solucionar problemas -
>
>1. Criar uma nova pasta (teste mkdir)
>1. Navegar para esta nova pasta (teste de cd)
>1. Executar &#39;phonegap create helloWorld&#39;
>1. Navegue até helloWorld (cd helloWorld)
>1. Execute &#39;phonegap run android (ou substitua android por ios como descrito acima).
>1. O emulador será aberto executando o aplicativo PhoneGap recém-criado, informando &quot;Device Ready&quot; (Pronto para dispositivo) se a ponte JavaScript para o nativo estiver operacional.

>
>Isso verificará se o ambiente de desenvolvimento da CLI do PhoneGap está funcionando corretamente.

## Depurar JavaScripts com a depuração do Safari e do IOS {#debug-javascripts-with-safari-and-ios-debug}

Você pode depurar os JavaScripts do aplicativo usando as ferramentas de desenvolvedor do Safari, da mesma forma que faria com um aplicativo web.

## Ativar as ferramentas de desenvolvedor do Safari {#enable-safari-developer-tools}

Para ativar as ferramentas do desenvolvedor:

* Abrir preferências do Safari

   * Clique no Safari na barra de menus
   * Clique em Preferências

* Clique em Avançado na janela Preferência

![chlimage_1-47](assets/chlimage_1-47.png)

* Marque &quot;Mostrar menu Desenvolver na barra de menus&quot;
* Fechar a janela Preferências

## Conectar o Safari ao iOS {#connect-safari-to-ios}

Você pode conectar o Safari a um dispositivo ou emulador do iOS.

* Em uma janela de console, navegue até o diretório raiz da origem extraída.
* Digite o seguinte comando para iniciar seu aplicativo no dispositivo ou emulador.

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* Abrir o Safari
* Clique em Desenvolver na barra de menus
* Selecionar submenu do iOS Simulator
* Clique em home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## Depurar JavaScript com o Inspetor da Web do Safari {#debug-javascript-with-safari-s-web-inspector}

Você pode definir pontos de interrupção em qualquer lugar na sua origem. Quando você interage com o emulador ou dispositivo, a execução do aplicativo é interrompida nesses pontos de interrupção. Você pode percorrer a execução e inspecionar os valores nas variáveis.

* Clique em Recursos na janela Inspetor Web
* Navegue pela árvore de origem e clique no arquivo de origem desejado
* Clique no número da linha adjacente para adicionar um ponto de interrupção
* Interagir com dispositivo ou emulador

![chlimage_1-49](assets/chlimage_1-49.png)

* Use os botões de controle para continuar a execução, passar por cima, entrar e sair dos métodos:

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>Para ver os valores das variáveis, no método atual, passe o mouse sobre ele.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre o desenvolvimento de aplicativos com a CLI do PhoneGap, consulte [Acessar recursos do dispositivo](/help/mobile/phonegap-access-device-features.md).
