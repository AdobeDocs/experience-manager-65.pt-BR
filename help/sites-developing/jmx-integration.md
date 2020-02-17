---
title: Integração de serviços com o console JMX
seo-title: Integração de serviços com o console JMX
description: Exponha os atributos e as operações do serviço para permitir que as tarefas administrativas sejam executadas criando e implantando MBeans para gerenciar serviços usando o Console JMX
seo-description: Exponha os atributos e as operações do serviço para permitir que as tarefas administrativas sejam executadas criando e implantando MBeans para gerenciar serviços usando o Console JMX
uuid: 4a489a24-af10-4505-8333-aafc0c81dd3e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 83c590e0-2e6c-4499-a6ea-216e4c7bc43c
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Integração de serviços com o console JMX{#integrating-services-with-the-jmx-console}

Crie e implante MBeans para gerenciar serviços usando o console JMX. Exponha os atributos e as operações do serviço para permitir a execução de tarefas administrativas.

Para obter informações sobre como usar o Console JMX, consulte [Monitorando recursos do servidor usando o console](/help/sites-administering/jmx-console.md)JMX.

## A estrutura JMX no Felix e no CQ5 {#the-jmx-framework-in-felix-and-cq}

Na plataforma Apache Felix, você implanta MBeans como serviços OSGi. Quando um serviço MBean é registrado no Registro de serviços OSGi, o módulo Aries JMX Whiteboard registra automaticamente o MBean no Servidor MBean. O MBean fica disponível para o Console JMX, que expõe os atributos e operações públicos.

![quadro](assets/jmxwhiteboard.png)

## Criar MBeans para CQ5 e CRX {#creating-mbeans-for-cq-and-crx}

Os MBeans que você cria para gerenciar recursos do CQ5 ou do CRX são baseados na interface javax.management.DynamicMBean. Para criá-los, siga os padrões de design comuns definidos na especificação JMX:

* Crie a interface de gerenciamento, incluindo get, set e is métodos para definir atributos e outros métodos para definir operações.
* Crie a classe de implementação. A classe deve implementar DynamicMBean ou estender uma classe de implementação de DynamicMBean.
* Siga a convenção de nomenclatura padrão para que o nome da classe de implementação seja o nome da interface com o sufixo MBean.

Além de definir a interface de gerenciamento, a interface também define a interface de serviço OSGi. A classe de implementação implementa o serviço OSGi.

### Usando anotações para fornecer informações de MBean {#using-annotations-to-provide-mbean-information}

O pacote [com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) fornece várias anotações e classes para fornecer facilmente metadados MBean ao console JMX. Use essas anotações e classes em vez de adicionar informações diretamente ao objeto MBeanInfo do MBean.

**Anotações**

Adicione anotações à interface de gerenciamento para especificar metadados MBean. As informações são exibidas no console JMX para cada classe de implementação implantada. As anotações a seguir estão disponíveis (para obter informações completas, consulte o JavaDocs [com.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html)adobe.granite.jmx.annotation):

* **** Descrição: Fornece uma descrição da classe ou do método MBean. Quando usada na declaração de classe, a descrição é exibida na página Console JMX do MBean. Quando usada em um método, a descrição é exibida como texto de passagem para o atributo ou operação correspondente.
* **** Impacto: O impacto de um método. Valores de parâmetro válidos são os campos definidos por [javax.management.MBeanOperationInfo](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html).

* **** Nome: Especifica o nome a ser exibido para um parâmetro de operação. Use essa anotação para substituir o nome real do parâmetro de método usado na interface.
* **** OpenTypeInfo: Especifica a classe a ser usada para representar dados compostos ou dados tabulares no Console JMX. Para uso com Open MBeans
* **** TabularTypeInfo: Usado para anotar a classe usada para representar dados tabulares.

**Classes**

As classes são fornecidas para a criação de MBeans dinâmicos que consomem as anotações adicionadas às interfaces:

* **** AnnotatedStandardMBean: Uma subclasse da classe javax.management.StandardMBean que fornece automaticamente ao console JMX os metadados da anotação.
* **** OpenAnnotatedStandardMBean: Uma subclasse da classe AnnotatedStandardMBean para criar Mbeans abertos que consomem a anotação OpenTypeInfo.

### Desenvolvimento de MBeans {#developing-mbeans}

Normalmente, seu MBean é um reflexo do serviço OSGi que você deseja gerenciar. Na plataforma Felix, você cria o MBean como criaria para implantação em outras plataformas de servidor Java. Uma diferença principal é que você pode usar anotações para especificar informações do MBean:

* Interface de gerenciamento: Define atributos usando métodos getter, setter e is. Define operações usando qualquer outro método público. Usa anotações para fornecer metadados para o objeto BeanInfo.
* Classe MBean: Implementa a interface de gerenciamento. Estende a classe AnnotatedStandardMBean para que processe as anotações na interface.

O seguinte exemplo de MBean fornece informações sobre o repositório CRX. A interface usa a anotação Descrição para fornecer informações ao console JMX.

#### Interface de gerenciamento {#management-interface}

```java
package com.adobe.example.myapp;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes repository properties.")
public interface ExampleMBean {

    @Description("The name of the repository.")
    String getRepositoryName();

    @Description("The vendor of the repository.")
    String   getRepositoryVendor();

    @Description("The URL of repository vendor.")
    String getVendorUrl();
}
```

A classe de implementação usa o serviço SlingRepository para recuperar informações sobre o repositório CRX.

#### Classe de implementação MBean {#mbean-implementation-class}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

O gráfico a seguir mostra a página para este MBean no Console JMX.

![jmxdescription](assets/jmxdescription.png)

### Registrando MBeans {#registering-mbeans}

Quando você registra MBeans como um serviço OSGi, eles são automaticamente registrados no Servidor MBean. Para instalar um MBean no CQ5, inclua-o em um pacote e exporte o serviço MBean como faria com qualquer outro serviço OSGi.

Além dos metadados relacionados ao OSGi, você também deve fornecer metadados exigidos pelo módulo Aries JMX Whiteboard para registrar o MBean no servidor MBean:

* **** O nome da interface DynamicMBean: Declarar que o serviço MBean implementa a interface `javax.management.DynamicMBea`n. Esta declaração notifica o módulo Aries JMX Whiteboard de que o serviço é um serviço MBean.

* **** O domínio MBean e as propriedades principais: No Felix, você fornece essas informações como uma propriedade do serviço OSGi do MBean. Essas são as mesmas informações que você normalmente fornece ao Servidor MBean em um `javax.management.ObjectName` objeto.

Quando seu MBean é um reflexo de um serviço singular, somente uma única instância do serviço MBean é necessária. Nesse caso, se você usar o plug-in Felix SCR Maven, poderá usar as anotações Apache Felix Service Component Runtime (SCR) na classe de implementação MBean para especificar os metadados relacionados a JMX. Para instanciar várias instâncias de MBean, você pode criar outra classe que executa esse registro do serviço OSGi do MBean. Nesse caso, os metadados relacionados ao JMX são gerados em tempo de execução.

**Single MBean**

Os MBeans para os quais você pode definir todos os atributos e operações no momento do projeto podem ser implantados usando anotações SCR na classe de implementação MBean. No exemplo a seguir, o `value` atributo da `Service` anotação declara que o serviço implementa a `DynamicMBean` interface. O `name` atributo da `Property` anotação especifica o domínio JMX e as propriedades principais.

#### Classe de implementação MBean com anotações SCR {#mbean-implementation-class-with-scr-annotations}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

@Component(immediate = true)
@Property(name = "jmx.objectname", value="com.adobe.example:type=CRX")
@Service(value = DynamicMBean.class)
public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

**Várias instâncias de serviço MBean**

Para gerenciar várias instâncias de um serviço gerenciado, crie várias instâncias do serviço MBean correspondente. Além disso, as instâncias de serviço MBean devem ser criadas ou removidas quando as instâncias gerenciadas são iniciadas ou interrompidas. Você pode criar uma classe de gerenciador MBean para instanciar os serviços MBean no tempo de execução e gerenciar o ciclo de vida do serviço.

Use o BundleContext para registrar o MBean como um serviço OSGi. Inclua as informações relacionadas ao JMX no objeto Dictionary que você usa como argumento do método BundleContext.registerService.

No exemplo de código a seguir, o serviço ExampleMBean é registrado de forma programática. O objeto componentContext é ComponentContext, que fornece acesso a BundleContext.

#### Trecho de código: Registro de serviço MBean programático {#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

O exemplo MBean na próxima seção fornece mais detalhes.

Um gerenciador de serviços MBean é útil quando as configurações de serviço são armazenadas no repositório. O gerente pode recuperar informações do serviço e usá-las para configurar e criar o MBean correspondente. A classe manager também pode acompanhar eventos de alteração de repositório e atualizar os serviços MBean de acordo.

## Exemplo: Monitorando modelos de fluxo de trabalho usando JMX {#example-monitoring-workflow-models-using-jmx}

O MBean neste exemplo fornece informações sobre os modelos do CQ5 Workflow armazenados no repositório. Uma classe de gerenciador MBean cria MBeans com base em modelos de Fluxo de trabalho que são armazenados no repositório e registra seu serviço OSGi no tempo de execução. Este exemplo consiste em um único pacote contendo os seguintes membros:

* WorkflowMBean: A interface de gerenciamento.
* WorkflowMBeanImpl: A classe de implementação MBean.
* WorkflowMBeanManager: A interface da classe do gerenciador MBean.
* WorkflowMBeanManagerImpl: A classe de implementação do gerenciador MBean.

**** Observação: Para simplificar, o código neste exemplo não executa o registro em log ou reage a exceções lançadas.

WorkflowMBeanManagerImpl inclui um método de ativação de componente. Quando o componente é ativado, o método executa as seguintes tarefas:

* Obtém um BundleContext para o pacote.
* Consulta o repositório para obter os caminhos dos modelos de Fluxo de trabalho existentes.
* Cria MBeans para cada modelo de Fluxo de trabalho.
* Registra os MBeans no registro de serviço OSGi.

Os metadados MBean aparecem no Console JMX com o domínio com.adobe.example, o tipo workflow_model e Propriedades é o caminho do nó de configuração do modelo de fluxo de trabalho.

![jmxworkflow](assets/jmxworkflowmbean.png)

### O exemplo MBean {#the-example-mbean}

Este exemplo requer uma interface e uma implementação MBean que sejam reflexos na `com.day.cq.workflow.model.WorkflowModel` interface. O MBean é muito simples para que o exemplo possa se concentrar nos aspectos de configuração e implantação do design. O MBean expõe um único atributo, o nome do modelo.

#### Interface WorkflowMBean {#workflowmbean-interface}

```java
package com.adobe.example.myapp.api;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes Workflow model properties.")
public interface WorkflowMBean {

 @Description("The name of the Workflow model.")
 String getModelName();
}
```

#### WorkflowMBeanImpl {#workflowmbeanimpl}

```java
package com.adobe.example.myapp.impl;

import javax.management.NotCompliantMBeanException;

import com.day.cq.workflow.model.WorkflowModel;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

public class WorkflowMBeanImpl extends AnnotatedStandardMBean implements WorkflowMBean {

 WorkflowModel model;

 protected WorkflowMBeanImpl(WorkflowModel inmodel)
   throws NotCompliantMBeanException {
  super(WorkflowMBean.class);
  model=inmodel;
 }

 public String getModelName() {
  return model.getTitle();
 }
}
```

### O exemplo do MBean Manager {#the-example-mbean-manager}

O serviço WorkflowMBeanManager inclui o método de ativação de componente que cria serviços WorkflowMBean. A implementação do serviço inclui os seguintes métodos:

* ativar: O ativador de componentes. Cria a sessão JCR para ler os nós de configuração WorkflowModel. O nó raiz onde as configurações de modelo são armazenadas é definido em um campo estático. O nome do nó de configuração também é definido em um campo estático. Este método chama outros métodos que obtêm os caminhos do modelo de nó e criam o modelo WorkflowMBeans.
* getModelIds: Atravessa o repositório abaixo do nó raiz e recupera o caminho de cada nó modelo.
* makeMBean: Usa o caminho do modelo para criar um objeto WorkflowModel, cria um WorkflowMBean para ele e registra seu serviço OSGi.

>[!NOTE]
>
>A implementação WorkflowMBeanManager só cria serviços MBean para configurações de modelo que existem quando o componente é ativado. Uma implementação mais robusta escuta os eventos do repositório relacionados às novas configurações do modelo e às alterações ou exclusões da configuração do modelo existente. Quando ocorre uma alteração, o gerente pode criar, modificar ou remover o serviço WorkflowMBean correspondente.


#### Interface WorkflowMBeanManager {#workflowmbeanmanager-interface}

```java
package com.adobe.example.myapp.api;

public interface WorkflowMBeanManager {

}
```

#### WorkflowMBeanManagerImpl {#workflowmbeanmanagerimpl}

```java
package com.adobe.example.myapp.impl;

import java.util.*;

import org.apache.felix.scr.annotations.*;

import javax.jcr.Session;
import javax.jcr.Node;
import javax.jcr.NodeIterator;
import javax.jcr.RepositoryException;
import javax.management.ObjectName;

import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.framework.ServiceRegistration;
import org.osgi.service.component.ComponentContext;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.workflow.WorkflowService;
import com.day.cq.workflow.WorkflowSession;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.example.myapp.api.WorkflowMBeanManager;

/**Instantiates and registers WorkflowMBean services */
@Component(immediate=true)
@Service(value=WorkflowMBeanManager.class)
public class WorkflowMBeanManagerImpl implements WorkflowMBeanManager {
 //The ComponentContext provides access to the BundleContext
 private ComponentContext componentContext;

 //Use the SlingRepository service to read model nodes
 @Reference
        private SlingRepository repository = null;

 //Use the WorkflowService service to create WorkflowModel objects
 @Reference
 private WorkflowService workflowservice = null;

  private Session session;

         //Details about model nodes
  private static final String MODEL_ROOT ="/etc/workflow/models";
  private static final String MODEL_NODE = "model";

  private Set<String> modelIds = new HashSet<String>();

        //Storage for ServiceRegistrations for MBean services
  private Collection<ServiceRegistration> mbeanRegistrations= new Vector<ServiceRegistration>(0,1);

 @Activate
        protected void activate(ComponentContext ctx) {
             //Traverse the repository and load the model nodes
             try {
                   session = repository.loginAdministrative(null);
                   // load and store model node paths
                   if (session.nodeExists(MODEL_ROOT)) {
                          getModelIds(session.getNode(MODEL_ROOT));
                   }
                   //Create MBeans for each model
                   for(String modid: modelIds){
                    makeMBean(modid);
                    }
             }catch(Exception e){ }
          }

        /**
         * Add JMX domain and key properties to a collection
         * Instantiate a WorkflowModel and its WorkflowMBeanImpl object
         * Register the MBean OSGi service
         */
 private void makeMBean(String modelId) {
             // create MBean for the model
             try {
                 Dictionary<String, String> mbeanProps = new Hashtable<String, String>();
                 //These properties appear on the JMX Console home page
                 mbeanProps.put("jmx.objectname", "com.adobe.example:type=workflow_model,id=" + ObjectName.quote(modelId));
                 WorkflowSession wfsession = workflowservice.getWorkflowSession(session);
                 WorkflowMBeanImpl mbean = new WorkflowMBeanImpl(wfsession.getModel(modelId));

                ServiceRegistration serviceregistration = componentContext.getBundleContext().registerService(WorkflowMBean.class.getName(), mbean, mbeanProps);
                //Store the ServiceRegistration objects for deactivation
                mbeanRegistrations.add(serviceregistration);
             } catch (Throwable t) {}
         }

        /**
         * Traverses the repository branch below a given Node. Stores the path of each model node.
         */
 private void getModelIds(Node node) throws RepositoryException {
  try{
                     NodeIterator iter = node.getNodes();
                     while (iter.hasNext()) {
                           Node n = iter.nextNode();
                           //Look for "jcr:content" nodes
                           if (n.getName().equals("jcr:content")) {
                                //get the path of the model node and save it
                                if(n.hasNode(MODEL_NODE)){
                                      modelIds.add(n.getNode(MODEL_NODE).getPath());
                                 }
                           } else{
                                   //Scan child nodes
                                   getModelIds(n);
                           }
                       }
  }catch(Exception e){ }
       }

        /**
         * Log out of the JCR session and unregister WorkflowMBean services
         */
        @Deactivate
        protected void deactivate() {
          session.logout();
          session=null;
          for(ServiceRegistration sr:mbeanRegistrations){
         sr.unregister();
          }
        }
}
```

### O arquivo POM para o Exemplo MBean {#the-pom-file-for-the-example-mbean}

Para sua conveniência, você pode copiar e colar o seguinte código XML no arquivo pom.xml do projeto para criar o pacote de componentes. O POM faz referência a vários plug-ins e dependências necessários.

**Plug-ins:**

* Plug-in Apache Maven Compiler: Compila classes Java do código-fonte.
* Plug-in Apache Felix Maven Bundle: Cria o pacote e o manifesto
* Plug-in Apache Felix Maven SCR: Cria o arquivo descritor do componente e configura o cabeçalho do manifesto service-component.

**** Observação: No momento da gravação, o plug-in maven scr não é compatível com o plug-in m2e para o Eclipse. (Consulte o bug [Felix 3170](https://issues.apache.org/jira/browse/FELIX-3170).) Para usar o Eclipse IDE, instale o Maven e use a interface de linha de comando para executar compilações.

#### Exemplo de arquivo POM {#example-pom-file}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.2-SNAPSHOT</version>
  <name>mbean-simple</name>
  <url>www.adobe.com</url>
  <description>A simple MBean</description>
  <packaging>bundle</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-scr-plugin</artifactId>
                <version>1.7.2</version>
                <executions>
                    <execution>
                        <id>generate-scr-scrdescriptor</id>
              <goals>
                 <goal>scr</goal>
              </goals>
            </execution>
         </executions>
            </plugin>
             <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.6.0</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.api</artifactId>
            <version>2.0.8</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr</artifactId>
            <version>1.6.1-R1236132</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.jcr.api</artifactId>
            <version>2.0.4</version>
        </dependency>
        <dependency>
            <groupId>com.adobe.granite</groupId>
            <artifactId>com.adobe.granite.jmx</artifactId>
            <version>0.1.6</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
       <groupId>com.day.cq.wcm</groupId>
       <artifactId>cq-wcm-mobile-api</artifactId>
       <version>5.5.2</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>com.day.cq.workflow</groupId>
       <artifactId>cq-workflow-api</artifactId>
       <version>5.5.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>javax.jcr</groupId>
       <artifactId>jcr</artifactId>
       <version>2.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
                <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.6.4</version>
  <scope>provided</scope>
 </dependency>
    </dependencies>
</project>
```

Adicione o seguinte perfil ao seu arquivo de configurações do Mac para usar o repositório público da Adobe.

#### Perfil Maven {#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```
