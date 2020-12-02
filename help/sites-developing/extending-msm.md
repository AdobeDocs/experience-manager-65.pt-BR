---
title: Extensão do Gerenciador de vários sites
seo-title: Extensão do Gerenciador de vários sites
description: Esta página ajuda a estender as funcionalidades do Multi Site Manager
seo-description: Esta página ajuda a estender as funcionalidades do Multi Site Manager
uuid: dfa7d050-29fc-4401-8d4d-d6ace6b49bea
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6128c91a-4173-42b4-926f-bbbb2b54ba5b
docset: aem65
translation-type: tm+mt
source-git-commit: 3a1d02fc1bc561b54e57cf91abc8f4406ba8c365
workflow-type: tm+mt
source-wordcount: '2601'
ht-degree: 2%

---


# Extensão do Multi Site Manager{#extending-the-multi-site-manager}

Esta página ajuda a estender as funcionalidades do Multi Site Manager:

* Saiba mais sobre os principais membros da API Java MSM.
* Crie uma nova ação de sincronização que pode ser usada em uma configuração de implantação.
* Modifique o idioma padrão e os códigos de país.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Esta página deve ser lida juntamente com [Reutilizando conteúdo: Gerenciador de vários sites](/help/sites-administering/msm.md).
>
>As seguintes seções da reestruturação do repositório Sites no AEM 6.4 também podem ser de interesse:
>* [Configurações de Blueprint do Multi-site Manager](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-blueprint-configurations)
>* [Configurações de implantação do Multi-site Manager](https://docs.adobe.com/content/help/en/experience-manager-64/deploying/restructuring/sites-repository-restructuring-in-aem-6-4.html#multi-site-manager-rollout-configurations)


>[!CAUTION]
>
>O Multi Site Manager e sua API são usados durante a criação de um site, portanto, são destinados apenas ao uso em um ambiente do autor.

## Visão geral da API Java {#overview-of-the-java-api}

O Gerenciamento de vários sites consiste nos seguintes pacotes:

* [com.day.cq.wcm.msm.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

Os principais objetos de API MSM interagem da seguinte maneira (consulte também [Termos usados](/help/sites-administering/msm.md#terms-used)):

![chlimage_1-73](assets/chlimage_1-73.png)

* **`Blueprint`**

   Um `Blueprint` (como em [configuração do blueprint](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) especifica as páginas a partir das quais uma live copy pode herdar conteúdo.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   * O uso de uma configuração blueprint ( `Blueprint`) é opcional, mas:

      * Permite que o autor use a opção **Rollout** na origem (para modificações de envio (explicitamente) para cópias online herdadas dessa origem).
      * Permite que o autor use **Criar Site**; isso permite que o usuário selecione facilmente os idiomas e configure a estrutura da live copy.
      * Define a configuração padrão de implementação para qualquer cópia online resultante.

* **`LiveRelationship`** O  `LiveRelationship` especifica a conexão (relação) entre um recurso na live copy branch e seu recurso equivalente de origem/blueprint.

   * Os relacionamentos são usados ao realizar herança e implantação.
   * `LiveRelationship` os objetos fornecem acesso (referências) às configurações de implantação (  `RolloutConfig`)  `LiveCopy`e aos  `LiveStatus` objetos relacionados ao relacionamento.

   * Por exemplo, uma live copy é criada em `/content/copy/us` a partir da fonte/blueprint em `/content/we-retail/language-masters`. Os recursos `/content/we.retail/language-masters/en/jcr:content` e `/content/copy/us/en/jcr:content` formam uma relação.

* **`LiveCopy`** `LiveCopy` contém os detalhes de configuração para os relacionamentos (  `LiveRelationship`) entre os recursos de live copy e seus recursos de origem/blueprint.

   * Use a classe `LiveCopy` para acessar o caminho da página, o caminho da página de origem/blueprint, as configurações de implantação e se as páginas secundárias também estão incluídas no `LiveCopy`.

   * Um nó `LiveCopy` é criado sempre que **Criar Site** ou **Criar Live Copy** é usado.

* **`LiveStatus`**

   `LiveStatus` objetos fornecem acesso ao status de tempo de execução de um  `LiveRelationship`. Use para query do status de sincronização de uma live copy.

* **`LiveAction`**

   Um `LiveAction` é uma ação executada em cada recurso que está envolvido na implementação.

   * O LiveActions é gerado somente por RolloutConfigs.

* **`LiveActionFactory`**

   Cria `LiveAction` objetos com uma configuração `LiveAction`. As configurações são armazenadas como recursos no repositório.

* **`RolloutConfig`** O  `RolloutConfig` mantém uma lista de  `LiveActions`, a ser usada quando acionada. O `LiveCopy` herda o `RolloutConfig` e o resultado está presente no `LiveRelationship`.

   * A configuração de uma live copy pela primeira vez também usa um RolloutConfig (que aciona o LiveActions).

## Criando uma Nova Ação de Sincronização {#creating-a-new-synchronization-action}

Crie ações de sincronização personalizadas para usar com suas configurações de implementação. Crie uma ação de sincronização quando as [ações instaladas](/help/sites-administering/msm-sync.md#installed-synchronization-actions) não atenderem aos requisitos específicos do aplicativo. Para fazer isso, crie duas classes:

* Uma implementação da interface [ `com.day.cq.wcm.msm.api.LiveAction`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) que executa a ação.
* Um componente OSGI que implementa a interface [ `com.day.cq.wcm.msm.api.LiveActionFactory`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) e cria instâncias da sua classe `LiveAction`.

O `LiveActionFactory` cria instâncias da classe `LiveAction` para uma determinada configuração:

* `LiveAction` as classes incluem os seguintes métodos:

   * `getName`: Retorna o nome da ação O nome é usado para fazer referência à ação, por exemplo, em configurações de implantação.
   * `execute`: Executa as tarefas da ação.

* `LiveActionFactory` as classes incluem os seguintes membros:

   * `LIVE_ACTION_NAME`: Um campo que contém o nome do associado  `LiveAction`. Esse nome deve coincidir com o valor retornado pelo método `getName` da classe `LiveAction`.

   * `createAction`: Cria uma instância do  `LiveAction`. O parâmetro opcional `Resource` pode ser usado para fornecer informações de configuração.

   * `createsAction`: Retorna o nome do associado  `LiveAction`.

### Acessar o nó de configuração do LiveAction {#accessing-the-liveaction-configuration-node}

Use o nó de configuração `LiveAction` no repositório para armazenar informações que afetam o comportamento do tempo de execução da instância `LiveAction`. O nó no repositório que armazena a configuração `LiveAction` está disponível para o objeto `LiveActionFactory` no tempo de execução. Portanto, você pode adicionar propriedades ao nó de configuração e usá-las na implementação `LiveActionFactory`, conforme necessário.

Por exemplo, um `LiveAction` precisa armazenar o nome do autor do blueprint. Uma propriedade do nó de configuração inclui o nome da propriedade da página de blueprint que armazena as informações. No tempo de execução, `LiveAction` recupera o nome da propriedade da configuração e obtém o valor da propriedade.

O parâmetro do método ` [LiveActionFactory](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html).createAction` é um objeto `Resource`. Este objeto `Resource` representa o nó `cq:LiveSyncAction` para esta ação em tempo real na configuração de implementação; consulte [Criação de uma configuração de implantação](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). Como de costume ao usar um nó de configuração, você deve adaptá-lo a um objeto `ValueMap`:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Acessar nós de Público alvo, nós de origem e o LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Os seguintes objetos são fornecidos como parâmetros do método `execute` do objeto `LiveAction`:

* Um objeto [ `Resource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) que representa a origem do Live Copy.
* Um objeto `Resource` que representa o público alvo da Live Copy.
* O objeto [ `LiveRelationship`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) para a live copy.
* O valor `autoSave` indica se `LiveAction` deve salvar as alterações feitas no repositório.

* O valor reset indica o modo de redefinição de implantação.

Desses objetos, você pode obter todas as informações sobre o `LiveCopy`. Você também pode usar os objetos `Resource` para obter os objetos `ResourceResolver`, `Session` e `Node`. Esses objetos são úteis para manipular o conteúdo do repositório:

Na primeira linha do código a seguir, source é o objeto `Resource` da página de origem:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Os argumentos `Resource` podem ser `null` ou `Resources` objetos que não se adaptam a `Node` objetos, como [ `NonExistingResource`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/NonExistingResource.html).

## Criando uma nova configuração de implantação {#creating-a-new-rollout-configuration}

Crie uma configuração de implementação quando as configurações de implementação instaladas não atenderem aos requisitos do aplicativo:

* [Criar a configuração de implementação](#create-the-rollout-configuration).
* [Adicionar ações de sincronização à configuração de implementação](#add-synchronization-actions-to-the-rollout-configuration).

A nova configuração de implementação estará disponível para você quando definir configurações de implementação em um blueprint ou página de Live Copy.

>[!NOTE]
>
>Consulte também as [práticas recomendadas para personalizar implantações](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Criar a configuração de implantação {#create-the-rollout-configuration}

Para criar uma nova configuração de implantação:

1. CRXDE Lite aberto; por exemplo:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Vá até :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Esta é a versão personalizada do projeto de:
   >`/libs/msm/wcm/rolloutconfigs`
   >Deve ser criado se esta for a sua primeira configuração.

   >[!NOTE]
   >
   >Você não deve alterar nada no caminho /libs.
   >Isso ocorre porque o conteúdo de /libs é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos).
   >O método recomendado para configuração e outras alterações é:
   >* Recrie o item necessário (isto é, como ele existe em /libs) em /apps
   >* Faça quaisquer alterações em /apps


1. Em **Create** um nó com as seguintes propriedades:

   * **Nome**: O nome do nó da configuração de implantação. md#installed-synchronization-actions), por exemplo `contentCopy` ou `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Adicione as seguintes propriedades a este nó:
   * **Nome**: `jcr:title`

      **Tipo**: `String`
      **Valor**: Um título de identificação que será exibido na interface do usuário.
   * **Nome**: `jcr:description`

      **Tipo**: `String`
      **Valor**: Uma descrição opcional.
   * **Nome**: `cq:trigger`

      **Tipo**: `String`
      **Valor**: O  [Acionador ](/help/sites-administering/msm-sync.md#rollout-triggers) de implantação a ser usado. Selecionar de:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Clique em **Salvar tudo**.

### Adicionar ações de sincronização à configuração de implantação {#add-synchronization-actions-to-the-rollout-configuration}

As configurações de implantação são armazenadas abaixo do nó [configuração de implantação](#create-the-rollout-configuration) que você criou no nó `/apps/msm/<your-project>/rolloutconfigs`.

Adicione nós secundários do tipo `cq:LiveSyncAction` para adicionar ações de sincronização à configuração de implementação. A ordem dos nós de ação de sincronização determina a ordem em que as ações ocorrem.

1. Ainda no CRXDE Lite, selecione o nó [Configuração de implantação](#create-the-rollout-configuration).

   Por exemplo:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Crie** um nó com as seguintes propriedades de nó:

   * **Nome**: O nome do nó da ação de sincronização.
O nome deve ser igual ao **Nome da ação** na tabela em [Ações de sincronização](/help/sites-administering/msm-sync.md#installed-synchronization-actions), por exemplo `contentCopy` ou `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Adicione e configure quantos nós de ação de sincronização forem necessários. Reorganize os nós de ação para que sua ordem corresponda à ordem em que você deseja que ocorram. O nó de ação mais alto ocorre primeiro.

## Criação e uso de uma classe Simple LiveActionFactory {#creating-and-using-a-simple-liveactionfactory-class}

Siga os procedimentos desta seção para desenvolver um `LiveActionFactory` e usá-lo em uma configuração de implantação. Os procedimentos usam Maven e Eclipse para desenvolver e implantar o `LiveActionFactory`:

1. [Crie o ](#create-the-maven-project) projeto maven e importe-o para o Eclipse.
1. [Adicione ](#add-dependencies-to-the-pom-file) dependências ao arquivo POM.
1. [Implemente a  `LiveActionFactory` ](#implement-liveactionfactory) interface e implante o pacote OSGi.
1. [Criar a configuração de implementação](#create-the-example-rollout-configuration).
1. [Crie a live copy](#create-the-live-copy).

O projeto Maven e o código-fonte da classe Java estão disponíveis no repositório Git público.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto experienceemanager-java-msmrollout no GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Criar o projeto Maven {#create-the-maven-project}

O procedimento a seguir requer que você tenha adicionado o perfil adobe-public ao arquivo de configurações Maven.

* Para obter informações sobre o perfil adobe-public, consulte [Obtenção do Plug-in Content Package Maven](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Para obter informações sobre o arquivo de configurações Maven, consulte a Maven [Settings Reference](https://maven.apache.org/settings.html).

1. Abra um terminal ou uma sessão de linha de comando e altere o diretório para apontar para o local onde o projeto deve ser criado.
1. Digite o seguinte comando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Especifique os seguintes valores no prompt interativo:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`:  `MyLiveActionFactory`
   * `version`:  `1.0-SNAPSHOT`
   * `package`:  `MyPackage`
   * `appsFolderName`:  `myapp`
   * `artifactName`:  `MyLiveActionFactory package`
   * `packageGroup`:  `myPackages`

1. Eclipse do start e [importe o projeto Maven](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Adicionar dependências ao arquivo POM {#add-dependencies-to-the-pom-file}

Adicione dependências para que o compilador do Eclipse possa fazer referência às classes usadas no código `LiveActionFactory`.

1. No Explorador de projetos do Eclipse, abra o arquivo:

   `MyLiveActionFactory/pom.xml`

1. No editor, clique na guia `pom.xml` e localize a seção `project/dependencyManagement/dependencies`.
1. Adicione o XML a seguir dentro do elemento `dependencyManagement` e salve o arquivo.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Abra o arquivo POM para o pacote a partir de **Project Explorer** em `MyLiveActionFactory-bundle/pom.xml`.
1. No editor, clique na guia `pom.xml` e localize a seção projeto/dependências. Adicione o XML a seguir dentro do elemento dependências e salve o arquivo:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementação do LiveActionFactory {#implement-liveactionfactory}

A classe `LiveActionFactory` a seguir implementa um `LiveAction` que registra mensagens sobre as páginas de origem e de público alvo e copia a propriedade `cq:lastModifiedBy` do nó de origem para o nó de público alvo. O nome da ação live é `exampleLiveAction`.

1. No Eclipse Project Explorer, clique com o botão direito do mouse no pacote `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` e clique em **Novo** > **Classe**. Para **Nome**, digite `ExampleLiveActionFactory` e clique em **Concluir**.
1. Abra o arquivo `ExampleLiveActionFactory.java`, substitua o conteúdo pelo seguinte código e salve o arquivo.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Usando o terminal ou a sessão de comando, altere o diretório para o diretório `MyLiveActionFactory` (o diretório do projeto Maven). Em seguida, insira o seguinte comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   O arquivo AEM `error.log` deve indicar que o pacote foi iniciado.

   Por exemplo, [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Criar a Exemplo de Configuração de Rollout {#create-the-example-rollout-configuration}

Crie a configuração de implantação MSM que usa o `LiveActionFactory` que você criou:

1. Crie e configure uma [Configuração de implantação com o procedimento padrão](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) - e use as propriedades:

   * **Título**: Exemplo de configuração de implantação
   * **Nome**: examplerolloutconfig
   * **cq:trigger**:  `publish`

### Adicione a ação em tempo real à Exemplo de configuração de implantação {#add-the-live-action-to-the-example-rollout-configuration}

Configure a configuração de implantação criada no procedimento anterior para que ela use a classe `ExampleLiveActionFactory`.

1. CRXDE Lite aberto; por exemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Crie o seguinte nó em `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nome**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Clique em **Salvar tudo**.
1. Selecione o nó `exampleLiveAction` e adicione a seguinte propriedade:

   * **Nome**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valor**:  `true`

   Essa propriedade indica para a classe `ExampleLiveAction` que a propriedade `cq:LastModifiedBy` deve ser replicada da origem para o nó do público alvo.

1. Clique em **Salvar tudo**.

### Criar a Live Copy {#create-the-live-copy}

[Crie uma ](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) cópia ao vivo da ramificação Inglês/Produtos do Site de Referência We.Retail usando sua configuração de implementação:

* **Fonte**:  `/content/we-retail/language-masters/en/products`

* **Configuração** de implantação: Exemplo de configuração de implantação

Ative a página **Products** (inglês) da ramificação de origem e observe as mensagens de log geradas pela classe `LiveAction`:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a new node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Alteração de nomes de idiomas e países padrão {#changing-language-names-and-default-countries}

AEM usa um conjunto padrão de códigos de idioma e país.

* O código de idioma padrão é o código de duas letras minúsculas, conforme definido pela ISO-639-1.
* O código padrão do país é o código de duas letras em minúsculas ou maiúsculas, conforme definido pela ISO 3166.

O MSM usa uma lista armazenada de códigos de idioma e país para determinar o nome do país associado ao nome da versão de idioma da sua página. Você pode alterar os seguintes aspectos da lista, se necessário:

* Títulos de idioma
* Nomes de países
* Países padrão para idiomas (para códigos como `en`, `de`, entre outros)

A lista de idioma é armazenada abaixo do nó `/libs/wcm/core/resources/languages`. Cada nó filho representa um idioma ou um país de idioma:

* O nome do nó é o código do idioma (como `en` ou `de`), ou o código language_country (como `en_us` ou `de_ch`).

* A propriedade `language` do nó armazena o nome completo do idioma para o código.
* A propriedade `country` do nó armazena o nome completo do país para o código.
* Quando o nome do nó consiste apenas em um código de idioma (como `en`), a propriedade country é `*`, e uma propriedade adicional `defaultCountry` armazena o código do idioma-país para indicar o país a ser usado.

![chlimage_1-76](assets/chlimage_1-76.png)

Para modificar os idiomas:

1. Abra o CRXDE Lite no navegador da Web; por exemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Selecione a pasta `/apps` e clique em **Criar**, em seguida **Criar pasta.**

   Nomeie a nova pasta `wcm`.

1. Repita a etapa anterior para criar a árvore de pastas `/apps/wcm/core`. Crie um nó do tipo `sling:Folder` em `core` chamado `resources`. <!-- ![chlimage_1-77](assets/chlimage_1-77.png) -->

1. Clique com o botão direito do mouse no nó `/libs/wcm/core/resources/languages` e clique em **Copiar**.
1. Clique com o botão direito do mouse na pasta `/apps/wcm/core/resources` e clique em **Colar**. Modifique os nós secundários conforme necessário.
1. Clique em **Salvar tudo**.
1. Clique em **Ferramentas**, **Operações** em seguida **Console Web**. Nesse console, clique em **OSGi** e **Configuração**.
1. Localize e clique em **Gerente de Idioma WCM do Day CQ**, altere o valor de **Lista de Idioma** para `/apps/wcm/core/resources/languages` e clique em **Salvar**.

   ![chlimage_1-78](assets/chlimage_1-78.png)

## Configuração de bloqueios MSM em propriedades da página (interface habilitada para toque) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Ao criar uma propriedade de página personalizada, talvez seja necessário considerar se a nova propriedade deve ser qualificada para implantação em qualquer cópia ao vivo.

Por exemplo, se duas novas propriedades de página estiverem sendo adicionadas:

* Email de contato:

   * Esta propriedade não precisa ser distribuída, pois será diferente em cada país (ou marca, etc.).

* Estilo visual principal:

   * O requisito do projeto é que essa propriedade seja distribuída como é (normalmente) comum a todos os países (ou marcas, etc.).

Em seguida, é necessário garantir que:

* Email de contato:

   * Está excluído das propriedades distribuídas; consulte [Excluindo Propriedades e Tipos de Nó da Sincronização](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Estilo visual principal:

   * Certifique-se de que você não tem permissão para editar essa propriedade na interface habilitada para toque, a menos que a herança seja cancelada, e também de que você possa reinstalar a herança; isso é controlado ao clicar nos links de cadeia/cadeia quebrada que alternam para indicar o status da conexão.

Se uma propriedade de página está sujeita a implantação e, portanto, sujeita a cancelamento/reinstalação da herança durante a edição, é controlada pela propriedade de diálogo:

* `cq-msm-lockable`

   * é aplicável a itens em uma caixa de diálogo de interface habilitada para toque
   * criará o símbolo de elo de cadeia na caixa de diálogo
   * permite a edição somente se a herança for cancelada (o link da cadeia está quebrado)
   * aplica-se somente ao primeiro nível filho do recurso
   * **Tipo**: `String`

   * **Valor**: seja titular do nome da propriedade em questão (e seja comparável ao valor da propriedade  `name`; por exemplo, consulte
      `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Quando `cq-msm-lockable` for definido, a quebra/fechamento da cadeia interagirá com a MSM da seguinte maneira:

* se o valor de `cq-msm-lockable` for:

   * **Relativo**  (por exemplo,  `myProperty` ou  `./myProperty`)

      * ela adicionará e removerá a propriedade de `cq:propertyInheritanceCancelled`.
   * **Absoluto**  (por exemplo,  `/image`)

      * quebrar a cadeia cancelará a herança adicionando a combinação `cq:LiveSyncCancelled` a `./image` e definindo `cq:isCancelledForChildren` como `true`.

      * fechar a cadeia reverterá a herança.


>[!NOTE]
>
>`cq-msm-lockable` aplica-se ao primeiro nível filho do recurso a ser editado e não é funcional em nenhum ancestral de nível mais profundo, independentemente do valor ser definido como absoluto ou relativo.

>[!NOTE]
>
>Quando você reativa a herança, a propriedade da página de cópia ativa não é sincronizada automaticamente com a propriedade source. Você pode solicitar manualmente uma sincronização, se necessário.
