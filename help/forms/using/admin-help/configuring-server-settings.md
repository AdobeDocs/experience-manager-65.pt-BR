---
title: Definição das configurações do servidor
seo-title: Configuring Server Settings
description: A página Configurações do servidor fornece acesso ao email, à notificação de tarefa e às configurações de notificação do administrador.
seo-description: The Server Settings page provides access to email, task notification and administrator notification settings.
uuid: 73b51ac0-56e5-4748-bb33-e3986c69eb2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e047a95e-0acb-438a-8d27-f005c0adc508
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2625'
ht-degree: 0%

---

# Definição das configurações do servidor {#configuring-server-settings}

A página Configurações do servidor fornece acesso a várias configurações para o fluxo de trabalho de formulários:

* **Configurações de email** que permitem mensagens de email de saída, juntamente com as configurações do servidor de email usadas para essas mensagens. (Consulte [Definição das configurações de email](configuring-server-settings.md#configuring-email-settings).)
* **Configurações de notificação de tarefa** que ativa, desativa ou modifica as mensagens enviadas em notificações por email para usuários finais e grupos em relação a suas tarefas. (Consulte [Configurar notificações para usuários e grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Configurações de notificação do administrador** que ative, desative ou modifique as mensagens enviadas em notificações por email para tarefas administrativas. (Consulte [Configuração de notificações para administradores](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Definição das configurações de email {#configuring-email-settings}

Você pode especificar uma conta de email para o servidor de formulários, por meio da qual ele envia mensagens de email para usuários e administradores de formulários AEM. Essas mensagens de email são usadas para notificar e lembrar aos usuários as tarefas que eles devem concluir, notificar o usuário das tarefas que atingiram um prazo e notificar o administrador de qualquer erro de processo que ocorrer.

Para habilitar o envio de mensagens de email entre AEM formulários e usuários, configure as configurações de email de saída na página Configurações de email . O email de saída deve usar um servidor SMTP.

Para permitir que formulários AEM recebam e manipulem mensagens de email de entrada de usuários, crie um terminal de email para o serviço Concluir tarefa. (Consulte [Criar um terminal de email para o serviço Concluir tarefa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Se os processos forem projetados e implementados sem exigir email, não será necessário configurar nenhuma das opções na página Configurações de email .

### Definir configurações de email de saída {#configure-outgoing-email-settings}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Configurações do servidor > Configurações de email.
1. Selecione Ativar mensagens de saída.
1. Na caixa Servidor SMTP, digite o nome ou o endereço IP do servidor de email. Todas as mensagens de email de notificação do fluxo de trabalho de formulários são enviadas deste servidor de email.
1. Nas caixas Nome de usuário e Senha, digite o nome de logon e a senha a serem usados quando o servidor SMTP exigir autenticação. Deixe-os em branco se o logon anônimo for permitido.
1. Na caixa Endereço de email, digite o endereço de email a ser usado como endereço de retorno para mensagens de email enviadas pelo fluxo de trabalho de formulários.

   >[!NOTE]
   >
   >Se você estiver usando o Microsoft Exchange Server e o Endereço de email for um endereço de email inválido, o servidor Microsoft Exchange não enviará um email para Listas de distribuição. Para resolver o problema, selecione o **Ativar comunicação externa** separadamente para cada lista de distribuição no servidor do Microsoft Exchange.

1. Clique em Salvar.

>[!NOTE]
>
>Se você inserir informações incorretas, poderá clicar em Cancelar para voltar à página exibida anteriormente.

### Configuração de modelos de email para usar o AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>O espaço de trabalho do Flex foi descontinuado para AEM versão dos formulários.

Por padrão, os emails enviados por AEM formulários contêm links para (obsoleto para AEM formulários no JEE) Flex Workspace. Você pode configurar AEM formulários para enviar emails com links para o AEM Forms Workspace. Para saber mais sobre os benefícios do AEM Forms Workspace sobre (obsoleto para formulários AEM no JEE) Flex Workspace, consulte [this](/help/forms/using/features-html-workspace-available-flex.md) artigo 10. o

1. No console de administração, clique em Início > Serviços > fluxo de trabalho de formulários > Configurações do servidor > Notificações de tarefa.
1. Abrir modelo de atribuição de tarefa.
1. Defina o modelo nas notificações da tarefa para o seguinte: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurar notificações para usuários e grupos {#configuring-notifications-for-users-and-groups}

Na página Notificação de tarefa , é possível configurar modelos que o fluxo de trabalho de formulários usará para gerar as notificações por email enviadas a usuários e grupos. Você pode personalizar e formatar as notificações usando variáveis de fluxo de trabalho de formulários.

Você configura os seguintes tipos de notificações para usuários e grupos:

* lembretes
* atribuições de tarefa
* prazos

Para gerar notificações por email para um grupo, especifique um endereço de email para o grupo no Gerenciamento de usuários. <!--Fix broken link See Setting up and organizing users -->Quando o fluxo de trabalho de formulários envia uma notificação por email para um grupo, cada membro do grupo que tem um endereço de email especificado recebe a notificação por email. Quando um membro do grupo recebe uma notificação por email e deseja reivindicar a tarefa, o membro deve clicar no link de reivindicação na notificação por email, o que abre a página de detalhes da tarefa no Workspace. A partir daí, o membro pode reivindicar ou reivindicar e abrir o item de trabalho.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

### Configurar lembretes para usuários ou grupos {#configure-reminders-for-users-or-groups}

Você pode enviar notificações de lembrete para o usuário ou grupo atribuído quando um prazo para concluir uma tarefa estiver se aproximando. As regras para determinar exatamente quando uma notificação de lembrete é enviada são determinadas pelo desenvolvedor do processo.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de notificação, clique em Lembrete (para usuários) ou em Grupo - Lembrete (para grupos).
1. Selecione Ativar Lembrete ou Ativar Grupo - Lembrete.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados com a mensagem de email de lembrete, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto para a linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email , selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de atribuição de tarefa para usuários ou grupos {#configure-task-assignment-notifications-for-users-or-groups}

Você pode enviar notificações de atribuição de tarefa a um usuário ou grupo quando uma tarefa for atribuída a eles.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de Notificação, clique em Atribuição de Tarefa para usuários ou Grupo - Atribuição de Tarefa para grupos.
1. Selecione Habilitar Atribuição de Tarefa para usuários ou Habilitar Grupo - Atribuição de Tarefa para grupos.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados com a mensagem de email de atribuição de tarefa, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto para a linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email , selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de prazo para usuários ou grupos {#configure-deadline-notifications-for-users-or-groups}

Você pode enviar notificações de prazo para usuários e grupos quando o prazo para agir em uma tarefa atribuída tiver expirado. Uma notificação de prazo geralmente é informativa porque o usuário não pode mais agir na tarefa atribuída.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de notificação, clique em Prazo (para usuários) ou Grupo - Prazo (para grupos).
1. Selecione Habilitar prazo ou Habilitar grupo - prazo.
1. Na caixa Assunto, digite o texto para a linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email , selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Ocultar a tag NÃO DELETE para todos os emails {#hide-the-do-not-delete-tag-for-all-emails}

Você pode configurar o email para ocultar a tag de rastreamento NÃO DELETE em todos os emails enviados em um processo centrado no ser humano.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configuração de notificações para administradores {#configuring-notifications-for-administrators}

Você pode configurar modelos que o fluxo de trabalho de formulários usará para gerar as notificações por email enviadas aos administradores.

Você configura os seguintes tipos de notificações para administradores:

* ramificação paralisada
* operação paralisada

### Configurar notificações de ramificação paralisada {#configure-stalled-branch-notifications}

Se uma ramificação for interrompida (para de continuar deliberadamente ou por causa de um erro), será possível enviar uma notificação por email a um administrador ou outro usuário, que poderá então investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Ramificação paralisada.
1. Selecione Habilitar Ramificação Paralisada.
1. Na caixa Endereço de email, digite os endereços dos usuários para notificar quando uma ramificação for interrompida. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto para a linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato de mensagem, selecione o formato no qual a mensagem de email é enviada, HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email , selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usa. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de operação paralisada {#configure-stalled-operation-notifications}

Se uma operação for interrompida (para de continuar deliberadamente ou por causa de um erro), você poderá enviar uma notificação por email a um administrador ou outro usuário, que poderá investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Operação paralisada.
1. Selecione Enable Stalled Operation (Ativar operação paralisada).
1. Na caixa Endereços de email, digite os endereços dos usuários a serem notificados quando uma operação for interrompida. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto para a linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre a personalização deste campo, consulte [Personalização do conteúdo das notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Clique em Salvar.

## Personalização do conteúdo das notificações {#customizing-the-content-of-notifications}

As páginas Notificações de tarefa e Notificações do administrador fornecem vários recursos que permitem personalizar mensagens de notificação:

* editor de rich text
* seletor de variável
* Geração de URL

### Editor de Rich Text {#rich-text-editor}

A área Modelo de notificação é um editor de rich text que permite gerar HTML para as mensagens de notificação por email. Fornece opções de formatação de fonte e parágrafo, que são encontradas abaixo da caixa Modelo de notificação. As opções incluem tipo de fonte, tamanho, estilo e cor, bem como alinhamento e marcadores de parágrafo.

### Geração de URL {#url-generation}

Somente para Notificações de Tarefa, o fluxo de trabalho do Forms inclui duas configurações de URL predefinidas que você pode arrastar da lista Geração de Url para a caixa Modelo de Notificação e depois personalizar:

* OpenTask está disponível para os tipos de notificação Lembrete e Atribuição de Tarefa. Esse URL fornece um link para a tarefa no Workspace, permitindo que o usuário acesse a tarefa rapidamente a partir da notificação por email. Quando você arrasta o URL OpenTask para a caixa Modelo de notificação, o URL está no seguinte formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* O ClaimTask está disponível para os tipos de notificação Grupo - Lembrete e Grupo - Atribuição de Tarefa. Esse URL fornece um link para a página de detalhes da tarefa no Workspace, onde o usuário pode reivindicar ou reivindicar e abrir o item de trabalho. Quando você arrasta o URL ClaimTask para a caixa Modelo de notificação, o URL está no seguinte formato:

   `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

Se a solução for implantada em um ambiente em cluster, substitua `@@notification-host@@` com o endereço do cluster.

`<`*PORTA* `>` é o número da porta do ouvinte HTTP do servidor de aplicativos. A porta de ouvinte HTTP padrão para os servidores de aplicativos compatíveis é a seguinte:

**JBoss:** 8080

**Servidor WebLogic do Oracle:** 7001

**IBM WebSphere:** 9080

Para que esses URLs funcionem corretamente, substitua `<`*PORTA* `>` com o número da porta apropriado para seu ambiente.

>[!NOTE]
>
>Se você estiver usando um aplicativo Web personalizado diferente do Forms para fornecer aos usuários acesso às tarefas, deverá usar um formato de URL apropriado para seu aplicativo personalizado.

### Seletor de variável {#variable-picker}

A lista Seletor de variável fornece variáveis úteis que você pode arrastar e soltar nas caixas Assunto ou Modelo de notificação. Quando você solta uma variável nas caixas Assunto ou Modelo de notificação, ela muda para o nome da variável do fluxo de trabalho de formulários real com dois símbolos @ em qualquer lado, por exemplo, `@@taskid@@`.

Para lembretes, atribuições de tarefa e prazos para usuários e grupos, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação :

**descrição** O conteúdo da propriedade Description, conforme definido na etapa do usuário (ponto inicial, operação Assign Task ou operação Assign Multiple Tasks) do processo no Workbench.

**instruções** O conteúdo da propriedade Instruções da Tarefa, conforme definido na etapa do usuário do processo no Workbench.

**host de notificação** O nome de host do servidor de aplicativos do AEM forms .

**nome do processo** O nome do processo.

**nome da operação** O nome da etapa.

**brincalhão** O identificador exclusivo da tarefa atual.

**ações** Produz uma lista numerada de rotas válidas (por exemplo, Aprovar, Rejeitar) em que o recipient pode clicar.

Além disso, para lembretes de grupo, atribuições de tarefa de grupo e prazos de grupo, você também pode usar:

**group-name** O nome do grupo ao qual foi atribuído o item de trabalho.

>[!NOTE]
>
>Se uma variável não tiver valor, nada será retornado.

Para ramificações paralisadas, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação :

**branch-id** O identificador da ramificação.

**process-id** O identificador da instância do processo.

**host de notificação** O nome de host do servidor de aplicativos do AEM forms .

Para operações paralisadas, você pode usar as seguintes variáveis nas caixas Assunto e Modelo de notificação :

**action-id** O identificador da operação.

**branch-id** O identificador da ramificação.

**process-id** O identificador da instância do processo.

**host de notificação** O nome de host do servidor de aplicativos do AEM forms .

### Uso de uma variável na caixa Assunto {#using-a-variable-in-the-subject-box}

Se você digitar o seguinte texto na caixa Assunto para notificações de Atribuição de Tarefa:

`Please complete task @@taskid@@`

O usuário recebe uma mensagem de email com o seguinte assunto se a tarefa 376 for atribuída:

`Please complete task 376`

### Uso de variáveis na caixa Modelo de notificação {#using-variables-in-the-notification-template-box}

Se você digitar o seguinte texto na caixa Modelo de notificação para notificações de Ramificação Paralisada:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

O administrador recebe uma mensagem de email que contém o seguinte conteúdo se o número da ramificação for 4868 e o nome do servidor for `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configurar conexões de monitoramento de atividade comercial {#configuring-business-activity-monitoring-connections}

O Business Activity Monitoring, um módulo opcional, fornece um conjunto de painéis operacionais que fornecem visibilidade em tempo real de suas operações e indicadores-chave de desempenho.

Na página Configurações do BAM, defina as conexões com o servidor que executa o BAM para que os eventos relacionados ao processo possam ser rastreados e transmitidos para esse servidor.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Configurações do BAM.
1. Na caixa Host BAM, digite o nome do servidor que executa o BAM. O padrão é localhost.
1. Na caixa Porta BAM, digite a porta a ser usada para se conectar ao servidor que executa BAM. A porta BAM padrão para JBoss é 8080, WebLogic é 7001 e WebSphere é 9080.
1. Na caixa Host do servidor, digite o nome ou o endereço IP do servidor de formulários do host. O valor padrão é localhost.
1. Na caixa Porta do servidor, digite o número da porta usada pelo servidor de formulários.
1. Nas caixas Nome de usuário e Senha, digite o ID de usuário e a senha apropriados para acessar o Servidor BAM. O nome de usuário padrão é CognosNowAdmin e a senha padrão é Gerente.
1. Clique em Salvar.
