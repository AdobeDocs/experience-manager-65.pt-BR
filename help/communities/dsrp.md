---
title: DSRP - Provedor de Recurso de Armazenamento de Banco de Dados Relacional
description: Configurar o AEM Communities para usar um banco de dados relacional como seu armazenamento comum
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# DSRP - Provedor de Recurso de Armazenamento de Banco de Dados Relacional {#dsrp-relational-database-storage-resource-provider}

## Sobre o DSRP {#about-dsrp}

Quando o AEM Communities é configurado para usar um banco de dados relacional como armazenamento comum, o conteúdo gerado pelo usuário (UGC) pode ser acessado de todas as instâncias de criação e publicação sem a necessidade de sincronização ou replicação.

Consulte também [Características das opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Requisitos {#requirements}

* [MySQL](#mysql-configuration), um banco de dados relacional.
* [Apache Solr](#solr-configuration), uma plataforma de pesquisa.

>[!NOTE]
>
>A configuração de armazenamento padrão agora é armazenada em conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) em vez de `etc` caminho (`/etc/socialconfig/srpc/defaultconfiguration`). É recomendável seguir as instruções do [etapas de migração](#zerodt-migration-steps) para fazer com que o defaultsrp funcione conforme esperado.

## Configuração de Banco de Dados Relacional {#relational-database-configuration}

### Configuração do MySQL {#mysql-configuration}

Uma instalação do MySQL pode ser compartilhada entre os recursos de ativação e o armazenamento comum (DSRP) no mesmo pool de conexões usando nomes de banco de dados (esquema) diferentes e também conexões diferentes (servidor:porta).

Para obter detalhes sobre a instalação e a configuração, consulte [Configuração do MySQL para DSRP](dsrp-mysql.md).

### Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (SRP) usando coleções diferentes.

Se as coleções Oak e SRP forem usadas intensamente, um segundo Solr pode ser instalado por motivos de desempenho.

Para ambientes de produção, o modo SolrCloud fornece desempenho aprimorado em relação ao modo independente (uma configuração Solr única e local).

Para obter detalhes sobre a instalação e a configuração, consulte [Configuração Solr para SRP](solr.md).

### Selecionar DSRP {#select-dsrp}

A variável [Console de configuração de armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

Na criação, para acessar o console Configuração de armazenamento

* Entrar com privilégios de administrador
* No **menu principal**

   * Selecionar **[!UICONTROL Ferramentas]** (no painel esquerdo)
   * Selecionar **[!UICONTROL Communities]**
   * Selecionar **[!UICONTROL Configuração de armazenamento]**

      * Como exemplo, o local resultante é: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >A configuração de armazenamento padrão agora é armazenada em conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) em vez de `etc` caminho (`/etc/socialconfig/srpc/defaultconfiguration`). É recomendável seguir as instruções do [etapas de migração](#zerodt-migration-steps) para fazer com que o defaultsrp funcione conforme esperado.

  ![dsrp-config](assets/dsrp-config.png)

* Selecionar **[!UICONTROL Provedor do recurso de armazenamento do banco de dados (DSRP, Database Storage Resource Provider)]**
* **Configuração do banco de dados**

   * **[!UICONTROL Nome da fonte de dados JDBC]**

     O nome fornecido para a conexão MySQL deve ser igual ao inserido em [Configuração OSGi do JDBC](dsrp-mysql.md#configurejdbcconnections)

     *padrão*: comunidades

   * **[!UICONTROL Nome do banco de dados]**

     Nome dado ao esquema em [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *padrão*: comunidades

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) Host**

     Deixe esse valor em branco se estiver executando o Solr usando o ZooKeeper interno. Senão, ao executar em [Modo SolrCloud](solr.md#solrcloud-mode) com um ZooKeeper externo, defina este valor para o URI do ZooKeeper, como *my.server.com:80*

     *padrão*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

     *padrão*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Coleção Solr]**

     *padrão*: coleção1

* Selecione **[!UICONTROL Enviar]**.

### Nenhuma etapa de migração de tempo de inatividade para defaultsrp {#zerodt-migration-steps}

Para garantir que a página defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funcionar conforme esperado, siga estas etapas:

1. Renomear o caminho em `/etc/socialconfig` para `/etc/socialconfig_old`, para que a configuração do sistema retorne ao jsrp(padrão).
1. Ir para a página defaultsrp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), em que jsrp está configurado. Clique em **[!UICONTROL enviar]** para que o novo nó de configuração padrão seja criado em `/conf/global/settings/community/srpc`.
1. Excluir a configuração padrão criada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiar a configuração antiga `/etc/socialconfig_old/srpc/defaultconfiguration` no lugar do nó excluído (`/conf/global/settings/community/srpc/defaultconfiguration`) na etapa anterior.
1. Excluir o antigo `etc` nó `/etc/socialconfig_old`.

## Publicar a configuração {#publishing-the-configuration}

O DSRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação:

* No autor:

   * Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**
   * Clique duas vezes **[!UICONTROL Ativar árvore]**
   * **Caminho inicial**:

      * Navegue até `/etc/socialconfig/srpc/`

   * Assegurar `Only Modified` não está selecionado.
   * Selecionar **[!UICONTROL Ativar]**.

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, frequentemente inseridos no ambiente de publicação, visitem:

* [Sincronização de usuário](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Reindexação de Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar DSRP Solr, siga a documentação para [reindexação de MSRP](msrp.md#msrp-reindex-tool)No entanto, ao reindexar para DSRP, use este URL em vez de: **/services/social/datastore/rdb/reindex**

Por exemplo, um comando curl para reindexar DSRP seria semelhante a:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
