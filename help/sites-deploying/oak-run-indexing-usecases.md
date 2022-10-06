---
title: Casos de uso da indexação Oak-run.jar
seo-title: Oak-run.jar Indexing Use Cases
description: Saiba mais sobre os vários casos de usuário para executar indexação com a ferramenta Oak-run.
seo-description: Learn about the various user cases for performing indexing with the Oak-run tool.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 0%

---

# Casos de uso da indexação Oak-run.jar{#oak-run-jar-indexing-use-cases}

O Oak-run oferece suporte à indexação de casos de uso na linha de comando sem precisar orquestrar a execução desses casos de uso por meio AEM console JMX.

Os benefícios abrangentes de usar a abordagem de comando de índice oak-run.jar para gerenciar índices Oak são:

1. O comando Oak-run index fornece um novo conjunto de ferramentas de indexação para o AEM 6.4.
1. A execução do Oak reduz o tempo de reindexação, o que reduz os tempos de reindexação em repositórios maiores.
1. A execução do Oak reduz o consumo de recursos durante a reindexação no AEM, resultando em um desempenho geral do sistema melhor.
1. O Oak-run fornece reindexação fora de banda, suporta situações em que a produção deve estar disponível e não pode tolerar manutenção ou tempo de inatividade necessário para reindexar.

As seções abaixo forneceriam comandos de amostra. o comando oak-run index suporta todas as configurações NodeStore e BlobStore. Os exemplos fornecidos abaixo são sobre configurações com FileDataStore e SegmentNodeStore.

## Caso de uso 1 - Verificação de consistência do índice {#usercase1indexconsistencycheck}

Este é um caso de uso relacionado à corrupção do índice. Em alguns casos, não foi possível determinar quais dos índices estão corrompidos. Portanto, o Adobe forneceu ferramentas que:

1. Executa verificações de consistência de índice em todos os índices e fornece um relatório sobre quais índices são válidos e quais não são válidos;
1. As ferramentas podem ser utilizadas mesmo que não AEM acessíveis;
1. É fácil de usar.

A verificação de índices corrompidos pode ser executada por meio de `--index-consistency-check` operação:

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

Para diagnosticar alguns dos casos em torno do Adobe de desempenho da consulta, geralmente exigia a definição de índice existente, as estatísticas relacionadas ao índice da configuração do cliente. Até agora, essa informação estava espalhada por vários recursos. Para facilitar a solução de problemas, o Adobe criou ferramentas que:

1. Despejar todas as definições de índice presentes no sistema em um único arquivo JSON;

1. Eliminar estatísticas importantes dos índices existentes;

1. Despejar conteúdo do índice para análise offline;

1. Usará mesmo se AEM não estiver acessível

As operações acima agora podem ser feitas por meio dos seguintes comandos operation index:

* `--index-info` - Coleta e despeja várias estatísticas relacionadas aos índices

* `--index-definitions` - Coleta e despeja definições de índice

* `--index-dump` - Conteúdo do índice de despejos

Veja abaixo um exemplo de como os comandos funcionam na prática:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Os relatórios seriam gerados em `indexing-result/index-info.txt` e `indexing-result/index-definitions.json`

Além disso, os mesmos detalhes são fornecidos por meio do Console da Web e fazem parte do zip do despejo de configuração. Elas podem ser acessadas no seguinte local:

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Benefícios {#uc2benefits}

Essa ferramenta permite a coleta de todos os detalhes necessários relacionados a problemas de indexação ou consulta rapidamente e reduz o tempo gasto na extração dessas informações.

## Caso de uso 3 - Reindexação {#usecase3reindexing}

Dependendo do [cenários](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), em alguns casos, a reindexação precisa ser executada. Atualmente, a reindexação é feita definindo a variável `reindex` sinalizador para `true` no nó de definição de índice por meio do CRXDE ou pela interface do usuário do Gerenciador de índice. Depois que o sinalizador é definido, a reindexação é feita de forma assíncrona.

Alguns pontos para observar sobre a reindexação:

* A reindexação é muito mais lenta no `DocumentNodeStore` configurações comparadas a `SegmentNodeStore` Configurações em que todo o conteúdo é local;

* Com o design atual, enquanto a reindexação acontece, o indexador assíncrono é bloqueado e todos os outros índices assíncronos ficam obsoletos e não obtêm atualização pela duração da indexação. Por isso, se o sistema estiver em uso, os usuários podem não ver resultados atualizados;
* A reindexação envolve a travessia de todo o repositório, que pode colocar uma alta carga na configuração do AEM e, portanto, afetar a experiência do usuário final;
* Para um `DocumentNodeStore` Instalação em que a reindexação possa demorar um tempo considerável, se a ligação à base de dados Mongo falhar no meio da operação, a indexação teria de ser reiniciada do zero;

* Em alguns casos, a reindexação pode demorar muito por causa da extração de texto. Isso é específico principalmente para configurações com muitos arquivos PDF, onde o tempo gasto na extração de texto pode afetar o tempo de indexação.

Para atingir esses objetivos, a ferramenta de índice oak-run oferece suporte a diferentes modos para reindexação, que podem ser usados conforme necessário. O comando oak-run index oferece os seguintes benefícios:

* **reindexação fora de banda** - a reindexação oak-run pode ser feita separadamente de uma configuração de AEM em execução e, portanto, minimiza o impacto na instância de AEM que está em uso;

* **reindexação fora de faixa** - A reindexação tem lugar sem afetar as operações de indexação. Isso significa que o indexador assíncrono pode continuar a indexar outros índices;

* **Reindexação simplificada para instalações do DocumentNodeStore** - Para `DocumentNodeStore` instalações, a reindexação pode ser feita com um único comando que assegure que a reindexação seja feita da melhor maneira;

* **Oferece suporte à atualização das definições de índice e à introdução de novas definições de índice**

### Reindexar - DocumentNodeStore {#reindexdocumentnodestore}

Para `DocumentNodeStore` a reindexação de instalações pode ser feita por meio de um único comando oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Isso oferece os seguintes benefícios

* Impacto mínimo na execução de instâncias de AEM. A maioria das leituras pode ser feita em servidores secundários e a execução de AEM caches não é negativamente afetada devido a toda a travessia necessária para reindexação;
* Os usuários também podem fornecer um JSON de um índice novo ou atualizado por meio do `--index-definitions-file` opção.

### Reindexar - SegmentNodeStore {#reindexsegmentnodestore}

Para `SegmentNodeStore` a reindexação de instalações pode ser feita de uma das seguintes maneiras:

#### Reindexação online - SegmentNodeStore {#onlinereindexsegmentnodestore}

Siga a forma estabelecida para a reindexação através da definição `reindex` sinalizador.

#### Reindexação online - SegmentNodeStore - A instância de AEM está em execução {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Para `SegmentNodeStore` O instala somente um processo pode acessar arquivos de segmento no modo leitura-gravação. Devido a isso, algumas operações na indexação de oak-run exigem etapas manuais adicionais sendo executadas.

Isso envolveria o seguinte:

1. Texto da etapa
1. Conecte o `oak-run` para o mesmo repositório usado pelo AEM no modo somente leitura e executar indexação. Um exemplo de como fazer isso:

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Por fim, importe os arquivos de índice criados por meio da `IndexerMBean#importIndex` operação a partir do caminho em que oak-run salvou os arquivos de indexação depois de executar o comando acima.

Nesse cenário, não é necessário interromper o servidor de AEM ou provisionar nenhuma nova instância. No entanto, como a indexação envolve a passagem de todo o repositório, ela aumentaria a carga de I/O na instalação, afetando negativamente o desempenho do tempo de execução.

#### Reindexação online - SegmentNodeStore - A instância AEM é desligada {#onlinereindexsegmentnodestoreaeminstanceisdown}

Para `SegmentNodeStore` a reindexação de instalações pode ser feita por meio de um único comando oak-run. No entanto, a instância de AEM precisa ser encerrada.

Você pode acionar a reindexação com o seguinte comando:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

A diferença entre essa abordagem e a explicada acima é que a criação do ponto de verificação e a importação do índice são feitas automaticamente. O lado negativo é que AEM precisa ficar inativo durante o processo.

#### Reindexação fora da banda - SegmentNodeStore {#outofbandreindexsegmentnodestore}

Nesse caso de uso, é possível executar a reindexação em uma configuração clonada para minimizar o impacto na instância de AEM em execução:

1. Crie um ponto de verificação por meio de uma operação JMX. Você pode fazer isso indo para o [Console JMX](/help/sites-administering/jmx-console.md) e procurar `CheckpointManager`. Em seguida, clique no botão **createCheckpoint(long p1)** operação usando um valor alto para expiração em segundos (por exemplo, **2592000**).
1. Copie o `crx-quickstart` pasta para uma nova máquina
1. Executar reindexação por meio do comando oak-run index

1. Copie os arquivos de índice gerados para AEM servidor

1. Importe os arquivos de índice via JMX.

Nesse caso de uso, presume-se que o Data Store esteja acessível em outra instância, o que pode não ser possível se `FileDataStore` é colocada em uma solução de armazenamento baseada em nuvem como EBS. Isso exclui o cenário em que `FileDataStore` também é clonado. Se a definição de índice não executar indexação de texto completo, então acesse `DataStore` não é obrigatório.

## Caso de uso 4 - Atualização das definições do índice {#usecase4updatingindexdefinitions}

Atualmente, é possível enviar alterações na definição do índice por meio de [ACS - Garantia de índice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) pacote. Isso permite o envio das definições de índice por meio do pacote de conteúdo, que posteriormente requer a reindexação para ser executada por meio da configuração da variável `reindex` sinalizador para `true`.

Isso funciona bem em instalações menores, onde a reindexação não leva muito tempo. No entanto, para repositórios muito grandes, a reindexação será feita em um período consideravelmente maior. Para esses casos, agora podemos usar a ferramenta de índice oak-run.

O Oak-run agora oferece suporte para fornecer definições de índice no formato JSON e criação de índice no modo fora de banda, onde nenhuma alteração é executada em uma instância ativa.

O processo que você precisa considerar para este caso de uso é:

1. Um desenvolvedor atualizaria as definições de índice em uma instância local e geraria um arquivo JSON de definição de índice por meio da variável `--index-definitions` opção

1. O JSON atualizado é então fornecido ao Administrador do sistema
1. O Administrador do sistema segue a abordagem fora de banda e prepara o índice em uma instalação diferente
1. Depois que isso for concluído, os arquivos de índice gerados serão importados em uma instalação AEM em execução.
