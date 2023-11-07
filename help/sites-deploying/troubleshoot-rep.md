---
title: Solução de problemas de replicação
description: Este artigo fornece informações sobre como solucionar problemas de replicação.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Solução de problemas de replicação{#troubleshooting-replication}

Esta página fornece informações sobre como solucionar problemas de replicação.

## Problema {#problem}

A replicação (replicação não reversa) está falhando por algum motivo.

## Resolução {#resolution}

Há vários motivos para a replicação falhar. Este artigo explica a abordagem que pode ser adotada ao analisar esses problemas.

**As replicações estão sendo acionadas ao clicar no botão Ativar? Caso CONTRÁRIO, faça o seguinte:**

1. Acesse /crx/explorer e faça logon como administrador.
1. Abra o &quot;Content Explorer&quot;
1. Consulte se um nó /bin/replicate ou /bin/replicate.json existe. Se o nó existir, exclua-o e salve.

**As replicações estão sendo enfileiradas nas filas do agente de replicação?**

Verifique isso acessando /etc/replication/agents.author.html e clicando nos agentes de replicação para verificar.

**Se uma fila de agente ou algumas filas de agente estiverem travadas:**

1. A fila mostra **bloqueado** Status? Em caso afirmativo, a instância de publicação não está em execução ou não está respondendo? Verifique a instância de publicação para ver o que há de errado com ela. Ou seja, verifique os registros e veja se há um erro OutOfMemory ou algum outro problema. Se estiver apenas lento, então pegue os despejos de thread e analise-os.
1. O status da fila mostra **A fila está ativa - nº pendente**? Basicamente, o trabalho de replicação pode estar preso em uma leitura de soquete aguardando a instância de publicação ou o Dispatcher responder. Isso pode significar que a instância de publicação ou o Dispatcher está sobrecarregada ou travada em um bloqueio. Obtenha despejos de thread do autor e da publicação neste caso.

   * Abra os despejos de thread do autor em um analisador de despejo de thread. Verifique se ele mostra que o trabalho de evento sling do agente de replicação está preso em um socketRead.
   * Abra os despejos de thread em publicar em um analisador de despejo de thread e analise o que pode estar fazendo com que a instância de publicação não responda. Você deve ver uma thread com POST /bin/receive em seu nome, que é a thread que recebe a replicação do autor.

**Se todas as filas do agente estiverem travadas**

1. É possível que um conteúdo específico não possa ser serializado em /var/replication/data devido à corrupção do repositório ou a algum outro problema. Consulte o site logs/error.log para verificar se há um erro relacionado. Para limpar o item de replicação inválido, faça o seguinte:

   1. Acesse https://&lt;host>:&lt;port>/crx/de e faça logon como usuário administrador.
   1. Clique em &quot;Ferramentas&quot; no menu superior.
   1. Clique no botão de lupa.
   1. Selecione &quot;XPath&quot; como Type.
   1. Na caixa &quot;Consulta&quot;, digite esta consulta /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) ordem de @slingevent:criada
   1. Clique em &quot;Pesquisar&quot;.
   1. Nos resultados, os itens principais são os trabalhos de evento do sling mais recentes. Clique em cada uma e localize as replicações paralisadas correspondentes ao que aparece na parte superior da fila.

1. Pode haver algo errado com as filas de trabalho da estrutura de eventos do sling. Tente reiniciar o pacote org.apache.sling.event no/system/console.
1. Pode ser que o processamento de trabalhos esteja desativado. Você pode verificar isso no Felix Console na guia Evento do Sling. Verifique se exibido - Evento do Apache Sling (O PROCESSAMENTO DE TRABALHO ESTÁ DESATIVADO!)

   * Em caso positivo, marque Manipulador de eventos de trabalho do Apache Sling na guia Configuração no Console Felix. Pode ser que a caixa de seleção &#39;Processamento de trabalho ativado&#39; esteja desmarcada. Se essa opção estiver marcada e ainda exibir &quot;o processamento do trabalho está desativado&quot;, verifique se há alguma sobreposição em /apps/system/config que esteja desabilitando o processamento do trabalho. Tente criar um nó osgi:config para jobmanager.enabled com um valor booleano como true e verifique novamente se a ativação foi iniciada e se não há mais trabalhos na fila.

1. Também pode ocorrer que a configuração de DefaultJobManager entre em um estado inconsistente. Isso pode acontecer quando alguém modifica manualmente a configuração do &quot;Manipulador de eventos de trabalho do Apache Sling&quot; por meio do OSGiconsole (por exemplo, desative e reative a propriedade &quot;Processamento de trabalho ativado&quot; e salve a configuração).

   * Neste ponto, a configuração DefaultJobManager armazenada em crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config entra em um estado inconsistente. E mesmo que a propriedade &quot;Manipulador de eventos de trabalho do Apache Sling&quot; mostre &quot;Processamento de trabalho ativado&quot; para estar no estado marcado, quando alguém navega até a guia Evento do Sling, ela mostra a mensagem - O PROCESSAMENTO DE TRABALHO ESTÁ DESATIVADO e a replicação não funciona.
   * Para resolver esse problema, navegue até a página Configuração do console OSGi e exclua a configuração &quot;Manipulador de eventos de trabalho do Apache Sling&quot;. Em seguida, reinicie o nó Principal do cluster para colocar a configuração de volta em um estado consistente. Isso deve corrigir o problema e a replicação começa a funcionar novamente.

**Criar um replication.log**

Às vezes, é útil definir todos os logs de replicação para serem adicionados em um arquivo de log separado no nível DEBUG. Para fazer isso:

1. Acesse https://host:port/system/console/configMgr e faça logon como administrador.
1. Localize o fatory Apache Sling Logging Logger e crie uma instância clicando no **+** à direita da configuração de fábrica. Isso cria um novo logger de log.
1. Defina a configuração desta forma:

   * Nível de log: DEBUG
   * Caminho do arquivo de log: logs/replication.log
   * Categorias: com.day.cq.replication

1. Se você suspeitar que o problema esteja relacionado a eventos/trabalhos do sling de alguma forma, também será possível adicionar esse pacote do Java™ em categorias:org.apache.sling.event

## Pausando Fila do Agente de Replicação  {#pausing-replication-agent-queue}

Às vezes, pode ser adequado pausar a fila de replicação para reduzir a carga no sistema de criação, sem desabilitá-la. Atualmente, isso só é possível por um hack de configuração temporária de uma porta inválida. A partir da versão 5.4, você pode ver o botão Pausar na fila do agente de replicação. Ele tem algumas limitações

1. O estado não é persistente, o que significa que, se você reiniciar um servidor ou um pacote de replicação for reciclado, ele voltará ao estado em execução.
1. A pausa fica ociosa por um período mais curto (OOB 1 hora depois de nenhuma atividade com replicação por outros threads) e não por um tempo mais longo. Porque há um recurso no sling que evita threads ociosos. Basicamente, verifique se uma thread da fila de trabalhos está sem uso há mais tempo. Nesse caso, ela inicia os ciclos de limpeza. Devido ao ciclo de limpeza, ele interrompe a thread e, portanto, a configuração pausada é perdida. Como os trabalhos são persistentes, ele inicia um novo thread para processar a fila que não tem detalhes da configuração pausada. Devido a esta fila se transforma em estado de execução.

## As permissões de página não são replicadas na ativação do usuário {#page-permissions-are-not-replicated-on-user-activation}

As permissões de página não são replicadas porque são armazenadas nos nós aos quais o acesso é concedido, não com o usuário.

Em geral, as permissões de página não devem ser replicadas do autor para publicar e não são usadas por padrão. Isso ocorre porque os direitos de acesso devem ser diferentes nesses dois ambientes. Portanto, o Adobe recomenda que você configure ACLs em publicação, separadamente do autor.

## Fila de replicação bloqueada ao replicar informações de namespace de Autor para Publicação {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

Às vezes, a fila de replicação é bloqueada ao tentar replicar informações de namespace da instância do autor para a instância de publicação. Isso acontece porque o usuário de replicação não tem `jcr:namespaceManagement` Privilégio. Para evitar esse problema, verifique se:

* O usuário de replicação (conforme configurado no [Transporte](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) também existe na instância Publish.
* O usuário tem privilégios de leitura e gravação no caminho em que o conteúdo está instalado.
* O usuário tem `jcr:namespaceManagement` no nível do repositório. Você pode conceder o privilégio da seguinte maneira:

1. Faça logon no CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Clique em **Controle de acesso** guia.
1. Selecionar **Repositório**.
1. Clique em **Adicionar entrada** (o ícone com sinal de mais).
1. Insira o nome do usuário.
1. Selecionar `jcr:namespaceManagement` na lista de privilégios.
1. Clique em **OK**.
