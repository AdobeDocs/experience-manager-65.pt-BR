---
title: Configuração das configurações de administração segura para formulários AEM no JEE
seo-title: Configuração das configurações de administração segura para formulários AEM no JEE
description: Saiba como administrar contas de usuário e serviços que, embora obrigatórios em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.
seo-description: Saiba como administrar contas de usuário e serviços que, embora obrigatórios em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.
uuid: 04e45d06-f57d-406c-8228-15f483199430
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: d211d8b0-e75f-49c3-808d-5d0e26ad3a6b
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuração das configurações de administração segura para formulários AEM no JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Saiba como administrar contas de usuário e serviços que, embora obrigatórios em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.

Geralmente, os desenvolvedores não usam o ambiente de produção para criar e testar seus aplicativos. Portanto, você deve administrar contas de usuário e serviços que, embora obrigatórios em um ambiente de desenvolvimento privado, não são exigidos em um ambiente de produção.

Este artigo descreve os métodos para reduzir a superfície geral do ataque por meio das opções de administração fornecidas pelo AEM Forms no JEE.

## Desativar acesso remoto não essencial a serviços {#disabling-non-essential-remote-access-to-services}

Depois que o AEM Forms no JEE é instalado e configurado, muitos serviços estão disponíveis para invocação remota no SOAP e Enterprise JavaBeans™ (EJB). O termo remoto, neste caso, refere-se a qualquer chamador que tenha acesso de rede às portas SOAP, EJB ou AMF (Action Message Format) para o servidor de aplicativos.

Embora os formulários AEM em serviços JEE exijam credenciais válidas para um chamador autorizado, você deve permitir somente acesso remoto aos serviços que precisam ser acessados remotamente. Para obter acessibilidade limitada, você deve reduzir o conjunto de serviços acessíveis remotamente ao mínimo possível para um sistema operacional e, em seguida, habilitar a invocação remota para os serviços adicionais de que precisa.

O AEM Forms em serviços JEE sempre precisa de pelo menos acesso SOAP. Normalmente, esses serviços são necessários para uso pelo Workbench, mas também incluem serviços que são chamados pelo aplicativo da Web do Workspace.

Conclua este procedimento usando a página da Web Aplicativos e Serviços no Console de administração:

1. Faça logon no Console de administração digitando o seguinte URL em um navegador da Web:

   ```as3
            https://[host name]:'port'/adminui
   ```

1. Clique em **Serviços > Aplicativos e serviços > Preferências**.
1. Defina Preferências para visualização de até 200 serviços e pontos finais na mesma página.
1. Clique em **Serviços** > **Aplicativos e serviços** > Gerenciamento **de** ponto de extremidade.
1. Selecione **EJB** na lista **Provedor** e clique em **Filtro**.
1. Para desativar todos os pontos de extremidade EJB, marque a caixa de seleção ao lado de cada um na lista e clique em **Desativar**.
1. Clique em **Avançar** e repita a etapa anterior para todos os pontos finais EJB. Certifique-se de que o EJB esteja listado na coluna Provedor antes de desativar os pontos de extremidade.
1. Selecione **SOAP** na lista **Provedor** e clique em **Filtro**.
1. Para remover pontos de extremidade SOAP, marque a caixa de seleção ao lado de cada um na lista e clique em **Remover**. Não remova os seguintes pontos finais:

   * AuthenticationManagerService
   * DiretoryManagerService
   * JobManager
   * evento_management_service
   * evento_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Clique em **Avançar** e repita a etapa anterior para pontos de extremidade SOAP que não estejam na lista acima. Certifique-se de que SOAP esteja listado na coluna Provedor antes de remover pontos de extremidade.

## Desativar o acesso anônimo não essencial aos serviços {#disabling-non-essential-anonymous-access-to-services}

Alguns serviços de servidor de formulários permitem invocação não autenticada (anônima) para algumas operações. Isso significa que uma ou mais operações expostas pelo serviço podem ser chamadas como qualquer usuário autenticado ou como nenhum usuário autenticado.

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```as3
            https://[host name]:'port'/adminui
   ```

1. Clique em **Serviços > Aplicativos e serviços > Gerenciamento** de serviços.
1. Clique no nome do serviço que deseja desativar (por exemplo, AuthenticationManagerService).
1. Clique na guia **** Segurança, desmarque Acesso **anônimo permitido** e clique em **Salvar**.
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
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService
   Se você pretende expor qualquer um desses serviços para invocação remota, também deve considerar a desativação do acesso anônimo para esses serviços. Caso contrário, qualquer chamador com acesso à rede para este serviço poderá invocar o serviço sem transmitir credenciais válidas.

   O acesso anônimo deve ser desabilitado para quaisquer serviços que não sejam necessários. Muitos serviços internos exigem autenticação anônima para serem ativados, pois eles precisam ser chamados por qualquer usuário potencial no sistema sem serem pré-autorizados.

## Alteração do tempo limite global padrão {#changing-the-default-global-time-out}

Os usuários finais podem autenticar no AEM Forms por meio do Workbench, de aplicativos da Web do AEM Forms ou de aplicativos personalizados que chamam os serviços do servidor do AEM Forms. Uma configuração de tempo limite global é usada para especificar por quanto tempo esses usuários podem interagir com formulários AEM (usando uma asserção baseada em SAML) antes de serem forçados a reautenticar. A configuração padrão é de duas horas. Em um ambiente de produção, a quantidade de tempo precisa ser reduzida para o número mínimo de minutos aceitáveis.

### Minimizar o limite de tempo de reautenticação {#minimize-reauthentication-time-limit}

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```as3
            https://[host name]:'port'/adminui
   ```

1. Clique em **Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos** de configuração.
1. Clique em **Exportar** para produzir um arquivo config.xml com as configurações existentes do AEM Forms.
1. Abra o arquivo XML em um editor e localize a seguinte entrada:

   `<entry key=”assertionValidityInMinutes” value=”120”/>`

1. Altere o valor para qualquer número maior que 5 (em minutos) e salve o arquivo.
1. No console de administração, navegue até a página Importar e exportar arquivos de configuração.
1. Digite o caminho para o arquivo config.xml modificado ou clique em Procurar para navegar até ele.
1. Clique em **Importar** para carregar o arquivo config.xml modificado e clique em **OK**.

