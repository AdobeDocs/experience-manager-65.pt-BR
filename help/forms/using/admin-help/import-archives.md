---
title: Importar e gerenciar arquivos
description: Saiba como importar e gerenciar arquivos. O arquivo importa e gerencia LCAs criados no workbench. É possível importar, configurar, usar e excluir um arquivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Importar e gerenciar arquivos {#import-and-manage-archives}

Use a guia arquivos para importar e gerenciar LCAs criadas no workbench.

## Importar um arquivo {#import-an-archive}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia Arquivos.
1. Clique em Importar.
1. Clique em Procurar para localizar o arquivo a ser importado e, em seguida, clique em Visualizar.
1. Revise a lista de recursos e objetos que serão instalados com o arquivamento. Verifique se não há conflitos com recursos, objetos e configurações de serviço existentes porque nenhum recurso desfazer está disponível.

   Se você optar por importar as configurações de serviço, os formulários AEM importarão todos os arquivos de configuração de processo (endpoints, perfis de segurança e parâmetros de configuração de serviço) usados pelos processos no LCA.

1. Clique em Importar.
1. Revise os resultados da importação e clique em Ignorar configuração para concluir o processo de importação ou clique em Configurar para configurar o arquivo.

   >[!NOTE]
   >
   >Se você clicar em Ignorar configuração, poderá configurar o arquivo posteriormente.

1. Se você clicar em Configurar, a página Configurar Pontos de Extremidade será exibida, onde você poderá fazer as alterações necessárias:

   * Para renomear um endpoint ou editar sua descrição, clique nele.
   * Para adicionar um ponto de extremidade do Gerenciador de tarefas, clique em Adicionar Gerenciador de tarefas. Para obter detalhes sobre as configurações do Gerenciador de Tarefas, consulte [Configurando pontos de extremidade do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um endpoint de Pasta monitorada, clique em Adicionar WatchedFolder. Para obter detalhes sobre as configurações da Pasta monitorada, consulte [configurações do ponto de extremidade da pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de Email, consulte [Configurações de ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto final EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto final.
   * Para adicionar um endpoint de SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o endpoint.
   * Para adicionar um ponto de extremidade Remoting, clique em Adicionar Remoting. Para obter detalhes sobre as configurações de Comunicação Remota, consulte [Configurações de ponto de extremidade de Comunicação Remota](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um endpoint REST, clique em Add REST e especifique um nome e uma descrição para o endpoint. Observe o URL de invocação REST exibido na página Adicionar Ponto de Extremidade REST.
   * Para remover um endpoint, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, será exibida uma página Configurar Parâmetros, onde você configura os parâmetros de serviço e clica em Próximo.
1. Na página Configurar perfil de segurança, faça as alterações necessárias:

   * **Exigir que chamadores se autentiquem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

     Se *Chamadores são necessários para autenticar* no momento, o chamador do serviço deve ser autenticado e a entidade de usuário desse chamador deve ser autorizada a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadores não autenticados.

     Se *Chamadores não são necessários para autenticar* for exibido, o chamador do serviço não precisa ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização. Para exigir autenticação, clique em Exigir autenticação dos chamadores.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço depois de ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha entre as seguintes opções:

     **Não especificado:** O comportamento padrão é usado.

     **Chamador:** Usa a mesma identidade do usuário que invocou o serviço.

     **Sistema:** Executa o serviço com privilégios totais. Essa é a configuração padrão para processos de longa duração.

     **Usuário Nomeado:** Permite que você execute o serviço como um usuário específico. Essa é a configuração padrão para processos de vida curta. Ao selecionar essa opção, clique em Selecionar Usuário para exibir a página Selecionar Principal, onde você pode pesquisar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Próximo e selecione as permissões que deseja atribuir a este principal:

     **INVOKE_PERM:** Para invocar todas as operações no serviço

     **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço

     **SUPERVISOR_PERM:** Para exibir dados de instância de processo para um serviço criado a partir de um processo

     **START_STOP_PERM:** Para iniciar e parar um serviço

     **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar pontos de extremidade para um serviço

     **CREATE_VERSION_PERM:** Para criar uma versão do serviço

     **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

     **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

     **READ_PERM:** Para exibir o serviço

     Clique em Concluído para adicionar o principal ao perfil de segurança.

1. Clique em Finished para concluir a configuração.

## Configurar os formulários AEM que fazem parte de um arquivo {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia Arquivos.
1. Na página Gerenciamento de Arquivamento, selecione o arquivo de arquivamento a ser configurado.
1. Na página Exibir arquivo, selecione o recurso de arquivo destacado.
1. Configure o arquivo de arquivamento do processo importado.

## Use o assistente de configuração para configurar os formulários AEM que fazem parte de um arquivo {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia Arquivos.
1. Clique em Configurar ao lado do arquivo a ser configurado.
1. A página Configurar Pontos de Extremidade é exibida, onde você pode fazer as alterações necessárias:

   * Para renomear um endpoint ou editar sua descrição, clique nele.
   * Para adicionar um ponto de extremidade do Gerenciador de tarefas, clique em Adicionar Gerenciador de tarefas. Para obter detalhes sobre as configurações do Gerenciador de Tarefas, consulte [Configurando pontos de extremidade do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um endpoint de Pasta monitorada, clique em Adicionar WatchedFolder. Para obter detalhes sobre as configurações da Pasta monitorada, consulte [configurações do ponto de extremidade da pasta monitorada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de Email, consulte [Configurações de ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto final EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto final.
   * Para adicionar um endpoint de SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o endpoint.
   * Para adicionar um ponto de extremidade Remoting, clique em Adicionar Remoting. Para obter detalhes sobre as configurações de Comunicação Remota, consulte [Configurações de ponto de extremidade de Comunicação Remota](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um endpoint REST, clique em Add REST e especifique um nome e uma descrição para o endpoint. Observe o URL de invocação REST exibido na página Adicionar Ponto de Extremidade REST.
   * Para remover um endpoint, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, será exibida uma página Configurar Parâmetros, onde você configura os parâmetros de serviço e clica em Próximo.
1. Na página Configurar perfil de segurança, você pode fazer as alterações necessárias:

   * **Exigir que chamadores se autentiquem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

     Se *Chamadores são necessários para autenticar* no momento, o chamador do serviço deve ser autenticado e a entidade de usuário desse chamador deve ser autorizada a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadores não autenticados.

     Se *Chamadores não são necessários para autenticar* for exibido, o chamador do serviço pode ou não ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização. Para exigir autenticação, clique em Exigir autenticação dos chamadores.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço depois de ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha entre as seguintes opções:

     **Não especificado:** O comportamento padrão é usado.

     **Chamador:** Usa a mesma identidade do usuário que invocou o serviço.

     **Sistema:** Executa o serviço com privilégios totais. Essa é a configuração padrão para processos de longa duração.

     **Usuário Nomeado:** Permite que você execute o serviço como um usuário específico. Essa é a configuração padrão para processos de vida curta. Ao selecionar essa opção, clique em Selecionar Usuário para exibir a página Selecionar Principal, onde você pode pesquisar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Próximo e selecione as permissões que deseja atribuir a este principal:

     **INVOKE_PERM:** Para invocar todas as operações no serviço

     **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço

     **SUPERVISOR_PERM:** Para exibir dados de instância de processo para um serviço criado a partir de um processo

     **START_STOP_PERM:** Para iniciar e parar um serviço

     **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar pontos de extremidade para um serviço

     **CREATE_VERSION_PERM:** Para criar uma versão do serviço

     **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

     **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

     **READ_PERM:** Para exibir o serviço

     Clique em Concluído para adicionar o principal ao perfil de segurança.

## Remover um arquivo {#remove-an-archive}

>[!NOTE]
>
>Para remover um arquivo contendo ativos armazenados em um repositório de terceiros (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), você também deve excluir os arquivos de ativos do repositório usando o Workbench.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de arquivo.
1. Na página Gerenciamento de Arquivamento, marque a caixa de seleção do arquivamento a ser removido e clique em Remover.
