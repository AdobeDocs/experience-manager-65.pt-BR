---
title: Configuração de Solr para SRP
seo-title: Configuração de Solr para SRP
description: Uma instalação do Apache Solr pode ser compartilhada entre a loja de nós (Oak) e a loja comum (SRP) usando coleções diferentes
seo-description: Uma instalação do Apache Solr pode ser compartilhada entre a loja de nós (Oak) e a loja comum (SRP) usando coleções diferentes
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: 7acd89d830b9e758eec1b5a4beb18c22e4d12dcf
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 2%

---


# Configuração de Solr para SRP {#solr-configuration-for-srp}

## Solr para AEM plataforma {#solr-for-aem-platform}

Uma instalação do [Apache Solr](https://lucene.apache.org/solr/) pode ser compartilhada entre a loja [de](../../help/sites-deploying/data-store-config.md) nós (Oak) e a loja [](working-with-srp.md) comum (SRP) usando coleções diferentes.

Se as coleções Oak e SRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o modo [](#solrcloud-mode) SolrCloud fornece um desempenho aprimorado em relação ao modo independente (uma configuração única local de Solr).

### Requisitos {#requirements}

Baixe e instale o Apache Solr:

* [Versão 4.10](https://archive.apache.org/dist/lucene/solr/4.10.4/) ou [versão 5.x](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* A Solr requer Java 1.7 ou superior
* Nenhum serviço é necessário
* Escolha dos modos de execução:

   * Modo autônomo
   * [Modo](#solrcloud-mode) SolrCloud (recomendado para ambientes de produção)

* Escolha da pesquisa multilíngue (MLS)

   * [Instalação do MLS padrão](#installing-standard-mls)
   * [Instalação do Advanced MLS](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

[O modo SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) é recomendado para ambientes de produção. Durante a execução no modo SolrCloud, a SolrCloud deve ser instalada e configurada antes da instalação da Pesquisa multilíngue (MLS).

A recomendação é seguir as instruções da SolrCloud para instalar:

* 3 Nós do SolrCloud no mesmo servidor.
* Um ZooKeeper externo do Apache.

Também é recomendável configurar o JVM para ajustar o uso de memória e a coleta de lixo.

### Exemplo de configuração JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuração do SolrCloud {#solrcloud-setup-commands}

Durante a execução no modo SolrCloud, antes da instalação do MLS, é necessário usar e conhecer os seguintes comandos de configuração do SolrCloud.

#### 1. Carregar uma configuração no ZooKeeper {#upload-a-configuration-to-zookeeper}

Referência:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Criar uma coleção {#create-a-collection}

Referência:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create
](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Uso:
./bin/solr criar \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *porta*\
-s *número de fragmentos* \
-rf *número de réplicas*

#### 3. Vincular uma coleção a um conjunto de configurações {#link-a-collection-to-a-configuration-set}

Vincule uma coleção a uma configuração já carregada no ZooKeeper.

Referência:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Comparação do MLS padrão e avançado {#comparison-of-standard-and-advanced-mls}

A busca multilíngue (MLS) para AEM Communities foi criada para a plataforma Solr para fornecer uma busca aprimorada em todos os idiomas suportados, incluindo o inglês.

O MLS para comunidades AEM está disponível como MLS padrão ou MLS avançado. O MLS padrão inclui apenas configurações de Solr e exclui todos os plug-ins ou arquivos de recursos. O Advanced MLS é a solução mais abrangente e inclui configurações de Solr, bem como plug-ins e recursos relacionados

O MLS padrão inclui melhorias para a pesquisa de conteúdo para os seguintes idiomas:

* Inglês: Aprimorado o remetente para tentar corresponder às derivações de palavras.
* Japonês: Token japonês aprimorado para caracteres de meia largura.

O Advanced MLS inclui melhorias para a pesquisa de conteúdo para os seguintes idiomas:

* Inglês: Substituído por limmatizador.
* Alemão: Descompilador adicionado.
* Francês: Adicionada a manipulação de elisão.
* Chinês (simplificado): Adição de um tokenizer mais inteligente.
* Vários idiomas: Adicionado um rastreador, uma lista de palavra stop e um normalizador.

No total, os 33 idiomas a seguir são suportados no Advanced MLS.

| Arábico | Alemão | Norueguês |
|---|---|---|
| Búlgaro | Grego | Polaco |
| Chinês (simplificado) | Crioulo haitiano | Português |
| Chinês (Tradicional) | Hebraico | Romeno |
| Tcheco | Húngaro | Russo |
| Dinamarquês | Indonês | Eslovaco |
| Holandês | Italiano | Esloveno |
| Inglês | Japonês | Espanhol |
| Estônio | Coreano | Sueco |
| Finlandês | Letão | Tailandês |
| Francês | Lituano | Turco |

#### Comparação entre AEM 6.1 Solr search, Standard MLS e Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Observação**: AEM 6.1 refere-se ao AEM 6.1 Comunidades FP3 e anteriores.

![compare-solr-mls](assets/compare-solr-mls.png)

### Instalação do MLS padrão {#installing-standard-mls}

Para que a coleção SRP (MSRP ou DSRP) seja compatível com o Standard Multilingual Search (MLS), é necessário modificar dois arquivos de configuração do Solr:

* **schema.xml**
* **solrconfig.xml**

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 4.10.

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 5.x.

Os arquivos MLS padrão são armazenados no repositório AEM.

**Observação**: Embora os arquivos Solr estejam armazenados na pasta msrp/, eles também são para DSRP (não é necessário fazer alterações).

**Instruções** de download: Substitua `solrX` por `solr4` ou `solr5` conforme apropriado.

1. Usando CRXDE|Lite, localize:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Baixe no servidor local no qual o Solr está implantado.

   * Localize a propriedade do `jcr:content` nó `jcr:data` .
   * Selecione `view` para start do download.
   * Verifique se os arquivos foram salvos com os nomes e a codificação apropriados (UTF8).

1. Siga as instruções de instalação do modo independente ou do modo SolrCloud.

#### Modo SolrCloud - MLS padrão {#solrcloud-mode-standard-mls}

1. Instale e configure o Solr no modo SolrCloud.
1. Prepare uma nova configuração:

   1. Crie o new-config-dir*, como `solr-install-dir*/myconfig/`

   1. Copie o conteúdo do diretório de configuração Solr existente para *new-config-dir*

      * Para Solr4: cópia `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: cópia `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie o **schema.xml** e o **solrconfig.xml** baixados para o *new-config-dir* para substituir os arquivos existentes.


1. [Carregue a nova configuração](#upload-a-configuration-to-zookeeper) no ZooKeeper.
1. [Crie uma coleção](#create-a-collection) que especifique os parâmetros necessários, como o número de fragmentos, o número de réplicas e o nome da configuração.
1. Se o nome da configuração for *não *fornecido durante a criação da coleção, [vincule esta coleção](#link-a-collection-to-a-configuration-set) recém-criada com a configuração carregada no ZooKeeper.

1. Para MSRP, execute a Ferramenta [de reindexação](msrp.md#msrp-reindex-tool)MSRP, a menos que essa seja uma nova instalação.

#### Modo independente - MLS padrão {#standalone-mode-standard-mls}

1. Instale o Solr no modo independente.
1. Se estiver executando o Solr5, crie uma coleção1 (semelhante ao Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Faça backup de **schema.xml** e **solrconfig.xml** no diretório de configuração do Solr, como:

   * Para Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Criado para Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copie o **schema.xml** e o **solrconfig.xml** baixados para o mesmo diretório.

1. Reinicie o Solr.
1. Para MSRP, execute a Ferramenta [de reindexação](#msrpreindextool)MSRP, a menos que essa seja uma nova instalação.

### Instalação do Advanced MLS {#installing-advanced-mls}

Para a coleção SRP (MSRP ou DSRP) suportar MLS avançados, novos plug-ins Solr são necessários além de uma configuração personalizada de schema e Solr. Todos os itens necessários são empacotados em um arquivo zip baixável. Além disso, um script de instalação é incluído para uso quando o Solr é implantado no modo independente.

Para obter o pacote MLS avançado, consulte [AEM MLS](deploy-communities.md#aem-advanced-mls) avançado na seção de implantação da documentação.

Para começar a instalar o SolrCloud ou o modo independente:

* Baixe o arquivo zip AEM-SOLR-MLS para o servidor que hospeda o Solr.
* Desempacotar o arquivo.

#### Modo SolrCloud - MLS avançado {#solrcloud-mode-advanced-mls}

Instruções de instalação - observe as poucas diferenças para Solr4 e Solr5:

1. Instale e configure o Solr no modo SolrCloud.
1. Extraia o conteúdo do pacote MLS avançado para o disco. O conteúdo deve incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * **palavras-chave/** pasta
   * **perfis/** pasta
   * **extra-libs/** pasta

1. Prepare uma nova configuração:

   1. Criar um *novo diretório de configuração*

      * Como `solr-install-dir/myconfig/`
      * Criar subpastas `stopwords/` e `lang/`
   1. Copie o conteúdo do diretório de configuração do Solr existente para *new-config-dir*

      * Para Solr4: Copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: Copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie o **schema.xml** e o **solrconfig.xml** extraídos para *new-config-dir* para substituir os arquivos existentes.
   1. Para Solr5: Copiar `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` para `new-config-dir/lang/`
   1. Copie as **palavras-chave/** pasta extraídas para *new-config-dir* , resultando em `new-config-dir/stopwords/*.txt`



1. [Carregar a nova configuração](#upload-a-configuration-to-zookeeper) no ZooKeeper
1. Copiar os novos **perfis/** pasta ...

   * Para Solr4: Copiar para a pasta/recursos de cada nó
   * Para Solr5: Copie para cada pasta/servidor/recursos/ de instalação do Solr. Se todos os nós estiverem no mesmo diretório de instalação Solr, essa etapa será executada apenas uma vez.

1. Crie uma **lib/** pasta no diretório solr-home (contém solr.xml) de cada nó no SolrCloud. Copie os jars dos seguintes locais para a nova lib/ pasta em cada nó:

   * **extra-libs/** extraídos do pacote MLS avançado
   * *solr-install-dir/contrib/extração/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/speed/lib/*.jar
   * *solr-install-dir/dist/solr-speed*.jar
   * *solr-install-dir/contrib/análise-extras/lib/*.jar
   * *solr-install-dir/contrib/análise-extras/lucene-libs/*.jar

1. [Crie uma coleção](#create-a-collection) que especifique os parâmetros necessários, como o número de fragmentos, o número de réplicas e o nome da configuração.
1. Se o nome da configuração *não* tiver sido fornecido durante a criação da coleção, [vincule esta coleção](#link-a-collection-to-a-configuration-set) recém-criada à configuração carregada no ZooKeeper.

1. Para MSRP, execute a Ferramenta [de reindexação](#msrpreindextool)MSRP, a menos que essa seja uma nova instalação.

#### Modo independente - MLS avançado {#standalone-mode-advanced-mls}

Um script de instalação está incluído no pacote MLS avançado.

Depois que o conteúdo do pacote for extraído para o servidor que hospeda o servidor independente Solr, basta executar o script de instalação para instalar os recursos e os arquivos de configuração necessários.

* Instale o Solr no modo independente.
* Se estiver executando o Solr5, crie uma coleção1 (semelhante ao Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Execute o script de instalação: Install [-v 4|5] [-d solrhome] [-c collectionpath]onde:

   * -d lar

      Diretório de instalação do Solr

   * -c collectionpath

      Caminho da coleção no solar

   * --ajuda

      Imprimir opções de linha de comando

   * -v [4|5]

      Definir versão para solr

* Exemplo para Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Exemplo para Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* O script de instalação fará o backup de schema.xml e solrconfig.xml antes de instalar novas versões, anexando &quot;.oring&quot;

### Sobre o solrconfig.xml {#about-solrconfig-xml}

O arquivo **solrconfig.xml** controla o intervalo de confirmação automática e a visibilidade da pesquisa e exigirá testes e ajuste.

`<autoCommit>`: Por padrão, o intervalo AutoCommit, que é uma confirmação de hardware para um armazenamento estável, é definido como 15 segundos. O padrão da visibilidade da pesquisa é usar o índice de pré-confirmação.

Para alterar a pesquisa para usar um índice atualizado para refletir as alterações devidas à confirmação, altere o conteúdo `openSearcher` para verdadeiro.

`autoSoftCommit`: Uma confirmação &#39;soft&#39; garante que as alterações sejam visíveis (o índice é atualizado), mas não garante que as alterações sejam sincronizadas com o armazenamento estável (confirmação de hardware). O resultado é uma melhoria no desempenho. Por padrão, `autoSoftCommit` é desativado com o `maxTime` definido como -1.
