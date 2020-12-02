---
title: Criação de aplicativos móveis
seo-title: Criação de aplicativos móveis
description: Esta página fornece um artigo passo a passo completo sobre como criar um aplicativo móvel usando o código disponível no GitHub está disponível aqui.Crie seu aplicativo para instalar em um dispositivo ou simulador para teste ou para publicação em app stores. Você pode criar aplicativos localmente usando a interface de linha de comando PhoneGap ou na nuvem usando o PhoneGap Build.
seo-description: Esta página fornece um artigo passo a passo completo sobre como criar um aplicativo móvel usando o código disponível no GitHub está disponível aqui.Crie seu aplicativo para instalar em um dispositivo ou simulador para teste ou para publicação em app stores. Você pode criar aplicativos localmente usando a interface de linha de comando PhoneGap ou na nuvem usando o PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 1%

---


# Criação de aplicativos móveis{#building-mobile-applications}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Crie seu aplicativo para instalar em um dispositivo ou simulador para teste ou para publicação em app stores. Você pode criar aplicativos localmente usando a interface de linha de comando PhoneGap ou na nuvem usando o PhoneGap Build.

Um artigo passo a passo completo sobre como criar um aplicativo móvel usando o código disponível do GitHub está disponível [aqui](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Mover o aplicativo para a instância de publicação {#moving-the-application-to-the-publish-instance}

Mova os arquivos do aplicativo para a instância de publicação para que você possa fornecer atualizações de conteúdo às instâncias instaladas do aplicativo móvel e para criar o aplicativo usando o conteúdo publicado. Os aplicativos consistem em duas ramificações de nó no repositório:

* `/content/phonegap/apps/<application name>`: As páginas da Web que os autores criam e ativam.
* `/content/phonegap/content/<application name>`: Arquivos de configuração do aplicativo e configurações de Sincronização de conteúdo.

>[!NOTE]
>
>Se você não mover os arquivos do aplicativo para a instância de publicação, os autores de conteúdo não poderão atualizar o cache de Sincronização de conteúdo.

Você só precisa mover os arquivos na ramificação `/content/phonegap/content/<application name>` para a instância de publicação. Os arquivos na ramificação `/content/phonegap/apps/<application name>` são movidos quando o autor ativa as páginas.

AEM fornece dois métodos para mover o conteúdo em massa para a instância de publicação:

* [Use o comando Ativar árvore ](/help/sites-authoring/publishing-pages.md) no console de replicação.
* [Crie um ](/help/sites-administering/package-manager.md) pacote que contenha o conteúdo e replique o pacote.

Por exemplo, um aplicativo móvel chamado phonegapp é criado. O nó a seguir deve ser movido para a instância de publicação: /content/phonegap/content/phonegapp.

**Dica:** para mover um pacote da instância do autor para a instância de publicação, use o comando Replicar no pacote.

![chlimage_1-16](assets/chlimage_1-16.png)

## Criando usando a interface de linha de comando do PhoneGap {#building-using-the-phonegap-command-line-interface}

Compile o aplicativo PhoneGap em seu computador usando a CLI (Command-line Interface, interface de linha de comando) do PhoneGap. Para incluir o conteúdo AEM em seu aplicativo, AEM cria um arquivo ZIP que contém o conteúdo de seu aplicativo móvel, configurações de Sincronização de conteúdo e outros ativos necessários. Baixe o arquivo ZIP e inclua-o na sua compilação.

### Preparando seu Ambiente de compilação {#preparing-your-build-environment}

Para criar usando a CLI PhoneGap, é necessário instalar o Node.js e o utilitário cliente PhoneGap. Você precisa de uma conexão com a Internet para executar o seguinte procedimento.

1. Baixe e instale [Node.js](https://nodejs.org/).
1. Abra um terminal ou prompt de comando e digite o seguinte comando de nó para instalar o utilitário PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   Em um sistema Unix ou Linux, talvez seja necessário prefixar o comando com `sudo`.

   O terminal mostra os resultados de uma série de comandos de GET HTTP. Quando a instalação for bem-sucedida, o terminal mostrará onde as bibliotecas estão instaladas de maneira semelhante ao exemplo a seguir:

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. (Opcional) Obtenha o SDK para a plataforma móvel que você está direcionando:

   * Para criar aplicativos para a plataforma iOS, instale a versão mais recente do [Xcode](https://developer.apple.com/xcode/).
   * Para criar aplicativos Android, instale o [Android SDK](https://developer.android.com/).

### Download do arquivo ZIP de conteúdo {#downloading-the-content-zip-file}

Mova o conteúdo do aplicativo móvel para o sistema de arquivos.

1. Na página Aplicativos móveis, selecione seu aplicativo.
1. (Opcional) Para criar o aplicativo para instalações completas, na barra de ferramentas, clique ou toque no ícone Limpar cache.

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >O cache contém atualizações de conteúdo para aplicativos instalados. Limpar o cache evita todas as atualizações em cache.

1. Na barra de ferramentas, clique ou toque no ícone Baixar ativos CLI.

   ![](do-not-localize/chlimage_1-1.png)

1. Depois de salvar o arquivo ZIP, clique em Fechar na caixa de diálogo Êxito.
1. Extraia o conteúdo do arquivo ZIP.

### Usando a CLI do PhoneGap para criar {#using-the-phonegap-cli-to-build}

Use a CLI do PhoneGap para compilar e instalar o aplicativo. Para obter informações sobre como usar a CLI PhoneGap, consulte a documentação PhoneGap [Command-line Interface](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html).

1. Abra um terminal ou prompt de comando e altere o diretório atual para o arquivo ZIP do aplicativo baixado. Por exemplo, o seguinte altera o diretório para o arquivo ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Digite o comando phonegap para a plataforma que você está definindo como meta. Por exemplo, o seguinte comando cria o aplicativo para Android:

   ```shell
   phonegap build android
   ```

## Criando usando o PhoneGap Build {#building-using-phonegap-build}

Use o serviço de nuvem PhoneGap para criar seu aplicativo. Para executar esse procedimento, é necessário primeiro criar uma configuração de PhoneGap Build.

### Conectando ao PhoneGap Build {#connecting-to-phonegap-build}

Crie uma configuração de PhoneGap Build para que você possa usar os serviços de PhoneGap Build de dentro do AEM. Forneça o nome de usuário e a senha da conta de PhoneGap Build que você usará para criar seus aplicativos móveis.

1. Abra a página Ferramentas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Na área Operações do CQ, clique em Cloud Services.
1. Clique no link Configurar agora para PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Na caixa de diálogo Criar configuração, digite um valor para a propriedade Título. Por padrão, o valor da propriedade Name é derivado do título, no entanto, é possível inserir um nome. Clique em Criar.
1. Na caixa de diálogo Configuração do PhoneGap Build, digite o nome de usuário e a senha do PhoneGap Build e clique em OK.

### Usando o PhoneGap Build {#using-phonegap-build}

Envie seus recursos de aplicativo para o PhoneGap Build para compilação para as várias plataformas móveis.

1. Na página Aplicativos móveis, abra seu aplicativo móvel. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Opcional) Para criar o aplicativo para instalações completas, selecione o aplicativo e clique no ícone Limpar cache.

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >O cache contém atualizações de conteúdo para aplicativos instalados. Limpar o cache evita todas as atualizações em cache.

1. Selecione a página inicial e clique no ícone Criar remoto.

   ![](do-not-localize/chlimage_1-3.png)

   **Observação:** a versão Beta do AEM Beta não cria uma notificação Caixa de entrada quando a compilação é concluída com êxito.

1. Na caixa de diálogo Êxito, clique em PhoneGap Build para abrir a página do Adobe PhoneGap Build em [https://build.phonegap.com/apps](https://build.phonegap.com/apps). Se você estiver esperando que seu aplicativo apareça, poderá verificar a página [Status do PhoneGap Build](https://status.build.phonegap.com/).

   Para obter informações sobre como instalar a compilação, consulte a [Documentação do PhoneGap Build](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29).

   >[!NOTE]
   >
   >Contas de PhoneGap Build gratuito são permitidas em um aplicativo privado. As compilações do PhoneGap falham se você estiver criando um aplicativo privado adicional.

### Próximas etapas {#the-next-steps}

A próxima etapa após o processo de criação é aprender sobre a [Estrutura de um aplicativo](/help/mobile/phonegap-structure-an-app.md).
