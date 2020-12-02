---
title: Importar e gerenciar aplicativos
seo-title: Importar e gerenciar aplicativos
description: Saiba como importar e gerenciar aplicativos.
seo-description: Saiba como importar e gerenciar aplicativos.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---


# Importar e gerenciar aplicativos{#import-and-manage-applications}

Em formulários AEM, um *aplicativo* é um container para armazenar ativos necessários para implementar uma solução de formulários AEM. Exemplos de ativos são designs de formulário, fragmentos de formulário, imagens, processos, arquivos DX, guias de formulário, páginas HTML e arquivos SWF. Durante a fase de desenvolvimento de um projeto, os usuários do Workbench podem implantar aplicativos diretamente da visualização Aplicativos no Workbench. Depois de implantados, esses aplicativos são exibidos no console de administração, na guia Aplicativos da página Gerenciamento de aplicativos.

Quando um aplicativo estiver completo e pronto para implantação em um servidor de produção, o usuário do Workbench agrupará o aplicativo em um *AEM arquivo de aplicativo de formulários* (.lca). Em seguida, um administrador usa o console de administração para importar e implantar o arquivo do aplicativo, usando a guia Aplicativos na página Gerenciamento de aplicativos.

Você também pode usar a guia arquivamentos na página Gerenciamento de aplicativos para importar LCAs criados usando o workbench 8.x.

>[!NOTE]
>
>Há um problema conhecido de que os arquivos LCA de uma versão futura não são necessariamente compatíveis com versões anteriores. Embora seja possível visualização e importar arquivos LCA de uma versão futura de formulários AEM (por exemplo, uma versão de pré-visualização), isso não é suportado e pode resultar em comportamento anormal.

Use a guia Aplicativos para importar e gerenciar aplicativos que foram criados no Workbench. Os administradores de aplicativos também podem exportar a configuração do tempo de execução para um aplicativo. Exportar a configuração do tempo de execução elimina a necessidade de redefinir manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados. O arquivo de configuração do tempo de execução contém:

* configurações de serviço
* configurações do pool
* definições de configuração do ponto de extremidade
* perfis de segurança

## Importar um aplicativo ou arquivo {#import-an-application-or-archive}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique em Importar.
1. Clique em Procurar e selecione o arquivo .lca a ser importado e clique em Pré-visualização. A página Aplicativo de Pré-visualização exibe informações sobre o aplicativo.
1. (Opcional) Para ver uma lista dos ativos contidos no aplicativo, clique em Ativos de Visualização.
1. (Opcional) Para implantar os ativos no tempo de execução, selecione Implantar ativos no tempo de execução quando a importação estiver concluída. Se você não selecionar essa opção, poderá implantar os ativos mais tarde.
1. Clique em Importar. O aplicativo é exibido na guia Aplicativos.
1. Faça logon no repositório CRX com credenciais de administrador.
1. Navegue até content/dam/lcapplications

   >[!NOTE]
   >
   >Os aplicativos importados são exibidos no nó lcapplications.

1. Clique em um dos aplicativos importados.

   A guia Propriedades à direita exibe as propriedades do nó CRX selecionado.

   A propriedade **syncState** indica o estado de sincronização dos dados entre o servidor de formulários AEM e o repositório CRX. Assim que o processo de importação começar, esse estado será definido como 0 (zero). Esse estado indica que os dados não estão sincronizados no momento. Quando os dados são sincronizados, o estado é definido como 1.

## Implantar um aplicativo {#deploy-an-application}

É possível implantar aplicativos que você importou ou que os usuários do Workbench importaram do Workbench.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja implantar e clique em Implantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Desimplantar um aplicativo {#undeploy-an-application}

Você pode desimplantar aplicativos a partir do tempo de execução.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que você deseja desimplantar e clique em Desimplantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Remover um aplicativo do servidor {#remove-an-application-from-the-server}

Desimplante o aplicativo antes de removê-lo do servidor.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja remover e clique em Remover.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Importar a configuração do tempo de execução de um aplicativo {#import-an-application-s-runtime-configuration}

Se um administrador do aplicativo tiver exportado a configuração do tempo de execução de um aplicativo, você poderá importá-lo para o aplicativo implantado. É possível importá-lo usando o console de administração ou por meio da implantação LCA com script.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Importar configuração de tempo de execução.
1. Clique em Procurar e selecione o arquivo XML que contém a configuração do tempo de execução.
1. Clique em Importar.

## Exportar a configuração do tempo de execução de um aplicativo {#export-an-application-s-runtime-configuration}

Você pode exportar as informações de configuração do tempo de execução para aplicativos implantados.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Exportar configuração de tempo de execução e salve o arquivo de configuração (XML) produzido.

## Implantação com script de aplicativos de formulários AEM {#scripted-deployment-of-aem-forms-applications}

Você também pode usar uma ferramenta de implantação com script para implantar arquivos do aplicativo, incluindo um arquivo settings.xml que especifica as seguintes configurações:

* configurações de serviço
* configurações do pool
* definições de configuração do ponto de extremidade
* perfis de segurança

A implantação com script elimina a necessidade de reconfigurar manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados.

1. Em um prompt de comando, navegue até *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Consulte o arquivo ReadMe.txt para obter instruções mais detalhadas.
1. Modifique manualmente os arquivos scriptedDeploy.bat e sample-files/sample.xml como descrito no arquivo readme.txt.
1. Execute o arquivo scriptedDeploy.bat. Esta ação implanta o arquivo de arquivamento de formulários AEM com as configurações de substituição.

