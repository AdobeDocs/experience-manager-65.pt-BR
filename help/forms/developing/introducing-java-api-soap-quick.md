---
title: Introdução ao Java API QuickStart
seo-title: Introdução ao Java API QuickStart
description: Introdução ao Java API QuickStart
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Introdução ao Java API Quick Start {#introducing-java-api-quickstart}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O Adobe AEM Forms API Quick Start pode ajudá-lo a acelerar seus esforços para desenvolver programas que interagem com os serviços da AEM Forms. *Os* Inícios rápidos são programas completos que você pode copiar e colar em seus próprios projetos e usar como ponto de partida. Você pode executar um Início rápido para ver como ele se comporta e modificá-lo de acordo com suas necessidades.

As operações do AEM Forms podem ser executadas usando a API altamente digitada do AEM Forms e o modo de conexão deve ser definido como SOAP.

O Java fortemente digitado API Quick Start fornece uma lista de arquivos JAR necessários para executar o aplicativo Java. A maioria dos Java Quick Starts são aplicativos de console que são executados em `main`. No entanto, o Início rápido da API do Forms Java de tipo forte é implementado como servlet Java executado em um aplicativo da Web.

A listagem do arquivo JAR está localizada em uma seção de comentário localizada no início do Início rápido. Por exemplo, o comentário a seguir está localizado em um Início rápido de saída e é uma típica listagem de arquivos JAR encontrada em cada Início rápido de Java.

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

## Início rápido de vários serviços {#multiple-services-quick-start}

A maioria dos Inícios rápidos localizados em *Programação com AEM Forms no JEE* chama um serviço específico para executar uma operação. No entanto, alguns Quick Starts chamam vários serviços da AEM Forms para executar um determinado workflow. A lista a seguir fornece ícones rápidos do Java que chamam mais de um serviço AEM Forms:

[Início rápido (modo SOAP): Passar um documento localizado no Repositório AEM Forms para o serviço de saída usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)  Java (chama o serviço Repositório e Saída)

[Início rápido (modo SOAP): Criar um documento PDF com base em fragmentos usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)  Java (chama o serviço Assembler e Output)

[Início rápido (modo SOAP): Criar documentos PDF com dados XML enviados usando a API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)  Java (chama o serviço Forms, Output e Document Management)

[Início rápido (modo SOAP): Passar documentos para o serviço da Forms usando a API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)  Java (chama o serviço Forms e Gerenciamento de documentos)

[Início rápido (modo SOAP): Assinar digitalmente um formulário baseado em XFA usando a API](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)  Java (chama o serviço de assinatura e Forms)

[Início rápido (modo SOAP): Gerenciamento de funções e permissões usando a API](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)  Java (chama o DiretoryManager e o serviço AuthorizationManager )

[Início rápido (modo SOAP): Passar documentos para o serviço de saída usando a API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)  Java (chame o serviço de saída e gerenciamento de documentos)

>[!NOTE]
>
>O Início rápido, localizado em Programação com AEM Forms, é baseado no AEM Forms que está sendo implantado no JBoss® Application Server e no sistema operacional Microsoft® Windows®. No entanto, se estiver usando outro sistema operacional, como o UNIX®, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>A maioria dos Quick Starts de serviço da Web é gravada em C# e usa o .NET Framework. No entanto, é possível criar uma lógica de aplicativo cliente que possa invocar os serviços da AEM Forms em qualquer ambiente de desenvolvimento compatível com os padrões SOAP. (Consulte [Invocando o AEM Forms Usando Serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

