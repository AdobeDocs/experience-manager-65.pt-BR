---
title: Uso da reindexação offline para reduzir o tempo de inatividade durante uma atualização
description: Saiba como usar a metodologia de reindexação offline para reduzir o tempo de inatividade do sistema ao executar uma atualização AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: d3a69bbbc9c3707538be74fd05f94f20a688d860
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---


# Uso da reindexação offline para reduzir o tempo de inatividade durante uma atualização {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Introdução {#introduction}

Um dos principais desafios da atualização do Adobe Experience Manager é o tempo de inatividade associado ao ambiente do autor quando uma atualização no local é realizada. Os autores de conteúdo não poderão acessar o ambiente durante uma atualização. Portanto, é desejável minimizar o tempo necessário para executar a atualização. Para repositórios grandes, especialmente projetos da AEM Assets, que normalmente têm grandes armazenamentos de dados e um alto nível de uploads de ativos por hora, a reindexação de índices Oak leva uma porcentagem significativa do tempo de atualização.

Esta seção descreve como usar a ferramenta Oak-run para reindexar o repositório **antes** de executar a atualização, reduzindo assim o tempo de inatividade durante a atualização real. As etapas apresentadas podem ser aplicadas aos índices [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) para versões AEM 6.4 e posteriores.

## Visão geral {#overview}

Novas versões do AEM introduzem alterações nas definições de índice Oak à medida que o conjunto de recursos é expandido. As alterações nos índices Oak forçam a reindexação ao atualizar a instância AEM. A reindexação é cara para implantações de ativos, pois o texto em ativos (por exemplo, o texto no arquivo pdf) é extraído e indexado. Com repositórios MongoMK, os dados são persistentes na rede, aumentando ainda mais o tempo que a reindexação leva.

O problema que a maioria dos clientes enfrenta durante uma atualização é reduzir o tempo de inatividade. A solução é **ignorar** a atividade de reindexação durante a atualização. Isso pode ser feito criando os novos decs **antes** de executar a atualização e simplesmente importando-os durante a atualização.

## Abordagem {#approach}

![offline-reindexing-upgrade-text-extração](assets/offline-reindexing-upgrade-process.png)

A ideia é criar o índice antes da atualização, em relação às definições de índice da versão AEM público alvo usando a ferramenta [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) . O diagrama acima mostra a abordagem de reindexação offline.

Além disso, essa é a ordem das etapas conforme descrito na abordagem:

1. O texto dos binários é extraído primeiro
2. São criadas definições de índice de Públicos alvos
3. Índices offline são criados
4. Os índices são então importados durante o processo de atualização

### Extração de texto {#text-extraction}

Para permitir a indexação completa no AEM, o texto de binários como PDF é extraído e adicionado ao índice. Esta é geralmente uma etapa cara no processo de indexação. A extração de texto é uma etapa de otimização defendida especialmente para reindexar repositórios de ativos, pois armazena um grande número de binários.

![offline-reindexing-upgrade-text-extração](assets/offline-reindexing-upgrade-text-extraction.png)

O texto de binários armazenados no sistema pode ser extraído usando a ferramenta de execução de carvalho com a biblioteca de dicas. Um clone dos sistemas de produção pode ser executado antes da atualização e pode ser usado para esse processo de extração de texto. Esse processo cria o armazenamento de texto, seguindo as seguintes etapas:

**1. Analise o repositório e reúna os detalhes dos binários**

Essa etapa produz um arquivo CSV contendo uma tupla de binários, contendo um caminho e uma id de blob.

Execute o comando abaixo do diretório no qual deseja criar o índice. O exemplo abaixo assume o diretório inicial do repositório.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Onde `nodestore path` está o `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Use o `--fake-ds-path=temp` parâmetro em vez de `–fds-path` para acelerar o processo.

**2. Reutilizar o arquivo de texto binário disponível no índice existente**

Despeje os dados de índice do sistema existente e extraia o armazenamento de texto.

Você pode descarregar os dados de índice existentes usando o seguinte comando:

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Onde `nodestore path` está o `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Em seguida, use o despejo de índice acima para preencher a loja:

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Onde `oak-index-name` é o nome do índice de texto completo, por exemplo &quot;lucene&quot;.

**3. Execute o processo de extração de texto usando a biblioteca de dicas para os binários omitidos na etapa acima**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Onde `datastore path` é o caminho para o armazenamento de dados binário.

O armazenamento de texto criado pode ser atualizado e reutilizado para reindexar cenários no futuro.

Para obter mais detalhes sobre o processo de extração de texto, consulte a documentação [executada pelo](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)Oak.

### Reindexação offline {#offline-reindexing}

![reindexação offline-atualização-reindexação offline](assets/offline-reindexing-upgrade-offline-reindexing.png)

Crie o índice Lucene offline antes da atualização. Se estiver usando o MongoMK, é recomendável executá-lo diretamente em um dos nós do MongoMk, pois isso evita a sobrecarga da rede.

Para criar o índice offline, siga as etapas abaixo:

**1. Gerar definições de índice do Oak Lucene para a versão do público alvo AEM**

Despeje as definições de índice existentes. As definições de índice que sofreram alterações foram geradas usando o pacote de repositório Adobe Granite da versão AEM público alvo e oak-run.

Para descarregar a definição de índice da instância de AEM de **origem** , execute este comando:

>[!NOTE]
>
>Para mais informações sobre as definições do índice de dumping, consulte a documentação [do](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)Oak.

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Onde `datastore path` e `nodestore path` são da instância de AEM **de origem** .

Em seguida, gere definições de índice da versão de AEM do **público alvo** usando o pacote de repositório Granite da versão de público alvo.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> O processo de criação da definição de índice acima é suportado somente a partir da `oak-run-1.12.0` versão. A definição de metas é feita usando o pacote de repositório Granite `com.adobe.granite.repository-x.x.xx.jar`.

As etapas acima criam um arquivo JSON chamado `merge-index-definitions_target.json` que é a definição do índice.

**2. Criar um ponto de verificação no repositório**

Crie um ponto de verificação na instância AEM **fonte** de produção com uma duração longa. Isso deve ser feito antes da clonagem do repositório.

Por meio do console JMX localizado em `http://serveraddress:serverport/system/console/jmx`, acesse `CheckpointMBean` e crie um ponto de verificação com uma duração suficiente (por exemplo, 200 dias). Para isso, invoque `CheckpointMBean#createCheckpoint` com `17280000000` o argumento para a duração da vida em milissegundos.

Quando isso for feito, copie a ID do ponto de verificação recém-criada e valide a vida útil usando o JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Esse ponto de verificação será excluído quando o índice for importado posteriormente.

Para obter mais detalhes, consulte a criação [de ponto de](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) verificação na documentação do Oak.

**Executar indexação offline para as definições de índice geradas**

A reindexação de Lucene pode ser feita offline usando a execução de carvalho. Esse processo cria dados de índice no disco em `indexing-result/indices`. Ele **não** grava no repositório e, portanto, não requer interromper a execução da instância AEM. O repositório de texto criado é alimentado neste processo:

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indices in this file will be re-indexed.
```

O uso do `--doc-traversal-mode` parâmetro é útil em instalações MongoMK, pois melhora significativamente o tempo de reindexação, pois faz com que o conteúdo do repositório seja convertido em um arquivo simples local. No entanto, requer espaço em disco adicional de duplo do tamanho do repositório.

No caso do MongoMK, esse processo pode ser acelerado se essa etapa for executada em uma instância mais próxima à instância do MongoDB. Se executado no mesmo computador, a sobrecarga da rede pode ser evitada.

Detalhes técnicos adicionais podem ser encontrados na documentação de [execução de carvalho para indexação](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importando Índices {#importing-indices}

Com AEM 6.4 e versões mais recentes, a AEM tem a capacidade integrada de importar índices do disco na sequência de inicialização. A pasta `<repository>/indexing-result/indices` é monitorada para detectar a presença de dados de índice durante a inicialização. Você pode copiar o índice pré-criado no local acima durante o processo [de](in-place-upgrade.md#performing-the-upgrade) atualização antes de começar com a nova versão do **público alvo** AEM jar. AEM o importa para o repositório e remove o ponto de verificação correspondente do sistema. Assim, um reíndice é completamente evitado.

## Dicas e solução de problemas adicionais {#troubleshooting}

Abaixo, você encontrará algumas dicas úteis e instruções para solução de problemas.

### Reduza o impacto no sistema de produção em tempo real {#reduce-the-impact-on-the-live-production-system}

É recomendável clonar o sistema de produção e criar o índice offline usando o clone. Isso elimina qualquer impacto potencial no sistema de produção. No entanto, o ponto de verificação necessário para importar o índice precisa estar presente no sistema de produção. Portanto, a criação de um ponto de verificação antes de receber o clone é essencial.

### Preparar um Runbook e uma Execução de Avaliação {#prepare-a-runbook-and-trial-run}

É recomendável preparar um [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) e executar algumas avaliações antes de executar a atualização na produção.

### Modo de cruzamento Doc com indexação offline {#doc-traversal-mode-with-offline-indexing}

A indexação offline requer vários traversais de todo o repositório. Com instalações MongoMK, o repositório é acessado pela rede, afetando o desempenho do processo de indexação. Uma opção é executar o processo de indexação offline na própria réplica MongoDB, o que eliminará a sobrecarga da rede. Outra opção é o uso do modo de passagem doc.

O modo de travessia do documento pode ser aplicado adicionando o parâmetro da linha de comando `—doc-traversal` ao comando oak-run para indexação offline. Esse modo armazena uma cópia de todo o repositório no disco local como um arquivo simples e a usa para executar a indexação.
