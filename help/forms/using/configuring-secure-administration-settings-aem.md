---
title: Definição de configurações de administração segura para o AEM Forms no JEE
description: Saiba como administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin
exl-id: 40bc01b4-a59e-4420-81d6-2887857bddce
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Definição de configurações de administração segura para o AEM Forms no JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Saiba como administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção do AEM Forms no JEE.

Geralmente, os desenvolvedores não usam o ambiente de produção para criar e testar seus aplicativos. Portanto, você deve administrar contas de usuário e serviços que, embora necessários em um ambiente de desenvolvimento privado, não são necessários em um ambiente de produção.

Este artigo descreve métodos para reduzir a superfície de ataque geral por meio de opções de administração fornecidas pelo AEM Forms no JEE.

## Desativar o acesso remoto não essencial aos serviços {#disabling-non-essential-remote-access-to-services}

Depois que o AEM Forms no JEE é instalado e configurado, muitos serviços ficam disponíveis para invocação remota em SOAP e Enterprise JavaBeans™ (EJB). O termo remoto, neste caso, se refere a qualquer chamador que tenha acesso de rede às portas SOAP, EJB ou Action Message Format (AMF) do servidor de aplicativos.

Embora os serviços do AEM Forms no JEE exijam que credenciais válidas sejam passadas para um chamador autorizado, você deve permitir somente o acesso remoto aos serviços que precisam ser acessíveis remotamente. Para obter acessibilidade limitada, você deve reduzir o conjunto de serviços acessíveis remotamente ao mínimo possível para um sistema em funcionamento e, em seguida, habilitar a invocação remota para os serviços adicionais necessários.

Os serviços do AEM Forms no JEE sempre precisam pelo menos de acesso SOAP. Normalmente, esses serviços são necessários para uso pelo Workbench, mas também incluem serviços chamados pelo aplicativo web do Workspace.

Conclua este procedimento usando a página da Web Aplicativos e Serviços no Console de Administração:

1. Faça logon no Console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Serviços > Aplicativos e serviços > Preferências**.
1. Defina as Preferências para exibir até 200 serviços e pontos de extremidade na mesma página.
1. Clique em **Serviços** > **Aplicativos e serviços** > **Gerenciamento de Ponto de Extremidade**.
1. Selecionar **EJB** do **Provedor** e clique em **Filtro**.
1. Para desativar todos os endpoints de EJB, marque a caixa de seleção ao lado de cada um na lista e clique em **Desativar**.
1. Clique em **Próxima** e repita a etapa anterior para todos os pontos finais EJB. Certifique-se de que o EJB esteja listado na coluna Provedor antes de desativar os pontos finais.
1. Selecionar **SOAP** do **Provedor** e clique em **Filtro**.
1. Para remover pontos de extremidade SOAP, marque a caixa de seleção ao lado de cada um na lista e clique em **Remover**. Não remova os seguintes pontos de extremidade:

   * AuthenticationManagerService
   * DiretoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * ServiçoRepositório
   * ServiçoGerenciadorTarefa
   * GerenciadorDeFilaDeTarefas
   * ServiçoDeConsultaDoGerenciadorDeTarefas
   * LogonÚnicoWorkspace
   * ApplicationManager

1. Clique em **Próxima** e repita a etapa anterior para endpoints SOAP que não estão na lista acima. Certifique-se de que SOAP esteja listado na coluna Provedor antes de remover os pontos de extremidade.

## Desabilitação de acesso anônimo não essencial a serviços {#disabling-non-essential-anonymous-access-to-services}

Alguns serviços do Forms Server permitem a invocação não autenticada (anônima) para algumas operações. Isso significa que uma ou mais operações expostas pelo serviço podem ser chamadas como qualquer usuário autenticado ou como nenhum usuário autenticado.

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Serviços > Aplicativos e serviços > Gerenciamento de serviços**.
1. Clique no nome do serviço que deseja desativar (por exemplo, AuthenticationManagerService).
1. Clique em **Guia Segurança**, desmarcar **Acesso anônimo permitido** e clique em **Salvar**.
1. Complete as etapas 3 e 4 para os seguintes serviços:

   * AuthenticationManagerService
   * EJB
   * Email
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Comunicação remota
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormulárioAumentar
   * ServiçoGerenciadorTarefa
   * ConectorDoGerenciadorDeTarefas
   * ServiçoDeConsultaDoGerenciadorDeTarefas
   * GerenciadorDeFilaDeTarefas
   * GerenciadorDePontosDeExtremidadeDaTarefa
   * UserService
   * ServiçoDeModeloDePesquisaDoWorkspace
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Se você pretende expor qualquer um desses serviços para invocação remota, também deve considerar desativar o acesso anônimo para esses serviços. Caso contrário, qualquer chamador com acesso de rede a este serviço poderá invocá-lo sem passar credenciais válidas.

   O acesso anônimo deve ser desativado para qualquer serviço que não seja necessário. Muitos serviços internos exigem que a autenticação anônima seja habilitada, pois eles precisam ser invocados por qualquer usuário no sistema sem serem pré-autorizados.

## Alterar o tempo limite global padrão {#changing-the-default-global-time-out}

Os usuários finais podem se autenticar no AEM Forms por meio do Workbench, de aplicativos da Web do AEM Forms ou de aplicativos personalizados que chamam os serviços de servidor da AEM Forms. Uma configuração de tempo limite global é usada para especificar por quanto tempo esses usuários podem interagir com o AEM Forms (usando uma Asserção baseada em SAML) antes de serem forçados a reautenticar. A configuração padrão é de duas horas. Em um ambiente de produção, a quantidade de tempo precisa ser reduzida para o número mínimo de minutos aceitáveis.

### Minimizar limite de tempo de reautenticação {#minimize-reauthentication-time-limit}

1. Faça logon no console de administração digitando o seguinte URL em um navegador da Web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Clique em **Configurações > Gerenciamento De Usuários > Configuração > Importar E Exportar Arquivos De Configuração**.
1. Clique em **Exportar** para produzir um arquivo config.xml com as configurações existentes do AEM Forms.
1. Abra o arquivo XML em um editor e localize a seguinte entrada:

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. Altere o valor para qualquer número maior que 5 (em minutos) e salve o arquivo.
1. No console de administração, navegue até a página Importar e exportar arquivos de configuração.
1. Insira o caminho para o arquivo config.xml modificado ou clique em Procurar para navegar até ele.
1. Clique em **Importar** para fazer upload do arquivo config.xml modificado e clique em **OK**.
