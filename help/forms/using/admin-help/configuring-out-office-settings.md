---
title: Configuração das configurações fora do escritório
seo-title: Configuring Out of Office Settings
description: O recurso Esgotado permite especificar quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM.
seo-description: The Out of Office feature enables you to specify when a user will be out of the office and unable to complete tasks assigned by AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Configuração das configurações fora do escritório {#configuring-out-of-office-settings}

O recurso Esgotado permite que usuários ou administradores especifiquem quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM. Embora um usuário esteja definido como Ausente, suas tarefas são atribuídas a um ou mais usuários designados. Os usuários podem alterar suas configurações de Ausência Temporária no Workspace ou os administradores podem alterar as configurações em nome de um usuário no fluxo de trabalho de formulários.

Ao criar um processo, o usuário do Workbench pode especificar se uma tarefa pode ser redirecionada devido às configurações de Ausência Temporária.

## Exibir as informações de ausência do escritório de um usuário {#view-a-user-s-out-of-office-information}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Fora do escritório.
1. Na caixa próxima à parte superior da página Ausente, é possível executar um dos seguintes procedimentos:

   **Pesquisar por nome**

   Selecione a opção Pesquisar por nome . Digite todo o nome de usuário ou parte dele e clique em Localizar. Se você deixar o campo em branco, o workflow do Forms retornará uma lista de todos os usuários

   **Pesquisar por intervalo de datas**

   Selecione a opção Pesquisar por intervalo de datas . Especifique as datas de início e fim junto com os carimbos de data e hora desejados para limitar o resultado da pesquisa. Clique em Localizar.

1. Clique em um nome de usuário para exibir as informações de ausência do escritório do usuário abaixo da lista de usuários.

## Alterar o status de ausência do escritório de um usuário {#change-a-user-s-out-of-office-status}

1. Encontre o usuário, conforme descrito em [Exibir as informações de ausência do escritório de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que deseja alterar.
1. No *Nome do usuário* estiver na lista, selecione No Escritório ou Fora do Escritório.
1. Clique em Salvar.

## Adicionar um intervalo de datas Ausente para um usuário {#add-an-out-of-office-date-range-for-a-user}

1. Encontre o usuário, conforme descrito em [Exibir as informações de ausência do escritório de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que deseja alterar.
1. Clique em Adicionar intervalo de datas.
1. Informe a Hora Inicial e a Hora Final. Você pode clicar no ícone Calendário para selecionar uma data. Se você não especificar uma hora de término, o usuário será definido como fora do escritório indefinidamente.
1. Clique em Salvar.

## Atribuir um usuário para tarefas fora do escritório {#assign-a-user-for-out-of-office-tasks}

Embora um usuário esteja fora do escritório, é possível atribuir um ou mais usuários para realizar novas tarefas para o usuário. Você pode configurar as seguintes configurações:

* Atribua todas as novas tarefas a um usuário padrão designado.
* Não reatribua nenhuma tarefa. Novas tarefas permanecem atribuídas ao usuário que está fora do escritório.
* Atribua um usuário padrão que receberá a maioria das tarefas do usuário, mas especifique que as tarefas de determinados processos são reatribuídas a outros usuários ou permanecem atribuídas ao usuário que está fora do escritório.
* Não atribua um usuário padrão, mas atribua determinadas tarefas de determinados processos a usuários específicos.

   1. Encontre o usuário, conforme descrito em [Exibir as informações de ausência do escritório de um usuário](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Clique no nome do usuário que deseja alterar.
   1. Na lista Usuário padrão para tarefas fora do escritório, selecione um usuário na lista. Se não quiser designar um usuário padrão para receber itens reatribuídos, selecione Não atribuir.

      Se o nome de usuário apropriado não for exibido na lista, clique em Localizar usuário e use a caixa de diálogo Localizar usuário para procurar o usuário. Selecione o usuário apropriado na lista e clique em Selecionar usuário. Você também pode clicar em Exibir o agendamento do usuário na caixa de diálogo Localizar usuário para ver o agendamento de ausência do escritório do usuário selecionado.

   1. Se houver processos que não devem ser enviados ao usuário padrão, clique em Adicionar uma Exceção e selecione o processo e outro usuário na lista. Você também pode selecionar Não atribuir para que a tarefa permaneça atribuída ao usuário que está fora do escritório.
   1. Clique em Salvar.
