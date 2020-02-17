---
title: Instalação e configuração do servidor de segurança do documento
seo-title: Instalação e configuração do servidor de segurança do documento
description: 'Use a segurança do documento para distribuir com segurança todas as informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos. '
seo-description: 'Use a segurança do documento para distribuir com segurança todas as informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Instalação e configuração do servidor de segurança do documento {#installing-and-configuring-the-document-security-server}

Use a segurança do documento para distribuir com segurança todas as informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos.

A segurança de documentos do Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Usando a segurança do documento, é possível distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem o Adobe Portable Document Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

É possível proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um destinatário pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor do Document Security; aplique as políticas a documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. É possível distribuir o documento protegido por política para destinatários autorizados pela política.

A segurança de documentos também fornece clientes, visualizadores e indexadores para proteger documentos, exibir documentos protegidos e indexar documentos protegidos. Para obter informações detalhadas sobre a segurança do documento, consulte [sobre a segurança](/help/forms/using/admin-help/document-security.md)do documento.

## Topologia de implantação {#deployment-topology}

O recurso de segurança do documento está disponível somente no AEM Forms em JEE. Você precisa de uma única instância do AEM Forms no JEE. Você também pode criar um cluster ou farm de servidores AEM Forms, se necessário. A topologia a seguir é indicativa da topologia para executar o recurso de segurança do documento. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para o AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

O diagrama a seguir mostra a arquitetura típica do AEM Forms Document Security:

![](do-not-localize/document-security-typical-environment.png)

## Instalação de formulários AEM no JEE {#installing-aem-forms-on-jee}

Execute as seguintes etapas para instalar e configurar o AEM Forms no JEE:

1. Baixe o instalador do AEM 6.5 Forms em JEE do site de licenciamento da [Adobe (LWS)](https://licensing.adobe.com/). Você precisa de um contrato válido de manutenção e suporte para baixar o instalador.
1. Leia o documento [](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM Forms em plataformas suportadas por JEE e verifique se o software, o hardware, os sistemas operacionais, o servidor de aplicativos, os bancos de dados, os JDKs e outras infraestruturas estão prontos para instalar os AEM Forms no JEE.
1. (Somente instalações de não chave na mão) Leia a [Preparação para instalar o servidor](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) único do AEM Forms ou [Preparação para instalar o cluster](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) de servidores do AEM Forms e prepare seu ambiente para instalar e configurar o AEM Forms no JEE.
1. Dependendo do ambiente e do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções para concluir a instalação

   * [Instalar e implantar o AEM Forms no JEE usando chave de acesso JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Instalação e implantação de AEM Forms no JEE para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Instalação e implantação do AEM Forms no JEE para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Instalação e implantação do AEM Forms no JEE para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuração de AEM Forms em JEE no cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configurar o AEM Forms no JEE no cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuração de formulários AEM no cluster JEE no WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)
   >[!NOTE]
   >
   >Na tela de seleção Módulo do AEM Forms no JEE configuration manager, selecione a opção Document Security. A opção Document Security não exige que nenhum outro módulo seja selecionado.

## Próximas etapas {#next-steps}

* [Configurar opções de cliente e servidor](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Criar e gerenciar políticas](/help/forms/using/admin-help/creating-policies.md)
* [Criar e gerenciar conjuntos de políticas](/help/forms/using/admin-help/creating-policy-sets.md)
