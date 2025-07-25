---
title: Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6
description: Saiba como configurar armazenamentos de nós e armazenamentos de dados e como executar a coleta de lixo do armazenamento de dados.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '3461'
ht-degree: 1%

---

# Configuração de armazenamentos de nós e armazenamentos de dados no AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introdução {#introduction}

No Adobe Experience Manager (AEM), os dados binários podem ser armazenados independentemente dos nós de conteúdo. Os dados binários são armazenados em um armazenamento de dados, enquanto os nós de conteúdo são armazenados em um armazenamento de nós.

Os armazenamentos de dados e os armazenamentos de nó podem ser configurados usando a configuração OSGi. Cada configuração OSGi é referenciada usando um identificador persistente (PID).

## Etapas de configuração {#configuration-steps}

Para configurar o armazenamento de nós e o armazenamento de dados, execute estas etapas:

1. Copie o arquivo JAR do AEM quickstart para seu diretório de instalação.
1. Crie uma pasta `crx-quickstart/install` no diretório de instalação.
1. Primeiro, configure o armazenamento de nós criando um arquivo de configuração com o nome da opção de armazenamento de nós que você deseja usar no diretório `crx-quickstart/install`.

   Por exemplo, o armazenamento de nós Document (que é a base para a implementação MongoMK do AEM) usa o arquivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite o arquivo e defina suas opções de configuração.
1. Crie um arquivo de configuração com o PID do armazenamento de dados que deseja usar. Edite o arquivo para definir as opções de configuração.

   >[!NOTE]
   >
   >Consulte [Configurações de armazenamento de nós](#node-store-configurations) e [Configurações de armazenamento de dados](#data-store-configurations) para opções de configuração.

1. Inicie o AEM.

## Configurações do armazenamento de nós {#node-store-configurations}

>[!CAUTION]
>
>As versões mais recentes do Oak empregam um novo esquema de nomenclatura e formato para os arquivos de configuração OSGi. O novo esquema de nomenclatura exige que o arquivo de configuração seja nomeado como **.config** e o novo formato exige que os valores sejam digitados. Para obter detalhes, consulte [O Modelo de provisionamento do Apache Sling e Apache SlingStart - Formato de configuração padrão](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Se você atualizar de uma versão mais antiga do Oak, primeiro faça um backup da pasta `crx-quickstart/install`. Após a atualização, restaure o conteúdo da pasta para a instalação atualizada e modifique a extensão dos arquivos de configuração de **.cfg** para **.config**.

### Armazenamento de nós do segmento {#segment-node-store}

O armazenamento de nós de segmento é a base da implementação TarMK da Adobe no AEM6. Ele usa o PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` para configuração.

>[!CAUTION]
>
>O PID para o armazenamento do nó de Segmento foi alterado de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` do AEM 6 para `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` no AEM 6.3. Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Você pode configurar as seguintes opções:

* `repository.home`: Caminho para a página inicial do repositório em que os dados relacionados ao repositório são armazenados. Por padrão, os arquivos de segmento são armazenados no diretório `crx-quickstart/segmentstore`.

* `tarmk.size`: Tamanho máximo de um segmento em MB. O máximo padrão é 256 MB.
* `customBlobStore`: valor booleano indicando que um armazenamento de dados personalizado está sendo usado. O valor padrão é true para o AEM 6.3 e versões posteriores. Antes do AEM 6.3, o padrão era falso.

Este é um exemplo de arquivo `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Armazenamento do nó do documento {#document-node-store}

O armazenamento de nós de documentos é a base da implementação MongoMK do AEM. Ele usa o *PID `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`*. As seguintes opções de configuração estão disponíveis:

* `mongouri`: O [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessário para se conectar ao Banco de Dados Mongo. O padrão é `mongodb://localhost:27017`

* `db`: Nome do banco de dados Mongo. O padrão é **Oak** ``. However, new AEM 6 installations use **aem-author** ``como o nome de banco de dados padrão.

* `cache`: O tamanho do cache em MB. Isso é distribuído entre vários caches usados no DocumentNodeStore. O padrão é `256`

* `changesSize`: Tamanho em MB da coleção limitada usada em Mongo para armazenar a saída do diff em cache. O padrão é `256`

* `customBlobStore`: valor booleano indicando que um armazenamento de dados personalizado está sendo usado. O padrão é `false`.

Este é um exemplo de arquivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurações do armazenamento de dados {#data-store-configurations}

Ao lidar com um grande número de binários, é recomendável que um armazenamento de dados externo seja usado em vez dos armazenamentos de nó padrão para maximizar o desempenho.

Por exemplo, se o seu projeto exigir muitos ativos de mídia, armazená-los no Arquivo ou no Armazenamento de dados S3 torna mais rápido acessá-los do que armazená-los diretamente em um MongoDB.

O armazenamento de dados de arquivos oferece melhor desempenho do que o MongoDB, e as operações de backup e restauração do Mongo também são mais lentas com um grande número de ativos.

Os detalhes sobre os diferentes armazenamentos de dados e configurações são descritos abaixo.

>[!NOTE]
>
>Para habilitar Repositórios de Dados personalizados, verifique se `customBlobStore` está definido como `true` no respectivo arquivo de configuração de Repositório de Nós ([repositório de nós de segmentos](/help/sites-deploying/data-store-config.md#segment-node-store) ou [repositório de nós de documentos](/help/sites-deploying/data-store-config.md#document-node-store)).

### Armazenamento de dados do arquivo {#file-data-store}

Esta é a implementação do [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) presente no Jackrabbit 2. Ele fornece uma maneira de armazenar os dados binários como arquivos normais no sistema de arquivos. Ele usa o PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Estas opções de configuração estão disponíveis:

* `repository.home`: Caminho para a página inicial do repositório sob a qual vários dados relacionados ao repositório são armazenados. Por padrão, os arquivos binários seriam armazenados no diretório `crx-quickstart/repository/datastore`

* `path`: Caminho para o diretório no qual os arquivos serão armazenados. Se especificado, tem precedência sobre o valor `repository.home`

* `minRecordLength`: O tamanho mínimo em bytes de um arquivo armazenado no repositório de dados. O conteúdo binário menor que esse valor seria incorporado.

>[!NOTE]
>
>Ao usar um NAS para armazenar armazenamentos de dados de arquivos compartilhados, certifique-se de usar apenas dispositivos de alto desempenho para evitar problemas de desempenho.

## Armazenamento de dados Amazon S3 {#amazon-s-data-store}

O AEM pode ser configurado para armazenar dados no S3 (Simple Storage Service, serviço simples de armazenamento) da Amazon. Ele usa o PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` para configuração.

>[!NOTE]
>
>O AEM 6.5 é compatível com o armazenamento de dados no S3 da Amazon. No entanto, o suporte não se estende ao armazenamento de dados em outras plataformas, cujos fornecedores podem ter suas próprias implementações das APIs S3 da Amazon.

Para ativar a funcionalidade de armazenamento de dados do S3, um pacote de recursos contendo o Conector de armazenamento de dados do S3 deve ser baixado e instalado. Acesse o [Repositório do Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) e baixe a versão mais recente das versões 1.10.x do pacote de recursos (por exemplo, com.adobe.granite.oak.s3connector-1.10.0.zip). Além disso, baixe e instale o service pack mais recente da AEM, conforme listado na página [Notas de versão do AEM 6.5](/help/release-notes/release-notes.md).

>[!NOTE]
>
>Ao usar o AEM com TarMK, os binários serão armazenados por padrão no `FileDataStore`. Para usar TarMK com o S3 Datastore, você deve iniciar o AEM usando o modo de execução `crx3tar-nofds`, por exemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Após o download, você pode instalar e configurar o S3 Connector da seguinte maneira:

1. Extraia o conteúdo do arquivo zip do pacote de recursos para uma pasta temporária.

1. Vá para a pasta temporária e navegue até o seguinte local:

   ```xml
   jcr_root/libs/system/install
   ```

   Copiar todo o conteúdo do local acima para `<aem-install>/crx-quickstart/install.`

1. Se o AEM já estiver configurado para funcionar com o armazenamento Tar ou MongoDB, remova todos os arquivos de configuração existentes da pasta ***&lt;aem-install>**/*crx-quickstart*/*install* antes de continuar. Os arquivos que devem ser removidos são:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retorne ao local temporário onde o pacote de recursos foi extraído e copie o conteúdo da seguinte pasta:

   * `jcr_root/libs/system/config`

   para

   * `<aem-install>/crx-quickstart/install`

   Copie apenas os arquivos de configuração necessários para sua configuração atual. Para um armazenamento de dados dedicado e uma configuração de armazenamento de dados compartilhado, copie o arquivo `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >Em uma configuração de cluster, execute as etapas acima em todos os nós do cluster, um por um. Além disso, certifique-se de usar as mesmas configurações de S3 para todos os nós.

1. Edite o arquivo e adicione as opções de configuração exigidas pela configuração.
1. Inicie o AEM.

## Atualização para uma nova versão do S3 Connector 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Para atualizar para uma nova versão do conector S3 1.10.x (por exemplo, de 1.10.0 para 1.10.4), siga estas etapas:

1. Pare a instância do AEM.

1. Navegue até `<aem-install>/crx-quickstart/install/15` na pasta de instalação do AEM e faça um backup de seu conteúdo.
1. Após o backup, exclua a versão antiga do S3 Connector e suas dependências excluindo todos os arquivos jar na pasta `<aem-install>/crx-quickstart/install/15`, por exemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Os nomes de arquivo apresentados acima são usados apenas para fins ilustrativos.

1. Baixe a versão mais recente do pacote de recursos 1.10.x do [Repositório do Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Descompacte o conteúdo em uma pasta separada e navegue até `jcr_root/libs/system/install/15`.
1. Copie os arquivos jar para **&lt;aem-install>**/crx-quickstart/install/15 na pasta de instalação do AEM.
1. Inicie o AEM e verifique a funcionalidade do conector.

Você pode usar o arquivo de configuração com as opções detalhadas abaixo.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Opções de arquivo de configuração do S3 Connector {#s3-connector-configuration-file-options}

>[!NOTE]
>
>O conector S3 é compatível com autenticação de usuário do IAM e autenticação de função do IAM. Para usar a autenticação de função do IAM, omita os valores `accessKey` e `secretKey` do arquivo de configuração. O conector S3 assumirá como padrão a [função IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) atribuída à instância.

| Chave | Descrição | Padrão | Obrigatório |
| --- | --- | --- | --- |
| accessKey | ID da Chave de Acesso para o usuário do IAM com acesso ao bucket. | | Sim, quando as funções IAM não estiverem sendo usadas. |
| secretKey | Chave de acesso secreta para o usuário do IAM com acesso ao bucket. | | Sim, quando as funções IAM não estiverem sendo usadas. |
| cacheSize | O tamanho (em bytes) do cache local. | 64 GB | Não. |
| connectionTimeout | Defina o tempo de espera (em milissegundos) antes de atingir o tempo limite ao estabelecer uma conexão inicialmente. | 10000 | Não. |
| maxCachedBinarySize | Os binários com tamanho menor ou igual a esse valor (em bytes) são armazenados no cache de memória. | 17408 (17 KB) | Não. |
| maxConnections | Defina o número máximo de conexões HTTP abertas permitidas. | 50 | Não. |
| maxErrorRetry | Defina o número máximo de tentativas de repetição para solicitações com falha (recuperáveis). | 3 | Não. |
| minRecordLength | O tamanho mínimo de um objeto (em bytes) que deve ser armazenado no armazenamento de dados. | 16384 | Não. |
| caminho | O caminho local do armazenamento de dados do AEM. | `crx-quickstart/repository/datastore` | Não. |
| proxyHost | Defina o host do proxy opcional pelo qual o cliente se conecta. | | Não. |
| proxyPort | Defina a porta de proxy opcional pela qual o cliente se conecta. | | Não. |
| s3Bucket | Nome do bucket do S3. | | Sim |
| s3EndPoint | Endpoint da API REST S3. | | Não. |
| s3Region | Região onde o bucket está. Consulte esta [página](https://docs.aws.amazon.com/general/latest/gr/s3.html) para obter mais detalhes. | Região em que a instância do AWS está em execução. | Não. |
| socketTimeout | Defina o tempo de espera (em milissegundos) para que os dados sejam transferidos por uma conexão estabelecida e aberta antes que a conexão expire e seja fechada. | 50000 | Não. |
| stagingPurgeInterval | O intervalo (em segundos) para limpeza de uploads concluídos do cache de preparo. | 300 | Não. |
| stagingRetryInterval | O intervalo (em segundos) para repetir uploads com falha. | 600 | Não. |
| stagingSplitPercentage | A porcentagem de `cacheSize` a ser usada para preparo de carregamentos assíncronos. | 10 | Não. |
| uploadThreads | O número de threads de upload usados para uploads assíncronos. | 10 | Não. |
| writeThreads | O número de threads simultâneos usados para gravação via Gerenciador de Transferência S3. | 10 | Não. |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### Armazenamento em cache do DataStore {#data-store-caching}

>[!NOTE]
>
>As implementações DataStore de `S3DataStore`, `CachingFileDataStore` e `AzureDataStore` dão suporte ao cache do sistema de arquivos local. A implementação `CachingFileDataStore` é útil quando o DataStore está em NFS (Network File System).

Ao atualizar de uma implementação de cache mais antiga (pré-Oak 1.6), há uma diferença na estrutura do diretório de cache do sistema de arquivos local. Na antiga estrutura de cache, os arquivos baixados e carregados eram colocados diretamente no caminho do cache. A nova estrutura separa os downloads e uploads e os armazena em dois diretórios chamados `upload` e `download` no caminho do cache. O processo de atualização deve ser contínuo e todos os uploads pendentes devem ser agendados para upload, e todos os arquivos baixados anteriormente no cache são colocados no cache na inicialização.

Você também pode atualizar o cache offline usando o comando `datastorecacheupgrade` do oak-run. Para obter detalhes sobre como executar o comando, verifique o [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) do módulo oak-run.

O cache tem um limite de tamanho e pode ser configurado usando o parâmetro cacheSize.

#### Downloads {#downloads}

O cache local é verificado para o registro do arquivo/blob solicitado antes de acessá-lo do DataStore. Quando o cache excede o limite configurado (consulte o parâmetro `cacheSize`) ao adicionar um arquivo ao cache, alguns dos arquivos são removidos para recuperar espaço.

#### Upload assíncrono {#async-upload}

O cache oferece suporte a uploads assíncronos para o DataStore. Os arquivos são preparados localmente, no cache (no sistema de arquivos) e um trabalho assíncrono começa a fazer upload do arquivo. O número de uploads assíncronos é limitado pelo tamanho do cache de preparo. O tamanho do cache de preparo é configurado usando o parâmetro `stagingSplitPercentage`. Esse parâmetro define o percentual do tamanho do cache a ser usado para o cache de preparo. Além disso, a porcentagem de cache disponível para downloads é calculada como **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

Os uploads assíncronos são multithread e o número de threads é configurado usando o parâmetro `uploadThreads`.

Os arquivos são movidos para o cache de download principal depois que os uploads são concluídos. Quando o tamanho do cache de preparo excede seu limite, os arquivos são carregados de forma síncrona no DataStore até que os uploads assíncronos anteriores sejam concluídos e o espaço seja disponibilizado novamente no cache de preparo. Os arquivos carregados são removidos da área de preparo por um trabalho periódico cujo intervalo é configurado pelo parâmetro `stagingPurgeInterval`.

Uploads com falha (por exemplo, devido a uma interrupção da rede) são colocados em uma fila de tentativas e repetidos periodicamente. O intervalo de repetição é configurado usando o `stagingRetryInterval parameter`.

#### Configuração da replicação sem binários com o Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar a replicação sem binários com o S3, as seguintes etapas são necessárias:

1. Instale as instâncias de criação e publicação e verifique se elas foram iniciadas corretamente.
1. Vá para as configurações do agente de replicação, abrindo uma página em *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Pressione o botão **Editar** na seção **Configurações**.
1. Altere a opção de tipo **Serialização** para **Binário menos**.

1. Adicione o parâmetro &quot; `binaryless`= `true`&quot; no uri de transporte. Após a alteração, o uri deve ser semelhante ao seguinte:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas as instâncias de autor e publicação para permitir que as alterações sejam aplicadas.

#### Criação de um cluster usando S3 e MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Descompacte o quickstart do CQ usando o seguinte comando:

   `java -jar cq-quickstart.jar -unpack`

1. Depois que o AEM for desempacotado, crie uma pasta dentro do diretório de instalação *crx-quickstart*/*install*.

1. Crie estes dois arquivos dentro da pasta `crx-quickstart`:

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService*.*config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Após a criação dos arquivos, adicione as opções de configuração conforme necessário.

1. Instale os dois pacotes necessários para o armazenamento de dados S3, conforme explicado acima.
1. Verifique se o MongoDB está instalado e se uma instância de `mongod` está em execução.
1. Inicie o AEM com o seguinte comando:

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Repita as etapas de 1 a 4 para a segunda instância do AEM.
1. Inicie a segunda instância do AEM.

#### Configurar um armazenamento de dados compartilhado {#configuring-a-shared-data-store}

1. Primeiro, crie o arquivo de configuração do armazenamento de dados em cada instância necessária para compartilhar o armazenamento de dados:

   * Se você estiver usando um `FileDataStore`, crie um arquivo chamado `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e coloque-o na pasta `<aem-install>/crx-quickstart/install`.

   * Se estiver usando S3 como o armazenamento de dados, crie um arquivo chamado para `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` na pasta `<aem-install>/crx-quickstart/install` como acima.

1. Modifique os arquivos de configuração do armazenamento de dados em cada instância para que eles apontem para o mesmo armazenamento de dados. Para obter mais informações, consulte [Configurações do armazenamento de dados](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Se a instância tiver sido clonada de um servidor existente, remova o `clusterId` da nova instância usando a ferramenta oak-run mais recente enquanto o repositório estiver offline. O comando que você deve executar é:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Se um armazenamento de nó de Segmento estiver configurado, o caminho do repositório deverá ser especificado. Por padrão, o caminho é `<aem-install-folder>/crx-quickstart/repository/segmentstore.`. Se um repositório de nós do Documento estiver configurado, você poderá usar um [URI da Cadeia de Conexão do Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >A ferramenta de execução do Oak pode ser baixada neste local:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Devem ser usadas diferentes versões da ferramenta, dependendo da versão do Oak usada na instalação do AEM. Verifique a lista de requisitos de versão abaixo antes de usar a ferramenta:
   >
   >
   >
   >    * Para versões do Oak **1.2.x**, use o **1.2.12 ou mais recente** de execução do Oak
   >    * Para versões do Oak **mais recentes que a acima**, use a versão do Oak-run que corresponda ao núcleo do Oak da sua instalação do AEM.
   >
   >

1. Por último, valide a configuração. Para validar, procure um arquivo exclusivo adicionado ao armazenamento de dados por cada repositório que o está compartilhando. O formato dos arquivos é `repository-[UUID]`, onde a UUID é um identificador exclusivo de cada repositório individual.

   Portanto, uma configuração adequada deve ter quantos arquivos exclusivos houver repositórios compartilhando o armazenamento de dados.

   Os arquivos são armazenados de forma diferente, dependendo do armazenamento de dados:

   * Para o `FileDataStore`, os arquivos são criados no caminho raiz da pasta de armazenamento de dados.
   * Para o `S3DataStore`, os arquivos são criados no bucket do S3 configurado na pasta `META`.

## Armazenamento de dados Azure {#azure-data-store}

O AEM pode ser configurado para armazenar dados no serviço de armazenamento Azure da Microsoft®. Ele usa o PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` para configuração.

Para habilitar a funcionalidade de armazenamento de dados do Azure, um pacote de recursos contendo o Azure Connector deve ser baixado e instalado. Acesse o [Repositório do Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) e baixe a versão mais recente das versões 1.6.x do pacote de recursos (por exemplo, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Ao usar o AEM com TarMK, os binários são armazenados por padrão no FileDataStore. Para usar TarMK com o Azure DataStore, você deve iniciar o AEM usando o modo de execução `crx3tar-nofds`, por exemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Depois de baixado, você pode instalar e configurar o conector do Azure da seguinte maneira:

1. Extraia o conteúdo do arquivo zip do pacote de recursos para uma pasta temporária.

1. Vá para a pasta temporária e copie o conteúdo de `jcr_root/libs/system/install` para a pasta `<aem-install>crx-quickstart/install`.
1. Se o AEM já estiver configurado para funcionar com o armazenamento Tar ou MongoDB, remova todos os arquivos de configuração existentes da pasta `/crx-quickstart/install` antes de continuar. Os arquivos que devem ser removidos são:

   Para MongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retorne ao local temporário onde o pacote de recursos foi extraído e copie o conteúdo de `jcr_root/libs/system/config` para a pasta `<aem-install>/crx-quickstart/install`.
1. Edite o arquivo de configuração e adicione as opções de configuração exigidas pela configuração.
1. Inicie o AEM.

Você pode usar o arquivo de configuração com as seguintes opções:

* azureSas=&quot;&quot;: na versão 1.6.3 do conector, o suporte à Assinatura de Acesso Compartilhado (SAS) do Azure foi adicionado. **Se as credenciais SAS e de armazenamento existirem no arquivo de configuração, a SAS terá prioridade.** Para obter mais informações sobre a SAS, consulte a [documentação oficial](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview). Verifique se o caractere &#39;=&#39; tem escape como &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: O ponto de extremidade do Azure Blob. Por exemplo, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot;: O nome da conta de armazenamento. Para obter mais detalhes sobre as credenciais de autenticação do Microsoft® Azure, consulte a [documentação oficial](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create).

* secretKey=&quot;&quot;: A chave de acesso de armazenamento. Verifique se o caractere &#39;=&#39; tem escape como &#39;\=&#39;.
* container=&quot;&quot;: o nome do container do Microsoft® Azure blob Storage. O container é um agrupamento de um conjunto de blobs. Para obter detalhes adicionais, leia a [documentação oficial](https://learn.microsoft.com/en-us/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata?redirectedfrom=MSDN).
* maxConnections=&quot;&quot;: O número simultâneo de solicitações simultâneas por operação. O valor padrão é 1.
* maxErrorRetry=&quot;&quot;: Número de tentativas por solicitação. O valor padrão é 3.
* socketTimeout=&quot;&quot;: o intervalo de tempo limite, em milissegundos, usado para a solicitação. O valor padrão é 5 minutos.

Além das configurações acima, as seguintes configurações também podem ser definidas:

* caminho: o caminho do armazenamento de dados. O padrão é `<aem-install>/repository/datastore.`
* RecordLength: O tamanho mínimo de um objeto que deve ser armazenado no armazenamento de dados. O padrão é 16 KB.
* maxCachedBinarySize: binários com tamanho menor ou igual a esse tamanho são armazenados no cache de memória. O tamanho é em bytes. O padrão é 17408 (17 KB).
* cacheSize: o tamanho do cache. O valor é especificado em bytes. O padrão é 64 GB.
* secret: deve ser usado somente se estiver usando replicação sem binários para configuração de armazenamento de dados compartilhado.
* stagingSplitPercentage: a porcentagem do tamanho do cache configurada para ser usada para preparo de uploads assíncronos. O valor padrão é 10.
* uploadThreads: o número de threads de upload usados para uploads assíncronos. O valor padrão é 10.
* stagingPurgeInterval: o intervalo em segundos para limpeza de uploads concluídos do cache de preparo. O valor padrão é de 300 segundos (5 minutos).
* stagingRetryInterval: o intervalo de repetição em segundos para uploads com falha. O valor padrão é de 600 segundos (10 minutos).

>[!NOTE]
>
>Todas as configurações devem ser colocadas entre aspas, por exemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

O processo de coleta de lixo do armazenamento de dados é usado para remover quaisquer arquivos não utilizados no armazenamento de dados, liberando assim espaço em disco valioso no processo.

Você pode executar a coleta de lixo do armazenamento de dados ao:

1. Ir para o console JMX em *https://&lt;endereço_servidor:porta>/system/console/jmx*
1. Pesquisando por **RepositoryManagement.** Depois de encontrar o MBean do Gerenciador do repositório, clique nele para exibir as opções disponíveis.
1. Role até o final da página e clique no link **startDataStoreGC(boolean markOnly)**.
1. Na caixa de diálogo a seguir, digite `false` para o parâmetro `markOnly` e clique em **Chamar**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >O parâmetro `markOnly` significa se a fase de varredura da coleta de lixo é executada ou não.

## Coleta de lixo de armazenamento de dados para um armazenamento de dados compartilhado {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Ao executar a coleta de lixo em um armazenamento de dados clusterizado ou compartilhado, a configuração (com Mongo ou Segment Tar) do log pode exibir avisos sobre a incapacidade de excluir determinadas IDs de blob. As IDs de blob excluídas em uma coleta de lixo anterior são referenciadas incorretamente novamente por outros nós de cluster ou compartilhados que não têm informações sobre as exclusões de ID. Como resultado, quando a coleta de lixo é executada, ele registra um aviso ao tentar excluir uma ID que já foi excluída na última execução. Esse comportamento não afeta o desempenho ou a funcionalidade.

>[!NOTE]
>
>Se você estiver usando uma configuração de armazenamento de dados compartilhado e a coleta de lixo do armazenamento de dados estiver desativada, a execução da tarefa de limpeza do binário Lucene poderá aumentar repentinamente o espaço em disco usado. Considere desabilitar o BlobTracker em todas as instâncias de autor e publicação fazendo o seguinte:
>
>1. Pare a instância do AEM.
>2. Adicionar o parâmetro `blobTrackSnapshotIntervalInSecs=L"0"` no arquivo `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`. Este parâmetro exige o Oak 1.12.0, 1.10.2 ou posterior.
>3. Reinicie a instância do AEM.

Com versões mais recentes do AEM, a coleta de lixo do armazenamento de dados também pode ser executada em armazenamentos de dados compartilhados por mais de um repositório. Para executar a coleta de lixo do armazenamento de dados em um armazenamento de dados compartilhado, siga estas etapas:

1. Verifique se todas as tarefas de manutenção configuradas para a coleta de lixo do armazenamento de dados estão desabilitadas em todas as instâncias do repositório que compartilham o armazenamento de dados.
1. Execute as etapas mencionadas em [Coleta de Lixo Binário](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) individualmente em **todas** as instâncias do repositório que compartilham o repositório de dados. No entanto, digite `true` para o parâmetro `markOnly` antes de clicar no botão Chamar:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Depois de concluir o procedimento acima em todas as instâncias, execute a coleta de lixo do armazenamento de dados novamente de **qualquer** das instâncias:

   1. Vá para o console JMX e selecione o Mbean do gerenciador de repositório.
   1. Clique no link **Click startDataStoreGC(boolean markOnly)**.
   1. Na caixa de diálogo a seguir, insira `false` para o parâmetro `markOnly` novamente.

   Todos os arquivos encontrados são agrupados usando a fase de marcação usada antes e excluem o restante que não é usado do armazenamento de dados.
