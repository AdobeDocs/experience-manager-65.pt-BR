---
title: MSRP - Provedor de recursos do Armazenamento MongoDB
seo-title: MSRP - Provedor de recursos do Armazenamento MongoDB
description: Configurar AEM Communities para usar um banco de dados relacional como sua loja comum
seo-description: Configurar AEM Communities para usar um banco de dados relacional como sua loja comum
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: 6a9f273c6e9eb822e2d4765700361a205019b84c
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 1%

---


# MSRP - Provedor de recursos do Armazenamento MongoDB {#msrp-mongodb-storage-resource-provider}

## Sobre o MSRP {#about-msrp}

Quando o AEM Communities está configurado para usar o MSRP como sua loja comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das opções](working-with-srp.md#characteristics-of-srp-options) de SRP e das topologias [](topologies.md)recomendadas.

## Requisitos {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versão 2.6 ou superior
   * Não há necessidade de configurar mongos ou compartilhamento
   * Recomendar o uso de um conjunto de [réplicas](#mongoreplicaset)
   * Pode ser executado no mesmo host que AEM ou executado remotamente

* [Apache Solr](https://lucene.apache.org/solr/):

   * Versão 4.10 ou 5
   * A Solr requer Java 1.7 ou superior
   * Nenhum serviço é necessário
   * Escolha dos modos de execução:
      * Modo autônomo
      * [Modo](solr.md#solrcloud-mode) SolrCloud (recomendado para ambientes de produção)
   * Escolha da pesquisa multilíngue (MLS):
      * [Instalação do MLS padrão](solr.md#installing-standard-mls)
      * [Instalação do Advanced MLS](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Selecionar MSRP {#select-msrp}

O console [Configuração do](srp-config.md) Armazenamento permite a seleção da configuração padrão do armazenamento, que identifica qual implementação do SRP usar.

Em autor, para acessar o console Configuração do Armazenamento:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > Configuração **[!UICONTROL do]** Armazenamento.

![chlimage_1-28](assets/chlimage_1-28.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
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

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host do Zookeeper **

      Ao executar no modo [](solr.md#solrcloud-mode) SolrCloud com um ZooKeeper externo, defina esse valor como `HOST:PORT` para o ZooKeeper, como *my.server.com:2181*

      Para um conjunto ZooKeeper, insira `HOST:PORT` valores separados por vírgulas, como *host1:2181,host2:2181*

      Deixe em branco se estiver executando Solr no modo independente usando o ZooKeeper interno.
      *Padrão*: *&lt;blank>*

      * **[!UICONTROL URL]**SolrO URL usado para se comunicar com o Solr no modo independente.
Deixe em branco se estiver sendo executado no modo SolrCloud.

         *Padrão*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Coleção]**SolrO nome da coleção Solr.

         *Padrão*: coleção1

* Selecione **[!UICONTROL Enviar]**

>[!NOTE]
>
>O banco de dados mongoDB, que padroniza o nome `communities`, não deve ser definido como o nome de um banco de dados que está sendo usado para armazenamentos de [nó ou armazenamentos](../../help/sites-deploying/data-store-config.md)de dados (binários). Consulte também Elementos para [Armazenamentos no AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).


### Conjunto de Réplicas MongoDB {#mongodb-replica-set}

Para o ambiente de produção, é altamente recomendável configurar um conjunto de réplicas, um cluster de servidores MongoDB que implementa a replicação primária-secundária e o failover automatizado.

Para saber mais sobre conjuntos de réplicas, visite a documentação de [Replicação](https://docs.mongodb.org/manual/replication/) do MongoDB.

Para trabalhar com conjuntos de réplicas e aprender a definir conexões entre aplicativos e instâncias MongoDB, visite a documentação do Formato [URI da String de](https://docs.mongodb.org/manual/reference/connection-string/) Conexão do MongoDB.

#### URL de exemplo para conexão com um conjunto de réplicas  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre a loja de nós (Oak) e a loja comum (MSRP) usando coleções diferentes.

Se as coleções Oak e MSRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o modo [](solr.md#solrcloud-mode) SolrCloud fornece um desempenho aprimorado em relação ao modo independente (uma configuração única local de Solr).

Para obter detalhes sobre a configuração, consulte Configuração [Solr para SRP](solr.md).

### Atualização {#upgrading}

Se a atualização de uma versão anterior configurada com MSRP for feita, será necessário:

1. Execute a [atualização para AEM Communities](upgrade.md)
1. Instalar novos arquivos de configuração do Solr
   * Para MLS [padrão](solr.md#installing-standard-mls)
   * Para MLS [avançado](solr.md#installing-advanced-mls)
1. Reindexar a seção MSRPSee Ferramenta de reindexação [MSRP](#msrp-reindex-tool)

## Publicar a configuração {#publishing-the-configuration}

O MSRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para tornar a configuração idêntica disponível no ambiente publish, faça logon na instância do autor e siga as etapas a seguir:

* Navegue do menu principal até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
* Selecionar **[!UICONTROL Ativar árvore]**
* **[!UICONTROL Caminho de início]**:
   * Navegue até `/etc/socialconfig/srpc/`
* Selecionar **[!UICONTROL Ativar]**

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, perfis *de* usuários e grupos *de* usuários, normalmente inseridos no ambiente de publicação, visite

* [Sincronização do usuário](sync.md)
* [Gerenciamento de usuários e grupos de usuários](users.md)

## Ferramenta MSRP Reindex {#msrp-reindex-tool}

Há um terminal HTTP para reindexar o Solr for MSRP ao instalar novos arquivos de configuração ou reparar um índice de Solr danificado.

Com esta ferramenta, o MongoDB é a fonte da *verdade* para o MSRP; os backups só precisam ser feitos do MongoDB.

Toda a árvore UGC pode ser indexada novamente, ou apenas uma subárvore específica, conforme especificado pelo parâmetro *path *data.

Essa ferramenta pode ser executada a partir da linha de comando usando cURL ou qualquer outra ferramenta HTTP.

Ao reindexar, há uma compensação entre a memória e o desempenho controlado pelo parâmetro de dados *batchSize *, que especifica quantos registros UGC são indexados por lote.

Um padrão razoável é 5000:

* Se a memória for um problema, especifique um número menor
* Se a velocidade for um problema, especifique um número maior para aumentar a velocidade

### Execução da ferramenta de reindexação MSRP usando o comando cURL {#running-msrp-reindex-tool-using-curl-command}

O seguinte comando cURL mostra o que é necessário para uma solicitação HTTP reindexar o UGC armazenado no MSRP.

O formato básico é:

cURL -u *logon* -d *data* *reindex-url*

*sign* = administrative-id:passwordPor exemplo: admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = quantas entradas UGC devem ser reindexadas por operação
`/content/usergenerated/asi/mongo/`

*caminho* = o local raiz da árvore do UGC a ser reindexada

* Para reindexar todo o UGC, especifique o valor da `asipath`propriedade de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar o índice a algum UGC, especifique uma subárvore de `asipath`

*reindex-url* = o endpoint para reindexação de SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se você estiver [reindexando o DSRP Solr](dsrp.md), o URL será **/services/social/datastore/rdb/reindex**


### Exemplo de reindexação de MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Como demonstrar o MSRP {#how-to-demo-msrp}

Para configurar o MSRP para um ambiente de demonstração ou desenvolvimento, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

## Resolução de Problemas{#troubleshooting}

### UGC não visível no MongoDB {#ugc-not-visible-in-mongodb}

Verifique se o MSRP foi configurado para ser o provedor padrão ao verificar a configuração da opção armazenamento. Por padrão, o provedor de recursos do armazenamento é JSRP.

Em todas as instâncias de autor e publicação AEM, reveja o console [Configuração do](srp-config.md) Armazenamento ou verifique o repositório AEM:

* No JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , significa que o provedor do armazenamento é JSRP.
   * Se o nó srpc existir e contiver a configuração [](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)padrão do nó, as propriedades da configuração padrão deverão definir o MSRP como o provedor padrão.

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se você estiver atualizando de um site existente do AEM Communities 6.0, qualquer UGC pré-existente deve ser convertido para estar em conformidade com a estrutura necessária para a API [SRP](srp.md) após a atualização para o AEM Communities 6.3.

Há uma ferramenta de código aberto disponível no GitHub para esse fim:

* [Ferramenta de migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

A ferramenta de migração pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais AEM para importação para o AEM Communities 6.1 ou posterior.

### Erro - id_do_provedor de campo indefinido {#error-undefined-field-provider-id}

Se o seguinte erro for exibido nos registros, isso indica que o arquivo Solr schema não está configurado corretamente.

#### JsonMappingException: device_id de campo não definido {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver o erro, ao seguir as instruções de [instalação do Standard MLS](solr.md#installing-standard-mls), verifique se:

* Os arquivos de configuração XML foram copiados para o local correto do Solr.
* A Solr foi reiniciada após os novos arquivos de configuração substituírem os existentes.

### Falha na Conexão Segura ao MongoDB {#secure-connection-to-mongodb-fails}

Se uma tentativa de fazer uma conexão segura com o servidor MongoDB falhar devido a uma definição de classe ausente, será necessário atualizar o conjunto de drivers MongoDB, `mongo-java-driver`, disponível no repositório maven público.

1. Baixe o driver em [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versão 2.13.2 ou posterior).
1. Copie o pacote na pasta &quot;crx-quickstart/install&quot; para uma instância AEM.
1. Reinicie a instância AEM.

## Recursos {#resources}

* [AEM com MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentação do MongoDB](https://docs.mongodb.org/)

