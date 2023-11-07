---
title: Definindo Configurações de Ausência Temporária
description: O recurso Out of Office permite especificar quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Definindo Configurações de Ausência Temporária {#configuring-out-of-office-settings}

O recurso Out of Office permite que os usuários ou administradores especifiquem quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM. Embora um usuário esteja definido como Fora do escritório, suas tarefas são atribuídas a um ou mais usuários designados. Os usuários podem alterar as configurações de Ausência Temporária no Workspace ou os administradores podem alterar as configurações em nome de um usuário no fluxo de trabalho de formulários.

Ao criar um processo, o usuário do Workbench pode especificar se uma tarefa pode ser redirecionada devido às configurações de Ausência temporária.

## Exibir as informações de Ausência Temporária de um usuário {#view-a-user-s-out-of-office-information}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Ausência temporária.
1. Na caixa próxima à parte superior da página Ausência Temporária, você pode executar um dos seguintes procedimentos:

   **Pesquisar por nome**

   Selecione a opção Pesquisar por nome. Digite todo ou parte do nome de usuário e clique em Localizar. Se você deixar o campo em branco, o workflow do Forms retornará uma lista de todos os usuários.

   **Pesquisar por intervalo de datas**

   Selecione a opção Pesquisar por intervalo de datas. Especifique as datas de e até juntamente com os carimbos de data e hora desejados para limitar o resultado da pesquisa. Clique em Localizar.

1. Clique em um nome de usuário para exibir as informações de Ausência Temporária do usuário abaixo da lista de usuários.

## Alterar o status de ausência temporária de um usuário {#change-a-user-s-out-of-office-status}

1. Localize o usuário, conforme descrito em [Exibir as informações de Ausência Temporária de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que deseja alterar.
1. No *Nome do usuário* estiver listada no momento, selecione No escritório ou Fora do escritório.
1. Clique em Salvar.

## Adicionar um intervalo de datas de Ausência Temporária para um usuário {#add-an-out-of-office-date-range-for-a-user}

1. Localize o usuário, conforme descrito em [Exibir as informações de Ausência Temporária de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que deseja alterar.
1. Clique em Adicionar intervalo de datas.
1. Informe uma Hora Inicial e uma Hora Final. Você pode clicar no ícone Calendário para selecionar uma data. Se você não especificar uma hora de término, o usuário será definido como ausente indefinidamente.
1. Clique em Salvar.

## Atribuir um usuário para tarefas de Ausência Temporária {#assign-a-user-for-out-of-office-tasks}

Enquanto um usuário estiver fora do escritório, você poderá atribuir um ou mais usuários para executar novas tarefas para ele. Você pode definir as seguintes configurações:

* Atribuir todas as novas tarefas a um usuário padrão designado.
* Não reatribua nenhuma tarefa. Novas tarefas permanecem atribuídas ao usuário que está fora do escritório.
* Atribua um usuário padrão que receberá a maioria das tarefas do usuário, mas especifique que as tarefas de determinados processos sejam reatribuídas a outros usuários ou permaneçam atribuídas ao usuário que está fora do escritório.
* Não atribua um usuário padrão, mas atribua determinadas tarefas de determinados processos a usuários específicos.

   1. Localize o usuário, conforme descrito em [Exibir as informações de Ausência Temporária de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Clique no nome do usuário que deseja alterar.
   1. Na lista Usuário Padrão para Tarefas de Ausência Temporária, selecione um usuário na lista. Se você não quiser designar um usuário padrão para receber itens reatribuídos, selecione Não atribuir.

      Se o nome de usuário apropriado não for exibido na lista, clique em Localizar usuário e use a caixa de diálogo Localizar usuário para procurar o usuário. Selecione o usuário apropriado na lista e clique em Selecionar usuário. Você também pode clicar em Exibir Cronograma do Usuário na caixa de diálogo Localizar Usuário para ver o cronograma de ausência do usuário selecionado.

   1. Se houver processos que não devem ser enviados ao usuário padrão, clique em Adicionar uma exceção, selecione o processo e selecione outro usuário na lista. Você também pode selecionar Não atribuir para que a tarefa permaneça atribuída ao usuário que está fora do escritório.
   1. Clique em Salvar.
