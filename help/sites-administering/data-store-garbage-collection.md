---
title: Coleta de lixo do armazenamento de dados
description: Saiba como configurar a Coleta de lixo do armazenamento de dados para liberar espaço em disco.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 0dc4a8ce-5b0e-4bc9-a6f5-df2a67149e22
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 0%

---

# Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

Quando um ativo WCM convencional é removido, a referência ao registro de armazenamento de dados subjacente pode ser removida da hierarquia do nó, mas o próprio registro de armazenamento de dados permanece. Esse registro de armazenamento de dados não referenciado torna-se &quot;lixo&quot;, que não precisa ser retido. Nos casos em que existem vários ativos de lixo, é benéfico eliminá-los para preservar espaço e otimizar o desempenho de backup e manutenção do sistema de arquivos.

Na maioria das vezes, um aplicativo WCM tende a coletar informações, mas não a excluí-las com quase frequência. Embora novas imagens sejam adicionadas, mesmo substituindo versões antigas, o sistema de controle de versão ainda retém a antiga e permite a reversão para ela, se necessário. Dessa forma, a maior parte do conteúdo que adicionamos ao sistema é armazenada permanentemente. Então, qual é a fonte típica de &quot;lixo&quot; no repositório que podemos querer limpar?

O AEM usa o repositório como armazenamento para várias atividades internas e de manutenção do sistema:

* Pacotes criados e baixados
* Arquivos temporários criados para replicação de publicação
* Cargas de fluxo de trabalho
* Ativos criados temporariamente durante a renderização do DAM

Quando qualquer um desses objetos temporários é grande o suficiente para exigir armazenamento no armazenamento de dados e quando o objeto eventualmente passa para fora de uso, o próprio registro do armazenamento de dados permanece como &quot;lixo&quot;. Em um aplicativo WCM típico de criação/publicação, a maior fonte de lixo desse tipo é geralmente o processo de ativação de publicação. Quando os dados estiverem sendo replicados para publicação, eles serão coletados primeiro em coleções em um formato de dados eficiente chamado &quot;Durbo&quot; e armazenados no repositório em `/var/replication/data`. Os pacotes de dados geralmente são maiores que o limite de tamanho crítico do armazenamento de dados e, portanto, são armazenados como registros de armazenamento de dados. Quando a replicação é concluída, o nó em `/var/replication/data` é excluído, mas o registro de armazenamento de dados permanece como &quot;lixo&quot;.

Outra fonte de lixo recuperável são os pacotes. Os dados do pacote, como tudo o mais, são armazenados no repositório e, portanto, para pacotes com mais de 4 KB, no armazenamento de dados. Durante um projeto de desenvolvimento ou ao longo do tempo enquanto mantém um sistema, os pacotes podem ser criados e recriados muitas vezes, cada criação resultando em um novo registro de armazenamento de dados, tornando-o órfão do registro da criação anterior.

## Como funciona a coleta de lixo do armazenamento de dados? {#how-does-data-store-garbage-collection-work}

Se o repositório tiver sido configurado com um armazenamento de dados externo, [a coleta de lixo do armazenamento de dados será executada automaticamente](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) como parte da Janela de manutenção semanal. O administrador do sistema também pode [executar coleta de lixo do armazenamento de dados manualmente](#running-data-store-garbage-collection) conforme necessário. Em geral, recomenda-se que a coleta de lixo do armazenamento de dados seja executada periodicamente, mas que os seguintes fatores sejam considerados no planejamento das coletas de lixo do armazenamento de dados:

* As coletas de lixo do armazenamento de dados levam tempo e podem afetar o desempenho, portanto, devem ser planejadas adequadamente.
* A remoção de registros de lixo do armazenamento de dados não afeta o desempenho normal, portanto, não é uma otimização de desempenho.
* Se a utilização do armazenamento e fatores relacionados, como tempos de backup, não forem uma preocupação, a coleta de lixo do armazenamento de dados poderá ser adiada com segurança.

O coletor de lixo do armazenamento de dados primeiro faz uma observação do carimbo de data e hora atual quando o processo começa. A recolha é então realizada utilizando um algoritmo de marca multipasso/padrão de varrimento.

Na primeira fase, o coletor de lixo do armazenamento de dados realiza uma passagem abrangente de todo o conteúdo do repositório. Para cada objeto de conteúdo que tem uma referência a um registro de armazenamento de dados, ele localizou o arquivo no sistema de arquivos, executando uma atualização de metadados — modificando o atributo &quot;última modificação&quot; ou MTIME. Nesse ponto, os arquivos acessados por essa fase se tornam mais recentes que o carimbo de data e hora da linha de base inicial.

Na segunda fase, o coletor de lixo do armazenamento de dados atravessa a estrutura do diretório físico do armazenamento de dados da mesma forma que uma &quot;localização&quot;. Examinou o atributo &quot;last modified&quot; ou MTIME do arquivo e faz a seguinte determinação:

* Se o MTIME for mais recente que o carimbo de data e hora da linha de base inicial, o arquivo foi encontrado na primeira fase ou é um arquivo totalmente novo que foi adicionado ao repositório enquanto o processo de coleta estava em andamento. Em qualquer destes casos, o registro é considerado ativo e o processo não é apagado.
* Se o MTIME for anterior ao carimbo de data e hora da linha de base inicial, o arquivo não é um arquivo referenciado ativamente e é considerado lixo removível.

Essa abordagem funciona bem para um único nó com um armazenamento de dados privado. No entanto, o armazenamento de dados pode ser compartilhado e, se for, significa que as referências potencialmente ativas para registros do armazenamento de dados de outros repositórios não são verificadas e os arquivos referenciados ativos podem ser removidos por engano. É fundamental que o administrador do sistema entenda a natureza compartilhada do armazenamento de dados antes de planejar qualquer coleta de lixo e use o processo simples de coleta de lixo do armazenamento de dados integrado quando for conhecido que o armazenamento de dados não é compartilhado.

>[!NOTE]
>
>Ao executar a coleta de lixo em uma configuração de armazenamento de dados em cluster ou compartilhado (com Mongo ou Segment Tar), o log pode exibir avisos sobre a incapacidade de excluir determinadas IDs de blob. Isso acontece porque as IDs de blob excluídas em uma coleta de lixo anterior são referenciadas incorretamente novamente por outros nós de cluster ou compartilhados que não têm informações sobre as exclusões de ID. Como resultado, quando a coleta de lixo é executada, ele registra um aviso ao tentar excluir uma ID que já foi excluída na última execução. Esse comportamento não afeta o desempenho ou a funcionalidade.

## Executando Coleta de Lixo do Repositório de Dados {#running-data-store-garbage-collection}

Há três maneiras de executar a coleta de lixo do armazenamento de dados, dependendo da configuração do armazenamento de dados no qual o AEM está sendo executado:

1. Via [Limpeza de revisão](/help/sites-deploying/revision-cleanup.md) - um mecanismo de coleta de lixo geralmente usado para limpeza de armazenamento de nós.

1. Via [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-operations-dashboard) - um mecanismo de coleta de lixo específico para armazenamentos de dados externos, disponível no Painel de operações.
1. Através do [Console JMX](/help/sites-administering/jmx-console.md).

Se TarMK estiver sendo usado como armazenamento de nó e armazenamento de dados, a Limpeza de revisão poderá ser usada para a coleta de lixo do armazenamento de nó e do armazenamento de dados. No entanto, se um armazenamento de dados externo estiver configurado, como o Armazenamento de dados do sistema de arquivos, a coleta de lixo do armazenamento de dados deverá ser acionada explicitamente, separado da Limpeza de revisão. A coleta de lixo do armazenamento de dados pode ser acionada pelo Painel de operações ou pelo Console JMX.

A tabela abaixo mostra o tipo de coleta de lixo do armazenamento de dados que precisa ser usado para todas as implantações de armazenamento de dados compatíveis com o AEM 6:

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
   <td>Limpeza de revisão (os binários estão alinhados com o Repositório de segmentos)</td>
  </tr>
  <tr>
   <td>TarMK</td>
   <td>Sistema de arquivos externo</td>
   <td><p>Tarefa Coleta de Lixo do Armazenamento de Dados via Painel de Operações</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>MongoDB</td>
   <td><p>Tarefa Coleta de Lixo do Armazenamento de Dados via Painel de Operações</p> <p>Console JMX</p> </td>
  </tr>
  <tr>
   <td>MongoDB</td>
   <td>Sistema de arquivos externo</td>
   <td><p>Tarefa Coleta de Lixo do Armazenamento de Dados via Painel de Operações</p> <p>Console JMX</p> </td>
  </tr>
 </tbody>
</table>

### Execução da coleta de lixo do armazenamento de dados por meio do painel de operações {#running-data-store-garbage-collection-via-the-operations-dashboard}

A Janela de manutenção semanal integrada, disponível por meio da [Painel de operações](/help/sites-administering/operations-dashboard.md), contém uma tarefa interna para acionar a Coleta de lixo do armazenamento de dados às 1:00 aos domingos.

Se você precisar executar a coleta de lixo do armazenamento de dados fora desse período, ela poderá ser acionada manualmente por meio do Painel de operações.

Antes de executar a coleta de lixo do armazenamento de dados, você deve verificar se nenhum backup está em execução no momento.

1. Abra o Painel de operações em **Navegação** > **Ferramentas** > **Operações** > **Manutenção**.
1. Clique em **Janela de manutenção semanal**.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Selecione o **Coleta de lixo do armazenamento de dados** tarefa e, em seguida, clique na guia **Executar** ícone.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. A coleta de lixo do armazenamento de dados é executada e seu status é exibido no painel.

   ![chlimage_1-66](assets/chlimage_1-66.png)

>[!NOTE]
>
>A tarefa Coleta de Lixo do Armazenamento de Dados só estará visível se você tiver configurado um armazenamento de dados de arquivo externo. Consulte [Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obter informações sobre como configurar um armazenamento de dados de arquivo.

### Executando a coleta de lixo do armazenamento de dados por meio do console JMX {#running-data-store-garbage-collection-via-the-jmx-console}

Esta seção trata da execução manual da coleta de lixo do armazenamento de dados por meio do Console JMX. Se a sua instalação for configurada sem um armazenamento de dados externo, isso não se aplica à sua instalação. Em vez disso, consulte as instruções sobre como executar a Limpeza de revisão em [Manutenção do repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).

>[!NOTE]
>
>Se você estiver executando o TarMK com um armazenamento de dados externo, é necessário executar a Limpeza de revisão primeiro para que a coleta de lixo seja eficaz.

Para executar a coleta de lixo:

1. No Console de gerenciamento do Apache Felix OSGi, destaque a opção **Principal** e selecione **JMX** no menu a seguir.
1. Em seguida, pesquise por e clique no link **Gerenciador de repositório** MBean (ou vá para `https://<host>:<port>/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Drepository+manager%2Ctype%3DRepositoryManagement`).
1. Clique em **startDataStoreGC(boolean markOnly)**.
1. digite &quot;`true`&quot; para o `markOnly` se necessário:

   | **Opção** | **Descrição** |
   |---|---|
   | boolean markOnly | Defina como verdadeiro para marcar somente as referências e não varrer na operação de marcação e varredura. Esse modo deve ser usado quando o BlobStore subjacente for compartilhado entre vários repositórios diferentes. Para todos os outros casos, defina como falso para executar a coleta de lixo completa. |

1. Clique em **Chamar**. O CRX executa a coleta de lixo e indica quando ela foi concluída.

>[!NOTE]
>
>A coleta de lixo do armazenamento de dados não coletará arquivos que foram excluídos nas últimas 24 horas.

>[!NOTE]
>
>A tarefa de coleta de lixo do armazenamento de dados só será iniciada se você tiver configurado um armazenamento de dados de arquivo externo. Se um armazenamento de dados de arquivo externo não tiver sido configurado, a tarefa retornará a mensagem `Cannot perform operation: no service of type BlobGCMBean found` depois de invocar. Consulte [Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6](/help/sites-deploying/data-store-config.md#file-data-store) para obter informações sobre como configurar um armazenamento de dados de arquivo.

## Automatização da coleta de lixo do armazenamento de dados {#automating-data-store-garbage-collection}

Se possível, a coleta de lixo do armazenamento de dados deve ser executada quando houver pouca carga no sistema, por exemplo, de manhã.

A Janela de manutenção semanal integrada, disponível por meio da [Painel de operações](/help/sites-administering/operations-dashboard.md), contém uma tarefa interna para acionar a Coleta de lixo do armazenamento de dados às 1:00 aos domingos. Você também deve verificar se não há backups em execução no momento. O início da janela de manutenção pode ser personalizado por meio do painel, conforme necessário.

>[!NOTE]
>
>O motivo para não executá-lo simultaneamente é para que os arquivos antigos (e não utilizados) do armazenamento de dados também sejam submetidos a backup, de modo que, se for necessário reverter para uma revisão antiga, os binários ainda estejam lá no backup.

Se você não quiser executar a coleta de lixo do armazenamento de dados com a Janela de manutenção semanal no Painel de operações, ela também poderá ser automatizada usando os clientes HTTP wget ou curl. Este é um exemplo de como automatizar a coleta de lixo usando o curl:

>[!CAUTION]
>
>No exemplo a seguir `curl` comandos vários parâmetros podem precisar ser configurados para sua instância; por exemplo, o nome do host ( `localhost`), porta ( `4502`), senha do administrador ( `xyz`) e vários parâmetros para a coleta de lixo do armazenamento de dados real.

Este é um exemplo de comando curl para chamar a coleta de lixo do armazenamento de dados pela linha de comando:

```shell
curl -u admin:admin -X POST --data markOnly=true  https://localhost:4503/system/console/jmx/org.apache.jackrabbit.oak"%"3Aname"%"3Drepository+manager"%"2Ctype"%"3DRepositoryManagement/op/startDataStoreGC/boolean
```

O comando curl retorna imediatamente.

## Verificando a consistência do armazenamento de dados {#checking-data-store-consistency}

A verificação de consistência do armazenamento de dados relatará todos os binários de armazenamento de dados que estão ausentes, mas ainda são referenciados. Para iniciar uma verificação de consistência, siga estas etapas:

1. Vá para o console JMX. Para obter informações sobre como usar o console JMX, consulte [este artigo](/help/sites-administering/jmx-console.md#using-the-jmx-console).
1. Procure por **BlobGarbageCollection** Mbean e clique nele.
1. Clique em `checkConsistency()` link.

Após a conclusão da verificação de consistência, uma mensagem mostrará o número de binários relatados como ausentes. Se o número for maior que 0, verifique a `error.log` para obter mais detalhes sobre os binários ausentes.

Abaixo, você encontrará um exemplo de como os binários ausentes são relatados nos logs:

```xml
11:32:39.673 INFO [main] MarkSweepGarbageCollector.java:600 Consistency check found [1] missing blobs
```

```xml
11:32:39.673 WARN [main] MarkSweepGarbageCollector.java:602 Consistency check failure intheblob store : DataStore backed BlobStore [org.apache.jackrabbit.oak.plugins.blob.datastore.OakFileDataStore], check missing candidates in file /tmp/gcworkdir-1467352959243/gccand-1467352959243
```
