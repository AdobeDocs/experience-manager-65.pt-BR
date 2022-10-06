---
title: Configurar o Cloud Service Adobe PhoneGap Build
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: Siga esta página para configurar os serviços em nuvem e criar seu aplicativo com a build PhoneGap.
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---

# Configurar o Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

O **Bloco PhoneGap Build** no painel de aplicativos, o fornece a capacidade de criar e distribuir seu aplicativo móvel PhoneGap por meio do Adobe PhoneGap Build Service.

Todas as plataformas compatíveis definidas no **Gerenciar aplicativo** O bloco será criado com o PhoneGap Build ao enviar uma build remota com o **PhoneGap Build** Lado a lado.

Você pode enviar uma build remota para o [https://build.phonegap.com](https://build.phonegap.com) ou baixe a fonte para criar localmente com [CLI do PhoneGap](https://docs.phonegap.com/references/phonegap-cli/).

![Bloco PhoneGap Build](assets/chlimage_1-60.png)

## Configuração do Cloud Service {#configuring-the-cloud-service}

Para tirar proveito do PhoneGap Build, você precisa configurar o Cloud Service de PhoneGap Build de AEM com suas informações de conta de PhoneGap Build.

Caso não tenha uma conta no momento, navegue para [https://build.phonegap.com](https://build.phonegap.com) e cadastre-se! Se você tiver uma associação ao Adobe Creative Cloud, poderá ter suporte para até 25 aplicativos privados (aplicativos de origem não abertos).

Depois de verificar se a conta do PhoneGap Build está ativa, navegue até o Console de gerenciamento da AEM Cloud, especificamente o [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Use o **Gerenciar Cloud Services** bloco para configurar uma nova configuração do serviço de nuvem.

### Uso do mosaico Gerenciar Cloud Services {#using-manage-cloud-services-tile}

Antes de começar a criar seu aplicativo usando **PhoneGap Build** bloco , você deve configurar os serviços em nuvem usando o **Gerenciar Cloud Services** bloco do painel do AEM Mobile.

Para configurar serviços em nuvem para seu aplicativo, siga as etapas abaixo:

1. Clique em no canto superior direito do **Gerenciar Cloud Services** mosaico.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Choose **PhoneGap Build** da **Adicionar ou editar Cloud Service** tela.

   Clique em **Avançar**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Insira suas credenciais para criar uma nova configuração de nuvem.

   Depois de verificar, clique em **Enviar**. Essa configuração de nuvem configurada agora é exibida no **Gerenciar Cloud Services** mosaico.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Construindo seu aplicativo com o PhoneGap Build {#building-your-application-with-phonegap-build}

Após configurar os serviços em nuvem, você pode criar seu aplicativo com **PhoneGap Build** mosaico. Clique em no canto superior direito para escolher entre **Criar Remoto** ou **Fonte de download** opções.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar uma build remota com o Adobe PhoneGap Build, clique em **Criar Remoto**.

>[!NOTE]
>
>Se a build falhar por qualquer motivo (o ícone vermelho do iOS abaixo indica que a plataforma falhou), você pode passar o mouse sobre o ícone para obter a mensagem de erro. Como alternativa, você pode clicar no ponto triplo, &#39;...&#39; na parte inferior do bloco, para navegar diretamente para https://build.phonegap.com (você deve autenticar) e assistir e gerenciar a build diretamente.

### Criar seu aplicativo com a CLI do PhoneGap {#building-your-application-with-phonegap-cli}

O PhoneGap fornece uma interface de linha de comando para criar seu aplicativo localmente.

Compile o aplicativo PhoneGap no computador usando a CLI (PhoneGap Command Line Interface, interface de linha de comando do PhoneGap). Para incluir o conteúdo AEM no aplicativo, AEM cria um arquivo ZIP que contém o conteúdo do aplicativo móvel, as configurações de Sincronização de conteúdo e outros ativos necessários. Baixe o arquivo ZIP e inclua-o na sua build.

Para aproveitar ao máximo a interface da linha de comando do PhoneGap, é necessário configurar o ambiente local para incluir:

1. SDK da plataforma (iOS, Android, WindowsPhone, ...) e
1. CLI do PhoneGap

Você pode ler mais [here](https://docs.phonegap.com/references/phonegap-cli/).

Depois de instalar os pré-requisitos, faça um teste simples criando um aplicativo simples e executando-o no simulador ou melhor ainda no dispositivo, a partir de uma tentativa de terminal:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>adicione —emule no final desta linha se não quiser executá-la em seu dispositivo conectado.

Depois de verificar se o acima funciona, use o **PhoneGap Build** Lado a lado **Fonte de download**. Salve e descompacte o arquivo no sistema local. Feito isso:

* navegue até o arquivo salvo (pasta)
* executar &#39;phonegap run ios&#39; (ou android, etc)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um autor e desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Criação para Adobe PhoneGap Enterprise no AEM](/help/mobile/phonegap.md)
