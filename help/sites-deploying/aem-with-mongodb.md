---
title: Adobe Experience Manager com MongoDB
description: Saiba mais sobre as tarefas e considerações necessárias para uma implantação bem-sucedida do Adobe Experience Manager com MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 0%

---

# Adobe Experience Manager com MongoDB{#aem-with-mongodb}

Este artigo tem como objetivo melhorar o conhecimento sobre tarefas e considerações necessárias para a implantação bem-sucedida do AEM (Adobe Experience Manager) com MongoDB.

Para obter mais informações relacionadas à implantação, consulte o [Implantação e manutenção](/help/sites-deploying/deploy.md) da documentação.

## Quando usar MongoDB com AEM {#when-to-use-mongodb-with-aem}

O MongoDB é normalmente usado para oferecer suporte a implantações AEM autores, onde um dos seguintes critérios é atendido:

* Mais de 1000 usuários únicos por dia;
* Mais de 100 utilizadores simultâneos;
* Grandes volumes de edições de página;
* Grandes implantações ou ativações.

Os critérios acima são apenas para as instâncias de autor e não para qualquer instância de publicação que deve ser baseada em TarMK. O número de usuários se refere aos usuários autenticados, já que as instâncias de autor não permitem acesso não autenticado.

Se os critérios não forem atendidos, uma implantação ativa/standby do TarMK será recomendada para atender à disponibilidade. Geralmente, o MongoDB deve ser considerado em situações em que os requisitos de dimensionamento são maiores do que o que pode ser alcançado com um único item de hardware.

>[!NOTE]
>
>Informações adicionais sobre o dimensionamento de instâncias de autor e a definição de usuários simultâneos podem ser encontradas no [Diretrizes de dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Implantação mínima do MongoDB para AEM {#minimal-mongodb-deployment-for-aem}

Abaixo está uma implantação mínima para AEM no MongoDB. Para simplificar, a terminação SSL e os componentes de Proxy HTTP foram generalizados. Ele consiste em um único conjunto de réplicas do MongoDB, com um primário e dois segundos.

![chlimage_1-4](assets/chlimage_1-4.png)

Uma implantação mínima requer três `mongod` instâncias configuradas como um conjunto de réplicas. Uma instância é eleita primária com as outras instâncias sendo secundárias, com a eleição gerenciada por `mongod`. Anexado a cada instância há um disco local. Assim, o cluster pode suportar a carga, recomenda-se uma taxa de transferência mínima de 12 MB por segundo com mais de 3000 operações de E/S por segundo (IOPS).

Os autores do AEM são conectados à variável `mongod` com cada autor de AEM se conectando a todas as três `mongod` instâncias. As gravações são enviadas para o primário e as leituras podem ser lidas de qualquer uma das instâncias. O tráfego é distribuído com base no carregamento por um Dispatcher para qualquer uma das instâncias de autor AEM ativas. O armazenamento de dados do Oak é um `FileDataStore`, e o monitoramento do MongoDB é fornecido pelo MMS ou pelo MongoDB Ops Manager, dependendo da localização da implantação. O nível do sistema operacional e o monitoramento de log são fornecidos por soluções de terceiros, como Splunk ou Ganglia.

Nesta implantação, todos os componentes são necessários para uma implementação bem-sucedida. Qualquer componente ausente deixa a implementação não funcional.

### Sistemas operacionais {#operating-systems}

Para obter uma lista de sistemas operacionais compatíveis com o AEM 6, consulte o [Página Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Ambientes {#environments}

Os ambientes virtualizados são suportados desde que haja boa comunicação entre as diferentes equipes técnicas que executam o projeto. Esse suporte inclui a equipe que está executando AEM, a equipe que é proprietária do sistema operacional e a equipe que gerencia a infraestrutura virtualizada.

Existem requisitos específicos que abrangem a capacidade de E/S das instâncias do MongoDB que devem ser gerenciadas pela equipe que gerencia o ambiente virtualizado. Se o projeto usar uma implantação em nuvem, como o Amazon Web Services, as instâncias deverão ser provisionadas com capacidade e consistência de E/S suficientes para suportar as instâncias do MongoDB. Caso contrário, os processos MongoDB e o repositório Oak serão executados de forma inconfiável e irregular.

Nos ambientes virtualizados, o MongoDB requer configurações específicas de E/S e VM para garantir que o mecanismo de armazenamento do MongoDB não seja incapacitado pelas políticas de alocação de recursos da VMWare. Uma implementação bem-sucedida garante que não haja barreiras entre as várias equipes e que todas sejam assinadas para fornecer o desempenho necessário.

## Considerações sobre hardware {#hardware-considerations}

### Armazenamento {#storage}

Para alcançar o throughput de leitura e gravação com melhor desempenho sem a necessidade de dimensionamento horizontal prematuro, o MongoDB geralmente requer armazenamento ou armazenamento SSD com desempenho equivalente ao SSD.

### RAM {#ram}

As versões 2.6 e 3.0 do MongoDB que usam o mecanismo de armazenamento MMAP exigem que o conjunto de trabalho do banco de dados e seus índices se encaixem na RAM.

A RAM insuficiente resulta em uma redução significativa do desempenho. O tamanho do conjunto de trabalho e do banco de dados é altamente dependente do aplicativo. Embora algumas estimativas possam ser feitas, a maneira mais confiável de determinar a quantidade de RAM necessária é criar o aplicativo AEM e carregá-lo testando.

Para auxiliar no processo de teste de carga, pode-se assumir a seguinte relação entre o conjunto de trabalho e o tamanho total do banco de dados:

* 1:10 para armazenamento SSD
* 1:3 para armazenamento em disco rígido

Essas taxas significam que, para implantações de SSD, são necessários 200 GB de RAM para um banco de dados de 2 TB.

Embora as mesmas limitações se apliquem ao mecanismo de armazenamento WiredTiger no MongoDB 3.0, a correlação entre o conjunto de trabalho, a RAM e as falhas da página não é tão forte. O WiredTiger não usa o mapeamento de memória da mesma maneira que o mecanismo de armazenamento MMAP.

>[!NOTE]
>
>O Adobe recomenda o uso do mecanismo de armazenamento WiredTiger para implantações AEM 6.1 que estão usando o MongoDB 3.0.

### Armazenamento de dados {#data-store}

Devido às limitações do conjunto de trabalho do MongoDB, recomenda-se que o armazenamento de dados seja mantido independente do MongoDB. Na maioria dos ambientes, um `FileDataStore` usar um NAS disponível para todas as instâncias AEM deve ser usado. Para situações em que a Amazon Web Services é usada, também há uma `S3 DataStore`. Se por qualquer motivo, o armazenamento de dados for mantido no MongoDB, o tamanho do armazenamento de dados deverá ser adicionado ao tamanho total do banco de dados e os cálculos do conjunto de trabalho deverão ser ajustados adequadamente. Esse dimensionamento pode significar o provisionamento de mais RAM para manter o desempenho sem falhas na página.

## Monitoramento {#monitoring}

O acompanhamento é essencial para uma execução bem sucedida do projeto. Com conhecimento suficiente, é possível AEM no MongoDB sem monitoramento. No entanto, esse conhecimento costuma ser encontrado em engenheiros especializados em cada seção da implantação.

Esse conhecimento especializado geralmente envolve um engenheiro de P&amp;D que trabalha no Apache Oak Core e um especialista em MongoDB.

Sem monitoramento em todos os níveis, é necessário um conhecimento detalhado da base de código para diagnosticar problemas. Com o monitoramento em vigor e a orientação adequada sobre as principais estatísticas, as equipes de implementação podem reagir adequadamente às anomalias.

Embora seja possível usar ferramentas de linha de comando para obter um instantâneo rápido da operação de um cluster, fazer isso em tempo real em muitos hosts é quase impossível. As ferramentas de linha de comando raramente fornecem informações históricas além de alguns minutos e nunca permitem correlação cruzada entre diferentes tipos de métricas. Breve período de fundo lento `mongod` a sincronização requer um esforço manual significativo para correlacionar-se com a espera de E/S ou níveis de gravação excessivos em um recurso de armazenamento compartilhado de uma máquina virtual aparentemente desconectada.

### Gerenciador de nuvem do MongoDB {#mongodb-cloud-manager}

O MongoDB Cloud Manager é um serviço gratuito oferecido pelo MongoDB que permite o monitoramento e o gerenciamento de instâncias do MongoDB. Ele fornece uma visualização do desempenho e da integridade do cluster MongoDB em tempo real. Ele gerencia instâncias da nuvem e hospedadas de modo privado, desde que a instância possa acessar o servidor de monitoramento do Cloud Manager.

Ele requer um agente instalado na instância MongoDB que se conecta ao servidor de monitoramento. Há três níveis do agente:

* Um agente de automação que pode automatizar totalmente tudo no servidor MongoDB,
* Um agente de monitoramento que pode monitorar a `mongod` instância,
* Um agente de backup que pode realizar backups programados dos dados.

Embora o uso do Cloud Manager para automação de manutenção de um cluster MongoDB torne muitas das tarefas de rotina mais fáceis, ele não é necessário e nem está sendo usado para backup. No entanto, ao escolher o Cloud Manager para monitorar, é necessário monitorar.

Para obter mais informações sobre o MongoDB Cloud Manager, consulte o [Documentação do MongoDB](https://docs.cloud.mongodb.com/).

### Gerenciador de operações do MongoDB {#mongodb-ops-manager}

O MongoDB Ops Manager é o mesmo software que o MongoDB Cloud Manager. Depois de registrado, o Ops Manager pode ser baixado e instalado localmente em um data center privado ou em qualquer outro laptop ou desktop. Ele usa um banco de dados MongoDB local para armazenar dados e se comunicar da mesma forma que o Cloud Manager com os servidores gerenciados. Se você tiver políticas de segurança que proíbem um agente de monitoramento, deverá ser usado o Gerenciador de Operações do MongoDB.

### Monitoramento do sistema operacional {#operating-system-monitoring}

O monitoramento no nível do sistema operacional é necessário para executar um cluster MongoDB AEM.

Ganglia é um bom exemplo desse sistema e fornece uma imagem do intervalo e detalhes das informações necessárias que vão além das métricas básicas de saúde como CPU, média de carga e espaço livre em disco. Para diagnosticar problemas, são necessárias informações de nível inferior, como níveis de pool de entropia, Espera de E/S da CPU, soquetes no estado FIN_WAIT2.

### Agregação de log {#log-aggregation}

Com um cluster de vários servidores, a agregação de registros centrais é um requisito para um sistema de produção. Software como o Splunk oferece suporte à agregação de logs e permite que as equipes analisem os padrões de comportamento do aplicativo sem precisar coletar manualmente os logs.

## Listas de verificação {#checklists}

Esta seção trata de várias etapas que você deve tomar para garantir que as implantações do AEM e do MongoDB sejam configuradas corretamente antes da implementação do projeto.

### Rede {#network}

1. Primeiro, verifique se todos os hosts têm uma entrada DNS
1. Todos os hosts devem ser resolvidos pela entrada DNS de todos os outros hosts roteáveis
1. Todos os hosts MongoDB são roteáveis de todos os outros hosts MongoDB no mesmo cluster
1. Hosts MongoDB podem rotear pacotes para o MongoDB Cloud Manager e outros servidores de monitoramento
1. Os servidores AEM podem rotear pacotes para todos os servidores MongoDB
1. A latência de pacote entre qualquer servidor AEM e qualquer servidor MongoDB é menor que dois milissegundos, sem perda de pacote e uma distribuição padrão de um milissegundo ou menos.
1. Certifique-se de que não haja mais de dois saltos entre um AEM e um servidor MongoDB
1. Não há mais do que dois saltos entre dois servidores MongoDB
1. Não há roteadores superiores ao Nível 3 de OSI entre qualquer servidor principal (MongoDB ou AEM ou qualquer combinação).
1. Se for usado o truncamento de VLAN ou qualquer forma de túnel de rede, ele deverá estar em conformidade com as verificações de latência de pacote.

### Configuração de AEM {#aem-configuration}

#### Configuração do armazenamento de nós {#node-store-configuration}

As instâncias de AEM devem ser configuradas para usar AEM com MongoMK. A base da implementação do MongoMK no AEM é o Document Node Store.

Para obter mais informações sobre como configurar Lojas de nós, consulte [Configuração de armazenamentos de nó e armazenamentos de dados em AEM](/help/sites-deploying/data-store-config.md).

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
O AEM do servidor MongoDB deve se conectar. As conexões são feitas a todos os membros conhecidos do conjunto de réplicas padrão. Se o MongoDB Cloud Manager for usado, a segurança do servidor será ativada. Portanto, a cadeia de conexão deve conter um nome de usuário e senha adequados. As versões não empresariais do MongoDB suportam apenas autenticação de nome de usuário e senha. Para obter mais informações sobre a sintaxe da string de conexão, consulte o [documentação](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
O nome do banco de dados. O padrão para AEM é 
`aem-author`.

* `customBlobStore`
Se a implantação armazenar binários no banco de dados, eles farão parte do conjunto de trabalho. Por esse motivo, é recomendável não armazenar binários no MongoDB, preferindo um armazenamento de dados alternativo como um 
`FileSystem` armazenamento de dados em um NAS.

* `cache`
O tamanho do cache em megabytes. Esse espaço é distribuído entre vários caches usados no 
`DocumentNodeStore`. O padrão é 256 MB. No entanto, o Oak lê os benefícios de desempenho de um cache maior.

* `blobCacheSize`
Os blobs usados com frequência podem ser armazenados em cache pelo AEM para evitar a sua recuperação do armazenamento de dados. Isso afeta mais o desempenho, especialmente ao armazenar blobs no banco de dados do MongoDB. Todos os Data Stores baseados no sistema de arquivos se beneficiam do cache de disco no nível do sistema operacional.

#### Configuração do armazenamento de dados {#data-store-configuration}

O Data Store é usado para armazenar arquivos de tamanho maior que um limite. Abaixo desse limite, os arquivos são armazenados como propriedades no Document Node Store. Se a variável `MongoBlobStore` é usada, uma coleção dedicada é criada no MongoDB para armazenar os blobs. Essa coleção contribui para o conjunto de trabalho da variável `mongod` e exige que `mongod` tem mais RAM para evitar problemas de desempenho. Por esse motivo, a configuração recomendada é evitar a variável `MongoBlobStore` para implantações de produção e uso `FileDataStore` com o backup de um NAS compartilhado entre todas as instâncias AEM. Como o cache no nível do sistema operacional é eficiente no gerenciamento de arquivos, o tamanho mínimo de um arquivo no disco deve ser definido próximo ao tamanho do bloco do disco. Isso garante que o sistema de arquivos seja usado com eficiência e muitos documentos pequenos não contribuem excessivamente para o conjunto de trabalho da `mongod` instância.

Esta é uma configuração típica do Data Store para uma implantação de AEM mínima com o MongoDB:

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
Tamanho em bytes. Os binários com menos de ou igual a esse tamanho são armazenados com o Armazenamento de nós do documento. Em vez de armazenar a ID do blob, o conteúdo do binário é armazenado. Com binários maiores que esse tamanho, a ID do binário é armazenada como uma propriedade do Documento na coleção de nós. E o corpo do binário é armazenado no 
`FileDataStore` no disco. 4096 bytes é um tamanho típico de bloco do sistema de arquivos.

* `path`
O caminho para a raiz do armazenamento de dados. Para uma implantação do MongoMK, esse caminho deve ser um sistema de arquivos compartilhado disponível para todas as instâncias AEM. Normalmente, é usado um servidor NAS (Network Attached Storage, armazenamento conectado à rede). Para implantações em nuvem como o Amazon Web Services, a variável 
`S3DataFileStore` também está disponível.

* `cacheSizeInMB`
O tamanho total do cache binário em Megabytes. É usado para armazenar em cache binários menores que o 
`maxCacheBinarySize` configuração.

* `maxCachedBinarySize`
O tamanho máximo em bytes de um binário armazenado em cache no cache binário. Se um Data Store baseado no sistema de arquivos for usado, não é recomendável usar valores altos para o cache do Data Store, pois os binários já estão armazenados em cache pelo sistema operacional.

#### Desabilitando a Dica de Consulta {#disabling-the-query-hint}

É recomendável desativar a dica de consulta enviada com todas as consultas adicionando a propriedade `-Doak.mongo.disableIndexHint=true` quando começar a AEM. Isso garante que o MongoDB calcule o índice mais apropriado para ser usado com base em estatísticas internas.

Se a dica de consulta não estiver desativada, qualquer ajuste de desempenho de índices não terá impacto no desempenho da AEM.

#### Ativar Cache Persistente para MongoMK {#enable-persistent-cache-for-mongomk}

Recomenda-se que uma configuração de cache persistente seja ativada para implantações do MongoDB, para maximizar a velocidade para ambientes com alto desempenho de leitura de E/S. Para obter mais detalhes, consulte a [Documentação do Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Otimizações do sistema operacional MongoDB {#mongodb-operating-system-optimizations}

### Suporte de sistema operacional {#operating-system-support}

O MongoDB 2.6 usa um mecanismo de armazenamento mapeado de memória que é sensível a alguns aspectos do gerenciamento de nível do sistema operacional entre RAM e disco. O Desempenho de consulta e leitura da instância do MongoDB depende de evitar ou eliminar operações lentas de E/S frequentemente chamadas de falhas de página. Esses problemas são falhas de página que se aplicam à variável `mongod` em particular. Não confunda com falhas de página no nível do sistema operacional.

Para operação rápida, o banco de dados MongoDB deve acessar apenas os dados que já estão na RAM. Os dados que ele deve acessar são compostos de índices e dados. Essa coleção de índices e dados é chamada de conjunto de trabalho. Onde o conjunto de trabalho for maior que a RAM disponível, o MongoDB terá que pagá-los a partir de um disco que incorre em um custo de E/S, removendo outros dados já na memória. Se o despejo fizer com que os dados sejam recarregados do disco, as falhas da página serão dominadas e o desempenho será degradado. Onde o conjunto de trabalho é dinâmico e variável, mais falhas de página são incorridas para suportar operações.

O MongoDB é executado em vários sistemas operacionais, incluindo uma grande variedade de sabores Linux®, Windows e macOS. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obter mais detalhes. Dependendo da escolha do seu sistema operacional, o MongoDB tem diferentes recomendações de nível de sistema operacional. Há documentos em [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) e resumido aqui para conveniência.

#### Linux® {#linux}

* Desative páginas iniciais transparentes e desfragmente. Consulte [Configurações de Páginas Enormes Transparentes](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) para obter mais informações.
* [Ajustar as configurações de leitura antecipada](https://docs.mongodb.com/manual/administration/production-notes/#readahead) nos dispositivos que armazenam os arquivos do banco de dados para que você se ajuste ao caso de uso.

   * Para o mecanismo de armazenamento MMAPv1, se seu conjunto de trabalho for maior que a RAM disponível e o padrão de acesso ao documento for aleatório, considere reduzir a leitura antes de 32 ou 16. Avalie configurações diferentes para encontrar um valor ideal que maximize a memória residente e diminua o número de falhas da página.
   * Para o mecanismo de armazenamento WiredTiger, defina com antecedência para 0 independentemente do tipo de mídia de armazenamento (girando, SSD e assim por diante). Em geral, use a configuração de leitura antecipada recomendada, a menos que o teste mostre um benefício mensurável, repetível e confiável em um valor de leitura antecipada mais alto. [Suporte profissional ao MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) pode fornecer conselhos e orientação sobre configurações leituras antecipadas diferentes de zero.

* Desative a ferramenta sintonizada se estiver executando o RHEL 7 / CentOS 7 em um ambiente virtual.
* Quando o RHEL 7/CentOS 7 é executado em um ambiente virtual, a ferramenta sintonizada chama automaticamente um perfil de desempenho derivado da taxa de transferência de desempenho, que define automaticamente as configurações de leitura antecipada em 4 MB. Essa configuração pode afetar negativamente o desempenho.
* Use os programadores de disco noop ou deadline para unidades SSD.
* Use o agendador de disco noop para unidades virtualizadas em VMs convidadas.
* Desative NUMA ou defina `vm.zone_reclaim_mode` para 0 e execute [monge](https://docs.mongodb.com/manual/administration/production-notes/#readahead) instâncias com intercalação de nó. Consulte: [Hardware MongoDB e NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obter mais informações.

* Ajuste os valores máximos no hardware para que eles se encaixem no caso de uso. Se vários [monge](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) ou [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) instâncias estão sendo executadas no mesmo usuário, dimensione os valores de limite de acordo. Consulte: [Configurações de limite UNIX®](https://docs.mongodb.com/manual/reference/ulimit/) para obter mais informações.

* Use o aviso para o [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) ponto de montagem.
* Configure identificadores de arquivos suficientes (fs.file-max), limites de pid do kernel (kernel.pid_max) e threads máximos por processo (kernel.threads-max) para sua implantação. Para sistemas grandes, os seguintes valores fornecem um bom ponto de partida:

   * fs.file-max valor 98000,
   * valor kernel.pid_max de 64000,
   * andkernel.threads-valor máximo de 64000

* Certifique-se de que o sistema tenha espaço de troca configurado. Consulte a documentação do seu sistema operacional para obter detalhes sobre o dimensionamento apropriado.
* Certifique-se de que a manutenção TCP predefinida do sistema está definida corretamente. Um valor de 300 geralmente oferece melhor desempenho para conjuntos de réplicas e clusters compartilhados. Consulte: [O tempo de manutenção do TCP afeta as implantações do MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) nas Perguntas frequentes para obter mais informações.

#### Windows {#windows}

* Considere desativar as atualizações de &quot;último tempo de acesso&quot; do NTFS. Essa configuração é análoga à desativação do tempo em sistemas semelhantes ao Unix.

### WiredTiger {#wiredtiger}

A partir do MongoDB 3.2, o mecanismo de armazenamento padrão para MongoDB é o mecanismo de armazenamento WiredTiger. Esse mecanismo fornece alguns recursos robustos e escaláveis que o tornam muito mais adequado para cargas de trabalho gerais de banco de dados. As seções a seguir descrevem esses recursos.

#### Moeda de nível de documento {#document-level-concurrency}

O WiredTiger usa o controle de simultaneidade no nível do documento para operações de gravação. Como resultado, vários clientes podem modificar documentos diferentes de uma coleção ao mesmo tempo.

Para a maioria das operações de leitura e gravação, o WiredTiger usa controle de simultaneidade otimista. O WiredTiger usa apenas bloqueios de intenção nos níveis global, de banco de dados e de coleta. Quando o mecanismo de armazenamento detecta conflitos entre duas operações, há um conflito de gravação que faz com que o MongoDB repita essa operação de forma transparente. Algumas operações globais, normalmente operações de curta duração envolvendo vários bancos de dados, ainda exigem um bloqueio global &quot;em toda a instância&quot;.

Algumas outras operações, como a remoção de uma coleção, ainda exigem um bloqueio de banco de dados exclusivo.

#### Instantâneos e pontos de verificação {#snapshots-and-checkpoints}

O WiredTiger usa o MVCC (MultiVersion Concurrency Control). No início de uma operação, o WiredTiger fornece um instantâneo point-in-time dos dados da transação. Um instantâneo apresenta uma exibição consistente dos dados na memória.

Ao gravar no disco, o WiredTiger grava todos os dados em um instantâneo no disco de uma maneira consistente em todos os arquivos de dados. O agora - [durável](https://docs.mongodb.com/manual/reference/glossary/#term-durable) Os dados atuam como um ponto de verificação nos arquivos de dados. O ponto de verificação garante que os arquivos de dados sejam consistentes até o último ponto de verificação, inclusive. Ou seja, os pontos de verificação podem atuar como pontos de recuperação.

O MongoDB configura o WiredTiger para criar pontos de verificação (ou seja, gravar os dados do snapshot no disco) em intervalos de 60 segundos ou 2 GB de dados do diário.

Durante a gravação de um novo ponto de verificação, o ponto de verificação anterior ainda é válido. Dessa forma, mesmo que MongoDB termine ou encontre um erro ao gravar um novo ponto de verificação, após a reinicialização, o MongoDB poderá se recuperar do último ponto de verificação válido.

O novo ponto de verificação se torna acessível e permanente quando a tabela de metadados da WiredTiger é atualizada automaticamente para fazer referência ao novo ponto de verificação. Quando o novo ponto de verificação estiver acessível, o WiredTiger liberará as páginas dos pontos de verificação antigos.

Utilizando WiredTiger, mesmo sem [diário](https://docs.mongodb.com/manual/reference/glossary/#term-durable), MongoDB pode se recuperar do último ponto de verificação; no entanto, para recuperar as alterações feitas após o último ponto de verificação, execute com [diário](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diário {#journal}

WiredTiger usa uma combinação de logon de transação de gravação com [pontos de verificação](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) para garantir a durabilidade dos dados.

O diário WiredTiger mantém todas as modificações de dados entre pontos de verificação. Se o MongoDB sair entre pontos de verificação, ele usará o diário para reproduzir todos os dados modificados desde o último ponto de verificação. Para obter informações sobre a frequência com que o MongoDB grava os dados do diário no disco, consulte [Processo de Lançamento](https://docs.mongodb.com/manual/core/journaling/#journal-process).

O diário WiredTiger é compactado usando o [molho](https://docs.mongodb.com/manual/core/journaling/#journal-process) biblioteca de compactação. Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use a [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) configuração.

Consulte [Jornando com WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>O tamanho mínimo do registro de log para WiredTiger é de 128 bytes. Se um registro de log tiver 128 bytes ou menos, WiredTiger não compactará esse registro.
>
>Você pode desativar o diário definindo [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) para falso, o que pode reduzir a sobrecarga da manutenção do diário.
>
>Para [autônoma](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) instâncias, não usar o diário significa que você perde algumas modificações de dados quando o MongoDB sai inesperadamente entre pontos de verificação. Para membros do [conjuntos de réplicas](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), o processo de replicação pode fornecer garantias suficientes de durabilidade.

#### Compactação {#compression}

Com o WiredTiger, o MongoDB oferece suporte à compactação para todas as coleções e índices. A compactação minimiza o uso do armazenamento em detrimento da CPU adicional.

Por padrão, o WiredTiger usa compactação de bloco com a variável [molho](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) biblioteca de compactação para todas as coleções e [compactação de prefixo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) para todos os índices.

Para coleções, bloqueie a compactação com [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) também está disponível. Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use a [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) configuração.

Para índices, para desativar [compactação de prefixo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), use o [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) configuração.

As configurações de compactação também são configuráveis por coleção e por índice durante a criação da coleção e do índice. Consulte [Especificar opções do mecanismo de armazenamento](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) e [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) opção.

Para a maioria das cargas de trabalho, as configurações de compactação padrão equilibram a eficiência do armazenamento e os requisitos de processamento.

O diário WiredTiger também é compactado por padrão. Para obter informações sobre compactação de diário, consulte [Diário](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso de memória {#memory-use}

Com o WiredTiger, o MongoDB usa o cache interno do WiredTiger e o cache do sistema de arquivos.

A partir do 3.4, o cache interno do WiredTiger, por padrão, usa o maior dos seguintes itens:

* 50% de RAM menos 1 GB ou
* 256 MB

Por padrão, o WiredTiger usa a compactação de bloco Snappy para todas as coleções e a compactação de prefixo para todos os índices. Os padrões de compactação são configuráveis em um nível global e também podem ser definidos em uma base por coleção e por índice durante a criação da coleção e do índice.

Diferentes representações são usadas para dados no cache interno do WiredTiger em relação ao formato no disco:

* Os dados no cache do sistema de arquivos são iguais ao formato no disco, incluindo benefícios de qualquer compactação para arquivos de dados. O cache do sistema de arquivos é usado pelo sistema operacional para reduzir a E/S do disco.

Os índices carregados no cache interno do WiredTiger têm uma representação de dados diferente no formato no disco, mas ainda podem aproveitar a compactação de prefixo de índice para reduzir o uso de RAM.

A compactação de prefixo de índice remove a duplicação de prefixos comuns de campos indexados.

Os dados de coleta no cache interno do WiredTiger são descompactados e usam uma representação diferente do formato no disco. A compactação em bloco pode fornecer economia significativa no armazenamento em disco, mas os dados devem ser descompactados para serem manipulados pelo servidor.

Através do cache do sistema de arquivos, o MongoDB usa automaticamente toda a memória livre que não é usada pelo cache WiredTiger ou por outros processos.

Para ajustar o tamanho do cache interno do WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar o tamanho do cache interno do WiredTiger acima do valor padrão.

### NUMA {#numa}

O NUMA (Non-Uniform Memory Access — Acesso Não Uniforme à Memória) permite que um kernel gerencie como a memória é mapeada para os núcleos do processador. Embora esse processo tente tornar o acesso à memória mais rápido para os núcleos, garantindo que eles sejam capazes de acessar os dados necessários, o NUMA interfere no MMAP, introduzindo uma latência adicional, pois a leitura não pode ser prevista. Como resultado, NUMA deve ser desativado para a variável `mongod` processar em todos os sistemas operacionais com capacidade.

Em essência, em uma arquitetura NUMA, a memória é conectada às CPUs e as CPUs são conectadas a um barramento. Em uma arquitetura SMP ou UMA, a memória é conectada ao barramento e compartilhada pelas CPUs. Quando um thread aloca memória em uma CPU NUMA, ele aloca de acordo com uma política. O padrão é alocar memória conectada à CPU local do thread, a menos que não haja disponibilidade, e nesse ponto ela usa memória de uma CPU gratuita a um custo mais alto. Depois de alocada, a memória não se move entre CPUs. A alocação é executada por uma política herdada do thread principal, que é, em última análise, o thread que iniciou o processo.

Em muitos bancos de dados que veem o computador como uma arquitetura de memória multicore uniforme, esse cenário faz com que a CPU inicial fique cheia primeiro e o preenchimento da CPU secundária mais tarde. Isso é especialmente verdadeiro se um thread central for responsável por alocar buffers de memória. A solução é alterar a política NUMA do thread principal usado para iniciar o `mongod` execute o seguinte comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Essa política aloca memória em uma maneira arredondada em todos os nós da CPU, garantindo uma distribuição uniforme em todos os nós. Ele não gera o mais alto desempenho de acesso à memória como em sistemas com vários hardwares de CPU. Cerca de metade das operações de memória são mais lentas e acima do barramento, mas `mongod` O não foi escrito para direcionar o NUMA de forma ótima, por isso é um compromisso razoável.

### Problemas NUMA {#numa-issues}

Se a variável `mongod` O processo é iniciado a partir de um local diferente do `/etc/init.d` , é provável que ele não tenha sido iniciado com a política NUMA correta. Dependendo da política padrão, podem surgir problemas. O motivo é que os vários instaladores do Gerenciador de pacotes Linux® para MongoDB também instalam um serviço com arquivos de configuração em `/etc/init.d` que executam a etapa descrita acima. Se você instalar e executar o MongoDB diretamente de um arquivo ( `.tar.gz`), você deve executar manualmente mongod sob o comando `numactl` processo.

>[!NOTE]
>
>Para obter mais informações sobre as políticas NUMA disponíveis, consulte o [documentação numérica](https://linux.die.net/man/8/numactl).

O processo MongoDB se comporta de forma diferente em diferentes políticas de alocação:

```

```

* `-membind=<nodes>`
Aloque somente os nós listados. Mongod não aloca memória em nós listados e pode não usar toda a memória disponível.

* `-cpunodebind=<nodes>`
Executar apenas nos nós. Mongod só é executado apenas nos nós especificados e só usa a memória disponível nesses nós.

* `-physcpubind=<nodes>`
Executar apenas em CPUs (núcleos) listadas. O Mongod só é executado apenas nas CPUs listadas e só usa a memória disponível nessas CPUs.

* `--localalloc`
Aloca sempre memória no nó atual, mas use todos os nós em que o thread é executado. Se um thread executar a alocação, somente a memória disponível para essa CPU será usada.

* `--preferred=<node>`
Prefere a alocação a um nó, mas retorna para outros se o nó preferencial estiver cheio. Pode ser usada a notação relativa para definir um nó. Além disso, os threads são executados em todos os nós.

Algumas políticas podem resultar em menos do que toda a RAM disponível sendo fornecida ao `mongod` processo. Ao contrário do MySQL, o MongoDB evita ativamente a paginação no nível do sistema operacional e, portanto, a variável `mongod` O processo pode ter menos memória disponível.

#### Troca {#swapping}

Devido à natureza intensiva de memória dos bancos de dados, a troca no nível do sistema operacional deve ser desativada. O processo MongoDB evita a troca por design.

#### Sistemas de arquivos remotos {#remote-filesystems}

Sistemas de arquivos remotos, como NFS, não são recomendados para arquivos de dados internos do MongoDB (os arquivos mongod process database) , pois apresentam muita latência. Não confunda com o sistema de arquivos compartilhado necessário para o armazenamento do Oak Blob (FileDataStore), onde NFS é recomendado.

#### Ler à frente {#read-ahead}

Ajuste Lido em frente para que, quando uma página é paginada usando uma leitura aleatória, blocos desnecessários não sejam lidos do disco. Esses resultados significam um consumo desnecessário de largura de banda de E/S.

### Requisitos do Linux® {#linux-requirements}

#### Versões mínimas do kernel {#minimum-kernel-versions}

* **2.6.23** para `ext4` filesystems

* **2.6.25** para `xfs` filesystems

#### Configurações recomendadas para discos de banco de dados {#recommended-settings-for-database-disks}

**Desativar tempo**

Recomenda-se que `atime` está desativado para os discos que contêm os bancos de dados.

**Definir o agendador de discos NOOP**

Faça o seguinte:

Primeiro, verifique o programador de E/S definido executando o seguinte comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se a resposta for `noop`Não há mais nada que você deva fazer.

Se NOOP não for o programador de E/S configurado, é possível alterá-lo executando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajustar o valor de leitura antecipada**

É recomendável usar um valor de 32 para os discos em que os bancos de dados MongoDB são executados. Esse valor é de 16 KB. Você pode defini-lo executando o seguinte:

```shell
sudo blockdev --setra <value> <device>
```

#### Ativar NTP {#enable-ntp}

Certifique-se de ter o NTP instalado e em execução na máquina que está hospedando os bancos de dados do MongoDB. Por exemplo, você pode instalá-lo usando o Gerenciador de Pacotes de yum em uma máquina CentOS:

```shell
sudo yum install ntp
```

Depois que o daemon NTP for instalado e iniciado com êxito, você poderá verificar o arquivo de deriva para o deslocamento de tempo do seu servidor.

#### Desativar Páginas Enormes e Transparentes {#disable-transparent-huge-pages}

O Red Hat® Linux® usa um algoritmo de gerenciamento de memória chamado THP (Transparent Huge Pages). É recomendável desativá-lo se estiver usando o sistema operacional para cargas de trabalho do banco de dados.

Você pode desativá-lo seguindo o procedimento abaixo:

1. Abra o `/etc/grub.conf` no editor de texto de sua escolha.
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
>Para obter mais informações sobre Páginas enormes e transparentes, consulte esta seção [artigo](https://access.redhat.com/solutions/46111).

#### Desativar NUMA {#disable-numa}

Na maioria das instalações em que o NUMA está ativado, o daemon do MongoDB o desabilita automaticamente se for executado como um serviço do `/etc/init.d` pasta.

Se esse não for o caso, você pode desativar o NUMA em um nível por processo. Para desativá-lo, execute os seguintes comandos:

```shell
numactl --interleave=all <path_to_process>
```

Onde `<path_to_process>` é o caminho para o processo mongod.

Em seguida, desative a recuperação de zona executando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajustar as configurações de limite do processo mongod {#tweak-the-ulimit-settings-for-the-mongod-process}

O Linux® permite um controle configurável sobre a alocação de recursos por meio do `ulimit` comando. Essa configuração pode ser feita de acordo com um usuário ou por processo.

É recomendável configurar o ulimit para o processo mongod de acordo com o [Configurações de limite recomendadas do MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Teste de desempenho de E/S do MongoDB {#test-mongodb-i-o-performance}

O MongoDB fornece uma ferramenta chamada `mongoperf` criado para testar o desempenho de E/S. É recomendável usá-lo para testar o desempenho de todas as instâncias do MongoDB que compõem sua infraestrutura.

Para obter informações sobre como usar `mongoperf`, visualize o [Documentação do MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>O `mongoperf` é um indicador do desempenho do MongoDB na plataforma em que é executado. Por conseguinte, os resultados não devem ser considerados definitivos para o desempenho de um sistema de produção.
>
>Para obter resultados de desempenho mais precisos, você pode executar testes complementares com o `fio` Ferramenta Linux®.

**Teste o desempenho de leitura nas máquinas virtuais que compõem sua implantação**

Depois de instalar a ferramenta, alterne para o diretório do banco de dados MongoDB para executar os testes. Em seguida, inicie o primeiro teste executando `mongoperf`com esta configuração:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

A saída desejada deve alcançar até dois gigabytes por segundo (2 GB/s) e 500.000 IOPS executando em 32 threads para todas as instâncias do MongoDB.

Execute um segundo teste, desta vez usando arquivos mapeados de memória, definindo a variável `mmf:true` parâmetro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

A saída do segundo teste deve ser consideravelmente superior à do primeiro, indicando o desempenho da transferência de memória.

>[!NOTE]
Ao executar os testes, verifique as estatísticas de uso de E/S das máquinas virtuais em questão no sistema de monitoramento do sistema operacional. Se indicarem valores inferiores a 100% para leituras de E/S, pode haver um problema com a máquina virtual.

**Teste o desempenho de gravação da instância principal do MongoDB**

Em seguida, verifique o desempenho de gravação de E/S da instância principal do MongoDB executando `mongoperf` no diretório do banco de dados MongoDB com as mesmas configurações:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

A saída desejada deve ser de 12 megabytes por segundo e atingir cerca de 3000 IOPS, com pouca variação entre o número de threads.

## Etapas para ambientes virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se estiver usando o WMWare ESX para gerenciar e implantar seus ambientes virtualizados, certifique-se de executar as seguintes configurações do console ESX para acomodar a operação MongoDB:

1. Desativar o balão de memória
1. Pré-alocar e reservar memória para as máquinas virtuais que hospedam os bancos de dados do MongoDB
1. Use o controle de E/S de armazenamento para alocar E/S suficiente para a `mongod` processo.
1. Garanta os recursos da CPU das máquinas que hospedam o MongoDB ao configurar [Reserva de CPU](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. Considere o uso de drivers de I/O paraVirtual. Consulte [artigo da base de conhecimento](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Para obter documentação sobre como configurar o MongoDB com o Amazon Web Services, verifique o [Configurar a integração do AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) artigo no site do MongoDB.

## Proteção do MongoDB antes da implantação {#securing-mongodb-before-deployment}

Veja esta publicação em [implantação segura do MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) para obter conselhos sobre como proteger a configuração de seus bancos de dados antes da implantação.

## Dispatcher {#dispatcher}

### Escolha do sistema operacional para o Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Para servir adequadamente sua implantação do MongoDB, o sistema operacional que hospeda o Dispatcher deve estar em execução **Apache httpd** **versão 2.4 ou superior.**

Além disso, certifique-se de que todas as bibliotecas usadas na criação estejam atualizadas para minimizar as implicações de segurança.

### Configuração do Dispatcher {#dispatcher-configuration}

Uma configuração típica do Dispatcher serve entre dez e 20 vezes mais a taxa de transferência de solicitação de uma única instância de AEM.

Como o Dispatcher não tem estado, ele pode ser dimensionado horizontalmente com facilidade. Em algumas implantações, os autores devem ser restritos de acessar determinados recursos. É recomendável usar um Dispatcher com as instâncias de autor.

Executar AEM sem um Dispatcher requer que a terminação SSL e o balanceamento de carga sejam executados por outro aplicativo. Isso é necessário porque as sessões devem ter afinidade para a instância de AEM em que são criadas, um conceito conhecido como conexões aderentes. O motivo é garantir que as atualizações no conteúdo exibam latência mínima.

Verifique a [Documentação do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para obter mais informações sobre como configurá-lo.

### Configuração adicional {#additional-configuration}

#### Conexões adesivas {#sticky-connections}

As conexões adesivas garantem que as páginas personalizadas e os dados de sessão de um usuário sejam todos compostos na mesma instância do AEM. Esses dados são armazenados na instância, portanto as solicitações subsequentes do mesmo usuário retornam à mesma instância.

Recomenda-se que as conexões aderentes sejam habilitadas para todas as solicitações de roteamento de camadas internas para as instâncias de AEM, incentivando as solicitações subsequentes a alcançar a mesma instância de AEM. Isso ajuda a minimizar a latência, que de outra forma seria perceptível quando o conteúdo é atualizado entre instâncias.

#### Expira longa {#long-expires}

Por padrão, o conteúdo enviado de um Dispatcher AEM tem cabeçalhos Last-Modified e Etag , sem nenhuma indicação da expiração do conteúdo. Esse fluxo garante que a interface do usuário sempre obtenha a versão mais recente do recurso. Também significa que o navegador executa uma operação GET para ver se o recurso foi alterado. Como resultado, pode resultar em várias solicitações para as quais a resposta HTTP é 304 (Não modificada), dependendo do carregamento da página. Para recursos que não expiram, definir um cabeçalho Expires e remover os cabeçalhos Last-Modified e ETag fazem com que o conteúdo seja armazenado em cache. E, nenhuma outra solicitação de atualização é feita até que a data no cabeçalho Expires seja atendida.

No entanto, usar esse método significa que não há uma maneira razoável de fazer com que o recurso expire no navegador antes que o cabeçalho Expires expire. Para mitigar esse fluxo de trabalho, o HtmlClientLibraryManager pode ser configurado para usar URLs imutáveis para bibliotecas de clientes.

Esses URLs não devem ser alterados. Quando o corpo do recurso contido no URL muda, as alterações são refletidas no URL, garantindo que o navegador solicite a versão correta do recurso.

A configuração padrão adiciona um seletor ao HtmlClientLibraryManager. Sendo um seletor, o recurso é armazenado em cache no Dispatcher com o seletor intacto. Além disso, esse seletor pode ser usado para garantir o comportamento de expiração correto. O seletor padrão segue o `lc-.*?-lc` padrão. As seguintes diretivas de configuração de httpd do Apache garantem que todas as solicitações que correspondem a esse padrão sejam atendidas com um tempo de expiração adequado.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sem cheira {#no-sniff}

Quando o conteúdo é enviado sem tipo de conteúdo, muitos navegadores tentam adivinhar o tipo de conteúdo lendo os primeiros bytes do conteúdo. Este método é chamado de &quot;sniffing&quot;. O sniffing abre uma vulnerabilidade de segurança, pois os usuários que podem gravar no repositório podem fazer upload de conteúdo mal-intencionado sem nenhum tipo de conteúdo.

Por isso, é aconselhável adicionar um `no-sniff` cabeçalho para recursos servidos pelo Dispatcher. No entanto, o Dispatcher não armazena cabeçalhos em cache. Dessa forma, significa que qualquer conteúdo servido do sistema de arquivos local tem seu tipo de conteúdo determinado pela extensão, em vez de usar o cabeçalho de tipo de conteúdo original do servidor de origem AEM.

Nenhum sniff poderá ser ativado com segurança se o aplicativo Web for conhecido por nunca fornecer recursos em cache sem um tipo de arquivo.

Você pode ativar Sem farejo, inclusive:

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

As configurações padrão do Dispatcher permitem uma Política de segurança de conteúdo aberta, também conhecida como CSP. Essas configurações permitem que uma página carregue recursos de todos os domínios sujeitos às políticas padrão da sandbox do navegador.

É desejável restringir de onde os recursos podem ser carregados para evitar o carregamento de código para o mecanismo JavaScript de servidores estrangeiros não confiáveis ou não verificados.

A CSP permite o ajuste fino das políticas. No entanto, em um aplicativo complexo, os cabeçalhos de CSP devem ser desenvolvidos com cuidado, já que políticas muito restritivas podem quebrar partes da interface do usuário.

>[!NOTE]
Para obter mais informações sobre como isso funciona, consulte o [Página OWASP sobre a política de segurança de conteúdo](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Dimensionamento {#sizing}

Para obter mais informações sobre dimensionamento, consulte o [Diretrizes de dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md).

### Otimização de desempenho do MongoDB {#mongodb-performance-optimization}

Para obter informações genéricas sobre o desempenho do MongoDB, consulte [Análise do desempenho do MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitações conhecidas {#known-limitations}

### Instalações simultâneas {#concurrent-installations}

Embora o uso simultâneo de várias instâncias de AEM com um único banco de dados seja compatível com o MongoMK, as instalações simultâneas não são.

Para contornar esse problema, execute a instalação com um único membro primeiro e adicione os outros depois que o primeiro terminar de instalar.

### Tamanho do nome da página {#page-name-length}

Se AEM estiver em execução em uma implantação do gerenciador de persistência do MongoMK, [os nomes de página são limitados a 150 caracteres.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
Consulte a [Documentação do MongoDB](https://docs.mongodb.com/manual/reference/limits/) assim, você pode se familiarizar com as limitações e limites conhecidos do MongoDB.
