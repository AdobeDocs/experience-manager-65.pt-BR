---
title: Conectar o AEM Forms com o LiveCycle Adobe
seo-title: Conectar o AEM Forms com o LiveCycle Adobe
description: AEM conector LiveCycle permite iniciar o LiveCycle ES4 Document Services a partir de AEM aplicativos e fluxos de trabalho.
seo-description: AEM conector LiveCycle permite iniciar o LiveCycle ES4 Document Services a partir de AEM aplicativos e fluxos de trabalho.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---


# Conectar o AEM Forms com o LiveCycle Adobe {#connecting-aem-forms-with-adobe-livecycle}

O conector de LiveCycle Adobe Experience Manager (AEM) permite a invocação simplificada do Adobe LiveCycle ES4 Document Services de dentro AEM aplicativos e fluxos de trabalho da Web. O LiveCycle fornece um SDK de cliente avançado, que permite que aplicativos clientes iniciem serviços do LiveCycle usando APIs Java. AEM LiveCycle Connector simplifica o uso dessas APIs no ambiente OSGi.

## Conectando AEM servidor ao Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector faz parte do [pacote complementar do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Depois de instalar o pacote do complemento AEM Forms, execute as etapas a seguir para adicionar detalhes do servidor LiveCycle AEM Console da Web.

1. No gerenciador de configuração AEM console da Web, localize o componente de configuração do SDK do cliente do Adobe LiveCycle.
1. Clique no componente para editar o URL do servidor de configuração, o nome de usuário e a senha.
1. Revise as configurações e clique em **Salvar**.

Embora as propriedades sejam autoexplicativas, as mais importantes são as seguintes:

* **URL do servidor**  - Especifica o URL para o servidor do LiveCycle. Se você quiser que o LiveCycle e o AEM se comuniquem via https, comece AEM com a seguinte JVM

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   opção.

* **Nome de usuário** - Especifica o nome de usuário da conta que é usada para estabelecer a comunicação entre o AEM e o LiveCycle. A conta é uma conta de usuário do LiveCycle com permissões para iniciar o Document Services.
* **Senha** - Especifica a senha.
* **Nome do serviço**  - Especifica os serviços que são iniciados usando as credenciais do usuário fornecidas nos campos Nome de usuário e Senha. Por padrão, nenhuma credencial é passada ao iniciar os serviços do LiveCycle.

## Iniciando serviços de documento {#starting-document-services}

Os aplicativos clientes podem iniciar programaticamente os serviços do LiveCycle usando uma API Java, Serviços da Web, Remoção e REST. Para clientes Java, o aplicativo pode usar o SDK do LiveCycle. O SDK do LiveCycle fornece uma API Java para iniciar esses serviços remotamente. Por exemplo, para converter um Documento do Microsoft Word em PDF, o cliente inicia o GeneratePDFSService. O fluxo de invocação consiste nas seguintes etapas:

1. Crie uma instância ServiceClientFactory .
1. Cada serviço fornece uma classe de cliente. Para iniciar um serviço, crie uma instância cliente do serviço.
1. Inicie o serviço e processe o resultado.

AEM LiveCycle Connector simplifica o fluxo ao expor essas instâncias do cliente como serviços OSGi que podem ser acessados usando meios OSGi padrão. O conector LiveCycle fornece os seguintes recursos:

* Instâncias do cliente como Serviço OSGi: Os clientes empacotados como pacotes OSGI são listados na seção [Document Services list](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Cada jar do cliente registra a instância do cliente como serviço OSGi no Registro de Serviço OSGi.
* Propagação de Credencial do Usuário: Os detalhes de conexão necessários para se conectar ao servidor do LiveCycle são gerenciados em um local central.
* Serviço ServiceClientFactory: Para iniciar os processos, o aplicativo cliente pode acessar a instância ServiceClientFactory .

### Começando por Referências de Serviço do Registro de Serviço OSGi {#starting-via-service-references-from-osgi-service-registry}

Para iniciar um serviço exposto no AEM, execute as seguintes etapas:

1. Determine as dependências de maven. Adicione dependência ao jar do cliente necessário no arquivo maven pom.xml. No mínimo, adicione dependência aos jars adobe-livecycle-client e adobe-usermanager-client.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   Para iniciar um serviço, adicione a dependência Maven correspondente para o serviço. Para obter a lista de dependências, consulte [Lista de serviços de documento](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). Por exemplo, para o serviço Gerar PDF, adicione a seguinte dependência:

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. Obtenha a referência de serviço. Obtenha um identificador para a instância do serviço. Se estiver escrevendo uma classe Java, você poderá usar as anotações dos Serviços Declarativos.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   O trecho de código acima inicia a API createPDF de GeneratePdfServiceClient para converter um documento em PDF. Você pode executar invocação semelhante em um JSP usando o seguinte código. A principal diferença é que o código a seguir usa o Sling ScriptHelper para acessar o GeneratePdfServiceClient.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### Iniciando via ServiceClientFactory {#starting-via-serviceclientfactory}

A classe ServiceClientFactory é necessária em alguns casos. Por exemplo, você precisa que ServiceClientFactory chame processos.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## Suporte para RunAs {#runas-support}

Quase todos os serviços de documento no LiveCycle exigem autenticação. Você pode usar qualquer uma das seguintes opções para iniciar esses serviços sem fornecer credenciais explícitas no código:

### lista de permissões configuração de  {#allowlist-configuration}

A configuração do SDK do cliente do LiveCycle contém uma configuração sobre nomes de serviço. Essa configuração é uma lista de serviços para os quais a lógica de invocação usa credencial de administrador pronta para uso. Por exemplo, se você adicionar serviços DiretoryManager (parte da API de Gerenciamento de Usuário) a essa lista, qualquer código de cliente poderá usar diretamente o serviço e a camada de invocação passará automaticamente as credenciais configuradas como parte da solicitação enviada para o servidor do LiveCycle

### RunAsManager {#runasmanager}

Como parte da integração, é fornecido um novo serviço RunAsManager. Ele permite que você controle programaticamente as credenciais a serem usadas ao fazer chamadas para o servidor do LiveCycle.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

Se quiser passar credenciais diferentes, você poderá usar o método sobrecarregado que utiliza uma instância PasswordCredential.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### Propriedade InvocationRequest {#invocationrequest-property}

Se você chamar um processo ou usar diretamente a classe ServiceClientFactory e criar um InvocationRequest, poderá especificar uma propriedade para indicar que a camada de invocação deve usar credenciais configuradas.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Lista de serviços de documento {#document-services-list}

### Pacote de API do SDK do cliente do Adobe LiveCycle {#adobe-livecycle-client-sdk-api-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Dependências de Maven {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do SDK do cliente do Adobe LiveCycle {#adobe-livecycle-client-sdk-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Dependências de Maven {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Pacote do cliente Adobe LiveCycle TaskManager {#adobe-livecycle-taskmanager-client-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Dependências de Maven {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente Adobe LiveCycle Workflow {#adobe-livecycle-workflow-client-bundle}

O seguinte serviço está disponível:

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Dependências de Maven {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente Adobe LiveCycle PDF Generator {#adobe-livecycle-pdf-generator-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Dependências de Maven {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente do Adobe LiveCycle Application Manager {#adobe-livecycle-application-manager-client-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Dependências de Maven {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente do Assembler do Adobe LiveCycle {#adobe-livecycle-assembler-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Dependências de Maven {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente de integração de dados de formulário do Adobe LiveCycle {#adobe-livecycle-form-data-integration-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Dependências de Maven {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente Adobe LiveCycle Forms {#adobe-livecycle-forms-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Dependências de Maven {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente Adobe LiveCycle Output {#adobe-livecycle-output-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.output.client.OutputClient

#### Dependências de Maven {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente Adobe LiveCycle Reader Extensions {#adobe-livecycle-reader-extensions-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Dependências de Maven {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente do Adobe LiveCycle Rights Manager {#adobe-livecycle-rights-manager-client-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Dependências de Maven {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do cliente de assinaturas do Adobe LiveCycle {#adobe-livecycle-signatures-client-bundle}

O seguinte serviço está disponível:

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Dependências de Maven {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente Truststore do Adobe LiveCycle {#adobe-livecycle-truststore-client-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Dependências de Maven {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Pacote do Cliente do Repositório do Adobe LiveCycle {#adobe-livecycle-repository-client-bundle}

Os seguintes serviços estão disponíveis:

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Dependências de Maven {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
