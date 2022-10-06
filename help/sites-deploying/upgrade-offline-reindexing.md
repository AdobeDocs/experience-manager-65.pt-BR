---
title: Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização
description: Saiba como usar a metodologia de reindexação offline para reduzir o tempo de inatividade do sistema ao executar uma atualização de AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# Usar a reindexação offline para reduzir o tempo de inatividade durante uma atualização {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introdução {#introduction}

Um dos principais desafios da atualização do Adobe Experience Manager é o tempo de inatividade associado ao ambiente de criação quando uma atualização no local é realizada. Os autores de conteúdo não poderão acessar o ambiente durante uma atualização. Portanto, é desejável minimizar a quantidade de tempo necessária para executar a atualização. Para repositórios grandes, especialmente projetos da AEM Assets, que normalmente têm grandes armazenamentos de dados e um alto nível de uploads de ativos por hora, a reindexação de índices do Oak leva uma porcentagem significativa do tempo de atualização.

Esta seção descreve como usar a ferramenta Oak-run para reindexar o repositório **before** executar a atualização, reduzindo assim o tempo de inatividade durante a atualização real. As etapas apresentadas podem ser aplicadas a [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) índices para versões AEM 6.4 e superior.

## Visão geral {#overview}

Novas versões do AEM introduzem alterações nas definições de índice Oak à medida que o conjunto de recursos é expandido. As alterações nos índices do Oak forçam a reindexação ao atualizar a instância do AEM. A reindexação é cara para implantações de ativos, pois o texto em ativos (por exemplo, o texto no arquivo pdf) é extraído e indexado. Com repositórios MongoMK, os dados persistem na rede, aumentando ainda mais o tempo que a reindexação leva.

O problema que a maioria dos clientes enfrentam durante uma atualização é reduzir a janela de tempo de inatividade. A solução é **ignorar** a atividade de reindexação durante a atualização. Isso pode ser feito criando-se novos decretos **before** para executar a atualização, basta importá-los durante a atualização.

## Abordagem {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

A ideia é criar o índice antes da atualização, em relação às definições de índice da versão de AEM de destino usando o [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) ferramenta. O diagrama acima mostra a abordagem de reindexação offline.

Além disso, esta é a ordem das etapas conforme descrito na abordagem:

1. O texto de binários é extraído primeiro
2. Definições de índice do Target são criadas
3. Os índices offline são criados
4. Os índices são importados durante o processo de atualização

### Extração de texto {#text-extraction}

Para permitir a indexação completa em AEM, o texto de binários como o PDF é extraído e adicionado ao índice. Geralmente, essa é uma etapa cara no processo de indexação. A extração de texto é uma etapa de otimização defendida especialmente para reindexar repositórios de ativos, pois armazena um grande número de binários.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

O texto de binários armazenados no sistema pode ser extraído usando a ferramenta oak-run com a biblioteca tika. Um clone dos sistemas de produção pode ser feito antes da atualização e pode ser usado para esse processo de extração de texto. Esse processo cria o armazenamento de texto, seguindo as seguintes etapas:

**1. Analise o repositório e colete os detalhes de binários**

Essa etapa produz um arquivo CSV contendo uma tupla de binários, contendo um caminho e uma id de blob.

Execute o comando abaixo no diretório em que deseja criar o índice. O exemplo abaixo assume o diretório inicial do repositório.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Onde `nodestore path` é `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Use o `--fake-ds-path=temp` em vez de `–fds-path` para acelerar o processo.

**2. Reutilizar o armazenamento de texto binário disponível no índice existente**

Despeje os dados de índice do sistema existente e extraia o armazenamento de texto.

Você pode despejar os dados de índice existentes usando o seguinte comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Onde `nodestore path` é `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Em seguida, use o despejo de índice acima para preencher a loja:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Onde `oak-index-name` é o nome do índice de texto completo, por exemplo, &quot;lucene&quot;.

**3. Execute o processo de extração de texto usando a biblioteca de dicas para os binários ignorados na etapa acima**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Onde `datastore path` é o caminho para o armazenamento de dados binário.

O armazenamento de texto criado pode ser atualizado e reutilizado para cenários de reindexação no futuro.

Para obter mais detalhes sobre o processo de extração de texto, consulte o [Documentação Oak-run](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Reindexação offline {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Crie o índice Lucene offline antes da atualização. Se estiver usando o MongoMK, é recomendável executá-lo diretamente em um dos nós do MongoMk, pois isso evita a sobrecarga da rede.

Para criar o índice offline, siga as etapas abaixo:

**1. Gerar definições de índice Oak Lucene para a versão de AEM de destino**

Despeje as definições de índice existentes. As definições de índice que sofreram alteração foram geradas usando o pacote de repositório Adobe Granite da versão de AEM de destino e oak-run.

Para despejar a definição do índice do **source** AEM instância, execute este comando:

>[!NOTE]
>
>Para mais informações sobre definições de índices de dumping, consulte o [Documentação do Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Onde `datastore path` e `nodestore path` são da **source** AEM instância.

Em seguida, gere definições de índice a partir da variável **target** AEM versão usando o pacote de repositório Granite da versão de destino.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> O processo de criação da definição de índice acima é compatível somente com o `oak-run-1.12.0` em diante. O direcionamento é feito usando o pacote de repositório do Granite `com.adobe.granite.repository-x.x.xx.jar`.

As etapas acima criam um arquivo JSON chamado `merge-index-definitions_target.json` que é a definição do índice.

**2. Criar um ponto de verificação no repositório**

Criar um ponto de verificação na produção **source** AEM instância com uma duração longa. Isso deve ser feito antes da clonagem do repositório.

Por meio do console JMX localizado em `http://serveraddress:serverport/system/console/jmx`, vá para `CheckpointMBean` e criar um ponto de verificação com duração suficiente (por exemplo, 200 dias). Para isso, chame `CheckpointMBean#createCheckpoint` com `17280000000` como o argumento para a duração da vida útil em milissegundos.

Depois disso, copie a ID do ponto de verificação recém-criada e valide a vida útil usando JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Esse ponto de verificação será excluído quando o índice for importado posteriormente.

Para obter mais detalhes, consulte [criação do ponto de verificação](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) na documentação do Oak.

**Executar indexação offline para as definições de índice geradas**

A reindexação do Lucene pode ser feita offline usando oak-run. Esse processo cria dados de índice no disco em `indexing-result/indexes`. Ele faz **not** gravar no repositório e, portanto, não é necessário parar a instância AEM em execução. O armazenamento de texto criado é alimentado neste processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

Uso do `--doc-traversal-mode` O parâmetro é útil para instalações do MongoMK, pois melhora significativamente o tempo de reindexação, pois detalha o conteúdo do repositório em um arquivo simples local. No entanto, ele requer espaço em disco adicional do dobro do tamanho do repositório.

No caso do MongoMK, esse processo poderá ser acelerado se essa etapa for executada em uma instância mais próxima da instância do MongoDB. Se executado na mesma máquina, a sobrecarga da rede pode ser evitada.

Os detalhes técnicos adicionais podem ser encontrados na seção [documentação de oak-run para indexação](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importação de índices {#importing-indexes}

Com AEM 6.4 e versões mais recentes, o AEM tem o recurso integrado para importar índices do disco na sequência de inicialização. A pasta `<repository>/indexing-result/indexes` O é observado para a presença de dados de índice durante a inicialização. Você pode copiar o índice pré-criado para o local acima durante a [processo de atualização](in-place-upgrade.md#performing-the-upgrade) antes de começar com a nova versão do **target** AEM jar. AEM o importa para o repositório e remove o ponto de verificação correspondente do sistema. Assim, uma reindexação é completamente evitada.

## Dicas e solução de problemas adicionais {#troubleshooting}

Abaixo você encontrará algumas dicas úteis e instruções para a solução de problemas.

### Reduza o impacto no sistema de produção em tempo real {#reduce-the-impact-on-the-live-production-system}

É recomendável clonar o sistema de produção e criar o índice offline usando o clone. Isso elimina qualquer impacto potencial no sistema de produção. No entanto, o ponto de verificação necessário para importar o índice precisa estar presente no sistema de produção. Portanto, criar um ponto de verificação antes de tomar o clone é essencial.

### Preparar um Runbook e uma Execução de Avaliação {#prepare-a-runbook-and-trial-run}

Recomenda-se a preparação de uma [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) e realizar algumas tentativas antes de executar a atualização na produção.

### Modo de passagem do documento com indexação offline {#doc-traversal-mode-with-offline-indexing}

A indexação offline requer várias travessias de todo o repositório. Com as instalações do MongoMK, o repositório é acessado pela rede, afetando o desempenho do processo de indexação. Uma opção é executar o processo de indexação offline na própria réplica do MongoDB, o que eliminará a sobrecarga da rede. Outra opção é o uso do modo de passagem doc.

O modo de travessia do documento pode ser aplicado adicionando o parâmetro da linha de comando `—doc-traversal` para o comando oak-run para indexação offline. Esse modo armazena uma cópia de todo o repositório no disco local como um arquivo simples e a usa para executar a indexação.
