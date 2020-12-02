---
title: Importar e gerenciar arquivos
seo-title: Importar e gerenciar arquivos
description: Saiba como importar e gerenciar arquivos.
seo-description: Saiba como importar e gerenciar arquivos.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 0%

---


# Importar e gerenciar arquivos {#import-and-manage-archives}

Use a guia arquivamentos para importar e gerenciar LCAs criados no Workbench.

## Importar um arquivo {#import-an-archive}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia arquivamentos.
1. Clique em Importar.
1. Clique em Procurar para localizar o arquivo a ser importado e clique em Pré-visualização.
1. Revise a lista de recursos e objetos que serão instalados com o arquivo. Certifique-se de que não haja conflitos com recursos, objetos e configurações de serviço existentes porque nenhum recurso de desfazer está disponível.

   Se você optar por importar as configurações de serviço, os formulários AEM importam todos os arquivos de configuração do processo (pontos de extremidade, perfis de segurança e parâmetros de configuração do serviço) usados pelos processos no LCA.

1. Clique em Importar.
1. Revise os resultados da importação e clique em Ignorar configuração para concluir o processo de importação ou clique em Configurar para configurar o arquivo.

   >[!NOTE]
   >
   >Se você clicar em Ignorar configuração, poderá configurar o arquivo mais tarde.

1. Se você clicar em Configurar, a página Configurar pontos finais será exibida, onde você poderá fazer as alterações necessárias:

   * Para renomear um terminal ou editar sua descrição, clique nele.
   * Para adicionar um terminal do Gerenciador de Tarefas, clique em Adicionar Gerenciador de Tarefas. Para obter detalhes sobre as configurações do Gerenciador de Tarefas, consulte [Definição de pontos finais do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um terminal de Pasta assistida, clique em Adicionar pasta assistida. Para obter detalhes sobre as configurações de Pasta assistida, consulte [Configurações de ponto de extremidade de pasta assistida](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de E-mail, consulte [Configurações de ponto de extremidade de e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto de extremidade EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um terminal SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o terminal.
   * Para adicionar um terminal Remoto, clique em Adicionar Remota. Para obter detalhes sobre as configurações de Remota, consulte [Configurações de ponto de extremidade remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um ponto de extremidade REST, clique em Adicionar REST e especifique um nome e uma descrição para o ponto de extremidade. Observe o URL de invocação REST exibido na página Adicionar ponto de extremidade REST.
   * Para remover um terminal, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, uma página Configurar parâmetros será exibida, onde você configura os parâmetros de serviço e clica em Avançar.
1. Na página Configurar Perfil de Segurança, faça as alterações necessárias:

   * **Exigir que os chamadores autenticem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

      Se *Os chamadores forem atualmente necessários para autenticar* for exibido, o chamador do serviço deve ser autenticado e o principal do usuário para esse chamador deve ser autorizado a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadas não autenticadas.

      Se *Chamadores não forem necessários para autenticar* for exibido, o chamador do serviço não precisará ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização. Para exigir autenticação, clique em Exigir que os chamadores autenticem.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço depois de ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha uma das seguintes opções:

      **Não especificado:** o comportamento padrão é usado.

      **Invocador:** Usa a mesma identidade do usuário que chamou o serviço.

      **Sistema:** executa o serviço com privilégios totais. Essa é a configuração padrão para processos duradouros.

      **Usuário nomeado:** permite que você execute o serviço como um usuário específico. Essa é a configuração padrão para processos de duração curta. Ao selecionar essa opção, clique em Selecionar usuário para exibir a página Selecionar principal, na qual você pode pesquisar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Avançar e selecione as permissões que deseja atribuir a este principal:

      **INVOKE_PERM:** Para chamar todas as operações no serviço

      **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço

      **SUPERVISOR_PERM:** Para visualização dos dados da instância do processo para um serviço criado a partir de um processo

      **START_STOP_PERM:** Para start e parar um serviço

      **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar pontos de extremidade de um serviço

      **CREATE_VERSION_PERM:** Para criar uma nova versão do serviço

      **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

      **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

      **READ_PERM:** Para visualização do serviço

      Clique em Concluído para adicionar o principal ao perfil de segurança.

1. Clique em Concluído para concluir a configuração.

## Configure os formulários AEM que fazem parte de um arquivo de arquivamento {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia arquivamentos.
1. Na página Gerenciamento de arquivo, selecione o arquivo de arquivo a ser configurado.
1. Na página Arquivo de Visualizações, selecione o recurso de arquivamento realçado.
1. Configure o arquivo de arquivamento do processo importado.

## Use o assistente de configuração para configurar os formulários AEM que fazem parte de um arquivo de arquivamento {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de aplicativos e clique na guia arquivamentos.
1. Clique em Configurar ao lado do arquivo de arquivamento para configurar.
1. A página Configurar pontos de extremidade é exibida, onde você pode fazer as alterações necessárias:

   * Para renomear um terminal ou editar sua descrição, clique nele.
   * Para adicionar um terminal do Gerenciador de Tarefas, clique em Adicionar Gerenciador de Tarefas. Para obter detalhes sobre as configurações do Gerenciador de Tarefas, consulte [Definição de pontos finais do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um terminal de Pasta assistida, clique em Adicionar pasta assistida. Para obter detalhes sobre as configurações de Pasta assistida, consulte [Configurações de ponto de extremidade de pasta assistida](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de E-mail, consulte [Configurações de ponto de extremidade de e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto de extremidade EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um terminal SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o terminal.
   * Para adicionar um terminal Remoto, clique em Adicionar Remota. Para obter detalhes sobre as configurações de Remota, consulte [Configurações de ponto de extremidade remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um ponto de extremidade REST, clique em Adicionar REST e especifique um nome e uma descrição para o ponto de extremidade. Observe o URL de invocação REST exibido na página Adicionar ponto de extremidade REST.
   * Para remover um terminal, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, uma página Configurar parâmetros será exibida, onde você configura os parâmetros de serviço e clica em Avançar.
1. Na página Configurar Perfil de Segurança, é possível fazer as alterações necessárias:

   * **Exigir que os chamadores autenticem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

      Se *Os chamadores forem atualmente necessários para autenticar* for exibido, o chamador do serviço deve ser autenticado e o principal do usuário para esse chamador deve ser autorizado a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadas não autenticadas.

      Se *Chamadores não forem necessários para autenticar* for exibido, o chamador do serviço pode ou não ser autenticado. A invocação do serviço sempre terá êxito porque não há verificação de autorização. Para exigir autenticação, clique em Exigir que os chamadores autenticem.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço depois de ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha uma das seguintes opções:

      **Não especificado:** o comportamento padrão é usado.

      **Invocador:** Usa a mesma identidade do usuário que chamou o serviço.

      **Sistema:** executa o serviço com privilégios totais. Essa é a configuração padrão para processos duradouros.

      **Usuário nomeado:** permite que você execute o serviço como um usuário específico. Essa é a configuração padrão para processos de duração curta. Ao selecionar essa opção, clique em Selecionar usuário para exibir a página Selecionar principal, na qual você pode pesquisar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Avançar e selecione as permissões que deseja atribuir a este principal:

      **INVOKE_PERM:** Para chamar todas as operações no serviço

      **MODIFY_CONFIG_PERM:** Para modificar a configuração de um serviço

      **SUPERVISOR_PERM:** Para visualização dos dados da instância do processo para um serviço criado a partir de um processo

      **START_STOP_PERM:** Para start e parar um serviço

      **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar pontos de extremidade de um serviço

      **CREATE_VERSION_PERM:** Para criar uma nova versão do serviço

      **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

      **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

      **READ_PERM:** Para visualização do serviço

      Clique em Concluído para adicionar o principal ao perfil de segurança.

## Remover um arquivo {#remove-an-archive}

>[!NOTE]
>
>Para remover um arquivo que contenha ativos armazenados em um repositório de terceiros (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), você também deve excluir os arquivos de ativos do repositório usando o Workbench.

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de arquivamento.
1. Na página Gerenciamento de arquivo, marque a caixa de seleção do arquivo a ser removido e clique em Remover.

