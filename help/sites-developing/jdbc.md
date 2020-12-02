---
title: Conexão com Bancos de Dados SQL
seo-title: Conexão com Bancos de Dados SQL
description: Acessar um banco de dados SQL externo para que seus aplicativos AEM possam interagir com os dados
seo-description: Acessar um banco de dados SQL externo para que seus aplicativos AEM possam interagir com os dados
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Conexão com Bancos de Dados SQL{#connecting-to-sql-databases}

Acesse um banco de dados SQL externo para que seus aplicativos CQ possam interagir com os dados:

1. [Crie ou obtenha um pacote OSGi que exporte o pacote](#bundling-the-jdbc-database-driver) de driver JDBC.
1. [Configure um provedor](#configuring-the-jdbc-connection-pool-service) de pool de fontes de dados JDBC.
1. [Obtenha um objeto de fonte de dados e crie a conexão em seu código](#connecting-to-the-database).

## Pacote do driver de banco de dados JDBC {#bundling-the-jdbc-database-driver}

Alguns fornecedores de banco de dados fornecem drivers JDBC em um pacote OSGi, por exemplo [MySQL](https://www.mysql.com/downloads/connector/j/). Se o driver JDBC para seu banco de dados não estiver disponível como um pacote OSGi, obtenha o JAR do driver e coloque-o em um pacote OSGi. O pacote deve exportar os pacotes necessários para interagir com o servidor de banco de dados. O pacote também deve importar os pacotes aos quais faz referência.

O exemplo a seguir usa o plug-in [Bundle para Maven](https://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html) para vincular o driver HSQLDB em um pacote OSGi. O POM instrui o plug-in a incorporar o arquivo hsqldb.jar identificado como uma dependência. Todos os pacotes org.hsqldb são exportados.

O plug-in determina automaticamente quais pacotes serão importados e os lista no arquivo MANIFEST.MF do pacote. Se algum dos pacotes não estiver disponível no servidor CQ, o pacote não será start ao instalar. Duas soluções possíveis são as seguintes:

* Indique no POM que os pacotes são opcionais. Use essa solução quando a conexão JDBC não exigir os membros do pacote. Use o elemento Importar pacote para indicar os pacotes opcionais, como no exemplo a seguir:

   `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* Encapsule os arquivos JAR que contêm os pacotes em um pacote OSGi que exporta os pacotes e implante o pacote. Use essa solução quando os membros do pacote forem necessários durante a execução do código.

O conhecimento do código-fonte permite que você decida qual solução usar. Você também pode tentar qualquer solução e executar testes para validar a solução.

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

* [Microsoft SQL Server](https://www.microsoft.com/en-us/download/details.aspx?displaylang=en&amp;id=11774)
* [Oracle](https://www.oracle.com/technetwork/database/features/jdbc/index-091264.html)
* [IBM DB2](https://www-01.ibm.com/support/docview.wss?uid=swg27007053)

### Configurando o serviço de pool de conexão JDBC {#configuring-the-jdbc-connection-pool-service}

Adicione uma configuração para o serviço do pool de conexões JDBC que usa o driver JDBC para criar objetos de fonte de dados. O código do aplicativo usa esse serviço para obter o objeto e se conectar ao banco de dados.

O JDBC Connections Pool ( `com.day.commons.datasource.jdbcpool.JdbcPoolService`) é um serviço de fábrica. Se você precisar de conexões que usam propriedades diferentes, por exemplo, acesso somente leitura ou acesso de leitura/gravação, crie várias configurações.

Ao trabalhar com o CQ, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configurando o OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos.

As seguintes propriedades estão disponíveis para configurar um serviço de conexão em pool. Os nomes das propriedades são listados conforme aparecem no Console da Web. O nome correspondente para um nó `sling:OsgiConfig` aparece entre parênteses. Exemplos de valores são mostrados para um servidor HSQLDB e um banco de dados que tem um alias de `mydb`:

* Classe de driver JDBC ( `jdbc.driver.class`): A classe Java a ser usada que implementa a interface java.sql.Driver, por exemplo `org.hsqldb.jdbc.JDBCDriver`. O tipo de dados é `String`.

* URI de conexão JDBC ( `jdbc.connection.uri`): O URL do banco de dados a ser usado para criar a conexão, por exemplo `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. O formato do URL deve ser válido para uso com o método getConnection da classe java.sql.DriverManager. O tipo de dados é `String`.

* Nome de usuário ( `jdbc.username`): O nome de usuário a ser usado para autenticação no servidor de banco de dados. O tipo de dados é `String`.

* Senha ( `jdbc.password`): A senha a ser usada para autenticação do usuário. O tipo de dados é `String`.

* Query de validação ( `jdbc.validation.query`): A instrução SQL a ser usada para verificar se a conexão foi bem-sucedida, por exemplo `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. O tipo de dados é `String`.

* Somente leitura por padrão (default.readonly): Selecione essa opção quando desejar que a conexão forneça acesso somente leitura. O tipo de dados é `Boolean`.
* Confirmação automática por padrão ( `default.autocommit`): Selecione essa opção para criar transações separadas para cada comando SQL enviado para o banco de dados e cada transação é automaticamente confirmada. Não selecione essa opção ao confirmar transações explicitamente em seu código. O tipo de dados é `Boolean`.

* Tamanho do pool ( `pool.size`): O número de conexões simultâneas a serem disponibilizadas para o banco de dados. O tipo de dados é `Long`.

* Espera do pool ( `pool.max.wait.msec`): A quantidade de tempo antes de uma solicitação de conexão expirar. O tipo de dados é `Long`.

* Nome da fonte de dados ( `datasource.name`): O nome dessa fonte de dados. O tipo de dados é `String`.

* Propriedades de serviço adicionais ( `datasource.svc.properties`): Um conjunto de pares de nome/valor que você deseja anexar ao URL da conexão. O tipo de dados é `String[]`.

O serviço JDBC Connections Pool é uma fábrica. Portanto, se você usar um nó `sling:OsgiConfig` para configurar o serviço de conexão, o nome do nó deverá incluir o PID do serviço de fábrica seguido por *`-alias`*. O alias que você usa deve ser exclusivo para todos os nós de configuração desse PID. Um nome de nó de exemplo é `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool`.

![chlimage_1-7](assets/chlimage_1-7a.png)

### Conexão com o banco de dados {#connecting-to-the-database}

Em seu código Java, use o serviço DataSourcePool para obter um objeto `javax.sql.DataSource` para a configuração criada. O serviço DataSourcePool fornece o método `getDataSource` que retorna um objeto `DataSource` para um determinado nome de fonte de dados. Como argumento de método, use o valor da propriedade Datasource Name (ou `datasource.name`) que você especificou para a configuração do Pool de Conexões JDBC.

O seguinte exemplo de código JSP obtém uma instância da fonte de dados hsqldbds, executa um query SQL simples e exibe o número de resultados que são retornados.

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
>Se o método getDataSource lançar uma exceção porque a fonte de dados não foi encontrada, verifique se a configuração do serviço do Pool de Conexões está correta. Verifique os nomes, valores e tipos de dados da propriedade.


>[!NOTE]
>
>Para saber como injetar um DataSourcePool em um pacote OSGi, consulte [Injeção de um serviço DataSourcePool em um pacote OSGi da Adobe Experience Manager](https://helpx.adobe.com/experience-manager/using/datasourcepool.html).

