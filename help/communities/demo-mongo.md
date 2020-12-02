---
title: Como configurar o MongoDB para demonstração
seo-title: Como configurar o MongoDB para demonstração
description: Como configurar o MSRP para uma instância de autor e uma instância de publicação
seo-description: Como configurar o MSRP para uma instância de autor e uma instância de publicação
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Como configurar o MongoDB para demonstração {#how-to-setup-mongodb-for-demo}

## Introdução {#introduction}

Este tutorial descreve como configurar [MSRP](msrp.md) para a instância *um autor* e *uma instância publish*.

Com essa configuração, o conteúdo da comunidade pode ser acessado de ambientes de autor e publicação sem a necessidade de reproduzir ou reverter o conteúdo gerado pelo usuário (UGC).

Essa configuração é adequada para ambientes *que não são de produção*, como para desenvolvimento e/ou demonstração.

**Um ambiente  ** de produção deve:**

* Executar MongoDB com um conjunto de réplicas
* Usar a SolrCloud
* Conter várias instâncias do editor

## MongoDB {#mongodb}

### Instalar MongoDB {#install-mongodb}

* Baixe o MongoDB de [https://www.mongodb.org/](https://www.mongodb.org/)

   * Opção de SO:

      * Linux
      * Mac 10.8
      * Windows 7
   * Escolha da versão:

      * No mínimo, use a versão 2.6


* Configuração básica

   * Siga as instruções de instalação do MongoDB.
   * Configurar para mondeus:

      * Não há necessidade de configurar mongos ou o compartilhamento.
   * A pasta MongoDB instalada será chamada de &lt;mongo-install>.
   * O caminho do diretório de dados definido será conhecido como &lt;mongo-dbpath>.


* O MongoDB pode ser executado no mesmo host que AEM ou ser executado remotamente.

### Start MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mondeus —dbpath  &lt;mongo-dbpath>

Isso start um servidor MongoDB usando a porta padrão 27017.

* Para Mac, aumente o limite com o start arg &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Se MongoDB for iniciado *depois de* AEM, **reinicie** todas as instâncias **AEM** para que se conectem corretamente ao MongoDB.

### Opção de produção de demonstração: Configurar Conjunto de Réplicas MongoDB {#demo-production-option-setup-mongodb-replica-set}

Os comandos a seguir são um exemplo de como configurar um conjunto de réplicas com 3 nós em localhost:

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

### Instalar o Solr {#install-solr}

* Baixe o Solr de [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adequado para qualquer SO.
   * Versão 7.0 do Solr.
   * A Solr requer Java 1.7 ou superior.

* Configuração básica

   * Siga a configuração do Solr &#39;example&#39;.
   * Nenhum serviço é necessário.
   * A pasta Solr instalada será chamada de &lt;solr-install>.

### Configure o Solr para AEM Communities {#configure-solr-for-aem-communities}

Para configurar uma coleção Solr para MSRP para demonstração, há duas decisões a serem tomadas (selecione os links para a documentação principal para obter detalhes):

1. Execute o Solr independente ou [modo SolrCloud](msrp.md#solrcloudmode).
1. Instale [standard](msrp.md#installingstandardmls) ou [pesquisa avançada](msrp.md#installingadvancedmls) multilingue (MLS).

### Solar independente {#standalone-solr}

O método para executar Solr pode diferir dependendo da versão e da maneira de instalação. O [guia de referência Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) é a documentação autoritativa.

Para simplificar, usando a versão 4.10 como exemplo, start Solr no modo independente:

* cd para &lt;solrinstall>/example
* java - jar start.jar

Isso start um servidor HTTP Solr usando a porta padrão 8983. Você pode navegar até o console Solr para obter um console Solr para teste.

* console padrão Solr: [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Se o Solr Console não estiver disponível, verifique os registros em &lt;solrinstall>/example/logs. Verifique se o SOLR está tentando se ligar a um nome de host específico que não pode ser resolvido (por exemplo, &quot;user-macbook-pro&quot;).
Em caso positivo, atualize o arquivo etc/hosts com uma nova entrada para esse nome de host (por exemplo, 127.0.0.1 user-macbook-pro) e o Solr será start corretamente.

### SolrCloud {#solrcloud}

Para executar uma configuração muito básica (e não de produção) da solrCloud, use a proteção de start com:

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identifique MongoDB como Repositório Comum {#identify-mongodb-as-common-store}

Inicie o autor e publique AEM instâncias, se necessário.

Se AEM estava sendo executado antes do MongoDB ser iniciado, as instâncias AEM precisarão ser reiniciadas.

Siga as instruções na página principal da documentação: [MSRP - MongoDB Common Store](msrp.md)

## Testar {#test}

Para testar e verificar a loja comum MongoDB, poste um comentário na instância de publicação e a visualização na instância do autor, bem como a visualização do UGC no MongoDB e no Solr:

1. Na instância de publicação, navegue até a página [Guia de componentes da comunidade](http://localhost:4503/content/community-components/en/comments.html) e selecione o componente Comentários.
1. Faça logon para postar um comentário:
1. Digite o texto na caixa de entrada de texto do comentário e clique em **[!UICONTROL Post]**

   ![post-comment](assets/post-comment.png)

1. Basta visualização o comentário na [instância do autor](http://localhost:4502/content/community-components/en/comments.html) (provavelmente ainda está conectado como admin / admin).

   ![visualização](assets/view-comment.png)

   Observação: Embora existam nós JCR sob o *asipath* no autor, eles são para a estrutura SCF. O UGC real não está no JCR, está no MongoDB.

1. Visualização o UGC em monGodb **[!UICONTROL Communities]** > **[!UICONTROL Coleções]** > **[!UICONTROL Conteúdo]**

   ![conteúdo de ugc](assets/ugc-content.png)

1. Visualização o UGC no Solr:

   * Navegue até Solr painel: [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Usuário `core selector` para selecionar `collection1`.
   * Selecionar `Query`.
   * Selecionar `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Resolução de problemas {#troubleshooting}

### Nenhum UGC é exibido {#no-ugc-appears}

1. Verifique se o MongoDB está instalado e em execução corretamente.

1. Verifique se o MSRP foi configurado para ser o provedor padrão:

   * Em todas as instâncias de autor e publicação AEM, revisite o [console de Configuração do Armazenamento](srp-config.md) ou verifique o repositório AEM:

   * No JCR, se [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) não contiver um nó [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), isso significa que o provedor do armazenamento é JSRP.
   * Se o nó srpc existir e contiver o nó [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), as propriedades da configuração default deverão definir MSRP como o provedor padrão.

1. Verifique se AEM foi reiniciado após a seleção do MSRP.
