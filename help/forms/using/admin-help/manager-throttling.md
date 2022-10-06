---
title: Gerenciador de trabalho e limitação
seo-title: Work Manager and throttling
description: Este documento fornece informações de fundo sobre o Gerenciador de Trabalho e fornece instruções sobre como configurar as opções de limitação do Gerenciador de Trabalho.
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Gerenciador de trabalho e limitação{#work-manager-and-throttling}

AEM formulários (e versões anteriores) usavam as filas do JMS para executar operações de forma assíncrona. Em AEM formulários, as filas do JMS foram substituídas pelo Gerenciador de trabalho. Este documento fornece informações de fundo sobre o Gerenciador de Trabalho e fornece instruções sobre como configurar as opções de limitação do Gerenciador de Trabalho.

## Sobre operações de duração longa (assíncrona) {#about-long-lived-asynchronous-operations}

Em AEM formulários, as operações executadas pelos serviços podem ter vida curta (síncrona) ou longa (assíncrona). As operações de curta duração são concluídas de forma síncrona no mesmo thread a partir do qual foram chamadas. Essas operações aguardam uma resposta antes de continuar.

Operações de longa duração podem estender-se por sistemas ou até mesmo estender-se além da organização, como quando um cliente deve preencher e enviar um formulário de pedido de empréstimo como parte de uma solução maior que integra várias tarefas automáticas e humanas. Essas operações devem continuar enquanto se aguarda uma resposta. As operações de longa duração executam o seu trabalho subjacente de forma assíncrona, permitindo que os recursos sejam utilizados de outra forma enquanto aguardam a conclusão. Ao contrário de uma operação de curta duração, o Gerenciador de Trabalho não considera uma operação de longa duração concluída uma vez que é chamada. Um acionador externo, como um sistema que solicita outra operação no mesmo serviço ou um usuário que envia um formulário, deve ocorrer para concluir a operação.

## Sobre o Gerenciador de Trabalho {#about-work-manager}

AEM formulários (e versões anteriores) usavam as filas do JMS para executar operações de forma assíncrona. AEM formulários usa o Gerenciador de trabalho para agendar e executar operações assíncronas por meio de threads gerenciados.

As operações assíncronas são tratadas dessa maneira:

1. O Gerenciador de trabalho recebe um item de trabalho para execução.
1. O Gerenciador de Trabalho armazena o item de trabalho em uma tabela de banco de dados e atribui um identificador exclusivo ao item de trabalho. O registro do banco de dados contém todas as informações necessárias para executar o item de trabalho.
1. Os threads do Gerenciador de trabalho extraem itens de trabalho quando os threads se tornam livres. Antes de extrair os itens de trabalho, os threads podem verificar se os serviços necessários foram iniciados, se há tamanho de heap suficiente para extrair o próximo item de trabalho e se há ciclos de CPU suficientes para processar o item de trabalho. O Gerenciador de Trabalho também avalia atributos do item de trabalho (como sua prioridade) ao programar sua execução.

AEM administradores de formulários podem usar o Monitor de integridade para verificar as estatísticas do Gerenciador de trabalho, como o número de itens de trabalho na fila e seus status. Você também pode usar o Monitor de Integridade para pausar, retomar, tentar novamente ou excluir itens de trabalho. (Consulte [Exibir estatísticas relacionadas ao Gerenciador de Trabalho](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## Configuração das opções de limitação do Gerenciador de Trabalho {#configuring-work-manager-throttling-options}

Você pode configurar a limitação para o Gerenciador de trabalho, de modo que os itens de trabalho sejam agendados somente quando houver recursos de memória suficientes disponíveis. Você configura a limitação definindo as seguintes opções da JVM no servidor de aplicativos.

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
   <td><p>Especifica o intervalo de tempo, em milissegundos, que o Gerenciador de Trabalho usa ao verificar novos itens em sua fila.</p><p>O valor dessa opção é um número inteiro. O valor padrão é <code>1000</code> milissegundos (1 segundo). </p><p>Se o volume de invocações assíncronas for baixo, você poderá aumentar esse valor. Por exemplo, você pode aumentá-lo para algo entre 2000 e 5000 (2 a 5 segundos). </p><p>Se o volume de invocações assíncronas for alto, o valor padrão deverá ser suficiente, mas você poderá usar um valor menor, se necessário. Diminuir esse valor demais (por exemplo, abaixo de 50, o que resulta em uma frequência de pesquisa de 20 vezes por segundo) causa uma sobrecarga substancial no sistema.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>Defina essa opção como <code>true</code> para ativar o modo de depuração ou para falso para desativá-lo. </p><p>No modo de depuração, as mensagens relacionadas às violações da política do Gerenciador de trabalho e às ações de pausa/retomada do Gerenciador de trabalho são registradas. Defina essa opção como true somente ao solucionar problemas.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>Defina essa opção como <code>true</code> ativar a limitação com base nas definições de controlo de memória a seguir descritas, ou <code>false</code> para desativar a limitação.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>Especifica a porcentagem máxima de memória que pode ser usada antes que o Gerenciador de Trabalho controle as tarefas recebidas.</p><p>O valor padrão para essa opção é <code>95</code>. Esse valor deve ser bom para a maioria dos sistemas. Aumente-o somente se o sistema precisar fazer o push para atingir a capacidade máxima. Mas observe que ao aumentar esse valor, o risco de problemas de falta de memória também aumenta.</p><p>Se você estiver executando AEM formulários em um ambiente em cluster, talvez queira definir as configurações de limite de controle de memória de forma diferente em diferentes nós do cluster. Por exemplo, você pode ter um limite alto mais baixo nos nós A e B, que são programados em seu balanceador de carga para trabalho interativo. E você poderia ter limites mais altos definidos nos nós C e D, que não são usados pelo balanceador de carga, mas reservados para o trabalho assíncrono.</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>Especifica a porcentagem máxima de memória que pode ser usada antes que o Gerenciador de Trabalho pare de limitar tarefas de entrada.</p><p>O valor padrão para essa opção é <code>20</code>. Esse valor deve ser bom para a maioria dos sistemas.</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>Especifica o tamanho máximo do lote para o gerenciador de trabalho. O tamanho padrão do lote é 10.</p><p>Se o status de um processo no gerenciador de trabalho não for atualizado mesmo após a conclusão da tarefa, defina o tamanho do lote como 1.</p></td>
  </tr>
 </tbody>
</table>

**Adicionar opções Java ao JBoss**

1. Pare o servidor de aplicativos JBoss.
1. Abra o *[raiz do appserver]*/bin/run.bat (Windows) ou run.sh (Linux ou UNIX) em um editor e adicione qualquer uma das opções do Java, conforme necessário, no formato `-Dproperty=value`.
1. Reinicie o servidor.

**Adicionar opções de Java ao WebLogic**

1. Inicie o Console de Administração do WebLogic digitando `https://[host name]:[port]/console` em um navegador da Web.
1. Digite o nome de usuário e a senha que você criou para o domínio do WebLogic Server e clique em Registrar no Change Center, clique em Bloquear e editar.
1. Em Estrutura de domínio, clique em Ambiente > Servidores e, no painel direito, clique no nome do servidor gerenciado.
1. Na próxima tela, clique na guia Configuração > Início do servidor .
1. Na caixa Argumentos , anexe os argumentos necessários ao final do conteúdo atual. Por exemplo, para desativar o Monitor de integridade, adicione:

   `-Dadobe.healthmonitor.enabled=false` desativa o Monitor de integridade.

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado do WebLogic.

**Adicionar opções Java ao WebSphere**

1. Na árvore de navegação do Console Administrativo do WebSphere, clique em Servidores > Tipos de Servidor > Servidores de aplicativos WebSphere.
1. No painel direito, clique no nome do servidor.
1. Em Infraestrutura do servidor, clique em Java e fluxo de trabalho de formulários > Definição do processo.
1. Em Additional Properties, clique em Java Virtual Machine.
1. Na caixa Generic JVM arguments, digite os argumentos necessários.
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração principal.
