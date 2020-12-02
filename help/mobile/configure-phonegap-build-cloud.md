---
title: Configure seu Cloud Service Adobe PhoneGap Build
seo-title: Configure seu Cloud Service Adobe PhoneGap Build
description: Siga esta página para configurar os serviços em nuvem e criar seu aplicativo com a criação do PhoneGap.
seo-description: Siga esta página para configurar os serviços em nuvem e criar seu aplicativo com a criação do PhoneGap.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# Configure seu Cloud Service Adobe PhoneGap Build {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O **PhoneGap Build mosaico** no painel de aplicativos fornece a capacidade de criar e distribuir seu aplicativo móvel PhoneGap pelo Adobe PhoneGap Build Service.

Todas as plataformas compatíveis definidas no bloco **Gerenciar aplicativo** serão construídas com PhoneGap Build ao enviar uma compilação remota com o bloco **PhoneGap Build**.

Você pode enviar uma compilação remota para [https://build.phonegap.com](https://build.phonegap.com) ou baixar a fonte para criar localmente com [CLI PhoneGap](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build](assets/chlimage_1-60.png)

## Configuração do Cloud Service {#configuring-the-cloud-service}

Para aproveitar melhor o PhoneGap Build, é necessário configurar o Cloud Service de PhoneGap Build de AEM com as informações da conta de PhoneGap Build.

Se você não tiver uma conta no momento, navegue até [https://build.phonegap.com](https://build.phonegap.com) e inscreva-se! Se você tiver uma associação ao Adobe Creative Cloud, poderá ter suporte para até 25 aplicativos privados (aplicativos de origem não abertos).

Depois de verificar se sua conta de PhoneGap Build está ativa, navegue até o console de gerenciamento da AEM Cloud, especificamente o [Cloud Service de PhoneGap Build](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html).

Use o bloco **Gerenciar Cloud Services** para configurar uma nova configuração de serviço em nuvem.

### Usando o bloco Gerenciar Cloud Services {#using-manage-cloud-services-tile}

Antes de começar a criar seu aplicativo usando o bloco **PhoneGap Build**, você deve configurar seus serviços em nuvem usando o bloco **Gerenciar Cloud Services** do painel AEM Mobile.

Para configurar serviços em nuvem para seu aplicativo, siga as etapas abaixo:

1. Clique no canto superior direito do bloco **Gerenciar Cloud Services**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Escolha a opção **PhoneGap Build** na tela **Adicionar ou Editar Cloud Service**.

   Clique em **Avançar**.

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Insira suas credenciais para criar uma nova configuração de nuvem.

   Depois de verificado, clique em **Enviar**. Essa configuração de nuvem configurada agora é exibida no bloco **Gerenciar Cloud Services**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

### Criação do aplicativo com o PhoneGap Build {#building-your-application-with-phonegap-build}

Depois de configurar os serviços em nuvem, você pode criar seu aplicativo com o bloco **PhoneGap Build**. Clique no canto superior direito para escolher entre as opções **Build Remote** ou **Download Source**.

![chlimage_1-64](assets/chlimage_1-64.png)

Para invocar uma compilação remota com o Adobe PhoneGap Build, clique em **Construir remoto**.

>[!NOTE]
>
>Se a compilação falhar por qualquer motivo (o ícone vermelho do iOS abaixo indica que a plataforma falhou), você pode passar o mouse sobre o ícone para obter a mensagem de erro. Como alternativa, você pode clicar no ponto triplo, &#39;...&#39; na parte inferior do bloco para navegar diretamente até https://build.phonegap.com (você deve autenticar) e observar e gerenciar a criação diretamente.

### Criação de seu aplicativo com o PhoneGap CLI {#building-your-application-with-phonegap-cli}

O PhoneGap fornece uma interface de linha de comando para criar seu aplicativo localmente.

Compile o aplicativo PhoneGap em seu computador usando a CLI (Command Line Interface, interface de linha de comando) do PhoneGap. Para incluir o conteúdo AEM em seu aplicativo, AEM cria um arquivo ZIP que contém o conteúdo de seu aplicativo móvel, configurações de Sincronização de conteúdo e outros ativos necessários. Baixe o arquivo ZIP e inclua-o na sua compilação.

Para aproveitar a interface de linha de comando do PhoneGap, é necessário configurar o ambiente local para incluir:

1. Plataforma SDK (iOS, Android, WindowsPhone, ...) e,
1. CLI PhoneGap

Você pode ler mais [aqui](https://docs.phonegap.com/references/phonegap-cli/).

Depois de instalar os pré-requisitos, faça um teste simples criando um aplicativo simples e executando-o no simulador ou melhor ainda no dispositivo, a partir de uma tentativa de terminal:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>adicione —emule ao final desta linha se você não quiser executá-la em seu dispositivo conectado.

Depois de verificar se o procedimento acima funciona, use o bloco **PhoneGap Build** para **Baixar fonte**. Salve e descompacte o arquivo no sistema local. Uma vez feito:

* navegar até o arquivo salvo (pasta)
* executar &#39;phonegap run ios&#39; (ou android etc)

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um autor e desenvolvedor, consulte os recursos abaixo:

* [Desenvolvimento para Adobe PhoneGap Enterprise com AEM](/help/mobile/developing-in-phonegap.md)
* [Criação para Adobe PhoneGap Enterprise no AEM](/help/mobile/phonegap.md)
