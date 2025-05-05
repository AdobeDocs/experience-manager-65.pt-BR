---
title: Como configurar o MongoDB para demonstração
description: Como configurar o MSRP para uma instância de autor e uma instância de publicação
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Como configurar o MongoDB para demonstração {#how-to-setup-mongodb-for-demo}

## Introdução {#introduction}

Este tutorial descreve como configurar o [MSRP](msrp.md) para uma instância de *um autor* e uma instância de *uma publicação*.

Com essa configuração, o conteúdo da comunidade pode ser acessado de ambientes do autor e de publicação sem a necessidade de encaminhar ou reverter o conteúdo gerado pelo usuário (UGC) replicado.

Esta configuração é adequada para ambientes de *não produção*, como para desenvolvimento e/ou demonstração.

**Um ambiente de *produção* deve:**

* Executar MongoDB com um conjunto de réplicas
* Usar SolrCloud
* Conter várias instâncias do editor

## MongoDB {#mongodb}

### Instalar MongoDB {#install-mongodb}

* Baixar MongoDB de [https://www.mongodb.com/](https://www.mongodb.com/)

   * Opção de sistema operacional:

      * Linux®
      * Mac 10.8
      * Windows 7

   * Escolha da versão:

      * No mínimo, use a versão 2.6

* Configuração básica

   * Siga as instruções de instalação do MongoDB.
   * Configurar para mongod:

      * Não é necessário configurar mongos ou fragmentação.

   * A pasta MongoDB instalada é chamada &lt;mongo-install>.
   * O caminho do diretório de dados definido é chamado &lt;mongo-dbpath>.

* O MongoDB pode ser executado no mesmo host que o AEM ou remotamente.

### Iniciar MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

Isso inicia um servidor MongoDB usando a porta padrão 27017.

* Para o Mac, aumente o ulimit com o argumento inicial &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se o MongoDB for iniciado *após* o AEM, **reinicie** todas as instâncias de **AEM** para que elas se conectem corretamente ao MongoDB.

### Opção de produção de demonstração: configurar conjunto de réplicas do MongoDB {#demo-production-option-setup-mongodb-replica-set}

Os comandos a seguir são um exemplo de configuração de um conjunto de réplicas com três nós no host local:

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Instalar Solr {#install-solr}

* Baixar Solr de [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adequado para qualquer SO.
   * Solr versão 7.0.
   * Solr requer Java™ 1.7 ou superior.

* Configuração básica

   * Siga o &quot;exemplo&quot; de configuração Solr.
   * Nenhum serviço é necessário.
   * A pasta Solr instalada é chamada &lt;solr-install>.

### Configurar Solr para AEM Communities {#configure-solr-for-aem-communities}

Para configurar uma coleção Solr para MSRP for demo, há duas decisões a serem tomadas (selecione os links para a documentação principal para obter detalhes):

1. Executar Solr em modo autônomo ou [SolrCloud](msrp.md#solrcloudmode).
1. Instale o MLS (pesquisa multilíngue) [padrão](msrp.md#installingstandardmls) ou [avançado](msrp.md#installingadvancedmls).

### Solr independente {#standalone-solr}

O método de execução do Solr pode diferir dependendo da versão e da maneira de instalação. O [Guia de referência Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) é a documentação autoritativa.

Para simplificar, usando a versão 4.10 como exemplo, inicie o Solr no modo independente:

* cd para &lt;solrinstall>/example
* Java™ -jar start.jar

Este processo inicia um servidor HTTP Solr usando a porta padrão 8983. Você pode navegar até o console Solr para obter um console Solr para testes.

* console Solr padrão: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se o Console Solr não estiver disponível, verifique os logs em &lt;solrinstall>/example/logs. Verifique se o SOLR está tentando se vincular a um nome de host específico que não pode ser resolvido (por exemplo, &quot;user-macbook-pro&quot;).
>
>Em caso afirmativo, atualize o arquivo `etc/hosts` com uma nova entrada para esse nome de host (por exemplo, 127.0.0.1 user-macbook-pro) para iniciar Solr corretamente.

### SolrCloud {#solrcloud}

Para executar uma configuração básica (não de produção) solrCloud, inicie solr com:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identificar MongoDB como Armazenamento comum {#identify-mongodb-as-common-store}

Inicie o autor e publique instâncias AEM, se necessário.

Se o AEM estava em execução antes do MongoDB ser iniciado, as instâncias do AEM devem ser reiniciadas.

Siga as instruções na página principal da documentação: [MSRP - Loja Comum MongoDB](msrp.md)

## Testar {#test}

Para testar e verificar o armazenamento comum do MongoDB, publique um comentário na instância de publicação, exiba-o na instância de autor e exiba o UGC no MongoDB e no Solr:

1. Na instância de publicação, navegue até a página [Guia dos Componentes da Comunidade](http://localhost:4503/content/community-components/en/comments.html) e selecione o componente Comentários.
1. Faça logon para publicar um comentário:
1. Insira texto na caixa de entrada de texto de comentário e clique em **[!UICONTROL Post]**

   ![pós-comentário](assets/post-comment.png)

1. Basta exibir o comentário na [instância do autor](http://localhost:4502/content/community-components/en/comments.html) (provavelmente ainda conectado como administrador/administrador).

   ![exibir-comentário](assets/view-comment.png)

   Observação: embora existam nós JCR no *asipath* no autor, esses nós são para a estrutura SCF. O UGC real não está no JCR, ele está no MongoDB.

1. Exibir o UGC no mongodb **[!UICONTROL Comunidades]** > **[!UICONTROL Coleções]** > **[!UICONTROL Conteúdo]**

   ![ugc-content](assets/ugc-content.png)

1. Exibir o UGC no Solr:

   * Navegue até o painel Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Usuário `core selector` para selecionar `collection1`.
   * Selecione `Query`.
   * Selecione `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Resolução de problemas {#troubleshooting}

### Nenhum UGC é exibido {#no-ugc-appears}

1. Verifique se o MongoDB está instalado e em execução corretamente.

1. Verifique se o MSRP foi configurado para ser o provedor padrão:

   * Em todas as instâncias de AEM de autoria e publicação, visite novamente o [console de Configuração de Armazenamento](srp-config.md) ou verifique o repositório AEM:

   * No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) não contiver um nó [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades defaultconfiguration deverão definir MSRP como o provedor padrão.

1. Verifique se o AEM foi reiniciado após a seleção de MSRP.
