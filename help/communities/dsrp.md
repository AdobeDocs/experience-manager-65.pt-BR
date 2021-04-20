---
title: DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional
seo-title: DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional
description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
seo-description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 3%

---


# DSRP - Provedor de Recursos de Armazenamento do Banco de Dados Relacional {#dsrp-relational-database-storage-resource-provider}

## Sobre o DSRP {#about-dsrp}

Quando o AEM Communities é configurado para usar um banco de dados relacional como armazenamento comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das Opções de SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](topologies.md).

## Requisitos {#requirements}

* [MySQL](#mysql-configuration), um banco de dados relacional.
* [Apache Solr](#solr-configuration), uma plataforma de pesquisa.

>[!NOTE]
>
>A configuração de armazenamento padrão agora é armazenada em conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) em vez de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). É recomendável seguir as [etapas de migração](#zerodt-migration-steps) para fazer com que os padrões funcionem conforme esperado.

## Configuração do Banco de Dados Relacional {#relational-database-configuration}

### Configuração do MySQL {#mysql-configuration}

Uma instalação do MySQL pode ser compartilhada entre os recursos de ativação e o armazenamento comum (DSRP) no mesmo pool de conexões usando nomes de banco de dados diferentes (esquema) e também conexões diferentes (servidor:porta).

Para obter detalhes de instalação e configuração, consulte [Configuração do MySQL para DSRP](dsrp-mysql.md).

### Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre o armazenamento de nós (Oak) e o armazenamento comum (SRP) usando diferentes coleções.

Se as coleções Oak e SRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o modo SolrCloud fornece desempenho aprimorado em relação ao modo independente (uma configuração única e local Solr).

Para obter detalhes de instalação e configuração, consulte [Configuração Solr para SRP](solr.md).

### Selecione DSRP {#select-dsrp}

O [console Configuração de Armazenamento](srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação do SRP usar.

Na criação, para acessar o console Configuração de armazenamento

* Fazer logon com privilégios de administrador
* No **menu principal**

   * Selecione **[!UICONTROL Ferramentas]** (no painel esquerdo)
   * Selecione **[!UICONTROL Comunidades]**
   * Selecione **[!UICONTROL Configuração de Armazenamento]**

      * Como exemplo, o local resultante é: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >A configuração de armazenamento padrão agora é armazenada no caminho conf(`/conf/global/settings/community/srpc/defaultconfiguration`)      em vez de caminho etc (`/etc/socialconfig/srpc/defaultconfiguration`). É recomendável seguir as [etapas de migração](#zerodt-migration-steps) para fazer com que os padrões funcionem conforme esperado.
   ![dsrp-config](assets/dsrp-config.png)

* Selecione **[!UICONTROL Provedor de Recursos de Armazenamento de Banco de Dados (DSRP)]**
* **Configuração do banco de dados**

   * **[!UICONTROL Nome da fonte de dados JDBC]**

      O nome fornecido para a conexão MySQL deve ser igual ao inserido em [Configuração JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *padrão*: comunidades

   * **[!UICONTROL Nome do banco de dados]**

      Nome dado ao schema no script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *padrão*: comunidades

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host do Zookeeper**

      Deixe esse valor em branco se estiver executando Solr usando o ZooKeeper interno. Caso contrário, ao executar no modo [SolrCloud](solr.md#solrcloud-mode) com um ZooKeeper externo, defina esse valor para o URI do ZooKeeper, como *my.server.com:80*

      *padrão*:  *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *padrão*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Coleção Solr]**

      *padrão*: collection1

* Selecione **[!UICONTROL Enviar]**.

### Etapas de migração de tempo de inatividade zero para defaultsrp {#zerodt-migration-steps}

Siga estas etapas para garantir que a página padrão srp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funcione conforme esperado:

1. Renomeie o caminho em `/etc/socialconfig` para `/etc/socialconfig_old`, para que a configuração do sistema volte para jsrp (padrão).
1. Vá para a página padrão srp [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), onde jsrp está configurado. Clique no botão **[!UICONTROL submit]** para que o novo nó de configuração padrão seja criado em `/conf/global/settings/community/srpc`.
1. Exclua a configuração padrão criada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copie a configuração antiga `/etc/socialconfig_old/srpc/defaultconfiguration` no lugar do nó excluído (`/conf/global/settings/community/srpc/defaultconfiguration`) na etapa anterior.
1. Exclua o nó etc antigo `/etc/socialconfig_old`.

## Publicar a configuração {#publishing-the-configuration}

O DSRP deve ser identificado como a loja comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação:

* No autor:

   * Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**
   * Dê um clique duplo para **[!UICONTROL Ativar a árvore]**
   * **Caminho de início**:

      * Navegue até `/etc/socialconfig/srpc/`
   * Certifique-se de que `Only Modified` não esteja selecionado.
   * Selecione **[!UICONTROL Ativar]**.


## Gerenciando dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, normalmente inseridos no ambiente de publicação, visite:

* [Sincronização de usuários](sync.md)
* [Gerenciar usuários e grupos de usuários](users.md)

## Reindexando Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar o DSRP Solr, siga a documentação para [reindexando o MSRP](msrp.md#msrp-reindex-tool). No entanto, ao reindexar para DSRP, use este URL: **/services/social/datastore/rdb/reindex**

Por exemplo, um comando curl para reindexar o DSRP seria semelhante a:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

