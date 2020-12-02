---
title: Suporte a RDBMS no AEM 6.4
seo-title: Suporte a RDBMS no AEM 6.4
description: Saiba mais sobre o suporte à persistência do banco de dados relacional no AEM 6.4 e as opções de configuração disponíveis.
seo-description: Saiba mais sobre o suporte à persistência do banco de dados relacional no AEM 6.4 e as opções de configuração disponíveis.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---


# Suporte a RDBMS no AEM 6.4{#rdbms-support-in-aem}

## Visão geral {#overview}

O suporte para a persistência do banco de dados relacional no AEM é implementado usando o Documento Microkernel. O Microkernel do Documento é a base que também é usada para implementar a persistência do MongoDB.

Ele consiste em uma API Java baseada na API Java Mongo. Uma implementação de uma API BlobStore também é fornecida. Por padrão, os blobs são armazenados no banco de dados.

Para obter mais informações sobre os detalhes de implementação, consulte a documentação [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>O suporte para **PostgreSQL 9.4** também é fornecido, mas somente para fins de demonstração. Ele não estará disponível para ambientes de produção.

## Bancos de dados suportados {#supported-databases}

Para obter mais informações sobre o nível de suporte ao banco de dados relacional no AEM, consulte a [página Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

## Etapas de configuração {#configuration-steps}

O repositório é criado pela configuração do serviço `DocumentNodeStoreService` OSGi. Foi estendido para suportar a persistência do banco de dados relacional, além do MongoDB.

Para que funcione, uma fonte de dados precisa ser configurada com AEM. Isso é feito pelo arquivo `org.apache.sling.datasource.DataSourceFactory.config`. Os drivers JDBC para o respectivo banco de dados precisam ser fornecidos separadamente, já que os pacotes OSGi estão dentro da configuração local.

Para obter etapas sobre como criar pacotes OSGi para drivers JDBC, consulte esta [documentação](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) no site Apache Sling.

Depois que os pacotes estiverem em vigor, siga as etapas abaixo para configurar o AEM com a persistência RDB:

1. Verifique se o daemon do banco de dados foi iniciado e se você tem um banco de dados ativo para uso com AEM.
1. Copie o AEM 6.3 jar no diretório de instalação.
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento de nó do documento criando um arquivo de configuração com o seguinte nome no diretório `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configure a fonte de dados e os parâmetros JDBC criando outro arquivo de configuração com o seguinte nome na pasta `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Para obter informações detalhadas sobre a configuração da fonte de dados para cada banco de dados suportado, consulte [Opções de configuração da fonte de dados](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Em seguida, prepare os pacotes JDBC OSGi a serem usados com AEM:

   1. Na pasta `crx-quickstart/install`, crie uma pasta chamada `9`.

   1. Coloque o JDBC jar na nova pasta.

1. Finalmente, o start AEM com os modos de execução `crx3` e `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opções de configuração da fonte de dados {#data-source-configuration-options}

A configuração `org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi é usada para configurar os parâmetros necessários para a comunicação entre o AEM e a camada de persistência do banco de dados.

As seguintes opções de configuração estão disponíveis:

* `datasource.name:` O nome da fonte de dados. O padrão é `oak`.

* `url:` A string de URL do banco de dados que precisa ser usado com o JDBC. Cada tipo de banco de dados tem seu próprio formato de string de URL. Para obter mais informações, consulte [Formatos de cadeia de caracteres de URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) abaixo.

* `driverClassName:` O nome da classe do driver JDBC. Isso será diferente dependendo do banco de dados que você deseja usar e, subsequentemente, do driver que é necessário para se conectar a ele. Abaixo estão os nomes de classe para todos os bancos de dados suportados pela AEM:

   * `org.postgresql.Driver` PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` para Oracle;
   * `com.mysql.jdbc.Driver` MySQL e MariaDB (experimental);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` para Microsoft SQL Server (experimental).

* `username:` O nome de usuário em que o banco de dados é executado.

* `password:` A senha do banco de dados.

### Formatos de cadeia de caracteres de URL {#url-string-formats}

Um formato de string de URL diferente é usado na configuração da fonte de dados, dependendo do tipo de banco de dados que precisa ser usado. Abaixo está uma lista de formatos para os bancos de dados que AEM atualmente compatíveis:

* `jdbc:postgresql:databasename` PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` para Oracle;
* `jdbc:mysql://localhost:3306/databasename` MySQL e MariaDB (experimental);
* `jdbc:sqlserver://localhost:1453;databaseName=name` para Microsoft SQL Server (experimental).

## Limitações conhecidas {#known-limitations}

Embora o uso simultâneo de várias instâncias AEM com um único banco de dados seja suportado pela persistência de RDBMS, as instalações simultâneas não são.

Para contornar esse problema, primeiro execute a instalação com um único membro e adicione os outros depois que a primeira instalação terminar.

