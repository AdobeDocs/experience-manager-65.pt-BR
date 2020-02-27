---
title: AEM com MongoDB
seo-title: AEM com MongoDB
description: Saiba mais sobre as tarefas e considerações necessárias para um AEM bem-sucedido com a implantação do MongoDB.
seo-description: Saiba mais sobre as tarefas e considerações necessárias para um AEM bem-sucedido com a implantação do MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a

---


# AEM com MongoDB{#aem-with-mongodb}

Este artigo tem como objetivo melhorar o conhecimento sobre tarefas e considerações necessárias para implantar com êxito o Adobe Experience Manager com MongoDB.

Para obter mais informações relacionadas à implantação, consulte a seção [Implantação e manutenção](/help/sites-deploying/deploy.md) da documentação.

## Quando usar o MongoDB com o AEM {#when-to-use-mongodb-with-aem}

Normalmente, o MongoDB será usado para suportar implantações de autores do AEM, onde um dos seguintes critérios é atendido:

* Mais de 1000 utilizadores únicos por dia;
* Mais de 100 utilizadores simultâneos;
* Grandes volumes de edições de página;
* Grandes implantações ou ativações.

Os critérios acima são apenas para as instâncias do autor e não para qualquer instância de publicação que deve ser baseada em TarMK. O número de usuários se refere a usuários autenticados, já que as instâncias do autor não permitem acesso não autenticado.

Se os critérios não forem atendidos, uma implantação ativa/standby do TarMK é recomendada para atender à disponibilidade. Geralmente, o MongoDB deve ser considerado em situações em que os requisitos de dimensionamento são maiores do que o que pode ser obtido com um único item de hardware.

>[!NOTE]
>
>Informações adicionais sobre o dimensionamento de instâncias do autor e a definição de usuários simultâneos podem ser encontradas nas Diretrizes [de dimensionamento de](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)hardware.

### Implantação mínima do MongoDB para o AEM {#minimal-mongodb-deployment-for-aem}

Abaixo está uma implantação mínima do AEM no MongoDB. Para simplificar, a terminação SSL e os componentes HTTP Proxy foram generalizados. Ele consiste em um único conjunto de réplicas MongoDB, com um primário e dois secundários.

![chlimage_1-4](assets/chlimage_1-4.png)

Uma implantação mínima requer três `mongod` instâncias configuradas como um conjunto de réplicas. Uma instância será eleita primária, com as outras instâncias sendo secundárias, com a eleição gerenciada por `mongod`. Anexado a cada instância há um disco local. Para que o cluster suporte a carga, recomenda-se uma saída mínima de 12 MB/s com mais de 3000 operações de E/S por segundo (IOPS).

Os autores do AEM estão conectados às `mongod` instâncias, com cada autor do AEM se conectando a todas as três `mongod` instâncias. As gravações são enviadas para o principal e as leituras podem ser lidas de qualquer uma das instâncias. O tráfego é distribuído com base na carga de um despachante para qualquer uma das instâncias ativas do autor de AEM. O armazenamento de dados OAK é um `FileDataStore`e o monitoramento MongoDB é fornecido pelo MMS ou pelo MongoDB Ops Manager, dependendo da localização da implantação. O nível do sistema operacional e o monitoramento de log são fornecidos por soluções de terceiros como Splunk ou Ganglia.

Nesta implantação, todos os componentes são necessários para uma implementação bem-sucedida. Qualquer componente ausente deixará a implementação inoperante.

### Sistemas operacionais {#operating-systems}

Para obter uma lista dos sistemas operacionais suportados para o AEM 6, consulte a página [Requisitos](/help/sites-deploying/technical-requirements.md)técnicos.

### Ambientes {#environments}

Os ambientes virtualizados são suportados desde que haja boa comunicação entre as diferentes equipes técnicas que executam o projeto. Isso inclui a equipe que está executando o AEM, a equipe que possui o sistema operacional e a equipe que gerencia a infraestrutura virtualizada.

Existem requisitos específicos que abrangem a capacidade de E/S das instâncias MongoDB que precisam ser gerenciadas pela equipe que gerencia o ambiente virtualizado. Se o projeto fizer uso de uma implantação em nuvem, como os Serviços da Web da Amazon, as instâncias precisarão ser provisionadas com capacidade de E/S e consistência suficientes para suportar as instâncias do MongoDB. Caso contrário, os processos MongoDB e o repositório Oak serão executados de forma inconfiável e irregular.

Nos ambientes virtualizados, o MongoDB exigirá configurações específicas de E/S e VM para garantir que o mecanismo de armazenamento do MongoDB não seja incapacitado pelas políticas de alocação de recursos da VMWare. Uma implementação bem-sucedida garantirá que não haja barreiras entre as várias equipes e todas se inscrevem para fornecer o desempenho necessário.

## Considerações sobre hardware {#hardware-considerations}

### Armazenamento {#storage}

Para alcançar o throughput de leitura e gravação com melhor desempenho sem a necessidade de dimensionamento horizontal prematuro, o MongoDB geralmente exige armazenamento ou armazenamento SSD com desempenho equivalente ao SSD.

### RAM {#ram}

As versões 2.6 e 3.0 do MongoDB que usam o mecanismo de armazenamento MMAP exigem que o conjunto de trabalho do banco de dados e seus índices se encaixe na RAM.

RAM insuficiente resultará em uma redução significativa do desempenho. O tamanho do conjunto de trabalho e do banco de dados é altamente dependente do aplicativo. Embora algumas estimativas possam ser feitas, a maneira mais confiável de determinar a quantidade de RAM necessária é criar o aplicativo AEM e carregá-lo testando.

Para auxiliar no processo de teste de carga, é possível assumir a seguinte proporção do conjunto de trabalho em relação ao tamanho total do banco de dados:

* 1:10 para armazenamento SSD
* 1:3 para armazenamento em disco rígido

Isso significa que, no caso de implantações de SSD, 200 GB de RAM serão necessários para um banco de dados de 2 TB.

Embora as mesmas limitações se apliquem ao mecanismo de armazenamento WiredTiger no MongoDB 3.0, a correlação entre o conjunto de trabalho, a RAM e as falhas de página não é tão forte quanto o WiredTiger não usa o mapeamento de memória da mesma forma que o mecanismo de armazenamento MMAP.

>[!NOTE]
>
>A Adobe recomenda usar o mecanismo de armazenamento WiredTiger para implantações do AEM 6.1 que estejam usando o MongoDB 3.0.

### Data Store {#data-store}

Devido às limitações do conjunto de trabalho MongoDB, é altamente recomendável que o armazenamento de dados seja mantido independentemente do MongoDB. Na maioria dos ambientes, deve ser usado um `FileDataStore` uso de um NAS disponível para todas as instâncias do AEM. Para situações em que os Serviços Web da Amazon são usados, há também um `S3 DataStore`. Se, por qualquer motivo, o armazenamento de dados for mantido no MongoDB, o tamanho do armazenamento de dados deverá ser adicionado ao tamanho total do banco de dados e os cálculos do conjunto de trabalho ajustados apropriadamente. Isso pode significar provisionamento significativamente maior de RAM para manter o desempenho sem falhas na página.

## Monitoramento {#monitoring}

O acompanhamento é vital para uma implementação bem sucedida do projeto. Embora com conhecimento suficiente seja possível executar o AEM no MongoDB sem monitoramento, esse conhecimento é normalmente encontrado em engenheiros especializados para cada seção do desenvolvimento.

Normalmente, isso envolve um engenheiro de P&amp;D trabalhando no Apache Oak Core e um especialista em MongoDB.

Sem monitoramento a todos os níveis, será necessário um conhecimento detalhado da base de códigos para diagnosticar problemas. Com a monitorização em vigor e orientações adequadas sobre as principais estatísticas, as equipes de implementação poderão reagir adequadamente às anomalias.

Embora seja possível usar ferramentas de linha de comando para obter um instantâneo rápido da operação de um cluster, fazer isso em tempo real em muitos hosts é quase impossível. As ferramentas de linha de comando raramente fornecem informações históricas além de alguns minutos e nunca permitem correlações cruzadas entre diferentes tipos de métricas. Um breve período de `mongod` sincronização lenta em segundo plano requer um esforço manual significativo para correlacionar-se com a Espera de E/S ou níveis excessivos de gravação a um recurso de armazenamento compartilhado de uma máquina virtual aparentemente desconectada.

### Gerenciador de nuvem MongoDB {#mongodb-cloud-manager}

O MongoDB Cloud Manager é um serviço gratuito oferecido pelo MongoDB que permite o monitoramento e o gerenciamento de instâncias do MongoDB. Fornece uma visão do desempenho e da integridade do cluster MongoDB em tempo real. Ele gerencia instâncias de nuvem e hospedadas privadamente, desde que a instância possa acessar o servidor de monitoramento do Cloud Manager.

Ele requer um agente instalado na instância MongoDB que se conecte ao servidor de monitoramento. Há 3 níveis do agente:

* Um agente de automação que pode automatizar completamente tudo no servidor MongoDB.
* Um agente de monitorização que possa monitorizar a `mongod` instância,
* Um agente de backup que pode executar backups programados dos dados.

Embora o uso do Cloud Manager para automação de manutenção de um cluster MongoDB torne muitas das tarefas de rotina mais fáceis, ele não é obrigatório e nem está sendo usado para backup. No entanto, ao escolher o Gerenciador de nuvem para monitorar, é necessário monitorar.

Para obter mais informações sobre o MongoDB Cloud Manager, consulte a documentação [do](https://docs.cloud.mongodb.com/)MongoDB.

### Gerenciador de operações do MongoDB {#mongodb-ops-manager}

O MongoDB Ops Manager é o mesmo software do MongoDB Cloud Manager. Depois de registrado, o Ops Manager pode ser baixado e instalado localmente em um data center privado ou em qualquer outro laptop ou computador desktop. Ele usa um banco de dados MongoDB local para armazenar dados e se comunicar exatamente da mesma forma que o Cloud Manager com os servidores gerenciados. Se você tiver políticas de segurança que proíbam um agente de monitoramento, o MongoDB Ops Manager deverá ser usado.

### Monitoramento do sistema operacional {#operating-system-monitoring}

O monitoramento no nível do sistema operacional é necessário para executar um cluster AEM MongoDB.

Ganglia é um bom exemplo desse sistema e fornece uma imagem da faixa e detalhes das informações necessárias que vão além das métricas básicas de saúde, como CPU, média de carga e espaço livre em disco. Para diagnosticar problemas, são necessárias informações de nível mais baixo, como níveis de pool de entropia, Espera de E/S da CPU, soquetes no estado FIN_WAIT2.

### Agregação de log {#log-aggregation}

Com um cluster de vários servidores, a agregação de registros centrais é um requisito para um sistema de produção. Softwares como o Splunk oferecem suporte à agregação de registros e permitem que as equipes analisem os padrões de comportamento do aplicativo sem precisar coletar os registros manualmente.

## Listas de verificação {#checklists}

Esta seção trata de várias etapas que devem ser tomadas para garantir que suas implantações do AEM e do MongoDB estejam configuradas corretamente antes da implementação do projeto.

### Rede {#network}

1. Primeiro, verifique se todos os hosts têm uma entrada DNS
1. Todos os hosts devem ser resolvidos pela entrada DNS de todos os outros hosts roteáveis
1. Todos os hosts MongoDB são roteáveis de todos os outros hosts MongoDB no mesmo cluster
1. Os hosts MongoDB podem rotear pacotes para o MongoDB Cloud Manager e outros servidores de monitoramento
1. Os servidores AEM podem rotear pacotes para todos os servidores MongoDB
1. A latência de pacote entre qualquer servidor AEM e qualquer servidor MongoDB é menor que dois milissegundos, sem perda de pacotes e distribuição padrão de um milissegundo ou menos.
1. Verifique se não há mais de dois saltos entre um servidor AEM e um servidor MongoDB
1. Não há mais de dois saltos entre dois servidores MongoDB
1. Não há roteadores maiores que o OSI Nível 3 entre os servidores principais (MongoDB ou AEM ou qualquer combinação).
1. Se for usado truncamento de VLAN ou qualquer forma de encapsulamento de rede, ele deverá estar em conformidade com as verificações de latência de pacotes.

### Configuração do AEM {#aem-configuration}

#### Configuração do armazenamento de nós {#node-store-configuration}

As instâncias do AEM devem ser configuradas para usar o AEM com MongoMK. A base da implementação do MongoMK no AEM é o Document Node Store.

Para obter mais informações sobre como configurar Nó Stores, consulte [Configuração de Nó Stores e Data Stores no AEM](/help/sites-deploying/data-store-config.md).

Veja abaixo um exemplo da configuração do Document Node Store para uma implantação mínima do MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Em que:

* `mongodburi`
Este é o servidor MongoDB ao qual o AEM precisa se conectar. As conexões são feitas a todos os membros conhecidos do conjunto de réplicas padrão. Se o MongoDB Cloud Manager for usado, a segurança do servidor será ativada. Consequentemente, a cadeia de conexão deve conter um nome de usuário e senha adequados. Versões não corporativas do MongoDB só suportam autenticação de nome de usuário e senha. Para obter mais informações sobre a sintaxe da string de conexão, consulte a [documentação](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
O nome do banco de dados. O padrão para o AEM é `aem-author`.

* `customBlobStore`
Se a implantação armazenar binários no banco de dados, eles farão parte do conjunto de trabalho. Por isso, é aconselhável não armazenar binários no MongoDB, preferindo um armazenamento de dados alternativo como um armazenamento de dados `FileSystem` em um NAS.

* `cache`
O tamanho do cache em Megabytes. Isso é distribuído entre vários caches usados no `DocumentNodeStore`. O padrão é 256 MB. Entretanto, o desempenho de leitura Oak se beneficiará de um cache maior.

* `blobCacheSize`
Os blobs usados com frequência podem ser armazenados em cache pelo AEM para evitar que eles sejam obtidos novamente no armazenamento de dados. Isso terá mais impacto no desempenho, especialmente ao armazenar blobs no banco de dados MongoDB. Todos os Data Stores baseados no sistema de arquivos se beneficiarão do cache em disco no nível do sistema operacional.

#### Configuração do armazenamento de dados {#data-store-configuration}

O Data Store é usado para armazenar arquivos de tamanho maior que um limite. Abaixo desse limite, os arquivos são armazenados como propriedades no Document Node Store. Se o `MongoBlobStore` for usado, uma coleção dedicada será criada no MongoDB para armazenar os blobs. Essa coleção contribui para o conjunto de trabalho da `mongod` instância e exigirá que ela `mongod` tenha mais RAM para evitar problemas de desempenho. Por esse motivo, a configuração recomendada é evitar o uso `MongoBlobStore` para implantações de produção e o `FileDataStore` backup de um NAS compartilhado entre todas as instâncias do AEM. Como o cache em nível de sistema operacional é eficiente no gerenciamento de arquivos, o tamanho mínimo de um arquivo em disco deve ser definido próximo ao tamanho do bloco do disco para que o sistema de arquivos seja usado eficientemente e muitos documentos pequenos não contribuam excessivamente para o conjunto de trabalho da `mongod` instância.

Esta é uma configuração típica do Data Store para uma implantação mínima do AEM com MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

Em que:

* `minRecordLength`
Tamanho em bytes. Os binários com menos de ou igual a esse tamanho são armazenados com o Document Node Store. Em vez de armazenar a ID do blob, o conteúdo do binário é armazenado. Para binários maiores que esse tamanho, a ID do binário é armazenada como uma propriedade do Documento na coleção de nós, e o corpo do binário é armazenado no `FileDataStore` disco. 4096 bytes é um tamanho típico de bloco do sistema de arquivos.

* `path`
O caminho para a raiz do armazenamento de dados. Para uma implantação do MongoMK, este deve ser um sistema de arquivos compartilhado disponível para todas as instâncias do AEM. Normalmente, um servidor NAS (Network Attached Storage, armazenamento conectado à rede) é usado. Para implantações em nuvem como os Serviços da Web da Amazon, o `S3DataFileStore` está disponível.

* `cacheSizeInMB`
O tamanho total do cache binário em Megabytes. É usado para armazenar em cache binários menores que a `maxCacheBinarySize` configuração.

* `maxCachedBinarySize`
O tamanho máximo em bytes de um binário armazenado em cache no cache binário. Se um Data Store baseado no sistema de arquivos for usado, não é recomendável usar valores altos para o cache do Data Store, pois os binários já estão em cache pelo sistema operacional.

#### Desabilitando a dica de consulta {#disabling-the-query-hint}

É recomendável desativar a dica de consulta enviada com todas as consultas adicionando a propriedade

`-Doak.mongo.disableIndexHint=true`

ao iniciar o AEM. Dessa forma, o MongoDB calculará o índice mais apropriado para usar com base em estatísticas internas.

Se a dica de consulta não estiver desativada, qualquer ajuste de desempenho de índices não terá impacto no desempenho do AEM.

#### Habilitar Cache Persistente para MongoMK {#enable-persistent-cache-for-mongomk}

É recomendável que uma configuração de cache persistente seja ativada para implantações MongoDB, a fim de maximizar a velocidade para ambientes com alto desempenho de leitura de E/S. Para obter mais detalhes, consulte a documentação [do](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)Jackrabbit Oak.

## Otimizações do sistema operacional MongoDB {#mongodb-operating-system-optimizations}

### Suporte ao sistema operacional {#operating-system-support}

O MongoDB 2.6 usa um mecanismo de armazenamento mapeado de memória que é sensível a alguns aspectos do gerenciamento no nível do sistema operacional entre RAM e Disco. O Desempenho de consulta e leitura da instância MongoDB depende de evitar ou eliminar operações de E/S lentas, geralmente chamadas de falhas de página. Essas são falhas de página que se aplicam ao `mongod` processo em particular. Eles não devem ser confundidos com falhas de página no nível do sistema operacional.

Para uma operação rápida, o banco de dados MongoDB só deve acessar os dados que já estão na RAM. Os dados que ele precisa acessar são compostos de índices e dados. Essa coleção de índices e dados é chamada de conjunto de trabalho. Quando o conjunto de trabalho for maior que a RAM disponível, o MongoDB terá que paginar os dados do disco com um custo de E/S, removendo outros dados já na memória. Se o despejo fizer com que os dados sejam recarregados a partir de falhas na página do disco dominarão e o desempenho diminuirá. Quando o conjunto de trabalho for dinâmico e variável, ocorrerão mais falhas de página para suportar operações.

O MongoDB é executado em vários sistemas operacionais, incluindo uma grande variedade de modelos Linux, Windows e Mac OS. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obter mais detalhes. Dependendo da escolha do sistema operacional, o MongoDB tem diferentes recomendações de nível de sistema operacional. Há documentos em [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) e resumidos aqui para sua conveniência.

#### Linux {#linux}

* Desative páginas iniciais transparentes e desfragmentar. Consulte Configurações [de páginas grandes e](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) transparentes para obter mais informações.
* [Ajuste as configurações](https://docs.mongodb.com/manual/administration/production-notes/#readahead) de leitura antecipada nos dispositivos que armazenam seus arquivos de banco de dados para atender ao caso de uso.

   * Para o mecanismo de armazenamento MMAPv1, se o conjunto de trabalho for maior que a RAM disponível e o padrão de acesso ao documento for aleatório, considere diminuir a leitura para 32 ou 16. Avalie diferentes configurações para encontrar um valor ideal que maximize a memória residente e diminua o número de falhas da página.
   * Para o mecanismo de armazenamento WiredTiger, defina com antecedência para 0, independentemente do tipo de mídia de armazenamento (rotação, SSD etc.). Em geral, use a configuração de leitura antecipada recomendada, a menos que o teste mostre um benefício mensurável, repetível e confiável em um valor de leitura antecipada mais alto. [O suporte](https://docs.mongodb.com/manual/administration/production-notes/#readahead) profissional MongoDB pode fornecer conselhos e orientação sobre configurações antecipadas que não sejam zero.

* Desative a ferramenta ajustada se estiver executando o RHEL 7 / CentOS 7 em um ambiente virtual.
* Quando o RHEL 7 / CentOS 7 é executado em um ambiente virtual, a ferramenta ajustada chama automaticamente um perfil de desempenho derivado da throughput de desempenho, que define automaticamente as configurações de leitura antecipada como 4 MB. Isso pode afetar negativamente o desempenho.
* Use os programadores de disco noop ou de prazo final para unidades SSD.
* Use o programador de disco noop para unidades virtualizadas em VMs convidadas.
* Desative NUMA ou defina vm.zone_rerequest_mode como 0 e execute instâncias [monboa](https://docs.mongodb.com/manual/administration/production-notes/#readahead) com intercalamento de nó. Consulte: Hardware [MongoDB e NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obter mais informações.

* Ajuste os valores máximos em seu hardware para atender ao caso de uso. Se várias instâncias [mondeus](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) ou [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) estiverem em execução sob o mesmo usuário, dimensione os valores máximos de acordo. Consulte: Configurações [de limite](https://docs.mongodb.com/manual/reference/ulimit/) UNIX para obter mais informações.

* Use noatime para o ponto de montagem [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) .
* Configure identificadores de arquivos suficientes (fs.file-max), limite de pid do kernel (kernel.pid_max) e segmentos máximos por processo (kernel.threads-max) para sua implantação. Para sistemas grandes, os valores a seguir fornecem um bom ponto de partida:

   * valor fs.file-max de 98000,
   * valor kernel.pid_max de 64000,
   * andkernel.threads-valor máximo de 64000

* Verifique se o espaço de troca do sistema está configurado. Consulte a documentação do sistema operacional para obter detalhes sobre o dimensionamento apropriado.
* Verifique se a manutenção TCP padrão do sistema está definida corretamente. Um valor de 300 geralmente oferece melhor desempenho para conjuntos de réplicas e clusters compartilhados. Consulte: O tempo de ativação do TCP [afeta as implantações do MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) em Perguntas frequentes para obter mais informações.

#### Windows {#windows}

* Considere desativar as atualizações de &quot;última hora de acesso&quot; do NTFS. Isso é análogo à desativação do tempo em sistemas semelhantes ao Unix.

### WiredTiger {#wiredtiger}

A partir do MongoDB 3.2, o mecanismo de armazenamento padrão para MongoDB é o mecanismo de armazenamento WiredTiger. Este mecanismo fornece vários recursos robustos e dimensionáveis que o tornam muito mais adequado para cargas de trabalho gerais de banco de dados. As seções a seguir descrevem esses recursos.

#### Simultaneidade de nível de documento {#document-level-concurrency}

O WiredTiger usa controle de simultaneidade em nível de documento para operações de gravação. Como resultado, vários clientes podem modificar diferentes documentos de uma coleção ao mesmo tempo.

Para a maioria das operações de leitura e gravação, o WiredTiger usa controle de simultaneidade otimista. O WiredTiger usa apenas bloqueios intencionais nos níveis global, de banco de dados e de coleta. Quando o mecanismo de armazenamento detecta conflitos entre duas operações, um deles terá um conflito de gravação que faz com que o MongoDB repita essa operação de forma transparente. Algumas operações globais, normalmente operações de curta duração envolvendo vários bancos de dados, ainda requerem um bloqueio global &quot;em toda a instância&quot;.

Algumas outras operações, como descartar uma coleção, ainda exigem um bloqueio de banco de dados exclusivo.

#### Instantâneos e pontos de verificação {#snapshots-and-checkpoints}

O WiredTiger usa MVCC (MultiVersion Concurrency Control). No início de uma operação, o WiredTiger fornece um instantâneo point-in-time dos dados para a transação. Um instantâneo apresenta uma visualização consistente dos dados na memória.

Ao gravar em disco, o WiredTiger grava todos os dados em um instantâneo em disco de maneira consistente em todos os arquivos de dados. Os dados agora [duráveis](https://docs.mongodb.com/manual/reference/glossary/#term-durable) atuam como um ponto de verificação nos arquivos de dados. O ponto de verificação garante que os ficheiros de dados sejam coerentes até ao último ponto de verificação, inclusive; ou seja, os pontos de verificação podem funcionar como pontos de recuperação.

O MongoDB configura o WiredTiger para criar pontos de verificação (ou seja, gravar os dados do snapshot no disco) em intervalos de 60 segundos ou 2 gigabytes de dados do diário.

Durante a gravação de um novo ponto de verificação, o ponto de verificação anterior ainda é válido. Dessa forma, mesmo se o MongoDB terminar ou encontrar um erro ao gravar um novo ponto de verificação, ao reiniciar, o MongoDB poderá se recuperar do último ponto de verificação válido.

O novo ponto de verificação fica acessível e permanente quando a tabela de metadados do WiredTiger é automaticamente atualizada para fazer referência ao novo ponto de verificação. Quando o novo ponto de verificação estiver acessível, o WiredTiger libera as páginas dos pontos de verificação antigos.

Usando o WiredTiger, mesmo sem [registro em log](https://docs.mongodb.com/manual/reference/glossary/#term-durable), o MongoDB pode se recuperar do último ponto de verificação; no entanto, para recuperar as alterações feitas após o último ponto de verificação, execute com o [diário](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diário {#journal}

A WiredTiger usa um log de transações de gravação antecipada em combinação com [pontos](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) de verificação para garantir a durabilidade dos dados.

O diário WiredTiger persiste em todas as modificações de dados entre pontos de verificação. Se o MongoDB sair entre pontos de verificação, ele usará o diário para reproduzir todos os dados modificados desde o último ponto de verificação. Para obter informações sobre a frequência com que o MongoDB grava os dados do diário no disco, consulte Processo [de Lançamento](https://docs.mongodb.com/manual/core/journaling/#journal-process).

O diário WiredTiger é compactado usando a biblioteca de compactação [instantânea](https://docs.mongodb.com/manual/core/journaling/#journal-process) . Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use a configuração [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) .

Para obter mais informações, consulte: [Viajando com WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>O tamanho mínimo de registro de log para WiredTiger é de 128 bytes. Se um registro de log tiver 128 bytes ou menos, o WiredTiger não compactará esse registro.
>
>Você pode desativar o registro em diário definindo [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) como false, o que pode reduzir a sobrecarga da manutenção do registro em log.
>
>Para instâncias [autônomas](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) , não usar o diário significa que você perderá algumas modificações de dados quando o MongoDB sair inesperadamente entre pontos de verificação. Para membros de conjuntos [de](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)réplicas, o processo de replicação pode fornecer garantias de durabilidade suficientes.

#### Compactação {#compression}

Com o WiredTiger, o MongoDB suporta compactação para todas as coleções e índices. A compactação minimiza o uso do armazenamento em detrimento da CPU adicional.

Por padrão, o WiredTiger usa a compactação de bloco com a biblioteca de compactação [instantânea](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) para todas as coleções e a compactação [de](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) prefixo para todos os índices.

Para coleções, a compactação de bloco com [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) também está disponível. Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use a configuração [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) .

Para índices, para desativar a compactação [de](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)prefixo, use a configuração [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) .

As configurações de compactação também são configuráveis por coleção e por índice durante a criação da coleção e do índice. Consulte [Especificar opções](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) do mecanismo de armazenamento e [db.collection.createIndex() opção storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) .

Para a maioria das cargas de trabalho, as configurações de compactação padrão equilibram a eficiência do armazenamento e os requisitos de processamento.

O diário WiredTiger também é compactado por padrão. Para obter informações sobre a compactação de diário, consulte [Diário](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso da memória {#memory-use}

Com o WiredTiger, o MongoDB utiliza o cache interno do WiredTiger e o cache do sistema de arquivos.

A partir do 3.4, o cache interno do WiredTiger, por padrão, usará o maior de:

* 50% de RAM menos 1 GB ou
* 256 MB

Por padrão, o WiredTiger usa a compactação de bloco Snappy para todas as coleções e a compactação de prefixo para todos os índices. Os padrões de compactação são configuráveis em um nível global e também podem ser definidos por coleção e por índice durante a coleta e a criação do índice.

Diferentes representações são usadas para dados no cache interno do WiredTiger em relação ao formato no disco:

* Os dados no cache do sistema de arquivos são os mesmos que no formato em disco, incluindo os benefícios de qualquer compactação para arquivos de dados. O cache do sistema de arquivos é usado pelo sistema operacional para reduzir a E/S do disco.

Os índices carregados no cache interno do WiredTiger têm uma representação de dados diferente no formato em disco, mas ainda podem aproveitar a compactação de prefixo de índice para reduzir o uso da RAM.

A compactação de prefixo de índice remove a duplicação de prefixos comuns de campos indexados.

Os dados de coleta no cache interno do WiredTiger são descompactados e usam uma representação diferente do formato no disco. A compactação em bloco pode proporcionar economia significativa no armazenamento em disco, mas os dados devem ser descompactados para serem manipulados pelo servidor.

Por meio do cache do sistema de arquivos, o MongoDB usa automaticamente toda a memória livre que não é usada pelo cache WiredTiger ou por outros processos.

Para ajustar o tamanho do cache interno do WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar o tamanho do cache interno do WiredTiger acima do valor padrão.

### NUMA {#numa}

O NUMA (Non Uniform Memory Access) permite que um kernel gerencie como a memória é mapeada para os núcleos do processador. Embora isso tente tornar o acesso à memória mais rápido para os núcleos, garantindo que eles sejam capazes de acessar os dados necessários, o NUMA interfere no MMAP, introduzindo latência adicional, já que a leitura não pode ser prevista. Por isso, o NUMA precisa ser desabilitado para o `mongod` processo em todos os sistemas operacionais com capacidade.

Basicamente, em uma arquitetura NUMA, a memória é conectada às CPUs e as CPUs são conectadas a um barramento. Em uma arquitetura SMP ou UMA, a memória é conectada ao barramento e compartilhada pelas CPUs. Quando um thread aloca memória em uma CPU NUMA, ele a aloca de acordo com uma política. O padrão é alocar memória conectada à CPU local do thread, a menos que não haja memória, e nesse ponto ela usa memória de uma CPU gratuita a um custo mais alto. Depois de alocada, a memória não se move entre CPUs. A alocação é executada por uma política herdada do thread pai, que é, em última análise, o thread que iniciou o processo.

Em muitos bancos de dados que veem a máquina como uma arquitetura de memória uniforme de vários núcleos, isso faz com que a CPU inicial fique cheia primeiro e o preenchimento da CPU secundária mais tarde, especialmente se um thread central for responsável por alocar buffers de memória. A solução é alterar a política NUMA do segmento principal usado para iniciar o `mongod` processo.

Isso pode ser feito executando o seguinte comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Essa política aloca memória em uma maneira redonda em todos os nós da CPU, garantindo uma distribuição uniforme em todos os nós. Ele não gera o mais alto desempenho de acesso à memória como em sistemas com vários hardwares da CPU. Cerca de metade das operações de memória serão mais lentas e acima do barramento, mas não `mongod` foi escrita para atingir o NUMA da melhor forma, portanto é um compromisso razoável.

### Problemas NUMA {#numa-issues}

Se o `mongod` processo for iniciado a partir de um local diferente da `/etc/init.d` pasta, é provável que ele não seja iniciado com a política NUMA correta. Dependendo da política padrão, podem ocorrer problemas. Isso ocorre porque os vários instaladores do gerenciador de pacote Linux para MongoDB também instalam um serviço com arquivos de configuração localizados em `/etc/init.d` que executam a etapa descrita acima. Se você instalar e executar o MongoDB diretamente de um arquivo ( `.tar.gz`), então será necessário executar manualmente o MongoDB durante o `numactl` processo.

>[!NOTE]
>
>Para obter mais informações sobre as políticas NUMA disponíveis, consulte a documentação [numérica](https://linux.die.net/man/8/numactl).

O processo MongoDB terá um comportamento diferente em diferentes políticas de alocação:

```

```

* `-membind=<nodes>`
Aloque apenas os nós listados. Mondeus não alocará memória nos nós listados e talvez não use toda a memória disponível.

* `-cpunodebind=<nodes>`
Executar somente nos nós. Mondeus só será executado nos nós especificados e usará apenas a memória disponível nesses nós.

* `-physcpubind=<nodes>`
Executar somente em CPUs (núcleos) listadas. Mondeus só será executado nas CPUs listadas e usará apenas a memória disponível nessas CPUs.

* `--localalloc`
Sempre alocar memória no nó atual, mas usar todos os nós em que o thread é executado. Se um thread executar alocação, então somente a memória disponível para essa CPU será usada.

* `--preferred=<node>`
Prefere a alocação a um nó, mas reverte para outros se o nó preferencial estiver cheio. A notação relativa para definir um nó pode ser usada. Além disso, os threads são executados em todos os nós.

Algumas das políticas podem resultar em menos do que toda a RAM disponível seja fornecida ao `mongod` processo. Ao contrário do MySQL, o MongoDB evita ativamente a paginação no nível do sistema operacional e, consequentemente, o `mongod` processo pode obter menos memória disponível.

#### Troca {#swapping}

Devido à natureza intensiva de memória dos bancos de dados, a troca no nível do sistema operacional deve ser desativada. O processo MongoDB evitará a troca por design.

#### Sistemas de arquivos remotos {#remote-filesystems}

Sistemas de arquivos remotos, como NFS, não são recomendados para arquivos de dados internos do MongoDB (os arquivos mondeus do banco de dados de processo), porque eles apresentam muita latência. Isso não deve ser confundido com o sistema de arquivos compartilhado necessário para o armazenamento do Oak Blob (FileDataStore), onde o NFS é recomendado.

#### Leia à frente {#read-ahead}

A leitura antecipada precisa ser ajustada para que, quando uma página for paginada usando uma leitura aleatória, os blocos desnecessários não sejam lidos do disco, resultando em consumo desnecessário de largura de banda de E/S.

### Requisitos Linux {#linux-requirements}

#### Versões mínimas do kernel {#minimum-kernel-versions}

* **2.6.23** para sistemas de `ext4` arquivos

* **2.6.25** para sistemas de `xfs` arquivos

#### Configurações recomendadas para discos de banco de dados {#recommended-settings-for-database-disks}

**Desativar tempo**

É recomendável que `atime` seja desativado para os discos que conterão os bancos de dados.

**Definir o agendador de discos NOOP**

Você pode fazer isso:

Primeiro, verifique o programador de E/S que está definido no momento. Isso pode ser feito executando o seguinte comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se a resposta for `noop` , não há nada que você precise fazer mais.

Se NOOP não for o programador de E/S configurado, você poderá alterá-lo executando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajustar o valor de leitura antecipada**

É recomendável usar um valor de 32 para os discos de onde os bancos de dados MongoDB são executados. Isso equivale a 16 quilobytes. Você pode defini-lo executando:

```shell
sudo blockdev --setra <value> <device>
```

#### Ativar NTP {#enable-ntp}

Verifique se o NTP está instalado e em execução no computador que está hospedando os bancos de dados MongoDB. Por exemplo, você pode instalá-lo usando o gerenciador de pacote yum em uma máquina CentOS:

```shell
sudo yum install ntp
```

Depois que o daemon NTP tiver sido instalado e iniciado com êxito, você poderá verificar o arquivo de derivação para o deslocamento de tempo do servidor.

#### Desativar páginas grandes transparentes {#disable-transparent-huge-pages}

O Red Hat Linux usa um algoritmo de gerenciamento de memória chamado THP (Transparent Huge Pages). É recomendável desativá-la se você estiver usando o sistema operacional para cargas de trabalho do banco de dados.

Você pode desativá-la seguindo o procedimento abaixo:

1. Abra o `/etc/grub.conf` arquivo no editor de texto de sua escolha.
1. Adicione a seguinte linha ao arquivo grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Finalmente, verifique se a configuração entrou em vigor executando:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se THP estiver desativado, a saída do comando acima deve ser:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Para obter mais informações sobre páginas grandes transparentes, consulte este [artigo](https://access.redhat.com/solutions/46111).

#### Desativar NUMA {#disable-numa}

Na maioria das instalações onde o NUMA está ativado, o daemon MongoDB o desativará automaticamente se for executado como um serviço da `/etc/init.d` pasta.

Caso contrário, você pode desativar o NUMA em um nível por processo. Para desativá-lo, execute estes comandos:

```shell
numactl --interleave=all <path_to_process>
```

Onde `<path_to_process>` está o caminho para o processo de mondeus.

Em seguida, desative a recuperação de zona executando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajustar as configurações máximas do processo mondeus {#tweak-the-ulimit-settings-for-the-mongod-process}

O Linux permite o controle configurável sobre a alocação de recursos por meio do `ulimit` comando. Isso pode ser feito com base em um usuário ou por processo.

É recomendável configurar o limite para o processo mondeus de acordo com as Configurações [máximas recomendadas do](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)MongoDB.

#### Teste o desempenho de E/S MongoDB {#test-mongodb-i-o-performance}

O MongoDB fornece uma ferramenta chamada `mongoperf` que é projetada para testar o desempenho de E/S. É recomendável usá-lo para testar o desempenho de todas as instâncias do MongoDB que compõem sua infraestrutura.

Para obter informações sobre como usar `mongoperf`, consulte a documentação [do](https://docs.mongodb.org/manual/reference/program/mongoperf/)MongoDB.

>[!NOTE]
>
>Observe que `mongoperf` é projetado para ser um indicador do desempenho do MongoDB na plataforma em que é executado. Por conseguinte, os resultados não devem ser considerados definitivos para a realização de um sistema de produção.
>
>Para obter resultados de desempenho mais precisos, você pode executar testes complementares com a ferramenta `fio` Linux.

**Teste o desempenho de leitura nas máquinas virtuais que compõem sua implantação**

Depois de instalar a ferramenta, alterne para o diretório de banco de dados MongoDB para executar os testes. Em seguida, inicie o primeiro teste executando `mongoperf`com esta configuração:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

A saída desejada deve atingir até dois gigabytes por segundo (2 GB/s) e 500.000 IOPS em execução a 32 threads para todas as instâncias MongoDB.

Execute um segundo teste, desta vez usando arquivos mapeados de memória, definindo o `mmf:true` parâmetro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

A saída do segundo teste deve ser consideravelmente superior à do primeiro, indicando o desempenho da transferência de memória.

>[!NOTE]
>
>Ao executar os testes, verifique as estatísticas de uso de E/S das máquinas virtuais em questão no sistema de monitoramento do sistema operacional. Se indicarem valores inferiores a 100% para leituras de E/S, pode haver um problema com a máquina virtual.

**Teste o desempenho de gravação da instância principal MongoDB**

Em seguida, verifique o desempenho de gravação de E/S da instância principal MongoDB executando `mongoperf` a partir do diretório de banco de dados MongoDB com as mesmas configurações:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

A saída desejada deve ser de 12 megabytes por segundo e atingir cerca de 3000 IOPS, com pouca variação entre o número de threads.

## Etapas para ambientes virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se você estiver usando o WMWare ESX para gerenciar e implantar seus ambientes virtualizados, certifique-se de executar as seguintes configurações no console ESX para acomodar a operação MongoDB:

1. Desativar balonamento de memória
1. Pré-alocar e reservar memória para as máquinas virtuais que hospedarão os bancos de dados MongoDB
1. Use o controle de E/S de armazenamento para alocar E/S suficiente ao `mongod` processo.
1. Garanta os recursos da CPU das máquinas que hospedam o MongoDB definindo a Reserva da [CPU](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Considere o uso de drivers de E/S ParaVirtual. Para obter mais informações sobre como fazer isso, consulte este artigo [da](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010398)base de conhecimento.

### Serviços Web da Amazon {#amazon-web-services}

Para obter a documentação sobre como configurar o MongoDB com os Serviços da Web da Amazon, consulte o artigo [Configurar integração](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) do AWS no site do MongoDB.

## Protegendo MongoDB antes da implantação {#securing-mongodb-before-deployment}

Consulte esta publicação para obter conselhos sobre como proteger a configuração de seus bancos de dados antes da implantação, implantando [com segurança o MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) .

## Dispatcher {#dispatcher}

### Escolhendo o sistema operacional para o Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Para atender adequadamente à implantação do MongoDB, o sistema operacional que hospedará o dispatcher deve estar executando o **Apache httpd** **versão 2.4 ou superior.**

Além disso, certifique-se de que todas as bibliotecas usadas na sua criação estejam atualizadas para minimizar as implicações de segurança.

### Configuração do Dispatcher {#dispatcher-configuration}

Uma configuração típica do Dispatcher servirá de dez a vinte vezes mais do throughput de solicitação de uma única instância do AEM.

Como o Dispatcher é principalmente apátrida, ele pode ser dimensionado horizontalmente com facilidade. Em algumas implantações, os autores precisam ser impedidos de acessar determinados recursos. Por isso, é altamente recomendável usar um dispatcher com as instâncias do autor.

A execução do AEM sem um despachante exigirá que a terminação SSL e o balanceamento de carga sejam executados por outro aplicativo. Isso é necessário porque as sessões devem ter afinidade com a instância do AEM em que foram criadas, um conceito conhecido como conexões aderentes. O objetivo disso é garantir que as atualizações do conteúdo exibam uma latência mínima.

Consulte a documentação [do](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) Dispatcher para obter mais informações sobre como configurá-la.

### Configuração adicional {#additional-configuration}

#### Conexões aderentes {#sticky-connections}

As conexões adesivas garantem que as páginas personalizadas e os dados da sessão de um usuário sejam todos compostos na mesma instância do AEM. Esses dados são armazenados na instância, portanto as solicitações subsequentes do mesmo usuário retornarão à mesma instância.

Recomenda-se que as conexões aderentes sejam ativadas para todas as solicitações de roteamento de camadas internas para as instâncias do AEM, incentivando solicitações subsequentes a atingirem a mesma instância do AEM. Isso ajudará a minimizar a latência que, de outra forma, seria perceptível quando o conteúdo for atualizado entre as instâncias.

#### Expira longa {#long-expires}

Por padrão, o conteúdo enviado de um despachante do AEM tem cabeçalhos Última modificação e Etag, sem nenhuma indicação de expiração do conteúdo. Embora isso garanta que a interface do usuário sempre obtenha a versão mais recente do recurso, isso também significa que o navegador executará uma operação GET para verificar se o recurso foi alterado. Isso pode resultar em várias solicitações nas quais a resposta HTTP é 304 (não modificada), dependendo do carregamento da página. Para recursos que não expiram, configurar um cabeçalho Expira e remover os cabeçalhos Última modificação e ETag farão com que o conteúdo seja armazenado em cache e nenhuma solicitação de atualização adicional seja feita até que a data no cabeçalho Expira seja atendida.

No entanto, usar esse método significa que não há uma maneira razoável de fazer com que o recurso expire no navegador antes que o cabeçalho Expira expire. Para atenuar isso, o HtmlClientLibraryManager pode ser configurado para usar URLs imutáveis para bibliotecas de clientes.

Esses URLs não devem ser alterados. Quando o corpo do recurso contido no URL for alterado, as alterações serão automaticamente refletidas no URL, garantindo que o navegador solicitará a versão correta do recurso.

A configuração padrão adiciona um seletor ao HtmlClientLibraryManager. Sendo um seletor, o recurso é armazenado em cache no dispatcher com o seletor intacto. Além disso, esse seletor pode ser usado para garantir o comportamento correto de expiração. O seletor padrão segue o `lc-.*?-lc` padrão. As seguintes diretivas de configuração httpd do Apache garantirão que todas as solicitações que correspondem a esse padrão sejam atendidas com um tempo de expiração adequado.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sem cheiro {#no-sniff}

Quando o conteúdo é enviado sem nenhum tipo de conteúdo, muitos navegadores tentarão adivinhar o tipo de conteúdo lendo os primeiros bytes do conteúdo. Isso se chama &quot;cheirar&quot;. O sniffing abre uma vulnerabilidade de segurança, pois os usuários que podem gravar no repositório podem carregar conteúdo mal-intencionado sem nenhum tipo de conteúdo.

Por isso, é aconselhável adicionar um `no-sniff` cabeçalho aos recursos servidos pelo expedidor. No entanto, o dispatcher não armazena os cabeçalhos em cache. Isso significa que qualquer conteúdo servido do sistema de arquivos local terá seu tipo de conteúdo determinado por sua extensão, em vez de usar o cabeçalho original do tipo de conteúdo do servidor de origem do AEM.

Nenhum cheirão pode ser ativado com segurança se o aplicativo da Web for conhecido por nunca servir recursos em cache sem um tipo de arquivo.

Você pode ativar No Sniff, inclusive:

```xml
Header set X-Content-Type-Options "nosniff"
```

Também pode ser ativado seletivamente:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Política de segurança de conteúdo {#content-security-policy}

As configurações padrão do dispatcher permitem uma Política de segurança de conteúdo aberta, também conhecida como CSP. Isso permite que uma página carregue recursos de todos os domínios sujeitos às políticas padrão da caixa de proteção do navegador.

É desejável restringir de onde os recursos podem ser carregados para evitar o carregamento de código no mecanismo javascript de servidores estrangeiros não confiáveis ou não verificados.

A DEP permite o ajuste fino das políticas. No entanto, num aplicativo complexo, os cabeçalhos do CSP precisam ser desenvolvidos com cuidado, uma vez que políticas que sejam muito restritivas podem quebrar partes da interface do usuário.

>[!NOTE]
>
>Para obter mais informações sobre como isso funciona, consulte a página [OWASP sobre a política](https://www.owasp.org/index.php/Content_Security_Policy)de segurança de conteúdo.

### Dimensionamento {#sizing}

Para obter mais informações sobre dimensionamento, consulte as Diretrizes [de dimensionamento de](/help/managing/hardware-sizing-guidelines.md)hardware.

### Otimização do desempenho do MongoDB {#mongodb-performance-optimization}

Para obter informações genéricas sobre o desempenho do MongoDB, consulte [Analisando o desempenho](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)do MongoDB.

## Limitações conhecidas {#known-limitations}

### Instalações Simultâneas {#concurrent-installations}

Embora o uso simultâneo de várias instâncias do AEM com um único banco de dados seja suportado pelo MongoMK, as instalações simultâneas não são.

Para contornar esse problema, primeiro execute a instalação com um único membro e adicione os outros depois que a primeira instalação terminar.

### Tamanho do nome da página {#page-name-length}

If AEM is running on a MongoMK persistence manager deployment, [page names are limited to 150 characters.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Consulte a documentação](https://docs.mongodb.com/manual/reference/limits/) do MongoDB para se familiarizar com as limitações e limites conhecidos do próprio MongoDB.

