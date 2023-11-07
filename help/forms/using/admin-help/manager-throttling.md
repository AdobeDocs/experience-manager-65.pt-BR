---
title: Gerenciador de trabalho e limitação
description: Este documento fornece informações de fundo sobre o Work Manager e fornece instruções sobre a configuração das opções de limitação do Work Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---

# Gerenciador de trabalho e limitação{#work-manager-and-throttling}

Os formulários AEM (e versões anteriores) usavam filas JMS para executar operações de forma assíncrona. Nos formulários AEM, as filas JMS foram substituídas pelo Work Manager. Este documento fornece informações de fundo sobre o Work Manager e fornece instruções sobre a configuração das opções de limitação do Work Manager.

## Sobre operações de longa duração (assíncronas) {#about-long-lived-asynchronous-operations}

Nos formulários AEM, as operações realizadas pelos serviços podem ser de curta duração (síncronas) ou de longa duração (assíncronas). As operações de curta duração são concluídas de forma síncrona no mesmo thread a partir do qual foram chamadas. Essas operações aguardam uma resposta antes de continuar.

Operações de longa duração podem abranger sistemas ou até mesmo se estender além da organização, como quando um cliente precisa preencher e enviar um formulário de solicitação de empréstimo como parte de uma solução maior que integra várias tarefas automatizadas e humanas. Essas operações devem continuar enquanto aguardamos uma resposta. Operações de longa duração executam seu trabalho subjacente de forma assíncrona, permitindo que os recursos sejam envolvidos enquanto aguardam a conclusão. Ao contrário de uma operação de curta duração, o Work Manager não considera uma operação de longa duração como concluída após ser chamada. Um acionador externo, como um sistema que solicita outra operação no mesmo serviço ou um usuário que envia um formulário, deve ocorrer para concluir a operação.

## Sobre o Gerenciador de trabalho {#about-work-manager}

Os formulários AEM (e versões anteriores) usavam filas JMS para executar operações de forma assíncrona. O AEM Forms usa o Work Manager para agendar e executar operações assíncronas por meio de threads gerenciados.

As operações assíncronas são tratadas da seguinte maneira:

1. O Work Manager recebe um item de trabalho para execução.
1. O Work Manager armazena o item de trabalho em uma tabela de banco de dados e atribui um identificador exclusivo ao item de trabalho. O registro do banco de dados contém todas as informações necessárias para executar o item de trabalho.
1. As threads do Work Manager extraem itens de trabalho quando as threads se tornam livres. Antes de extrair os itens de trabalho, as threads podem verificar se os serviços necessários estão iniciados, se há tamanho de heap suficiente para extrair o próximo item de trabalho e se há ciclos de CPU suficientes para processar o item de trabalho. O Work Manager também avalia os atributos do item de trabalho (como sua prioridade) ao programar sua execução.

Os administradores de formulários AEM podem usar o Health Monitor para verificar as estatísticas do Work Manager, como o número de itens de trabalho na fila e seus status. Você também pode usar o Monitor de Integridade para pausar, retomar, repetir ou excluir itens de trabalho. (Consulte [Exibir estatísticas relacionadas ao Gerenciador de Trabalho](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configurar opções de limitação do Work Manager {#configuring-work-manager-throttling-options}

Você pode configurar a limitação para o Work Manager, de modo que os itens de trabalho sejam agendados somente quando houver recursos de memória suficientes disponíveis. Você configura a limitação definindo as seguintes opções JVM em seu servidor de aplicativos.

<table>
 <thead>
  <tr>
   <th><p>Propriedade</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>Especifica o intervalo de tempo, em milissegundos, que o Work Manager utiliza ao verificar novos itens em sua fila.</p><p>O valor dessa opção é um número inteiro. O valor padrão é <code>1000</code> milissegundos (1 segundo). </p><p>Se o volume de invocações assíncronas for baixo, você poderá aumentar esse valor. Por exemplo, você pode aumentá-lo para algo entre 2000 e 5000 (2 a 5 segundos). </p><p>Se o volume de invocações assíncronas for alto, o valor padrão deverá ser suficiente, mas você poderá usar um valor menor, se necessário. Diminuir muito esse valor (por exemplo, abaixo de 50, o que resulta em uma frequência de pesquisa de 20 vezes por segundo) causa uma sobrecarga substancial no sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Defina essa opção como <code>true</code> para ativar o modo de depuração, ou para falso para desativá-lo. </p><p>No modo de depuração, mensagens relacionadas a violações de política do Work Manager e ações de pausa/retomada do Work Manager são registradas. Defina essa opção como true somente ao solucionar problemas.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Defina essa opção como <code>true</code> para permitir a limitação com base nas configurações de controle de memória descritas abaixo, ou para <code>false</code> para desativar a limitação.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Especifica a porcentagem máxima de memória que pode estar em uso antes que o Work Manager limite trabalhos de entrada.</p><p>O valor padrão para essa opção é <code>95</code>. Esse valor deve ser adequado para a maioria dos sistemas. Aumente-o somente se o sistema precisar avançar para a capacidade máxima. Mas observe que, à medida que você aumenta esse valor, o risco de problemas de falta de memória também aumenta.</p><p>Se você estiver executando formulários AEM em um ambiente em cluster, convém definir as configurações de limite de controle de memória de forma diferente em diferentes nós do cluster. Por exemplo, você pode ter um limite superior mais baixo nos nós A e B, que são programados no balanceador de carga para trabalho interativo. E você pode ter limites superiores definidos nos nós C e D, que não são usados pelo balanceador de carga, mas reservados para trabalho assíncrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Especifica a porcentagem máxima de memória que pode estar em uso antes que o Work Manager pare de limitar trabalhos de entrada.</p><p>O valor padrão para essa opção é <code>20</code>. Esse valor deve ser adequado para a maioria dos sistemas.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Especifica o tamanho máximo do lote para o gerenciador de trabalho. O tamanho padrão do lote é 10.</p><p>Se o status de um processo no gerenciador de trabalho não for atualizado mesmo depois que a tarefa for concluída, defina o tamanho do lote para 1.</p></td>
  </tr>
 </tbody>
</table>

**Adicionar opções Java ao JBoss**

1. Interrompa o servidor da aplicação JBoss.
1. Abra o *[raiz do appserver]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) em um editor e adicione qualquer uma das opções de Java, conforme necessário, no formato `-Dproperty=value`.
1. Reinicie o servidor.

**Adicionar opções Java ao WebLogic**

1. Inicie o Console de Administração do WebLogic digitando `https://[host name]:[port]/console` em um navegador da Web.
1. Digite o nome de usuário e a senha criados para o domínio do WebLogic Server e clique em Registrar no Centro de Alterações, em Bloquear e Editar.
1. Em Estrutura do domínio, clique em Ambiente > Servidores e, no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique na guia Configuração > na guia Início do servidor.
1. Na caixa Argumentos, anexe os argumentos necessários ao final do conteúdo atual. Por exemplo, para desativar o Health Monitor, adicione:

   `-Dadobe.healthmonitor.enabled=false` desabilita o Monitor de Integridade.

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

**Adicionar opções de Java ao WebSphere**

1. Na árvore de navegação do Console administrativo do WebSphere, clique em Servidores > Tipos de servidor > Servidores de aplicativos WebSphere.
1. No painel direito, clique no nome do servidor.
1. Em Infraestrutura do servidor, clique em Fluxo de trabalho de formulários e Java > Definição de processo.
1. Em Propriedades adicionais, clique em Java Virtual Machine.
1. Na caixa Generic JVM arguments, digite os argumentos necessários.
1. Clique em OK ou em Aplicar e, em seguida, clique em Salvar diretamente na configuração-mestre.
