---
title: Suporte RDBMS no AEM 6.4
seo-title: RDBMS Support in AEM 6.4
description: Saiba mais sobre o suporte à persistência do banco de dados relacional no AEM 6.4 e as opções de configuração disponíveis.
seo-description: Learn about the relational database persistence support in AEM 6.4 and the available configuration options.
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
feature: Configuring
exl-id: 1e34c5ca-9e08-4b2a-901c-ab28aeb4a807
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Suporte RDBMS no AEM 6.4{#rdbms-support-in-aem}

## Visão geral {#overview}

O suporte para a persistência do banco de dados relacional no AEM é implementado usando o Microkernel de Documento. O Microkernel de Documento é a base que também é usada para implementar a persistência do MongoDB.

Consiste em uma API Java baseada na API Java do Mongo. Uma implementação de uma API BlobStore também é fornecida. Por padrão, os blobs são armazenados no banco de dados.

Para obter mais informações sobre os detalhes de implementação, consulte o [RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) e [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) documentação.

>[!NOTE]
>
>Suporte para **PostgreSQL 9.4** também é fornecido, mas somente para fins de demonstração. Ele não estará disponível para ambientes de produção.

## Bancos de Dados Suportados {#supported-databases}

Para obter mais informações sobre o nível de suporte a Banco de Dados Relacional no AEM, consulte o [Página Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

## Etapas de configuração {#configuration-steps}

O repositório é criado configurando o `DocumentNodeStoreService` Serviço OSGi. Ele foi estendido para oferecer suporte à persistência de banco de dados relacional, além do MongoDB.

Para que funcione, uma fonte de dados precisa ser configurada com AEM. Isso é feito por meio da variável `org.apache.sling.datasource.DataSourceFactory.config` arquivo. Os drivers JDBC para o respectivo banco de dados precisam ser fornecidos separadamente como pacotes OSGi dentro da configuração local.

Para obter as etapas sobre a criação de pacotes OSGi para drivers JDBC, consulte esta [documentação](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle) no site do Apache Sling.

Depois que os pacotes estiverem em vigor, siga as etapas abaixo para configurar o AEM com a persistência de RDB:

1. Certifique-se de que o daemon do banco de dados foi iniciado e que você tem um banco de dados ativo para usar com o AEM.
1. Copie o jar do AEM 6.3 no diretório de instalação.
1. Crie uma pasta chamada `crx-quickstart\install` no diretório de instalação.
1. Configure o armazenamento do nó do documento criando um arquivo de configuração com o seguinte nome no `crx-quickstart\install` diretório:

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. Configure a fonte de dados e os parâmetros JDBC criando outro arquivo de configuração com o seguinte nome no `crx-quickstart\install` pasta:

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >Para obter informações detalhadas sobre a configuração da fonte de dados para cada banco de dados suportado, consulte [Opções de configuração da fonte de dados](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options).

1. Em seguida, prepare os pacotes OSGi do JDBC para serem usados com o AEM:

   1. No `crx-quickstart/install` criar uma pasta chamada `9`.

   1. Coloque o jar JDBC na nova pasta.

1. Por fim, comece AEM com o `crx3` e `crx3rdb` runmodes:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## Opções de configuração da fonte de dados {#data-source-configuration-options}

O `org.apache.sling.datasource.DataSourceFactory-oak.config` A configuração OSGi é usada para configurar os parâmetros necessários para a comunicação entre o AEM e a camada de persistência do banco de dados.

As seguintes opções de configuração estão disponíveis:

* `datasource.name:` O nome da fonte de dados. O padrão é `oak`.

* `url:` A cadeia de caracteres do URL do banco de dados que precisa ser usado com o JDBC. Cada tipo de banco de dados tem seu próprio formato de string de URL. Para obter mais informações, consulte [Formatos da string do URL](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats) abaixo.

* `driverClassName:` O nome da classe do driver JDBC. Isso será diferente dependendo do banco de dados que deseja usar e, subsequentemente, do driver necessário para se conectar a ele. Abaixo estão os nomes de classe para todos os bancos de dados suportados pelo AEM:

   * `org.postgresql.Driver` PostgreSQL;
   * `com.ibm.db2.jcc.DB2Driver` DB2;
   * `oracle.jdbc.OracleDriver` para Oracle;
   * `com.mysql.jdbc.Driver` para MySQL e MariaDB (experimental);
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` para Microsoft SQL Server (experimental).

* `username:` O nome de usuário em que o banco de dados é executado.

* `password:` A senha do banco de dados.

### Formatos da string do URL {#url-string-formats}

Um formato de string de URL diferente é usado na configuração da fonte de dados, dependendo do tipo de banco de dados que precisa ser usado. Abaixo está uma lista de formatos para os bancos de dados que AEM atualmente:

* `jdbc:postgresql:databasename` PostgreSQL;
* `jdbc:db2://localhost:port/databasename` DB2;
* `jdbc:oracle:thin:localhost:port:SID` para Oracle;
* `jdbc:mysql://localhost:3306/databasename` para MySQL e MariaDB (experimental);
* `jdbc:sqlserver://localhost:1453;databaseName=name` para Microsoft SQL Server (experimental).

## Limitações conhecidas {#known-limitations}

Embora o uso simultâneo de várias instâncias de AEM com um único banco de dados seja compatível com a persistência do RDBMS, as instalações simultâneas não são.

Para contornar isso, execute a instalação com um único membro primeiro e adicione os outros depois que o primeiro terminar de instalar.
