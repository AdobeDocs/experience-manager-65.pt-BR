---
title: Como acessar programaticamente o JCR do AEM
description: Você pode modificar programaticamente nós e propriedades localizados no repositório AEM, que faz parte do Adobe Experience Cloud
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Como acessar programaticamente o JCR do AEM{#how-to-programmatically-access-the-aem-jcr}

Você pode modificar programaticamente nós e propriedades localizados no repositório do Adobe CQ, que faz parte do Adobe Experience Cloud. Para acessar o repositório CQ, use a API Java™ Content Repository (JCR). Você pode usar a API JCR do Java™ para criar, substituir, atualizar e excluir conteúdo (CRUD) localizado no repositório do Adobe CQ. Para obter mais informações sobre a API JCR do Java™, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artigo de desenvolvimento modifica o Adobe CQ JCR de um aplicativo Java™ externo. Por outro lado, você pode modificar o JCR de um pacote OSGi usando a API do JCR. Para obter detalhes, consulte [Persistência de dados CQ no Repositório de Conteúdo Java™](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Para usar a API JCR, adicione o arquivo `jackrabbit-standalone-2.4.0.jar` ao caminho de classe do seu aplicativo Java™. Você pode obter este arquivo JAR da página da Web da API JCR no endereço [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para saber como consultar o JCR do Adobe CQ usando a API de consulta JCR, consulte [Consulta de dados do Adobe Experience Manager usando a API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Criar uma instância do Repositório {#create-a-repository-instance}

Embora existam diferentes maneiras de se conectar a um repositório e estabelecer uma conexão, este artigo de desenvolvimento usa um método estático que pertence à classe `org.apache.jackrabbit.commons.JcrUtils`. O nome do método é `getRepository`. Esse método usa um parâmetro de string que representa o URL do servidor do Adobe CQ. Por exemplo, `http://localhost:4503/crx/server`.

O método `getRepository` retorna uma instância `Repository`, como mostrado no exemplo de código a seguir.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Criar uma instância de sessão {#create-a-session-instance}

A instância `Repository` representa o repositório do CRX. Use a instância `Repository` para estabelecer uma sessão com o repositório. Para criar uma sessão, chame o método `login` da instância `Repository` e passe um objeto `javax.jcr.SimpleCredentials`. O método `login` retorna uma instância `javax.jcr.Session`.

Você cria um objeto `SimpleCredentials` usando seu construtor e transmitindo os seguintes valores de cadeia de caracteres:

* O nome de usuário;
* A senha correspondente

Ao passar o segundo parâmetro, chame o método `toCharArray` do objeto String. O código a seguir mostra como chamar o método `login` que retorna um `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Criar uma instância de Nó {#create-a-node-instance}

Use uma instância `Session` para criar uma instância `javax.jcr.Node`. Uma instância `Node` permite que você execute operações de nó. Por exemplo, você pode criar um nó. Para criar um nó que represente o nó raiz, chame o método `getRootNode` da instância `Session`, conforme mostrado na linha de código a seguir.

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

## Recuperar valores do nó {#retrieve-node-values}

Para recuperar um nó e seu valor, chame o método `getNode` da instância `Node` e passe um valor de cadeia de caracteres que represente o caminho totalmente qualificado para o nó. Considere a estrutura do nó criada no exemplo de código anterior. Para recuperar o nó day, especifique adobe/day, como mostrado no seguinte código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Criar nós no Repositório do Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

O exemplo de código Java™ a seguir representa uma classe Java™ que se conecta ao Adobe CQ, cria uma instância `Session` e adiciona novos nós. Um nó recebe um valor de dados e, em seguida, o valor do nó e seu caminho são gravados no console. Quando terminar a sessão, faça logout.

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

Após executar o exemplo de código completo e criar os nós, você pode visualizar os novos nós no **[!UICONTROL CRXDE Lite]**, conforme mostrado na ilustração a seguir.

![chlimage_1-68](assets/chlimage_1-68a.png)
