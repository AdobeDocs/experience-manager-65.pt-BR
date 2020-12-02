---
title: Configuração de configurações fora do escritório
seo-title: Configuração de configurações fora do escritório
description: O recurso Fora do escritório permite especificar quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM.
seo-description: O recurso Fora do escritório permite especificar quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---


# Configuração das configurações fora do escritório {#configuring-out-of-office-settings}

O recurso Fora do escritório permite que usuários ou administradores especifiquem quando um usuário estará fora do escritório e não poderá concluir tarefas atribuídas por formulários AEM. Enquanto um usuário estiver definido como Fora do escritório, suas tarefas serão atribuídas a um ou mais usuários designados. Os usuários podem alterar suas configurações de Ausência Temporária no Workspace ou os administradores podem alterar as configurações em nome de um usuário no fluxo de trabalho dos formulários.

Ao criar um processo, o usuário do Workbench pode especificar se uma tarefa pode ser redirecionada devido às configurações de Ausência Temporária.

## Visualização de informações de usuário fora do escritório {#view-a-user-s-out-of-office-information}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Fora do escritório.
1. Na caixa próxima à parte superior da página Fora do escritório, é possível fazer o seguinte:

   **Pesquisar por nome**

   Selecione a opção Pesquisar por nome. Digite todo o nome de usuário ou parte dele e clique em Localizar. Se você deixar o campo em branco, o fluxo de trabalho do Forms retornará uma lista de todos os usuários

   **Pesquisar por intervalo de datas**

   Selecione a opção Pesquisar por intervalo de datas. Especifique as datas de início e fim junto com os carimbos de data e hora desejados para restringir o resultado da pesquisa. Clique em Localizar.

1. Clique em um nome de usuário para exibir as informações de Ausência Temporária do usuário abaixo da lista de usuários.

## Alterar o status de usuário fora do escritório {#change-a-user-s-out-of-office-status}

1. Localize o usuário, conforme descrito em [Visualização de informações de usuários que não estão em escritório](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que você deseja alterar.
1. No momento, em *Nome de usuário* é lista, selecione No escritório ou Fora do escritório.
1. Clique em Salvar.

## Adicionar um intervalo de datas fora do escritório para um usuário {#add-an-out-of-office-date-range-for-a-user}

1. Localize o usuário, conforme descrito em [Visualização de informações de usuários que não estão em escritório](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Clique no nome do usuário que você deseja alterar.
1. Clique em Adicionar intervalo de datas.
1. Insira uma Hora do Start e uma Hora Final. Você pode clicar no ícone Calendário para selecionar uma data. Se você não especificar uma hora de término, o usuário será definido como fora do escritório indefinidamente.
1. Clique em Salvar.

## Atribuir um usuário para tarefas fora do escritório {#assign-a-user-for-out-of-office-tasks}

Enquanto um usuário estiver fora do escritório, você pode atribuir um ou mais usuários para executar quaisquer novas tarefas para o usuário. É possível configurar as seguintes configurações:

* Atribua todas as novas tarefas a um usuário padrão designado.
* Não reatribua nenhuma tarefa. As novas tarefas permanecem atribuídas ao usuário que está fora do escritório.
* Atribua um usuário padrão que receberá a maioria das tarefas do usuário, mas especifique se as tarefas de determinados processos serão reatribuídas a outros usuários ou permanecerão atribuídas ao usuário que estiver fora do escritório.
* Não atribua um usuário padrão, mas atribua determinadas tarefas de determinados processos a usuários específicos.

   1. Localize o usuário, conforme descrito em [Visualização de informações de usuários que não estão em escritório](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Clique no nome do usuário que você deseja alterar.
   1. Na lista Usuário padrão para Tarefas fora do Office, selecione um usuário na lista. Se você não quiser designar um usuário padrão para receber itens reatribuídos, selecione Não atribuir.

      Se o nome de usuário apropriado não for exibido na lista, clique em Localizar usuário e use a caixa de diálogo Localizar usuário para procurar o usuário. Selecione o usuário apropriado na lista e clique em Selecionar usuário. Você também pode clicar em Visualização do agendamento do usuário na caixa de diálogo Localizar usuário para ver o agendamento do usuário selecionado fora do escritório.

   1. Se houver processos que não devem ser enviados para o usuário padrão, clique em Adicionar uma exceção, selecione o processo e outro usuário da lista. Você também pode selecionar Não atribuir para que a tarefa permaneça atribuída ao usuário que está fora do escritório.
   1. Clique em Salvar.

