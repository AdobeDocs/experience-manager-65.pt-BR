---
title: Introdução ao Java API QuickStart
seo-title: Introdução ao Java API QuickStart
description: 'null'
seo-description: 'null'
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Introdução ao Start rápido da API Java {#introducing-java-api-quickstart}

Start rápido de API da Adobe AEM Forms pode ajudá-lo a acelerar seus esforços para desenvolver programas que interagem com os serviços da AEM Forms. *Os* Start rápidos são programas completos que você pode copiar e colar em seus próprios projetos e usar como ponto de partida. Você pode executar um Start rápido para ver como ele se comporta e modificá-lo de acordo com suas próprias necessidades.

As operações do AEM Forms podem ser executadas usando a API fortemente tipada do AEM Forms e o modo de conexão deve ser definido como SOAP.

O Start rápido da API de tipo Java fornece uma lista de arquivos JAR necessários para executar o aplicativo Java. A maioria dos Start rápidos do Java são aplicativos de console executados no `main`. No entanto, o Start Quick da API do Forms Java fortemente tipado é implementado como servlet Java executado em um aplicativo da Web.

A listagem de arquivos JAR está localizada em uma seção de comentários localizada no início do Start rápido. Por exemplo, o comentário a seguir está localizado em um start rápido de Saída e é uma lista de arquivos JAR típica encontrada em cada Start rápido de Java.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Start rápido de vários serviços {#multiple-services-quick-start}

A maioria dos Start rápidos localizados em *Programando com a AEM Forms no JEE* chama um serviço específico para executar uma operação. Entretanto, alguns Start rápidos chamam vários serviços da AEM Forms para executar um determinado fluxo de trabalho. A lista a seguir fornece start rápidos do Java que chamam mais de um serviço AEM Forms:

[Start rápido (modo SOAP): Transmissão de um documento localizado no Repositório AEM Forms para o serviço de Saída usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) Java (chama o serviço Repositório e Saída)

[Start rápido (modo SOAP): Criação de um documento PDF com base em fragmentos usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) Java (chama o Assembler e o serviço de Saída)

[Start rápido (modo SOAP): Criação de Documentos PDF com dados XML enviados usando a API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) Java (chama o serviço Forms, Output e Documento Management)

[Start rápido (modo SOAP): Transmissão de documentos para o serviço Forms usando a API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) Java (chama o serviço Forms e Gerenciamento de Documentos)

[Start rápido (modo SOAP): Assinando digitalmente um formulário baseado em XFA usando a API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) Java (chama o serviço de assinatura e Forms)

[Start rápido (modo SOAP): Gerenciando funções e permissões usando a API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) Java (chama o DiretoryManager e o serviço AuthorizationManager )

[Start rápido (modo SOAP): Transmissão de documentos para o Serviço de Saída usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) Java (chame o serviço de Gerenciamento de Saída e Documentos)

>[!NOTE]
>
>Os Start rápidos localizados em Programação com a AEM Forms são baseados na AEM Forms que está sendo implantada no JBoss® Application Server e no sistema operacional Microsoft® Windows®. Entretanto, se você estiver usando outro sistema operacional, como o UNIX®, substitua os caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se você estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)

>[!NOTE]
>
>A maioria dos Start Rápidos do serviço da Web são escritos em C# e usam a estrutura .NET. No entanto, você pode criar uma lógica de aplicativo cliente capaz de invocar os serviços da AEM Forms em qualquer ambiente de desenvolvimento compatível com os padrões SOAP. (Consulte [Invocando o AEM Forms usando os serviços](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)da Web.)

