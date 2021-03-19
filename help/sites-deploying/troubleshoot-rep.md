---
title: Solução de problemas de replicação
seo-title: Solução de problemas de replicação
description: Este artigo fornece informações sobre como solucionar problemas de replicação.
seo-description: Este artigo fornece informações sobre como solucionar problemas de replicação.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuração
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---


# Solução de problemas de replicação{#troubleshooting-replication}

Esta página fornece informações sobre como solucionar problemas de replicação.

## Problema {#problem}

A replicação (replicação não reversa) está falhando por algum motivo.

## Resolução {#resolution}

Há vários motivos para a replicação falhar. Este artigo explica a abordagem que pode ser adotada ao analisar esses problemas.

**As replicações estão sendo acionadas ao clicar no botão Ativar? Se NÃO, faça o seguinte:**

1. Vá para /crx/explorer e faça logon como administrador.
1. Abra o &quot;Explorador de Conteúdo&quot;
1. Veja se existe um nó /bin/replicate ou /bin/replicate.json. Se o nó existir, exclua-o e salve.

**As replicações estão sendo enfileiradas nas filas do agente de replicação?**

Verifique isso indo para /etc/replication/agents.author.html e clique nos agentes de replicação para verificar.

**Se uma fila de agente ou algumas filas de agente estiverem presas:**

1. A fila mostra o status **bloqueado**? Em caso afirmativo, a instância de publicação não está em execução ou não responde totalmente? Verifique a instância de publicação para ver o que há de errado com ela (ou seja, verifique os logs e veja se há um erro OutOfMemory ou algum outro problema. Em seguida, se estiver apenas lento, pegue os despejos de encadeamento e analise-os.
1. O status da fila mostra **A fila está ativa - # pending**? Basicamente, o trabalho de replicação pode estar preso em uma leitura de soquete aguardando a instância de publicação ou o dispatcher responder. Isso pode significar que a instância de publicação ou o dispatcher está sob alta carga ou preso em um bloqueio. Pegue despejos de encadeamento do autor e publique neste caso.

   * Abra os dumps de encadeamento do autor em um analisador de despejo de encadeamento, verifique se ele mostra que o trabalho de evento de sling do agente de replicação está preso em um socketRead.
   * Abra os dumps de encadeamento da publicação em um analisador de dump de encadeamento, analise o que pode estar fazendo com que a instância de publicação não responda. Você deve ver um thread com POST /bin/receive em seu nome, que é o thread que recebe a replicação do autor.

**Se todas as filas de agente estiverem presas**

1. É possível que um determinado conteúdo não possa ser serializado em /var/replication/data devido a corrupção do repositório ou algum outro problema. Verifique se há um erro relacionado no logs/error.log. Para limpar o item de replicação incorreto, faça o seguinte:

   1. Vá para https://&lt;host>:&lt;port>/crx/de e faça logon como usuário administrador.
   1. Clique em &quot;Ferramentas&quot; no menu superior.
   1. Clique no botão da lupa.
   1. Selecione &quot;XPath&quot; como Type.
   1. Na caixa &quot;Consulta&quot;, digite esta consulta /jcr:root/var/eventing/jobs//element(*,slingevent:Job) order by @slingevent:created
   1. Clique em &quot;Pesquisar&quot;
   1. Nos resultados, os itens principais são os trabalhos de eventos de sling mais recentes. Clique em cada uma e localize as replicações presas que correspondem ao que aparece na parte superior da fila.

1. Pode haver algo errado com as filas de trabalho da estrutura de eventos do sling. Tente reiniciar o pacote org.apache.sling.event no /system/console.
1. Pode ser que o processamento de trabalho esteja completamente desligado. Você pode verificar isso no Felix Console na guia Eventos do Sling. Verifique se é exibido - Apache Sling Eventing (O PROCESSAMENTO DE TAREFA ESTÁ DESATIVADO!)

   * Se sim, marque Apache Sling Job Event Handler na guia Configuração no Felix Console. Pode ser que a caixa de seleção &#39;Processamento de trabalho ativado&#39; esteja desmarcada. Se essa opção estiver marcada e ainda assim exibir que &quot;o processamento de tarefas está desativado&quot;, verifique se há alguma sobreposição em /apps/system/config que esteja desativando o processamento de tarefas. Tente criar um nó osgi:config para jobmanager.enabled com um valor booleano para true e verifique novamente se a ativação foi iniciada e se não há mais tarefas na fila.

1. Também pode ser o caso em que a configuração DefaultJobManager fica em um estado inconsistente. Isso pode acontecer quando alguém modifica manualmente a configuração do &quot;Manipulador de evento do trabalho do Apache Sling&quot; por meio do console OSG (por exemplo, desative e reative a propriedade &quot;Processamento de trabalho ativado&quot; e salve a configuração).

   * Neste ponto, a configuração DefaultJobManager que é armazenada em crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config entra em um estado inconsistente. E mesmo que a propriedade &#39;Manipulador de Evento de Trabalho do Apache Sling&#39; mostre &#39;Processamento de Trabalho Ativado&#39; como estando no estado marcado, quando se navega até a guia Evento do Sling, ela mostra a mensagem - O PROCESSAMENTO DO JOB ESTÁ DESATIVADO e a replicação não funciona.
   * Para resolver esse problema, seria necessário navegar até a página Configuração do console OSGi e excluir a configuração &quot;Manipulador de evento do trabalho do Apache&quot;. Em seguida, reinicie o nó Principal do cluster para obter a configuração de volta a um estado consistente. Isso deve corrigir o problema e a replicação começará a funcionar novamente.

**Criar um replication.log**

Às vezes, pode ser muito útil definir todos os logs de replicação a serem adicionados em um arquivo de log separado no nível DEBUG. Para fazer isso:

1. Vá para https://host:port/system/console/configMgr e faça logon como administrador.
1. Localize a fábrica Apache Sling Logging Logger e crie uma instância clicando no botão **+** à direita da configuração de fábrica. Isso criará um novo logger de registro.
1. Defina a configuração desta forma:

   * Nível de registro: DEPURAR
   * Caminho do arquivo de log: logs/replication.log
   * Categorias: com.day.cq.replication

1. Se você suspeitar que o problema esteja relacionado a eventos/trabalhos do sling de alguma forma, também poderá adicionar este pacote java em categories:org.apache.sling.event

## Pausando Fila do Agente de Replicação {#pausing-replication-agent-queue}

Às vezes, pode ser adequado pausar a fila de replicação para reduzir a carga no sistema de autor, sem desativá-la. Atualmente, isso só é possível por meio de uma pilha de configuração temporária de uma porta inválida. A partir da 5.4, você pode ver o botão pausar na fila do agente de replicação, ele tem alguma limitação

1. O estado não é persistente, o que significa que se você reiniciar um servidor ou um pacote de replicação for reciclado, ele retornará ao estado de execução.
1. A pausa fica inativa por um período mais curto (OOB 1 hora após nenhuma atividade com replicação por outros threads) e não por um tempo mais longo. Porque há um recurso no sling que evita threads ociosos. Basicamente, verifique se um encadeamento de fila de trabalhos foi usado por um tempo maior, se assim for, ele inicia os ciclos de limpeza. Devido ao ciclo de limpeza, ele interrompe o thread e, portanto, a configuração pausada é perdida. Como os trabalhos são persistentes, ele inicia um novo thread para processar a fila que não tem detalhes da configuração pausada. Devido a essa fila, o fica em estado de execução.

## As permissões de página não são replicadas na ativação do usuário {#page-permissions-are-not-replicated-on-user-activation}

As permissões de página não são replicadas porque são armazenadas nos nós aos quais o acesso é concedido, não com o usuário.

Em geral, as permissões de página não devem ser replicadas do autor para publicação e não são por padrão. Isso ocorre porque os direitos de acesso devem ser diferentes nesses dois ambientes. Portanto, é recomendável configurar ACLs na publicação separadamente do autor.

## Fila de replicação bloqueada ao replicar informações do namespace do Autor para Publicar {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

Em alguns casos, a fila de replicação é bloqueada ao tentar replicar informações do namespace da instância do autor para a instância de publicação. Isso acontece porque o usuário de replicação não tem privilégio `jcr:namespaceManagement`. Para evitar esse problema, verifique se:

* O usuário de replicação (conforme configurado na guia [Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)>User) também existe na instância Publish .
* O usuário tem privilégios de leitura e gravação no caminho em que o conteúdo é instalado.
* O usuário tem privilégio `jcr:namespaceManagement` no nível do repositório. É possível conceder o privilégio da seguinte maneira:

1. Faça logon no CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Clique na guia **Controle de acesso**.
1. Selecione **Repositório**.
1. Clique em **Adicionar entrada** (o ícone de adição).
1. Insira o nome do usuário.
1. Selecione `jcr:namespaceManagement` na lista de privilégios.
1. Clique em OK.

