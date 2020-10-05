---
title: DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional
seo-title: DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional
description: Configurar a AEM Communities para usar um banco de dados relacional como sua loja comum
seo-description: Configurar a AEM Communities para usar um banco de dados relacional como sua loja comum
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: bbaf9afbf009281c0009bf3895e82988540e15f0
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - Provedor de Recursos de Armazenamento de Banco de Dados Relacional {#dsrp-relational-database-storage-resource-provider}

## Sobre o DSRP {#about-dsrp}

Quando a AEM Communities está configurada para usar um banco de dados relacional como sua loja comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das opções](working-with-srp.md#characteristics-of-srp-options) de SRP e das topologias [](topologies.md)recomendadas.

## Introdução {#requirements}

* [MySQL](#mysql-configuration), um banco de dados relacional.
* [Apache Solr](#solr-configuration), uma plataforma de pesquisa.

>[!NOTE]
>
>A configuração padrão do armazenamento agora é armazenada em conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) em vez de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). É aconselhável seguir as etapas [de](#zerodt-migration-steps) migração para fazer com que os padrões funcionem conforme esperado.


## Configuração de Banco de Dados Relacional {#relational-database-configuration}

### Configuração do MySQL {#mysql-configuration}

Uma instalação do MySQL pode ser compartilhada entre os recursos de ativação e o armazenamento comum (DSRP) no mesmo pool de conexões usando nomes de banco de dados diferentes (schema) e também conexões diferentes (servidor:porta).

Para obter detalhes sobre instalação e configuração, consulte Configuração [MySQL para DSRP](dsrp-mysql.md).

### Configuração de Solr {#solr-configuration}

Uma instalação Solr pode ser compartilhada entre a loja de nós (Oak) e a loja comum (SRP) usando coleções diferentes.

Se as coleções Oak e SRP forem usadas intensamente, uma segunda Solr poderá ser instalada por motivos de desempenho.

Para ambientes de produção, o modo SolrCloud fornece desempenho aprimorado em relação ao modo independente (uma configuração única e local de Solr).

Para obter detalhes sobre instalação e configuração, consulte Configuração [Solr para SRP](solr.md).

### Selecione DSRP {#select-dsrp}

O console [Configuração do](srp-config.md) Armazenamento permite a seleção da configuração padrão do armazenamento, que identifica qual implementação do SRP usar.

Em autor, para acessar o console Configuração do Armazenamento

* Fazer logon com privilégios de administrador
* No menu **principal**

   * Selecione **[!UICONTROL Ferramentas]** (no painel esquerdo)
   * Selecionar **[!UICONTROL comunidades]**
   * Selecionar configuração do **[!UICONTROL Armazenamento]**

      * Como exemplo, o local resultante é: [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >A configuração padrão do armazenamento agora é armazenada em conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) em vez de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). É aconselhável seguir as etapas [de](#zerodt-migration-steps) migração para fazer com que os padrões funcionem conforme esperado.
   ![dsrp-config](assets/dsrp-config.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Configuração do banco de dados**

   * **[!UICONTROL Nome da fonte de dados JDBC]**

      O nome dado à conexão MySQL deve ser o mesmo que foi inserido na configuração [JDBC OSGi](dsrp-mysql.md#configurejdbcconnections)

      *padrão*: comunidades

   * **[!UICONTROL Nome do banco de dados]**

      Nome dado ao schema no script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *padrão*: comunidades

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Host do Zookeeper**

      Deixe esse valor em branco se estiver executando Solr usando o ZooKeeper interno. Caso contrário, ao executar no modo [](solr.md#solrcloud-mode) SolrCloud com um ZooKeeper externo, defina esse valor para o URI do ZooKeeper, como *my.server.com:80*

      *padrão*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *padrão*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Coleção Solr]**

      *padrão*: coleção1

* Selecione **[!UICONTROL Enviar]**.

### Etapas de migração de zero para o padrão srp {#zerodt-migration-steps}

Siga estas etapas para garantir que a página padrão [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) funcione como esperado:

1. Renomeie o caminho em `/etc/socialconfig` para `/etc/socialconfig_old`, para que a configuração do sistema volte para jsrp (padrão).
1. Vá para a página padrão [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), onde jsrp está configurado. Clique no botão **[!UICONTROL enviar]** para que o novo nó de configuração padrão seja criado em `/conf/global/settings/community/srpc`.
1. Exclua a configuração padrão criada `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copie a configuração antiga `/etc/socialconfig_old/srpc/defaultconfiguration` no lugar do nó excluído (`/conf/global/settings/community/srpc/defaultconfiguration`) na etapa anterior.
1. Exclua o nó antigo etc `/etc/socialconfig_old`.

## Publicar a configuração {#publishing-the-configuration}

O DSRP deve ser identificado como o repositório comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente publish:

* Autor:

   * Navegue do menu principal até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**
   * Dê um clique duplo para **[!UICONTROL Ativar a árvore]**
   * **Caminho de início**:

      * Navegue até `/etc/socialconfig/srpc/`
   * Verifique se não `Only Modified` está selecionado.
   * Selecione **[!UICONTROL Ativar]**.


## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, perfis *de* usuários e grupos *de* usuários, normalmente inseridos no ambiente de publicação, visite:

* [Sincronização do usuário](sync.md)
* [Gerenciamento de usuários e grupos de usuários](users.md)

## Reindexação do Solr para DSRP {#reindexing-solr-for-dsrp}

Para reindexar o DSRP Solr, siga a documentação para [reindexar o MSRP](msrp.md#msrp-reindex-tool); no entanto, ao reindexar o DSRP, use este URL: **/services/social/datastore/rdb/reindex**

Por exemplo, um comando curl para reindexar o DSRP seria semelhante a:

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

