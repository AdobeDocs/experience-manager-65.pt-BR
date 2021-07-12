---
title: MSRP - Provedor de recursos de armazenamento MongoDB
seo-title: MSRP - Provedor de recursos de armazenamento MongoDB
description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
seo-description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---

# MSRP - Provedor de recursos de armazenamento MongoDB {#msrp-mongodb-storage-resource-provider}

## Sobre o MSRP {#about-msrp}

Quando o AEM Communities é configurado para usar o MSRP como armazenamento comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das Opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Requisitos {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versão 2.6 ou superior
   * Não é necessário configurar mongos ou compartilhamento
   * Recomenda-se o uso de um [conjunto de réplicas](#mongoreplicaset)
   * Pode ser executado no mesmo host que AEM ou executado remotamente

* [Apache Solr](https://lucene.apache.org/solr/):

   * Versão Solr 7.0
   * A Solr requer o Java 1.7 ou superior
   * Nenhum serviço é necessário
   * Escolha dos modos de execução:
      * Modo autônomo
      * [Modo SolrCloud](solr.md#solrcloud-mode)  (recomendado para ambientes de produção)
   * Escolha da pesquisa multilíngue (MLS):
      * [Instalação do MLS padrão](solr.md#installing-standard-mls)
      * [Instalação do MLS avançado](solr.md#installing-advanced-mls)

## Configuração do MongoDB {#mongodb-configuration}

### Selecionar MSRP {#select-msrp}

O [console Configuração de Armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação do SRP usar.

Na autora, para acessar o console Configuração de armazenamento:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de armazenamento]**.

![msrp](assets/msrp.png)

* Selecione **[!UICONTROL Provedor de Recursos de Armazenamento do MongoDB (MSRP)]**
* **[!UICONTROL Configuração do mongoDB]**

   * **[!UICONTROL URI do mongoDB]**

      *padrão*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de dados do mongoDB]**

      *padrão*: comunidades

   * **[!UICONTROL Coleção de UGC do mongoDB]**

      *padrão*: conteúdo

   * **[!UICONTROL Coleção de anexos do mongoDB]**

      *padrão*: anexos

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host do Zookeeper**

      Ao executar no [modo SolrCloud](solr.md#solrcloud-mode) com um ZooKeeper externo, defina esse valor para `HOST:PORT` para o ZooKeeper, como *my.server.com:2181*

      Para um Conjunto ZooKeeper, insira valores `HOST:PORT` separados por vírgula, como *host1:2181,host2:2181*

      Deixe em branco se estiver executando Solr no modo independente usando o ZooKeeper interno.
      *Padrão*:  *&lt;blank>*

      * **[!UICONTROL URL]**
URLTo URL usado para se comunicar com Solr no modo independente.
Deixe em branco se estiver executando no modo SolrCloud.

         *Padrão*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr]**
CollectionO nome da coleção Solr.

         *Padrão*: collection1

* Selecione **[!UICONTROL Enviar]**

>[!NOTE]
>
>O banco de dados mongoDB, que padroniza o nome `communities`, não deve ser definido para o nome de um banco de dados que está sendo usado para [armazenamentos de nó ou dados (binários) armazenamentos](../../help/sites-deploying/data-store-config.md). Consulte também [Elementos de Armazenamento no AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de Réplicas do MongoDB {#mongodb-replica-set}

Para o ambiente de produção, é altamente recomendável configurar um conjunto de réplicas, um cluster de servidores MongoDB que implementa a replicação primária secundária e o failover automatizado.

Para saber mais sobre conjuntos de réplicas, visite a documentação [Replication](https://docs.mongodb.org/manual/replication/) do MongoDB.

Para trabalhar com conjuntos de réplicas e aprender a definir conexões entre aplicativos e instâncias MongoDB, visite a documentação [Connection String URI Format](https://docs.mongodb.org/manual/reference/connection-string/) do MongoDB.

#### Exemplo de Url para Conexão com um Conjunto de Réplicas  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (MSRP) usando diferentes coleções.

Se as coleções Oak e MSRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o [modo SolrCloud](solr.md#solrcloud-mode) fornece desempenho aprimorado em relação ao modo independente (uma configuração única e local Solr).

Para obter detalhes de configuração, consulte [Configuração Solr para SRP](solr.md).

### Atualização {#upgrading}

Se estiver atualizando de uma versão anterior configurada com o MSRP, será necessário:

1. Execute o [upgrade para AEM Communities](upgrade.md)
1. Instalar novos arquivos de configuração do Solr
   * Para [MLS padrão](solr.md#installing-standard-mls)
   * Para [MLS avançado](solr.md#installing-advanced-mls)
1. Reindexar MSRP
Consulte a seção [Ferramenta MSRP Reindex](#msrp-reindex-tool)

## Publicar a configuração {#publishing-the-configuration}

O MSRP deve ser identificado como o armazenamento comum em todas as instâncias de criação e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação, faça logon na instância do autor e siga as etapas:

* Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
* Selecione **[!UICONTROL Ativar árvore]**
* **[!UICONTROL Caminho de início]**:
   * Navegue até `/etc/socialconfig/srpc/`
* Selecione **[!UICONTROL Ativar]**

## Gerenciar dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, normalmente inseridos no ambiente de publicação, visite

* [Sincronização de usuários](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Ferramenta de reindexação MSRP {#msrp-reindex-tool}

Há um terminal HTTP para reindexar o Solr para MSRP ao instalar novos arquivos de configuração ou reparar um índice Solr danificado.

Com essa ferramenta, o MongoDB é a fonte de *true* para MSRP; os backups só precisam ser feitos do MongoDB.

Toda a árvore UGC pode ser reindexada ou apenas uma subárvore específica, conforme especificado pelo parâmetro *path *data .

Essa ferramenta pode ser executada a partir da linha de comando usando cURL ou qualquer outra ferramenta HTTP.

Ao reindexar, há uma compensação entre a memória e o desempenho controlado pelo parâmetro *batchSize *data , que especifica quantos registros UGC são reindexados por lote.

Um padrão razoável é 5000:

* Se a memória for um problema, especifique um número menor
* Se a velocidade for um problema, especifique um número maior para aumentar a velocidade

### Execução da ferramenta de reindexação MSRP usando o comando cURL {#running-msrp-reindex-tool-using-curl-command}

O seguinte comando cURL mostra o que é necessário para uma solicitação HTTP reindexar o UGC armazenado no MSRP.

O formato básico é:

cURL -u *sign* -d *data* *reindex-url*

*sign*  = administration-id:password Por exemplo: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size*  = quantas entradas UGC devem ser reindexadas por operação 
`/content/usergenerated/asi/mongo/`

*path*  = o local raiz da árvore do UGC para reindexar

* Para reindexar todos os UGC, especifique o valor da propriedade `asipath`de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar o índice a algum UGC, especifique uma subárvore de `asipath`

*reindex-url*  = o endpoint para reindexação do SRP 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se você estiver [reindexando DSRP Solr](dsrp.md), o URL será **/services/social/datastore/rdb/reindex**

### Exemplo de reindexação MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Como demonstrar o MSRP {#how-to-demo-msrp}

Para configurar o MSRP para um ambiente de demonstração ou desenvolvimento, consulte [Como configurar o MongoDB para Demo](demo-mongo.md).

## Resolução de problemas {#troubleshooting}

### UGC não visível no MongoDB {#ugc-not-visible-in-mongodb}

Verifique se o MSRP foi configurado para ser o provedor padrão, verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é o JSRP.

Em todas as instâncias de criação e publicação AEM, revisite o [console de Configuração de Armazenamento](srp-config.md) ou verifique o repositório AEM:

* No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades da configuração padrão deverão definir o MSRP para ser o provedor padrão.

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se estiver atualizando de um site AEM Communities 6.0 existente, qualquer UGC pré-existente deverá ser convertido para estar em conformidade com a estrutura necessária para a API [SRP](srp.md) após a atualização para o AEM Communities 6.3.

Há uma ferramenta de código aberto disponível no GitHub para essa finalidade:

* [Ferramenta de migração UGC da AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

A ferramenta de migração pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais AEM para importação no AEM Communities 6.1 ou posterior.

### Erro - provider_id de campo indefinido {#error-undefined-field-provider-id}

Se o seguinte erro for visto nos logs, isso indica que o arquivo de esquema Solr não está configurado corretamente.

#### JsonMappingException: campo indefinido provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver o erro, ao seguir as instruções para [Instalar o MLS padrão](solr.md#installing-standard-mls), verifique se:

* Os arquivos de configuração XML foram copiados para o local correto do Solr.
* A Solr foi reiniciada depois que os novos arquivos de configuração substituíram os existentes.

### Falha na Conexão Segura ao MongoDB {#secure-connection-to-mongodb-fails}

Se uma tentativa de fazer uma conexão segura com o servidor MongoDB falhar devido a uma definição de classe ausente, é necessário atualizar o pacote de driver MongoDB, `mongo-java-driver`, disponível no repositório Maven público.

1. Baixe o driver de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versão 2.13.2 ou posterior).
1. Copie o pacote na pasta &quot;crx-quickstart/install&quot; para uma instância do AEM.
1. Reinicie a instância de AEM.

## Recursos {#resources}

* [AEM com MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentação do MongoDB](https://docs.mongodb.org/)
