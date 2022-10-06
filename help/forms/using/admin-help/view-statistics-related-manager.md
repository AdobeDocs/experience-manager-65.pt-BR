---
title: Exibir estatísticas relacionadas ao Gerenciador de Trabalho
seo-title: View statistics related to Work Manager
description: A guia Gerenciador de Trabalho exibe estatísticas relacionadas aos itens do Gerenciador de Trabalho. Saiba como visualizar e filtrar os itens de trabalho.
seo-description: The Work Manager tab displays statistics that relate to Work Manager items. Learn how you can view and filter the work items.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 0%

---

# Exibir estatísticas relacionadas ao Gerenciador de Trabalho {#view-statistics-related-to-work-manager}

A guia Gerenciador de Trabalho exibe estatísticas relacionadas aos itens do Gerenciador de Trabalho. Esses itens de trabalho estão em estados diferentes, dependendo de onde estão em seu processo. (Consulte [Status (somente para categorias Padrão, Fluxo de trabalho ou Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Você pode filtrar as informações para exibir apenas um subconjunto dos itens usando as várias opções disponíveis (por exemplo, Status ou Categoria). Você pode classificar os trabalhos ou itens de trabalho resultantes (em ordem crescente ou decrescente) clicando em um dos cabeçalhos da coluna. Além disso, é possível gerenciar os itens de trabalho usando as ferramentas de operação exibidas acima da lista de itens de trabalho.

## Filtrar os itens de trabalho {#filter-the-work-items}

1. Clique na guia Gerenciador de trabalho .
1. Selecione os critérios para um ou mais filtros descritos abaixo e clique em Ir.

### Categoria {#category}

**Padrão:** Todos os itens de trabalho aos quais o cliente não atribuiu uma categoria quando foram submetidos. O Gerenciador de trabalho gerencia esses itens, portanto, os status pertencem ao Gerenciador de trabalho.

**Gerenciador de tarefas:** Todas as tarefas que pertencem ao Gerenciador de Tarefas. O Gerenciador de Jobs gerencia seus próprios trabalhos e tem seus próprios status de trabalho. Consulte os status específicos da tarefa descritos abaixo.

**Fluxo de trabalho:** Todos os itens de trabalho que pertencem à execução do Workflow. O fluxo de trabalho não gerencia seus próprios itens de trabalho, mas depende do Gerenciador de Trabalho; portanto, os status pertencem ao Gerenciador de trabalho.

**Eventos:** Todos os itens de trabalho que pertencem ao Gerenciamento de eventos. A Gestão de Eventos não gere os seus próprios itens de trabalho, mas depende do Gestor de Trabalho; portanto, os status pertencem ao Gerenciador de trabalho.

### Status (somente para categorias Padrão, Fluxo de trabalho ou Eventos) {#status-for-default-workflow-or-events-categories-only}

**Mostrar tudo:** Exibe todos os itens de trabalho atuais.

**Programado:** Exibe todos os itens de trabalho prontos para execução pelo servidor de aplicativos, mas ainda não iniciados.

**Em pausa:** Exibe todos os itens de trabalho agendados que o aplicativo cliente pausou. Esses itens podem ser executados ou excluídos. (Consulte Gerenciar itens de trabalho ou tarefas.)

**Em Andamento:** Exibe todos os itens de trabalho que o Gerenciador de Trabalho do servidor de aplicativos selecionou e concluirá ou falhará. Não é possível usar operações nesses itens de trabalho.

**Concluído:** Exibe todos os itens de trabalho que foram executados com êxito. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada. Você pode excluir esses itens usando a operação Excluir itens. (Consulte Gerenciar itens de trabalho ou tarefas.)

**Falha:** Exibe todos os itens de trabalho que não foram concluídos com êxito devido a uma condição de erro. Estes itens de trabalho podem ser repetidos algumas vezes usando a operação Itens de Repetição. (Consulte Gerenciar itens de trabalho ou tarefas.) Um link Failure na coluna Status permite acessar os detalhes sobre a falha.

**Desconhecido:** Exibe todos os itens de trabalho cujo status é desconhecido.

### Status (somente para a categoria Gerenciador de Tarefas) {#status-for-job-manager-category-only}

**Concluído:** Exibe todas as tarefas que foram executadas com êxito. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada.

**Concluído Solicitado:** Exibe tarefas para as quais uma solicitação concluída foi feita.

**Falha solicitada:** Exibe tarefas para as quais uma solicitação de falha foi feita.

**Falha:** Exibe trabalhos que não foram concluídos com êxito devido a uma condição de erro. Um link Failure na coluna Status permite acessar os detalhes sobre a falha.

**Encerrar Solicitado:** Exibe tarefas para as quais uma solicitação de término foi feita.

**Terminado:** Exibe tarefas que foram encerradas sem concluir.

**Suspender Solicitado:** Exibe tarefas para as quais uma solicitação de suspensão foi feita.

**Suspenso:** Exibe tarefas que são suspensas.

**Retomar Solicitado:** Exibe tarefas para as quais uma solicitação de retomada foi feita.

**Em fila:** Exibe tarefas que estão na fila.

**Em execução:** Exibe tarefas que estão sendo executadas.

### Nome do servidor {#server-name}

Somente para servidores em cluster, selecione o nome do nó para exibir os itens de trabalho ou itens de trabalho que foram criados apenas nesse servidor. Se a opção Mostrar tudo estiver selecionada, todos os itens de trabalho para todos os nós em um cluster serão exibidos.

### Criar horário {#create-time}

Selecione uma opção neste filtro para mostrar apenas os itens de trabalho que foram criados dentro do período de tempo selecionado. Por exemplo, selecionar 1 dia exibe todos os itens de trabalho que foram criados dentro de 24 horas antes do tempo definido no filtro Antes de .

### Antes de {#prior-to}

Define a data e a hora que o filtro Criar hora usa como data final. Mantenha a opção Usar data e hora atuais selecionada para filtrar de volta da data e hora atuais, ou desmarque a opção e insira os valores apropriados. Clique nos ícones do calendário ou do relógio para selecionar valores usando essas ferramentas.

Por exemplo, selecionar Criar horário = 1 dia e Antes de = Usar data atual e hora retorna todos os itens de trabalho que foram criados nas últimas 24 horas.

>[!NOTE]
>
>Nas implantações do banco de dados do Oracle, os filtros de intervalo de datas (ou seja, Criar hora e Antes das configurações) não funcionam com precisão. Use outro filtro para recuperar itens de trabalho.

## Sobre a interface da guia Gerenciador de trabalho {#about-the-work-manager-tab-interface}

Quando você executa uma consulta do Gerenciador de Trabalho ou realiza uma operação em um item de trabalho ou tarefa, uma mensagem é exibida acima da lista. Esta mensagem fornece feedback sobre a ação iniciada e, em alguns casos, um link Mais informações para fornecer detalhes. Por exemplo, se a operação iniciada falhar, a mensagem afirmará o mesmo e fornecerá um link para obter detalhes sobre o erro.

Quando você clica em Mais Informações, a caixa de diálogo Detalhes da Operação exibe uma lista dos itens de trabalho ou tarefas que foram selecionados durante a operação. Você pode clicar em cada item da lista para exibir os Detalhes do erro na parte inferior da caixa de diálogo.

### Gerenciar itens de trabalho ou trabalhos {#manage-the-work-items-or-jobs}

1. Use as ferramentas de operação descritas abaixo para gerenciar os itens de trabalho ou tarefas na lista.

   >[!NOTE]
   >
   >As operações estão disponíveis dependendo do status do item.

   **Excluir itens:** Exclui o item de trabalho ou tarefa selecionado.

   **Pausar itens:** Pausa o item de trabalho ou tarefa selecionado.

   **Retomar itens:** Retoma o item de trabalho ou tarefa selecionado do seu estado pausado.

   **Itens de Tentativa:** Tenta executar novamente o item de trabalho ou tarefa selecionado a partir do seu estado atual.

   Você pode verificar se uma operação foi bem-sucedida clicando em Mais informações acima da lista. Uma caixa de diálogo que contém os itens de trabalho ou tarefas selecionados e seus status é exibida.

## Informações adicionais sobre status de itens de trabalho {#additional-information-about-work-item-statuses}

Uma transição de estado típica para um item de trabalho é New > Scheduled > In Progress > Complete ou Failure.

O estado Pausado interrompe esse fluxo normal. O aplicativo cliente ou o administrador do sistema podem iniciar essa interrupção (por exemplo, para manutenção ou atualização). É possível reverter essa ação usando a operação Retomar para mover o item de trabalho de volta para um estado Programado.

Um item de trabalho em um estado Agendado está na fila para execução que ainda não começou. Esses itens podem ser pausados ou excluídos ou serão movidos para o estado Em andamento quando o Gerenciador de trabalho os retirar da fila. Itens de trabalho em andamento não podem ser modificados. Eles serão concluídos ou falharão.

O estado Failed ocorre como resultado de uma condição de erro que ocorre durante a execução do item de trabalho. Se você suspeitar que os erros sejam circunstanciais (devido ao contexto no momento da execução), poderá tentar novamente a execução, colocando o item de trabalho de volta na fila. Apenas um número limitado de tentativas é permitido.
