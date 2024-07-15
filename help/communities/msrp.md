---
title: MSRP - Provedor de Recurso de Armazenamento MongoDB
description: Configurar o AEM Communities para usar um banco de dados relacional como seu armazenamento comum
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP - Provedor de Recurso de Armazenamento MongoDB {#msrp-mongodb-storage-resource-provider}

## Sobre o MSRP {#about-msrp}

Quando o AEM Communities é configurado para usar o MSRP como seu armazenamento comum, o conteúdo gerado pelo usuário (UGC) pode ser acessado de todas as instâncias de criação e publicação sem a necessidade de sincronização ou replicação.

Consulte também [Características das Opções SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias Recomendadas](topologies.md).

## Requisitos {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versão 2.6 ou superior
   * Não é necessário configurar mongos ou fragmentação
   * Recomendamos o uso de um [conjunto de réplicas](#mongoreplicaset)
   * Pode ser executado no mesmo host que o AEM ou remotamente

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr versão 7.0
   * Solr requer Java 1.7 ou superior
   * Nenhum serviço é necessário
   * Opção de modos de execução:
      * Modo independente
      * [Modo SolrCloud](solr.md#solrcloud-mode) (recomendado para ambientes de produção)
   * Opção de Pesquisa Multilíngue (MLS):
      * [Instalando o MLS Padrão](solr.md#installing-standard-mls)
      * [Instalando o MLS Avançado](solr.md#installing-advanced-mls)

## Configuração do MongoDB {#mongodb-configuration}

### Selecionar MSRP {#select-msrp}

O [console de Configuração de Armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

Na criação, para acessar o console Configuração de armazenamento:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Configuração de Armazenamento]**.

![msrp](assets/msrp.png)

* Selecionar **[!UICONTROL Provedor de Recurso de Armazenamento MongoDB (MSRP)]**
* **[!UICONTROL Configuração do mongoDB]**

   * **[!UICONTROL URI do mongoDB]**

     *padrão*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Banco de dados do mongoDB]**

     *padrão*: comunidades

   * **[!UICONTROL Coleção de UGC do mongoDB]**

     *padrão*: conteúdo

   * **[!UICONTROL Coleção de anexos do mongoDB]**

     *padrão*: anexos

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) Host**

     Ao executar no [modo SolrCloud](solr.md#solrcloud-mode) com um ZooKeeper externo, defina este valor como `HOST:PORT` para o ZooKeeper, como *my.server.com:2181*

     Para um Conjunto do ZooKeeper, insira valores `HOST:PORT` separados por vírgula, como *host1:2181,host2:2181*

     Deixe em branco se estiver executando o Solr no modo independente usando o ZooKeeper interno.
     *Padrão*: *&lt;em branco>*

      * **[!UICONTROL URL Solr]**
O URL usado para se comunicar com Solr no modo independente.
Deixe em branco se estiver executando no modo SolrCloud.
        *Padrão*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Coleção Solr]**
O nome da coleção Solr.
        *Padrão*: coleção1

* Selecionar **[!UICONTROL Enviar]**

>[!NOTE]
>
>O banco de dados mongoDB, que tem como padrão o nome `communities`, não deve ser definido como o nome de um banco de dados que está sendo usado para [armazenamentos de nós ou armazenamentos de dados (binários)](../../help/sites-deploying/data-store-config.md). Consulte também [Elementos de Armazenamento no AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de réplicas do MongoDB {#mongodb-replica-set}

Para o ambiente de produção, é altamente recomendável configurar um conjunto de réplicas, um cluster de servidores MongoDB que implementa a replicação primária-secundária e o failover automatizado.

Para saber mais sobre conjuntos de réplicas, visite a documentação [Replicação](https://docs.mongodb.org/manual/replication/) do MongoDB.

Para trabalhar com conjuntos de réplicas e saber como definir conexões entre aplicativos e instâncias MongoDB, visite a documentação [Formato URI de cadeia de conexão](https://docs.mongodb.org/manual/reference/connection-string/) do MongoDB.

#### Exemplo de Url para Conexão com um Conjunto de Réplicas  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (MSRP) usando coleções diferentes.

Se as coleções do Oak e do MSRP forem usadas intensamente, um segundo Solr poderá ser instalado por motivos de desempenho.

Para ambientes de produção, o [modo SolrCloud](solr.md#solrcloud-mode) oferece melhor desempenho do que o modo autônomo (uma configuração Solr local única).

Para obter detalhes sobre a configuração, consulte [Configuração Solr para SRP](solr.md).

### Atualizando {#upgrading}

Se atualizar de uma versão anterior configurada com MSRP, será necessário:

1. Executar a [atualização para o AEM Communities](upgrade.md)
1. Instalar novos arquivos de configuração Solr
   * Para [MLS padrão](solr.md#installing-standard-mls)
   * Para [MLS avançado](solr.md#installing-advanced-mls)
1. Reindexar MSRP
Consulte a seção [Ferramenta de Reindexação do MSRP](#msrp-reindex-tool)

## Publicar a configuração {#publishing-the-configuration}

O MSRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação, faça logon na instância do autor e siga as etapas:

* Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
* Selecionar **[!UICONTROL Ativar árvore]**
* **[!UICONTROL Caminho Inicial]**:
   * Navegar até `/etc/socialconfig/srpc/`
* Selecionar **[!UICONTROL Ativar]**

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuários* e *grupos de usuários*, inseridos com frequência no ambiente de publicação, visite

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Ferramenta Reindexação MSRP {#msrp-reindex-tool}

Há um ponto de extremidade HTTP para reindexação de Solr para MSRP ao instalar novos arquivos de configuração ou reparar um índice Solr danificado.

Com esta ferramenta, o MongoDB é a origem da *verdade* para MSRP; os backups só precisam ser feitos do MongoDB.

A árvore UGC inteira pode ser reindexada ou apenas uma subárvore específica, conforme especificado pelo parâmetro de dados *path *.

Essa ferramenta pode ser executada a partir da linha de comando usando cURL ou qualquer outra ferramenta HTTP.

Ao reindexar, há uma compensação entre a memória e o desempenho controlado pelo parâmetro de dados *batchSize *, que especifica quantos registros UGC são reindexados por lote.

Um padrão razoável é 5000:

* Se a memória for um problema, especifique um número menor
* Se a velocidade for um problema, especifique um número maior para aumentar a velocidade

### Executando a Ferramenta de Reindexação MSRP com o Comando cURL {#running-msrp-reindex-tool-using-curl-command}

O comando cURL a seguir mostra o que é necessário para uma solicitação HTTP reindexar o UGC armazenado no MSRP.

O formato básico é:

cURL -u *signin* -d *data* *reindex-url*

*entrada* = administrator-id:password
Por exemplo: admin:admin

*dados* = &quot;batchSize=*size*&amp;path=*path&quot;*

*tamanho* = quantas entradas de UGC devem ser reindexadas por operação
`/content/usergenerated/asi/mongo/`

*caminho* = o local raiz da árvore de UGC a ser reindexada

* Para reindexar todo o UGC, especifique o valor da propriedade `asipath` de
  `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar o índice a algum UGC, especifique uma subárvore de `asipath`

*reindex-url* = o ponto de extremidade para reindexação de SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se você estiver [reindexando DSRP Solr](dsrp.md), a URL será **/services/social/datastore/rdb/reindex**

### Exemplo de reindexação de MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Como demonstrar o MSRP {#how-to-demo-msrp}

Para configurar o MSRP para um ambiente de demonstração ou desenvolvimento, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

## Resolução de problemas {#troubleshooting}

### UGC não visível no MongoDB {#ugc-not-visible-in-mongodb}

Verifique se o MSRP foi configurado como o provedor padrão verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP.

Em todas as instâncias de AEM de autoria e publicação, revisite o [console de Configuração de Armazenamento](srp-config.md) ou verifique o repositório AEM:

* No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Não contém um nó [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades defaultconfiguration deverão definir MSRP como o provedor padrão.

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se estiver atualizando de um site existente do AEM Communities 6.0, qualquer UGC pré-existente deverá ser convertido para se adequar à estrutura necessária para a API [SRP](srp.md) após a atualização para o AEM Communities 6.3.

Há uma ferramenta de código aberto disponível no GitHub para esta finalidade:

* [Ferramenta de Migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

A ferramenta de migração pode ser personalizada para exportar o UGC de versões anteriores de comunidades sociais do AEM para importação no AEM Communities 6.1 ou posterior.

### Erro - campo indefinido provider_id {#error-undefined-field-provider-id}

Se o erro a seguir for visto nos logs, isso indicará que o arquivo de esquema Solr não está configurado corretamente.

#### JsonMappingException: campo indefinido provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Para resolver o erro, ao seguir as instruções para [Instalando MLS Padrão](solr.md#installing-standard-mls), verifique se:

* Os arquivos de configuração XML foram copiados para o local Solr correto.
* O Solr foi reiniciado depois que os novos arquivos de configuração substituíram os existentes.

### Falha na conexão segura com o MongoDB {#secure-connection-to-mongodb-fails}

Se uma tentativa de fazer uma conexão segura com o servidor MongoDB falhar devido a uma definição de classe ausente, é necessário atualizar o pacote de drivers MongoDB, `mongo-java-driver`, disponível no repositório público do Maven.

1. Baixe o driver de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versão 2.13.2 ou posterior).
1. Copie o pacote na pasta &quot;crx-quickstart/install&quot; para uma instância de AEM.
1. Reinicie a instância do AEM.

## Recursos {#resources}

* [AEM com MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentação do MongoDB](https://docs.mongodb.org/)
