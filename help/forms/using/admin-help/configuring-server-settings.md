---
title: Configuração das configurações do servidor
seo-title: Configuração das configurações do servidor
description: A página Configurações do servidor fornece acesso a email, notificação de tarefa e configurações de notificação do administrador.
seo-description: A página Configurações do servidor fornece acesso a email, notificação de tarefa e configurações de notificação do administrador.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configuração das configurações do servidor {#configuring-server-settings}

A página Configurações do servidor fornece acesso a várias configurações para o fluxo de trabalho de formulários:

* **Configurações** de email que ativam mensagens de email de saída, juntamente com as configurações do servidor de email usadas para essas mensagens. (See [Configuring email settings](configuring-server-settings.md#configuring-email-settings).)
* **Configurações** de notificação de Tarefa que habilitam, desabilitam ou modificam as mensagens enviadas em notificações por email para usuários finais e grupos relacionados às tarefas. (Consulte [Configurar notificações para usuários e grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Configurações** de notificação do administrador que habilitam, desabilitam ou modificam as mensagens enviadas em notificações por email para tarefas administrativas. (Consulte [Configurar notificações para administradores](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Definição das configurações de email {#configuring-email-settings}

Você pode especificar uma conta de email para o servidor de formulários, por meio da qual ela envia mensagens de email para usuários e administradores de formulários AEM. Essas mensagens de email são usadas para notificar e lembrar os usuários de tarefas de que eles devem concluir, notificar o usuário sobre tarefas que atingiram um prazo limite e notificar o administrador de quaisquer erros de processo que ocorrerem.

Para habilitar o envio de mensagens de email entre formulários AEM e usuários, configure as configurações de email de saída na página Configurações de email. O email de saída deve usar um servidor SMTP.

Para permitir que os formulários AEM recebam e lidem com mensagens de email recebidas dos usuários, crie um terminal de email para o serviço de Tarefa completa. (Consulte [Criar um terminal de email para o serviço](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)de Tarefa completa).

Se seus processos forem projetados e implementados sem a necessidade de email, você não precisará configurar nenhuma das opções na página Configurações de email.

### Definir configurações de email de saída {#configure-outgoing-email-settings}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Configurações do servidor > Configurações de e-mail.
1. Selecione Ativar mensagens de saída.
1. Na caixa Servidor SMTP, digite o nome do servidor de email ou o endereço IP. Todas as mensagens de email de notificação do fluxo de trabalho de formulários são enviadas deste servidor de email.
1. Nas caixas Nome de usuário e Senha, digite o nome de login e a senha a serem usados quando o servidor SMTP exigir autenticação. Deixe-os em branco se o logon anônimo for permitido.
1. Na caixa Endereço de email, digite o endereço de email a ser usado como endereço de retorno para mensagens de email enviadas pelo fluxo de trabalho dos formulários.

   >[!NOTE]
   >
   >Se você estiver usando o Microsoft Exchange Server e o Endereço de email for inválido, o servidor do Microsoft Exchange falhará ao enviar um email para o Distribution Lista. Para resolver o problema, selecione a opção **Ativar comunicação** externa separadamente para cada Lista de distribuição no servidor Microsoft Exchange.

1. Clique em Salvar.

>[!NOTE]
>
>Se inserir informações incorretas, clique em Cancelar para voltar à página exibida anteriormente.

### Configuração de modelos de e-mail para usar o AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão de formulários do AEM.

Por padrão, os e-mails enviados pelos formulários AEM contêm links para (obsoletos para formulários AEM no JEE) Flex Workspace. Você pode configurar formulários AEM para enviar emails com links para o AEM Forms Workspace. Para saber mais sobre os benefícios do AEM Forms Workspace sobre (Obsoleto para formulários AEM no JEE) Flex Workspace, consulte [este](/help/forms/using/features-html-workspace-available-flex.md) artigo.

1. No console de administração, clique em Home > Serviços > fluxo de trabalho de formulários > Configurações do servidor > Notificações de Tarefa.
1. Abra o modelo de atribuição de tarefa.
1. Defina o modelo nas notificações de tarefa para o seguinte: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```as3
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurar notificações para usuários e grupos {#configuring-notifications-for-users-and-groups}

Na página Notificação de Tarefa, é possível configurar modelos que o fluxo de trabalho dos formulários usará para gerar as notificações por email enviadas a usuários e grupos. Você pode personalizar e formatar as notificações usando variáveis de fluxo de trabalho de formulários.

Você configura os seguintes tipos de notificações para usuários e grupos:

* lembretes
* Atribuições de tarefa
* prazos

Para gerar notificações por email para um grupo, especifique um endereço de email para o grupo no Gerenciamento de usuários. <!--Fix broken link See Setting up and organizing users -->Quando o fluxo de trabalho dos formulários envia uma notificação por email para um grupo, cada membro do grupo que tem um endereço de email especificado recebe a notificação por email. Quando um membro do grupo recebe uma notificação por e-mail e deseja solicitar a tarefa, o membro deve clicar no link da solicitação na notificação por e-mail, que abre a página de detalhes da tarefa no Workspace. A partir daí, o membro pode reivindicar ou reivindicar e abrir o item de trabalho.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão de formulários do AEM.

### Configurar lembretes para usuários ou grupos {#configure-reminders-for-users-or-groups}

Você pode enviar notificações de lembrete ao usuário ou grupo atribuído quando um prazo para concluir uma tarefa estiver se aproximando. As regras para determinar exatamente quando uma notificação de lembrete é enviada são determinadas pelo desenvolvedor do processo.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de Tarefa.
1. Em Tipo de notificação, clique em Lembrete (para usuários) ou em Grupo - Lembrete (para grupos).
1. Selecione Ativar lembrete ou Ativar grupo - lembrete.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados com a mensagem de email do lembrete, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista de formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de atribuição de tarefa para usuários ou grupos {#configure-task-assignment-notifications-for-users-or-groups}

Você pode enviar notificações de atribuição de tarefa a um usuário ou grupo quando uma tarefa for atribuída a ele.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de Tarefa.
1. Em Tipo de notificação, clique em Atribuição de Tarefa para usuários ou Grupo - Atribuição de Tarefa para grupos.
1. Selecione Ativar atribuição de Tarefa para usuários ou Ativar atribuição de grupo - Tarefa para grupos.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados com a mensagem de email de atribuição da tarefa, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista de formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de prazo para usuários ou grupos {#configure-deadline-notifications-for-users-or-groups}

Você pode enviar notificações de prazo para usuários e grupos quando o prazo para agir com base em uma tarefa atribuída tiver expirado. Uma notificação de prazo normalmente é informativa, pois o usuário não pode mais agir na tarefa atribuída.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de Tarefa.
1. Em Tipo de notificação, clique em Prazo (para usuários) ou em Grupo - Prazo (para grupos).
1. Selecione Habilitar prazo ou Habilitar grupo - prazo.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista de formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Ocultar a tag NÃO EXCLUIR para todos os emails {#hide-the-do-not-delete-tag-for-all-emails}

Você pode configurar e-mail para ocultar o tag de rastreamento NÃO EXCLUIR em todos os e-mails enviados em um processo centralizado no ser humano. Para obter detalhes, consulte [Como ocultar a tag &#39;DO-NOT-DELETE&#39; com CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html)

## Configurar notificações para administradores {#configuring-notifications-for-administrators}

Você pode configurar modelos que o fluxo de trabalho dos formulários usará para gerar as notificações por email enviadas aos administradores.

Você configura os seguintes tipos de notificações para administradores:

* ramo parado
* operação parada

### Configurar notificações de ramificação paradas {#configure-stalled-branch-notifications}

Se uma ramificação parar (parar de continuar deliberadamente ou devido a um erro), você pode receber uma notificação por email para um administrador ou outro usuário, que pode então investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Ramificação parada.
1. Selecione Ativar Ramificação Parada.
1. Na caixa Endereço de email, digite os endereços dos usuários que serão notificados quando uma ramificação parar. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista de formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usa. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de operação parada {#configure-stalled-operation-notifications}

Se uma operação parar (parar de continuar deliberadamente ou devido a um erro), você pode receber uma notificação por email para um administrador ou outro usuário, que pode investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Operação parada.
1. Selecione Ativar operação parada.
1. Na caixa Endereços de e-mail, digite os endereços dos usuários para notificá-los quando uma operação parar. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Esse campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar este campo, consulte [Personalizar o conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Clique em Salvar.

## Personalização do conteúdo das notificações {#customizing-the-content-of-notifications}

As páginas Notificações de Tarefa e Notificações do administrador fornecem vários recursos que permitem personalizar mensagens de notificação:

* editor de rich text
* seletor de variáveis
* Geração de URL

### Rich text editor {#rich-text-editor}

A área Modelo de notificação é um editor de rich text que permite gerar HTML para as mensagens de notificação por email. Fornece opções de formatação de fonte e parágrafo, que são encontradas abaixo da caixa Modelo de notificação. As opções incluem tipo de fonte, tamanho, estilo e cor, bem como alinhamento de parágrafo e marcadores.

### Geração de URL {#url-generation}

Somente para Notificações de Tarefa, o fluxo de trabalho do Forms inclui duas configurações de URL predefinidas que você pode arrastar da lista Geração de Url para a caixa Modelo de Notificação e, em seguida, personalizar:

* OpenTask está disponível para os tipos de notificação Lembrete e Atribuição de Tarefa. Esse URL fornece um link para a tarefa no Workspace, permitindo que o usuário acesse a tarefa rapidamente a partir da notificação por email. Quando você arrasta o URL OpenTask para a caixa Modelo de notificação, o URL está no seguinte formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask está disponível para os tipos de notificação Grupo - Lembrete e Grupo - Atribuição de Tarefa. Este URL fornece um link para a página de detalhes da tarefa no Workspace, onde o usuário pode solicitar ou solicitar e abrir o item de trabalho. Quando você arrasta o URL ClaimTask para a caixa Modelo de notificação, o URL está no seguinte formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão de formulários do AEM.

Se sua solução for implantada em um ambiente agrupado, substitua-a `@@notification-host@@` pelo endereço do cluster.

`<`*PORT *`>`é o número da porta do ouvinte HTTP do servidor de aplicativos. A porta de escuta HTTP padrão para os servidores de aplicativos suportados é a seguinte:

**JBoss:** 8080

**Oracle WebLogic Server:** 7001

**IBM WebSphere:** 9080

Para fazer com que esses URLs funcionem corretamente, substitua `<`*PORT *`>`pelo número da porta apropriado para o seu ambiente.

>[!NOTE]
>
>Se você estiver usando um aplicativo da Web personalizado diferente do Forms para fornecer aos usuários acesso ao tarefa, em vez disso, deverá usar um formato de URL apropriado para seu aplicativo personalizado.

### Seletor de variável {#variable-picker}

A lista Seletor de variáveis fornece variáveis úteis que você pode arrastar e soltar nas caixas Assunto ou Modelo de notificação. Quando você solta uma variável nas caixas Assunto ou Modelo de notificação, ela muda para o nome da variável do fluxo de trabalho de formulários real com dois símbolos @ em ambos os lados, por exemplo, `@@taskid@@`.

Para lembretes, atribuições de tarefa e prazos para usuários e grupos, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**descrição** O conteúdo da propriedade Descrição, conforme definido na etapa do usuário (ponto de start, operação Atribuir Tarefa ou operação Atribuir várias Tarefas) do processo no Workbench.

**instruções** O conteúdo da propriedade Instruções de Tarefa, conforme definido na etapa do usuário do processo no Workbench.

**notification-host** O nome de host do servidor de aplicativos de formulários AEM.

**process-name** O nome do processo.

**operation-name** O nome da etapa.

**tasboy** O identificador exclusivo da tarefa atual.

**ações** Produz uma lista numerada de rotas válidas (por exemplo, Aprovar, Rejeitar) em que o recipient pode clicar.

Além disso, para lembretes de grupo, atribuições de tarefa de grupo e prazos de grupo, você também pode usar:

**group-name** O nome do grupo ao qual foi atribuído o item de trabalho.

>[!NOTE]
>
>Se uma variável não tiver valor, nada será retornado.

Para ramificações paradas, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**branch-id** O identificador do ramo.

**process-id** O identificador da instância do processo.

**notification-host** O nome de host do servidor de aplicativos de formulários AEM.

Para operações paradas, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**action-id** O identificador da operação.

**branch-id** O identificador do ramo.

**process-id** O identificador da instância do processo.

**notification-host** O nome de host do servidor de aplicativos de formulários AEM.

### Uso de uma variável na caixa Assunto {#using-a-variable-in-the-subject-box}

Se você digitar o seguinte texto na caixa Assunto para notificações de Atribuição de Tarefa:

`Please complete task @@taskid@@`

O usuário receberá uma mensagem de email com o seguinte assunto se a tarefa 376 for atribuída:

`Please complete task 376`

### Uso de variáveis na caixa Modelo de notificação {#using-variables-in-the-notification-template-box}

Se você digitar o seguinte texto na caixa Modelo de notificação para notificações de Ramificação Parada:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

O administrador recebe uma mensagem de email que contém o seguinte conteúdo se o número da ramificação for 4868 e o nome do servidor for `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurando conexões de Monitoramento de Atividades Comerciais {#configuring-business-activity-monitoring-connections}

O Business Atividade Monitoring, um módulo opcional, fornece um conjunto de painéis operacionais que fornecem visibilidade em tempo real de suas operações e indicadores-chave de desempenho.

Na página Configurações de configuração do BAM, você define as conexões com o servidor que executa o BAM para que os eventos relacionados ao processo possam ser rastreados e transmitidos para esse servidor.

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Configurações do servidor > Configurações de configuração do BAM.
1. Na caixa Host do BAM, digite o nome do servidor que executa o BAM. O padrão é localhost.
1. Na caixa Porta BAM, digite a porta a ser usada para conectar-se ao servidor que executa o BAM. A porta BAM padrão para JBoss é 8080, WebLogic é 7001 e WebSphere é 9080.
1. Na caixa Host do servidor, digite o nome ou endereço IP do servidor de formulários host. O valor padrão é localhost.
1. Na caixa Porta do servidor, digite o número da porta usado pelo servidor de formulários.
1. Nas caixas Nome de usuário e Senha, digite a ID de usuário e a senha apropriadas para acessar o Servidor BAM. O nome de usuário padrão é CognosNowAdmin e a senha padrão é manager.
1. Clique em Salvar.

