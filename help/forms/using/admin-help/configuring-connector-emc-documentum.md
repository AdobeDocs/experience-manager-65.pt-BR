---
title: Configurando o conector para o EMC Documentum
description: Saiba como configurar o Connector for EMC Documentum para permitir a comunicação entre o AEM Forms e o EMC Documentum.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a31a496f-87b9-43c0-a98c-5f6ca5d11690
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 1%
---
# Configurando o conector para o EMC Documentum {#configuring-connector-for-emc-documentum}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

O Connector for EMC Documentum permite a comunicação entre o AEM Forms e o EMC Documentum. Para obter informações adicionais em segundo plano, consulte &quot;Conectores para ECM&quot; na [Referência de Serviços](https://www.adobe.com/go/learn_aemforms_services_63).

A configuração do Connector for EMC Documentum envolve a configuração da conexão do servidor e das credenciais do repositório.

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Na versão atual, os ativos são armazenados no repositório nativo do AEM Forms e os serviços do Provedor do repositório foram descontinuados. A migração de ativos de um repositório ECM para o repositório do AEM Forms é feita ao fazer um upgrade para o AEM Forms. Para obter mais informações, consulte o Guia de atualização de formulários do AEM para o servidor de aplicativos.

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

**Nome do Provedor de Serviço do Repositório Atual:** O nome do provedor de serviço do repositório atual

**Provedor do repositório da Documentum ECM:** Transforma o provedor do repositório da Documentum no provedor do repositório. Esta opção foi descontinuada

**provedor do repositório:** Transforma o provedor do repositório nativo no provedor do repositório

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

## Habilitar a solicitação para compartilhamento de filas de tarefas do Workspace {#enable-the-request-for-sharing-of-workspace-task-queues}

Algumas etapas manuais são necessárias para garantir que o recurso Request for Sharing of Task Queue (Solicitação de compartilhamento de fila de tarefas) no Workspace funcione corretamente com o Connector for EMC Documentum.

1. Depois que o AEM Forms for implantado e o Workbench for instalado, faça logon no Workbench e abra a visualização Recursos. Você determinará onde o arquivo QueueSharing.swf está localizado nessa visualização.
1. Arraste o arquivo QueueSharing.swf da Exibição de recursos para a área de trabalho do Windows ou um local equivalente, dependendo do seu sistema operacional.
1. No console de administração, clique em Services > Connector for EMC Documentum > Configuration Settings.
1. Em Repository Service Provider Information (Informações do provedor de serviços do repositório), altere o provedor do repositório configurado para EMC Documentum Repository Provider.
1. Inicie o Workbench e copie o arquivo QueueSharing.swf do local em que você o copiou originalmente (por exemplo, a área de trabalho do Windows ou outro local) em um diretório existente dentro do repositório do EMC Documentum.
1. Na view Processos do Workbench, abra o processo Compartilhamento de Filas.
1. Na visualização Variáveis, abra as propriedades da variável &quot;theForm&quot; e altere o URI para corresponder ao caminho em que você colocou o arquivo QueueSharing.swf na etapa 5.
1. Salve o processo.
1. Migre o processo para o ambiente de produção de acordo com a política de sua organização.
