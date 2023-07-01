---
title: Desenvolvimento de aplicativos móveis
description: Esta página fornece um artigo passo a passo completo sobre como criar um aplicativo para dispositivos móveis usando o código disponível no GitHub, que está disponível aqui. Crie seu aplicativo para instalação em um dispositivo ou simulador para teste ou publicação em app stores. Você pode criar aplicativos localmente usando a interface de linha de comando do PhoneGap ou na nuvem usando o PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 4fd5e9a1bc603202ee52e85a1c09125b13cec315
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 1%

---

# Desenvolvimento de aplicativos móveis{#building-mobile-applications}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Crie seu aplicativo para instalação em um dispositivo ou simulador para teste ou publicação em app stores. Você pode criar aplicativos localmente usando a interface de linha de comando do PhoneGap ou na nuvem usando o PhoneGap Build.

Um artigo passo a passo completo sobre como criar um aplicativo móvel usando o código disponível no GitHub está disponível [aqui](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Mover o aplicativo para a instância de publicação {#moving-the-application-to-the-publish-instance}

Mova os arquivos do aplicativo para a instância de publicação, para que você possa fornecer atualizações de conteúdo para as instâncias instaladas do aplicativo móvel e criar o aplicativo usando o conteúdo publicado. Os aplicativos consistem em duas ramificações de nó no repositório:

* `/content/phonegap/apps/<application name>`: as páginas da Web que os autores criam e ativam.
* `/content/phonegap/content/<application name>`: Arquivos de configuração do aplicativo e configurações da Sincronização de conteúdo.

>[!NOTE]
>
>Se você não mover os arquivos do aplicativo para a instância de publicação, os autores de conteúdo não poderão atualizar o cache da sincronização de conteúdo.

Você só precisa mover os arquivos no `/content/phonegap/content/<application name>` para a instância de publicação. Os arquivos no `/content/phonegap/apps/<application name>` As ramificações são movidas quando o autor ativa as páginas.

O AEM fornece dois métodos para mover conteúdo em massa para a instância de publicação:

* [Usar o comando Ativar árvore](/help/sites-authoring/publishing-pages.md) no console de replicação.
* [Criar um pacote](/help/sites-administering/package-manager.md) que contém o conteúdo e replique o pacote.

Por exemplo, um aplicativo móvel chamado phonegapapp é criado. O nó a seguir deve ser movido para a instância de publicação: /content/phonegap/content/phonegapapp.

**Dica:** Para mover um pacote da instância do autor para a instância de publicação, use o comando Replicar no pacote.

![chlimage_1-16](assets/chlimage_1-16.png)

## Criação usando a interface de linha de comando do PhoneGap {#building-using-the-phonegap-command-line-interface}

Compile o aplicativo PhoneGap no computador usando a CLI (Command-line Interface, interface de linha de comando) do PhoneGap. Para incluir o conteúdo AEM no aplicativo, o AEM cria um arquivo ZIP que contém o conteúdo do aplicativo móvel, as configurações de sincronização de conteúdo e outros ativos necessários. Baixe o arquivo ZIP e inclua-o na sua versão.

### Preparação do ambiente de criação {#preparing-your-build-environment}

Para criar usando a CLI do PhoneGap, você precisa instalar o Node.js e o utilitário do cliente PhoneGap. Você precisa de uma conexão com a Internet para executar o procedimento a seguir.

1. Baixar e instalar [Node.js](https://nodejs.org/en).
1. Abra um terminal ou prompt de comando e digite o seguinte comando do nó para instalar o utilitário PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   Em um sistema UNIX® ou Linux®, talvez seja necessário prefixar o comando com `sudo`.

   O terminal mostra os resultados de uma série de comandos HTTP GET. Quando a instalação for bem-sucedida, o terminal mostrará onde as bibliotecas são instaladas, semelhante ao seguinte exemplo:

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

1. (Opcional) Obtenha o SDK para a plataforma móvel para a qual você está direcionando:

   * Para criar aplicativos para a plataforma iOS, instale a versão mais recente do [Xcode](https://developer.apple.com/xcode/).
   * Para criar aplicativos Android™, instale o [Android™ SDK](https://developer.android.com/).

### Download do arquivo ZIP de conteúdo {#downloading-the-content-zip-file}

Mova o conteúdo do aplicativo móvel para o sistema de arquivos.

1. Na página Aplicativos móveis, selecione seu aplicativo.
1. (Opcional) Para criar o aplicativo para instalações completas, na barra de ferramentas, clique no ícone Limpar cache.

   ![Ícone Limpar cache indicado por um símbolo de link quebrado.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >O cache armazena atualizações de conteúdo para aplicativos instalados. A limpeza do cache anula todas as atualizações em cache.

1. Na barra de ferramentas, clique ou toque no ícone Baixar ativos da CLI.

   ![Ícone Download de ativos CLI indicado pelo símbolo de tablet sobreposto.](do-not-localize/chlimage_1-1.png)

1. Depois de salvar o arquivo ZIP, clique em Fechar na caixa de diálogo Êxito.
1. Extraia o conteúdo do arquivo ZIP.

### Uso da CLI do PhoneGap para criar {#using-the-phonegap-cli-to-build}

Use a CLI do PhoneGap para compilar e instalar o aplicativo. Para obter informações sobre como usar a CLI do PhoneGap, consulte a Interface de linha de comando do PhoneGap (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`).

1. Abra um terminal ou prompt de comando e altere o diretório atual para o arquivo ZIP do aplicativo baixado. Por exemplo, o seguinte altera o diretório para o arquivo ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Digite o comando phonegap para a plataforma que você está direcionando. Por exemplo, o comando a seguir cria o aplicativo para Android™:

   ```shell
   phonegap build android
   ```

## Construindo Usando o PhoneGap Build {#building-using-phonegap-build}

Use o serviço de nuvem PhoneGap para criar seu aplicativo. Para executar esse procedimento, primeiro você deve criar uma configuração de PhoneGap Build.

### Conectando ao PhoneGap Build {#connecting-to-phonegap-build}

Crie uma configuração de PhoneGap Build para poder usar os serviços de PhoneGap Build no AEM. Forneça o nome de usuário e a senha da conta do PhoneGap Build que será usada para criar seus aplicativos para dispositivos móveis.

1. Abra a página Ferramentas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Na área Operações do CQ, clique em Cloud Services.
1. Clique no link Configurar agora para o PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Na caixa de diálogo Criar configuração, digite um valor para a propriedade Título. Por padrão, o valor da propriedade Nome é derivado do título, no entanto, você pode inserir um nome. Clique em Criar.
1. Na caixa de diálogo Configuração do PhoneGap Build, digite seu nome de usuário e senha do PhoneGap Build e clique em OK.

### Usando PhoneGap Build {#using-phonegap-build}

Envie os recursos do aplicativo ao PhoneGap Build para compilação nas várias plataformas móveis.

1. Na página Aplicativos móveis, abra o aplicativo móvel. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Opcional) Para criar o aplicativo para instalações completas, selecione o aplicativo e clique no ícone Limpar cache.

   ![Ícone Limpar cache indicado por um símbolo de link quebrado.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >O cache armazena atualizações de conteúdo para aplicativos instalados. A limpeza do cache anula todas as atualizações em cache.

1. Selecione a página inicial e clique no ícone Criar remoto.

   ![Ícone Build Remote indicado por duas engrenagens redondas.](do-not-localize/chlimage_1-3.png)

   **Nota:** A versão Beta do AEM Beta não cria uma notificação na Caixa de entrada quando a build é concluída com sucesso.

1. Na caixa de diálogo Sucesso, clique em PhoneGap Build para abrir a página Adobe PhoneGap Build em `https://build.phonegap.com/apps`. Se estiver esperando o aplicativo aparecer, verifique o Status do PhoneGap Build em `https://status.build.phonegap.com/`.

   Para obter informações sobre como instalar o build, consulte a [Documentação do PhoneGap Build](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Contas de PhoneGap Build gratuito têm permissão para um aplicativo privado. As builds do PhoneGap falham se você estiver criando um aplicativo privado adicional.

### Próximas etapas {#the-next-steps}

A próxima etapa após o processo de construção é aprender sobre o [Estrutura de um aplicativo](/help/mobile/phonegap-structure-an-app.md).
