---
title: Como desenvolver projetos de AEM usando o Eclipse
seo-title: How to Develop AEM Projects Using Eclipse
description: Este guia descreve como usar o Eclipse para desenvolver projetos baseados em AEM
seo-description: This guide describes how to use Eclipse for developing AEM based projects
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
exl-id: 9d421599-0417-4329-a528-9cda4e3716f5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Como desenvolver projetos de AEM usando o Eclipse{#how-to-develop-aem-projects-using-eclipse}

Este guia descreve como usar o Eclipse para desenvolver projetos baseados em AEM.

>[!NOTE]
>
>O Adobe agora fornece o [Ferramentas de desenvolvimento do AEM para Eclipse](/help/sites-developing/aem-eclipse.md) que ajuda a desenvolver soluções para AEM com o Eclipse.

## Visão geral {#overview}

Para começar a usar o desenvolvimento do AEM no Eclipse, as seguintes etapas são necessárias.

Cada uma delas é explicada com mais detalhes no restante desta instrução.

* Instalar o Eclipse 4.3 (Kepler)
* Configurar o projeto do AEM com base no Maven
* Preparar o suporte a JSP para o Eclipse no POM Maven
* Importar o projeto Maven para o Eclipse

>[!NOTE]
>
>Este guia é baseado no Eclipse 4.3 (Kepler) e AEM 5.6.1.

## Instalar o Eclipse {#install-eclipse}

Baixe o &quot;Eclipse IDE para desenvolvedores Java EE&quot; no [Página de downloads do Eclipse](https://www.eclipse.org/downloads/).

Instale o Eclipse seguindo o [Instruções de instalação](https://wiki.eclipse.org/Eclipse/Installation).

## Configurar o projeto do AEM com base no Maven {#set-up-your-aem-project-based-on-maven}

Em seguida, configure seu projeto usando o Maven, conforme descrito em [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).

## Preparar suporte a JSP para o Eclipse {#prepare-jsp-support-for-eclipse}

O Eclipse também pode fornecer suporte para trabalhar com JSP, por exemplo,

* preenchimento automático de bibliotecas de tags
* Reconhecimento do Eclipse de objetos definidos por &lt;cq:defineobjects /> e &lt;sling:defineobjects />

Para que isso funcione:

1. Siga as instruções em [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) in [Como criar projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).
1. Adicione o seguinte à &lt;build /> no POM do módulo de conteúdo.

   O plug-in de suporte Maven do Eclipse, m2e, não fornece suporte para maven-jspc-plugin, e essa configuração informa à m2e para ignorar o plug-in e a tarefa relacionada de limpar os resultados temporários da compilação.

   Isso não é um problema: como observado no [Como trabalhar com JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps), o maven-jspc-plugin nessa configuração é usado apenas para validar a compilação de JSPs como parte do processo de build. O Eclipse já relata problemas em JSPs e não depende desse plug-in Maven para fazer isso.

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
1. Na caixa de diálogo Importar, escolha Maven > Projetos Maven existentes e clique em &quot;Próximo&quot;.

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. Insira o caminho para a pasta de nível superior do projeto, depois clique em &quot;Selecionar tudo&quot; e &quot;Concluir&quot;.

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. Agora tudo está pronto para usar o Eclipse para desenvolver seu projeto AEM, incluindo autopreenchimento JSP.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Se você incluir `/libs/foundation/global.jsp` ou outros JSPs no `/libs`, você deve copiá-lo para o seu projeto para que o Eclipse possa resolver a inclusão. Ao mesmo tempo, você precisa garantir que ele não seja incluído no seu pacote de conteúdo pelo Maven. Como fazer isso é descrito em [Como construir projetos AEM usando o Apache Maven](/help/sites-developing/ht-projects-maven.md).
