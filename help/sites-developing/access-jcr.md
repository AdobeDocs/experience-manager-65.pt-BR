---
title: Como acessar programaticamente o JCR do AEM
description: Você pode modificar programaticamente nós e propriedades localizados no repositório AEM, que faz parte do Adobe Experience Cloud
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
source-git-commit: 152b6078d6a19f8220564188d4d5d5a7bdee4146
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Como acessar programaticamente o JCR do AEM{#how-to-programmatically-access-the-aem-jcr}

Você pode modificar programaticamente nós e propriedades localizados no repositório do Adobe CQ, que faz parte do Adobe Experience Cloud. Para acessar o repositório CQ, use a API Java™ Content Repository (JCR). Você pode usar a API JCR do Java™ para criar, substituir, atualizar e excluir conteúdo (CRUD) localizado no repositório do Adobe CQ. Para obter mais informações sobre a API JCR do Java™, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artigo de desenvolvimento modifica o Adobe CQ JCR de um aplicativo Java™ externo. Por outro lado, você pode modificar o JCR de um pacote OSGi usando a API do JCR. Para obter detalhes, consulte [Persistência de dados do CQ no repositório de conteúdo Java™](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
Para usar a API JCR, adicione o `jackrabbit-standalone-2.4.0.jar` para o caminho de classe do seu aplicativo Java™. Você pode obter esse arquivo JAR da página da Web da API JCR em [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
Para saber como consultar o JCR do Adobe CQ usando a API de consulta JCR, consulte [Consulta de dados do Adobe Experience Manager usando a API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Criar uma instância do Repositório {#create-a-repository-instance}

Embora existam diferentes maneiras de se conectar a um repositório e estabelecer uma conexão, este artigo de desenvolvimento usa um método estático que pertence ao `org.apache.jackrabbit.commons.JcrUtils` classe. O nome do método é `getRepository`. Esse método usa um parâmetro de string que representa o URL do servidor do Adobe CQ. Por exemplo, `http://localhost:4503/crx/server`.

A variável `getRepository` o método retorna um `Repository` como mostrado no exemplo de código a seguir.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Criar uma instância de sessão {#create-a-session-instance}

A variável `Repository` representa o repositório CRX. Você usa o `Repository` para estabelecer uma sessão com o repositório. Para criar uma sessão, chame o `Repository` da instância `login` e transmita um `javax.jcr.SimpleCredentials` objeto. A variável `login` o método retorna um `javax.jcr.Session` instância.

Você cria um `SimpleCredentials` usando seu construtor e transmitindo os seguintes valores de string:

* O nome de usuário;
* A senha correspondente

Ao passar o segundo parâmetro, chame o comando de `toCharArray` método. O código a seguir mostra como chamar a variável `login` método que retorna um `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Criar uma instância de Nó {#create-a-node-instance}

Use um `Session` instância para criar um `javax.jcr.Node` instância. A `Node` permite executar operações de nó. Por exemplo, você pode criar um nó. Para criar um nó que represente o nó raiz, chame o `Session` da instância `getRootNode` conforme mostrado na linha de código a seguir.

```java
//Create a Node
Node root = session.getRootNode();
```

Depois de criar um `Node`instância, é possível executar tarefas como criar outro nó e adicionar um valor a ele. Por exemplo, o código a seguir cria dois nós e adiciona um valor ao segundo nó.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores do nó {#retrieve-node-values}

Para recuperar um nó e seu valor, chame o `Node` da instância `getNode` e passe um valor de string que representa o caminho totalmente qualificado para o nó. Considere a estrutura do nó criada no exemplo de código anterior. Para recuperar o nó day, especifique adobe/day, como mostrado no seguinte código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Criar nós no Repositório do Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

O seguinte exemplo de código Java™ representa uma classe Java™ que se conecta ao Adobe CQ, cria uma `Session` e adiciona novos nós. Um nó recebe um valor de dados e, em seguida, o valor do nó e seu caminho são gravados no console. Quando terminar a sessão, faça logout.

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

Depois de executar o exemplo de código completo e criar os nós, você pode visualizar os novos nós na **[!UICONTROL CRXDE Lite]**, conforme mostrado na ilustração a seguir.

![chlimage_1-68](assets/chlimage_1-68a.png)
