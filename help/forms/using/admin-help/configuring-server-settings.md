---
title: Definição das configurações do servidor
description: A página Configurações do servidor fornece acesso a e-mail, notificação de tarefas e configurações de notificação do administrador.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 362b7b91-c58b-4e47-a6ef-56a4b54a100c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '2643'
ht-degree: 0%

---

# Definição das configurações do servidor {#configuring-server-settings}

A página Configurações do servidor fornece acesso a várias configurações para o fluxo de trabalho de formulários:

* **Configurações de email** que permitem mensagens de email de saída, juntamente com as configurações do servidor de email usadas para essas mensagens. (Consulte [Definindo configurações de email](configuring-server-settings.md#configuring-email-settings).)
* **Configurações de notificação de tarefa** que habilitam, desabilitam ou modificam as mensagens enviadas em notificações por email para usuários finais e grupos em relação a suas tarefas. (Consulte [Configurar notificações para usuários e grupos](configuring-server-settings.md#configuring-notifications-for-users-and-groups).)
* **Configurações de notificação do administrador** que habilitam, desabilitam ou modificam as mensagens enviadas em notificações por email para tarefas administrativas. (Consulte [Configurar notificações para administradores](configuring-server-settings.md#configuring-notifications-for-administrators).)

## Definição das configurações de email {#configuring-email-settings}

Você pode especificar uma conta de email para o Forms Server, por meio da qual ele envia mensagens de email para usuários e administradores de formulários AEM. Essas mensagens de email são usadas para notificar e lembrar os usuários sobre as tarefas que eles devem concluir, notificar o usuário sobre tarefas que atingiram um prazo final e notificar o administrador sobre erros de processo que ocorram.

Para habilitar o envio de mensagens de email entre formulários AEM e usuários, defina as configurações de email de saída na página Configurações de email. O email de saída deve usar um servidor SMTP.

Para permitir que os formulários AEM recebam e lidem com as mensagens de email recebidas dos usuários, crie um terminal de email para o serviço Tarefa Completa. (Consulte [Criar um ponto de extremidade de email para o serviço Concluir Tarefa](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)).

Se seus processos forem projetados e implementados sem a necessidade de enviar um email, não será necessário configurar nenhuma das opções na página Configurações de email.

### Definir configurações de email de saída {#configure-outgoing-email-settings}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Configurações do servidor > Configurações de email.
1. Selecione Ativar mensagens de saída.
1. Na caixa Servidor SMTP, digite o nome do servidor de email ou o endereço IP. Todas as mensagens de email de notificação do workflow de formulários são enviadas deste servidor de email.
1. Nas caixas Nome de usuário e Senha, digite o nome de login e a senha a serem usados quando o servidor SMTP exigir autenticação. Deixe-os em branco se o logon anônimo for permitido.
1. Na caixa Endereço de email, digite o endereço de email que será usado como o endereço de retorno para mensagens de email enviadas pelo workflow dos formulários.

   >[!NOTE]
   >
   >Se você estiver usando o Microsoft Exchange Server e o Endereço de email for um endereço inválido, o Microsoft Exchange Server não enviará um email para Listas de distribuição. Para resolver o problema, selecione a opção **Habilitar Comunicação Externa** separadamente para cada Lista de Distribuição no Microsoft Exchange Server.

1. Clique em Salvar.

>[!NOTE]
>
>Se você inserir informações incorretas, poderá clicar em Cancelar para voltar à página exibida anteriormente.

### Configuração de modelos de email para usar o AEM Forms Workspace {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão do AEM forms.

Por padrão, os emails enviados pelo AEM contêm links para (obsoleto para o AEM forms no JEE) o Flex Workspace. Você pode configurar formulários AEM para enviar emails com links para o AEM Forms Workspace. Para saber mais sobre os benefícios do AEM Forms Workspace em relação ao (obsoleto para o AEM no JEE) Flex Workspace, consulte o artigo [this](/help/forms/using/features-html-workspace-available-flex.md).

1. No console de administração, clique em Início > Serviços > Fluxo de trabalho de formulários > Configurações do servidor > Notificações de tarefa.
1. Abra o modelo de atribuição de tarefa.
1. Defina o modelo nas notificações de tarefa para o seguinte: `https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## Configurar notificações para usuários e grupos {#configuring-notifications-for-users-and-groups}

Na página Notificação de tarefa, é possível configurar os modelos que o fluxo de trabalho dos formulários usará para gerar as notificações por email enviadas aos usuários e grupos. É possível personalizar e formatar as notificações usando variáveis de fluxo de trabalho de formulários.

Você configura os seguintes tipos de notificações para usuários e grupos:

* lembretes
* atribuições de tarefas
* prazos

Para gerar notificações por email para um grupo, especifique um endereço de email para o grupo no Gerenciamento de usuários. <!--Fix broken link See Setting up and organizing users -->Quando o fluxo de trabalho de formulários envia uma notificação por email para um grupo, cada membro do grupo que tem um endereço de email especificado recebe a notificação por email. Quando um membro do grupo recebe uma notificação por email e deseja reivindicar a tarefa, ele deve clicar no link de reivindicação na notificação por email, que abre a página de detalhes da tarefa no Workspace. A partir daí, o membro pode reivindicar ou reivindicar e abrir o item de trabalho.

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

### Configurar lembretes para usuários ou grupos {#configure-reminders-for-users-or-groups}

Você pode enviar notificações de lembrete ao usuário ou grupo atribuído quando o prazo para concluir uma tarefa estiver se aproximando. As regras para determinar exatamente quando uma notificação de lembrete é enviada são determinadas pelo desenvolvedor do processo.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de notificação, clique em Lembrete (para usuários) ou Grupo - Lembrete (para grupos).
1. Selecione Ativar lembrete ou Ativar grupo - lembrete.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados com a mensagem de email de lembrete, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato da mensagem, selecione o formato em que a mensagem de email é enviada, seja HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de atribuição de tarefas para usuários ou grupos {#configure-task-assignment-notifications-for-users-or-groups}

Você pode enviar notificações de atribuição de tarefa a um usuário ou grupo quando uma tarefa for atribuída a ele.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de notificação, clique em Atribuição de tarefa para usuários ou em Grupo - Atribuição de tarefa para grupos.
1. Selecione Habilitar atribuição de tarefa para usuários ou Habilitar grupo - Atribuição de tarefa para grupos.
1. (Somente notificações do usuário) Para incluir um anexo do formulário e seus dados na mensagem de email de atribuição da tarefa, selecione Incluir dados do formulário.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato da mensagem, selecione o formato em que a mensagem de email é enviada, seja HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de prazo para usuários ou grupos {#configure-deadline-notifications-for-users-or-groups}

Você pode enviar notificações de prazo final para usuários e grupos quando o prazo para agir em uma tarefa atribuída tiver expirado. Uma notificação de prazo geralmente é informativa, pois o usuário não pode mais agir de acordo com a tarefa atribuída.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações de tarefa.
1. Em Tipo de notificação, clique em Prazo (para usuários) ou Grupo - Prazo (para grupos).
1. Selecione Ativar prazo ou Ativar grupo - prazo final.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato da mensagem, selecione o formato em que a mensagem de email é enviada, seja HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usará. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Ocultar a tag DO NOT DELETE para todos os emails {#hide-the-do-not-delete-tag-for-all-emails}

Você pode configurar o email para ocultar a tag de rastreamento DO NOT DELETE em todos os emails enviados em um processo centrado no ser humano.

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## Configurar notificações para administradores {#configuring-notifications-for-administrators}

Você pode configurar modelos que o workflow de formulários usará para gerar as notificações por email enviadas aos administradores.

Você configura os seguintes tipos de notificações para administradores:

* ramificação paralisada
* operação paralisada

### Configurar notificações de ramificação paralisada {#configure-stalled-branch-notifications}

Se uma ramificação for interrompida (o processo é interrompido deliberadamente ou devido a um erro), você pode enviar uma notificação por email para um administrador ou outro usuário, que pode investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Ramificação paralisada.
1. Selecione Habilitar ramificação paralisada.
1. Na caixa Endereço de email, digite os endereços dos usuários a serem notificados quando uma ramificação for interrompida. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Na lista Formato da mensagem, selecione o formato em que a mensagem de email é enviada, seja HTML ou Texto. O formato padrão é HTML.
1. Na lista Codificação de email, selecione o formato de codificação a ser usado para a mensagem de email. O padrão é UTF-8, que a maioria dos usuários fora do Japão usa. Os usuários no Japão podem selecionar ISO2022-JP.
1. Clique em Salvar.

### Configurar notificações de operações interrompidas {#configure-stalled-operation-notifications}

Se uma operação for interrompida (interrompida deliberadamente ou devido a um erro), você poderá enviar uma notificação por e-mail a um administrador ou outro usuário, que poderá investigar o problema.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Notificações do administrador.
1. Em Tipo de notificação, clique em Operação interrompida.
1. Selecione Habilitar Operação Paralisada.
1. Na caixa Endereços de email, digite os endereços dos usuários que serão notificados quando uma operação for interrompida. Use o formato user@domain.com e separe cada endereço com uma vírgula. Normalmente, esse endereço de email é para um administrador.
1. Na caixa Assunto, digite o texto da linha de assunto da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications)
1. Na caixa Modelo de notificação, digite o texto para o corpo da mensagem de email. Este campo é pré-preenchido com texto padrão. Para obter detalhes sobre como personalizar esse campo, consulte [Personalização do conteúdo de notificações](configuring-server-settings.md#customizing-the-content-of-notifications).
1. Clique em Salvar.

## Personalização do conteúdo de notificações {#customizing-the-content-of-notifications}

As páginas Notificações de Tarefa e Notificações do Administrador fornecem vários recursos que permitem personalizar mensagens de notificação:

* editor de rich text
* seletor de variável
* Geração de URL

### Editor de Rich Text {#rich-text-editor}

A área Modelo de notificação é um editor de rich text que permite gerar HTML para as mensagens de notificação por email. Ela fornece opções de formatação de fonte e parágrafo, que são encontradas abaixo da caixa Modelo de notificação. As opções incluem tipo de fonte, tamanho, estilo e cor, além de alinhamento de parágrafo e marcadores.

### Geração de URL {#url-generation}

Somente para Notificações de Tarefas, o workflow do Forms inclui duas configurações de URL predefinidas que você pode arrastar da lista Geração de URL para a caixa Modelo de Notificação e, em seguida, personalizar:

* OpenTask está disponível para os tipos de notificação Lembrete e Atribuição de tarefa. Esse URL fornece um link para a tarefa no Workspace, permitindo que o usuário acesse a tarefa rapidamente a partir da notificação por email. Quando você arrasta o URL OpenTask para a caixa Modelo de notificação, o URL está no seguinte formato:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask está disponível para os tipos de notificação Grupo - Lembrete e Grupo - Atribuição de tarefa. Esse URL fornece um link para a página de detalhes da tarefa no Workspace, onde o usuário pode reivindicar ou reivindicar e abrir o item de trabalho. Quando você arrasta o URL da Tarefa de Declaração para a caixa Modelo de Notificação, o URL está no seguinte formato:

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

Se a solução for implantada em um ambiente de cluster, substitua `@@notification-host@@` pelo endereço do cluster.

`<`*PORTA* `>` é o número da porta do ouvinte HTTP do servidor de aplicativos. A porta de listener HTTP default para os servidores de aplicativos suportados é a seguinte:

**JBoss:** 8080

**Servidor WebLogic do Oracle:** 7001

**IBM WebSphere:** 9080

Para que essas URLs funcionem corretamente, substitua `<`*PORT* `>` pelo número de porta apropriado para seu ambiente.

>[!NOTE]
>
>Se você estiver usando um aplicativo web personalizado diferente do Forms para fornecer aos usuários acesso às tarefas, deverá usar um formato de URL apropriado para seu aplicativo personalizado.

### Seletor de variáveis {#variable-picker}

A lista Seletor de variáveis fornece variáveis úteis que você pode arrastar e soltar nas caixas Assunto ou Modelo de notificação. Quando você solta uma variável nas caixas Assunto ou Modelo de notificação, ela é alterada para o nome real da variável do fluxo de trabalho dos formulários com dois símbolos @ em cada lado dela, por exemplo, `@@taskid@@`.

Para lembretes, atribuições de tarefas e prazos de conclusão para usuários e grupos, é possível usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**descrição** O conteúdo da propriedade Description, conforme definido na etapa do usuário (ponto inicial, operação Atribuir tarefa ou operação Atribuir várias tarefas) do processo no Workbench.

**instruções** o conteúdo da propriedade Instruções da tarefa, conforme definido na etapa do usuário do processo no Workbench.

**notification-host** O nome do host do servidor de aplicativos de formulários AEM.

**process-name** O nome do processo.

**nome-da-operação** O nome da etapa.

**taskid** o identificador exclusivo da tarefa atual.

**actions** Produz uma lista numerada de rotas válidas (por exemplo, Aprovar, Rejeitar) em que o destinatário pode clicar.

Além disso, para lembretes de grupo, atribuições de tarefa de grupo e prazos finais de grupo, você também pode usar:

**nome-do-grupo** O nome do grupo ao qual o item de trabalho foi atribuído.

>[!NOTE]
>
>Se uma variável não tiver valor, nada será retornado.

Para ramificações interrompidas, é possível usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**branch-id** O identificador da ramificação.

**process-id** O identificador de instância do processo.

**notification-host** O nome do host do servidor de aplicativos de formulários AEM.

Para operações interrompidas, é possível usar as seguintes variáveis nas caixas Assunto e Modelo de notificação:

**action-id** O identificador da operação.

**branch-id** O identificador da ramificação.

**process-id** O identificador de instância do processo.

**notification-host** O nome do host do servidor de aplicativos de formulários AEM.

### Uso de uma variável na caixa Assunto {#using-a-variable-in-the-subject-box}

Se você digitar o seguinte texto na caixa Assunto para as notificações de Atribuição de Tarefa:

`Please complete task @@taskid@@`

O usuário receberá uma mensagem de email com o seguinte assunto se for atribuída a tarefa 376:

`Please complete task 376`

### Utilização de variáveis na caixa Modelo de notificação {#using-variables-in-the-notification-template-box}

Se você digitar o seguinte texto na caixa Modelo de Notificação para notificações de Ramificação Interrompida:

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

O administrador receberá uma mensagem de email com o seguinte conteúdo se o número da filial for 4868 e o nome do servidor for `ServerXYZ`:

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Configuração de conexões de Monitoramento de Atividades de Negócios {#configuring-business-activity-monitoring-connections}

O Business Activity Monitoring, um módulo opcional, fornece um conjunto de painéis operacionais que fornecem visibilidade em tempo real sobre suas operações e os indicadores-chave de desempenho.

Na página Definições de Configuração do BAM, você define as conexões com o servidor que executa o BAM para que os eventos relacionados ao processo possam ser rastreados e transmitidos a esse servidor.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Configurações do servidor > Configurações do BAM.
1. Na caixa Host BAM, digite o nome do servidor que executa o BAM. O padrão é localhost.
1. Na caixa Porta BAM, digite a porta a ser usada para conectar ao servidor que executa o BAM. A porta BAM padrão para JBoss é 8080, WebLogic é 7001 e WebSphere é 9080.
1. Na caixa Host do Servidor, digite o nome ou o endereço IP do Forms Server do host. O valor padrão é localhost.
1. Na caixa Porta do servidor, digite o número da porta usada pelo servidor do Forms.
1. Nas caixas Nome do usuário e Senha, digite o ID do usuário e a senha apropriados para acessar o Servidor BAM. O nome de usuário padrão é CognosNowAdmin e a senha padrão é manager.
1. Clique em Salvar.
