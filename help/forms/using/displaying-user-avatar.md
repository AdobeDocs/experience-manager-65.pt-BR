---
title: Exibir o avatar do usuário
seo-title: Exibir o avatar do usuário
description: Como personalizar a área de trabalho AEM Forms para exibir a imagem de um usuário conectado.
seo-description: Como personalizar a área de trabalho AEM Forms para exibir a imagem de um usuário conectado.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Exibir o avatar do usuário {#displaying-the-user-avatar}

O avatar do usuário conectado é exibido no canto superior direito da área de trabalho do AEM Forms. Além disso, os avatares dos relatórios diretos na hierarquia organizacional são exibidos na Visualização do Gerente. Você pode configurar o espaço de trabalho do AEM Forms para selecionar as imagens de usuário do banco de dados, por exemplo, o servidor LDAP.

>[!NOTE]
>
>A proporção de aspecto suportada das imagens do usuário é 1:1.

1. Crie um DSC, usando os detalhes mencionados na próxima etapa. Para obter mais informações, consulte o tópico Desenvolvimento de componentes para o AEM Forms no Guia de AEM Forms [de programação](https://www.adobe.com/go/learn_aemforms_programming_63) .
1. No DSC, defina um novo SPI que exponha os métodos getCurrentUserImageUrl e getUserImageUrl para obter um URL de imagem para um usuário AEM Forms. A seguir está um exemplo de trecho de código Java™:

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Crie um arquivo component.xml. Certifique-se de que spec-id esteja conforme mostrado no trecho de código abaixo.

   O trecho de código a seguir é uma amostra. Personalize-o de acordo com seus requisitos específicos.

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Implante o DSC por meio do Workbench. Reinicie o `ProcessManagementClientSessionService` serviço.
1. Talvez seja necessário atualizar seu navegador ou fazer logout/login com o usuário novamente.
