---
title: Estatísticas de visualização relacionadas ao Gerenciador de Trabalho
seo-title: Estatísticas de visualização relacionadas ao Gerenciador de Trabalho
description: A guia Gerenciador de trabalho exibe estatísticas relacionadas aos itens do Gerenciador de trabalho. Saiba como você pode visualização e filtrar os itens de trabalho.
seo-description: A guia Gerenciador de trabalho exibe estatísticas relacionadas aos itens do Gerenciador de trabalho. Saiba como você pode visualização e filtrar os itens de trabalho.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---


# Estatísticas de visualização relacionadas ao Gerenciador de Trabalho {#view-statistics-related-to-work-manager}

A guia Gerenciador de trabalho exibe estatísticas relacionadas aos itens do Gerenciador de trabalho. Esses itens de trabalho estão em estados diferentes dependendo de onde estão em seu processo. (Consulte [Status (somente para categorias padrão, fluxo de trabalho ou Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Você pode filtrar as informações para visualização somente em um subconjunto dos itens usando as várias opções disponíveis (por exemplo, Status ou Categoria). Você pode classificar os itens de trabalho ou de cargo resultantes (em ordem crescente ou decrescente) clicando em um dos cabeçalhos da coluna. Além disso, você pode gerenciar os itens de trabalho usando as ferramentas de operação exibidas acima da lista de itens de trabalho.

## Filtrar os itens de trabalho {#filter-the-work-items}

1. Clique na guia Gerente de trabalho.
1. Selecione os critérios para um ou mais dos filtros descritos abaixo e clique em Ir.

### Categoria {#category}

**Padrão:** Todos os itens de trabalho aos quais o cliente não atribuiu uma categoria quando foram submetidos. O Gerenciador de trabalho gerencia esses itens, portanto, os status pertencem ao Gerenciador de trabalho.

**Gerenciador de tarefas:** todos os trabalhos que pertencem ao Gerenciador de tarefas. O Gerenciador de Jobs gerencia seus próprios jobs e tem seus próprios status. Consulte os status específicos da ordem de produção descritos abaixo.

**Fluxo de trabalho:** todos os itens de trabalho que pertencem à execução do Fluxo de trabalho. O fluxo de trabalho não gerencia seus próprios itens de trabalho, mas depende do Gerente de Trabalho; portanto, os status pertencem ao Gerente de trabalho.

**Eventos:** Todos os itens de trabalho que pertencem ao Gerenciamento de Eventos. A gestão de eventos não gere os seus próprios itens de trabalho, mas depende do gestor de trabalho; portanto, os status pertencem ao Gerente de trabalho.

### Status (somente para categorias padrão, de fluxo de trabalho ou de Eventos) {#status-for-default-workflow-or-events-categories-only}

**Mostrar tudo:** Exibe todos os itens de trabalho atuais.

**Agendado:** exibe todos os itens de trabalho prontos para execução pelo servidor de aplicativos, mas ainda não iniciados.

**Pausado:** Exibe todos os itens de trabalho programados que o aplicativo cliente pausou. Esses itens podem ser executados ou excluídos. (Consulte Gerenciar itens de trabalho ou trabalhos.)

**Em andamento:** exibe todos os itens de trabalho que o Gerente de trabalho do servidor de aplicativos selecionou e que serão concluídos ou reprovados. Não é possível usar operações nesses itens de trabalho.

**Concluído:** exibe todos os itens de trabalho que foram executados com êxito. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada. Você pode excluir esses itens usando a operação Excluir itens. (Consulte Gerenciar itens de trabalho ou trabalhos.)

**Falha:** exibe todos os itens de trabalho que não foram concluídos com êxito devido a uma condição de erro. Estes itens de trabalho podem ser repetidos algumas vezes usando a operação Repetir itens. (Consulte Gerenciar itens de trabalho ou trabalhos.) Um link Falha na coluna Status permite acessar detalhes sobre a falha.

**Desconhecido:** Exibe todos os itens de trabalho cujo status é desconhecido.

### Status (somente para categoria do Gerenciador de Jobs) {#status-for-job-manager-category-only}

**Concluído:** Exibe todos os trabalhos que foram executados com êxito. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada.

**Concluir Solicitado:** Exibe trabalhos para os quais foi feita uma solicitação completa.

**Falha solicitada:** exibe trabalhos para os quais uma solicitação de falha foi feita.

**Falha:** exibe trabalhos que não foram concluídos com êxito devido a uma condição de erro. Um link Falha na coluna Status permite acessar detalhes sobre a falha.

**Terminar Solicitado:** Exibe trabalhos para os quais uma solicitação de término foi feita.

**Terminado:** Exibe trabalhos que foram encerrados sem conclusão.

**Suspender Solicitado:** Exibe trabalhos para os quais uma solicitação de suspensão foi feita.

**Suspenso:** Exibe trabalhos que estão suspensos.

**Retomar Solicitado:** Exibe trabalhos para os quais uma solicitação de retomada foi feita.

**Em fila:** Exibe trabalhos que estão na fila.

**Execução:** Exibe trabalhos que estão sendo executados.

### Nome do servidor {#server-name}

Somente para servidores clusterizados, selecione o nome do nó para exibir os itens de trabalho ou itens de trabalho criados apenas nesse servidor. Se a opção Mostrar tudo estiver selecionada, todos os itens de trabalho para todos os nós em um cluster serão exibidos.

### Criar hora {#create-time}

Selecione uma opção neste filtro para mostrar apenas os itens de trabalho que foram criados dentro do período de tempo selecionado. Por exemplo, selecionar 1 dia exibe todos os itens de trabalho criados dentro de 24 horas antes do horário definido no filtro Antes.

### Antes de {#prior-to}

Define a data e a hora que o filtro Criar hora usa como data final. Mantenha a opção Usar data e hora atuais selecionada para filtrar de volta da data e hora atuais, ou desmarque a opção e insira os valores apropriados. Clique nos ícones do calendário ou do relógio para selecionar valores usando essas ferramentas.

Por exemplo, selecionar Criar hora = 1 dia e Anterior a = Usar data e hora atuais retorna todos os itens de trabalho que foram criados nas últimas 24 horas.

>[!NOTE]
>
>Nas implantações de banco de dados Oracle, os filtros de intervalo de datas (ou seja, Criar tempo e Antes das configurações) não funcionam corretamente. Use outro filtro para recuperar itens de trabalho.

## Sobre a interface da guia do Gerenciador de Trabalho {#about-the-work-manager-tab-interface}

Quando você executa um query do Gerenciador de trabalho ou executa uma operação em um item de trabalho ou tarefa, uma mensagem é exibida acima da lista. Esta mensagem fornece feedback sobre a ação iniciada e, em alguns casos, um link Mais informações para fornecer detalhes. Por exemplo, se a operação que você iniciou falhou, a mensagem afirmará tanto quanto e fornecerá um link para obter detalhes sobre o erro.

Quando você clica em Mais informações, a caixa de diálogo Detalhes da operação exibe uma lista dos itens de trabalho ou trabalhos que foram selecionados durante a operação. Você pode clicar em cada item de lista para visualização dos Detalhes do erro na parte inferior da caixa de diálogo.

### Gerenciar itens de trabalho ou trabalhos {#manage-the-work-items-or-jobs}

1. Use as ferramentas de operação descritas abaixo para gerenciar os itens de trabalho ou as tarefas na lista.

   >[!NOTE]
   >
   >As operações estão disponíveis dependendo do status do item.

   **Excluir itens:** exclui o item de trabalho ou o trabalho selecionado.

   **Pausar itens:** pausa o item de trabalho ou o trabalho selecionado.

   **Retomar itens:** Retorna o item de trabalho ou o trabalho selecionado de seu estado pausado.

   **Itens de Tentativa:** Tenta executar novamente o item de trabalho ou o trabalho selecionado de seu estado atual.

   Você pode verificar se uma operação foi bem-sucedida clicando em Mais informações acima da lista. Uma caixa de diálogo que contém os itens de trabalho ou trabalhos selecionados e seus status é exibida.

## Informações adicionais sobre status de item de trabalho {#additional-information-about-work-item-statuses}

Uma transição de estado típica para um item de trabalho é Novo > Agendado > Em andamento > Concluído ou Falha.

O estado Pausado interrompe esse fluxo normal. O aplicativo cliente ou o administrador do sistema pode iniciar essa interrupção (por exemplo, para manutenção ou atualização). É possível reverter essa ação usando a operação Retomar para mover o item de trabalho de volta para um estado Programado.

Um item de trabalho em um estado Programado está na fila para execução que ainda não começou. Esses itens podem ser pausados ou excluídos ou serão movidos para o estado Em andamento quando o Gerenciador de Trabalho os retirar da fila. Os itens de trabalho em andamento não podem ser modificados. Eles irão completar ou falhar.

O estado Falhou ocorre como resultado de uma condição de erro que ocorre durante a execução do item de trabalho. Se você suspeitar que os erros sejam circunstanciais (devido ao contexto no momento da execução), poderá repetir a execução, colocando o item de trabalho de volta na fila. Apenas um número limitado de tentativas é permitido.
