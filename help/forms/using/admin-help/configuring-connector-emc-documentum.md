---
title: Configurando o Connector para EMC Documentum
seo-title: Configurando o Connector para EMC Documentum
description: Saiba como configurar o Connector for EMC Documentum para permitir a comunicação entre formulários AEM e EMC Documentum.
seo-description: Saiba como configurar o Connector for EMC Documentum para permitir a comunicação entre formulários AEM e EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurando o Connector para EMC Documentum {#configuring-connector-for-emc-documentum}

O Connector for EMC Documentum permite a comunicação entre formulários AEM e EMC Documentum. Para obter informações adicionais de plano de fundo, consulte &quot;Conectores para ECM&quot; na Referência [de](https://www.adobe.com/go/learn_aemforms_services_63)serviços.

A configuração do Connector for EMC Documentum envolve a configuração da conexão do servidor e das credenciais do repositório.

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Na versão atual, os ativos são armazenados no repositório nativo de formulários do AEM e os serviços do Provedor de repositório foram descontinuados. A migração de ativos de um repositório ECM para o repositório de formulários AEM é feita quando você faz uma atualização para formulários AEM. Para obter mais informações, consulte o Guia de atualização de formulários do AEM para seu servidor de aplicativos.

## Configuração da conexão com o servidor {#configuring-the-server-connection}

Este tópico descreve as tarefas do Connector for EMC Documentum que você pode executar na página Configurações.

>[!NOTE]
>
>Se você estiver configurando todas as configurações simultaneamente, basta clicar em Salvar uma vez.

### Configurar o servidor {#configure-the-server}

É necessário configurar as informações do servidor do Agente de Conexão. Essas informações são necessárias para conectar-se aos repositórios de conteúdo da Documentum e iniciar o Connector for EMC Documentum.

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações de configuração do Documentum, digite o nome do host ou endereço IP e o número da porta do agente de conexão. O número da porta deve ser um número inteiro positivo (por exemplo, 1489).
1. Clique em Salvar.

### Configurar credenciais do principal {#configure-principal-credentials}

Ao configurar as credenciais principais, o nome do repositório que você fornecer dependerá de um nome de repositório explícito ser fornecido durante o logon.

Se você digitar um nome de usuário ou senha incorretos, você obterá os seguintes resultados, dependendo se o serviço está sendo executado no momento:

* Se o serviço EMC Documentum Repository Provider e o serviço EMC Documentum Content Repository Connector forem interrompidos, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço EMC Documentum Repository Provider ou o serviço EMC Documentum Content Repository Connector for iniciado, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credenciais imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações sobre Credenciais Principais da Documentum, digite o nome de usuário e a senha de um usuário com privilégios de superadministrador.
1. Se um nome de repositório explícito não for fornecido durante o logon, digite o nome do repositório ao qual as credenciais estão associadas.
1. Clique em Salvar.

### Alterar o provedor de serviços de repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviços de repositório usar com o Documentum. As chamadas de serviço do repositório são delegadas ao provedor configurado. As opções disponíveis são as seguintes:

**** Nome atual do provedor de serviços do repositório: O nome do provedor de serviços de repositório atual

**** Provedor de repositório do ECM Documentum: Torna o provedor do repositório Documentum o provedor do repositório. Esta opção foi substituída

**** provedor de repositório: Torna o provedor de repositório nativo o provedor do repositório

***Observação **: Para selecionar um provedor de serviços de repositório diferente daqueles listados, configure RepositoryService em Aplicativos e Serviços > Gerenciamento de serviços.<!-- Fix broken link (See Managing Services) -->*

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações do Provedor de Serviços do Repositório, selecione o provedor de serviços do repositório alternativo.
1. Clique em Salvar.

## Configurando credenciais do repositório {#configuring-repository-credentials}

As informações de credenciais do Documentum são usadas no contexto do sistema de formulários do AEM. As credenciais do repositório são específicas a repositórios específicos no Documentum. Você pode fornecer credenciais para qualquer número de repositórios; no entanto, você pode especificar apenas um conjunto de credenciais por repositório.

### Adicionar uma credencial de repositório {#add-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações de credenciais do repositório.
1. Clique em Adicionar. A página Informações de credenciais do sistema Documentum é exibida.
1. Insira um nome para o repositório.
1. Insira um nome de usuário e senha.
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiver em execução, as informações de credenciais serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

### Remover uma credencial do repositório {#remove-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Marque a caixa de seleção ao lado do repositório do qual deseja remover credenciais e clique em Remover. As credenciais do repositório selecionado são removidas do banco de dados.

### Alterar o nome de usuário e a senha de uma credencial de repositório {#change-the-user-name-and-password-for-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Clique no nome do repositório para editar credenciais.
1. Altere o nome de usuário ou a senha do repositório, ou ambos. (O nome do repositório é somente leitura.)
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiver em execução, as informações de credenciais serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

## Ativar a solicitação para compartilhamento de filas de tarefas do Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Algumas etapas manuais são necessárias para garantir que o recurso Solicitar compartilhamento da fila de tarefas no Workspace funcione corretamente com o Connector for EMC Documentum.

1. Depois que os formulários AEM forem implantados e o Workbench for instalado, faça logon no Workbench e abra a exibição Recursos. Você determinará onde o arquivo QueueSharing.swf está localizado nesta exibição.
1. Arraste o arquivo QueueSharing.swf da Exibição de recursos para a área de trabalho do Windows ou um local equivalente, dependendo do sistema operacional.
1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Em Informações do provedor de serviços de repositório, altere o provedor de repositório configurado para Provedor de repositório do EMC Documentum.
1. Inicie o Workbench e copie o arquivo QueueSharing.swf do local em que você o copiou originalmente (por exemplo, a área de trabalho do Windows ou outro local) em um diretório existente no repositório do EMC Documentum.
1. Na exibição Processos do Workbench, abra o processo Compartilhamento de Filas.
1. Na exibição Variáveis, abra as propriedades da variável &quot;theForm&quot; e altere o URI para corresponder ao caminho onde você colocou o arquivo QueueSharing.swf na etapa 5.
1. Salve o processo.
1. Migre o processo para o ambiente de produção de acordo com a política de sua organização.

