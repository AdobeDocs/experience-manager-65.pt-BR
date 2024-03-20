---
title: Importar e gerenciar aplicativos
description: Saiba como importar e gerenciar aplicativos. Um aplicativo é um container para armazenar ativos necessários à implementação de uma solução de formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Importar e gerenciar aplicativos{#import-and-manage-applications}

Nos formulários AEM, um *aplicativo* O é um container para armazenar ativos necessários à implementação de uma solução de formulários AEM. Exemplos de ativos são designs de formulário, fragmentos de formulário, imagens, processos, arquivos DDX, guias de formulário, páginas de HTML e arquivos SWF. Durante a fase de desenvolvimento de um projeto, os usuários do Workbench podem implantar aplicativos diretamente da visualização Aplicativos no Workbench. Depois de implantados, esses aplicativos aparecem no console de administração, na guia Aplicativos da página Gerenciamento de aplicativos.

Quando um aplicativo está concluído e pronto para implantação em um servidor de produção, o usuário do Workbench compacta o aplicativo em um *Arquivo de aplicativo de formulários AEM* (.lca). Em seguida, um administrador usa o console de administração para importar e implantar o arquivo de aplicativo, usando a guia Aplicativos na página Gerenciamento de aplicativos.

Você também pode usar a guia arquivos na página Gerenciamento de aplicativos para importar LCAs que foram criadas usando o Workbench 8.x.

>[!NOTE]
>
>Há um problema conhecido de que os arquivos LCA de uma versão futura não são necessariamente compatíveis com versões anteriores. Embora seja possível visualizar e importar arquivos LCA de uma versão futura do AEM Forms (por exemplo, uma versão de pré-visualização), isso não é suportado e pode resultar em um comportamento aberrante.

Use a guia Aplicativos para importar e gerenciar aplicativos criados no Workbench. Os administradores de aplicativos também podem exportar a configuração de tempo de execução de um aplicativo. A exportação da configuração de tempo de execução elimina a necessidade de redefinir manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados. O arquivo de configuração de tempo de execução contém:

* definições de configuração do serviço
* definições de configuração do pool
* definições de configuração do endpoint
* perfis de segurança

## Importar um aplicativo ou arquivo {#import-an-application-or-archive}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique em Importar.
1. Clique em Procurar, selecione o arquivo .lca a ser importado e clique em Visualizar. A página Visualizar Aplicativo exibe informações sobre o aplicativo.
1. (Opcional) Para ver uma lista dos ativos contidos no aplicativo, clique em Exibir ativos.
1. (Opcional) Para implantar os ativos no tempo de execução, selecione Implantar ativos no tempo de execução quando a importação estiver concluída. Se você não selecionar essa opção, será possível implantar os ativos posteriormente.
1. Clique em Importar. O aplicativo é exibido na guia Aplicativos.
1. Faça logon no repositório CRX com credenciais de administrador.
1. Navegar até content/dam/capplications

   >[!NOTE]
   >
   >Os aplicativos importados são exibidos no nó capplications.

1. Clique em um dos aplicativos importados.

   A guia Propriedades à direita exibe as propriedades do nó CRX selecionado.

   A variável **syncState** indica o estado de sincronização de dados entre o AEM Forms Server e o repositório CRX. Assim que o processo de importação começar, esse estado é definido como 0 (zero). Este estado indica que os dados não estão sincronizados no momento. Quando os dados são sincronizados, o estado é definido como 1.

## Implantar um aplicativo {#deploy-an-application}

Você pode implantar aplicativos importados ou que os usuários do Workbench importaram do Workbench.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja implantar e clique em Implantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Desimplantar um aplicativo {#undeploy-an-application}

Você pode desimplantar aplicativos do tempo de execução.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado da aplicação que você deseja desimplantar e clique em Desimplantar.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Remover um aplicativo do servidor {#remove-an-application-from-the-server}

Desimplante o aplicativo antes de removê-lo do servidor.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Marque a caixa de seleção ao lado do aplicativo que deseja remover e clique em Remover.
1. Clique em OK na caixa de diálogo de confirmação exibida.

## Importar a configuração de tempo de execução de um aplicativo {#import-an-application-s-runtime-configuration}

Se um administrador de aplicativo exportou a configuração de tempo de execução de um aplicativo, você pode importá-lo para o aplicativo implantado. Você pode importá-lo usando o console de administração ou por meio da implantação do LCA com script.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Importar configuração de tempo de execução.
1. Clique em Procurar e selecione o arquivo XML que contém a configuração de tempo de execução.
1. Clique em Importar.

## Exportar a configuração de tempo de execução de um aplicativo {#export-an-application-s-runtime-configuration}

Você pode exportar as informações de configuração de tempo de execução dos aplicativos implantados.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos.
1. Clique no nome do aplicativo.
1. Clique em Exportar configuração de tempo de execução e salve o arquivo de configuração (XML) produzido.

## Implantação com script de aplicativos de formulários AEM {#scripted-deployment-of-aem-forms-applications}

Você também pode usar uma ferramenta de disponibilização com script para disponibilizar arquivos da aplicação, incluindo um arquivo settings.xml que especifica as seguintes definições:

* definições de configuração do serviço
* definições de configuração do pool
* definições de configuração do endpoint
* perfis de segurança

A implantação com script elimina a necessidade de redefinir manualmente as configurações no ambiente de produção antes de iniciar os aplicativos implantados.

1. Em um prompt de comando, navegue até *[raiz de aem-forms]*/sdk/misc/Foundation/ArchiveManagement.
1. Consulte o arquivo ReadMe.txt para obter instruções mais detalhadas.
1. Modifique manualmente os arquivos scriptedDeploy.bat e sample-files/sample.xml conforme descrito no arquivo readme.txt.
1. Execute o arquivo scriptedDeploy.bat. Essa ação implanta o arquivo de arquivamento de formulários AEM com as configurações de substituição.
