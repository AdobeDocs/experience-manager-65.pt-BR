---
title: Importar e gerenciar aplicativos
seo-title: Import and manage applications
description: Saiba como importar e gerenciar aplicativos.
seo-description: Learn how to import and manage applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Importar e gerenciar aplicativos{#import-and-manage-applications}

Em AEM formulários, um *aplicativo* é um contêiner para armazenar ativos necessários para implementar uma solução de formulários AEM. Exemplos de ativos são designs de formulário, fragmentos de formulário, imagens, processos, arquivos DDX, Guias de formulário, HTML pages e arquivos de SWF. Durante a fase de desenvolvimento de um projeto, os usuários do Workbench podem implantar aplicativos diretamente da visualização Aplicativos no Workbench. Depois de implantados, esses aplicativos aparecem no console de administração, na guia Aplicativos da página Gerenciamento de aplicativos .

Quando um aplicativo está concluído e pronto para implantação em um servidor de produção, o usuário do Workbench compacta o aplicativo em um *Arquivo de aplicativo para formulários AEM* (.lca). Em seguida, um administrador usa o console de administração para importar e implantar o arquivo do aplicativo, usando a guia Aplicativos na página Gerenciamento de aplicativos .

Você também pode usar a guia arquivamentos na página Gerenciamento de aplicativos para importar LCAs que foram criadas usando o workbench 8.x.

>[!NOTE]
>
>Há um problema conhecido em que os arquivos LCA de uma versão futura não são necessariamente compatíveis com versões anteriores. Embora seja possível visualizar e importar arquivos LCA de uma versão futura de formulários AEM (por exemplo, uma versão de visualização), isso não é suportado e pode resultar em comportamento aberrante.

Use a guia Aplicativos para importar e gerenciar aplicativos que foram criados no Workbench. Os administradores de aplicativos também podem exportar a configuração de tempo de execução para um aplicativo. Exportar a configuração de tempo de execução elimina a necessidade de redefinir manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados. O arquivo de configuração de tempo de execução contém:

* configurações de serviço
* configurações de pool
* configurações de ponto de extremidade
* perfis de segurança

## Importar um aplicativo ou arquivo {#import-an-application-or-archive}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Clique em Importar.
1. Clique em Procurar, selecione o arquivo .lca a ser importado e clique em Visualizar. A página Visualizar aplicativo exibe informações sobre o aplicativo.
1. (Opcional) Para ver uma lista dos ativos contidos no aplicativo, clique em Exibir ativos.
1. (Opcional) Para implantar os ativos no tempo de execução, selecione Implantar ativos no tempo de execução quando a importação estiver concluída. Se você não selecionar essa opção, poderá implantar os ativos posteriormente.
1. Clique em Importar. O aplicativo é exibido na guia Aplicativos .
1. Faça logon no repositório CRX com credenciais de administrador.
1. Navegue até content/dam/lcapplications

   >[!NOTE]
   >
   >Os aplicativos importados são exibidos no nó lcapplications .

1. Clique em um dos aplicativos importados.

   A guia Properties à direita exibe as propriedades do nó CRX selecionado.

   O **syncState** indica o estado de sincronização dos dados entre o servidor de formulários AEM e o repositório CRX. Assim que o processo de importação começar, esse estado será definido como 0 (zero). Esse estado indica que os dados não estão sincronizados no momento. Quando os dados são sincronizados, o estado é definido como 1.

## Implantar um aplicativo {#deploy-an-application}

É possível implantar aplicativos que você importou ou que usuários do Workbench importaram do Workbench.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja implantar e clique em Implantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Desimplantar um aplicativo {#undeploy-an-application}

Você pode cancelar a implantação de aplicativos no tempo de execução.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja desimplantar e clique em Desimplantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Remover um aplicativo do servidor {#remove-an-application-from-the-server}

Desimplante o aplicativo antes de removê-lo do servidor.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja remover e clique em Remover.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Importar a configuração de tempo de execução de um aplicativo {#import-an-application-s-runtime-configuration}

Se um administrador de aplicativos exportou a configuração de tempo de execução para um aplicativo, você pode importá-lo para o aplicativo implantado. Você pode importá-lo usando o console de administração ou por meio da implantação de LCA com script.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Importar configuração de tempo de execução.
1. Clique em Procurar e selecione o arquivo XML que contém a configuração de tempo de execução.
1. Clique em Importar.

## Exportar a configuração de tempo de execução de um aplicativo {#export-an-application-s-runtime-configuration}

Você pode exportar as informações de configuração do tempo de execução para aplicativos implantados.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Exportar configuração de tempo de execução e salve o arquivo de configuração (XML) produzido.

## Implantação com script de aplicativos AEM forms {#scripted-deployment-of-aem-forms-applications}

Você também pode usar uma ferramenta de implantação com script para implantar arquivos de aplicativo, incluindo um arquivo settings.xml que especifica as seguintes configurações:

* configurações de serviço
* configurações de pool
* configurações de ponto de extremidade
* perfis de segurança

A implantação com script elimina a necessidade de redefinir manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados.

1. Em um prompt de comando, navegue até *[raiz do aem-forms]*/sdk/misc/Foundation/ArchiveManagement.
1. Consulte o arquivo ReadMe.txt para obter instruções mais detalhadas.
1. Modifique manualmente os arquivos scriptedDeploy.bat e sample-files/sample.xml conforme descrito no arquivo readme.txt.
1. Execute o arquivo scriptedDeploy.bat. Essa ação implanta o arquivo de formulários AEM com as configurações de substituição.
