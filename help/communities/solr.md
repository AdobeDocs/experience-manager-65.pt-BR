---
title: Configuração Solr para SRP
seo-title: Solr Configuration for SRP
description: Uma instalação do Apache Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (SRP) usando coleções diferentes
seo-description: An Apache Solr installation may be shared between the node store (Oak) and common store (SRP) by using different collections
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: ce6d24e53a27b64a5d0a9db2e4b6672bd77cf9ec
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 2%

---

# Configuração Solr para SRP {#solr-configuration-for-srp}

## Solr para plataforma AEM {#solr-for-aem-platform}

Um [Apache Solr](https://solr.apache.org/) a instalação pode ser compartilhada entre o [armazenamento de nós](../../help/sites-deploying/data-store-config.md) (Oak) e [armazenamento comum](working-with-srp.md) (SRP) usando diferentes coleções.

Se as coleções Oak e SRP forem usadas intensamente, um segundo Solr pode ser instalado por motivos de desempenho.

Para ambientes de produção, [Modo SolrCloud](#solrcloud-mode) O fornece desempenho aprimorado em relação ao modo independente (uma configuração Solr única e local).

### Requisitos {#requirements}

Baixe e instale o Apache Solr:

* [Versão 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr requer Java™ 1.7 ou superior
* Nenhum serviço é necessário
* Opção de modos de execução:

   * Modo independente
   * [Modo SolrCloud](#solrcloud-mode) (recomendado para ambientes de produção)

* Opção de pesquisa multilíngue (MLS)

   * [Instalando o MLS Padrão](#installing-standard-mls)
   * [Instalando o MLS Avançado](#installing-advanced-mls)

## Modo SolrCloud {#solrcloud-mode}

[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) O modo de é recomendado para ambientes de produção. Ao executar no modo SolrCloud, o SolrCloud deve ser instalado e configurado antes de instalar a Pesquisa multilíngue (MLS).

A recomendação é seguir as instruções da SolrCloud para instalar:

* 3 nós SolrCloud no mesmo servidor.
* Um ZooKeeper externo do Apache.

Também é recomendável configurar a JVM para ajustar o uso de memória e a coleta de lixo.

### Exemplo de configuração de JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Comandos de configuração do SolrCloud {#solrcloud-setup-commands}

Ao executar no modo SolrCloud, antes da instalação do MLS, é necessário usar e conhecer os seguintes comandos de configuração do SolrCloud.

#### 1. Fazer upload de uma configuração no ZooKeeper {#upload-a-configuration-to-zookeeper}

Referência:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Uso: sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *servidor:porta* \
-confname *myconfig-name *\
- solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Criar uma coleção {#create-a-collection}

Referência:
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

Uso:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *porta*\
-s *number-of-shards* \
-rf *número de réplicas*

#### 3. Vincular uma coleção a um conjunto de configurações {#link-a-collection-to-a-configuration-set}

Vincular uma coleção a uma configuração já carregada no ZooKeeper.

Referência:
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

Uso: sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *servidor:porta* \
-coleção *mycollection-name* \
-confname *myconfig-name*

### Comparação de MLS Padrão e Avançado {#comparison-of-standard-and-advanced-mls}

A Pesquisa multilíngue (MLS) para o AEM Communities foi criada para a plataforma Solr, a fim de fornecer pesquisa aprimorada em todos os idiomas compatíveis, incluindo inglês.

O MLS para AEM Communities está disponível como MLS Padrão ou MLS Avançado. O MLS padrão inclui apenas as definições de configuração Solr e exclui todos os plug-ins ou arquivos de recurso. O MLS avançado é a solução mais abrangente e inclui definições de configuração do Solr, bem como plug-ins e recursos relacionados

O MLS padrão inclui aprimoramentos para a pesquisa de conteúdo nos seguintes idiomas:

* English: Improved stemmer for attempt to match word derivations. (Inglês: Melhoria do lemmer para tentar combinar derivações de palavras.)
* Japonês: aprimoramento da geração de tokens em japonês para caracteres de meia largura.

O MLS avançado inclui aprimoramentos na pesquisa de conteúdo para os seguintes idiomas:

* Inglês: Replacement stemmer with lemmatizer.
* Alemão: adição do decompounder.
* Francês: Adição de controle de elisão.
* Chinês (simplificado): adição de um tokenizer mais inteligente.
* Vários idiomas: Adição de um lematizador, uma lista de palavras de interrupção e um normalizador.

Ao todo, os 33 idiomas a seguir são suportados no MLS avançado.

| Árabe | Alemão | Norueguês |
|---|---|---|
| Búlgaro | Grego | Polonês |
| Chinês (simplificado) | Crioulo haitiano | Português |
| Chinês (Tradicional) | Hebraico | Romeno |
| Tcheco | Húngaro | Russo |
| Dinamarquês | Indonésio | Eslovaco |
| Holandês | Italiano | Esloveno |
| Inglês | Japonês | Espanhol |
| Estoniano | Coreano | Sueco |
| Finlandês | Letão | Tailandês |
| Francês | Lituano | Turco |

#### Comparação entre pesquisa AEM 6.1 Solr, MLS padrão e MLS avançado {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Nota**: AEM 6.1 refere-se ao AEM 6.1 Communities FP3 e anterior.

![compare-solr-mls](assets/compare-solr-mls.png)

### Instalando o MLS Padrão {#installing-standard-mls}

Para a coleção SRP (MSRP ou DSRP), para oferecer suporte à Pesquisa Multilíngue Padrão (MLS), é necessário modificar dois dos arquivos de configuração do Solr:

* **schema.xml**
* **solrconfig.xml**

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 4.10.

Arquivos MLS padrão (schema.xml, solrconfig.xml) para Solr 5.x.

Os arquivos MLS padrão são armazenados no repositório AEM.

**Nota**: Embora os arquivos Solr sejam armazenados na pasta msrp/, eles também são para DSRP (nenhuma alteração é necessária).

**Instruções de download**: Substituir `solrX` com `solr4` ou `solr5` conforme adequado.

1. Usando o CRXDE|Lite, localize:

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Baixar para o servidor local no qual o Solr está implantado.

   * Localize o `jcr:content` do nó `jcr:data` propriedade.
   * Para iniciar o download, selecione `view`.
   * Verifique se os arquivos foram salvos com os nomes e a codificação apropriados (UTF8).

1. Siga as instruções de instalação para o modo independente ou SolrCloud.

#### Modo SolrCloud - MLS Padrão {#solrcloud-mode-standard-mls}

1. Instalar e configurar o Solr no modo SolrCloud.
1. Preparar uma nova configuração:

   1. Crie new-config-dir* como `solr-install-dir*/myconfig/`

   1. Copiar o conteúdo do diretório de configuração Solr existente para *new-config-dir*

      * Para Solr4: copy `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: copy `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copie o baixado **schema.xml** e **solrconfig.xml** para *new-config-dir* para substituir arquivos existentes.


1. [Fazer upload da nova configuração](#upload-a-configuration-to-zookeeper) para o ZooKeeper.
1. [Criar uma coleção](#create-a-collection) especificar os parâmetros necessários, como número de fragmentos, número de réplicas e nome da configuração.
1. Se o nome da configuração *não *foi fornecido durante a criação da coleção, [vincular esta coleção recém-criada](#link-a-collection-to-a-configuration-set) com a configuração carregada no ZooKeeper.

1. Para MSRP, execute [Ferramenta Reindexação MSRP](msrp.md#msrp-reindex-tool), a menos que essa instalação seja nova.

#### Modo Independente - MLS Padrão {#standalone-mode-standard-mls}

1. Instale o Solr no modo independente.
1. Se estiver executando Solr5, crie uma coleção1 (semelhante a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Backup **schema.xml** e **solrconfig.xml** no diretório de configuração Solr, como:

   * Para Solr4: `solr-install-dir/example/solr/collection1/conf/`
   * Criado para Solr5: `solr-install-dir/server/solr/collection1/conf/`

1. Copie o baixado **schema.xml** e **solrconfig.xml** nesse mesmo diretório.

1. Reiniciar Solr.
1. Para MSRP, execute [Ferramenta Reindexação MSRP](#msrpreindextool), a menos que essa instalação seja nova.

### Instalando o MLS Avançado {#installing-advanced-mls}

Para que a coleção SRP (MSRP ou DSRP) seja compatível com MLS avançado, novos plug-ins Solr são necessários, além de um esquema personalizado e uma configuração Solr. Todos os itens necessários são empacotados em um arquivo zip para download. Além disso, um script de instalação é incluído para uso quando o Solr é implantado no modo independente.

Para obter o pacote MLS Avançado, consulte [MLS avançado para AEM](deploy-communities.md#aem-advanced-mls) na seção de implantação da documentação.

Para começar a instalação do SolrCloud ou do modo independente:

* Faça o download do arquivo zip AEM-SOLR-MLS para o servidor que hospeda o Solr.
* Descompacte o arquivo.

#### Modo SolrCloud - MLS Avançado {#solrcloud-mode-advanced-mls}

Instruções de instalação - observe as poucas diferenças para Solr4 e Solr5:

1. Instalar e configurar o Solr no modo SolrCloud.
1. Extraia o conteúdo do pacote MLS Avançado para o disco. O conteúdo deve incluir:

   * **schema.xml**
   * **solrconfig.xml**
   * **palavras irrelevantes/** pasta
   * **profiles/** pasta
   * **extra-libs/** pasta

1. Preparar uma nova configuração:

   1. Criar um *new-config-dir*

      * Tais como `solr-install-dir/myconfig/`
      * Criar subpastas `stopwords/` e `lang/`
   1. Copiar o conteúdo do diretório de configuração Solr existente para *new-config-dir*

      * Para Solr4: Copiar `solr-install-dir/example/solr/collection1/conf/`
      * Para Solr5: Copiar `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copiar o extraído **schema.xml** e **solrconfig.xml** para *new-config-dir* para substituir arquivos existentes.
   1. Para Solr5: Copiar `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` para `new-config-dir/lang/`
   1. Copiar o extraído **palavras irrelevantes/** pasta para *new-config-dir* resultando em `new-config-dir/stopwords/*.txt`



1. [Fazer upload da nova configuração](#upload-a-configuration-to-zookeeper) para o ZooKeeper
1. Copie o novo **profiles/** pasta ...

   * Para Solr4: Copiar para a pasta/recursos de cada nó
   * Para Solr5: Copiar para a pasta/recursos/servidor de cada instalação Solr. Se todos os nós estiverem no mesmo diretório de instalação Solr, essa etapa será executada apenas uma vez.

1. Criar um **lib/** pasta no diretório solr-home (contém solr.xml) de cada nó na SolrCloud. Copie os jars dos seguintes locais para a nova biblioteca/pasta em cada nó:

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

1. [Criar uma coleção](#create-a-collection) especificar os parâmetros necessários, como número de fragmentos, número de réplicas e nome da configuração.
1. Se o nome da configuração foi *não* fornecido durante a criação da coleção, [vincular esta coleção recém-criada](#link-a-collection-to-a-configuration-set) com a configuração carregada no ZooKeeper.

1. Para MSRP, execute [Ferramenta Reindexação MSRP](#msrpreindextool), a menos que essa instalação seja nova.

#### Modo Independente - MLS Avançado {#standalone-mode-advanced-mls}

Um script de instalação está incluído no pacote MLS Avançado.

Depois que o conteúdo do pacote for extraído para o servidor que hospeda o servidor Solr independente, execute o script de instalação para instalar os recursos necessários e os arquivos de configuração.

* Instale o Solr no modo independente.
* Se estiver executando Solr5, crie uma coleção1 (semelhante a Solr4):

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Execute o script de instalação: Instalar [-v 4|5] [- d solrhome] [-c caminho de coleção]
em que:

   * - d solrhome

      Diretório de instalação Solr

   * -c caminho de coleção

      Caminho da coleção em solr

   * --ajuda

      Imprimir opções da linha de comando

   * -v [4|5]

      Definir versão para solr

* Exemplo para Solr 4.10.4:

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Exemplo para Solr 5.4.0:

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Nota**:

* O script de instalação faz backup de schema.xml e solrconfig.xml antes de instalar novas versões anexando &quot;.orig&quot;

### Sobre solrconfig.xml {#about-solrconfig-xml}

A variável **solrconfig.xml** arquivo controla o intervalo de confirmação automática e a visibilidade da pesquisa e requer testes e ajuste.

`<autoCommit>`: por padrão, o intervalo de AutoCommit, que é uma confirmação forçada para armazenamento estável, é definido como 15 segundos. A visibilidade da pesquisa é padronizada como usar o índice pré-confirmação.

Para alterar a pesquisa para usar um índice atualizado para refletir as alterações causadas pela confirmação, altere o `openSearcher` para verdadeiro.

`autoSoftCommit`: uma confirmação &#39;suave&#39; garante que as alterações estejam visíveis (o índice é atualizado), mas não garante que as alterações sejam sincronizadas com o armazenamento estável (confirmação permanente). O resultado é uma melhoria no desempenho. Por padrão, `autoSoftCommit` está desabilitado com o contido `maxTime` defina como -1.
