---
title: Adobe Experience Manager com MongoDB
description: Saiba mais sobre as tarefas e as considerações necessárias para uma implantação bem-sucedida do Adobe Experience Manager com MongoDB.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 0%

---

# Adobe Experience Manager com MongoDB{#aem-with-mongodb}

Este artigo tem como objetivo melhorar o conhecimento sobre tarefas e considerações necessárias para a implantação bem-sucedida do AEM (Adobe Experience Manager) com MongoDB.

Para obter mais informações sobre implantação, consulte o [Implantação e manutenção](/help/sites-deploying/deploy.md) seção da documentação.

## Quando usar MongoDB com AEM {#when-to-use-mongodb-with-aem}

O MongoDB é normalmente usado para oferecer suporte a implantações de autores de AEM, onde um dos seguintes critérios é atendido:

* Mais de 1000 utilizadores únicos por dia;
* Mais de 100 usuários simultâneos;
* Grandes volumes de edições de página;
* Implantações ou ativações grandes.

Os critérios acima são somente para as instâncias do autor e não para nenhuma instância de publicação que deve ser baseada em TarMK. O número de usuários se refere a usuários autenticados, pois as instâncias de autor não permitem acesso não autenticado.

Se os critérios não forem atendidos, uma implantação ativo/standby de TarMK será recomendada para tratar da disponibilidade. Geralmente, o MongoDB deve ser considerado em situações em que os requisitos de dimensionamento são maiores do que o que pode ser obtido com um único item de hardware.

>[!NOTE]
>
>Informações adicionais sobre o dimensionamento de instâncias de autor e a definição de usuários simultâneos podem ser encontradas na [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Implantação mínima do MongoDB para AEM {#minimal-mongodb-deployment-for-aem}

Abaixo está uma implantação mínima para o AEM no MongoDB. Para simplificar, a terminação SSL e os componentes do Proxy HTTP foram generalizados. Consiste em um único conjunto de réplicas MongoDB, com um primário e dois secundários.

![chlimage_1-4](assets/chlimage_1-4.png)

Uma implantação mínima requer três `mongod` instâncias configuradas como um conjunto de réplicas. Uma instância é eleita primária e as outras instâncias são secundárias, com a eleição gerenciada por `mongod`. Anexado a cada instância está um disco local. Para que o cluster possa suportar a carga, recomenda-se um throughput mínimo de 12 MB por segundo com mais de 3.000 operações de E/S por segundo (IOPS).

Os autores do AEM estão conectados ao `mongod` instâncias, com cada autor AEM se conectando aos três `mongod` instâncias. As gravações são enviadas para o principal e as leituras podem ser lidas de qualquer uma das instâncias. O tráfego é distribuído com base na carga por um Dispatcher para qualquer uma das instâncias de autor ativas do AEM. O armazenamento de dados do Oak é um `FileDataStore`, e o monitoramento do MongoDB é fornecido pelo MMS ou MongoDB Ops Manager, dependendo da localização da implantação. O nível do sistema operacional e o monitoramento de registros são fornecidos por soluções de terceiros, como Splunk ou Ganglia.

Nesta implantação, todos os componentes são necessários para uma implementação bem-sucedida. Qualquer componente ausente deixa a implementação não funcional.

### Sistemas operacionais {#operating-systems}

Para obter uma lista de sistemas operacionais compatíveis com o AEM 6, consulte a [Página Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### Ambientes {#environments}

Os ambientes virtualizados são suportados desde que haja uma boa comunicação entre as diferentes equipes técnicas que executam o projeto. Esse suporte inclui a equipe que está executando o AEM, a equipe que possui o sistema operacional e a equipe que gerencia a infraestrutura virtualizada.

Há requisitos específicos que abrangem a capacidade de E/S das instâncias do MongoDB que devem ser gerenciadas pela equipe que gerencia o ambiente virtualizado. Se o projeto usar uma implantação em nuvem, como o Amazon Web Services, as instâncias deverão ser provisionadas com capacidade e consistência de E/S suficientes para dar suporte às instâncias do MongoDB. Caso contrário, os processos do MongoDB e o repositório do Oak serão executados de forma não confiável e irregular.

Nos ambientes virtualizados, o MongoDB requer configurações específicas de E/S e VM para garantir que o mecanismo de armazenamento do MongoDB não seja prejudicado pelas políticas de alocação de recursos da VMWare. Uma implementação bem-sucedida garante que não haja barreiras entre as várias equipes, e todas estão inscritas para fornecer o desempenho necessário.

## Considerações sobre hardware {#hardware-considerations}

### Armazenamento {#storage}

Para alcançar a taxa de transferência de leitura e gravação para melhor desempenho sem a necessidade de dimensionamento horizontal prematuro, o MongoDB geralmente requer armazenamento de dados SSD ou armazenamento de dados com desempenho equivalente ao SSD.

### RAM {#ram}

As versões 2.6 e 3.0 do MongoDB que usam o mecanismo de armazenamento MMAP exigem que o conjunto de trabalho do banco de dados e seus índices se encaixem na RAM.

A RAM insuficiente resulta em uma redução significativa do desempenho. O tamanho do conjunto de trabalho e do banco de dados é altamente dependente do aplicativo. Embora algumas estimativas possam ser feitas, a maneira mais confiável de determinar a quantidade de RAM necessária é criar o aplicativo AEM e testá-lo.

Para auxiliar no processo de teste de carga, a seguinte proporção de conjunto de trabalho para o tamanho total do banco de dados pode ser presumida:

* 1:10 para armazenamento de dados SSD
* 1:3 para armazenamento em disco rígido

Essas taxas significam que para implantações de SSD são necessários 200 GB de RAM para um banco de dados de 2 TB.

Embora as mesmas limitações se apliquem ao mecanismo de armazenamento WiredTiger no MongoDB 3.0, a correlação entre o conjunto de trabalho, a RAM e as falhas de página não é tão forte. O WiredTiger não usa o mapeamento de memória da mesma forma que o mecanismo de armazenamento MMAP.

>[!NOTE]
>
>A Adobe recomenda o uso do mecanismo de armazenamento WiredTiger para implantações AEM 6.1 que usam MongoDB 3.0.

### Armazenamento de dados {#data-store}

Devido às limitações do conjunto de trabalho do MongoDB, é recomendável que o armazenamento de dados seja mantido independente do MongoDB. Na maioria dos ambientes, uma `FileDataStore` deve-se usar um NAS disponível para todas as instâncias AEM. Para situações em que o Amazon Web Services é usado, também há uma `S3 DataStore`. Se, por qualquer motivo, o armazenamento de dados for mantido no MongoDB, o tamanho do armazenamento de dados deverá ser adicionado ao tamanho total do banco de dados e os cálculos do conjunto de trabalho deverão ser ajustados adequadamente. Esse dimensionamento pode significar o provisionamento de mais RAM para manter o desempenho sem falhas de página.

## Monitoramento {#monitoring}

O acompanhamento é vital para uma implementação bem-sucedida do projeto. Com conhecimento suficiente, é possível executar o AEM no MongoDB sem monitoramento. No entanto, esse conhecimento normalmente é encontrado em engenheiros especializados para cada seção da implantação.

Esse conhecimento especializado geralmente envolve um engenheiro de P&amp;D que trabalha no Apache Oak Core e um especialista em MongoDB.

Sem monitoramento em todos os níveis, é necessário um conhecimento detalhado da base de código para diagnosticar problemas. Com o acompanhamento em vigor e orientações adequadas sobre as principais estatísticas, as equipes de execução podem reagir adequadamente às anomalias.

Embora seja possível usar ferramentas de linha de comando para obter um instantâneo rápido da operação de um cluster, fazer isso em tempo real em muitos hosts é quase impossível. As ferramentas de linha de comando raramente fornecem informações históricas além de alguns minutos e nunca permitem a correlação cruzada entre diferentes tipos de métricas. Um breve período de fundo lento `mongod` A sincronização requer um esforço manual significativo para correlacionar com os níveis de espera de I/O ou de gravação excessiva a um recurso de armazenamento compartilhado de uma máquina virtual aparentemente desconectada.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

O MongoDB Cloud Manager é um serviço gratuito oferecido pelo MongoDB que permite o monitoramento e o gerenciamento de instâncias do MongoDB. Ele fornece uma visualização do desempenho e da integridade do cluster MongoDB em tempo real. Ele gerencia instâncias na nuvem e hospedadas de forma privada, desde que a instância possa acessar o servidor de monitoramento do Cloud Manager.

Ele requer um agente instalado na instância do MongoDB que se conecta ao servidor de monitoramento. Há três níveis do agente:

* Um agente de automação que pode automatizar completamente tudo no servidor MongoDB,
* Um agente de monitoramento que pode monitorar o `mongod` instância,
* Um agente de backup que pode executar backups programados dos dados.

Embora o uso do Cloud Manager para automação de manutenção de um cluster MongoDB torne muitas das tarefas de rotina mais fáceis, ele não é necessário e nem o está usando para backup. No entanto, ao escolher o Cloud Manager para monitorar, o monitoramento é necessário.

Para obter mais informações sobre o MongoDB Cloud Manager, consulte o [Documentação do MongoDB](https://docs.cloud.mongodb.com/).

### Gerenciador de Operações do MongoDB {#mongodb-ops-manager}

O MongoDB Ops Manager é o mesmo software que o MongoDB Cloud Manager. Depois de registrado, o Ops Manager pode ser baixado e instalado localmente em um data center privado ou em qualquer outro laptop ou computador desktop. Ele usa um banco de dados MongoDB local para armazenar dados e se comunica da mesma forma que o Cloud Manager com os servidores gerenciados. Se você tiver políticas de segurança que proíbam um agente de monitoramento, o MongoDB Ops Manager deverá ser usado.

### Monitoramento do sistema operacional {#operating-system-monitoring}

É necessário o monitoramento em nível de sistema operacional para executar um cluster AEM MongoDB.

O Ganglia é um bom exemplo de um sistema desse tipo e fornece uma imagem sobre a variedade e os detalhes das informações necessárias, que vão além das métricas básicas de integridade, como CPU, média de carga e espaço livre em disco. Para diagnosticar problemas, são necessárias informações de nível inferior, como níveis de pool de entropia, Espera de E/S da CPU e soquetes no estado FIN_WAIT2.

### Agregação de Log {#log-aggregation}

Com um cluster de vários servidores, a agregação central de registros é um requisito para um sistema de produção. Softwares como o Splunk oferecem suporte à agregação de logs e permitem que as equipes analisem os padrões de comportamento do aplicativo sem precisar coletar manualmente os logs.

## Listas de verificação {#checklists}

Esta seção trata de várias etapas necessárias para garantir que suas implantações de AEM e MongoDB sejam configuradas corretamente antes de implementar seu projeto.

### Rede {#network}

1. Primeiro, verifique se todos os hosts têm uma entrada de DNS
1. Todos os hosts devem ser resolvidos por sua entrada de DNS de todos os outros hosts roteáveis
1. Todos os hosts MongoDB podem ser roteados de todos os outros hosts MongoDB no mesmo cluster
1. Os hosts MongoDB podem rotear pacotes para o MongoDB Cloud Manager e os outros servidores de monitoramento
1. Servidores AEM podem rotear pacotes para todos os servidores MongoDB
1. A latência de pacote entre qualquer servidor AEM e qualquer servidor MongoDB é menor que dois milissegundos, sem perda de pacote e com uma distribuição padrão de um milissegundo ou menos.
1. Verifique se não há mais de dois saltos entre um AEM e um servidor MongoDB
1. Não há mais do que dois saltos entre dois servidores MongoDB
1. Não há roteadores mais altos que o nível 3 de OSI entre quaisquer servidores núcleo (MongoDB ou AEM ou qualquer combinação).
1. Se o entroncamento VLAN ou qualquer forma de tunelamento de rede for usado, ele deverá estar em conformidade com as verificações de latência de pacote.

### Configuração do AEM {#aem-configuration}

#### Configuração do armazenamento de nós {#node-store-configuration}

As instâncias de AEM devem ser configuradas para usar AEM com MongoMK. A base da implementação do MongoMK no AEM é o Document Node Store.

Para obter mais informações sobre como configurar lojas de nós, consulte [Configuração de armazenamentos de nós e armazenamentos de dados no AEM](/help/sites-deploying/data-store-config.md).

Veja abaixo um exemplo da configuração do Document Node Store para uma implantação mínima do MongoDB:

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Em que:

* `mongodburi`
O AEM do servidor MongoDB deve se conectar ao. As conexões são feitas a todos os membros conhecidos do conjunto de réplicas padrão. Se o MongoDB Cloud Manager for usado, a segurança do servidor será ativada. Portanto, a cadeia de conexão deve conter um nome de usuário e senha adequados. As versões não empresariais do MongoDB são compatíveis apenas com autenticação de nome de usuário e senha. Para obter mais informações sobre a sintaxe da string de conexão, consulte o [documentação](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
O nome do banco de dados. O padrão para AEM é `aem-author`.

* `customBlobStore`
Se a implantação armazenar binários no banco de dados, eles farão parte do conjunto de trabalho. Por esse motivo, é aconselhável não armazenar binários no MongoDB, preferindo um armazenamento de dados alternativo como um `FileSystem` armazenamento de dados em um NAS.

* `cache`
O tamanho do cache em megabytes. Esse espaço é distribuído entre os vários caches usados no `DocumentNodeStore`. O padrão é 256 MB. No entanto, o desempenho de leitura do Oak se beneficia de um cache maior.

* `blobCacheSize`
Blobs usados com frequência podem ser armazenados em cache pelo AEM para evitar sua nova busca no armazenamento de dados. Isso tem mais impacto no desempenho, especialmente ao armazenar blobs no banco de dados do MongoDB. Todos os Data Stores baseados em sistema de arquivos se beneficiam do cache de disco no nível do sistema operacional.

#### Configuração do armazenamento de dados {#data-store-configuration}

O Armazenamento de dados é usado para armazenar arquivos de tamanho maior que um limite. Abaixo desse limite, os arquivos são armazenados como propriedades no Document Node Store. Se a variável `MongoBlobStore` for usada, uma coleção dedicada será criada no MongoDB para armazenar os blobs. Essa coleção contribui para o conjunto de trabalho da `mongod` e exige que `mongod` tem mais RAM para evitar problemas de desempenho. Por esse motivo, a configuração recomendada é evitar a `MongoBlobStore` para implantações de produção e uso `FileDataStore` respaldado por um NAS compartilhado entre todas as instâncias AEM. Como o cache em nível de sistema operacional é eficiente no gerenciamento de arquivos, o tamanho mínimo de um arquivo no disco deve ser definido próximo ao tamanho do bloco do disco. Isso garante que o sistema de arquivos seja usado de maneira eficiente, e muitos documentos pequenos não contribuem excessivamente para o conjunto de trabalho do `mongod` instância.

Esta é uma configuração típica do armazenamento de dados para uma implantação mínima do AEM com MongoDB:

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
Tamanho em bytes. Binários menores ou iguais a esse tamanho são armazenados com o Document Node Store. Em vez de armazenar a ID do blob, o conteúdo do binário é armazenado. Com binários maiores que esse tamanho, a ID do binário é armazenada como uma propriedade do Documento na coleção de nós. E, o corpo do binário é armazenado no `FileDataStore` no disco. 4096 bytes é um tamanho típico de bloco do sistema de arquivos.

* `path`
O caminho para a raiz do armazenamento de dados. Para uma implantação do MongoMK, esse caminho deve ser um sistema de arquivos compartilhado disponível para todas as instâncias do AEM. Normalmente, um servidor NAS (Network Attached Storage, armazenamento conectado à rede) é usado. Para implantações em nuvem como o Amazon Web Services, a variável `S3DataFileStore` O também está disponível.

* `cacheSizeInMB`
O tamanho total do cache binário em Megabytes. É usado para armazenar binários em cache menos do que o `maxCacheBinarySize` configuração.

* `maxCachedBinarySize`
O tamanho máximo em bytes de um binário armazenado em cache no cache binário. Se um Armazenamento de dados baseado em sistema de arquivos for usado, não é recomendável usar valores altos para o cache do Armazenamento de dados, pois os binários já estão armazenados em cache pelo sistema operacional.

#### Desabilitação da Dica de Consulta {#disabling-the-query-hint}

É recomendável desativar a dica de consulta enviada com todas as consultas adicionando a propriedade `-Doak.mongo.disableIndexHint=true` quando você inicia o AEM. Isso garante que o MongoDB calcule no índice mais apropriado para usar com base em estatísticas internas.

Se a dica de consulta não estiver desativada, qualquer ajuste de desempenho dos índices não afetará o desempenho do AEM.

#### Ativar cache persistente para MongoMK {#enable-persistent-cache-for-mongomk}

Recomenda-se que uma configuração de cache persistente seja ativada para implantações do MongoDB, a fim de maximizar a velocidade para ambientes com alto desempenho de leitura de E/S. Para obter mais detalhes, consulte [Documentação do Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Otimizações do sistema operacional MongoDB {#mongodb-operating-system-optimizations}

### Suporte a sistema operacional {#operating-system-support}

O MongoDB 2.6 usa um mecanismo de armazenamento de memória mapeada que é sensível a alguns aspectos do gerenciamento de nível do sistema operacional entre a RAM e o Disco. O desempenho de consulta e leitura da instância do MongoDB depende de evitar ou eliminar operações lentas de E/S, geralmente chamadas de falhas de página. Esses problemas são falhas de página que se aplicam à variável `mongod` em particular. Não confunda com falhas de página no nível do sistema operacional.

Para uma operação rápida, o banco de dados MongoDB deve acessar apenas os dados que já estão na RAM. Os dados que ele deve acessar são compostos de índices e dados. Essa coleção de índices e dados é chamada de conjunto de trabalho. Quando o conjunto de trabalho é maior que a RAM disponível, o MongoDB tem que paginar esses dados no disco, incorrendo em um custo de E/S, removendo outros dados já na memória. Se a remoção fizer com que os dados sejam recarregados do disco, as falhas de página dominarão e o desempenho será prejudicado. Quando o conjunto de trabalho é dinâmico e variável, ocorrem mais falhas de página para dar suporte às operações.

O MongoDB é executado em vários sistemas operacionais, incluindo uma grande variedade de opções de Linux®, Windows e macOS. Consulte [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) para obter detalhes adicionais. Dependendo da sua escolha de sistema operacional, o MongoDB tem diferentes recomendações de nível de sistema operacional. Há documentos em [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) e resumido aqui para conveniência.

#### Linux® {#linux}

* Desativar páginas de abraços transparentes e desfragmentar. Consulte [Configurações de páginas enormes transparentes](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) para obter mais informações.
* [Ajustar as configurações de leitura antecipada](https://docs.mongodb.com/manual/administration/production-notes/#readahead) nos dispositivos que armazenam os arquivos do banco de dados para que se ajustem ao caso de uso.

   * Para o mecanismo de armazenamento MMAPv1, se o seu conjunto de trabalho for maior que a RAM disponível e o padrão de acesso a documentos for aleatório, considere diminuir a leitura antecipada para 32 ou 16. Avalie configurações diferentes para que você possa encontrar um valor ideal que maximize a memória residente e reduza o número de falhas da página.
   * Para o mecanismo de armazenamento WiredTiger, defina readahead como 0, independentemente do tipo de mídia de armazenamento (rotação, SSD e assim por diante). Em geral, use a configuração recomendada de leitura antecipada, a menos que os testes mostrem um benefício mensurável, repetível e confiável em um valor de leitura antecipada mais alto. [Suporte profissional MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) O pode fornecer conselhos e orientação sobre configurações de leitura antecipada diferentes de zero.

* Desative a ferramenta ajustada se estiver executando o RHEL 7/CentOS 7 em um ambiente virtual.
* Quando o RHEL 7/CentOS 7 é executado em um ambiente virtual, a ferramenta ajustada chama automaticamente um perfil de desempenho derivado da taxa de transferência de desempenho, que define automaticamente as configurações de leitura antecipada para 4 MB. Essa configuração pode afetar negativamente o desempenho.
* Use os programadores de disco noop ou deadline para unidades SSD.
* Use o programador de disco noop para unidades virtualizadas em VMs convidadas.
* Desabilitar NUMA ou conjunto `vm.zone_reclaim_mode` para 0 e execute [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) instâncias com intercalação de nó. Consulte: [Hardware MongoDB e NUMA](https://docs.mongodb.com/manual/administration/production-notes/#readahead) para obter mais informações.

* Ajuste os valores de ulimit em seu hardware para que eles se encaixem no seu caso de uso. Se vários [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) ou [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) ocorrências estiverem sendo executadas com o mesmo usuário, dimensione os valores de ulimit de acordo. Consulte: [Configurações de limite do UNIX®](https://docs.mongodb.com/manual/reference/ulimit/) para obter mais informações.

* Use noatime para o [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) ponto de montagem.
* Configure manipuladores de arquivos suficientes (fs.file-max), limite de pid do kernel (kernel.pid_max) e máximo de threads por processo (kernel.threads-max) para sua implantação. Para sistemas grandes, os seguintes valores fornecem um bom ponto de partida:

   * fs.file-max de 98.000,
   * valor kernel.pid_max de 64000,
   * andkernel.threads-valor máximo de 64000

* Verifique se o sistema tem o espaço de troca configurado. Consulte a documentação do seu sistema operacional para obter detalhes sobre o dimensionamento apropriado.
* Verifique se o keepalive de TCP padrão do sistema está definido corretamente. Um valor de 300 geralmente oferece melhor desempenho para conjuntos de réplicas e clusters fragmentados. Consulte: [O tempo de manutenção de atividade de TCP afeta as implantações do MongoDB?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) nas Perguntas frequentes para obter mais informações.

#### Windows {#windows}

* Considere desabilitar atualizações de &quot;hora do último acesso&quot; do NTFS. Essa configuração é análoga à desativação de atime em sistemas Unix.

### WiredTiger {#wiredtiger}

A partir do MongoDB 3.2, o mecanismo de armazenamento padrão para o MongoDB é o mecanismo de armazenamento WiredTiger. Esse mecanismo fornece alguns recursos robustos e escalonáveis, tornando-o muito mais adequado para cargas de trabalho gerais gerais de banco de dados. As seções a seguir descrevem esses recursos.

#### Simultaneidade no Nível do Documento {#document-level-concurrency}

O WiredTiger usa controle de simultaneidade no nível do documento para operações de gravação. Como resultado, vários clientes podem modificar diferentes documentos de uma coleção ao mesmo tempo.

Para a maioria das operações de leitura e gravação, o WiredTiger usa um controle de simultaneidade otimista. O WiredTiger usa apenas bloqueios de intenção nos níveis global, de banco de dados e de coleção. Quando o mecanismo de armazenamento detecta conflitos entre duas operações, ocorre um conflito de gravação, fazendo com que o MongoDB repita de forma transparente essa operação. Algumas operações globais, normalmente operações de curta duração envolvendo vários bancos de dados, ainda exigem um bloqueio global &quot;em toda a instância&quot;.

Algumas outras operações, como descartar uma coleção, ainda exigem um bloqueio de banco de dados exclusivo.

#### Instantâneos e pontos de verificação {#snapshots-and-checkpoints}

WiredTiger usa Controle de Simultaneidade MultiVersion (MVCC). No início de uma operação, o WiredTiger fornece um instantâneo point-in-time dos dados para a transação. Um instantâneo apresenta uma exibição consistente dos dados na memória.

Ao gravar em disco, o WiredTiger grava todos os dados em um instantâneo no disco de maneira consistente em todos os arquivos de dados. O agora- [durável](https://docs.mongodb.com/manual/reference/glossary/#term-durable) Os dados atuam como um ponto de verificação nos arquivos de dados. O ponto de verificação garante a consistência dos arquivos de dados até o último ponto de verificação, inclusive. Ou seja, os pontos de verificação podem agir como pontos de recuperação.

O MongoDB configura o WiredTiger para criar pontos de verificação (ou seja, gravar os dados do instantâneo no disco) em intervalos de 60 segundos ou 2 GB de dados de diário.

Durante a gravação de um novo ponto de verificação, o ponto de verificação anterior ainda é válido. Dessa forma, mesmo que o MongoDB termine ou encontre um erro ao gravar um novo ponto de verificação, após a reinicialização, o MongoDB pode se recuperar do último ponto de verificação válido.

O novo checkpoint se torna acessível e permanente quando a tabela de metadados do WiredTiger é atualizada com precisão para fazer referência ao novo checkpoint. Quando o novo ponto de verificação estiver acessível, o WiredTiger liberará páginas dos pontos de verificação antigos.

Usando o WiredTiger, mesmo sem [registro em log](https://docs.mongodb.com/manual/reference/glossary/#term-durable), o MongoDB pode se recuperar do último ponto de verificação; no entanto, para recuperar alterações feitas após o último ponto de verificação, execute com [registro em log](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Diário {#journal}

O WiredTiger usa uma combinação de logon de transação de gravação antecipada com [pontos de verificação](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) para garantir a durabilidade dos dados.

O journal do WiredTiger persiste todas as modificações de dados entre os pontos de verificação. Se o MongoDB existir entre os pontos de verificação, ele usará o journal para repetir todos os dados modificados desde o último ponto de verificação. Para obter informações sobre a frequência com que o MongoDB grava os dados de registro em disco, consulte [Processo de registro em log](https://docs.mongodb.com/manual/core/journaling/#journal-process).

O diário WiredTiger é compactado usando o [snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process) biblioteca de compactação. Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use o [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) configuração.

Consulte [Registro em log com o WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>O tamanho mínimo do registro de log para WiredTiger é de 128 bytes. Se um registro de log tiver 128 bytes ou menos, o WiredTiger não compactará esse registro.
>
>Você pode desativar o registro em log configurando [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) como false, o que pode reduzir a sobrecarga de manutenção do journal.
>
>Para [independente](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) instâncias, não usar o journal significa que você perde algumas modificações de dados quando o MongoDB sair inesperadamente entre pontos de verificação. Para membros de [conjuntos de réplicas](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), o processo de replicação pode fornecer garantias suficientes de durabilidade.

#### Compactação {#compression}

Com o WiredTiger, o MongoDB oferece suporte à compactação para todas as coleções e índices. A compactação minimiza o uso do armazenamento à custa da CPU adicional.

Por padrão, o WiredTiger usa compactação de bloco com o [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) biblioteca de compactação para todas as coleções e [compactação de prefixo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) para todos os índices.

Para coleções, compactação de bloco com [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) O também está disponível. Para especificar um algoritmo de compactação alternativo ou nenhuma compactação, use o [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) configuração.

Para índices, para desativar [compactação de prefixo](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), use o [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) configuração.

As configurações de compactação também podem ser definidas com base em coleção e índice durante a criação da coleção e do índice. Consulte [Especificar Opções de Mecanismo de Armazenamento](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) e [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) opção.

Para a maioria das cargas de trabalho, as configurações de compactação padrão equilibram a eficiência do armazenamento e os requisitos de processamento.

O journal WiredTiger também é compactado por padrão. Para obter informações sobre compactação de diário, consulte [Diário](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Uso de memória {#memory-use}

Com o WiredTiger, o MongoDB usa o cache interno do WiredTiger e o cache do sistema de arquivos.

A partir da versão 3.4, o cache interno do WiredTiger usa, por padrão, o maior dos seguintes:

* 50% de RAM menos 1 GB ou
* 256 MB

Por padrão, o WiredTiger usa a compactação de bloco Snappy para todas as coleções e a compactação de prefixo para todos os índices. Os padrões de compactação são configuráveis em nível global e também podem ser definidos com base em coleção e índice durante a criação da coleção e do índice.

Diferentes representações são usadas para dados no cache interno do WiredTiger em comparação ao formato no disco:

* Os dados no cache do sistema de arquivos são os mesmos do formato em disco, incluindo os benefícios de qualquer compactação para arquivos de dados. O cache do sistema de arquivos é usado pelo sistema operacional para reduzir a E/S de disco.

Os índices carregados no cache interno do WiredTiger têm uma representação de dados diferente do formato no disco, mas ainda podem aproveitar a compactação do prefixo do índice para reduzir o uso da RAM.

A compactação do prefixo de índice desduplica prefixos comuns de campos indexados.

Os dados de coleta no cache interno do WiredTiger são descompactados e usam uma representação diferente do formato no disco. A compactação de blocos pode proporcionar uma economia significativa no armazenamento em disco, mas os dados devem ser descompactados para serem manipulados pelo servidor.

Através do cache do sistema de arquivos, o MongoDB usa automaticamente toda a memória livre que não é usada pelo cache WiredTiger ou por outros processos.

Para ajustar o tamanho do cache interno do WiredTiger, consulte [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) e [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Evite aumentar o tamanho do cache interno do WiredTiger acima do valor padrão.

### NUMA {#numa}

NUMA (Non-Uniform Memory Access — Acesso não-uniforme à memória) permite que um kernel gerencie como a memória é mapeada para os núcleos do processador. Embora esse processo tente tornar o acesso à memória mais rápido para os núcleos, garantindo que eles possam acessar os dados necessários, o NUMA interfere no MMAP, introduzindo latência adicional, pois as leituras não podem ser previstas. Como resultado, o NUMA deve ser desativado para a variável `mongod` em todos os sistemas operacionais habilitados.

Em essência, em uma arquitetura NUMA, a memória é conectada às CPUs e as CPUs são conectadas a um barramento. Em uma arquitetura SMP ou UMA, a memória é conectada ao barramento e compartilhada pelas CPUs. Quando um thread aloca memória em uma CPU NUMA, ele aloca de acordo com uma política. O default é alocar memória anexada à CPU local do thread, a menos que não haja memória livre. Nesse momento, ela usa memória de uma CPU livre a um custo mais alto. Depois de alocada, a memória não se move entre as CPUs. A alocação é executada por uma política herdada do thread pai, que é o thread que iniciou o processo.

Em muitos bancos de dados que veem o computador como uma arquitetura de memória uniforme de vários núcleos, esse cenário faz com que a CPU inicial fique cheia primeiro e a CPU secundária fique cheia mais tarde. É especialmente verdadeiro se um thread central for responsável pela alocação de buffers de memória. A solução é alterar a política NUMA do thread principal usado para iniciar o `mongod` execute o seguinte comando:

```shell
numactl --interleaved=all <mongod> -f config
```

Essa política aloca memória de forma alternada em todos os nós da CPU, garantindo uma distribuição uniforme em todos os nós. Ele não gera o acesso de mais alto desempenho à memória, como em sistemas com vários hardwares de CPU. Cerca de metade das operações de memória é mais lenta e ultrapassa o barramento, mas `mongod` não foi escrito para direcionar NUMA de maneira ideal, portanto, é um compromisso razoável.

### Problemas NUMA {#numa-issues}

Se a variável `mongod` o processo é iniciado em um local diferente do `/etc/init.d` pasta, é provável que ele não tenha iniciado com a política NUMA correta. Dependendo da política padrão, podem ocorrer problemas. O motivo é porque os vários instaladores do Gerenciador de pacotes do Linux® para MongoDB também instalam um serviço com arquivos de configuração no `/etc/init.d` que executam a etapa descrita acima. Se você instalar e executar o MongoDB diretamente de um arquivo ( `.tar.gz`), você deve executar manualmente o mongod sob o `numactl` processo.

>[!NOTE]
>
>Para obter mais informações sobre as políticas NUMA disponíveis, consulte o [documentação numactl](https://linux.die.net/man/8/numactl).

O processo MongoDB se comporta de forma diferente em diferentes políticas de alocação:

```

```

* `-membind=<nodes>`
Alocar somente nos nós listados. Mongod não aloca memória nos nós listados e pode não usar toda a memória disponível.

* `-cpunodebind=<nodes>`
Executar somente nos nós. Mongod só é executado nos nós especificados e só usa a memória disponível nesses nós.

* `-physcpubind=<nodes>`
Executar somente nas CPUs (núcleos) listadas. Mongod só roda nas CPUs listadas e só usa a memória disponível nessas CPUs.

* `--localalloc`
Sempre alocar memória no nó atual, mas usar todos os nós nos quais o thread é executado. Se um thread executar a alocação, apenas a memória disponível para essa CPU será usada.

* `--preferred=<node>`
Prefere alocação a um nó, mas retorna a outros se o nó preferencial estiver cheio. A notação relativa para definir um nó pode ser usada. Além disso, as threads são executadas em todos os nós.

Algumas das políticas podem resultar em menos que toda a RAM disponível fornecida ao `mongod` processo. Ao contrário do MySQL, o MongoDB evita ativamente a paginação em nível de sistema operacional e, portanto, a `mongod` o processo pode obter menos memória que parece disponível.

#### Trocando {#swapping}

Devido à natureza intensiva de memória dos bancos de dados, a troca de nível de sistema operacional deve ser desativada. O processo MongoDB evita a troca por design.

#### Sistemas de arquivos remotos {#remote-filesystems}

Os sistemas de arquivos remotos, como o NFS, não são recomendados para arquivos de dados internos do MongoDB (os arquivos de banco de dados de processo mongod) , porque eles apresentam muita latência. Não confunda com o sistema de arquivos compartilhados necessário para o armazenamento do Oak Blob&#39;s (FileDataStore), onde o NFS é recomendado.

#### Leia adiante {#read-ahead}

Ajuste a Leitura antecipadamente para que, quando uma página for paginada usando uma leitura aleatória, os blocos desnecessários não sejam lidos do disco. Esses resultados significam um consumo desnecessário de largura de banda de E/S.

### Requisitos do Linux® {#linux-requirements}

#### Versões mínimas do kernel {#minimum-kernel-versions}

* **2.6.23** para `ext4` sistemas de arquivos

* **2.6.25** para `xfs` sistemas de arquivos

#### Configurações Recomendadas para Discos de Banco de Dados {#recommended-settings-for-database-disks}

**Desativar horário**

Recomenda-se que `atime` está desativado para os discos que contêm os bancos de dados.

**Definir o programador de disco NOOP**

Faça o seguinte:

Primeiro, verifique o programador de I/O que está configurado executando o seguinte comando:

```shell
cat /sys/block/sdg/queue/scheduler
```

Se a resposta for `noop`Não há nada mais que você deva fazer.

Se NOOP não for o programador de E/S configurado, você poderá alterá-lo executando:

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajustar o valor de leitura antecipada**

É recomendável usar um valor de 32 para os discos em que os bancos de dados MongoDB são executados. Esse valor é de 16 KB. Você pode defini-lo executando o seguinte:

```shell
sudo blockdev --setra <value> <device>
```

#### Ativar NTP {#enable-ntp}

Verifique se o NTP está instalado e em execução na máquina que está hospedando os bancos de dados do MongoDB. Por exemplo, você pode instalá-lo usando o Gerenciador de pacotes yum em uma máquina CentOS:

```shell
sudo yum install ntp
```

Depois que o daemon NTP tiver sido instalado e iniciado com êxito, você poderá verificar o deslocamento de tempo do arquivo de descompasso do seu servidor.

#### Desativar páginas grandes transparentes {#disable-transparent-huge-pages}

O Red Hat® Linux® usa um algoritmo de gerenciamento de memória chamado THP (Transparent Huge Pages). É recomendável desativá-la se estiver usando o sistema operacional para cargas de trabalho de banco de dados.

Você pode desativá-lo seguindo o procedimento abaixo:

1. Abra o `/etc/grub.conf` no editor de texto de sua escolha.
1. Adicione a seguinte linha ao arquivo grub.conf:

   ```xml
   transparent_hugepage=never
   ```

1. Por fim, verifique se a configuração foi aplicada executando:

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Se o THP estiver desativado, a saída do comando acima deve ser:

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Para obter mais informações sobre páginas grandes transparentes, consulte este [artigo](https://access.redhat.com/solutions/46111).

#### Desabilitar NUMA {#disable-numa}

Na maioria das instalações em que o NUMA está ativado, o daemon MongoDB o desativa automaticamente se for executado como um serviço do `/etc/init.d` pasta.

Se esse não for o caso, você poderá desativar NUMA em um nível por processo. Para desativá-lo, execute os seguintes comandos:

```shell
numactl --interleave=all <path_to_process>
```

Onde `<path_to_process>` é o caminho para o processo de mongod.

Em seguida, desative a recuperação de região executando:

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Ajustar as configurações de limite para o processo mongod {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® permite o controle configurável sobre a alocação de recursos por meio do `ulimit` comando. Essa configuração pode ser feita com base em um usuário ou por processo.

É recomendável configurar o ulimit para o processo mongod de acordo com o [Configurações de ulimit recomendadas pelo MongoDB](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Teste de desempenho de E/S do MongoDB {#test-mongodb-i-o-performance}

O MongoDB fornece uma ferramenta chamada `mongoperf` projetado para testar o desempenho de E/S. É recomendável usá-lo para testar o desempenho de todas as instâncias do MongoDB que compõem sua infraestrutura.

Para obter informações sobre como usar `mongoperf`, exiba a [Documentação do MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>A variável `mongoperf` é um indicador de desempenho do MongoDB na plataforma em que ele é executado. Por conseguinte, os resultados não devem ser tratados como definitivos para o desempenho de um sistema de produção.
>
>Para obter resultados de desempenho mais precisos, é possível executar testes complementares com o `fio` ferramenta Linux®.

**Teste o desempenho de leitura nas máquinas virtuais que compõem sua implantação**

Após instalar a ferramenta, alterne para o diretório do banco de dados MongoDB para executar os testes. Em seguida, inicie o primeiro teste executando `mongoperf`com esta configuração:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

A saída desejada deve atingir até dois gigabytes por segundo (2 GB/s) e 500.000 IOPS executados em 32 threads para todas as instâncias do MongoDB.

Execute um segundo teste, desta vez usando arquivos mapeados de memória, configurando o `mmf:true` parâmetro:

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

A saída do segundo teste deve ser consideravelmente maior do que o primeiro, indicando o desempenho da transferência de memória.

>[!NOTE]
>
>Ao executar os testes, verifique as estatísticas de uso de E/S das máquinas virtuais em questão no sistema de monitoramento do sistema operacional. Se eles indicarem valores inferiores a 100% para leituras de E/S, pode haver um problema com sua máquina virtual.

**Testar o desempenho de gravação da instância MongoDB primária**

Em seguida, verifique o desempenho de gravação de E/S da instância primária do MongoDB executando o `mongoperf` no diretório do banco de dados MongoDB com as mesmas configurações:

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

A saída desejada deve ser de 12 megabytes por segundo e atingir cerca de 3000 IOPS, com pouca variação entre o número de threads.

## Etapas para ambientes virtualizados {#steps-for-virtualised-environments}

### VMWare {#vmware}

Se você estiver usando o WMWare ESX para gerenciar e implantar seus ambientes virtualizados, certifique-se de executar as seguintes configurações no console ESX para acomodar a operação MongoDB:

1. Desativar balão de memória
1. Pré-alocar e reservar memória para as máquinas virtuais que hospedam os bancos de dados do MongoDB
1. Use o Storage I/O Control para alocar I/O suficiente para o `mongod` processo.
1. Garantir os recursos de CPU das máquinas que hospedam o MongoDB definindo [Reserva de CPU](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)

1. Considere usar drivers ParaVirtual I/O. Consulte [artigo da base de conhecimento](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Para obter a documentação sobre como configurar o MongoDB com Amazon Web Services, verifique a [Configurar a integração do AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) artigo no site do MongoDB.

## Proteção do MongoDB antes da implantação {#securing-mongodb-before-deployment}

Ver esta publicação em [implantação segura do MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) para obter dicas sobre como proteger a configuração dos bancos de dados antes da implantação.

## Dispatcher {#dispatcher}

### Escolha do Sistema Operacional para o Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Para atender corretamente à implantação do MongoDB, o sistema operacional que hospeda o Dispatcher deve estar em execução **Apache httpd** **versão 2.4 ou superior.**

Além disso, verifique se todas as bibliotecas usadas na sua build estão atualizadas para minimizar as implicações de segurança.

### Configuração do Dispatcher {#dispatcher-configuration}

Uma configuração típica do Dispatcher atende entre dez a 20 vezes mais a taxa de transferência de solicitação de uma única instância do AEM.

Como o Dispatcher não tem estado, ele pode ser dimensionado horizontalmente com facilidade. Em algumas implantações, os autores devem ser impedidos de acessar determinados recursos. É recomendável usar um Dispatcher com as instâncias do autor.

A execução do AEM sem um Dispatcher requer que a terminação SSL e o balanceamento de carga sejam executados por outro aplicativo. Isso é necessário porque as sessões devem ter afinidade com a instância do AEM em que são criadas, um conceito conhecido como conexões aderentes. O motivo é garantir que as atualizações do conteúdo exibam latência mínima.

Verifique a [Documentação do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) para obter mais informações sobre como configurá-lo.

### Configuração adicional {#additional-configuration}

#### Conexões adesivas {#sticky-connections}

As conexões adesivas garantem que páginas personalizadas e dados de sessão de um usuário sejam todos compostos na mesma instância do AEM. Esses dados são armazenados na instância, de modo que as solicitações subsequentes do mesmo usuário retornam à mesma instância.

Recomenda-se que as conexões aderentes sejam ativadas para todas as camadas internas que roteam solicitações para as instâncias de AEM, incentivando as solicitações subsequentes a alcançar a mesma instância de AEM. Isso ajuda a minimizar a latência que seria percebida quando o conteúdo é atualizado entre as instâncias.

#### Expira por muito tempo {#long-expires}

Por padrão, o conteúdo enviado de um Dispatcher do AEM tem cabeçalhos Last-Modified e Etag, sem nenhuma indicação da expiração do conteúdo. Esse fluxo garante que a interface do usuário sempre obtenha a versão mais recente do recurso. Também significa que o navegador executa uma operação GET para ver se o recurso foi alterado. Como resultado, pode resultar em várias solicitações às quais a resposta HTTP é 304 (Não modificado), dependendo do carregamento da página. Para recursos que não expiram, definir um cabeçalho Expira e remover os cabeçalhos Última modificação e ETag fazem com que o conteúdo seja armazenado em cache. Além disso, não é feita mais nenhuma solicitação de atualização até que a data no cabeçalho Expira seja atendida.

No entanto, usar esse método significa que não há uma maneira razoável de fazer com que o recurso expire no navegador antes que o cabeçalho Expire expire. Para mitigar esse fluxo de trabalho, o HtmlClientLibraryManager pode ser configurado para usar URLs imutáveis para bibliotecas de clientes.

É garantido que esses URLs não serão alterados. Quando o corpo do recurso contido no URL é alterado, as alterações são refletidas no URL, garantindo que o navegador solicite a versão correta do recurso.

A configuração padrão adiciona um seletor ao HtmlClientLibraryManager. Por ser um seletor, o recurso é armazenado em cache no Dispatcher com o seletor intacto. Além disso, esse seletor pode ser usado para garantir o comportamento de expiração correto. O seletor padrão segue o `lc-.*?-lc` padrão. As seguintes diretivas de configuração do Apache httpd garantem que todas as solicitações correspondentes a esse padrão sejam atendidas com um tempo de expiração adequado.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sem sniff {#no-sniff}

Quando o conteúdo é enviado sem nenhum tipo de conteúdo, muitos navegadores tentam adivinhar o tipo de conteúdo lendo os primeiros bytes do conteúdo. Esse método é chamado de &quot;sniffing&quot;. O sniffing abre uma vulnerabilidade de segurança, pois os usuários que podem gravar no repositório podem carregar conteúdo mal-intencionado sem nenhum tipo de conteúdo.

Por esta razão, é aconselhável adicionar um `no-sniff` cabeçalho para recursos fornecidos pelo Dispatcher. No entanto, o Dispatcher não armazena cabeçalhos em cache. Dessa forma, significa que qualquer conteúdo veiculado a partir do sistema de arquivos local tem seu tipo de conteúdo determinado por sua extensão, em vez de usar o cabeçalho do tipo de conteúdo original a partir do servidor AEM de origem.

Nenhum sniff pode ser ativado com segurança se o aplicativo da web é conhecido por nunca servir recursos em cache sem um tipo de arquivo.

Você pode ativar o No Sniff inclusive:

```xml
Header set X-Content-Type-Options "nosniff"
```

Ele também pode ser ativado seletivamente:

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Política de segurança de conteúdo {#content-security-policy}

As configurações padrão do Dispatcher permitem uma Política de segurança de conteúdo aberta, também conhecida como CSP. Essas configurações permitem que uma página carregue recursos de todos os domínios sujeitos às políticas padrão da sandbox do navegador.

É desejável restringir de onde os recursos podem ser carregados para evitar o carregamento de código no mecanismo JavaScript de servidores externos não confiáveis ou não verificados.

A CSP permite o ajuste fino das políticas. No entanto, em um aplicativo complexo, os cabeçalhos de CSP devem ser desenvolvidos com cuidado, pois políticas muito restritivas podem quebrar partes da interface do usuário.

>[!NOTE]
>
>Para obter mais informações sobre como isso funciona, consulte [Página OWASP sobre Política de segurança de conteúdo](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Dimensionamento {#sizing}

Para obter mais informações sobre dimensionamento, consulte a [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md).

### Otimização do desempenho do MongoDB {#mongodb-performance-optimization}

Para obter informações genéricas sobre o desempenho do MongoDB, consulte [Análise de desempenho do MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limitações conhecidas {#known-limitations}

### Instalações Simultâneas {#concurrent-installations}

Embora o MongoMK suporte o uso simultâneo de várias instâncias de AEM com um único banco de dados, as instalações simultâneas não são.

Para contornar esse problema, certifique-se de executar a instalação com um único membro primeiro e adicionar os outros depois que o primeiro terminar de instalar.

### Comprimento do nome da página {#page-name-length}

Se o AEM estiver sendo executado em uma implantação do gerenciador de persistência MongoMK, [Os nomes de página são limitados a 150 caracteres.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>Consulte a [Documentação do MongoDB](https://docs.mongodb.com/manual/reference/limits/) para que você possa se familiarizar com as limitações e limites conhecidos do MongoDB.
