---
title: Como configurar o MongoDB para demonstração
description: Como configurar o MSRP para uma instância de autor e uma instância de publicação
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# Como configurar o MongoDB para demonstração {#how-to-setup-mongodb-for-demo}

## Introdução {#introduction}

Este tutorial descreve como configurar [MSRP](msrp.md) para *um autor* instância e *uma publicação* instância.

Com essa configuração, o conteúdo da comunidade pode ser acessado de ambientes do autor e de publicação sem a necessidade de encaminhar ou reverter o conteúdo gerado pelo usuário (UGC) replicado.

Essa configuração é adequada para *não produção* ambientes como para desenvolvimento e/ou demonstração.

**A *produção* O ambiente deve:**

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

* &lt;mongo-install>/bin/mongod — dbpath &lt;mongo-dbpath>

Isso inicia um servidor MongoDB usando a porta padrão 27017.

* Para o Mac, aumente o ulimit com o argumento inicial &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB for iniciado *após* AEM **reiniciar** all **AEM** para que se conectem corretamente ao MongoDB.

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

1. Executar Solr em independente ou [Modo SolrCloud](msrp.md#solrcloudmode).
1. Instalar [padrão](msrp.md#installingstandardmls) ou [avançado](msrp.md#installingadvancedmls) pesquisa multilíngue (MLS).

### Solr independente {#standalone-solr}

O método de execução do Solr pode diferir dependendo da versão e da maneira de instalação. A variável [Guia de referência de Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) O é a documentação autoritativa.

Para simplificar, usando a versão 4.10 como exemplo, inicie o Solr no modo independente:

* cd para &lt;solrinstall>/exemplo
* Java™ -jar start.jar

Este processo inicia um servidor HTTP Solr usando a porta padrão 8983. Você pode navegar até o console Solr para obter um console Solr para testes.

* console Solr padrão: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se o Console Solr não estiver disponível, verifique os logs em &lt;solrinstall>/example/logs. Verifique se o SOLR está tentando se vincular a um nome de host específico que não pode ser resolvido (por exemplo, &quot;user-macbook-pro&quot;).
>
Em caso afirmativo, atualize `etc/hosts` com uma nova entrada para esse nome de host (por exemplo, 127.0.0.1 user-macbook-pro) para iniciar Solr corretamente.

### SolrCloud {#solrcloud}

Para executar uma configuração básica (não de produção) solrCloud, inicie solr com:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identificar MongoDB como Armazenamento comum {#identify-mongodb-as-common-store}

Inicie o autor e publique instâncias AEM, se necessário.

Se o AEM estava em execução antes do MongoDB ser iniciado, as instâncias do AEM devem ser reiniciadas.

Siga as instruções na página principal da documentação: [MSRP - Armazenamento comum do MongoDB](msrp.md)

## Testar {#test}

Para testar e verificar o armazenamento comum do MongoDB, publique um comentário na instância de publicação, exiba-o na instância de autor e exiba o UGC no MongoDB e no Solr:

1. Na instância de publicação, navegue até o [Guia de componentes da comunidade](http://localhost:4503/content/community-components/en/comments.html) e selecione o componente Comentários.
1. Faça logon para publicar um comentário:
1. Insira o texto na caixa de entrada de texto do comentário e clique em **[!UICONTROL Publicar]**

   ![pós-comentário](assets/post-comment.png)

1. Basta visualizar o comentário no [instância do autor](http://localhost:4502/content/community-components/en/comments.html) (provavelmente ainda conectado como administrador/administrador).

   ![exibir-comentário](assets/view-comment.png)

   Observação: embora existam nós JCR no *asipath* na criação, esses nós são para a estrutura SCF. O UGC real não está no JCR, ele está no MongoDB.

1. Visualizar o UGC no mongodb **[!UICONTROL Communities]** > **[!UICONTROL Coleções]** > **[!UICONTROL Conteúdo]**

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

   * Em todas as instâncias de AEM do autor e de publicação, revisite a [Console de configuração de armazenamento](srp-config.md)ou verifique o repositório AEM:

   * No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) não contém um [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) significa que o provedor de armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades defaultconfiguration devem definir o MSRP como o provedor padrão.

1. Verifique se o AEM foi reiniciado após a seleção de MSRP.
