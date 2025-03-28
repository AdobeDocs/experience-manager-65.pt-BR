---
title: Suporte RDBMS no AEM 6.4
description: Saiba mais sobre o suporte à persistência de banco de dados relacional no AEM 6.4 e as opções de configuração disponíveis.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Suporte RDBMS no AEM 6.4{#rdbms-support-in-aem}

## Visão geral {#overview}

O suporte à persistência do banco de dados relacional no AEM é implementado usando o Document Microkernel. O Document Microkernel é a base que também é usada para implementar a persistência do MongoDB.

Ele consiste em uma API Java baseada na API Java Mongo. Uma implementação de uma API BlobStore também é fornecida. Por padrão, os blobs são armazenados no banco de dados.

Para obter mais informações sobre os detalhes da implementação, consulte a documentação do [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e do [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html).

>[!NOTE]
>
>Também é fornecido suporte ao **PostgreSQL 9.4**, mas apenas para fins de demonstração. Ele não estará disponível para ambientes de produção.

## Bancos de dados suportados {#supported-databases}

Para obter mais informações sobre o nível de suporte ao Banco de Dados Relacional no AEM, consulte a [página Requisitos Técnicos](/help/sites-deploying/technical-requirements.md).

## Etapas de configuração {#configuration-steps}

O repositório é criado pela configuração do serviço OSGi `DocumentNodeStoreService`. Ele foi estendido para oferecer suporte à persistência de bancos de dados relacionais, além do MongoDB.

Para funcionar, uma fonte de dados precisa ser configurada com AEM. Isso é feito através do arquivo `org.apache.sling.datasource.DataSourceFactory.config`. Os drivers JDBC para o respectivo banco de dados precisam ser fornecidos separadamente como pacotes OSGi dentro da configuração local.

Para obter etapas sobre como criar pacotes OSGi para drivers JDBC, consulte esta [documentação](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) no site do Apache Sling.

Quando os pacotes estiverem em vigor, siga as etapas abaixo para configurar o AEM com persistência RDB:

1. Verifique se o daemon do banco de dados foi iniciado e se você tem um banco de dados ativo para uso com AEM.
1. Copie o jar do AEM 6.3 no diretório de instalação.
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento do nó de documentos criando um arquivo de configuração com o seguinte nome no diretório `crx-quickstart\install`:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configure a fonte de dados e os parâmetros JDBC criando outro arquivo de configuração com o seguinte nome na pasta `crx-quickstart\install`:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`

   >[!NOTE]
   >
   >Para obter informações detalhadas sobre a configuração da fonte de dados para cada banco de dados com suporte, consulte [Opções de Configuração do Data Source](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Em seguida, prepare os pacotes OSGi do JDBC a serem usados com AEM:

   1. Na pasta `crx-quickstart/install`, crie uma pasta chamada `9`.

   1. Coloque o jar JDBC na nova pasta.

1. Finalmente, inicie o AEM com os modos de execução `crx3` e `crx3rdb`:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opções de configuração do Data Source {#data-source-configuration-options}

A configuração OSGi `org.apache.sling.datasource.DataSourceFactory-oak.config` é usada para configurar os parâmetros necessários para a comunicação entre o AEM e a camada de persistência do banco de dados.

As seguintes opções de configuração estão disponíveis:

* `datasource.name:` O nome da fonte de dados. O padrão é `oak`.

* `url:` A cadeia de caracteres de URL do banco de dados que precisa ser usada com JDBC. Cada tipo de banco de dados tem seu próprio formato de string de URL. Para obter mais informações, consulte [Formatos de Cadeia de Caracteres de URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) abaixo.

* `driverClassName:` O nome da classe do driver JDBC. Isso será diferente dependendo do banco de dados que você deseja usar e, subsequentemente, do driver necessário para se conectar a ele. Abaixo estão os nomes de classe de todos os bancos de dados suportados pelo AEM:

   * `org.postgresql.Driver` para PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` para DB2;
   * `oracle.jdbc.OracleDriver` para o Oracle;
   * `com.mysql.jdbc.Driver` para MySQL e MariaDB (experimental);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` para Microsoft SQL Server (experimental).

* `username:` O nome de usuário com o qual o banco de dados é executado.

* `password:` A senha do banco de dados.

### Formatos de string de URL {#url-string-formats}

Um formato de cadeia de caracteres de URL diferente é usado na configuração da fonte de dados, dependendo do tipo de banco de dados que precisa ser usado. Abaixo está uma lista de formatos para os bancos de dados compatíveis atualmente com o AEM:

* `jdbc:postgresql:databasename` para PostgreSQL;
* `jdbc:db2://localhost:port/databasename` para DB2;
* `jdbc:oracle:thin:localhost:port:SID` para o Oracle;
* `jdbc:mysql://localhost:3306/databasename` para MySQL e MariaDB (experimental);
* `jdbc:sqlserver://localhost:1453;databaseName=name` para Microsoft SQL Server (experimental).

## Limitações conhecidas {#known-limitations}

Embora o uso simultâneo de várias instâncias de AEM com um único banco de dados seja suportado pela persistência do RDBMS, as instalações simultâneas não são.

Para contornar isso, certifique-se de executar a instalação com um único membro primeiro e adicionar os outros depois que o primeiro terminar de instalar.
