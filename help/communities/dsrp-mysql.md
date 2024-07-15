---
title: Configuração do MySQL para DSRP
description: Como se conectar ao servidor MySQL e estabelecer o banco de dados UGC
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Configuração do MySQL para DSRP {#mysql-configuration-for-dsrp}

O MySQL é um banco de dados relacional que pode ser usado para armazenar conteúdo gerado pelo usuário (UGC).

Essas instruções descrevem como se conectar ao servidor MySQL e estabelecer o banco de dados UGC.

## Requisitos {#requirements}

* [Pacote de recursos das Comunidades mais recentes](deploy-communities.md#latestfeaturepack)
* [Driver JDBC para MySQL](deploy-communities.md#jdbc-driver-for-mysql)
* Um banco de dados relacional:

   * [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server versão 5.6 ou posterior

      * Pode ser executado no mesmo host que o AEM ou remotamente

   * [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/)

## Instalar o MySQL {#installing-mysql}

O [MySQL](https://dev.mysql.com/downloads/mysql/) deve ser baixado e instalado seguindo as instruções para o sistema operacional de destino.

### Nomes de tabela em minúsculas {#lower-case-table-names}

Como o SQL não diferencia maiúsculas de minúsculas, para sistemas operacionais que diferenciam maiúsculas de minúsculas, é necessário incluir uma configuração para colocar em minúsculas todos os nomes de tabela.

Por exemplo, para especificar todos os nomes de tabela em minúsculas em um sistema operacional Linux:

* Editar arquivo `/etc/my.cnf`
* Na seção `[mysqld]`, adicione a seguinte linha:

  `lower_case_table_names = 1`

### Conjunto de caracteres UTF8 {#utf-character-set}

Para fornecer melhor suporte multilíngue, é necessário usar o conjunto de caracteres UTF8.

Altere o MySQL para ter UTF8 como seu conjunto de caracteres:

* mysql > SET NAMES &#39;utf8&#39;;

Altere o banco de dados MySQL para o padrão UTF8:

* Editar arquivo `/etc/my.cnf`
* Na seção `[client]`, adicione a seguinte linha:

  `default-character-set=utf8`

* Na seção `[mysqld]`, adicione a seguinte linha:

  `character-set-server=utf8`

## Instalando o MySQL Workbench {#installing-mysql-workbench}

O MySQL Workbench fornece uma interface para executar scripts SQL que instalam o esquema e os dados iniciais.

O MySQL Workbench deve ser baixado e instalado seguindo as instruções para o SO de destino.

## Conexão das comunidades {#communities-connection}

Quando o MySQL Workbench é iniciado pela primeira vez, a menos que já esteja em uso para outros propósitos, ele ainda não mostrará nenhuma conexão:

![mysqlconnection](assets/mysqlconnection.png)

### Novas Configurações de Conexão {#new-connection-settings}

1. Selecione o ícone `+` à direita de `MySQL Connections`.
1. Na caixa de diálogo `Setup New Connection`, insira os valores apropriados para sua plataforma

   Para fins de demonstração, com a instância AEM do autor e o MySQL no mesmo servidor:

   * Nome da Conexão: `Communities`
   * Método de Conexão: `Standard (TCP/IP)`
   * Nome do host: `127.0.0.1`
   * Nome de Usuário: `root`
   * Senha: `no password by default`
   * Esquema Padrão: `leave blank`

1. Selecione `Test Connection` para verificar a conexão com o serviço MySQL em execução

**Notas**:

* A porta padrão é `3306`
* O Nome da Conexão escolhido é inserido como o nome da fonte de dados na [configuração OSGi JDBC](#configurejdbcconnections)

#### Nova conexão das comunidades {#new-communities-connection}

![conexão-comunidade](assets/community-connection.png)

## Configuração do Banco de Dados {#database-setup}

Abra a conexão Communities para instalar o banco de dados.

![instalar-banco-de-dados](assets/install-database.png)

### Obter o script SQL {#obtain-the-sql-script}

O script SQL é obtido do repositório AEM:

1. Navegar até o CRXDE Lite

   * Por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Selecione a pasta /libs/social/config/datastore/dsrp/schema
1. Baixar `init-schema.sql`

   ![esquema-banco-de-dados-crxde](assets/database-schema-crxde.png)

Um método para baixar o esquema é:

* Selecione o nó `jcr:content` para o arquivo sql
* Observe que o valor da propriedade `jcr:data` é um link de exibição

* Selecione o link de exibição para salvar os dados em um arquivo local

### Criar o banco de dados DSRP {#create-the-dsrp-database}

Siga as etapas abaixo para instalar o banco de dados. O nome padrão do banco de dados é `communities`.

Se o nome do banco de dados for alterado no script, altere-o também na [configuração do JDBC](#configurejdbcconnections).

#### Etapa 1: abrir arquivo SQL {#step-open-sql-file}

No MySQL Workbench

* No menu suspenso Arquivo, selecione a opção **[!UICONTROL Abrir Script SQL]**
* Selecionar o script `init_schema.sql` baixado

![select-sql-script](assets/select-sql-script.png)

#### Etapa 2: executar Script SQL {#step-execute-sql-script}

Na janela Workbench do arquivo aberto na Etapa 1, selecione o `lightening (flash) icon` para executar o script.

Na imagem a seguir, o arquivo `init_schema.sql` está pronto para ser executado:

![executar-sql-script](assets/execute-sql-script.png)

#### Atualizar {#refresh}

Depois que o script for executado, será necessário atualizar a seção `SCHEMAS` de `Navigator` para ver o novo banco de dados. Use o ícone de atualização à direita de &#39;SCHEMAS&#39;:

![atualizar-esquema](assets/refresh-schema.png)

## Configurar conexão JDBC {#configure-jdbc-connection}

A configuração OSGi do **Pool de Conexões JDBC do Day Commons** configura o Driver JDBC do MySQL.

Todas as instâncias AEM de publicação e de criação devem apontar para o mesmo servidor MySQL.

Quando o MySQL é executado em um servidor diferente do AEM, o nome do host do servidor deve ser especificado no lugar de &quot;localhost&quot; no conector JDBC.

* Em cada autor e instância de AEM publicada.
* Conectado com privilégios de administrador.
* Acesse o [console da Web](../../help/sites-deploying/configuring-osgi.md).

   * Por exemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* Localizar o `Day Commons JDBC Connections Pool`
* Selecione o ícone `+` para criar uma configuração de conexão.

  ![configurar-jdbc-conexão](assets/configure-jdbc-connection.png)

* Insira os seguintes valores:

   * **[!UICONTROL classe de driver JDBC]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL URI de conexão JDBC]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     Especifique o servidor no lugar de localhost se o servidor MySQL não for o mesmo que &#39;este&#39; servidor AEM *comunidades* for o nome padrão do banco de dados (esquema).

   * **[!UICONTROL Nome de Usuário]**: `root`

     Ou insira o Nome de usuário configurado para o servidor MySQL, se não for &#39;root&#39;.

   * **[!UICONTROL Senha]**:

     Limpar este campo se nenhuma senha for definida para o MySQL,

     caso contrário, digite a senha configurada para o Nome de usuário do MySQL.

   * **[!UICONTROL Nome da fonte de dados]**: nome inserido para a [conexão MySQL](#new-connection-settings), por exemplo, &#39;comunidades&#39;.

* Selecione **[!UICONTROL Salvar]**
