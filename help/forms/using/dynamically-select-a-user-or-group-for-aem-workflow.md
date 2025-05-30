---
title: Selecionar dinamicamente um usuário ou grupo para etapas de fluxo de trabalho centradas no AEM Forms
description: Saiba como selecionar um usuário ou grupo para um workflow do AEM Forms no tempo de execução.
content-type: troubleshooting
topic-tags: publish
exl-id: 3c48660e-5e4f-4615-82d4-9f1f285c2a39
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Selecionar dinamicamente um usuário ou grupo para etapas de fluxo de trabalho centradas no AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Saiba como selecionar um usuário ou grupo para um workflow do AEM Forms no tempo de execução.

Em grandes organizações, há requisitos para selecionar usuários dinamicamente para um processo. Por exemplo, selecionar um agente de campo para atender um cliente com base na proximidade do agente com o cliente. Nesse cenário, o agente é selecionado dinamicamente.

Atribuir tarefas e etapas do Adobe Sign de [fluxos de trabalho centrados no Forms no OSGi](/help/forms/using/aem-forms-workflow.md) fornece opções para selecionar um usuário dinamicamente. Você pode usar pacotes ECMAScript ou OSGi para selecionar dinamicamente um destinatário para a etapa Atribuir tarefa ou para selecionar signatários para a etapa Assinar documento.

## Usar ECMAScript para selecionar dinamicamente um usuário ou grupo {#use-ecmascript-to-dynamically-select-a-user-or-group}

O ECMAScript é uma linguagem de script. Ele é usado para aplicativos de script e servidor do lado do cliente. Execute as seguintes etapas para selecionar dinamicamente um usuário ou um grupo usando o ECMAScript:

1. Abra o CRXDE Lite. A URL é `https://'[server]:[port]'/crx/de/index.jsp`
1. Crie um arquivo com extensão .ecma no seguinte caminho. Se o caminho (estrutura do nó) não existir, crie-o:

   * (Caminho para a etapa Atribuir Tarefa) `/apps/fd/dashboard/scripts/participantChooser`
   * (Caminho para etapa de Assinatura) `/apps/fd/workflow/scripts/adobesign`

1. Adicione o ECMAScript, que tem a lógica para selecionar dinamicamente um usuário, ao arquivo .ecma. Clique em **[!UICONTROL Salvar tudo]**.

   Para scripts de exemplo, consulte [Exemplos de ECMAScripts para selecionar dinamicamente um usuário ou grupo](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Adicione o nome de exibição do script. Esse nome é exibido nas etapas do workflow. Para especificar o nome:

   1. Expanda o nó do script, clique com o botão direito do mouse no nó **[!UICONTROL jcr:content]** e clique em **[!UICONTROL Mixins]**.
   1. Adicione a propriedade `mix:title` na caixa de diálogo Editar misturas e clique em **OK**.
   1. Adicione a seguinte propriedade ao nó jcr:content do script:

      | Nome | Tipo | Valor |
      |--- |--- |--- |
      | jcr:title | String | Especifique o nome do script. Por exemplo, escolha o agente de campo mais próximo. Esse nome é exibido nas etapas Atribuir tarefa e Assinar documento. |

   1. Clique em **Salvar tudo**. O script fica disponível para seleção nos componentes do workflow para AEM.

      ![script](assets/script.png)

### Exemplos de ECMAScripts para escolher dinamicamente um usuário ou grupo {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

O exemplo de ECMAScript a seguir seleciona dinamicamente um destinatário para a etapa Atribuir tarefa. Neste script, um usuário é selecionado com base no caminho da carga. Antes de usar esse script, verifique se todos os usuários mencionados no script existem no AEM. Se os usuários mencionados no script não existirem no AEM, o processo relacionado poderá falhar.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

O exemplo de ECMAScript a seguir seleciona dinamicamente um destinatário para a etapa Adobe Sign. Antes de usar o script abaixo, verifique se as informações do usuário (endereços de email e números de telefone) mencionadas no script estão corretas. Se as informações do usuário mencionadas no script estiverem incorretas, o processo relacionado poderá falhar.

>[!NOTE]
>
>Ao usar o ECMAScript para Adobe Sign, o script deve estar no repositório crx em /apps/fd/workflow/scripts/adobesign/ e deve ter uma função chamada getAdobeSignRecipients para retornar uma lista de usuários.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Usar interface Java para escolher dinamicamente um usuário ou grupo {#use-java-interface-to-dynamically-choose-a-user-or-group}

Você pode usar a interface Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para escolher dinamicamente um usuário ou grupo para as etapas Adobe Sign e Atribuir tarefa. Você pode criar um pacote OSGi que usou a interface Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e implantá-lo no servidor do AEM Forms. Ela disponibiliza a opção para seleção nos componentes Atribuir tarefa e Adobe Sign do workflow AEM.

Você precisa dos arquivos [jar do SDK do cliente do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) e [jar do granite](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) para compilar a amostra de código listada abaixo. Adicione esses arquivos jar como dependências externas ao projeto do pacote OSGi. Você pode usar qualquer Java IDE para criar um pacote OSGi. O procedimento a seguir fornece etapas para usar o Eclipse para criar um pacote OSGi:

1. Abra o Eclipse IDE. Navegue até **[!UICONTROL Arquivo]**> **[!UICONTROL Novo projeto]**.
1. Na tela Selecionar um assistente, selecione **[!UICONTROL Projeto Maven]** e clique em **[!UICONTROL Avançar]**.
1. No Novo projeto Maven, mantenha os padrões e clique em **[!UICONTROL Próximo]**. Selecione um arquétipo e clique em **[!UICONTROL Avançar]**. Por exemplo, maven-archetype-quickstart. Especifique a **[!UICONTROL ID do Grupo]**, a **[!UICONTROL ID do Artefato]**, a **[!UICONTROL versão]** e o **[!UICONTROL pacote]** para o projeto e clique em **[!UICONTROL Concluir]**. O projeto é criado.
1. Abra o arquivo pom.xml para edição e substitua todo o conteúdo do arquivo pelo seguinte:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Adicione o código-fonte que usa a interface Java [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para escolher dinamicamente um usuário ou grupo para a etapa de tarefa Atribuir. Para obter o código de exemplo, consulte [Amostra para escolher dinamicamente um usuário ou grupo usando a interface Java](#-sample-scripts-for).
1. Abra um prompt de comando e navegue até o diretório que contém o projeto de pacote OSGi. Use o seguinte comando para criar o pacote OSGi:

   `mvn clean install`

1. Faça upload do pacote para um servidor do AEM Forms. Você pode usar o Gerenciador de pacotes AEM para importar o pacote para o servidor do AEM Forms.

Depois que o pacote é importado, a opção para escolher a interface Java para selecionar dinamicamente um usuário ou grupo fica disponível no para as etapas Adobe Sign e Atribuir tarefa.

### Exemplo de código Java para escolher dinamicamente um usuário ou grupo {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

O código de amostra a seguir escolhe dinamicamente um destinatário para a etapa do Adobe Sign. Você usa o código em um pacote OSGi. Antes de usar o código listado abaixo, verifique se as informações do usuário (endereços de email e números de telefone) mencionadas no código estão corretas. Se as informações do usuário mencionadas no código estiverem incorretas, o processo relacionado poderá falhar.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```
