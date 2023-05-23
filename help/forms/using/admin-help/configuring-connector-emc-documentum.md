---
title: Configurando o conector para o EMC Documentum
seo-title: Configuring Connector for EMC Documentum
description: Saiba como configurar o Connector for EMC Documentum para permitir a comunicação entre formulários AEM e o EMC Documentum.
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

# Configurando o conector para o EMC Documentum {#configuring-connector-for-emc-documentum}

O Connector for EMC Documentum permite a comunicação entre formulários AEM e o EMC Documentum. Para obter informações adicionais, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

A configuração do Connector for EMC Documentum envolve a configuração da conexão do servidor e das credenciais do repositório.

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Na versão atual, os ativos são armazenados no repositório nativo de formulários AEM e os serviços do Provedor do repositório foram descontinuados. A migração de ativos de um repositório de ECM para o repositório de formulários AEM é feita ao fazer uma atualização para formulários AEM. Para obter mais informações, consulte o Guia de atualização de formulários AEM para o servidor de aplicativos.

## Configuração da conexão do servidor {#configuring-the-server-connection}

Este tópico descreve as tarefas do Connector for EMC Documentum que você pode executar na página Configurações Definições.

>[!NOTE]
>
>Se você estiver definindo todas as configurações simultaneamente, só será necessário clicar em Salvar uma vez.

### Configurar o servidor {#configure-the-server}

Você precisa configurar as informações do servidor do agente de conexão. Essas informações são necessárias para conectar-se aos repositórios de conteúdo da Documentum e iniciar o Connector for EMC Documentum.

1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Na área Informações de Configuração da Documentum, digite o nome do host ou endereço IP e o número da porta do agente de conexão. O número da porta deve ser um inteiro positivo (por exemplo, 1489).
1. Clique em Salvar.

### Configurar credenciais da entidade {#configure-principal-credentials}

Ao configurar as credenciais principais, o nome do repositório fornecido dependerá se um nome de repositório explícito for fornecido durante o logon.

Se você digitar um nome de usuário ou senha incorretos, os resultados a seguir serão obtidos, dependendo se o serviço estiver sendo executado no momento:

* Se os serviços do Provedor de Repositório da EMC Documentum e do Conector de Repositório de Conteúdo da EMC Documentum forem interrompidos, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço EMC Documentum Repository Provider ou o serviço EMC Documentum Content Repository Connector forem iniciados, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credencial imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Na área Informações de Credenciais Principais da Documentum, digite o nome de usuário e a senha de um usuário com privilégios de superadministrador.
1. Se um nome de repositório explícito não for fornecido durante o logon, insira o nome do repositório ao qual as credenciais estão associadas.
1. Clique em Salvar.

### Alterar o provedor de serviços do repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviços de repositório usar com a Documentum. As chamadas de serviço do repositório são delegadas ao provedor configurado. As opções disponíveis são as seguintes:

**Nome do Provedor de Serviços do Repositório Atual:** O nome do provedor de serviços de repositório atual

**Provedor de repositório ECM Documentum:** Torna o provedor do repositório Documentum o provedor do repositório. Esta opção foi descontinuada

**provedor do repositório:** Torna o provedor do repositório nativo o provedor do repositório

>[!NOTE]
>
>Para selecionar um provedor de serviços de repositório diferente dos listados, configure Serviço de Repositório em Aplicativos e Serviços > Gerenciamento de Serviços. <!-- Fix broken link (See Managing Services) -->.

1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Na área Informações do Provedor de Serviços do Repositório, selecione o provedor de serviços do repositório alternativo.
1. Clique em Salvar.

## Configurar credenciais do repositório {#configuring-repository-credentials}

As informações de credencial da Documentum são usadas no contexto do sistema de formulários AEM. As credenciais de repositório são específicas para repositórios específicos na Documentum. É possível fornecer credenciais para qualquer número de repositórios; no entanto, você pode especificar apenas um conjunto de credenciais por repositório.

### Adicionar uma credencial de repositório {#add-a-repository-credential}

1. No console de administração, clique em Services > Connector for EMC Documentum > Repository Credentials Settings.
1. Clique em Adicionar. A página Informações de Credenciais do Sistema da Documentum é exibida.
1. Insira um nome para o repositório.
1. Digite um nome de usuário e uma senha.
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiverem em execução, as informações de credencial serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

### Remover uma credencial de repositório {#remove-a-repository-credential}

1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Marque a caixa de seleção ao lado do repositório do qual remover as credenciais e clique em Remover. As credenciais do repositório selecionado são removidas do banco de dados.

### Alterar o nome de usuário e a senha de uma credencial de repositório {#change-the-user-name-and-password-for-a-repository-credential}

1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Clique no nome do repositório para o qual editar credenciais.
1. Altere o nome de usuário ou a senha do repositório, ou ambos. (O nome do repositório é somente leitura.)
1. Clique em Salvar.

Se o Content Repository Connector for EMC Documentum Service e/ou o Repository Service for EMC Documentum estiverem em execução, as informações de credencial serão verificadas em relação ao repositório especificado antes de serem armazenadas no banco de dados. Se as credenciais forem inválidas ou existirem, uma mensagem de erro será exibida.

## Habilitar a solicitação para compartilhamento de filas de tarefas do Espaço de trabalho {#enable-the-request-for-sharing-of-workspace-task-queues}

Algumas etapas manuais são necessárias para garantir que o recurso Request for Sharing of Task Queue (Solicitação de compartilhamento de fila de tarefas) no Workspace funcione corretamente com o Connector for EMC Documentum.

1. Depois que os formulários AEM forem implantados e o Workbench for instalado, faça logon no Workbench e abra a visualização Recursos. Você determinará onde o arquivo QueueSharing.swf está localizado nessa visualização.
1. Arraste o arquivo QueueSharing.swf da Exibição de recursos para a área de trabalho do Windows ou um local equivalente, dependendo do seu sistema operacional.
1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Em Repository Service Provider Information (Informações do provedor de serviços do repositório), altere o provedor do repositório configurado para EMC Documentum Repository Provider.
1. Inicie o Workbench e copie o arquivo QueueSharing.swf do local em que você o copiou originalmente (por exemplo, a área de trabalho do Windows ou outro local) em um diretório existente dentro do repositório do EMC Documentum.
1. Na view Processos do Workbench, abra o processo Compartilhamento de Filas.
1. Na visualização Variáveis, abra as propriedades da variável &quot;theForm&quot; e altere o URI para corresponder ao caminho em que você colocou o arquivo QueueSharing.swf na etapa 5.
1. Salve o processo.
1. Migre o processo para o ambiente de produção de acordo com a política de sua organização.
