---
title: Conectando a Bancos de Dados SQL
description: Acessar um banco de dados SQL externo no para que seus aplicativos AEM possam interagir com os dados
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---

# Conectando a Bancos de Dados SQL{#connecting-to-sql-databases}

Acesse um banco de dados SQL externo no para que seus aplicativos de CQ possam interagir com os dados:

1. [Crie ou obtenha um pacote OSGi que exporte o pacote de driver JDBC](#bundling-the-jdbc-database-driver).
1. [Configurar um provedor de pool de fonte de dados JDBC](#configuring-the-jdbc-connection-pool-service).
1. [Obtenha um objeto de fonte de dados e crie a conexão em seu código](#connecting-to-the-database).

## Agrupando o driver do banco de dados JDBC {#bundling-the-jdbc-database-driver}

Alguns fornecedores de bancos de dados fornecem drivers JDBC em um pacote OSGi, por exemplo, [MySQL](https://dev.mysql.com/downloads/connector/j/). Se o driver JDBC do seu banco de dados não estiver disponível como um pacote OSGi, obtenha o JAR do driver e coloque-o em um pacote OSGi. O pacote deve exportar os pacotes necessários para interagir com o servidor de banco de dados. O pacote também deve importar os pacotes aos quais faz referência.

O exemplo a seguir usa o [Plug-in do pacote para Maven](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html) para envolver o driver HSQLDB em um pacote OSGi. O POM instrui o plug-in a incorporar o arquivo hsqldb.jar identificado como uma dependência. Todos os pacotes org.hsqldb são exportados.

O plug-in determina automaticamente quais pacotes devem ser importados e os lista no arquivo MANIFEST.MF do pacote. Se qualquer um dos pacotes não estiver disponível no servidor CQ, o pacote não será iniciado na instalação. Duas soluções possíveis são as seguintes:

* Indique no POM que os pacotes são opcionais. Use esta solução quando a conexão JDBC não exigir realmente os membros do pacote. Use o elemento Import-Package para indicar pacotes opcionais, como no exemplo a seguir:

  `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Envolva os arquivos JAR que contêm os pacotes em um pacote OSGi que exporta os pacotes e implante o pacote. Use esta solução quando os membros do pacote forem necessários durante a execução do código.

O conhecimento do código-fonte permite decidir qual solução usar. Você também pode experimentar qualquer uma das soluções e executar testes para validar a solução.

### POM que empacota hsqldb.jar {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

Os links a seguir abrem as páginas de download de alguns produtos de banco de dados populares:

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### Configurando o serviço de pool de conexão JDBC {#configuring-the-jdbc-connection-pool-service}

Adicione uma configuração para o serviço Pool de Conexões JDBC que usa o driver JDBC para criar objetos de origem de dados. O código do aplicativo usa esse serviço para obter o objeto e conectar-se ao banco de dados.

O Pool de Conexões JDBC ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) é um serviço de fábrica. Se você precisar de conexões que usem propriedades diferentes, por exemplo, acesso somente leitura ou de leitura/gravação, crie várias configurações.

Ao trabalhar com o CQ, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

As seguintes propriedades estão disponíveis para configurar um serviço de conexão em pool. Os nomes das propriedades são listados à medida que aparecem no Console da Web. O nome correspondente de um nó `sling:OsgiConfig` aparece entre parênteses. Os valores de exemplo são mostrados para um servidor HSQLDB e um banco de dados que tem um alias de `mydb`:

* Classe de Driver JDBC ( `jdbc.driver.class`): a classe Java™ a ser usada que implementa a interface java.sql.Driver, por exemplo, `org.hsqldb.jdbc.JDBCDriver`. O tipo de dados é `String`.

* URI da Conexão JDBC ( `jdbc.connection.uri`): A URL do banco de dados a ser usada para criar a conexão, por exemplo, `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. O formato do URL deve ser válido para uso com o método getConnection da classe java.sql.DriverManager. O tipo de dados é `String`.

* Nome de usuário ( `jdbc.username`): o nome de usuário a ser usado para autenticação com o servidor de banco de dados. O tipo de dados é `String`.

* Senha ( `jdbc.password`): a senha a ser usada para autenticação do usuário. O tipo de dados é `String`.

* Consulta de Validação ( `jdbc.validation.query`): a instrução SQL a ser usada para verificar se a conexão foi bem-sucedida; por exemplo, `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. O tipo de dados é `String`.

* Somente leitura por padrão (default.readonly): selecione essa opção quando quiser que a conexão forneça acesso somente leitura. O tipo de dados é `Boolean`.
* Autocommit By Default ( `default.autocommit`): Selecione esta opção para criar transações separadas para cada comando SQL enviado ao banco de dados e cada transação é automaticamente confirmada. Não selecione essa opção quando estiver confirmando transações explicitamente no código. O tipo de dados é `Boolean`.

* Tamanho do Pool ( `pool.size`): O número de conexões simultâneas a serem disponibilizadas para o banco de dados. O tipo de dados é `Long`.

* Espera do pool ( `pool.max.wait.msec`): o tempo antes que uma solicitação de conexão expire. O tipo de dados é `Long`.

* Nome da fonte de dados ( `datasource.name`): o nome dessa fonte de dados. O tipo de dados é `String`.

* Propriedades de Serviço Adicional ( `datasource.svc.properties`): Um conjunto de pares de nome/valor que você deseja anexar à URL de conexão. O tipo de dados é `String[]`.

O serviço Pool de Conexões JDBC é uma fábrica. Portanto, se você usar um nó `sling:OsgiConfig` para configurar o serviço de conexão, o nome do nó deverá incluir o PID do serviço de fábrica seguido por *`-alias`*. O alias usado deve ser exclusivo para todos os nós de configuração para esse PID. Um exemplo de nome de nó é `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Conexão com o banco de dados {#connecting-to-the-database}

Em seu código Java™, use o serviço DataSourcePool para obter um objeto `javax.sql.DataSource` para a configuração que você criou. O serviço DataSourcePool fornece o método `getDataSource` que retorna um objeto `DataSource` para um determinado nome de fonte de dados. Como argumento do método, use o valor da propriedade Nome da Fonte de Dados (ou `datasource.name`) que você especificou para a configuração do Pool de Conexões JDBC.

O código JSP de exemplo a seguir obtém uma instância da fonte de dados hsqldbds, executa uma consulta SQL simples e exibe o número de resultados retornados.

#### JSP que executa uma pesquisa de banco de dados {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>Se o método getDataSource gerar uma exceção porque a fonte de dados não foi encontrada, verifique se a configuração do serviço Pool de Conexões está correta. Verifique os nomes das propriedades, os valores e os tipos de dados.
>

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
