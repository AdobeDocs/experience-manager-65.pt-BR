---
title: Componentes e serviços Java&trade; APIQuick Start (SOAP)
description: Saiba como manipular programaticamente componentes e serviços do AEM Forms usando o Java&trade; API Quick Start (SOAP).
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
role: Developer
exl-id: fe1198b5-4145-4dcd-ab8a-4015daaf89b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Componentes e serviços Início rápido da API Java™ (SOAP) {#components-and-services-java-apiquick-start-soap}

O Java™ API Quick Start (SOAP) está disponível para componentes e serviços.


[Início rápido (modo SOAP): implantação de um componente usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-deploying-a-component-using-the-java-api)

[Início rápido (modo SOAP): definição do contexto de execução de um serviço usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api)

[Início rápido (modo SOAP): desativação da segurança do serviço usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-disabling-service-security-using-the-java-api)

[Início rápido (modo SOAP): iniciar um serviço usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-starting-a-service-using-the-java-api)

[Início rápido (modo SOAP): Modificando valores de configuração de serviço usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api)

[Início rápido (modo SOAP): remoção de componentes usando o Java](components-services-java-api-quick.md#quick-start-soap-mode-removing-components-using-the-java-api)


As operações do AEM Forms podem ser executadas usando a API altamente tipada do AEM Forms e o modo de conexão deve ser definido como SOAP.

>[!NOTE]
>
>Não é possível manipular componentes e serviços de forma programática usando serviços da Web.

>[!NOTE]
>
>O início rápido na programação com formulários AEM é baseado no Forms Server que está sendo implantado no JBoss® e no sistema operacional Windows. No entanto, se você estiver usando outro sistema operacional, como o UNIX®, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se estiver usando outro servidor de aplicações J2EE, certifique-se de especificar propriedades de conexão válidas. Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>Se você tiver um componente personalizado e estiver usando protocolos SOAP ou EJB para chamar DSCs no mesmo servidor local, e essas chamadas pararem de funcionar após uma atualização, use a estratégia de chamada na VM. Use o método de invocação DSC na VM com ServiceClientFactory padrão e não construa ServiceClientFactory usando protocolos SOAP ou EJB.

## Início rápido (modo SOAP): implantação de um componente usando a API Java™ {#quick-start-soap-mode-deploying-a-component-using-the-java-api}

O exemplo do Java™ a seguir implanta um componente baseado em um arquivo JAR chamado *adobe-emailSample-dsc.jar*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode)
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
     */ 
 import java.io.FileInputStream; 
 import java.util.*; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class DeployComponents { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Reference a JAR file that represents the component to deploy 
         //    FileInputStream componentFile = new FileInputStream("C:\\Adobe\adobe-emailSample-dsc.jar");  
              
             FileInputStream componentFile = new FileInputStream("C:\\A22\Bank.jar");  
             Document component = new Document(componentFile);  
              
             //Install the component 
             Component myComponent = componentReg.install(component); 
             componentReg.start(myComponent); 
              
             System.out.println("The component has been deployed");  
             } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## Início rápido (modo SOAP): definição do contexto de execução de um serviço usando a API Java™ {#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api}

O exemplo de código Java™ a seguir define o contexto de execução Executar como Invoker para um serviço de exemplo chamado *EncryptDocument*.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar  
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
        * The JBoss files must be kept in the jboss\bin\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start sets the Run-As Invoker to a service named EncryptDocument 
     */ 
 public class SetRunAsConfiguration { 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument service 
         ServiceConfiguration _config  = _src.getHeadActiveConfiguration("EncryptDocument"); 
          
         //Set the RUN_AS_INVOKER execution context 
         ModifyServiceConfigurationInfo _configModifyInfo = new ModifyServiceConfigurationInfo(); 
         _configModifyInfo.setServiceId(_config.getServiceId()); 
         _configModifyInfo.setMajorVersion(_config.getMajorVersion()); 
         _configModifyInfo.setMinorVersion(_config.getMinorVersion()); 
         _configModifyInfo.setRunAsConfiguration(ServiceConfiguration.RUN_AS_INVOKER); 
         _config = _src.modifyConfiguration(_configModifyInfo); 
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Início rápido (modo SOAP): desativação da segurança do serviço usando a API Java™ {#quick-start-soap-mode-disabling-service-security-using-the-java-api}

O exemplo de código Java™ a seguir desativa a segurança do serviço EncryptDocument de exemplo e dos serviços que são chamados dentro desse serviço (os serviços Set Value e Encryption ).

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start disables security from the EncryptDocument process 
     * and each service that is in this process 
     */ 
 public class DisableSecurity{ 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                      
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument process and each service that is  
         //invoked from within the EncryptDocument process 
         ServiceConfiguration encryptDocumentService  = _src.getHeadActiveConfiguration("EncryptDocument"); 
         ServiceConfiguration setValueService  = _src.getHeadActiveConfiguration("SetValue"); 
         ServiceConfiguration encryptionService  = _src.getHeadActiveConfiguration("EncryptionService"); 
          
         //Create a ModifyServiceInfo object 
         ModifyServiceInfo si = new ModifyServiceInfo(); 
          
         //Disable security from the EncryptDocument service 
         si.setId(encryptDocumentService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the SetValue service 
         si.setId(setValueService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the EncryptionService 
         si.setId(encryptionService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
              
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Início rápido (modo SOAP): iniciar um serviço usando a API Java™ {#quick-start-soap-mode-starting-a-service-using-the-java-api}

O exemplo de código Java™ a seguir inicia um serviço chamado *SendEmailService*.

```java
 package com.adobe.sample.servicemanager; 
  
 /** 
     * This Java Quick Start uses the following JAR files: 
     * 1. adobe-livecycle-client.jar 
     * 2. adobe-usermanager-client.jar 
     * 3. adobe-workflow-client-sdk.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed on Jboss) 
     * 6. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     * 7. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 public class StartService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms      
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadActiveConfiguration("SendEmailService"); 
          
             //Start the SendEmailService 
             serviceReg.start(myServiceConfig); 
             } 
              
                 catch(Exception e) 
                 { 
                     e.printStackTrace(); 
                 } 
     } 
 } 
  
 
```

## Início rápido (modo SOAP): modificação de valores de configuração de serviços usando a API Java™ {#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api}

O exemplo do Java™ a seguir modifica os valores de configuração que pertencem ao Serviço SendEmail.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
        * 2. adobe-livecycle-client.jar 
        * 3. adobe-usermanager-client.jar 
        * 4. activation.jar (required for SOAP mode) 
        * 5. axis.jar (required for SOAP mode) 
        * 6. commons-codec-1.3.jar (required for SOAP mode) 
        * 7. commons-collections-3.2.jar  (required for SOAP mode) 
        * 8. commons-discovery.jar (required for SOAP mode) 
        * 9. commons-logging.jar (required for SOAP mode) 
        * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
        * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
        * 12. jaxrpc.jar (required for SOAP mode) 
        * 13. log4j.jar (required for SOAP mode) 
        * 14. mail.jar (required for SOAP mode) 
        * 15. saaj.jar (required for SOAP mode) 
        * 16. wsdl4j.jar (required for SOAP mode) 
        * 17. xalan.jar (required for SOAP mode) 
        * 18. xbean.jar (required for SOAP mode) 
        * 19. xercesImpl.jar (required for SOAP mode) 
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
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ConfigParameter; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
  
 public class ModifyService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms     
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadServiceConfiguration("SendEmailService"); 
                              
             //Create a ModifyServiceConfigurationInfo object 
                 ModifyServiceConfigurationInfo modService = new ModifyServiceConfigurationInfo(); 
                      
             //Set configuration values required by the SendEmailService 
             String serviceId = myServiceConfig.getServiceId(); 
             modService.setServiceId(serviceId); 
             modService.setMajorVersion(1); 
             modService.setConfigParameterAsText("smtpHost","mySMTPSERVER"); 
             modService.setConfigParameterAsText("smtpUser","smyUserName");     
             modService.setConfigParameterAsText("smtpPassword","myPassword");     
                      
             //Modify the service's configuration values 
             serviceReg.modifyConfiguration(modService); 
                          
             //Conform the new configuration values 
             ServiceConfiguration serviceConfig = serviceReg.getServiceConfiguration("SendEmailService",1,0); 
             ConfigParameter cp = serviceConfig.getConfigParameter("smtpUser"); 
             String configValue = cp.getTextValue();  
             System.out.println(configValue); 
             } 
      
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```

## Início rápido (modo SOAP): remoção de componentes usando a API Java™ {#quick-start-soap-mode-removing-components-using-the-java-api}

O seguinte exemplo de código Java™ remove um componente usando a API Java™.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-taskmanager-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed 
     * on JBoss) 
     * 6. commons-code-1.3.jar 
     * 7. adobe-workflow-client-sdk.jar 
     * 8. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
     * 9. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss) 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class RemoveComponent { 
  
     public static void main(String[] args) { 
          
         try{ 
               //Set connection properties required to invoke AEM Forms                                                                                                                        
               Properties connectionProps = new Properties(); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Retrieve the Id of the component to remove from the service container 
             Component myComponent = componentReg.getComponent("com.adobe.livecycle.sample.email.emailSampleComponent", "1.0"); 
              
             //Determine if the component is in a running state 
             if (myComponent.getState()== Component.RUNNING) 
             { 
                 //Stop the component 
                 Component stoppedComponent = componentReg.stop(myComponent); 
                  
                 //Uninstall the component 
                 componentReg.uninstall(stoppedComponent); 
             } 
             else 
                 componentReg.uninstall(myComponent); 
                  
             System.out.println("The component was removed."); 
             } 
              
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```
