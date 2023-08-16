---
title: Exibir estatísticas relacionadas ao Gerenciador de Trabalho
seo-title: View statistics related to Work Manager
description: A guia Gerenciador de trabalho exibe estatísticas relacionadas aos itens do Gerenciador de trabalho. Saiba como visualizar e filtrar os itens de trabalho.
seo-description: The Work Manager tab displays statistics that relate to Work Manager items. Learn how you can view and filter the work items.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 0%

---

# Exibir estatísticas relacionadas ao Gerenciador de Trabalho {#view-statistics-related-to-work-manager}

A guia Gerenciador de trabalho exibe estatísticas relacionadas aos itens do Gerenciador de trabalho. Esses itens de trabalho estão em estados diferentes, dependendo de onde estão em seu processo. (Consulte [Status (somente para as categorias Padrão, Fluxo de trabalho ou Eventos)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) É possível filtrar as informações para exibir apenas um subconjunto dos itens usando as várias opções disponíveis (por exemplo, Status ou Categoria). Você pode classificar itens de trabalho ou de trabalho resultantes (em ordem crescente ou decrescente) clicando em um dos cabeçalhos de coluna. Além disso, você pode gerenciar os itens de trabalho usando as ferramentas de operação exibidas acima da lista de itens de trabalho.

## Filtrar os itens de trabalho {#filter-the-work-items}

1. Clique na guia Work Manager.
1. Selecione os critérios para um ou mais dos filtros descritos abaixo e clique em Ir.

### Categoria {#category}

**Padrão:** Todos os itens de trabalho aos quais o cliente não atribuiu uma categoria quando foram enviados. O Work Manager gerencia esses itens, portanto, os status pertencem ao Work Manager.

**Gerenciador de Jobs:** Todos os jobs que pertencem ao Gerenciador de Jobs. O Gerenciador de Jobs gerencia seus próprios jobs e tem seus próprios status de job. Consulte os status de tarefa específicos descritos abaixo.

**Fluxo de trabalho:** Todos os itens de trabalho que pertencem à execução do fluxo de trabalho. O workflow não gerencia seus próprios itens de trabalho, mas depende do Work Manager; portanto, os status pertencem ao Work Manager.

**Eventos:** Todos os itens de trabalho que pertencem ao Gerenciamento de eventos. O Gerenciamento de eventos não gerencia seus próprios itens de trabalho, mas depende do Work Manager; portanto, os status pertencem ao Work Manager.

### Status (somente para as categorias Padrão, Fluxo de trabalho ou Eventos) {#status-for-default-workflow-or-events-categories-only}

**Mostrar tudo:** Exibe todos os itens de trabalho atuais.

**Agendado:** Exibe todos os itens de trabalho prontos para execução pelo servidor de aplicativos, mas que ainda não foram iniciados.

**Pausado:** Exibe todos os itens de trabalho agendados que o aplicativo cliente pausou. Esses itens podem ser executados ou excluídos. (Consulte Gerenciar itens de trabalho ou processos.)

**Em andamento:** Exibe todos os itens de trabalho que o Gerenciador de Trabalho do servidor de aplicativos selecionou e que serão concluídos ou falharão. Não é possível usar operações nesses itens de trabalho.

**Concluído:** Exibe todos os itens de trabalho executados com sucesso. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada. Você pode excluir esses itens usando a operação Excluir itens. (Consulte Gerenciar itens de trabalho ou processos.)

**Falha:** Exibe todos os itens de trabalho que não foram concluídos com êxito devido a uma condição de erro. Esses itens de trabalho podem ser repetidos algumas vezes usando a operação Repetir itens. (Consulte Gerenciar itens de trabalho ou processos.) Um link Failure (Falha) na coluna Status permite acessar detalhes sobre a falha.

**Desconhecido:** Exibe todos os itens de trabalho cujo status é desconhecido.

### Status (somente para a categoria Gerenciador de Jobs) {#status-for-job-manager-category-only}

**Concluído:** Exibe todos os jobs que foram executados com sucesso. Os itens de trabalho persistentes permanecem nesse estado e os itens não persistentes são excluídos após a conclusão dos retornos de chamada para os manipuladores de retorno de chamada.

**Conclusão solicitada:** Exibe os jobs para os quais foi feita uma solicitação completa.

**Falha solicitada:** Exibe os jobs para os quais foi feita uma solicitação de falha.

**Falha:** Exibe os jobs que não foram concluídos com êxito devido a uma condição de erro. Um link Failure (Falha) na coluna Status permite acessar detalhes sobre a falha.

**Encerramento solicitado:** Exibe os jobs para os quais foi feita uma solicitação de finalização.

**Encerrado:** Exibe jobs que foram encerrados sem conclusão.

**Suspensão solicitada:** Exibe os jobs para os quais foi feita uma solicitação de suspensão.

**Suspenso:** Exibe os jobs suspensos.

**Retomada solicitada:** Exibe os jobs para os quais foi feita uma solicitação de retomada.

**Na fila:** Exibe os jobs que estão na fila.

**Em execução:** Exibe os jobs que estão em execução.

### Nome do servidor {#server-name}

Somente para servidores clusterizados, selecione o nome do nó para exibir os itens de trabalho ou itens de trabalho criados apenas nesse servidor. Se Mostrar Tudo estiver selecionado, todos os itens de trabalho de todos os nós em um cluster serão exibidos.

### Horário de criação {#create-time}

Selecione uma opção neste filtro para mostrar apenas os itens de trabalho criados dentro do período selecionado. Por exemplo, selecionar 1 dia exibe todos os itens de trabalho que foram criados 24 horas antes do horário definido no filtro Antes de.

### Antes de {#prior-to}

Define a data e a hora que o filtro Criar hora usa como data final. Mantenha a opção Usar data e hora atuais selecionada para filtrar a partir da data e hora atuais ou desmarque a opção e insira os valores apropriados. Clique nos ícones de calendário ou nos ícones de relógio para selecionar valores usando essas ferramentas.

Por exemplo, selecionar Criar hora = 1 dia e Antes de = Usar data e hora atuais retorna todos os itens de trabalho que foram criados nas últimas 24 horas.

>[!NOTE]
>
>Em implantações de banco de dados de Oracle, os filtros de intervalo de datas (ou seja, Criar hora e Antes das configurações) não funcionam com precisão. Use outro filtro para recuperar itens de trabalho.

## Sobre a interface da guia Work Manager {#about-the-work-manager-tab-interface}

Quando você executa uma consulta do Work Manager ou executa uma operação em um item de trabalho ou job, uma mensagem é exibida acima da lista. Esta mensagem fornece feedback sobre a ação que você iniciou e, em alguns casos, um link Mais informações para fornecer detalhes. Por exemplo, se a operação iniciada falhar, a mensagem informará o máximo e fornecerá um link para obter detalhes sobre o erro.

Quando você clica em Mais Informações, a caixa de diálogo Detalhes da Operação exibe uma lista dos itens de trabalho ou trabalhos selecionados durante a operação. Você pode clicar em cada item da lista para exibir os Detalhes do Erro na parte inferior da caixa de diálogo.

### Gerenciar itens de trabalho ou trabalhos {#manage-the-work-items-or-jobs}

1. Use as ferramentas de operação descritas abaixo para gerenciar os itens de trabalho ou trabalhos na lista.

   >[!NOTE]
   >
   >As operações estão disponíveis dependendo do status do item.

   **Excluir itens:** Exclui o item de trabalho ou trabalho selecionado.

   **Pausar itens:** Pausa o item de trabalho ou trabalho selecionado.

   **Retomar itens:** Retoma o item de trabalho ou a tarefa selecionada do seu estado pausado.

   **Tentar novamente os itens:** Tenta executar novamente o item de trabalho ou trabalho selecionado a partir do seu estado atual.

   Você pode verificar se uma operação foi bem-sucedida clicando em Mais informações acima da lista. Uma caixa de diálogo que contém os itens de trabalho ou trabalhos selecionados e seus status é exibida.

## Informações adicionais sobre status de item de trabalho {#additional-information-about-work-item-statuses}

Uma transição de estado típica para um item de trabalho é Novo > Programado > Em andamento > Concluído ou Falha.

O estado Paused interrompe esse fluxo normal. O aplicativo cliente ou o administrador do sistema pode iniciar essa interrupção (por exemplo, para manutenção ou atualização). Você pode reverter essa ação usando a operação Retomar para mover o item de trabalho de volta para o estado Programado.

Um item de trabalho em um estado Agendado é enfileirado para execução que ainda não começou. Esses itens podem ser pausados ou excluídos, ou serão movidos para o estado Em andamento quando o Work Manager os retirar da fila. Itens de trabalho que estão em andamento não podem ser modificados. Eles serão concluídos ou não.

O estado Falha ocorre como resultado de uma condição de erro que ocorre durante a execução do item de trabalho. Se você suspeitar que os erros sejam circunstanciais (devido ao contexto no momento da execução), poderá repetir a execução, colocando o item de trabalho de volta na fila. Somente um número limitado de tentativas é permitido.
