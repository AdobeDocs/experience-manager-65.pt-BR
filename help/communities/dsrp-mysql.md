---
title: Configuração do MySQL para DSRP
seo-title: MySQL Configuration for DSRP
description: Como se conectar ao servidor MySQL e estabelecer o banco de dados UGC
seo-description: How to connect to the MySQL server and establish the UGC database
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Configuração do MySQL para DSRP {#mysql-configuration-for-dsrp}

O MySQL é um banco de dados relacional que pode ser usado para armazenar conteúdo gerado pelo usuário (UGC).

Essas instruções descrevem como se conectar ao servidor MySQL e estabelecer o banco de dados UGC.

## Requisitos {#requirements}

* [Pacote de recursos das Comunidades mais recentes](deploy-communities.md#latestfeaturepack)
* [Driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Um banco de dados relacional:

   * [Servidor MySQL](https://dev.mysql.com/downloads/mysql/) Community Server versão 5.6 ou posterior

      * Pode ser executado no mesmo host que o AEM ou remotamente
   * [Workbench do MySQL](https://dev.mysql.com/downloads/tools/workbench/)


## Instalar o MySQL {#installing-mysql}

[MySQL](https://dev.mysql.com/downloads/mysql/) deve ser baixado e instalado seguindo as instruções para o SO de destino.

### Nomes de tabela em minúsculas {#lower-case-table-names}

Como o SQL não diferencia maiúsculas de minúsculas, para sistemas operacionais que diferenciam maiúsculas de minúsculas, é necessário incluir uma configuração para colocar em minúsculas todos os nomes de tabela.

Por exemplo, para especificar todos os nomes de tabela em minúsculas em um sistema operacional Linux:

* Editar arquivo `/etc/my.cnf`
* No `[mysqld]` adicione a seguinte linha:

   `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para fornecer melhor suporte multilíngue, é necessário usar o conjunto de caracteres UTF8.

Altere o MySQL para ter UTF8 como seu conjunto de caracteres:

* mysql > SET NAMES &#39;utf8&#39;;

Altere o banco de dados MySQL para o padrão UTF8:

* Editar arquivo `/etc/my.cnf`
* No `[client]` adicione a seguinte linha:

   `default-character-set=utf8`

* No `[mysqld]` adicione a seguinte linha:

   `character-set-server=utf8`

## Instalando o MySQL Workbench {#installing-mysql-workbench}

O MySQL Workbench fornece uma interface para executar scripts SQL que instalam o esquema e os dados iniciais.

O MySQL Workbench deve ser baixado e instalado seguindo as instruções para o SO de destino.

## Conexão das comunidades {#communities-connection}

Quando o MySQL Workbench é iniciado pela primeira vez, a menos que já esteja em uso para outros propósitos, ele ainda não mostrará nenhuma conexão:

![mysqlconnection](assets/mysqlconnection.png)

### Novas Configurações de Conexão {#new-connection-settings}

1. Selecione o `+` ícone à direita de `MySQL Connections`.
1. No diálogo `Setup New Connection`, insira os valores apropriados para sua plataforma

   Para fins de demonstração, com a instância AEM do autor e o MySQL no mesmo servidor:

   * Nome da conexão: `Communities`
   * Método de Conexão: `Standard (TCP/IP)`
   * Nome do host: `127.0.0.1`
   * Nome de usuário: `root`
   * Senha: `no password by default`
   * Esquema padrão: `leave blank`

1. Selecionar `Test Connection` para verificar a conexão com o serviço MySQL em execução

**Notas**:

* A porta padrão é `3306`
* O Nome da Conexão escolhido é inserido como o nome da origem de dados em [Configuração OSGi do JDBC](#configurejdbcconnections)

#### Nova conexão das comunidades {#new-communities-connection}

![conexão de comunidade](assets/community-connection.png)

## Configuração do Banco de Dados {#database-setup}

Abra a conexão Comunidades para instalar o banco de dados.

![install-database](assets/install-database.png)

### Obter o script SQL {#obtain-the-sql-script}

O script SQL é obtido do repositório AEM:

1. Navegar até o CRXDE Lite

   * Por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Selecione a pasta /libs/social/config/datastore/dsrp/schema
1. Download `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

Um método para baixar o esquema é:

* Selecione o `jcr:content` nó do arquivo sql
* Observe o valor para o `jcr:data` a propriedade é um link de exibição

* Selecione o link de exibição para salvar os dados em um arquivo local

### Criar o banco de dados DSRP {#create-the-dsrp-database}

Siga as etapas abaixo para instalar o banco de dados. O nome padrão do banco de dados é `communities`.

Se o nome do banco de dados for alterado no script, altere-o também no campo [Configuração do JDBC](#configurejdbcconnections).

#### Etapa 1: abrir arquivo SQL {#step-open-sql-file}

No MySQL Workbench

* No menu suspenso Arquivo, selecione a **[!UICONTROL Abrir Script SQL]** opção
* Selecione o baixado `init_schema.sql` script

![select-sql-script](assets/select-sql-script.png)

#### Etapa 2: executar Script SQL {#step-execute-sql-script}

Na janela Workbench para o arquivo aberto na Etapa 1, selecione o `lightening (flash) icon` para executar o script.

Na imagem a seguir, a variável `init_schema.sql` O arquivo está pronto para ser executado:

![execute-sql-script](assets/execute-sql-script.png)

#### Atualizar {#refresh}

Depois que o script for executado, será necessário atualizar o `SCHEMAS` seção do `Navigator` para ver o novo banco de dados. Use o ícone de atualização à direita de &#39;SCHEMAS&#39;:

![refresh-schema](assets/refresh-schema.png)

## Configurar conexão JDBC {#configure-jdbc-connection}

A configuração do OSGi para **Pool de Conexões JDBC do Day Commons** configura o driver JDBC do MySQL.

Todas as instâncias AEM de publicação e de criação devem apontar para o mesmo servidor MySQL.

Quando o MySQL é executado em um servidor diferente do AEM, o nome do host do servidor deve ser especificado no lugar de &quot;localhost&quot; no conector JDBC.

* Em cada autor e instância de AEM publicada.
* Conectado com privilégios de administrador.
* Acesse o [console da web](../../help/sites-deploying/configuring-osgi.md).

   * Por exemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Localize o `Day Commons JDBC Connections Pool`
* Selecione o `+` ícone para criar uma nova configuração de conexão.

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* Insira os seguintes valores:

   * **[!UICONTROL Classe de driver JDBC]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI da conexão JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      Especificar servidor no lugar de localhost se o servidor MySQL não for o mesmo que &#39;este&#39; servidor AEM *comunidades* é o nome do banco de dados padrão (esquema).

   * **[!UICONTROL Nome de usuário]**: `root`

      Ou insira o Nome de usuário configurado para o servidor MySQL, se não for &#39;root&#39;.

   * **[!UICONTROL Senha]**:

      Limpar este campo se nenhuma senha for definida para o MySQL,

      caso contrário, digite a senha configurada para o Nome de usuário do MySQL.

   * **[!UICONTROL Nome da fonte de dados]**: nome inserido para o [Conexão MySQL](#new-connection-settings), por exemplo, &quot;comunidades&quot;.

* Selecione **[!UICONTROL Salvar]**
