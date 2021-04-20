---
title: Definição das configurações de administração segura para AEM Forms no JEE
seo-title: Definição das configurações de administração segura para AEM Forms no JEE
description: Saiba como administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.
seo-description: Saiba como administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# Definição das configurações de administração segura para AEM Forms no JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Saiba como administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.

Geralmente, os desenvolvedores não usam o ambiente de produção para criar e testar seus aplicativos. Portanto, você deve administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção.

Este artigo descreve métodos para reduzir a superfície geral dos ataques por meio de opções de administração fornecidas pelo AEM Forms no JEE.

## Desativar o acesso remoto não essencial aos serviços {#disabling-non-essential-remote-access-to-services}

Depois que o AEM Forms no JEE é instalado e configurado, muitos serviços estão disponíveis para invocação remota sobre SOAP e Enterprise JavaBeans™ (EJB). O termo remoto, neste caso, refere-se a qualquer chamador que tenha acesso de rede às portas SOAP, EJB ou Formato de Mensagem de Ação (AMF) para o servidor de aplicativos.

Embora a AEM Forms em serviços JEE exija que credenciais válidas sejam passadas para um chamador autorizado, você deve permitir somente acesso remoto aos serviços que você precisa acessar remotamente. Para alcançar acessibilidade limitada, você deve reduzir o conjunto de serviços acessíveis remotamente ao mínimo possível para um sistema operacional e, em seguida, habilitar a invocação remota para os serviços adicionais de que precisa.

A AEM Forms em serviços JEE sempre precisa de pelo menos acesso SOAP. Normalmente, esses serviços são necessários para o uso do Workbench, mas também incluem serviços que são chamados pelo aplicativo Web do Workspace.

Conclua este procedimento usando a página da Web Aplicativos e Serviços no Console de Administração:

1. Faça logon no Console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Services > Applications and Services > Preferences**.
1. Defina as Preferências para exibir até 200 serviços e endpoints na mesma página.
1. Clique em **Services** > **Applications and Services** > **Endpoint Management**.
1. Selecione **EJB** na lista **Provedor** e clique em **Filtro**.
1. Para desativar todos os pontos de extremidade EJB, marque a caixa de seleção ao lado de cada um na lista e clique em **Desativar**.
1. Clique em **Next** e repita a etapa anterior para todos os pontos de extremidade EJB. Certifique-se de que o EJB esteja listado na coluna Provedor antes de desativar os pontos de extremidade.
1. Selecione **SOAP** na lista **Provedor** e clique em **Filtro**.
1. Para remover pontos de extremidade SOAP, marque a caixa de seleção ao lado de cada um na lista e clique em **Remove**. Não remova os seguintes endpoints:

   * AuthenticationManagerService
   * DiretoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * GerenciadorDeFilasDeTarefas
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Clique em **Next** e repita a etapa anterior para pontos de extremidade SOAP que não estão na lista acima. Certifique-se de que o SOAP esteja listado na coluna Provedor antes de remover pontos de extremidade.

## Desativar o acesso anônimo não essencial aos serviços {#disabling-non-essential-anonymous-access-to-services}

Alguns serviços do servidor de formulários permitem a invocação não autenticada (anônima) para algumas operações. Isso significa que uma ou mais operações expostas pelo serviço podem ser chamadas como qualquer usuário autenticado ou como nenhum usuário autenticado.

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Services > Applications and Services > Service Management**.
1. Clique no nome do serviço que deseja desativar (por exemplo, AuthenticationManagerService).
1. Clique na **guia Segurança**, desmarque **Acesso Anônimo Permitido** e clique em **Salvar**.
1. Complete as etapas 3 e 4 para os seguintes serviços:

   * AuthenticationManagerService
   * EJB
   * E-mail
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoto
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * GerenciadorDeFilasDeTarefas
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Se você pretende expor qualquer um desses serviços para invocação remota, também deve considerar desativar o acesso anônimo para esses serviços. Caso contrário, qualquer chamador com acesso de rede a este serviço poderá invocar o serviço sem transmitir credenciais válidas.

   O acesso anônimo deve ser desativado para quaisquer serviços que não sejam necessários. Muitos serviços internos exigem que a autenticação anônima seja ativada porque eles precisam ser invocados por qualquer usuário no sistema sem ser pré-autorizado.

## Alteração do tempo limite global padrão {#changing-the-default-global-time-out}

Os usuários finais podem autenticar para o AEM Forms por meio do Workbench, de aplicativos da Web AEM Forms ou de aplicativos personalizados que chamam os serviços do servidor da AEM Forms. Uma configuração de tempo limite global é usada para especificar por quanto tempo esses usuários podem interagir com o AEM Forms (usando uma Asserção baseada em SAML) antes de serem forçados a reautenticar. A configuração padrão é de duas horas. Em um ambiente de produção, a quantidade de tempo precisa ser reduzida para o número mínimo de minutos aceitáveis.

### Minimizar o limite de tempo de reautenticação {#minimize-reauthentication-time-limit}

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Settings > User Management > Configuration > Import And Export Configuration Files**.
1. Clique em **Exportar** para produzir um arquivo config.xml com as configurações existentes do AEM Forms.
1. Abra o arquivo XML em um editor e localize a seguinte entrada:

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Altere o valor para qualquer número maior que 5 (em minutos) e salve o arquivo.
1. No console de administração, navegue até a página Importar e exportar arquivos de configuração .
1. Insira o caminho para o arquivo config.xml modificado ou clique em Procurar para navegar até ele.
1. Clique em **Importar** para carregar o arquivo config.xml modificado e clique em **OK**.

