---
title: Início Rápido da API de Serviço de Repositório
description: Use o serviço Repositório do AEM Forms para criar uma pasta, gravar um recurso, listar recursos, ler um recurso, atualizar um recurso, pesquisar recursos, criar relacionamentos entre recursos, bloquear um recurso, gerenciar listas de controle de acesso e excluir um recurso.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 703b6798-d40f-4769-96fc-e440090ca983
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# Início Rápido da API de Serviço de Repositório {#repository-service-api-quick-starts}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Os seguintes Quick Starts estão disponíveis para o serviço de Repositório do AEM Forms.

[Início rápido (modo SOAP): criação de uma pasta usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[Início rápido (modo SOAP): Gravação de um recurso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Início rápido (modo SOAP): listar recursos usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[Início rápido (modo SOAP): Leitura de um recurso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[Início rápido (modo SOAP): atualização de um recurso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[Início rápido (modo SOAP): procurando recursos usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[Início rápido (modo SOAP): criação de relacionamentos entre recursos usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[Início rápido (modo SOAP): bloqueio de um recurso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[Início rápido (modo SOAP): gerenciamento de listas de controle de acesso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-managing-access-control-lists-using-the-java-api)

[Início rápido (modo SOAP): exclusão de um recurso usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-deleting-a-resource-using-the-java-api)

As operações do AEM Forms podem ser executadas usando a API altamente tipada do AEM Forms e o modo de conexão deve ser definido como SOAP

**Aplicativos/AplicativoFormulários**

A maioria das inicializações rápidas do serviço de repositório do AEM Forms interage com um aplicativo chamado `Applications/FormsApplication,` conforme mostrado na ilustração a seguir.

A pasta FormsFolder é um local no repositório do AEM Forms. Você pode, por exemplo, adicionar programaticamente esta pasta ao `Applications/FormsApplication`. (Consulte [Início rápido (modo SOAP): Criando uma pasta usando a API Java](repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api).)

O caminho para um recurso no repositório do AEM Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

>[!NOTE]
>
>Você pode navegar pelo repositório do AEM Forms usando um navegador da Web. Para navegar no repositório, insira a seguinte URL em um navegador da Web `https://[server name]:[server port]/repository`. Você pode verificar os resultados de início rápido usando um navegador da Web. Por exemplo, se você adicionar conteúdo ao Repositório do AEM Forms, poderá ver o conteúdo em um navegador da Web.

>[!NOTE]
>
>Applications/FormsApplication não existe por padrão. Para seguir as inicializações rápidas, crie este aplicativo usando o Workbench. Para obter informações sobre como criar um aplicativo usando o Workbench, consulte [Introdução ao design de processo](https://www.adobe.com/go/learn_aemforms_workbench_65_br).

## Início rápido (modo SOAP): criação de uma pasta usando a API Java {#quick-start-soap-mode-creating-a-folder-using-the-java-api}

O exemplo de código Java a seguir cria uma pasta chamada *FormsFolder* no seguinte local `/Applications/FormsApplication/1.0/`. (Consulte [Criação de Pastas](/help/forms/developing/aem-forms-repository.md#creating-folders).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.*;
 import com.adobe.repository.infomodel.bean.*;
 
 public class CreateFolder {
 
     public static void main(String[] args) {
 
         // This quick start creates a folder in the AEM Forms repository
         //Ensure that you create a AEM Forms application named FormsApplication using Workbench
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Create a RepositoryInfomodelFactoryBean needed for creating resources
             RepositoryInfomodelFactoryBean repositoryInfomodelFactory = new RepositoryInfomodelFactoryBean(null);
 
             // Create a folder in a AEM Forms application named Application/FormsApplication
             ResourceCollection folder = repositoryInfomodelFactory.newResourceCollection(
                 new Id(),
                 new Lid(),
                 "FormsFolder"
             );
 
             // Set the folder’s description
             folder.setDescription("A folder to store forms");
 
             // Write the folder to the repository
             Resource newFolder = repositoryClient.writeResource("/Applications/FormsApplication/1.0/", folder);
 
             // Retrieve the folder’s identifier value
             String msg = "The identifier value of the new folder is" + newFolder.getId();
 
             // Print folder verification message
             System.out.println(msg);
 
         } catch (Exception e) {
                 System.out.println(
                     "Exception thrown while trying to create the folder" +
                     e.getMessage()
                 );
           }
     }
 }
```

## Início rápido (modo SOAP): Gravação de um recurso usando a API Java {#quick-start-soap-mode-writing-a-resource-using-the-java-api}

O exemplo de código Java a seguir grava um recurso chamado *loan.xdp* no repositório. O recurso foi adicionado ao local `/Applications/FormsApplication/1.0/FormsFolder`. (Consulte [Gravando Recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.Id;
 import com.adobe.repository.infomodel.Lid;
 
 import com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean;
 import com.adobe.repository.infomodel.bean.Resource;
 import com.adobe.repository.infomodel.bean.ResourceContent;
 
 public class WriteFile {
 
     // This quick start writes Loan.xdp to Applications/FormsApplication/1.0/FormsFolder
     //Ensure that you create a AEM Forms application named FormsApplication using Workbench
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a ResourceRepositoryClient object
         ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
         //Specify the parent path
          String parentResourcePath = "/Applications/FormsApplication/1.0/FormsFolder";
 
         //Create a RepositoryInfomodelFactoryBean object
          RepositoryInfomodelFactoryBean infomodelFactory = new RepositoryInfomodelFactoryBean(null);
 
         //Create a Resource object to add to the Repository
          Resource newResource = (Resource) infomodelFactory.newImage(
                             new Id(),
                             new Lid(),
                             "Loan.xdp");
 
         //Create a ResourceContent object that contains the content (file bytes)
         ResourceContent content = (ResourceContent) infomodelFactory.newResourceContent();
 
         //Create a Document that references an XDP file
         //to add to the Repository
         FileInputStream myForm = new FileInputStream("C:\\Adobe\Loan.xdp");
         Document form = new Document(myForm);
 
         //Set the description and the MIME type
         content.setDataDocument(form);
         content.setMimeType("application/vnd.adobe.xdp+xml");
 
         //Assign content to the Resource object
         newResource.setContent(content) ;
 
         //Set a description of the resource
         newResource.setDescription("An XDP file");
 
         //Commit to repository, and update resource
         //in memory (by assignment)
         Resource addResource = repositoryClient.writeResource(parentResourcePath, newResource);
 
         //Get the description of the returned Resource object
         System.out.println("The description of the new resource is "+addResource.getDescription());
 
         //Close the FileStream object
         myForm.close();
 
         } catch (Exception e) {
 
              e.printStackTrace();
            }
         }
 }
 
```

## Início rápido (modo SOAP): listar recursos usando a API Java {#quick-start-soap-mode-listing-resources-using-the-java-api}

O código Java a seguir lista recursos que estão em `Applications/FormsApplication/1.0/FormsFolder`. (Consulte [Listando Recursos](/help/forms/developing/aem-forms-repository.md#listing-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.Resource;
 
 //This quick start lists the content in Applications/FormsApplication/1.0/FormsFolder
 //Ensure that you create a AEM Forms application named Applications/FormsApplication using Workbench
 public class ListFiles {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // List all the files in the
             String resourceFolderPath = "/Applications/FormsApplication/1.0/FormsFolder";
 
             // Retrieve the list of resources under the folder path
             List members = repositoryClient.listMembers(resourceFolderPath);
 
             // Print out the resources that were found
             System.out.println("The following resources were found:");
             for (int i = 0; i < members.size(); i++) {
                 Resource r = (Resource)(members.get(i));
                 System.out.println(
                     "Resource name: " +
                     r.getName() +
                     "  Resource Description: " +
                     r.getDescription()
                 );
             }
 
         } catch (Exception e) {
              e.printStackTrace();
           }
     }
 }
```

## Início rápido (modo SOAP): Leitura de um recurso usando a API Java {#quick-start-soap-mode-reading-a-resource-using-the-java-api}

O exemplo de código Java a seguir lê um recurso chamado *Loan.xdp* do repositório. Arquivo XDP em `/Applications/FormsApplication/1.0/FormsFolder/`. (Consulte [Recursos de Leitura](/help/forms/developing/aem-forms-repository.md#reading-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.*;
 
 //This quick start retrieves Loan.xdp from Applications/FormsApplication/1.0/FormsFolder
 //Ensure that you create a AEM Forms application named FormsApplication using Workbench
 public class ReadFile {
 
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Specify the path to the Loan.xdp
             String resourceUri =  "/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
             // Retrieve the XDP file
             Resource r = repositoryClient.readResource(resourceUri);
 
             // Print the resource verification message
             System.out.println(
                 "Resource " +
                 resourceUri +
                 " was successfully retrieved." +
                 "Resource content contains " +
                 r.getContent().getDataDocument().length() +
                 " bytes."
             );
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to read the file" +
                 e.getMessage()
             );
         }
     }
 }
 
```

## Início rápido (modo SOAP): atualização de um recurso usando a API Java {#quick-start-soap-mode-updating-a-resource-using-the-java-api}

O exemplo de código Java a seguir atualiza `/Applications/FormsApplication/1.0/FormsFolder` modificando sua descrição. (Consulte [Atualizando Recursos](/help/forms/developing/aem-forms-repository.md#updating-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.*;
 import java.util.*;
 
 //This quick start updates the description of Applications/FormsApplication/1.0/FormsFolder
 //Ensure that you create a AEM Forms application named Applications/FormsApplication using Workbench
 public class UpdateResource {
 
     public static void main(String[] args) {
 
         // This example will update a resource in the AEM Forms repository
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Specify the URI of the resource to update
             String resourceUri =  "/Applications/FormsApplication/1.0/FormsFolder";
 
             // Retrieve the resource
             Resource resource = repositoryClient.readResource(resourceUri);
 
             // Update its description
             resource.setDescription("This folder stores XDP files");
 
             // Update the resource in the repository
             Resource updatedResource = repositoryClient.updateResource(
                 resourceUri,
                 resource,
                 true
             );
 
             // Print the resource verification message
             System.out.println(
                 "Resource " +
                 resourceUri +
                 "version " +
                 updatedResource.getMajorVersion() +
                 "." +
                 updatedResource.getMinorVersion() +
                 " was successfully updated."
             );
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to update the resource" +
                 e.getMessage()
             );
         }
     }
 }
 
```

## Início rápido (modo SOAP): procurando recursos usando a API Java {#quick-start-soap-mode-searching-for-resources-using-the-java-api}

O exemplo de código Java a seguir pesquisa por Loan.xdp em `Applications/FormsApplication/1.0/FormsFolder`. (Consulte [Pesquisando Recursos](/help/forms/developing/aem-forms-repository.md#searching-for-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.*;
 import com.adobe.repository.query.*;
 import com.adobe.repository.query.sort.*;
 
 //This quick start searches for Loan.xdp in Applications/FormsApplication/1.0/FormsFolder
 //Ensure that you create a AEM Forms application named FormsApplication using Workbench
 public class SearchResources {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Specify the URI of the target folder
             String testFolderUri = "/Applications/FormsApplication/1.0/FormsFolder";
 
             // Specify the attribute name for which to search
             String name = "Loan.xdp";
 
             // Create a Query used in the search
             Query query = new Query();
             Query.Statement statement = new Query.Statement(
                 Resource.ATTRIBUTE_NAME,
                 Query.Statement.OPERATOR_BEGINS_WITH,
                 name
             );
             statement.setNamespace(ResourceProperty.RESERVED_NAMESPACE_REPOSITORY);
             query.addStatement(statement);
 
             // Create the sort order used in the search
             SortOrder sortOrder = new SortOrder();
             SortOrder.Element element = new SortOrder.Element(Resource.ATTRIBUTE_NAME, true);
             sortOrder.addSortElement(element);
 
             // Search for the resources
             List listProperties = repositoryClient.searchProperties(
                 testFolderUri,
                 query,
                 ResourceCollection.DEPTH_INFINITE,
                 0,
                 10,
                 sortOrder
             );
 
             // Display the resources that were found
             System.out.println("The following resources were found:");
             for (int i = 0; i < listProperties.size(); i++) {
                 Resource r = (Resource)(listProperties.get(i));
                 System.out.println(r.getName());
             }
 
         } catch (Exception e) {
             System.out.println(
                 "An exception occurred while attempting to search for resources." +
                 e.getMessage()
             );
         }
     }
 }
```

## Início rápido (modo SOAP): criação de relacionamentos entre recursos usando a API Java {#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api}

O exemplo de código Java a seguir cria uma relação entre dois recursos no repositório do AEM Forms. (Consulte [Criando Relações de Recursos](/help/forms/developing/aem-forms-repository.md#creating-resource-relationships).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.*;
 import com.adobe.repository.infomodel.bean.*;
 
 public class CreateRelationship {
 
     public static void main(String[] args) {
 
         // This example creates a relationship between two resources in the AEM Forms repository.
         // First, two resources are created.
         // A dependence relationship between the two resources will then be established and verified.
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Create a RepositoryInfomodelFactoryBean needed for creating resources
             RepositoryInfomodelFactoryBean repositoryInfomodelFactory = new RepositoryInfomodelFactoryBean(null);
 
             // Specify the URI of the target folder for writing the resource
             String testFolderUri = "/Applications/FormsApplication/1.0/FormsFolder";
 
             // Create the resources to be written to the folder
             Resource testResource1 = repositoryInfomodelFactory.newResource(
                 new Id(),
                 new Lid(),
                 "FormFolderA"
             );
 
             Resource testResource2 = repositoryInfomodelFactory.newResource(
                 new Id(),
                 new Lid(),
                 "FormFolderB"
             );
 
             // Set the resources’ descriptions
             testResource1.setDescription("test resource1");
             testResource2.setDescription("test resource2");
 
             // Write the resources to the folder
             repositoryClient.writeResource(testFolderUri, testResource1);
             repositoryClient.writeResource(testFolderUri, testResource2);
 
             // Retrieve the resources’ URIs
             String resourceUri1 = testFolderUri + "/" + testResource1.getName();
             String resourceUri2 = testFolderUri + "/" + testResource2.getName();
 
             // Retrieve the resources to verify that they were successfully written
             Resource r1 = repositoryClient.readResource(resourceUri1);
             Resource r2 = repositoryClient.readResource(resourceUri2);
 
             // Create a relationship between the two resources
             repositoryClient.createRelationship(
                 resourceUri1,
                 resourceUri2,
                 Relation.TYPE_DEPENDANT_OF,
                 true
             );
 
             // Verify the relationship
             List relations = repositoryClient.getRelated(
                 resourceUri1,
                 true,
                 Relation.TYPE_DEPENDANT_OF
             );
 
             // Print the relationship
             for (int i = 0; i < relations.size(); i++) {
                 Resource r = (Resource)(relations.get(i));
                 System.out.println("Related resource: " + r.getName());
             }
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to create the relationship" +
                 e.getMessage()
             );
         }
     }
 }
```

## Início rápido (modo SOAP): bloqueio de um recurso usando a API Java {#quick-start-soap-mode-locking-a-resource-using-the-java-api}

O exemplo de código Java a seguir bloqueia /Applications/FormsApplication/1.0/FormsFolder/Loan.xdp. (Consulte [Bloqueando Recursos](/help/forms/developing/aem-forms-repository.md#locking-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.*;
 
 public class LockFile {
 
     public static void main(String[] args) {
 
         // This example will lock and unlock a resource in the AEM Forms repository.
         try {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Specify the URI of the resource to lock
             String resourceUri = "/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
             // Lock the resource
             repositoryClient.lockResource(
                 resourceUri,
                 Lock.SCOPE_EXCLUSIVE,
                 Lock.DEPTH_ZERO
             );
 
             // Retrieve the locks on the resource
             List locks = repositoryClient.getLocks(resourceUri);
 
             // Print out the locks for the resource
             System.out.println("The following locks now exist for the resource:");
             for (int i = 0; i < locks.size(); i++) {
                 Lock l = (Lock)(locks.get(i));
                 System.out.println(
                     "Lock owner: " +
                     l.getOwnerUserId() +
                     "  Lock depth: " +
                     l.getDepth() +
                     " Lock scope: " +
                     l.getType()
                 );
             }
 
             // Unlock the resource
             String lockToken = repositoryClient.unlockResource(resourceUri);
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to lock the file" +
                 e.getMessage()
             );
         }
     }
 }
```

## Início rápido (modo SOAP): gerenciamento de listas de controle de acesso usando a API Java {#quick-start-soap-mode-managing-access-control-lists-using-the-java-api}

O exemplo de código Java a seguir lê e cria listas de controle de acesso (ACLs) no repositório.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.bean.*;
 
 public class UseACL {
 
     public static void main(String[] args) {
 
         // This example will read and create access control lists for resources in the AEM Forms repository.
         try {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Specify the URI of the resource to be used
             String resourceUri = "/Applications/FormsApplication";
 
             // Retrieve the access control list for the resource
             AccessControlList acl = repositoryClient.readAccessControlList(resourceUri);
 
             // Retrieve a list of the users having access permissions
             List users = acl.getUsersWithPermissions();
 
             // Print out the list of users
             System.out.println("The following users have permissions:");
             for (int i = 0; i < users.size(); i++) {
                 String user = (String)(users.get(i));
                 System.out.println("User identifier: " + user);
             }
 
             // Set up a new access control list
             acl = new AccessControlList();
 
             // Retrieve a user identifier to be used in the access control list
             String userId = (String)(users.get(0));
 
             // Create traversal permissions for the user
             List permissions = new ArrayList();
             permissions.add(AccessControlEntry.READ_METADATA_USER_PERM);
             permissions.add(AccessControlEntry.READ_CONTENT_USER_PERM);
             acl.setPermissionsForUser(userId, permissions);
 
             // Set the access control list for the folder
             repositoryClient.writeAccessControlList(resourceUri, acl, true);
 
             // Print out confirmation message
             System.out.println("User " + userId + " has traversal permissions for the folder");
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to manage access control lists" +
                 e.getMessage()
             );
         }
     }
 }
```

## Início rápido (modo SOAP): exclusão de um recurso usando a API Java {#quick-start-soap-mode-deleting-a-resource-using-the-java-api}

O código Java a seguir exclui Loan.xdp de `Applications/FormsApplication/1.0/FormsFolder`. Se esse arquivo XDP não estiver nessa pasta, uma exceção será lançada. (Consulte [Excluindo Recursos](/help/forms/developing/aem-forms-repository.md#deleting-resources).)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-repository-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. commons-code-1.3.jar
     * 7. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 8. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 import com.adobe.repository.infomodel.*;
 import com.adobe.repository.infomodel.bean.*;
 import com.adobe.repository.RepositoryException;
 import com.adobe.idp.Document;
 
 
 // This quick start deletes Loan.xdp from Applications/FormsApplication/1.0/FormsFolder
 //If this XDP is not in this folder, an exception is thrown
 //Ensure that you create a AEM Forms application named FormsApplication using Workbench
 public class DeleteResource {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create the service client factory
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a ResourceRepositoryClient object using the service client factory
             ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
             // Create a RepositoryInfomodelFactoryBean needed for creating resources
             RepositoryInfomodelFactoryBean repositoryInfomodelFactory = new RepositoryInfomodelFactoryBean(null);
 
             // Specify the URI of the target folder from which the resource is deleted
             String testFolderUri = "/Applications/FormsApplication/1.0/FormsFolder";
 
             // Create the resource to be written to the folder
             Resource testResource = repositoryInfomodelFactory.newResource(
                 new Id(),
                 new Lid(),
                 "Loan.xdp"
             );
 
             // Retrieve the resource’s URI
             String resourceUri = testFolderUri + "/" + testResource.getName();
 
             // Retrieve the resource to verify that it exists
             Resource r = repositoryClient.readResource(resourceUri);
 
             // Print the resource verification message
             System.out.println(r.getName() +" is about to be deleted");
 
             // Delete the resource
             repositoryClient.deleteResource(resourceUri);
 
         } catch (Exception e) {
             System.out.println(
                 "Exception thrown while trying to delete the resource" +
                 e.getMessage()
             );
         }
     }
 }
 
 
```
