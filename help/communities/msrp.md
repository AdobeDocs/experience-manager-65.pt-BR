---
title: MSRP - Provedor de Recurso de Armazenamento MongoDB
description: Configurar o AEM Communities para usar um banco de dados relacional como seu armazenamento comum
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 0%

---

# MSRP - Provedor de Recurso de Armazenamento MongoDB {#msrp-mongodb-storage-resource-provider}

## Sobre o MSRP {#about-msrp}

Quando o AEM Communities é configurado para usar o MSRP como seu armazenamento comum, o conteúdo gerado pelo usuário (UGC) pode ser acessado de todas as instâncias de criação e publicação sem a necessidade de sincronização ou replicação.

Consulte também [Características das opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Requisitos {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Versão 2.6 ou superior
   * Não é necessário configurar mongos ou fragmentação
   * Recomenda fortemente o uso de um [conjunto de réplicas](#mongoreplicaset)
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

A variável [Console de configuração de armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

Na criação, para acessar o console Configuração de armazenamento:

* Na navegação global, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]** > **[!UICONTROL Configuração de armazenamento]**.

![msrp](assets/msrp.png)

* Selecionar **[!UICONTROL Provedor de recurso de armazenamento MongoDB (MSRP, na sigla em inglês)]**
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

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) Host**

     Ao executar em [Modo SolrCloud](solr.md#solrcloud-mode) com um ZooKeeper externo, defina esse valor como o `HOST:PORT` para o ZooKeeper, como *my.server.com:2181*

     Para um Conjunto do ZooKeeper, insira separado por vírgulas `HOST:PORT` valores, como *host1:2181,host2:2181*

     Deixe em branco se estiver executando o Solr no modo independente usando o ZooKeeper interno.
     *Padrão*: *&lt;blank>*

      * **[!UICONTROL URL de Solr]**
O URL usado para se comunicar com Solr no modo independente.
Deixe em branco se estiver executando no modo SolrCloud.
        *Padrão*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Coleção Solr]**
O nome da coleção Solr.
        *Padrão*: coleção1

* Selecionar **[!UICONTROL Enviar]**

>[!NOTE]
>
>O banco de dados mongoDB, que usa como padrão o nome `communities`, não deve ser definido com o nome de um banco de dados que está sendo usado para [armazenamentos de nó ou armazenamentos de dados (binários)](../../help/sites-deploying/data-store-config.md). Consulte também [Elementos de armazenamento no AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Conjunto de réplicas do MongoDB {#mongodb-replica-set}

Para o ambiente de produção, é altamente recomendável configurar um conjunto de réplicas, um cluster de servidores MongoDB que implementa a replicação primária-secundária e o failover automatizado.

Para saber mais sobre conjuntos de réplicas, visite MongoDB&#39;s [Replicação](https://docs.mongodb.org/manual/replication/) documentação.

Para trabalhar com conjuntos de réplicas e saber como definir conexões entre aplicativos e instâncias MongoDB, visite o MongoDB&#39;s [Formato URI da Cadeia de Caracteres de Conexão](https://docs.mongodb.org/manual/reference/connection-string/) documentação.

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

Se as coleções Oak e MSRP forem usadas intensamente, um segundo Solr pode ser instalado por motivos de desempenho.

Para ambientes de produção, [Modo SolrCloud](solr.md#solrcloud-mode) O fornece desempenho aprimorado em relação ao modo independente (uma configuração Solr única e local).

Para obter detalhes sobre a configuração, consulte [Configuração Solr para SRP](solr.md).

### Atualizando {#upgrading}

Se atualizar de uma versão anterior configurada com MSRP, será necessário:

1. Execute o [atualização para o AEM Communities](upgrade.md)
1. Instalar novos arquivos de configuração Solr
   * Para [MLS padrão](solr.md#installing-standard-mls)
   * Para [MLS avançado](solr.md#installing-advanced-mls)
1. Reindexar MSRP Consulte a seção [Ferramenta Reindexação MSRP](#msrp-reindex-tool)

## Publicar a configuração {#publishing-the-configuration}

O MSRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação, faça logon na instância do autor e siga as etapas:

* Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**.
* Selecionar **[!UICONTROL Ativar árvore]**
* **[!UICONTROL Caminho inicial]**:
   * Navegue até `/etc/socialconfig/srpc/`
* Selecionar **[!UICONTROL Ativar]**

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, frequentemente inseridos no ambiente de publicação, visitem

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Ferramenta Reindexação MSRP {#msrp-reindex-tool}

Há um ponto de extremidade HTTP para reindexação de Solr para MSRP ao instalar novos arquivos de configuração ou reparar um índice Solr danificado.

Com essa ferramenta, o MongoDB é a fonte de *verdade* para MSRP; os backups só precisam ser feitos do MongoDB.

A árvore UGC inteira pode ser reindexada ou apenas uma subárvore específica, conforme especificado pelo parâmetro de dados *path *.

Essa ferramenta pode ser executada a partir da linha de comando usando cURL ou qualquer outra ferramenta HTTP.

Ao reindexar, há uma compensação entre a memória e o desempenho controlado pelo parâmetro de dados *batchSize *, que especifica quantos registros UGC são reindexados por lote.

Um padrão razoável é 5000:

* Se a memória for um problema, especifique um número menor
* Se a velocidade for um problema, especifique um número maior para aumentar a velocidade

### Executando a Ferramenta de Reindexação MSRP com o Comando cURL {#running-msrp-reindex-tool-using-curl-command}

O comando cURL a seguir mostra o que é necessário para uma solicitação HTTP reindexar o UGC armazenado no MSRP.

O formato básico é:

cURL -u *fazer logon* -d *dados* *reindex-url*

*fazer logon* = administrator-id:password Por exemplo: admin:admin

*dados* = &quot;batchSize=*tamanho*&amp;caminho=*caminho&quot;*

*tamanho* = quantas entradas de UGC devem ser reindexadas por operação
`/content/usergenerated/asi/mongo/`

*caminho* = o local raiz da árvore do UGC a ser reindexado

* Para reindexar todo o UGC, especifique o valor do `asipath`propriedade de
  `/etc/socialconfig/srpc/defaultconfiguration`
* Para limitar o índice a algum UGC, especifique uma subárvore de `asipath`

*reindex-url* = o terminal para reindexação do SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Se você estiver [reindexação de DSRP Solr](dsrp.md), o URL é **/services/social/datastore/rdb/reindex**

### Exemplo de reindexação de MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Como demonstrar o MSRP {#how-to-demo-msrp}

Para configurar o MSRP para um ambiente de demonstração ou desenvolvimento, consulte [Como configurar o MongoDB para demonstração](demo-mongo.md).

## Resolução de problemas {#troubleshooting}

### UGC não visível no MongoDB {#ugc-not-visible-in-mongodb}

Verifique se o MSRP foi configurado como o provedor padrão verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP.

Em todas as instâncias de AEM do autor e de publicação, revisite a [Console de configuração de armazenamento](srp-config.md) ou verifique o repositório AEM:

* No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Não contém um [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades defaultconfiguration devem definir o MSRP como o provedor padrão.

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se atualizar de um site do AEM Communities 6.0 existente, qualquer UGC pré-existente deve ser convertido para estar em conformidade com a estrutura necessária para o [SRP](srp.md) API após atualizar para o AEM Communities 6.3.

Há uma ferramenta de código aberto disponível no GitHub para esta finalidade:

* [Ferramenta de migração UGC do AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

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

Para resolver o erro, ao seguir as instruções para [Instalando o MLS Padrão](solr.md#installing-standard-mls), garantir:

* Os arquivos de configuração XML foram copiados para o local Solr correto.
* O Solr foi reiniciado depois que os novos arquivos de configuração substituíram os existentes.

### Falha na conexão segura com o MongoDB {#secure-connection-to-mongodb-fails}

Se uma tentativa de fazer uma conexão segura com o servidor MongoDB falhar devido a uma definição de classe ausente, é necessário atualizar o pacote de drivers MongoDB, `mongo-java-driver`, disponível no repositório público do Maven.

1. Baixe o driver em [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (versão 2.13.2 ou posterior).
1. Copie o pacote na pasta &quot;crx-quickstart/install&quot; para uma instância de AEM.
1. Reinicie a instância do AEM.

## Recursos {#resources}

* [AEM com MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentação do MongoDB](https://docs.mongodb.org/)
