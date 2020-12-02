---
title: Como acessar programaticamente o JCR AEM
seo-title: Como acessar programaticamente o JCR AEM
description: Você pode modificar programaticamente os nós e as propriedades localizados no repositório AEM, que é parte da Adobe Marketing Cloud
seo-description: Você pode modificar programaticamente os nós e as propriedades localizados no repositório AEM, que é parte da Adobe Marketing Cloud
uuid: 2051d03f-430a-4cae-8f6d-e5bc727d733f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 69f62a38-7991-4009-8db7-ee8fd35dc535
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---


# Como acessar programaticamente o JCR AEM{#how-to-programmatically-access-the-aem-jcr}

Você pode modificar programaticamente os nós e as propriedades localizados no repositório Adobe CQ, que faz parte da Adobe Marketing Cloud. Para acessar o repositório do CQ, use a API Java Content Repository (JCR). Você pode usar a Java JCR API para executar operações de criação, substituição, atualização e exclusão (CRUD) em conteúdo localizado no repositório Adobe CQ. Para obter mais informações sobre a API Java JCR, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artigo de desenvolvimento modifica o Adobe CQ JCR de um aplicativo Java externo. Por outro lado, você pode modificar o JCR de um pacote OSGi usando a API JCR. Para obter detalhes, consulte [Dados CQ persistentes no repositório de conteúdo Java](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Para usar a API JCR, adicione o arquivo `jackrabbit-standalone-2.4.0.jar` ao caminho de classe do seu aplicativo Java. Você pode obter esse arquivo JAR da página da API JCR Java em [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para saber como query o Adobe CQ JCR usando a API do Query JCR, consulte [Consultando dados do Adobe Experience Manager usando a API do JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Criar uma instância do Repositório {#create-a-repository-instance}

Embora existam diferentes maneiras de se conectar a um repositório e estabelecer uma conexão, este artigo de desenvolvimento usa um método estático que pertence à classe `org.apache.jackrabbit.commons.JcrUtils`. O nome do método é `getRepository`. Esse método usa um parâmetro de string que representa a URL do servidor Adobe CQ. Por exemplo `http://localhost:4503/crx/server`.

O método `getRepository`retorna uma instância `Repository`conforme mostrado no exemplo de código a seguir.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Criar uma instância de Sessão {#create-a-session-instance}

A instância `Repository`representa o repositório CRX. Use a instância `Repository`para estabelecer uma sessão com o repositório. Para criar uma sessão, chame o método `Repository`da instância e transmita um objeto `javax.jcr.SimpleCredentials`. `login` O método `login`retorna uma instância `javax.jcr.Session`.

Você cria um objeto `SimpleCredentials`usando seu construtor e transmitindo os seguintes valores de string:

* O nome do utilizador;
* A senha correspondente

Ao transmitir o segundo parâmetro, chame o método `toCharArray`do objeto String. O código a seguir mostra como chamar o método `login`que retorna um `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Criar uma instância de Nó {#create-a-node-instance}

Use uma instância `Session`para criar uma instância `javax.jcr.Node`. Uma instância `Node`permite executar operações de nó. Por exemplo, você pode criar um novo nó. Para criar um nó que represente o nó raiz, chame o método `Session`da instância `getRootNode`, conforme mostrado na seguinte linha de código.

```java
//Create a Node
Node root = session.getRootNode();
```

Depois de criar uma instância `Node`, você pode executar tarefas como criar outro nó e adicionar um valor a ele. Por exemplo, o código a seguir cria dois nós e adiciona um valor ao segundo nó.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores de nó {#retrieve-node-values}

Para recuperar um nó e seu valor, chame o método `Node`da instância e transmita um valor de string que representa o caminho totalmente qualificado para o nó. `getNode` Considere a estrutura de nó criada no exemplo de código anterior. Para recuperar o nó do dia, especifique adobe/day, como mostrado no seguinte código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Criar nós no Adobe CQ Repository {#create-nodes-in-the-adobe-cq-repository}

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

Depois de executar o exemplo de código completo e criar os nós, você pode visualização os novos nós em **[!UICONTROL CRXDE Lite]**, como mostrado na ilustração a seguir.

![chlimage_1-68](assets/chlimage_1-68a.png)

