---
title: Casos de uso da indexação Oak-run.jar
seo-title: Casos de uso da indexação Oak-run.jar
description: Saiba mais sobre os vários casos de usuário para executar a indexação com a ferramenta Oak-run.
seo-description: Saiba mais sobre os vários casos de usuário para executar a indexação com a ferramenta Oak-run.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 0%

---


# Casos de uso da indexação Oak-run.jar{#oak-run-jar-indexing-use-cases}

Oak-run suporta a indexação de casos de uso na linha de comando sem precisar orquestrar a execução desses casos de uso por meio AEM console JMX.

Os benefícios abrangentes de usar a abordagem de comando de índice oak-run.jar para gerenciar índices Oak são:

1. O comando de índice Oak-run fornece um novo conjunto de ferramentas de indexação para AEM 6.4.
1. A execução de carvalho diminui o tempo de reindexação, o que reduz o tempo de reindexação em repositórios maiores.
1. A execução de carvalho reduz o consumo de recursos durante a reindexação em AEM, resultando em um desempenho geral do sistema melhor.
1. A execução em carvalho oferece reindexação fora de banda, compatível com situações em que a produção deve estar disponível e não pode tolerar manutenção ou tempo de inatividade necessários para reindexar.

As seções abaixo forneceriam comandos de amostra. o comando oak-run index suporta todas as configurações de NodeStore e BlobStore. Os exemplos fornecidos abaixo são sobre as configurações que têm FileDataStore e SegmentNodeStore.

## Caso de uso 1 - Verificação de consistência de índice {#usercase1indexconsistencycheck}

Este é um caso de uso relacionado à corrupção de índice. Em alguns casos, não foi possível determinar quais índices estão corrompidos. Portanto, a Adobe fornece ferramentas que:

1. Realiza verificações de consistência de índice em todos os índices e fornece um relatório sobre quais índices são válidos e quais não são válidos;
1. As ferramentas podem ser utilizadas mesmo que AEM não seja acessível;
1. É fácil de usar.

A verificação de índices corrompidos pode ser realizada por meio da operação `--index-consistency-check`:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Isso gerará um relatório em `indexing-result/index-consistency-check-report.txt`. Veja abaixo um exemplo de relatório:

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Benefícios {#uc1benefits}

Essa ferramenta agora pode ser usada pelo Suporte e pelo Administrador do sistema para determinar rapidamente quais índices estão corrompidos e, em seguida, reindexá-los.

## Caso de uso 2 - Estatísticas de índice {#usecase2indexstatistics}

Para diagnosticar alguns dos casos em torno do Adobe de desempenho do query geralmente exigem uma definição de índice existente, as estatísticas relacionadas ao índice da configuração do cliente. Até agora, essa informação foi espalhada por vários recursos. Para facilitar a solução de problemas, o Adobe criou ferramentas que:

1. Despeje toda a definição de índice presente no sistema em um único arquivo JSON;

1. Eliminar estatísticas importantes dos índices existentes;

1. Despejar conteúdo de índice para análise offline;

1. Será utilizável mesmo se AEM não estiver acessível

As operações acima agora podem ser feitas por meio dos seguintes comandos de índice de operação:

* `--index-info` - Recolha e despeja várias estatísticas relacionadas com os índices

* `--index-definitions` - Coleta e despeja definições de índice

* `--index-dump` - Conteúdo do índice de despejos

Veja abaixo um exemplo de como os comandos funcionam na prática:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Os relatórios seriam gerados em `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Além disso, os mesmos detalhes são fornecidos pelo Console da Web e fazem parte do zip de despejo de configuração. Eles podem ser acessados no seguinte local:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Benefícios {#uc2benefits}

Essa ferramenta permite a coleta rápida de todos os detalhes necessários relacionados a problemas de indexação ou query e reduz o tempo gasto na extração dessas informações.

## Caso de uso 3 - reindexação {#usecase3reindexing}

Dependendo dos [cenários](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), em alguns casos, é necessário reindexar. Atualmente, a reindexação é feita configurando o sinalizador `reindex` como `true` no nó de definição de índice por meio do CRXDE ou da interface de usuário do Gerenciador de índice. Depois que o sinalizador é definido, a reindexação é feita de forma assíncrona.

Alguns pontos para observar sobre a reindexação:

* A reindexação é muito mais lenta nas configurações `DocumentNodeStore` em comparação com as configurações `SegmentNodeStore` em que todo o conteúdo é local;

* Com o design atual, enquanto a reindexação acontece, o indexador assíncrono é bloqueado e todos os outros índices assíncronos tornam-se obsoletos e não obtêm atualizações durante a indexação. Por isso, se o sistema estiver em uso, os usuários podem não ver resultados atualizados;
* A reindexação envolve a passagem de todo o repositório, o que pode colocar uma carga elevada na configuração do AEM e, portanto, afetar a experiência do usuário final;
* Para uma instalação `DocumentNodeStore` em que a reindexação pode levar um tempo considerável, se a conexão com o banco de dados Mongo falhar no meio da operação, a indexação teria que ser reiniciada do zero;

* Em alguns casos, a reindexação pode levar muito tempo devido à extração de texto. Isso é específico principalmente para configurações com muitos arquivos PDF, onde o tempo gasto na extração de texto pode afetar o tempo de indexação.

Para atingir esses objetivos, a ferramenta de indexação de carvalho suporta diferentes modos de reindexação que podem ser usados conforme necessário. O comando oak-run index fornece os seguintes benefícios:

* **reindexação**  fora de banda - reindexação executada em carvalho pode ser feita separadamente de uma configuração AEM em execução e, portanto, minimiza o impacto na instância AEM que está em uso;

* **reindexação**  fora de faixa - A reindexação ocorre sem afetar as operações de indexação. Isto significa que o indexador assíncrono pode continuar a indexar outros índices;

* **Reindexação simplificada para instalações**  DocumentNodeStore - para  `DocumentNodeStore` instalações, a reindexação pode ser feita com um único comando que garante que a reindexação seja feita da maneira mais ideal;

* **Suporta a atualização das definições de índice e a introdução de novas definições de índice**

### Reindex - DocumentNodeStore {#reindexdocumentnodestore}

Para `DocumentNodeStore` instalações, a reindexação pode ser feita por meio de um único comando de execução de carvalho:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Isso proporciona os seguintes benefícios

* Impacto mínimo na execução de instâncias AEM. A maioria das leituras pode ser feita em servidores secundários e a execução AEM caches não é prejudicada negativamente devido a todas as transmissões necessárias para a reindexação;
* Os usuários também podem fornecer um JSON de um índice novo ou atualizado por meio da opção `--index-definitions-file`.

### Reindex - SegmentNodeStore {#reindexsegmentnodestore}

Para instalações `SegmentNodeStore`, a reindexação pode ser feita de uma das seguintes maneiras:

#### Reindexação online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga a forma estabelecida na qual a reindexação é feita por meio da configuração do sinalizador `reindex`.

#### Reindexação online - SegmentNodeStore - A instância AEM está em execução {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para instalações `SegmentNodeStore`, somente um processo pode acessar arquivos de segmento no modo de leitura/gravação. Devido a isso, algumas operações na indexação de carvalho exigem etapas manuais adicionais.

Isso envolveria:

1. Texto da etapa
1. Conecte `oak-run` ao mesmo repositório usado pelo AEM no modo somente leitura e execute a indexação. Um exemplo de como fazer isso:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Por fim, importe os arquivos de índice criados pela operação `IndexerMBean#importIndex` do caminho onde oak-run salvou os arquivos de indexação depois de executar o comando acima.

Nesse cenário, você não precisa parar o servidor AEM nem fornecer nenhuma nova instância. No entanto, como a indexação envolve a passagem de todo o repositório, isso aumentaria a carga de E/S na instalação, afetando negativamente o desempenho do tempo de execução.

#### Reindex Online - SegmentNodeStore - A instância AEM é Desligada {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para `SegmentNodeStore` instalações, a reindexação pode ser feita por meio de um único comando de execução de carvalho. No entanto, a instância AEM precisa ser fechada.

Você pode acionar a reindexação com o seguinte comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

A diferença entre essa abordagem e a descrita acima é que a criação do ponto de verificação e a importação do índice são feitas automaticamente. O lado negativo é que AEM precisa ficar inativo durante o processo.

#### Reindexação fora da banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

Nesse caso de uso, é possível executar a reindexação em uma configuração clonada para minimizar o impacto na instância AEM em execução:

1. Criar ponto de verificação por meio de uma operação JMX. Você pode fazer isso indo para [Console JMX](/help/sites-administering/jmx-console.md) e pesquisar `CheckpointManager`. Em seguida, clique na operação **createCheckpoint(long p1)** usando um valor alto para expiração em segundos (por exemplo, **2592000**).
1. Copie a pasta `crx-quickstart` para uma nova máquina
1. Executar reindexação por meio do comando oak-run index

1. Copiar os arquivos de índice gerados para AEM servidor

1. Importe os arquivos de índice via JMX.

Nesse caso de uso, presume-se que o Data Store esteja acessível em outra instância que pode não ser possível se `FileDataStore` for colocado em uma solução de armazenamento baseada em nuvem como EBS. Isso exclui o cenário em que `FileDataStore` também é clonado. Se a definição do índice não executar indexação de texto completo, então o acesso a `DataStore` não é necessário.

## Caso de uso 4 - Atualização das definições de índice {#usecase4updatingindexdefinitions}

Atualmente, você pode enviar alterações de definição de índice por meio do pacote [ACS Sure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Isso permite o envio das definições de índice por meio do pacote de conteúdo, que posteriormente requer a reindexação para ser executada por meio da configuração do sinalizador `reindex` como `true`.

Isso funciona bem para instalações menores onde a reindexação não demora muito. No entanto, para repositórios muito grandes, a reindexação será feita num período de tempo consideravelmente maior. Para esses casos, agora podemos usar a ferramenta de indexação de carvalho-run.

A execução de Oak agora oferece suporte ao fornecimento de definições de índice no formato JSON e à criação de índice no modo fora de banda, onde nenhuma alteração é executada em uma instância ativa.

O processo que você precisa considerar para este caso de uso é:

1. Um desenvolvedor atualizaria as definições de índice em uma instância local e geraria um arquivo JSON de definição de índice por meio da opção `--index-definitions`

1. O JSON atualizado é então fornecido ao administrador do sistema
1. O Administrador de sistema segue a abordagem fora de banda e prepara o índice em uma instalação diferente
1. Quando isso for concluído, os arquivos de índice gerados serão importados em uma instalação AEM em execução.

