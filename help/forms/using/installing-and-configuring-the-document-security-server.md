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
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# Instalação e configuração do servidor de segurança do documento {#installing-and-configuring-the-document-security-server}

Use a segurança do documento para distribuir com segurança todas as informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos.

A segurança do documento Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Usando a segurança do documento, é possível distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem Adobe Portable Documento Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

É possível proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um recipient pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os recipient podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor Documento Security; aplique as políticas aos documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. É possível distribuir o documento protegido por política para recipient autorizados pela política.

A segurança do documento também fornece clientes, visualizadores e indexadores para proteger documentos, documentos protegidos por visualização e documentos protegidos por índice. Para obter informações detalhadas sobre a segurança do documento, consulte [sobre a segurança do documento](/help/forms/using/admin-help/document-security.md).

## Topologia de implantação {#deployment-topology}

O recurso de segurança do documento está disponível somente no AEM Forms em JEE. Você precisa de uma única instância do AEM Forms no JEE. Você também pode criar um cluster ou farm de servidores AEM Forms, se necessário. A topologia a seguir indica a topologia para executar a capacidade de segurança do documento. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação para AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

O diagrama a seguir mostra a arquitetura típica da Segurança do Documento AEM Forms:

![](do-not-localize/document-security-typical-environment.png)

## Instalação do AEM Forms em JEE {#installing-aem-forms-on-jee}

Execute as seguintes etapas para instalar e configurar o AEM Forms no JEE:

1. Baixe o instalador do AEM 6.5 Forms em JEE do [Adobe Licensing Website (LWS)](https://licensing.adobe.com/). Você precisa de um contrato válido de manutenção e suporte para baixar o instalador.
1. Leia o documento [AEM Forms on JEE Supported Platforms](/help/forms/using/aem-forms-jee-supported-platforms.md) e verifique se o software, o hardware, os sistemas operacionais, o servidor de aplicativos, os bancos de dados, os JDKs e outras infraestruturas estão prontos para instalar o AEM Forms no JEE.
1. (Somente instalações de chave não-turna) Leia o [Preparando para instalar o AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) ou [Preparando para instalar o cluster de servidores AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) e prepare seu ambiente para instalar e configurar o AEM Forms no JEE.
1. Dependendo do ambiente e do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções para concluir a instalação

   * [Instalar e implantar o AEM Forms no JEE usando o chave-mão JBoss](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Instalação e implantação do AEM Forms no JEE para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Instalação e implantação do AEM Forms no JEE para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Instalação e implantação do AEM Forms no JEE para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuração do AEM Forms em JEE no cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuração do AEM Forms no JEE no cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configurando o AEM Forms no JEE no cluster WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Na tela de seleção Módulo do AEM Forms no gerenciador de configuração JEE, selecione a opção Segurança do Documento. A opção Segurança do Documento não exige que nenhum outro módulo seja selecionado.

## Próximas etapas {#next-steps}

* [Configurar opções de cliente e servidor](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Criar e gerenciar políticas](/help/forms/using/admin-help/creating-policies.md)
* [Criar e gerenciar conjuntos de políticas](/help/forms/using/admin-help/creating-policy-sets.md)
