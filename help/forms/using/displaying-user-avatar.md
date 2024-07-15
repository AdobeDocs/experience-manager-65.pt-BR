---
title: Exibir o avatar do usuário
description: Como personalizar o espaço de trabalho do AEM Forms para exibir a imagem de um usuário conectado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Exibir o avatar do usuário {#displaying-the-user-avatar}

O avatar do usuário conectado é exibido no canto superior direito do espaço de trabalho do AEM Forms. Além disso, os avatares dos subordinados diretos na hierarquia organizacional são exibidos na Exibição do gerente. Você pode configurar o espaço de trabalho do AEM Forms para escolher as imagens de usuário do banco de dados, digamos, servidor LDAP.

>[!NOTE]
>
>A proporção suportada das imagens do usuário é de 1:1.

1. Crie um DSC, usando os detalhes mencionados na próxima etapa. Para obter mais informações, consulte o tópico &quot;Desenvolvendo componentes para o AEM Forms&quot; no guia [Programação com o AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
1. No DSC, defina um novo SPI que exponha os métodos getCurrentUserImageUrl e getUserImageUrl para obter um URL de imagem para um usuário do AEM Forms. Este é um exemplo de trecho de código Java™:

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

1. Crie um arquivo component.xml. Certifique-se de que a spec-id esteja conforme mostrado no trecho de código abaixo.

   O fragmento de código a seguir é uma amostra do. Personalize-o para atender às suas necessidades específicas.

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

1. Implante o DSC por meio do Workbench. Reinicie o serviço `ProcessManagementClientSessionService`.
1. Talvez seja necessário atualizar o navegador ou fazer logout/logon com o usuário novamente.
