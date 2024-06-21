---
title: Instalação e configuração do servidor de segurança de documentos
description: Use a segurança de documentos para distribuir com segurança quaisquer informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos.
contentOwner: khsingh
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 939a2efa64c853928a9082aa30d7338e98deb695
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Instalação e configuração do servidor de segurança de documentos {#installing-and-configuring-the-document-security-server}

Use a segurança de documentos para distribuir com segurança quaisquer informações salvas em um formato compatível. Somente usuários autorizados podem acessar documentos protegidos.

A segurança de documentos do Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Com a segurança de documentos, você pode distribuir com segurança qualquer informação que tenha sido salva em um formato compatível. Os formatos de arquivo compatíveis incluem Adobe Portable Document Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

Você pode proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um destinatário pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor de Segurança de documentos; você aplica as políticas aos documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações contidas no documento. Você pode distribuir o documento protegido por política para recipients autorizados pela política.

A segurança de documentos também fornece clientes, visualizadores e indexadores para proteger documentos, exibir documentos protegidos e indexar documentos protegidos. Para obter informações detalhadas sobre segurança de documentos, consulte [sobre a segurança de documentos](/help/forms/using/admin-help/document-security.md).

## Topologia de implantação  {#deployment-topology}

O recurso de segurança de documentos está disponível somente no AEM Forms no JEE. Você precisa de uma única instância do AEM Forms no JEE. Você também pode criar um cluster ou farm de servidores do AEM Forms, se necessário. A topologia a seguir é uma topologia indicativa para executar o recurso de segurança de documentos. Para obter informações detalhadas sobre a topologia, consulte [Arquitetura e topologias de implantação do AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![Topologia do servidor de segurança de documentos](do-not-localize/document-security-server_topology.png)

O diagrama a seguir mostra a arquitetura típica da Segurança de documentos do AEM Forms:

![Ambiente típico de segurança de documentos](do-not-localize/document-security-typical-environment.png)

## Instalação do AEM Forms no JEE {#installing-aem-forms-on-jee}

Execute as seguintes etapas para instalar e configurar o AEM Forms no JEE:

1. Baixe o instalador do AEM 6.5 Forms no JEE [Site de Licenciamento de Adobe (LWS)](https://licensing.adobe.com/). Você precisa de um contrato válido de Manutenção e Suporte para baixar o instalador.
1. Leia o [Documento AEM Forms nas plataformas compatíveis com JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) e garantir que o software, o hardware, os sistemas operacionais, o servidor de aplicativos, os bancos de dados, os JDKs e outras infraestruturas estejam prontos para instalar o AEM Forms no JEE.
1. (Somente para instalações que não sejam de teclas na mão) Leia o [Preparação para instalar o AEM Forms single server](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) ou [Preparando-se para instalar o cluster de servidores do AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) e prepare seu ambiente para instalar e configurar o AEM Forms no JEE.
1. Dependendo do ambiente e do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções para concluir a instalação

   * [Instalação e implantação do AEM Forms no JEE usando o JBoss turnkey](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Instalação e implantação do AEM Forms no JEE para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Instalação e implantação do AEM Forms no JEE para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Instalação e implantação do AEM Forms no JEE para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuração do AEM Forms no JEE no cluster JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuração do AEM Forms no JEE no cluster WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuração do AEM Forms no JEE no cluster do WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Na tela Seleção de módulo do AEM Forms no gerenciador de configurações JEE, selecione a opção Segurança de documentos. A opção Segurança de documentos não requer a seleção de nenhum outro módulo.

## Próximas etapas {#next-steps}

* [Configurar opções de cliente e servidor](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Criação e gerenciamento de políticas](/help/forms/using/admin-help/creating-policies.md)
* [Criar e gerenciar conjuntos de políticas](/help/forms/using/admin-help/creating-policy-sets.md)
