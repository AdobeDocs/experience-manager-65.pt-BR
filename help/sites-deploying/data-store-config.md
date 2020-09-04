---
title: Configuração de armazenamentos de nó e armazenamentos de dados no AEM 6
seo-title: Configuração de armazenamentos de nó e armazenamentos de dados no AEM 6
description: Saiba como configurar armazenamentos de nó e armazenamentos de dados e como executar a coleta de lixo do armazenamento de dados.
seo-description: Saiba como configurar armazenamentos de nó e armazenamentos de dados e como executar a coleta de lixo do armazenamento de dados.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: f0ec3415ffef70c985828f17b32dc0d453c1ae7c
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 1%

---


# Configuração de armazenamentos de nó e armazenamentos de dados no AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Introdução {#introduction}

No Adobe Experience Manager (AEM), os dados binários podem ser armazenados independentemente dos nós de conteúdo. Os dados binários são armazenados em um armazenamento de dados, enquanto os nós de conteúdo são armazenados em um armazenamento de nós.

Tanto os armazenamentos de dados quanto os armazenamentos de nós podem ser configurados usando a configuração OSGi. Cada configuração OSGi é referenciada usando um identificador persistente (PID).

## Etapas de configuração {#configuration-steps}

Para configurar o armazenamento de nós e o armazenamento de dados, execute estas etapas:

1. Copie o arquivo JAR de início rápido AEM para seu diretório de instalação.
1. Crie uma pasta `crx-quickstart/install` no diretório de instalação.
1. Primeiro, configure o armazenamento de nós criando um arquivo de configuração com o nome da opção de armazenamento de nós que você deseja usar no `crx-quickstart/install` diretório.

   Por exemplo, o armazenamento de nó do Documento (que é a base para AEM implementação do MongoMK) usa o arquivo `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Edite o arquivo e defina suas opções de configuração.
1. Crie um arquivo de configuração com o PID do armazenamento de dados que deseja usar. Edite o arquivo para definir as opções de configuração.

   >[!NOTE]
   >
   >Consulte Configurações [de armazenamento de](#node-store-configurations) nós e Configurações [de armazenamento de](#data-store-configurations) dados para obter opções de configuração.

1. Start AEM.

## Configurações de armazenamento de nós {#node-store-configurations}

>[!CAUTION]
>
>As versões mais recentes do Oak utilizam um novo esquema de nomeação e formato para arquivos de configuração OSGi. O novo esquema de nomenclatura exige que o arquivo de configuração seja nomeado como **.config** e o novo formato requer que os valores sejam digitados e seja [documentado aqui](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Se você atualizar de uma versão anterior do Oak, certifique-se de fazer primeiro um backup da `crx-quickstart/install`pasta. Após a atualização, restaure o conteúdo da pasta para a instalação atualizada e modifique a extensão dos arquivos de configuração de **.cfg** para **.config**.
>
>Caso esteja lendo este artigo em preparação para uma atualização de uma instalação **AEM 5.x** , verifique se você consultou a documentação de [atualização](https://docs.adobe.com/content/docs/en/aem/6-0/deploy/upgrade.html) primeiro.

### Loja de Nó de Segmento {#segment-node-store}

O armazenamento de segmentos é a base da implementação do nó TarMK no AEM6. Ele usa o `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` PID para configuração.

>[!CAUTION]
>
>O PID para o repositório do nó Segmento foi alterado de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` AEM 6 para `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` AEM 6.3. Certifique-se de fazer os ajustes de configuração necessários para refletir essa alteração.

Você pode configurar as seguintes opções:

* `repository.home`: Caminho para a home do repositório no qual os dados relacionados ao repositório são armazenados. Por padrão, os arquivos de segmento são armazenados sob o `crx-quickstart/segmentstore` diretório.

* `tarmk.size`: Tamanho máximo de um segmento em MB. O padrão máximo é 256 MB.
* `customBlobStore`: Valor booliano que indica que um armazenamento de dados personalizado é usado. O valor padrão é verdadeiro para AEM 6.3 e versões posteriores. Antes do AEM 6.3, o padrão era falso.

Este é um exemplo de `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` arquivo:

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Loja de Nó de documento {#document-node-store}

O armazenamento de nó do documento é a base AEM implementação do MongoMK. Ele usa o `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. As seguintes opções de configuração estão disponíveis:

* `mongouri`: O [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) necessário para se conectar ao Banco de Dados Mongo. O padrão é `mongodb://localhost:27017`

* `db`: Nome do banco de dados Mongo. O padrão é **Oak** ``. However, new AEM 6 installations use **aem-author** ``como o nome padrão do banco de dados.

* `cache`: O tamanho do cache em MB. Isso é distribuído entre vários caches usados no DocumentNodeStore. O padrão é `256`

* `changesSize`: Tamanho em MB da coleção com limites usada no Mongo para armazenar a saída do diff em cache. O padrão é `256`

* `customBlobStore`: Valor booliano que indica que um armazenamento de dados personalizado será usado. O padrão é `false`.

Este é um exemplo de `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` arquivo:

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurações do armazenamento de dados {#data-store-configurations}

Ao lidar com um grande número de binários, recomenda-se que um armazenamento de dados externo seja usado em vez dos armazenamentos de nó padrão para maximizar o desempenho.

Por exemplo, se o seu projeto exigir um grande número de ativos de mídia, armazená-los no Arquivo ou no Armazenamento de dados S3 tornará o acesso mais rápido do que armazená-los diretamente em um MongoDB.

O File Data Store oferece melhor desempenho do que o MongoDB, e as operações de backup e restauração Mongo também são mais lentas com um grande número de ativos.

Os detalhes sobre os diferentes armazenamentos de dados e configurações estão descritos abaixo.

>[!NOTE]
>
>Para ativar os Repositórios de Dados personalizados, é necessário verificar se ele `customBlobStore` está definido como `true` no respectivo arquivo de configuração do Armazenamento de Nó (armazenamento[de nó de](/help/sites-deploying/data-store-config.md#segment-node-store) segmento ou armazenamento [de nó de](/help/sites-deploying/data-store-config.md#document-node-store)documento).

### Armazenamento de dados do arquivo {#file-data-store}

Esta é a implementação do [FileDataStore](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) presente em Jackrabbit 2. Ele fornece uma maneira de armazenar os dados binários como arquivos normais no sistema de arquivos. Ele usa o `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` PID.

Essas opções de configuração estão disponíveis:

* `repository.home`: Caminho para a home do repositório no qual vários dados relacionados ao repositório são armazenados. Por padrão, os arquivos binários seriam armazenados no `crx-quickstart/repository/datastore` diretório

* `path`: Caminho para o diretório sob o qual os arquivos serão armazenados. Se especificado, tem precedência sobre o `repository.home` valor

* `minRecordLength`: O tamanho mínimo em bytes de um arquivo armazenado no armazenamento de dados. O conteúdo binário menor que esse valor seria incorporado.

>[!NOTE]
>
>Ao usar um NAS para armazenar armazenamentos de dados de arquivos compartilhados, certifique-se de usar apenas dispositivos de alto desempenho para evitar problemas de desempenho.

## Amazon S3 Data Store {#amazon-s-data-store}

AEM pode ser configurado para armazenar dados no Serviço de Armazenamento Simples (S3) da Amazon. Ele usa o `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` PID para configuração.

Para habilitar a funcionalidade do armazenamento de dados S3, é necessário baixar e instalar um pacote de recursos contendo o S3 Datastore Connector. Vá para o Repositório [do](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/) Adobe e baixe a versão mais recente das versões 1.10.x do pacote de recursos (por exemplo, com.adobe.granite.oak.s3Connector-1.10.0.zip). Além disso, você também precisa baixar e instalar o service pack AEM mais recente, conforme listado na página Notas [de versão do](/help/release-notes/sp-release-notes.md) AEM 6.5.

>[!NOTE]
>
>Ao usar AEM com TarMK, os binários serão armazenados por padrão no `FileDataStore`. Para usar o TarMK com o S3 Datastore, é necessário start AEM usando o `crx3tar-nofds` modo de execução, por exemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Depois de baixado, você pode instalar e configurar o S3 Connector da seguinte maneira:

1. Extraia o conteúdo do arquivo zip do pacote de recursos para uma pasta temporária.

1. Vá para a pasta temporária e navegue até o seguinte local:

   ```xml
   jcr_root/libs/system/install
   ```

   Copie todo o conteúdo do local acima para `<aem-install>/crx-quickstart/install.`

1. Se o AEM já estiver configurado para funcionar com o armazenamento Tar ou MongoDB, remova todos os arquivos de configuração existentes da pasta ***&lt;aem-install>***/*crx-quickstart*/*install* antes de continuar. Os arquivos que precisam ser removidos são:

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retorne ao local temporário onde o pacote de recursos foi extraído e copie o conteúdo da seguinte pasta:

   * `jcr_root/libs/system/config`

   para

   * `<aem-install>/crx-quickstart/install`

   Certifique-se de copiar apenas os arquivos de configuração necessários para a sua configuração atual. Para um armazenamento de dados dedicado e uma configuração de armazenamento de dados compartilhado, copie o `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` arquivo.

   >[!NOTE]
   >
   >Em uma configuração de cluster, execute as etapas acima em todos os nós do cluster, um por um. Além disso, certifique-se de usar as mesmas configurações S3 para todos os nós.

1. Edite o arquivo e adicione as opções de configuração exigidas pela configuração.
1. Start AEM.

### Atualização para uma nova versão do conector S3 1.10.x {#upgrading-to-a-new-version-of-the-x-s-connector}

Se precisar atualizar para uma nova versão do conector S3 1.10.x (por exemplo, de 1.10.0 para 1.10.4), siga estas etapas:

1. Pare a instância AEM.

1. Navegue até `<aem-install>/crx-quickstart/install/15` a pasta de instalação AEM e faça um backup de seu conteúdo.
1. Após o backup, exclua a versão antiga do S3 Connector e suas dependências excluindo todos os arquivos jar na `<aem-install>/crx-quickstart/install/15` pasta, por exemplo:

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Os nomes de ficheiros apresentados acima são utilizados apenas para fins ilustrativos e não são definitivos.

1. Baixe a versão mais recente do pacote de recursos 1.8.x do Repositório do [Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Descompacte o conteúdo em uma pasta separada e navegue até `jcr_root/libs/system/install/15`.
1. Copie os arquivos jar para **&lt;aem-install>**/crx-quickstart/install/15 na pasta de instalação AEM.
1. Start AEM e verifique a funcionalidade do conector.

Você pode usar o arquivo de configuração com as seguintes opções:

* accessKey: A chave de acesso AWS.
* secretKey: A chave de acesso secreta AWS. **Observação:** Como alternativa, as funções [do](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) IAM podem ser usadas para autenticação. Se você estiver usando funções IAM, não será mais necessário especificar o `accessKey` e `secretKey`.

* s3Bucket: O nome do balde.
* s3Região: A região do balde.
* caminho: O caminho do armazenamento de dados. O padrão é **&lt;AEM install folder>/repository/datastore**
* minRecordLength: O tamanho mínimo de um objeto que deve ser armazenado no armazenamento de dados. O mínimo/padrão é **16 KB.**
* maxCachedBinarySize: Os binários com tamanho menor ou igual a esse tamanho serão armazenados no cache de memória. O tamanho está em bytes. O padrão é **17408 **(17 KB).

* cacheSize: O tamanho do cache. O valor é especificado em bytes. O padrão é **64 GB**.
* secret: Somente para ser usado se estiver usando replicação sem binários para configuração compartilhada de armazenamento de dados.
* stagingSplitPercentage: A porcentagem do tamanho do cache configurada para ser usada para fazer uploads assíncronos. O valor padrão é **10**.
* uploadThreads: O número de threads de uploads usados para uploads assíncronos. O valor padrão é **10**.
* stagingPurgeInterval: O intervalo, em segundos, para expurgar os carregamentos concluídos do cache de preparo. O valor padrão é **300** segundos (5 minutos).
* stagingRetryInterval: O intervalo de tentativas em segundos para carregar com falha. O valor padrão é **600** segundos (10 minutos).

### Opções de região do período {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>Oeste dos EUA</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>Oeste dos EUA (Califórnia do Norte)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>UE (Irlanda)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Pacífico Asiático (Cingapura)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Pacífico Asiático (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Pacífico Asiático (Tóquio)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>América do Sul (São Paulo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**Cache do DataStore**

>[!NOTE]
>
>As implementações do DataStore de `S3DataStore`e `CachingFileDataStore` `AzureDataStore` oferecem suporte ao cache do sistema de arquivos local. A `CachingFileDataStore` implementação é útil quando o DataStore está no NFS (Network File System).


Ao atualizar de uma implementação de cache mais antiga (pré-Oak 1.6), há uma diferença na estrutura do diretório de cache do sistema de arquivos local. Na estrutura antiga do cache, os arquivos baixados e carregados foram colocados diretamente no caminho do cache. A nova estrutura segrega os downloads e uploads e os armazena em dois diretórios nomeados `upload` e `download` em caminho de cache. O processo de atualização deve ser simples e todos os uploads pendentes devem ser agendados para upload e quaisquer arquivos baixados anteriormente no cache serão colocados no cache na inicialização.

Você também pode atualizar o cache offline usando o `datastorecacheupgrade` comando oak-run. Para obter detalhes sobre como executar o comando, verifique o módulo [readme](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md) para ver se o módulo é executado em carvalho.

O cache tem um limite de tamanho e pode ser configurado usando o parâmetro cacheSize.

**Downloads**

O cache local será verificado para o registro do arquivo/blob solicitado antes de acessá-lo do DataStore. Quando o cache exceder o limite configurado (consulte o `cacheSize` parâmetro) ao adicionar um arquivo ao cache, alguns arquivos serão removidos para recuperar espaço.

**Upload assíncrono**

O cache oferece suporte a uploads assíncronos para o DataStore. Os arquivos são preparados localmente, no cache (no sistema de arquivos) e em start de trabalho assíncronos para carregar o arquivo. O número de uploads assíncronos é limitado pelo tamanho do cache de preparo. O tamanho do cache de preparo é configurado usando o `stagingSplitPercentage` parâmetro. Esse parâmetro define a porcentagem do tamanho do cache a ser usada para o cache de preparo. Além disso, a porcentagem do cache disponível para downloads é calculada como **(100 -`stagingSplitPercentage`) *`cacheSize`**.

Os uploads assíncronos são multisegmentados e o número de threads é configurado usando o `uploadThreads` parâmetro.

Os arquivos são movidos para o cache principal de download após a conclusão dos uploads. Quando o tamanho do cache de armazenamento temporário excede seu limite, os arquivos são carregados sincronicamente no DataStore até que os uploads assíncronos anteriores sejam concluídos e o espaço volte a estar disponível no cache de armazenamento temporário. Os arquivos carregados são removidos da área de preparo por um trabalho periódico cujo intervalo é configurado pelo `stagingPurgeInterval` parâmetro.

Os uploads com falha (por exemplo, devido a uma interrupção de rede) são colocados em uma fila de tentativas e repetidos periodicamente. O intervalo de tentativas é configurado usando o `stagingRetryInterval parameter`.

#### Configuração da replicação sem binários com o Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Para configurar a replicação sem binários com S3, são necessárias as seguintes etapas:

1. Instale as instâncias de autor e publicação e verifique se elas foram iniciadas corretamente.
1. Vá para as configurações do agente de replicação, abrindo uma página em *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Pressione o botão **Editar** na seção **Configurações** .
1. Altere a opção **Serialization** type para **Binary less**.

1. Adicione o parâmetro &quot; `binaryless`= `true`&quot; no uri de transporte. Após a alteração, o uri deve ser semelhante ao seguinte:

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Reinicie todas as instâncias de autor e publicação para permitir que as alterações entrem em vigor.

#### Criação de um cluster usando S3 e MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Desempacotar Início rápido do CQ usando o seguinte comando:

   `java -jar cq-quickstart.jar -unpack`

1. Depois que AEM descompactado, crie uma pasta dentro do diretório de instalação *crx-quickstart*/*install*.

1. Crie estes dois arquivos dentro da `crx-quickstart` pasta:

   * *org.apache.Jackrabbit.oak.plugins.documento.DocumentNodeStoreService*.*configuração*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*configuração*

   Depois que os arquivos forem criados, adicione as opções de configuração conforme necessário.

1. Instale os dois pacotes necessários para o armazenamento de dados S3, conforme explicado acima.
1. Verifique se o MongoDB está instalado e se uma instância do `mongod` está em execução.
1. Start AEM com o seguinte comando:

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Repita as etapas de 1 a 4 para a segunda instância AEM.
1. Start a segunda instância AEM.

#### Configuração de um armazenamento de dados compartilhado {#configuring-a-shared-data-store}

1. Primeiro, crie o arquivo de configuração do armazenamento de dados em cada instância necessária para compartilhar o armazenamento de dados:

   * Se estiver usando um arquivo `FileDataStore`, crie um arquivo com o nome `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e coloque-o na `<aem-install>/crx-quickstart/install` pasta.

   * Se estiver usando S3 como o armazenamento de dados, crie um arquivo com o nome ou `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` na `<aem-install>/crx-quickstart/install` pasta como acima.

1. Modifique os arquivos de configuração do armazenamento de dados em cada instância para apontar para o mesmo armazenamento de dados. Para obter mais informações, consulte [este artigo](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Se a instância tiver sido clonada de um servidor existente, será necessário remover o da nova instância usando a ferramenta de execução de carvalho mais recente enquanto o repositório estiver offline. `clusterId` O comando que você precisa executar é:

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Se um armazenamento de nó do segmento estiver configurado, o caminho do repositório precisa ser especificado. Por padrão, o caminho é `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Se um armazenamento de nó de Documento estiver configurado, você pode usar um URI [](https://docs.mongodb.org/manual/reference/connection-string/)de cadeia de conexão mongo.

   >[!NOTE]
   >
   >A ferramenta Oak-run pode ser baixada deste local:
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Esteja ciente de que diferentes versões da ferramenta precisam ser usadas, dependendo da versão Oak usada com a instalação do AEM. Verifique a lista de requisitos de versão abaixo antes de usar a ferramenta:
   >
   >
   >
   >    * Para as versões **1.2.x** do Oak, use o Oak-run **1.2.12 ou mais recente**
   >    * Para versões do Oak **mais recentes do que as anteriores**, use a versão do Oak-run que corresponde ao núcleo Oak da instalação do AEM.


1. Por fim, valide a configuração. Para fazer isso, é necessário procurar um arquivo exclusivo adicionado ao armazenamento de dados por cada repositório que o esteja compartilhando. O formato dos arquivos é `repository-[UUID]`, onde o UUID é um identificador exclusivo de cada repositório individual.

   Portanto, uma configuração adequada deve ter tantos arquivos exclusivos quanto repositórios compartilhando o armazenamento de dados.

   Os arquivos são armazenados de forma diferente, dependendo do armazenamento de dados:

   * Para `FileDataStore` os arquivos são criados no caminho raiz da pasta do armazenamento de dados.
   * Para `S3DataStore` os arquivos são criados no bucket S3 configurado na `META` pasta.

## Armazenamento de dados Azure {#azure-data-store}

AEM pode ser configurado para armazenar dados no serviço do armazenamento do Azure da Microsoft. Ele usa o `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` PID para configuração.

Para habilitar a funcionalidade do repositório de dados do Azure, é necessário baixar e instalar um pacote de recursos que contenha o Conector do Azure. Vá para o Repositório [do](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) Adobe e baixe a versão mais recente das versões 1.6.x do pacote de recursos (por exemplo, com.adobe.granite.oak.azureblobConnector-1.6.3.zip).

>[!NOTE]
>
>Ao usar AEM com TarMK, os binários serão armazenados por padrão no FileDataStore. Para usar o TarMK com o Azure DataStore, é necessário start AEM usando o `crx3tar-nofds` modo de execução, por exemplo:

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Depois de baixado, você pode instalar e configurar o conector do Azure da seguinte maneira:

1. Extraia o conteúdo do arquivo zip do pacote de recursos para uma pasta temporária.

1. Vá para a pasta temporária e copie o conteúdo do `jcr_root/libs/system/install` para a `<aem-install>crx-quickstart/install` pasta.
1. Se AEM já estiver configurado para funcionar com o armazenamento Tar ou MongoDB, remova todos os arquivos de configuração existentes da `/crx-quickstart/install` pasta antes de continuar. Os arquivos que precisam ser removidos são:

   ParaMongoMK:

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Para TarMK:

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retorne ao local temporário onde o pacote de recursos foi extraído e copie o conteúdo do para `jcr_root/libs/system/config` a `<aem-install>/crx-quickstart/install` pasta.
1. Edite o arquivo de configuração e adicione as opções de configuração exigidas pela configuração.
1. Start AEM.

Você pode usar o arquivo de configuração com as seguintes opções:

* azureSas=&quot;&quot;: Na versão 1.6.3 do conector, foi adicionado o suporte a Azure Shared Access Signature (SAS). **Se as credenciais SAS e do armazenamento existirem no arquivo de configuração, a SAS terá prioridade.** Para obter mais informações sobre a SAS, consulte a documentação [](https://docs.microsoft.com/en-us/azure/storage/common/storage-dotnet-shared-access-signature-part-1)oficial. Certifique-se de que o caractere &#39;=&#39; tenha escape como &#39;\=&#39;.

* azureBlobEndpoint=&quot;&quot;: O Ponto Final do Blob do Azure. Por exemplo, https://&lt;conta-armazenamento>.blob.core.windows.net.
* accessKey=&quot;&quot;: O nome da conta do armazenamento. Para obter mais detalhes sobre as credenciais de autenticação do Microsoft Azure, consulte a documentação [](https://azure.microsoft.com/en-us/documentation/articles/storage-create-storage-account)oficial.

* secretKey=&quot;&quot;: A chave de acesso do armazenamento. Certifique-se de que o caractere &#39;=&#39; tenha escape como &#39;\=&#39;.
* container=&quot;&quot;: O nome do container do armazenamento blob do Microsoft Azure. O container é um agrupamento de um conjunto de blobs. Para mais informações, leia a documentação [](https://msdn.microsoft.com/en-us/library/dd135715.aspx)oficial.
* maxConnections=&quot;&quot;: O número simultâneo de solicitações simultâneas por operação. O valor padrão é 1.
* maxErrorRetry=&quot;&quot;: Número de tentativas por solicitação. O valor padrão é 3.
* socketTimeout=&quot;&quot;: O intervalo de tempo limite, em milissegundos, usado para a solicitação. O valor padrão é 5 minutos.

Além das configurações acima, as seguintes configurações também podem ser definidas:

* caminho: O caminho do armazenamento de dados. O padrão é `<aem-install>/repository/datastore.`
* RecordLength: O tamanho mínimo de um objeto que deve ser armazenado no armazenamento de dados. O padrão é 16KB.
* maxCachedBinarySize: Os binários com tamanho menor ou igual a esse tamanho serão armazenados no cache de memória. O tamanho está em bytes. O padrão é 17408 (17 KB).
* cacheSize: O tamanho do cache. O valor é especificado em bytes. O padrão é 64 GB.
* secret: Somente para ser usado se estiver usando replicação sem binários para configuração compartilhada de armazenamento de dados.
* stagingSplitPercentage: A porcentagem do tamanho do cache configurada para ser usada para fazer uploads assíncronos. O valor padrão é 10.
* uploadThreads: O número de threads de uploads usados para uploads assíncronos. O valor padrão é 10.
* stagingPurgeInterval: O intervalo, em segundos, para expurgar os carregamentos concluídos do cache de preparo. O valor padrão é 300 segundos (5 minutos).
* stagingRetryInterval: O intervalo de tentativas em segundos para carregar com falha. O valor padrão é 600 segundos (10 minutos).

>[!NOTE]
>
>Todas as configurações devem ser colocadas entre aspas, por exemplo:

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Data store garbage collection {#data-store-garbage-collection}

O processo de coleta de lixo do armazenamento de dados é usado para remover arquivos não utilizados no armazenamento de dados, liberando, assim, espaço valioso no disco no processo.

Você pode executar a coleta de lixo do armazenamento de dados ao:

1. Vá para o console JMX localizado em *https://&lt;nomedoservidor:porta>/system/console/jmx*
1. Pesquisando **RepositoryManagement.** Depois de encontrar o MBean do Gerenciador de repositório, clique nele para exibir as opções disponíveis.
1. Role até o final da página e clique no link **startDataStoreGC(boolean markOnly)** .
1. Na caixa de diálogo a seguir, digite `false` para o `markOnly` parâmetro e clique em **Chamar**:

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >O parâmetro `markOnly` significa se a fase de varredura da coleta de lixo será executada ou não.

## Coleta de lixo do Data Store para um armazenamento de dados compartilhado {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Ao executar a coleta de lixo em uma configuração de armazenamento de dados clusterizado ou compartilhado (com Mongo ou Segment Tar), o log pode exibir avisos sobre a incapacidade de excluir determinadas IDs de blob. Isso ocorre porque as IDs de blob excluídas em uma coleta de lixo anterior são referenciadas incorretamente novamente por outro cluster ou nós compartilhados que não têm informações sobre as exclusões de ID. Como resultado, quando a coleta de lixo é executada, ele registra um aviso ao tentar excluir uma ID que já foi excluída na última execução. Esse comportamento não afeta o desempenho nem a funcionalidade.

Com versões mais recentes de AEM, a coleta de lixo do armazenamento de dados também pode ser executada em armazenamentos de dados compartilhados por mais de um repositório. Para poder executar a coleta de lixo do armazenamento de dados em um armazenamento de dados compartilhado, execute as seguintes etapas:

1. Verifique se todas as tarefas de manutenção configuradas para a coleta de lixo do armazenamento de dados estão desativadas em todas as instâncias do repositório que compartilham o armazenamento de dados.
1. Execute as etapas mencionadas na Coleta [de lixo](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) binário individualmente em **todas** as instâncias do repositório que compartilham o armazenamento de dados. No entanto, certifique-se de inserir `true` para o `markOnly` parâmetro antes de clicar no botão Invocar:

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Depois de concluir o procedimento acima em todas as instâncias, execute a coleta de lixo do armazenamento de dados novamente em **qualquer** uma das instâncias:

   1. Vá para o console JMX e selecione o Repository Manager Mbean.
   1. Clique no link **Clique em startDataStoreGC(boolean markOnly)** .
   1. Na caixa de diálogo a seguir, insira novamente `false` o `markOnly` parâmetro.

   Isso coletará todos os arquivos encontrados usando a fase de marca usada antes e excluirá os demais que não forem utilizados do armazenamento de dados.

