---
title: Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização
description: Saiba como usar a metodologia de reindexação offline para reduzir o tempo de inatividade do sistema ao executar uma atualização do AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introdução {#introduction}

Um dos principais desafios na atualização do Adobe Experience Manager é o tempo de inatividade associado ao ambiente do autor quando uma atualização no local é executada. Os autores de conteúdo não poderão acessar o ambiente durante uma atualização. Portanto, é desejável minimizar a quantidade de tempo que leva para executar a atualização. Para repositórios grandes, especialmente projetos do AEM Assets, que normalmente têm grandes armazenamentos de dados e um alto nível de uploads de ativos por hora, a reindexação de índices do Oak leva uma porcentagem significativa do tempo de atualização.

Esta seção descreve como usar a ferramenta de execução do Oak para reindexar o repositório **antes** de executar a atualização, reduzindo assim o tempo de inatividade durante a atualização. As etapas apresentadas podem ser aplicadas a índices [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) para versões AEM 6.4 e superiores.

## Visão geral {#overview}

Novas versões do AEM introduzem alterações nas definições do índice Oak à medida que o conjunto de recursos é expandido. As alterações nos índices do Oak forçam a reindexação ao atualizar a instância AEM. A reindexação é cara para implantações de ativos, pois o texto nos ativos (por exemplo, texto em arquivo pdf) é extraído e indexado. Com repositórios MongoMK, os dados são mantidos pela rede, aumentando ainda mais a quantidade de tempo que a reindexação leva.

O problema que a maioria dos clientes está enfrentando durante uma atualização é reduzir o tempo de inatividade. A solução é **ignorar** a atividade de reindexação durante a atualização. Isso pode ser feito criando os novos índices **anteriores** para executar a atualização e simplesmente importando-os durante a atualização.

## Abordagem {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

A ideia é criar o índice antes da atualização, comparando as definições de índice da versão do AEM de destino usando a ferramenta [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). O diagrama acima mostra a abordagem de reindexação offline.

Além disso, esta é a ordem das etapas, conforme descrito na abordagem:

1. O texto de binários é extraído primeiro
2. As definições de índice de destino são criadas
3. Os índices offline foram criados
4. Os índices são importados durante o processo de atualização

### Extração de texto {#text-extraction}

Para ativar a indexação completa no AEM, o texto de binários como PDF é extraído e adicionado ao índice. Essa é geralmente uma etapa cara no processo de indexação. A extração de texto é uma etapa de otimização defendida especialmente para reindexar repositórios de ativos, pois eles armazenam um grande número de binários.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

O texto de binários armazenados no sistema pode ser extraído usando a ferramenta thge oak-run com a biblioteca tika. Um clone dos sistemas de produção pode ser obtido antes da atualização e pode ser usado para esse processo de extração de texto. Esse processo cria o armazenamento de texto, executando as seguintes etapas:

**1. Percorrer o repositório e coletar os detalhes de binários**

Essa etapa produz um arquivo CSV contendo uma tupla de binários, um caminho e uma ID de blob.

Execute o comando abaixo no diretório a partir do qual deseja criar o índice. O exemplo abaixo presume o diretório inicial do repositório.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Onde `nodestore path` é `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Use o parâmetro `--fake-ds-path=temp` em vez de `–fds-path` para acelerar o processo.

**2. Reutilizar o armazenamento de texto binário disponível no índice existente**

Despeje os dados de índice do sistema existente e extraia o armazenamento de texto.

Você pode despejar os dados de índice existentes usando o seguinte comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Onde `nodestore path` é `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Em seguida, use o despejo de índice acima para preencher o armazenamento:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Onde `oak-index-name` é o nome do índice de texto completo, por exemplo, &quot;lucene&quot;.

**3. Execute o processo de extração de texto usando a biblioteca tika para os binários perdidos na etapa acima**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Onde `datastore path` é o caminho para o armazenamento de dados binários.

O armazenamento de texto criado pode ser atualizado e reutilizado para cenários de reindexação no futuro.

Para obter mais detalhes sobre o processo de extração de texto, consulte a [documentação de execução do Oak](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexação offline {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Crie o índice Lucene offline antes da atualização. Se estiver usando MongoMK, é recomendável executá-lo diretamente em um dos nós MongoMk, pois isso evita a sobrecarga da rede.

Para criar o índice offline, siga as etapas abaixo:

**1. Gerar definições de índice Oak Lucene para a versão de destino AEM**

Despejar as definições de índice existentes. As definições de índice que sofreram alteração foram geradas usando o pacote de repositório do Adobe Granite da versão AEM de destino e oak-run.

Para despejar a definição de índice da instância AEM **origem**, execute este comando:

>[!NOTE]
>
>Para obter mais detalhes sobre definições de índice de dumping, consulte a [documentação do Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Onde `datastore path` e `nodestore path` são da instância AEM **origem**.

Em seguida, gere definições de índice a partir da versão AEM **target** usando o conjunto de repositórios Granite da versão de destino.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>O processo de criação de definição de índice acima tem suporte somente a partir da versão `oak-run-1.12.0`. O direcionamento é feito usando o pacote de repositório do Granite `com.adobe.granite.repository-x.x.xx.jar`.

As etapas acima criam um arquivo JSON chamado `merge-index-definitions_target.json`, que é a definição do índice.

**2. Criar um ponto de verificação no repositório**

Crie um ponto de verificação na instância do AEM **origem** de produção com uma vida útil longa. Isso deve ser feito antes da clonagem do repositório.

Através do console JMX localizado em `http://serveraddress:serverport/system/console/jmx`, vá para `CheckpointMBean` e crie um ponto de verificação com uma duração suficiente (por exemplo, 200 dias). Para isso, chame `CheckpointMBean#createCheckpoint` com `17280000000` como argumento para a duração da vida útil em milissegundos.

Depois disso, copie a ID do ponto de verificação recém-criada e valide o tempo de vida usando o JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
>Esse ponto de verificação será excluído quando o índice for importado posteriormente.

Para obter mais detalhes, consulte [criação de ponto de verificação](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) na documentação da Oak.

**Executar indexação offline para as definições de índice geradas**

A reindexação do Lucene pode ser feita offline usando oak-run. Este processo cria dados de índice no disco em `indexing-result/indexes`. Ele **não** grava no repositório e, portanto, não requer a interrupção da instância do AEM em execução. O armazenamento de texto criado é alimentado neste processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

O uso do parâmetro `--doc-traversal-mode` é útil para instalações do MongoMK, pois melhora significativamente o tempo de reindexação ao fazer spool do conteúdo do repositório em um arquivo simples local. No entanto, requer espaço adicional em disco com o dobro do tamanho do repositório.

Se houver MongoMK, esse processo poderá ser acelerado se essa etapa for executada em uma instância mais próxima à instância do MongoDB. Se executado na mesma máquina, a sobrecarga de rede pode ser evitada.

Detalhes técnicos adicionais podem ser encontrados na [documentação de execução do oak para indexação](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importação de índices {#importing-indexes}

Com o AEM 6.4 e versões mais recentes, o AEM tem o recurso integrado de importar índices do disco na sequência de inicialização. A pasta `<repository>/indexing-result/indexes` é observada pela presença de dados de índice durante a inicialização. Você pode copiar o índice pré-criado no local acima durante o [processo de atualização](in-place-upgrade.md#performing-the-upgrade) antes de começar com a nova versão do jar AEM **target**. O AEM o importa para o repositório e remove o ponto de verificação correspondente do sistema. Assim, um reindex é completamente evitado.

## Dicas adicionais e solução de problemas {#troubleshooting}

Abaixo você encontrará algumas dicas úteis e instruções para solução de problemas.

### Reduza o impacto no sistema de produção ativo {#reduce-the-impact-on-the-live-production-system}

É recomendável clonar o sistema de produção e criar o índice offline usando o clone. Isso elimina qualquer impacto potencial no sistema de produção. No entanto, o ponto de verificação necessário para importar o índice precisa estar presente no sistema de produção. Portanto, é essencial criar um ponto de verificação antes de obter o clone.

### Preparar um Runbook e uma Execução de Avaliação {#prepare-a-runbook-and-trial-run}

É recomendável preparar um [runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) e executar algumas avaliações antes de executar a atualização em produção.

### Modo De Passagem De Documentos Com Indexação Offline {#doc-traversal-mode-with-offline-indexing}

A indexação offline requer vários percursos de todo o repositório. Com instalações do MongoMK, o repositório é acessado pela rede, afetando o desempenho do processo de indexação. Uma opção é executar o processo de indexação offline na própria réplica do MongoDB, o que eliminará a sobrecarga da rede. Outra opção é o uso do modo de passagem de documento.

O modo de travessia de documentos pode ser aplicado adicionando o parâmetro de linha de comando `—doc-traversal` ao comando oak-run para indexação offline. Esse modo faz spool de uma cópia do repositório inteiro no disco local como um arquivo simples e o usa para executar a indexação.
