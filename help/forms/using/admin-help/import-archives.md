---
title: Importar e gerenciar arquivos
seo-title: Import and manage archives
description: Saiba como importar e gerenciar arquivos.
seo-description: Learn how to import and manage archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Importar e gerenciar arquivos {#import-and-manage-archives}

Use a guia arquivamentos para importar e gerenciar LCAs que foram criadas no workbench.

## Importar um arquivo {#import-an-archive}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos e clique na guia arquivamentos.
1. Clique em Importar.
1. Clique em Procurar para localizar o arquivo a ser importado e clique em Visualizar.
1. Revise a lista de recursos e objetos que serão instalados com o arquivo. Verifique se não há conflitos com recursos, objetos e configurações de serviço existentes porque nenhum recurso de desfazer está disponível.

   Se você optar por importar as configurações do serviço, os formulários AEM importam todos os arquivos de configuração do processo (endpoints, perfis de segurança e parâmetros de configuração do serviço) usados pelos processos no LCA.

1. Clique em Importar.
1. Revise os resultados da importação e clique em Ignorar configuração para concluir o processo de importação ou clique em Configurar para configurar o arquivo.

   >[!NOTE]
   >
   >Se você clicar em Ignorar configuração, poderá configurar o arquivo mais tarde.

1. Se você clicar em Configurar, a página Configurar endpoints será exibida, onde é possível fazer as alterações necessárias:

   * Para renomear um endpoint ou editar sua descrição, clique nele.
   * Para adicionar um ponto de extremidade do Gerenciador de Tarefas, clique em Adicionar Gerenciador de Tarefas. Para obter detalhes sobre as configurações do Gerenciador de tarefas, consulte [Configurando endpoints do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um endpoint de Pasta assistida, clique em Adicionar pasta assistida. Para obter detalhes sobre as configurações da Pasta assistida, consulte [Configurações de ponto de extremidade de pasta assistida](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de Email, consulte [Configurações do ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto de extremidade EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um ponto de extremidade SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um terminal Remoting, clique em Add Remoting. Para obter detalhes sobre as configurações de Remoção, consulte [Remoção das configurações de ponto de extremidade](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um ponto de extremidade REST, clique em Adicionar REST e especifique um nome e uma descrição para o ponto de extremidade. Observe o URL de invocação REST exibido na página Adicionar Ponto de Extremidade REST .
   * Para remover um ponto de extremidade, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, uma página Configurar parâmetros será exibida, onde você configurará os parâmetros de serviço e clicará em Avançar.
1. Na página Configurar perfil de segurança, faça as alterações necessárias:

   * **Exigir que os chamadores autenticem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

      If *Atualmente, os chamadores são necessários para autenticar* for exibido, o chamador do serviço deve ser autenticado e o responsável principal do usuário desse chamador deve ser autorizado a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadas não autenticadas.

      If *Os chamadores não são necessários para autenticar* for exibido, o chamador do serviço não precisará ser autenticado. A invocação do serviço sempre terá êxito porque não existe uma verificação de autorização. Para exigir autenticação, clique em Exigir que os chamadores sejam autenticados.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço após ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha entre as seguintes opções:

      **Não especificado:** O comportamento padrão é usado.

      **Invocador:** Usa a mesma identidade do usuário que invocou o serviço.

      **Sistema:** Executa o serviço com privilégios totais. Essa é a configuração padrão para processos de longa duração.

      **Usuário nomeado:** Permite executar o serviço como um usuário específico. Essa é a configuração padrão para processos de duração curta. Ao selecionar esta opção, clique em Selecionar Usuário para exibir a página Selecionar Principal, onde você pode procurar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar Principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Next e selecione as permissões que deseja atribuir a este principal:

      **INVOKE_PERM:** Para invocar todas as operações no serviço

      **MODIFY_CONFIG_PERM:** Modificação da configuração de um serviço

      **SUPERVISOR_PERM:** Para exibir dados da instância do processo para um serviço criado de um processo

      **START_STOP_PERM:** Para iniciar e parar um serviço

      **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar endpoints de um serviço

      **CREATE_VERSION_PERM:** Para criar uma nova versão do serviço

      **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

      **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

      **READ_PERM:** Para exibir o serviço

      Clique em Finished para adicionar o principal ao perfil de segurança.

1. Clique em Finished para concluir a configuração.

## Configurar os formulários AEM que fazem parte de um arquivo de arquivamento {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos e clique na guia arquivamentos.
1. Na página Gerenciamento de arquivo , selecione o arquivo de arquivo a ser configurado.
1. Na página Exibir arquivo , selecione o recurso de arquivo destacado.
1. Configure o arquivo de arquivamento de processos importado.

## Use o assistente de configuração para configurar os formulários de AEM que fazem parte de um arquivo de arquivamento {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Aplicativos e clique na guia arquivamentos.
1. Clique em Configurar ao lado do arquivo de arquivamento para configurar.
1. A página Configurar pontos de extremidade é exibida, onde é possível fazer as alterações necessárias:

   * Para renomear um endpoint ou editar sua descrição, clique nele.
   * Para adicionar um ponto de extremidade do Gerenciador de Tarefas, clique em Adicionar Gerenciador de Tarefas. Para obter detalhes sobre as configurações do Gerenciador de tarefas, consulte [Configurando endpoints do Gerenciador de Tarefas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * Para adicionar um endpoint de Pasta assistida, clique em Adicionar pasta assistida. Para obter detalhes sobre as configurações da Pasta assistida, consulte [Configurações de ponto de extremidade de pasta assistida](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * Para adicionar um terminal de email, clique em Adicionar email. Para obter detalhes sobre as configurações de Email, consulte [Configurações do ponto de extremidade de email](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * Para adicionar um ponto de extremidade EJB, clique em Adicionar EJB e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um ponto de extremidade SOAP, clique em Adicionar SOAP e especifique um nome e uma descrição para o ponto de extremidade.
   * Para adicionar um terminal Remoting, clique em Add Remoting. Para obter detalhes sobre as configurações de Remoção, consulte [Remoção das configurações de ponto de extremidade](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * Para adicionar um ponto de extremidade REST, clique em Adicionar REST e especifique um nome e uma descrição para o ponto de extremidade. Observe o URL de invocação REST exibido na página Adicionar Ponto de Extremidade REST .
   * Para remover um ponto de extremidade, marque a caixa de seleção ao lado dele e clique em Remover.

1. Clique em Avançar.
1. Se um processo ou serviço no LCA tiver parâmetros de configuração, uma página Configurar parâmetros será exibida, onde você configurará os parâmetros de serviço e clicará em Avançar.
1. Na página Configurar perfil de segurança, é possível fazer as alterações necessárias:

   * **Exigir que os chamadores autenticem:** Esta configuração indica se o serviço pode ser chamado com ou sem credenciais.

      If *Atualmente, os chamadores são necessários para autenticar* for exibido, o chamador do serviço deve ser autenticado e o responsável principal do usuário desse chamador deve ser autorizado a invocar o serviço; caso contrário, a tentativa de invocação será recusada. Para remover a necessidade de autenticação, clique em Permitir chamadas não autenticadas.

      If *Os chamadores não são necessários para autenticar* for exibido, o chamador do serviço pode ou não ser autenticado. A invocação do serviço sempre terá êxito porque não existe uma verificação de autorização. Para exigir autenticação, clique em Exigir que os chamadores sejam autenticados.

   * **Executar como:** Especifica a identidade de tempo de execução usada por um serviço após ter sido chamado. Para alterar essa opção, clique em Alterar. Escolha entre as seguintes opções:

      **Não especificado:** O comportamento padrão é usado.

      **Invocador:** Usa a mesma identidade do usuário que invocou o serviço.

      **Sistema:** Executa o serviço com privilégios totais. Essa é a configuração padrão para processos de longa duração.

      **Usuário nomeado:** Permite executar o serviço como um usuário específico. Essa é a configuração padrão para processos de duração curta. Ao selecionar esta opção, clique em Selecionar Usuário para exibir a página Selecionar Principal, onde você pode procurar e selecionar o usuário.

   * Para adicionar um principal ao perfil de segurança, clique em Adicionar Principal e selecione o usuário ou grupo a ser adicionado como principal. Clique em Next e selecione as permissões que deseja atribuir a este principal:

      **INVOKE_PERM:** Para invocar todas as operações no serviço

      **MODIFY_CONFIG_PERM:** Modificação da configuração de um serviço

      **SUPERVISOR_PERM:** Para exibir dados da instância do processo para um serviço criado de um processo

      **START_STOP_PERM:** Para iniciar e parar um serviço

      **ADD_REMOVE_ENDPOINTS_PERM:** Para adicionar, remover e modificar endpoints de um serviço

      **CREATE_VERSION_PERM:** Para criar uma nova versão do serviço

      **DELETE_VERSION_PERM:** Para excluir uma versão do serviço

      **MODIFY_VERSION_PERM:** Para modificar uma versão do serviço

      **READ_PERM:** Para exibir o serviço

      Clique em Finished para adicionar o principal ao perfil de segurança.

## Remover um arquivo {#remove-an-archive}

>[!NOTE]
>
>Para remover um arquivo contendo ativos armazenados em um repositório de terceiros (EMC Documentum Content Server, IBM FileNet Content Manager ou IBM Content Manager), você também deve excluir os arquivos de ativos do repositório usando o Workbench.

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Arquivo.
1. Na página Gerenciamento de arquivo , marque a caixa de seleção do arquivo a ser removido e clique em Remover.
