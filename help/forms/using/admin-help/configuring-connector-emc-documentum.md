---
title: Configurando o Connector para EMC Documentum
seo-title: Configuring Connector for EMC Documentum
description: Saiba como configurar o Connector for EMC Documentum para permitir a comunicação entre AEM forms e o EMC Documentum.
seo-description: Learn how to configure the Connector for EMC Documentum to enable communication between AEM forms and EMC Documentum.
uuid: fc96900a-ec8a-4efd-ad8e-25e9967e649b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e62370a7-9d9e-43a3-8014-8e53800c870d
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# Configurando o Connector para EMC Documentum {#configuring-connector-for-emc-documentum}

O Connector for EMC Documentum permite a comunicação entre AEM forms e o EMC Documentum. Para obter mais informações de fundo, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

Configurar o Connector para o EMC Documentum envolve configurar a conexão do servidor e as credenciais do repositório.

>[!NOTE]
>
>Em versões anteriores , os ativos podiam ser armazenados em um repositório ECM. Na versão atual, os ativos são armazenados no repositório nativo dos formulários AEM e os serviços do Provedor de Repositório foram descontinuados. A migração de ativos de um repositório ECM para o repositório AEM forms é feita ao executar uma atualização para AEM formulários. Para obter mais informações, consulte o guia de Atualização de formulários AEM para seu servidor de aplicativos.

## Configuração da conexão com o servidor {#configuring-the-server-connection}

Este tópico descreve as tarefas do Connector for EMC Documentum que você pode executar na página Configurações.

>[!NOTE]
>
>Se você estiver configurando todas as configurações simultaneamente, só precisará clicar em Salvar uma vez.

### Configurar o servidor {#configure-the-server}

É necessário configurar as informações do servidor do Agente de Conexão. Essas informações são necessárias para se conectar aos repositórios de conteúdo do Documentum e iniciar o Connector for EMC Documentum.

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações de Configuração da Documentum, insira o nome do host ou endereço IP e o número da porta do agente de conexão. O número da porta deve ser um número inteiro positivo (por exemplo, 1489).
1. Clique em Salvar.

### Configurar credenciais principais {#configure-principal-credentials}

Ao configurar as credenciais principais, o nome do repositório que você fornecer dependerá se um nome de repositório explícito será fornecido durante o logon.

Se você inserir um nome de usuário ou senha incorretos, obterá os seguintes resultados, dependendo se o serviço está em execução no momento:

* Se tanto o serviço EMC Documentum Repository Provider quanto o serviço EMC Documentum Content Repository Connector forem interrompidos, quando você salvar as informações de configuração de serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço EMC Documentum Repository Provider ou o serviço EMC Documentum Content Repository Connector forem iniciados, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credenciais imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações de Credenciais Principais da Documentum, digite o nome de usuário e a senha de um usuário com privilégios de superadministrador.
1. Se um nome de repositório explícito não for fornecido durante o logon, insira o nome do repositório ao qual as credenciais estão associadas.
1. Clique em Salvar.

### Alterar o provedor de serviços de repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviços de repositório usar com o Documentum. Chamadas de serviço de repositório são delegadas ao provedor que você configura. As opções disponíveis são as seguintes:

**Nome atual do provedor de serviços de repositório:** O nome do provedor de serviços de repositório atual

**Provedor de Repositório ECM Documentum:** Torna o provedor do repositório Documentum o provedor do repositório. Essa opção foi substituída

**provedor de repositório:** Torna o provedor do repositório nativo o provedor do repositório

>[!NOTE]
>
>Para selecionar um provedor de serviços de repositório diferente daqueles listados, configure o RepositoryService em Aplicativos e Serviços > Gerenciamento de Serviços. <!-- Fix broken link (See Managing Services) -->.

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Na área Informações do Provedor de Serviços de Repositório, selecione o provedor de serviço de repositório alternativo.
1. Clique em Salvar.

## Configuração de credenciais do repositório {#configuring-repository-credentials}

As informações de credenciais do Documentum são usadas no contexto do sistema de formulários de AEM. As credenciais do repositório são específicas a repositórios específicos no Documentum. Você pode fornecer credenciais para qualquer número de repositórios; no entanto, você pode especificar apenas um conjunto de credenciais por repositório.

### Adicionar uma credencial de repositório {#add-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações de Credenciais de Repositório.
1. Clique em Adicionar. A página Informações sobre Credenciais do Sistema da Documentum é exibida.
1. Insira um nome para o repositório.
1. Digite um nome de usuário e senha.
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiver em execução, as informações de credenciais serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

### Remover uma credencial de repositório {#remove-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Marque a caixa de seleção ao lado do repositório do qual deseja remover credenciais e clique em Remover. As credenciais para o repositório selecionado são removidas do banco de dados.

### Alterar o nome de usuário e a senha de uma credencial de repositório {#change-the-user-name-and-password-for-a-repository-credential}

1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Clique no nome do repositório para editar credenciais.
1. Altere o nome de usuário ou a senha do repositório, ou ambos. (O nome do repositório é somente leitura.)
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiver em execução, as informações de credenciais serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

## Habilitar a solicitação de compartilhamento de filas de tarefas do Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Algumas etapas manuais são necessárias para garantir que o recurso Solicitação de compartilhamento da fila de tarefas no Workspace funcione corretamente com o Connector for EMC Documentum.

1. Depois que AEM formulários for implantado e o Workbench for instalado, faça logon no Workbench e abra a visualização Recursos. Você determinará onde o arquivo QueueSharing.swf está localizado nessa visualização.
1. Arraste o arquivo QueueSharing.swf da Exibição de Recursos para a área de trabalho do Windows ou um local equivalente, dependendo do sistema operacional.
1. No console de administração, clique em Serviços > Conector para EMC Documentum > Configurações.
1. Em Informações do Provedor de Serviços de Repositório, altere o provedor de repositório configurado para Provedor de Repositório EMC Documentum.
1. Inicie o Workbench e copie o arquivo QueueSharing.swf do local onde você o copiou originalmente para (por exemplo, o desktop do Windows ou outro local) em um diretório existente dentro do repositório do EMC Documentum.
1. Na visualização Processos do Workbench, abra o processo de Compartilhamento de filas.
1. Na exibição Variáveis, abra as propriedades da variável &quot;theForm&quot; e altere o URI para corresponder ao caminho onde você colocou o arquivo QueueSharing.swf na etapa 5.
1. Salve o processo.
1. Migre o processo para o ambiente de produção de acordo com a política de sua organização.
