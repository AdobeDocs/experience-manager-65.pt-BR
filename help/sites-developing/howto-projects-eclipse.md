---
title: Como desenvolver projetos do AEM usando o Eclipse
seo-title: Como desenvolver projetos do AEM usando o Eclipse
description: Este guia descreve como usar o Eclipse para desenvolver projetos baseados no AEM
seo-description: Este guia descreve como usar o Eclipse para desenvolver projetos baseados no AEM
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# Como desenvolver projetos do AEM usando o Eclipse{#how-to-develop-aem-projects-using-eclipse}

Este guia descreve como usar o Eclipse para desenvolver projetos baseados no AEM.

>[!NOTE]
>
>A Adobe agora fornece as Ferramentas de desenvolvimento de [AEM para o Eclipse](/help/sites-developing/aem-eclipse.md) , que ajudam a desenvolver soluções de AEM com o Eclipse.

## Visão geral {#overview}

Para começar a desenvolver o AEM no Eclipse, as etapas a seguir são necessárias.

Cada um deles é explicado mais detalhadamente no restante deste Como.

* Instalar o Eclipse 4.3 (Kepler)
* Configure seu projeto do AEM com base no Maven
* Preparar suporte JSP para Eclipse no Maven POM
* Importar o projeto Maven para o Eclipse

>[!NOTE]
>
>Este guia é baseado no Eclipse 4.3 (Kepler) e no AEM 5.6.1.

## Instalar o Eclipse {#install-eclipse}

Baixe o &quot;Eclipse IDE for Java EE Developers&quot; na página [Downloads do](https://www.eclipse.org/downloads/)Eclipse.

Instale o Eclipse seguindo as instruções de [instalação](https://wiki.eclipse.org/Eclipse/Installation).

## Configure seu projeto do AEM com base no Maven {#set-up-your-aem-project-based-on-maven}

Em seguida, configure seu projeto usando o Maven, conforme descrito em [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparar suporte JSP para o Eclipse {#prepare-jsp-support-for-eclipse}

O Eclipse também pode fornecer suporte ao trabalho com o JSP, por exemplo,

* conclusão automática de bibliotecas de tags
* Consentização do Eclipse de objetos definidos por &lt;cq:defineObjects /> e &lt;sling:defineObjects />

Para que isso funcione:

1. Siga as instruções em [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) em [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Adicione o seguinte à seção &lt;build /> no POM do módulo de conteúdo.

   O plug-in de suporte Maven do Eclipse, m2e, não fornece suporte para o plug-in maven-jspc-e, e essa configuração instrui o m2e a ignorar o plug-in e a tarefa relacionada de limpeza dos resultados da compilação temporária.

   Isso não é um problema: como observado em [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), o plug-in maven-jspc nesta configuração é usado apenas para validar a compilação de JSPs como parte do processo de compilação. O Eclipse já informa quaisquer problemas em JSPs e não depende deste plug-in Maven para poder fazer isso.

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### Importar o projeto Maven para o Eclipse {#import-the-maven-project-into-eclipse}

1. No Eclipse, escolha Arquivo > Importar...
1. Na caixa de diálogo Importar, escolha Maven > Projetos Maven existentes e clique em &quot;Avançar&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Digite o caminho para a pasta de nível superior do projeto e clique em &quot;Selecionar tudo&quot; e &quot;Concluir&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Agora, todos os usuários estão prontos para usar o Eclipse para desenvolver seu projeto AEM, incluindo a conclusão automática do JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se você incluir `/libs/foundation/global.jsp` ou outros JSPs em `/libs`, será necessário copiá-los para o projeto para que o Eclipse possa resolver a inclusão. Ao mesmo tempo, é necessário certificar-se de que ele não esteja incluído em seu pacote de conteúdo pela Maven. Como fazer isso é descrito em [Como criar projetos do AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

