---
title: Como acessar programaticamente o JCR AEM
seo-title: Como acessar programaticamente o JCR AEM
description: Você pode modificar programaticamente os nós e as propriedades localizados no repositório do AEM, que faz parte da Adobe Marketing Cloud
seo-description: Você pode modificar programaticamente os nós e as propriedades localizados no repositório do AEM, que faz parte da Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970

---


# Como acessar programaticamente o JCR AEM{#how-to-programmatically-access-the-aem-jcr}

Você pode modificar programaticamente os nós e as propriedades localizados no repositório do Adobe CQ, que faz parte da Adobe Marketing Cloud. Para acessar o repositório do CQ, use a API Java Content Repository (JCR). Você pode usar a Java JCR API para executar operações de criação, substituição, atualização e exclusão (CRUD) em conteúdo localizado no repositório do Adobe CQ. Para obter mais informações sobre a Java JCR API, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artigo de desenvolvimento modifica o Adobe CQ JCR de um aplicativo Java externo. Por outro lado, você pode modificar o JCR de um pacote OSGi usando a API JCR. Para obter detalhes, consulte Dados CQ [persistentes no repositório](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)de conteúdo Java.

>[!NOTE]
>
>Para usar a API JCR, adicione o `jackrabbit-standalone-2.4.0.jar` arquivo ao caminho de classe do seu aplicativo Java. Você pode obter esse arquivo JAR na página da API Java JCR em [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para saber como consultar o JCR do Adobe CQ usando a API de consulta do JCR, consulte [Consultar dados do Adobe Experience Manager usando a API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)do JCR.

## Criar uma instância do Repositório {#create-a-repository-instance}

Embora existam diferentes maneiras de se conectar a um repositório e estabelecer uma conexão, este artigo de desenvolvimento usa um método estático que pertence à `org.apache.jackrabbit.commons.JcrUtils` classe. O nome do método é `getRepository`. Esse método usa um parâmetro de string que representa o URL do servidor Adobe CQ. Por exemplo `http://localhost:4503/crx/server`.

O `getRepository`método retorna uma `Repository`instância, como mostrado no exemplo de código a seguir.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Criar uma instância de Sessão {#create-a-session-instance}

A `Repository`instância representa o repositório CRX. Use a `Repository`instância para estabelecer uma sessão com o repositório. Para criar uma sessão, chame o `Repository`método da `login`instância e passe um `javax.jcr.SimpleCredentials` objeto. O `login`método retorna uma `javax.jcr.Session` instância.

Você cria um `SimpleCredentials`objeto usando seu construtor e transmitindo os seguintes valores de string:

* O nome do utilizador;
* A senha correspondente

Ao passar o segundo parâmetro, chame o `toCharArray`método do objeto String. O código a seguir mostra como chamar o `login`método que retorna um `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Criar uma instância de Nó {#create-a-node-instance}

Use uma `Session`instância para criar uma `javax.jcr.Node` instância. Uma `Node`instância permite executar operações de nó. Por exemplo, você pode criar um novo nó. Para criar um nó que represente o nó raiz, chame o `Session`método da `getRootNode` instância, como mostrado na seguinte linha de código.

```java
//Create a Node
Node root = session.getRootNode();
```

Depois de criar uma `Node`instância, você pode executar tarefas como criar outro nó e adicionar um valor a ele. Por exemplo, o código a seguir cria dois nós e adiciona um valor ao segundo nó.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores de nó {#retrieve-node-values}

Para recuperar um nó e seu valor, chame o `Node`método da `getNode`instância e transmita um valor de string que representa o caminho totalmente qualificado para o nó. Considere a estrutura de nó criada no exemplo de código anterior. Para recuperar o nó do dia, especifique adobe/day, como mostrado no seguinte código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Criar nós no repositório do Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

O exemplo de código Java a seguir representa uma classe Java que se conecta ao Adobe CQ, cria uma `Session`instância e adiciona novos nós. Um nó recebe um valor de dados e o valor do nó e seu caminho é gravado no console. Quando terminar a sessão, faça logoff.

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

Depois de executar o exemplo de código completo e criar os nós, você pode exibir os novos nós no **[!UICONTROL CRXDE Lite]**, como mostrado na ilustração a seguir.

![chlimage_1-68](assets/chlimage_1-68a.png)

