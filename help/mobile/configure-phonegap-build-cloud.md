---
title: Configurar o Cloud Service Adobe PhoneGap Build
description: Siga esta página para configurar os serviços em nuvem e criar seu aplicativo com o PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Configurar o Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O **Bloco de PhoneGap Build** no painel do aplicativo permite que você crie e distribua seu aplicativo para dispositivos móveis PhoneGap por meio do Serviço Adobe PhoneGap Build.

Todas as plataformas com suporte definidas no bloco **Gerenciar Aplicativo** são criadas com PhoneGap Build ao enviar uma compilação remota com o bloco **PhoneGap Build**.

Você pode enviar uma compilação remota para `https://build.phonegap.com` ou baixar a origem para compilação local com a CLI do PhoneGap em `https://docs.phonegap.com/references/phonegap-cli/`.

![Bloco de PhoneGap Build](assets/chlimage_1-60.png)

## Configuração do Cloud Service {#configuring-the-cloud-service}

Para aproveitar o PhoneGap Build, você deve configurar o Cloud Service de PhoneGap Build AEM com as informações de sua conta de PhoneGap Build.

Se você não tiver uma conta no momento, navegue até `https://build.phonegap.com` e inscreva-se! Se você tiver uma associação do Adobe Creative Cloud, poderá ter suporte para até 25 aplicativos privados (aplicativos de código não aberto).

Depois de verificar se a conta do PhoneGap Build está ativa, navegue até o Console de Gerenciamento da Nuvem AEM, especificamente o [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Use o bloco **Gerenciar Cloud Service** para definir uma nova configuração do serviço de nuvem.

### Utilização do bloco Gerenciar Cloud Service {#using-manage-cloud-services-tile}

Antes de começar a criar seu aplicativo usando o bloco **PhoneGap Build**, você deve configurar os serviços em nuvem usando o bloco **Gerenciar Cloud Service** no painel do AEM Mobile.

Para configurar os serviços em nuvem para seu aplicativo, siga as etapas abaixo:

1. Clique no canto superior direito do bloco **Gerenciar Cloud Service**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Escolha a opção **PhoneGap Build** na tela **Adicionar ou Editar Cloud Service**.

   Clique em **Avançar**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Insira suas credenciais para criar uma configuração na nuvem.

   Depois de verificado, clique em **Enviar**. Esta configuração de nuvem definida agora é exibida no bloco **Gerenciar Cloud Service**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Criando seu aplicativo com o PhoneGap Build {#building-your-application-with-phonegap-build}

Após configurar os serviços em nuvem, você pode criar seu aplicativo com o bloco **PhoneGap Build**. Clique no canto superior direito para escolher entre as opções **Compilar Remoto** ou **Baixar o Source**.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar uma compilação remota com o Adobe PhoneGap Build, clique em **Compilação Remota**.

>[!NOTE]
>
>Se a build falhar por qualquer motivo (o ícone vermelho do iOS abaixo indica que a plataforma falhou), você pode passar o mouse sobre o ícone para receber a mensagem de erro. Como alternativa, você pode clicar no ponto triplo, &#39;...&#39; na parte inferior do bloco para navegar diretamente até `https://build.phonegap.com` (você deve se autenticar) e observar e gerenciar sua compilação diretamente.

### Criando seu aplicativo com a CLI do PhoneGap {#building-your-application-with-phonegap-cli}

O PhoneGap fornece uma interface de linha de comando para criar o aplicativo localmente.

Compile o aplicativo PhoneGap em seu computador usando a CLI (Command-Line Interface, interface de linha de comando) do PhoneGap. Para incluir o conteúdo AEM no aplicativo, o AEM cria um arquivo ZIP que contém o conteúdo do aplicativo móvel, as configurações de sincronização de conteúdo e outros ativos necessários. Baixe o arquivo ZIP e inclua-o na sua versão.

Para aproveitar a CLI do PhoneGap, você deve configurar seu ambiente local para incluir:

1. SDK da Platform (iOS, Android™, Windows Phone ...) e
1. CLI do PhoneGap

Você pode ler mais aqui em `https://docs.phonegap.com/references/phonegap-cli/`.

Depois de instalar os pré-requisitos, faça um teste simples criando um aplicativo simples e executando-o no simulador ou melhor ainda no dispositivo, a partir de uma tentativa de terminal:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>Adicionar — emula no final desta linha se você não quiser executá-la em seu dispositivo conectado.

Depois de verificar se o item acima funciona, use o Bloco **PhoneGap Build** para **Baixar o Source**. Salve e descompacte o arquivo em seu sistema local. Depois que isso for feito:

* navegar até o arquivo salvo (pasta)
* executar &#39;phonegap run ios&#39; (ou android e assim por diante)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Autor e Desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento do Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Criação para Adobe PhoneGap Enterprise no AEM](/help/mobile/phonegap.md)
