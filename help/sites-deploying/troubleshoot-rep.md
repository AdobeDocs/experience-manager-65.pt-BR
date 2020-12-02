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
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---


# Solução de problemas de replicação{#troubleshooting-replication}

Esta página fornece informações sobre como solucionar problemas de replicação.

## Problema {#problem}

A replicação (replicação não reversa) está falhando por algum motivo.

## Resolução {#resolution}

Há vários motivos para a replicação falhar. Este artigo explica a abordagem que se pode adotar ao analisar essas questões.

**As replicações estão sendo acionadas ao clicar no botão Ativar? Se NÃO, faça o seguinte:**

1. Vá para /crx/explorer e faça logon como administrador.
1. Abra &quot;Content Explorer&quot;
1. Verifique se existe um nó /bin/replicate ou /bin/replicate.json. Se o nó existir, exclua-o e salve-o.

**As replicações estão sendo enfileiradas nas filas do agente de replicação?**

Para verificar isso, acesse /etc/replication/agents.author.html e clique nos agentes de replicação para verificar.

**Se uma fila de agente ou algumas filas de agente estiverem travadas:**

1. A fila mostra o status **bloqueado**? Em caso afirmativo, a instância de publicação não está em execução ou não está totalmente responsiva? Verifique a instância de publicação para ver o que há de errado com ela (ou seja, verifique os registros e veja se há um erro OutOfMemory ou algum outro problema). Então, se for apenas lento, pegue os despejos de thread e analise-os.
1. O status da fila mostra **A fila está ativa - # pendente**? Basicamente, o trabalho de replicação pode estar preso em uma leitura de soquete aguardando a resposta da instância pública ou do dispatcher. Isso pode significar que a instância de publicação ou o dispatcher está com carga alta ou preso em um bloqueio. Tire lixeiras do autor e publique neste caso.

   * Abra os despejos de thread do autor em um analisador de despejo de thread, verifique se ele mostra que o trabalho de evento de sling do agente de replicação está preso em um soqueteRead.
   * Abra os despejos de thread da publicação em um analisador de despejo de thread, analise o que pode estar fazendo com que a instância de publicação não responda. Você deve ver um thread com POST /bin/receive em seu nome, que é o thread que recebe a replicação do autor.

**Se todas as filas de agente estiverem travadas**

1. É possível que um determinado conteúdo não possa ser serializado em /var/Replication/data devido a danos no repositório ou a algum outro problema. Verifique se há um erro relacionado no logs/error.log. Para eliminar o item de replicação incorreto, faça o seguinte:

   1. Vá para https://&lt;host>:&lt;porta>/crx/de e faça logon como usuário administrador.
   1. Clique em &quot;Ferramentas&quot; no menu superior.
   1. Clique no botão de lupa.
   1. Selecione &quot;XPath&quot; como Tipo.
   1. Na caixa &quot;Query&quot;, digite este query /jcr:root/var/eventing/jobs//element(*,slingevent:Job) por @slingevent:created
   1. Clique em &quot;Pesquisar&quot;
   1. Nos resultados, os itens principais são os trabalhos de eventos de sling mais recentes. Clique em cada uma e localize as replicações presas que correspondem ao que aparece na parte superior da fila.

1. Pode haver algo errado com o envio de filas de trabalho da estrutura de eventos. Tente reiniciar o pacote org.apache.sling.evento no /system/console.
1. Pode ser que o processamento de trabalho esteja completamente desligado. Você pode verificar isso em Console do Felix na guia Eventos do Sling. Verifique se ele é exibido - Apache Sling Event (O PROCESSAMENTO DE TAREFA ESTÁ DESATIVADO!)

   * Em caso afirmativo, marque a guia Configuração do Manipulador de Eventos de trabalho Apache Sling no console do Felix. Pode ser que a caixa de seleção &#39;Processamento de trabalho ativado&#39; esteja desmarcada. Se essa opção estiver marcada e ainda assim for exibida, verifique se há alguma sobreposição em /apps/system/config que esteja desativando o processamento da tarefa. Tente criar um nó osgi:config para jobmanager.enabled com um valor booliano para true e verifique novamente se a ativação começou e se não há mais trabalhos na fila.

1. Também pode ser que a configuração DefaultJobManager fique em um estado inconsistente. Isso pode ocorrer quando alguém modifica manualmente a configuração do &quot;Apache Sling Job Evento Handler&quot; por meio do OSGiconsole (por exemplo, desative e reative a propriedade &quot;Job Processing Enabled&quot; e Salve a configuração).

   * Nesse ponto, a configuração DefaultJobManager armazenada em crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config entra em um estado inconsistente. E mesmo que a propriedade &#39;Apache Sling Job Evento Handler&#39; mostre &#39;Job Processing Enabled&#39; (Processamento de trabalho ativado) para estar em estado marcado, quando você navega até a guia Sling Eventing, ela mostra a mensagem - JOB PROCESSING IS DISABLED (O PROCESSAMENTO DE TAREFA ESTÁ DESATIVADO) e a replicação não funciona.
   * Para resolver esse problema, é necessário navegar até a página Configuração do console do OSGi e excluir a configuração do &quot;Manipulador de Eventos de trabalho Apache Sling&quot;. Em seguida, reinicie o nó Principal do cluster para obter a configuração de volta a um estado consistente. Isso deve corrigir o problema e a replicação será start de funcionar novamente.

**Criar um arquivo Replication.log**

Às vezes, pode ser muito útil definir todos os logs de replicação a serem adicionados em um arquivo de log separado no nível DEBUG. Para fazer isso:

1. Acesse https://host:port/system/console/configMgr e faça logon como administrador.
1. Localize a fábrica do Apache Sling Logging Logger e crie uma instância clicando no botão **+** à direita da configuração de fábrica. Isso criará um novo agente de log.
1. Defina a configuração desta forma:

   * Nível de registro: DEPURAÇÃO
   * Caminho do arquivo de log: logs/replication.log
   * Categorias: com.day.cq.replication

1. Se você suspeitar que o problema esteja relacionado ao envio de eventos/trabalhos de qualquer forma, você também poderá adicionar esse pacote java em categoria:org.apache.sling.evento

## Pausando Fila do Agente de Replicação {#pausing-replication-agent-queue}

Às vezes, pode ser adequado pausar a fila de replicação para reduzir a carga no sistema do autor, sem desativá-la. Atualmente, isso só é possível por meio de uma hack de configuração temporária de uma porta inválida. A partir da versão 5.4, você pode ver o botão de pausa na fila do agente de replicação, ele tem algumas limitações

1. O estado não é persistente, o que significa que se você reiniciar um servidor ou um pacote de replicação for reciclado, ele retornará ao estado de execução.
1. A pausa fica ociosa por um período mais curto (OOB 1 hora após nenhuma atividade com replicação por outros processos) e não por um tempo mais longo. Porque há um recurso no sling que evita os encadeamentos ociosos. Basicamente, verifique se um thread de fila de trabalhos não está sendo utilizado por mais tempo, se for esse o caso, iniciará os ciclos de limpeza. Devido ao ciclo de limpeza, ele interrompe o thread e, portanto, a configuração pausada é perdida. Como os trabalhos são persistentes, ele inicia um novo thread para processar a fila que não tem detalhes da configuração pausada. Devido a esta fila, o estado de execução é transformado.

## As permissões da página não são replicadas na Ativação do usuário {#page-permissions-are-not-replicated-on-user-activation}

As permissões de página não são replicadas porque são armazenadas nos nós aos quais o acesso é concedido, não com o usuário.

Em geral, as permissões de página não devem ser replicadas do autor para publicação e não são, por padrão. Isso porque os direitos de acesso devem ser diferentes nesses dois ambientes. Portanto, é recomendável configurar ACLs na publicação separadamente do autor.

## Fila de replicação bloqueada ao replicar informações de namespace do Autor para Publicar {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

Em alguns casos, a fila de replicação é bloqueada ao tentar replicar informações de namespace da instância do autor para a instância de publicação. Isso ocorre porque o usuário de replicação não tem `jcr:namespaceManagement` privilégio. Para evitar esse problema, verifique se:

* O usuário de replicação (conforme configurado na guia [Transport](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)>User) também existe na instância Publicar.
* O usuário tem privilégios de leitura e gravação no caminho em que o conteúdo está instalado.
* O usuário tem `jcr:namespaceManagement` privilégio no nível do repositório. Você pode conceder o privilégio da seguinte maneira:

1. Faça logon no CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) como administrador.
1. Clique na guia **Controle de acesso**.
1. Selecione **Repositório**.
1. Clique em **Adicionar entrada** (o ícone de adição).
1. Insira o nome do usuário.
1. Selecione `jcr:namespaceManagement` na lista de privilégios.
1. Clique em OK.

