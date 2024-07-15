---
title: Indexação por meio do Jar executado pela Oak
description: Saiba como executar a indexação por meio do Jar executado pela Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Indexação por meio do Jar executado pela Oak {#indexing-via-the-oak-run-jar}

A execução de Oak suporta todos os casos de uso de indexação na linha de comando sem precisar operar a partir do nível JMX. As vantagens da abordagem oak-run são:

1. É um novo conjunto de ferramentas de indexação para o AEM 6.4
1. Ele diminui o tempo para reindexação, o que afeta de maneira benéfica os tempos de reindexação em repositórios maiores
1. Ela está reduzindo o consumo de recursos durante a reindexação no AEM, o que resulta em melhor desempenho do sistema para outras atividades do AEM
1. A execução da Oak oferece suporte fora da banda: se as condições de produção não permitirem que você execute a reindexação em instâncias de produção, um ambiente clonado poderá ser usado para a reindexação, para evitar um impacto crítico no desempenho.

Veja abaixo uma lista dos casos de uso que podem ser usados ao executar operações de indexação por meio da ferramenta `oak-run`.

## Verificações de consistência de índice {#indexconsistencychecks}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Caso de Uso 1 - Verificação de Consistência de Índice](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`determina rapidamente se os índices Lucene Oak estão corrompidos.
* É seguro executar em uma instância de AEM em uso para verificar a consistência nos níveis 1 e 2.

![Verificações de Consistência de Índice](assets/screen_shot_2017-12-14at135758.png)

## Estatísticas de índice {#indexstatistics}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Caso de Uso 2 - Estatísticas de Índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` descarta todas as definições de índice, estatísticas de índice importantes e conteúdo de índice para análise offline.
* É seguro executar em uma instância de AEM em uso.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Árvore de decisão da abordagem de reindexação {#reindexingapproachdecisiontree}

Este diagrama é uma árvore decisória para quando usar as várias abordagens de reindexação.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Reindexação MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Caso de Uso 3 - Reindexação](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Pré-extração de texto para SegmentNodeStore e DocumentNodeStore {#textpre-extraction}

A [pré-extração de texto](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (um recurso existente com AEM 6.3) pode ser usada para reduzir o tempo de reindexação. A pré-extração de texto pode ser usada com todas as abordagens de reindexação.

Dependendo da abordagem de indexação do `oak-run.jar`, há várias etapas em ambos os lados da etapa Executar Reindexação no diagrama abaixo.

![Pré-extração de texto para SegmentNodeStore e DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>Laranja indica atividades em que o AEM deve estar em uma janela de manutenção.

### Reindexação online para MongoMK ou RDBMK usando oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexar - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Este é o método recomendado para reindexar instalações de AEM MongoMK (e RDBMK). Nenhum outro método deve ser usado.

Execute esse processo somente em uma única instância AEM no cluster.

![Reindexação online para MongoMK ou RDBMK usando oak-run.jar](assets/5.png)

## Reindexação do TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexar - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Considerações sobre Modo de Espera a Frio (TarMK)**

   * Não há considerações especiais para o Modo de Espera a Frio; as instâncias de Modo de Espera a Frio sincronizam as alterações como de costume.

* **Farms do Publish para o AEM (Farms do Publish do AEM devem ser sempre TarMK)**

   * Para o farm de publicação, isso deve ser feito para todas OU executar as etapas em uma única publicação. Em seguida, clone a configuração para outros (tomando todas as precauções normais ao clonar instâncias de AEM; sling.id - deve vincular a algo aqui).

### Reindexação online para TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexação Online - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Este é o método usado antes da introdução dos novos recursos de indexação do oak-run.jar. Isso é feito definindo a propriedade `reindex=true` no índice Oak.

Essa abordagem pode ser usada se os efeitos de tempo e desempenho para indexação forem aceitáveis para o cliente. Este é frequentemente o caso das instalações de AEM de pequena a média dimensão.

![Reindexação Online para TarMK](assets/6.png)

### Reindexação online do TarMK usando oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexação Online - SegmentNodeStore - A Instância AEM está em Execução](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

A reindexação online do TarMK usando o oak-run.jar é mais rápida do que a [Reindexação Online do TarMK](#onlinere-indexingfortarmk) descrita acima. No entanto, também requer a execução durante uma janela de manutenção; com a menção de que a janela é mais curta e mais etapas são necessárias para executar a reindexação.

>[!NOTE]
>
>Laranja indica operações em que o AEM deve ser executado em um período de manutenção.

![Indexando novamente o TarMK online usando oak-run.jar](assets/7.png)

### Reindexação offline do TarMK usando oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexação Online - SegmentNodeStore - A Instância do AEM está Desligada](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

A reindexação offline de TarMK é a abordagem de reindexação baseada em `oak-run.jar` mais simples para TarMK, pois requer um único comentário `oak-run.jar`. No entanto, exige que a instância do AEM seja desligada.

>[!NOTE]
>
>Vermelho indica operações em que o AEM deve ser desligado.

![Indexação offline de TarMK usando oak-run.jar](assets/8.png)

### Re-indexação fora de banda do TarMK usando oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Reindexação Fora de Banda - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

A reindexação fora de banda minimiza o impacto da reindexação em instâncias AEM em uso.

>[!NOTE]
>
>Vermelho indica operações em que o AEM pode ser desligado.

![Reindexação fora de banda de TarMK usando oak-run.jar](assets/9.png)

## Atualizando Definições de Indexação {#updatingindexingdefinitions}

>[!NOTE]
>
>Para obter informações mais detalhadas sobre este cenário, consulte [Caso de Uso 4 - Atualização das Definições de Índice](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Criação e atualização das definições de índice no TarMK usando o ACS Ensure Index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Verifique se o índice é um projeto suportado pela comunidade e não é compatível com o suporte do Adobe.

Isso permite a definição do índice de remessa por meio do pacote de conteúdo, o que resultará posteriormente na reindexação por meio da definição do sinalizador de reindexação como `true`. Isso funciona para configurações menores em que a reindexação não leva muito tempo.

Para obter mais informações, consulte a [Documentação do ACS Verificar Índice](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) para obter detalhes.

### Criando e atualizando definições de índice no TarMK usando oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Se o impacto no tempo ou no desempenho da reindexação usando métodos não `oak-run.jar` for muito alto, a seguinte abordagem baseada em `oak-run.jar` poderá ser usada para importar e reindexar definições do Índice Lucene em uma instalação de AEM baseada em TarMK.

![Criando e atualizando definições de índice no TarMK usando oak-run.jar](assets/10.png)

### Criação e atualização de definições de índice no MonogMK usando oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Se o impacto de tempo ou desempenho da reindexação usando métodos não `oak-run.jar` for muito alto, a seguinte abordagem baseada em `oak-run.jar` poderá ser usada para importar e reindexar definições de Índice Lucene em instalações de AEM baseadas em MongoMK.

![Criando e Atualizando Definições de Índice no MonogMK usando oak-run.jar](assets/11.png)
