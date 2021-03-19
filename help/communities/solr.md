---
title: Configuração de Solr para SRP
seo-title: Configuração de Solr para SRP
description: Uma instalação do Apache Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (SRP) usando diferentes coleções
seo-description: Uma instalação do Apache Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (SRP) usando diferentes coleções
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 2%

---


# Configuração Solr para SRP {#solr-configuration-for-srp}

## Solr para AEM plataforma {#solr-for-aem-platform}

Uma instalação [Apache Solr](https://lucene.apache.org/solr/) pode ser compartilhada entre o [armazenamento de nó](../../help/sites-deploying/data-store-config.md) (Oak) e o [armazenamento comum](working-with-srp.md) (SRP) usando coleções diferentes.

Se as coleções Oak e SRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o [modo SolrCloud](#solrcloud-mode) fornece desempenho aprimorado em relação ao modo independente (uma configuração única e local Solr).

### Requisitos {#requirements}

Baixe e instale o Apache Solr:

* [Versão 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* A Solr requer o Java 1.7 ou superior
* Nenhum serviço é necessário
* Escolha dos modos de execução:

   * Modo autônomo
   * [Modo SolrCloud](#solrcloud-mode)  (recomendado para ambientes de produção)

* Escolha da pesquisa multilíngue (MLS)

   * [Instalação do MLS padrão](#installing-standard-mls)
   * [Instalação do MLS avançado](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

[](https://cwiki.apache.org/confluence/display/solr/SolrCloud) O SolrCloudmode é recomendado em ambientes de produção. Ao executar no modo SolrCloud, o SolrCloud deve ser instalado e configurado antes de instalar o MLS (Multilingual Search).

A recomendação é seguir as instruções da SolrCloud para instalar:

* 3 Nós do SolrCloud no mesmo servidor.
* Um ZooKeeper externo do Apache.

Também é recomendável configurar a JVM para ajustar o uso de memória e a coleta de lixo.

### Exemplo de configuração da JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuração do SolrCloud {#solrcloud-setup-commands}

Ao executar no modo SolrCloud, antes da instalação do MLS, é necessário o uso e o conhecimento dos seguintes comandos de configuração do SolrCloud.

#### 1. Carregue uma configuração no ZooKeeper {#upload-a-configuration-to-zookeeper}

Referência:
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Uso:
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Crie uma coleção {#create-a-collection}

Referência:
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Uso:
./bin/solr criar \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *porta*\
-s *número de fragmentos* \
-rf *número de réplicas*

#### 3. Vincule uma coleção a um conjunto de configurações {#link-a-collection-to-a-configuration-set}

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

A Pesquisa multilíngue (MLS) para AEM Communities foi criada para a plataforma Solr para fornecer uma pesquisa aprimorada em todos os idiomas compatíveis, incluindo o inglês.

O MLS para comunidades de AEM está disponível como MLS padrão ou MLS avançado. O MLS padrão inclui apenas configurações de Solr e exclui todos os plug-ins ou arquivos de recursos. O MLS avançado é a solução mais abrangente e inclui configurações de Solr, bem como plug-ins e recursos relacionados

O MLS padrão inclui aprimoramentos para pesquisa de conteúdo para os seguintes idiomas:

* Inglês: Aprimorado o remetente para tentar corresponder derivações de palavras.
* Japonês: Token japonês aprimorado para caracteres de meia largura.

O MLS avançado inclui aprimoramentos para pesquisa de conteúdo para os seguintes idiomas:

* Inglês: Substituição de uma máquina de lavar por um limmatizador.
* Alemão: Adição do decompositor.
* Francês: Adição do controle de iluminação.
* Chinês (Simplificado): Adição de um tokenizer mais inteligente.
* Vários idiomas: Adicionado um remetente, uma lista de palavras de parada e um normalizador.

No total, os 33 idiomas a seguir são compatíveis com o MLS avançado.

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

#### Comparação entre AEM 6.1 Pesquisa Solr, MLS Padrão e MLS Avançado {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Observação**: AEM 6.1 refere-se ao AEM 6.1 FP3 das Comunidades e anterior.

![compare-solr-mls](assets/compare-solr-mls.png)

### Instalar o MLS padrão {#installing-standard-mls}

Para a coleção SRP (MSRP ou DSRP), para ser compatível com o Standard Multilingual Search (MLS), é necessário modificar dois dos arquivos de configuração do Solr:

* **schema.xml**
* **solrconfig.xml**

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 4.10.

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 5.x.

Os arquivos MLS padrão são armazenados no repositório AEM.

**Observação**: Embora os arquivos Solr sejam armazenados na pasta msrp/ , eles também são para DSRP (nenhuma alteração necessária).

**Instruções** de download: Substitua  `solrX` por  `solr4` ou  `solr5` conforme apropriado.

1. Usando o CRXDE|Lite, localize:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Baixe no servidor local em que o Solr é implantado.

   * Localize a propriedade `jcr:content` do nó `jcr:data`.
   * Selecione `view` para iniciar o download.
   * Verifique se os arquivos foram salvos com os nomes e a codificação apropriados (UTF8).

1. Siga as instruções de instalação para o modo independente ou o modo SolrCloud.

#### Modo SolrCloud - MLS padrão {#solrcloud-mode-standard-mls}

1. Instale e configure o Solr no modo SolrCloud.
1. Prepare uma nova configuração:

   1. Crie o new-config-dir* como `solr-install-dir*/myconfig/`

   1. Copie o conteúdo do diretório de configuração Solr existente para *new-config-dir*

      * Para Solr4: copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie o **schema.xml** e **solrconfig.xml** baixados para *new-config-dir* para substituir arquivos existentes.


1. [Carregue a nova ](#upload-a-configuration-to-zookeeper) configuração no ZooKeeper.
1. [Crie uma ](#create-a-collection) coleção especificando os parâmetros necessários, como número de fragmentos, número de réplicas e nome da configuração.
1. Se o nome da configuração foi *não *fornecido durante a criação da coleção, [vincule essa coleção recém-criada](#link-a-collection-to-a-configuration-set) com a configuração carregada no ZooKeeper.

1. Para MSRP, execute [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), a menos que esta seja uma nova instalação.

#### Modo independente - MLS padrão {#standalone-mode-standard-mls}

1. Instale o Solr no modo independente.
1. Se estiver executando o Solr5, crie uma coleção1 (semelhante a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Faça backup de **schema.xml** e **solrconfig.xml** no diretório de configuração Solr, como:

   * Para Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Criado para Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copie o **schema.xml** e **solrconfig.xml** baixados para o mesmo diretório.

1. Reinicie o Solr.
1. Para MSRP, execute [MSRP Reindex Tool](#msrpreindextool), a menos que esta seja uma nova instalação.

### Instalar o MLS avançado {#installing-advanced-mls}

Para que a coleção SRP (MSRP ou DSRP) ofereça suporte a MLS avançado, são necessários novos plug-ins Solr além de um esquema personalizado e uma configuração Solr. Todos os itens necessários são empacotados em um arquivo zip que pode ser baixado. Além disso, um script de instalação é incluído para uso quando Solr é implantado no modo independente.

Para obter o pacote MLS avançado, consulte [AEM MLS avançado](deploy-communities.md#aem-advanced-mls) na seção de implantação da documentação.

Para começar a instalar o SolrCloud ou o modo independente:

* Baixe o arquivo zip AEM-SOLR-MLS para a Solr de hospedagem de servidor.
* Descompacte o arquivo.

#### Modo SolrCloud - MLS avançado {#solrcloud-mode-advanced-mls}

Instruções de instalação - observe as poucas diferenças para Solr4 e Solr5:

1. Instale e configure o Solr no modo SolrCloud.
1. Extraia o conteúdo do pacote MLS avançado para o disco. O conteúdo deve incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/** folder
   * **perfis/** pasta
   * **extra-libs/** folder

1. Prepare uma nova configuração:

   1. Criar um *new-config-dir*

      * Como `solr-install-dir/myconfig/`
      * Criar subpastas `stopwords/` e `lang/`
   1. Copie o conteúdo do diretório de configuração Solr existente para *new-config-dir*

      * Para Solr4: Copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: Copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie o **schema.xml** e **solrconfig.xml** extraído para *new-config-dir* para substituir arquivos existentes.
   1. Para Solr5: Copiar `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` para `new-config-dir/lang/`
   1. Copie a pasta **stopwords/** extraída para *new-config-dir* resultando em `new-config-dir/stopwords/*.txt`



1. [Carregar a nova ](#upload-a-configuration-to-zookeeper) configuração no ZooKeeper
1. Copie a nova pasta **profiles/** ...

   * Para Solr4: Copiar para a pasta/recursos de cada nó
   * Para Solr5: Copie para cada pasta de servidor/recursos/ da instalação Solr. Se todos os nós estiverem no mesmo diretório de instalação Solr, essa etapa será executada apenas uma vez.

1. Crie uma pasta **lib/** no diretório solr-home (contém solr.xml) de cada nó no SolrCloud. Copie jars dos seguintes locais para a nova biblioteca/ pasta em cada nó:

   * **extra-libs/** extraído do pacote MLS avançado
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [Crie uma ](#create-a-collection) coleção especificando os parâmetros necessários, como número de fragmentos, número de réplicas e nome da configuração.
1. Se o nome da configuração for *not* fornecido durante a criação da coleção, [vincule esta coleção recém-criada](#link-a-collection-to-a-configuration-set) com a configuração carregada no ZooKeeper.

1. Para MSRP, execute [MSRP Reindex Tool](#msrpreindextool), a menos que esta seja uma nova instalação.

#### Modo independente - MLS avançado {#standalone-mode-advanced-mls}

Um script de instalação é incluído no pacote MLS avançado.

Depois que o conteúdo do pacote for extraído para o servidor que hospeda o servidor Solr independente, basta executar o script de instalação para instalar os recursos e os arquivos de configuração necessários.

* Instale o Solr no modo independente.
* Se estiver executando o Solr5, crie uma coleção1 (semelhante a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Execute o script de instalação: Instalar [-v 4|5] [-d solrhome] [-c collectionpath]
em que:

   * -d solrhome

      Diretório de instalação do Solr

   * -c collectionpath

      Caminho da coleção em solr

   * --ajuda

      Imprimir opções de linha de comando

   * -v [4|5]

      Definir versão para solr

* Exemplo para Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Exemplo para Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* O script de instalação fará o backup do schema.xml e do solrconfig.xml antes de instalar novas versões, anexando &quot;.oring&quot;

### Sobre solrconfig.xml {#about-solrconfig-xml}

O arquivo **solrconfig.xml** controla o intervalo de confirmação automática e a visibilidade da pesquisa e exigirá testes e ajuste.

`<autoCommit>`: Por padrão, o intervalo AutoCommit, que é um compromisso rígido com o armazenamento estável, é definido como 15 segundos. O padrão da visibilidade da pesquisa é usar o índice de pré-confirmação.

Para alterar a pesquisa para usar um índice atualizado para refletir as alterações devido à confirmação, altere o `openSearcher` contido para verdadeiro.

`autoSoftCommit`: Uma confirmação &quot;suave&quot; garante que as alterações sejam visíveis (o índice é atualizado), mas não garante que as alterações sejam sincronizadas com o armazenamento estável (confirmação rígida). O resultado é uma melhoria no desempenho. Por padrão, `autoSoftCommit` é desabilitado com o conteúdo `maxTime` definido como -1.
