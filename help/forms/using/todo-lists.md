---
title: Trabalhar com listas de tarefas
seo-title: Working with To-do lists
description: Como abrir, trabalhar e concluir as tarefas conforme necessário, como aprovar ou rejeitar uma solicitação ou adicionar mais informações.
seo-description: How to open, work on, and complete the tasks as required, such as approving or rejecting a request or adding more information.
uuid: f9cfad8e-5d0c-4a30-8153-2a03bf7dd986
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d8546227-d78d-4fe2-a092-222482bb69c9
docset: aem65
exl-id: c80bf347-d1ed-488f-a41a-ceb05a6df9e4
source-git-commit: 51e36e874fe84eab8558271b5c84b1c2e2f58ef0
workflow-type: tm+mt
source-wordcount: '4034'
ht-degree: 0%

---

# Trabalhar com listas de tarefas{#working-with-to-do-lists}

Ao exibir suas listas de itens a fazer, você pode ver as tarefas de um processo de negócios atribuído a você, a quaisquer grupos aos quais você pertence ou que são tarefas compartilhadas de outros usuários. Você pode abrir, trabalhar e concluir as tarefas conforme necessário, como aprovar ou rejeitar uma solicitação ou adicionar mais informações. Após concluir uma tarefa, ela é enviada para a próxima pessoa no processo de negócios,

## Sobre listas de tarefas {#about-todo-lists}

A área de trabalho do AEM Forms tem os três tipos a seguir de listas de itens a fazer:

* Listas individuais, que contêm tarefas atribuídas diretamente a você.
* Listas de grupos, que contêm tarefas atribuídas a um grupo. Qualquer membro do grupo pode abrir e concluir as tarefas. Para abrir uma tarefa, um membro de um grupo deve reivindicar a tarefa primeiro.
* Listas compartilhadas, que contêm tarefas atribuídas a um usuário que compartilhou sua lista de Tarefas Pendentes com você e possivelmente outros usuários. Qualquer usuário que compartilhe uma lista pode reivindicar, abrir e concluir tarefas compartilhadas.

Você pode executar algumas ações sem abrir a tarefa clicando nos ícones que aparecem quando você passa o ponteiro do mouse sobre uma tarefa.

>[!NOTE]
>
>Um ícone de exclamação indica que a tarefa é de alta prioridade.

## Tarefas típicas {#typical-tasks}

Ao abrir e trabalhar em uma tarefa, as ferramentas que estão disponíveis dependem da tarefa. Tarefas diferentes exigem ações diferentes e, por isso, algumas ferramentas podem ou não estar disponíveis para você. As tarefas típicas que você pode receber são descritas abaixo.

**Fornecer informações**: Você recebe uma tarefa que requer o preenchimento e envio de um formulário.

**Revisar informações**: Você recebe uma tarefa que requer que você revise as informações e faça logoff no conteúdo.

**Revisão multiusuário**: Você recebe uma tarefa ao mesmo tempo que outros usuários recebem a tarefa. Você e os outros usuários devem fornecer informações ou revisar o conteúdo, ou ambos. As seguintes ferramentas podem estar disponíveis com esse tipo de tarefa:

* Exibir as instruções para a tarefa
* Exibindo o status de conclusão de todos os usuários que recebem a tarefa
* Exibindo os comentários de todos os usuários que recebem a tarefa
* Adicionar comentários à tarefa por conta própria

As ferramentas adicionais que podem estar disponíveis com qualquer uma das tarefas acima incluem:

* Encaminhar
* Compartilhar
* Consulta
* Retorno
* Notas
* Anexos

## Abrir tarefas {#opening-tasks}

Você pode abrir e bloquear tarefas em sua lista de Tarefas pendentes ou reivindicar e abrir tarefas em um grupo ou em uma lista de Tarefas pendentes compartilhadas. Ao abrir uma tarefa, ela é exibida no painel principal. As outras tarefas são exibidas na lista de tarefas ao lado da lista de tarefas.

Se houver um URL de Resumo de Tarefa, a exibição Resumo de Tarefa será aberta por padrão, em vez do formulário associado a uma tarefa. Mesmo quando um usuário ativa a opção &quot;Abrir o formulário no modo maximizado&quot; em Atribuir tarefa, o formulário não abre no modo maximizado.

>[!NOTE]
>
>Ao abrir uma tarefa, dependendo dos padrões da tarefa, o formulário associado pode ser exibido na visualização completa.

### Abrir e bloquear uma tarefa da lista {#open-and-lock-a-task-from-your-list}

Ao abrir uma tarefa na lista de Tarefas Pendentes, se a lista for compartilhada, é possível bloquear a tarefa para impedir que outro usuário que tenha acesso à lista funcione na tarefa.

1. Na página Tarefas a fazer, no painel esquerdo, selecione a lista de Tarefas a fazer individual. Todas as suas tarefas são exibidas no painel do meio.

   >[!NOTE]
   >
   >Você pode filtrar as tarefas selecionando o tipo de processo na lista de Tarefas. Você pode selecionar sua lista de Tarefas Pendentes para exibir todas as tarefas na lista de Tarefas Pendentes novamente.

1. Se necessário, bloqueie a tarefa. Para bloquear uma tarefa, clique no ícone Todas as opções na tarefa e selecione Bloquear. Passe o ponteiro do mouse sobre a tarefa para que a opção fique disponível.

   >[!NOTE]
   >
   >Também é possível bloquear ou desbloquear uma tarefa em qualquer guia quando a tarefa estiver aberta.

   ![lock_task](assets/lock_task.png)

   Menu Todas as opções em uma tarefa

1. Abra a tarefa clicando nela.

### Abrir e reivindicar uma tarefa de uma lista compartilhada ou de grupo {#open-and-claim-a-task-from-a-shared-or-group-list}

Quando você abre e reivindica uma tarefa de um grupo ou lista compartilhada, a tarefa é movida do grupo ou lista compartilhada para sua lista de tarefas individuais. Outros usuários com acesso à lista não podem trabalhar na tarefa.

1. Na página Tarefas pendentes, no painel esquerdo, selecione um grupo ou uma lista de Tarefas Pendentes compartilhadas. Todas as tarefas são exibidas no painel do meio.
1. Execute uma destas etapas:

   * Para reivindicar uma tarefa, sem abri-la, de um grupo ou lista de tarefas compartilhadas, clique em  **Reclamação** passando o ponteiro do mouse sobre a tarefa. Como alternativa, quando a tarefa é aberta, o botão Reivindicação está disponível na barra de ações abaixo do painel de tarefas. Ao solicitar a solicitação, uma tarefa será movida da lista de itens a fazer compartilhada para a lista.
   * Para reivindicar e abrir uma tarefa de um grupo ou de uma lista de Tarefas Pendentes compartilhadas, clique em **Reivindicação e abertura**.

## Trabalhar com tarefas {#working-with-tasks}

Depois de abrir uma tarefa, as guias que são exibidas no painel principal e as ferramentas disponíveis dependem da tarefa. As guias que podem ser exibidas são descritas abaixo:

**Resumo da tarefa**: Quando uma tarefa é aberta, o painel Resumo da tarefa permite que você mostre informações sobre a tarefa, se ela existir, usando um URL especificado no processo na etapa Atribuir tarefa . Usando o Painel de Resumo de Tarefas, informações adicionais e relevantes de uma tarefa podem ser exibidas para adicionar mais valor ao usuário final do espaço de trabalho do AEM Forms. Essa guia não estará disponível, se o URL do Resumo de tarefas não existir.

**Detalhes**: Fornece algumas informações sobre a tarefa atual e o processo ao qual ela pertence.

**Formulário**: Exibe o formulário associado à tarefa. O formulário pode ser de vários tipos de arquivos, incluindo PDF, HTML, Guia e SWF. O formulário pode ter a aparência de um formulário normal impresso ou baseado na Web ou guiá-lo por uma série de painéis no estilo de assistente para coletar informações.

**Histórico**: Lista as tarefas que fazem parte da instância do processo e o formulário, atribuições de tarefa e anexos associados para cada tarefa.

**Anexos**: Exibe anexos existentes que estão associados à tarefa e adiciona anexos, se necessário.

**Notas**: Exibe as notas existentes associadas à tarefa e adiciona notas, se necessário.

Ao trabalhar em uma tarefa, as ferramentas que você pode ver e as ações que você pode realizar são descritas abaixo.

### Encaminhar, compartilhar ou consultar uma tarefa {#forward-share-or-consult-on-a-task}

Você pode encaminhar uma tarefa junto com quaisquer notas ou anexos a outro usuário ou compartilhar a tarefa ou consultar a tarefa com outro usuário. Se você alterar os dados do formulário associados a uma tarefa, salve o formulário como rascunho antes de encaminhar, compartilhar ou consultar a tarefa. Caso contrário, a tarefa será enviada sem o formulário atualizado. Depois que você encaminhar e compartilhar uma tarefa, o usuário que recebe a tarefa poderá reivindicar e concluí-la ou retorná-la a você. Se você consultar uma tarefa, o usuário só poderá retornar a tarefa para você.

1. Se você alterar um formulário associado a uma tarefa que deseja manter, clique em **Salvar**. A opção Salvar está disponível na barra de ações na parte inferior de cada guia. Caso contrário, a tarefa será enviada sem o formulário atualizado.

   >[!NOTE]
   >
   >O botão Salvar não está disponível para alguns formulários, dependendo da tarefa em que você está trabalhando.

1. Em qualquer guia, clique em um destes botões:

   * **Encaminhar**
   * **Compartilhar**
   * **Consulta**

   >[!NOTE]
   >
   >Dependendo da tarefa, também é possível executar essas ações a partir da lista de Tarefas sem abrir a tarefa.

1. Na janela pop-up, pesquise e selecione o nome do usuário com o qual encaminhar, compartilhar ou consultar a tarefa.

### Retornar uma tarefa {#return-a-task}

1. Em qualquer guia, clique em **Retorno**. A tarefa é retornada à lista de Tarefas do usuário que anteriormente encaminhou a tarefa para você ou compartilhou ou consultou a tarefa com você.

### Fazer uma tarefa off-line {#take-a-task-offline}

Você pode trabalhar em uma tarefa offline e enviar seu formulário posteriormente do Adobe® Reader® ou Adobe® Acrobat® Professional ou Adobe® Acrobat® Standard. Quando o formulário for enviado, seu cliente de email será iniciado com o endereço de email do servidor apropriado. Em seguida, você pode enviar o formulário preenchido por email para o servidor.

1. Em qualquer guia, clique em **Offline**.
1. Especifique um nome de arquivo para salvar o formulário e clique em **Salvar**. O formulário associado à tarefa é salvo localmente e a tarefa permanece em sua lista de tarefas pendentes até que o formulário seja enviado.

### Trabalhar com anexos {#work-with-attachments}

Você pode adicionar, atualizar, excluir ou salvar anexos localmente.

**Adicionar um anexo**

1. No **Anexos** guia , clique em **Procurar** para selecionar o arquivo a ser anexado.
1. Selecione o **Permissões** nível do anexo para outros usuários que participam do processo. Se você selecionar **Ler**, outros usuários podem salvar o arquivo localmente. Se você selecionar uma das permissões de edição, outros usuários também poderão fazer upload de um novo arquivo para substituir seu anexo.

   >[!NOTE]
   >
   >Você também pode adicionar comentários ao lado dos anexos.

1. Clique em **Fazer upload**. O arquivo é anexado ao formulário.

**Exibir um anexo**

1. No **Anexos** , clique no nome do arquivo do anexo a ser exibido.

**Salvar um anexo localmente**

1. Clique em um anexo para abri-lo. Salve o anexo aberto localmente.

**Atualizar um anexo**

1. Clique em **Editar** para o anexo. Selecione o arquivo com o qual substituir o anexo existente clicando em **Procurar**.

**Excluir um anexo**

1. Clique em **Excluir** para um anexo.

### Salve seu trabalho sem concluir a tarefa {#save-your-work-without-completing-the-task}

1. Em qualquer guia, toque em **Salvar**.

   A caixa de diálogo Salvar como rascunho é exibida. O nome padrão do rascunho é o nome da tarefa do template de tarefa.

   ![saveasrascunho](assets/saveasdraftdialog.png)

   >[!NOTE]
   >
   >Você pode configurar o espaço de trabalho para salvar automaticamente periodicamente as informações inseridas por um usuário como rascunho. Se o salvamento automático estiver ativado e um usuário estiver trabalhando em um rascunho, o rascunho será salvo periodicamente. No caso de salvamento automático, o nome padrão da tarefa é automaticamente utilizado.
   >
   >
   >Para obter mais informações, consulte Salvar rascunho periodicamente em [Gerenciamento de preferências](/help/forms/using/getting-started-livecycle-html-workspace.md).

1. Na caixa de diálogo Salvar como rascunho, especifique um nome exclusivo para a tarefa e toque em **OK**.

   ![saveasrastdialog_name](assets/saveasdraftdialog_name.png)

   O rascunho é salvo com o nome especificado. A tarefa permanece na lista de Tarefas e quaisquer alterações feitas no formulário são salvas na pasta Rascunhos . Além disso, em sua lista de Tarefas pendentes, é possível pesquisar o rascunho usando o nome do rascunho para retomar o trabalho.

   ![searchfortask](assets/searchfortask.png)

## Concluir tarefas {#completing-tasks}

A forma como você conclui uma tarefa depende da própria tarefa e da sua função no processo. Você pode ser solicitado a aprovar ou negar uma solicitação, fornecer conteúdo, revisar e verificar informações ou indicar que agiu.

Você pode concluir uma tarefa de várias maneiras:

* Uso das ações disponíveis em qualquer uma das guias
* Uso das ações criadas no próprio formulário
* Na lista de Tarefas Pendentes, sem abrir a tarefa

>[!NOTE]
>
>Essa opção estará disponível se `isMustOpenToComplete` não está selecionado na variável `Assign Task` no Workbench, ao projetar um processo.

* Por email, se você receber notificações por email

Ao concluir uma tarefa, dependendo da tarefa, uma caixa de diálogo de confirmação pode aparecer reafirmando sua ação. Por exemplo, você pode ver uma caixa de diálogo que solicita que você ateste a validade das informações fornecidas.

>[!NOTE]
>
>Se você tiver alterado uma tarefa, mas não estiver pronto para concluí-la, poderá salvar seu trabalho como rascunho clicando em Salvar e retornar a ela mais tarde.

### Concluir uma tarefa {#complete-a-task}

1. Execute uma das seguintes etapas:

   * Selecione a tarefa e clique no botão apropriado para a próxima etapa necessária no processo na parte inferior da lista.
   * Se o formulário não tiver botões e o botão Concluir no espaço de trabalho do AEM Forms estiver disponível, clique em **Concluído**.
   * Se o formulário tiver botões e o botão Concluir no espaço de trabalho do AEM Forms não estiver disponível, clique no botão apropriado no formulário para a próxima etapa necessária no processo.

   Se o formulário não tiver botões e o botão Concluir no espaço de trabalho do AEM Forms não estiver disponível, será exibida uma mensagem indicando que o formulário não pode ser enviado.

1. Se uma caixa de diálogo Confirmação for exibida, execute uma destas ações:

   * Clique em **OK** se você concluiu a tarefa e estiver pronto para fazer logoff nela.
   * Clique em **Cancelar** se quiser retornar à tarefa e não estiver pronto para fazer logoff nela.

>[!NOTE]
>
>Você pode ver um botão Enviar dentro de HTML forms quando as Propriedades do processo forem usadas em um formulário. Esse botão não fica visível quando o mesmo formulário é renderizado como PDF. Para concluir uma tarefa, clique no botão Submit disponível na parte inferior do espaço de trabalho do AEM Forms, fora do formulário e não no botão Submit no formulário.

### Tarefas de aprovação em massa {#bulk-approve-tasks}

É possível enviar várias tarefas da sua lista de Tarefas. Somente tarefas do mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de rota podem ser enviadas juntas.

>[!NOTE]
>
>Essa opção estará disponível se o campo ismustOpenToComplete não estiver selecionado na etapa Atribuir tarefa no Workbench, ao projetar um processo.

1. Na página Tarefas a fazer, no painel esquerdo, selecione a lista de Tarefas a fazer individual. Todas as suas tarefas são exibidas no painel do meio.
1. Selecionar **Ativar modo em massa**. Caixas de seleção são exibidas na frente das tarefas na lista.

   >[!NOTE]
   >
   >Essa opção não está disponível para tarefas para as quais o campo ismustOpenToComplete está selecionado na etapa Atribuir tarefa no Workbench, ao projetar um processo. As caixas de seleção de tais tarefas na lista TO-DO permanecem sempre desativadas.

1. Selecione tarefas para aprovação em massa. Várias tarefas do mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de rota podem ser selecionadas. Depois de selecionar uma tarefa para aprovação, somente as tarefas com o mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de rota permanecerão ativadas. O restante está desativado.

   ![1_bulkapproval](assets/1_bulkapproval.png)

1. Clique na opção Enviar disponível. As tarefas selecionadas são enviadas.

   ![bulkapproval](assets/bulkapproval.png)

## Participar de tarefas por email {#participating-in-tasks-through-email}

Você pode receber e concluir tarefas por email. Participar de tarefas por meio de emails elimina a necessidade de verificar regularmente sua lista de tarefas a serem feitas em busca de novas tarefas ou verificar na página Rastreamento o status de uma tarefa.

Primeiro, defina as preferências do espaço de trabalho do AEM Forms para receber notificações por email. O espaço de trabalho do AEM Forms pode enviar notificações por email para tarefas em sua lista de tarefas ou em qualquer lista de tarefas do grupo à qual você pertence. O administrador determina quando as mensagens de notificação por email são enviadas e quem as recebe.

As mensagens de email podem conter um link que abre a tarefa no espaço de trabalho do AEM Forms, um anexo do formulário usado para a tarefa ou ações para concluir a tarefa por email. Se um formulário for incluído na mensagem de email, você poderá abrir o formulário e concluir a tarefa se os botões para concluir a tarefa forem criados no formulário. Se as ações para concluir a tarefa forem incluídas na mensagem de email, você poderá concluir a tarefa clicando nas ações no email ou respondendo ao email com a ação digitada como a primeira linha no corpo do email.

>[!NOTE]
>
>* Para configurar o espaço de trabalho para usar os modelos de email apropriados, consulte o [Guia do administrador do AEM Forms JEE](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/).
>
>* Se os rascunhos forem encaminhados após o envio da tarefa no espaço de trabalho do AEM Forms, as notificações por email serão enviadas. Se os rascunhos forem encaminhados do ponto de partida do espaço de trabalho do AEM Forms, nenhuma notificação por email será enviada.


Ao concluir uma tarefa por email, a tarefa é removida da lista de Tarefas no espaço de trabalho do AEM Forms.

>[!NOTE]
>
>Se o usuário não estiver conectado no espaço de trabalho do AEM Forms no navegador e abrir um link para uma tarefa do tipo &quot;Fazer&quot;, o link direto para fazer não será aberto e exibirá uma exceção. Faça logon no espaço de trabalho do AEM Forms antes de clicar em links nos emails.

>[!NOTE]
>
>Não é possível encaminhar uma notificação por email para atribuir uma tarefa a outra pessoa. Você só pode encaminhar tarefas para outros usuários a partir do espaço de trabalho do AEM Forms.

### Receber mensagens de notificação por email {#receive-email-notification-messages}

1. Clique em **Preferências**.
1. No **Notificar eventos de tarefa por email** lista, selecione **Sim**.
1. Para incluir o formulário e os dados com a mensagem de email, no **Anexar o Forms no email** lista, selecione **Sim**.

## Participar em tarefas por meio de dispositivos móveis {#participating-in-tasks-through-mobile-devices}

Você pode usar o aplicativo AEM Forms workspace para participar de tarefas do seu dispositivo móvel. Antes de instalar o aplicativo, verifique com o administrador do sistema para garantir que sua organização suporte o uso do aplicativo AEM Forms workspace.

## Sobre prazos e lembretes {#about-deadlines-and-reminders}

A *prazo* determina a data e a hora em que você deve concluir uma tarefa. Quando um prazo passa, o servidor roteia a tarefa para a próxima etapa do processo (que pode ser a lista de itens a fazer de outro usuário) e, em seguida, o ícone de prazo aparece na tarefa. O ícone de prazo aparece independentemente das regras associadas ao processo.

A *lembrete* O notifica você sobre uma tarefa que requer sua atenção. Os lembretes ocorrem em um horário predeterminado e em intervalos regulares até que você conclua a tarefa associada. Ao receber um lembrete, o ícone de lembrete aparece na tarefa.

O processo de negócios determina o comportamento e o momento dos prazos e lembretes. Nem todos os processos têm prazos e lembretes. O administrador especifica se as notificações por email são enviadas para prazos e lembretes. Você pode definir suas preferências para receber notificações por email.

## Trabalhar com tarefas de grupos e filas compartilhadas {#working-with-tasks-from-group-and-shared-queues}

Todas as tarefas atribuídas a você aparecem na lista de Tarefas pendentes (fila).

Qualquer lista de itens a fazer compartilhada e de grupos que você tenha acesso também será exibida no painel esquerdo da página de itens a fazer. Você pode concluir tarefas de qualquer lista de tarefas pendentes à qual tenha acesso.

Uma lista de itens a fazer do grupo pode ter mais de um membro. Um administrador configura listas de itens a fazer do grupo com base nos requisitos específicos de sua organização. As listas de tarefas do grupo fornecem uma maneira de distribuir trabalho entre várias pessoas que compartilham responsabilidades semelhantes.

Por exemplo, cada membro da equipe processa formulários de solicitação de empréstimo. Todas essas tarefas são enviadas para uma lista de tarefas do grupo a que cada membro do seu grupo tem acesso. Cada membro do seu grupo pode acessar as tarefas a partir dessa lista de tarefas.

Uma lista de Tarefas Pendentes compartilhada é exibida quando outro usuário compartilha sua lista de Tarefas Pendentes com você ou compartilha uma tarefa explicitamente com você. Em seguida, você pode exibir as tarefas na lista de Tarefas Pendentes desse usuário e preenchê-las em seu nome. Por exemplo, se você estiver tirando férias, pode optar por compartilhar sua lista de tarefas pendentes com um colega que conclui as tarefas enquanto está ausente.

>[!NOTE]
>
>Você também pode especificar configurações de ausência do escritório para encaminhar tarefas para outros usuários enquanto estiver ausente.

Para trabalhar em uma tarefa de um grupo ou de uma lista de Tarefas Pendentes compartilhadas, reivindique a tarefa primeiro. Em seguida, você se torna o proprietário da tarefa até concluí-la ou encaminhá-la para outro usuário.

### Compartilhamento de filas {#sharing-queues}

Você pode compartilhar sua lista de Tarefas pendentes com outro usuário, que pode exibir as novas tarefas na lista de Tarefas pendentes e agir de acordo com elas para você. Se houver alguma tarefa na lista de Tarefas pendentes antes de compartilhar a lista de Tarefas, o outro usuário não poderá visualizá-las. O usuário pode visualizar e reivindicar apenas as tarefas que chegam à lista de Tarefas após conceder acesso à lista de Tarefas Pendentes.

Lembre-se de que para um usuário ver uma tarefa em uma fila compartilhada, o designer do processo deve habilitar a opção Adicionar ACL para fila compartilhada na guia Lista de Controle de Acesso à Tarefa (ACL) do Serviço de Usuário.

>[!NOTE]
>
>Se você planeja estar longe do escritório, também pode especificar configurações de ausência do escritório para encaminhar tarefas para outros usuários enquanto estiver fora, em vez de compartilhar toda a lista de itens a fazer.

**Compartilhar sua fila**

1. No **Filas** na guia no **Preferências** , clique no ícone &quot;+&quot; para &quot;Usuários que estão compartilhando minha fila no momento&quot;.
1. Pesquise e selecione o nome do usuário.
1. Clique em **Compartilhar** , para compartilhar sua Fila com o usuário selecionado.
1. Selecione o nome do usuário e clique em **Compartilhar**.

   >[!NOTE]
   >
   >Você pode remover um usuário de compartilhar sua lista de tarefas pendentes clicando em **X** no final da linha na qual o usuário está listado.

### Acessar outras filas {#accessing-other-queues}

Você pode solicitar acesso à lista de Tarefas Pendentes de outro usuário para visualizar e reivindicar quaisquer novas tarefas na lista de Tarefas Pendentes do usuário.

Quando você solicita acesso à lista de Tarefas Pendentes de outro usuário, o usuário recebe uma tarefa em sua lista de Tarefas Pendentes para aprovar ou negar sua solicitação. Depois que o usuário concluir a tarefa, você receberá uma notificação em sua lista de Tarefas.

Se você tiver acesso à lista de Tarefas Pendentes de outro usuário, não será possível visualizar as tarefas existentes na lista de Tarefas Pendentes do usuário antes de ter acesso a ela. Você pode exibir somente as tarefas que chegam na lista de Tarefas Pendentes do usuário depois de ter acesso à lista de Tarefas Pendentes.

**Acessar outra fila**

1. No **Preferências** , abra o **Filas** guia .
1. Clique em &quot;+&quot; para as &quot;filas de usuários às quais tenho acesso&quot;. Procure pelo nome do usuário na caixa de diálogo pop-up.
1. Selecione o nome do usuário e clique em **Solicitação**.

   >[!NOTE]
   >
   >Você pode remover seu acesso a outra lista de Tarefas Pendentes selecionando o nome de usuário nas Filas de Usuários às quais tenho Acesso e clicando em **X** no final da linha que menciona o nome do usuário. Não é possível remover seu acesso a outra lista de itens a fazer quando a solicitação para acessar a lista de itens a fazer ainda estiver pendente.

## Configuração de preferências fora do escritório {#setting-out-of-office-preferences}

Se você planeja estar fora do escritório, você pode especificar o que acontece com as tarefas atribuídas a você para esse período.

Você tem a opção de especificar uma data e hora de início e uma data e hora de término para que as configurações de ausência do escritório entrem em vigor. Se você estiver localizado em um fuso horário diferente do servidor, o fuso horário usado será o do servidor.

Você pode definir uma pessoa padrão para a qual todas as suas tarefas são enviadas. Você também pode especificar exceções para tarefas de processos específicos a serem enviadas para um usuário diferente ou para permanecer em sua lista de tarefas pendentes até que você retorne. Se a pessoa designada também estiver fora do escritório, a tarefa vai para o usuário que ela designou. Se a tarefa não puder ser atribuída a um usuário que não esteja fora do escritório, a tarefa permanecerá na lista de Tarefas.

>[!NOTE]
>
>Quando você estiver fora do escritório, todas as tarefas que anteriormente estavam em sua lista de Tarefas pendentes permanecerão lá e não serão encaminhadas a outros usuários.

### Definir preferências fora do escritório {#set-out-of-office-preferences}

1. Clique em **Preferências** e clique em **Fora do Escritório**.
1. Para especificar quando você está fora do escritório, execute uma destas etapas:

   * Para especificar que você está fora do escritório agora por um período de tempo indefinido, no **Atualmente** lista, selecione **Fora do escritório** mas não adicione um intervalo de datas.
   * Para especificar a data e hora de início em que você está fora do escritório e clique em &#39;+&#39; para **Fora do Escritório**. Use o calendário e a lista de horas para especificar a data e a hora de início. Se você não especificar uma data e hora de término, você será considerado fora do escritório indefinidamente a partir da data e hora de início até que suas preferências sejam alteradas.

1. Para especificar como suas tarefas devem ser manipuladas por padrão, selecione uma dessas opções no **Quando Fora do Escritório: Usuário padrão para tarefas fora do escritório** lista:

   * Selecionar **Não atribuir** para manter as tarefas na lista de Tarefas pendentes até que você retorne.
   * Selecionar **Localizar usuário** para procurar um usuário para atribuir suas tarefas. Ao selecionar um usuário, você também pode exibir seu agendamento de ausência do escritório.

1. Para definir exceções para o padrão, clique em + para **Exceções de Processo**, selecione o processo para criar uma exceção e, em seguida, selecione um usuário diferente ou selecione **Não atribuir** do **está atribuído a** lista.

   >[!NOTE]
   >
   >O designer de processo pode especificar que as tarefas de alguns processos sejam sempre mantidas privadas e não encaminhadas para outros usuários. Essa configuração substitui todas as configurações feitas.

1. Quando terminar de definir preferências, clique em **Salvar**. Se as configurações indicarem que você está fora do escritório, suas alterações entrarão em vigor imediatamente. Caso contrário, entrarão em vigor na data e hora de início especificadas. Se você fizer logon enquanto estiver fora do escritório, não será considerado no escritório até que você altere suas configurações.
