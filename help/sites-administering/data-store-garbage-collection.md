---
title: Coleta de lixo do armazenamento de dados
seo-title: Coleta de lixo do armazenamento de dados
description: Saiba como configurar a Coleta de lixo do Data Store para liberar espaço em disco.
seo-description: Saiba como configurar a Coleta de lixo do Data Store para liberar espaço em disco.
uuid: 49488a81-986a-4d1a-96c8-aeb6595fc094
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5b1e46c5-7e56-433e-b62e-2a76ea7be0fd
docset: aem65
translation-type: tm+mt
source-git-commit: 0eda6ee61acf737abc91d1e5df731e719663b3f2
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

Quando um ativo WCM convencional é removido, a referência ao registro do armazenamento de dados subjacente pode ser removida da hierarquia do nó, mas o próprio registro do armazenamento de dados permanece. Esse registro de armazenamento de dados não referenciado se torna &quot;lixo&quot; que não precisa ser retido. Nos casos em que existem vários ativos de lixo, é benéfico livrar-se deles para preservar espaço e otimizar o desempenho de backup e manutenção do sistema de arquivos.

Na maioria das vezes, um aplicativo WCM tende a coletar informações, mas não a excluir informações com tanta frequência. Embora novas imagens sejam adicionadas, mesmo após a substituição de versões antigas, o sistema de controle de versão ainda mantém o antigo e oferece suporte para reverter para ele, se necessário. Assim, a maior parte do conteúdo que consideramos como um acréscimo ao sistema é efetivamente armazenado permanentemente. Então qual é a fonte típica de &quot;lixo&quot; no repositório que podemos querer limpar?

AEM usa o repositório como armazenamento para várias atividades internas e domésticas:

* Pacotes criados e baixados
* Arquivos temporários criados para a replicação de publicação
* Cargas do fluxo de trabalho
* Ativos criados temporariamente durante a renderização do DAM

Quando qualquer um desses objetos temporários for grande o suficiente para exigir armazenamento no armazenamento de dados, e quando o objeto acabar descontinuando o uso, o próprio registro do armazenamento de dados permanecerá como &quot;lixo&quot;. Em um autor/aplicativo de publicação típico do WCM, a maior fonte de lixo desse tipo é geralmente o processo de publicação da ativação. Quando os dados estão sendo replicados para Publicar, eles serão coletados primeiro em coleções em um formato de dados eficiente chamado &quot;Durbo&quot; e armazenados no repositório em `/var/replication/data`. Geralmente, os conjuntos de dados são maiores que o limite de tamanho crítico para o armazenamento de dados e, portanto, acabam armazenados como registros do armazenamento de dados. Quando a replicação for concluída, o nó em `/var/replication/data` será excluído, mas o registro do armazenamento de dados permanecerá como &quot;lixo&quot;.

Outra fonte de lixo recuperável são os pacotes. Os dados do pacote, como todo o resto, são armazenados no repositório e, portanto, para pacotes maiores que 4 KB, no armazenamento de dados. Durante um projeto de desenvolvimento ou com o passar do tempo mantendo um sistema, os pacotes podem ser criados e recriados várias vezes, resultando em um novo registro de armazenamento de dados, órfando o registro da compilação anterior.

## Como funciona a coleta de lixo do armazenamento de dados? {#how-does-data-store-garbage-collection-work}

Se o repositório tiver sido configurado com um armazenamento de dados externo, [a coleta de lixo do armazenamento de dados será executada automaticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) como parte da Janela de manutenção semanal. O administrador do sistema também pode [executar a coleta de lixo do armazenamento de dados manualmente](#running-data-store-garbage-collection) conforme necessário. Em geral, recomenda-se que a coleta de lixo do armazenamento de dados seja executada periodicamente, mas que os seguintes fatores sejam considerados no planejamento das coleta de lixo do armazenamento de dados:

* As coleções de lixo do armazenamento de dados levam tempo e podem afetar o desempenho, portanto, devem ser planejadas de acordo.
* A remoção de registros de lixo do armazenamento de dados não afeta o desempenho normal, portanto, isso não é uma otimização de desempenho.
* Se a utilização do armazenamento e fatores relacionados, como o tempo de backup, não forem motivo de preocupação, a coleta de lixo do armazenamento de dados poderá ser adiada com segurança.

O coletor de lixo do armazenamento de dados primeiro anota o carimbo de data e hora atual quando o processo é iniciado. A coleção é então realizada usando um algoritmo de padrão de marca/varredura de vários passos.

Na primeira fase, o coletor de lixo do armazenamento de dados realiza uma ampla travessia de todo o conteúdo do repositório. Para cada objeto de conteúdo que tem uma referência a um registro de armazenamento de dados, ele localizou o arquivo no sistema de arquivos, realizando uma atualização de metadados — modificando o atributo &quot;última modificação&quot; ou MTIME. Nesse ponto, os arquivos acessados por essa fase se tornam mais recentes do que o carimbo de data e hora da linha de base inicial.

Na segunda fase, o coletor de lixo do armazenamento de dados atravessa a estrutura do diretório físico do armazenamento de dados da mesma forma que um &quot;localizar&quot;. Examinou o atributo &quot;última modificação&quot; ou MTIME do ficheiro e efetua a seguinte determinação:

* Se o MTIME for mais recente do que o carimbo de data e hora da linha de base inicial, o arquivo foi encontrado na primeira fase ou é um arquivo totalmente novo que foi adicionado ao repositório durante o processo de coleta. Em qualquer destes casos, o registro é considerado ativo e o processo não é apagado.
* Se o MTIME for anterior ao carimbo de data e hora da linha de base inicial, o arquivo não será um arquivo referenciado ativamente e será considerado um lixo removível.

Essa abordagem funciona bem para um único nó com um armazenamento de dados privado. No entanto, o armazenamento de dados pode ser compartilhado e, se for esse o caso, as referências ativas potencialmente ativas a registros de armazenamento de dados de outros repositórios não serão verificadas e os arquivos referenciados ativos poderão ser removidos por engano. É imperativo que o administrador do sistema entenda a natureza compartilhada do armazenamento de dados antes de planejar qualquer coleta de lixo, e use apenas o processo de coleta de lixo do armazenamento de dados integrado quando se sabe que o armazenamento de dados não é compartilhado.

>[!NOTE]
>
>Ao executar a coleta de lixo em uma configuração de armazenamento de dados clusterizado ou compartilhado (com Mongo ou Segment Tar), o log pode exibir avisos sobre a incapacidade de excluir determinadas IDs de blob. Isso ocorre porque as IDs de blob excluídas em uma coleta de lixo anterior são referenciadas incorretamente novamente por outro cluster ou nós compartilhados que não têm informações sobre as exclusões de ID. Como resultado, quando a coleta de lixo é executada, ele registra um aviso ao tentar excluir uma ID que já foi excluída na última execução. Esse comportamento não afeta o desempenho nem a funcionalidade.

## Execução da Coleta de Lixo do Data Store {#running-data-store-garbage-collection}

Existem três maneiras de executar a coleta de lixo do armazenamento de dados, dependendo da configuração do armazenamento de dados em que o AEM está sendo executado:

1. Via [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md) - um mecanismo de coleta de lixo normalmente usado para limpeza de armazenamento de nó.

1. Via [Coleta de Lixo do Repositório de Dados](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) - um mecanismo de coleta de lixo específico para armazenamentos de dados externos, disponível no Painel Operations.
1. Através do [Console JMX](/help/sites-administering/jmx-console.md).

Se TarMK estiver sendo usado como armazenamento de nó e armazenamento de dados, a Limpeza de revisão poderá ser usada para a coleta de lixo do armazenamento de nó e do armazenamento de dados. No entanto, se um armazenamento de dados externo estiver configurado, como Arquivo de Armazenamento de Dados do Sistema de Arquivos, a coleta de lixo do armazenamento de dados deverá ser explicitamente acionada separadamente da Limpeza de Revisão. A coleta de lixo do armazenamento de dados pode ser acionada pelo Painel Operações ou pelo Console JMX.

A tabela abaixo mostra o tipo de coleta de lixo do armazenamento de dados que precisa ser usado para todas as implantações do armazenamento de dados compatíveis no AEM 6:

<table>
 <tbody>
  <tr>
   <td><strong>Armazenamento de nós</strong><br /> </td>
   <td><strong>Armazenamento de dados</strong></td>
   <td><strong>Mecanismo de coleta de lixo</strong><br /> </td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>TarMK</td>
   <td>Limpeza de revisão (os binários são alinhados com o Repositório de segmentos)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>Sistema de arquivos externo</td>
   <td><p>Tarefa de coleta de lixo do Data Store por meio do Painel Operações</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Tarefa de coleta de lixo do Data Store por meio do Painel Operações</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>Sistema de arquivos externo</td>
   <td><p>Tarefa de coleta de lixo do Data Store por meio do Painel Operações</p> <p>Console JMX</p> </td>
  </tr>
 </tbody>
</table>

### Execução da coleta de lixo do armazenamento de dados por meio do Painel Operations {#running-data-store-garbage-collection-via-the-operations-dashboard}

A Janela de manutenção semanal integrada, disponível através do [Painel de operações](/help/sites-administering/operations-dashboard.md), contém uma tarefa integrada para acionar a Coleta de lixo do armazenamento de dados às 01h dos domingos.

Se você precisar executar a coleta de lixo do armazenamento de dados fora desse tempo, ela poderá ser acionada manualmente pelo Painel Operações.

Antes de executar a coleta de lixo do armazenamento de dados, verifique se não há backups em execução no momento.

1. Abra o Painel Operações por **Navegação** -> **Ferramentas** -> **Operações** -> **Manutenção**.
1. Clique ou toque na **Janela de manutenção semanal**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Selecione a tarefa **Coleta de lixo do Data Store** e clique ou toque no ícone **Executar**.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. A coleta de lixo do armazenamento de dados é executada e seu status é exibido no painel.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>A tarefa de coleta de lixo do armazenamento de dados só estará visível se você tiver configurado um armazenamento de dados de arquivo externo. Consulte [Configurando armazenamentos de nó e armazenamentos de dados no AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obter informações sobre como configurar um armazenamento de dados de arquivo.

### Execução da coleta de lixo do armazenamento de dados por meio do console JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Esta seção trata da execução manual da coleta de lixo do armazenamento de dados por meio do Console JMX. Se a instalação estiver configurada sem um armazenamento de dados externo, isso não se aplica à instalação. Em vez disso, consulte as instruções sobre como executar a limpeza Revisão em [Manutenção do Repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Se você estiver executando o TarMK com um armazenamento de dados externo, é necessário executar a Limpeza de revisão primeiro para que a coleta de lixo seja eficaz.

Para executar a coleta de lixo:

1. No Console de gerenciamento do Apache Felix OSGi, realce a guia **Main** e selecione **JMX** no seguinte menu.
1. Em seguida, procure e clique em **Gerenciador de repositório** MBean (ou vá para `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Clique em **startDataStoreGC(boolean markOnly)**.
1. digite &quot;`true`&quot; para o parâmetro `markOnly`, se necessário:

   | **Opção** | **Descrição** |
   |---|---|
   | booleano markOnly | Defina como true para marcar apenas referências e não para verificar a operação de marcação e varredura. Esse modo deve ser usado quando o BlobStore subjacente for compartilhado entre vários repositórios diferentes. Para todos os outros casos, defina-o como falso para executar a coleta completa de lixo. |

1. Clique em **Chamar**. O CRX executa a coleta de lixo e indica quando ela foi concluída.

>[!NOTE]
>
>A coleta de lixo do armazenamento de dados não coletará arquivos que foram excluídos nas últimas 24 horas.

>[!NOTE]
>
>A tarefa de coleta de lixo do armazenamento de dados só será start se você tiver configurado um armazenamento de dados externo. Se um armazenamento de dados de arquivo externo não tiver sido configurado, a tarefa retornará a mensagem `Cannot perform operation: no service of type BlobGCMBean found` após chamar. Consulte [Configurando armazenamentos de nó e armazenamentos de dados no AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obter informações sobre como configurar um armazenamento de dados de arquivo.

## Automatizando a coleta de lixo do armazenamento de dados {#automating-data-store-garbage-collection}

Se possível, a coleta de lixo do armazenamento de dados deve ser executada quando houver pouca carga no sistema, por exemplo pela manhã.

A Janela de manutenção semanal integrada, disponível através do [Painel de operações](/help/sites-administering/operations-dashboard.md), contém uma tarefa integrada para acionar a Coleta de lixo do armazenamento de dados às 01h dos domingos. Você também deve verificar se nenhum backup está sendo executado no momento. O start da janela de manutenção pode ser personalizado por meio do painel, conforme necessário.

>[!NOTE]
>
>O motivo para não executá-lo simultaneamente é que os arquivos antigos (e não utilizados) do armazenamento de dados também tenham backup, de modo que, se for necessário reverter para uma revisão antiga, os binários ainda estarão lá no backup.

Se você não quiser executar a coleta de lixo do armazenamento de dados com a Janela de manutenção semanal no Painel Operações, ela também poderá ser automatizada usando os clientes HTTP wget ou curl. Este é um exemplo de como automatizar o backup usando o curl:

>[!CAUTION]
>
>No exemplo a seguir, comandos `curl` podem ser necessários vários parâmetros configurados para a sua instância; por exemplo, o nome do host ( `localhost`), a porta ( `4502`), a senha do administrador ( `xyz`) e vários parâmetros para a coleta de lixo do armazenamento de dados real.

Este é um exemplo de comando curl para chamar a coleta de lixo do armazenamento de dados por meio da linha de comando:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

O comando curl retorna imediatamente.

## Verificando a consistência do armazenamento de dados {#checking-data-store-consistency}

A verificação de consistência do armazenamento de dados reportará todos os binários do armazenamento de dados ausentes, mas que ainda são referenciados. Para start de uma verificação de consistência, siga estas etapas:

1. Vá para o console JMX. Para obter informações sobre como usar o console JMX, consulte [este artigo](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Procure a Mbean **BlobGarbageCollection** e clique nela.
1. Clique no link `checkConsistency()`.

Depois que a verificação de consistência for concluída, uma mensagem mostrará o número de binários reportados como ausentes. Se o número for maior que 0, verifique `error.log` para obter mais detalhes sobre os binários ausentes.

Abaixo, você encontrará um exemplo de como os binários ausentes são reportados nos registros:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```

