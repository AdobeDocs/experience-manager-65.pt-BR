---
title: Introdução ao Java&trade; API QuickStart
description: Saiba como as operações do AEM Forms podem ser executadas usando a API altamente tipada do AEM Forms Java&trade; habilitada com conexão SOAP.
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 1d4062ef-fb24-4527-b899-896ce757beda
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Introdução ao Java™ API Quick Start {#introducing-java-api-quickstart}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O Adobe AEM Forms API Quick Start pode ajudá-lo a acelerar seus esforços para desenvolver programas que interajam com os serviços da AEM Forms. *Início rápido* s são programas completos que você pode copiar e colar em seus próprios projetos e usar como ponto de partida. Você pode executar um Início rápido para ver como ele se comporta e modificá-lo para atender às suas necessidades.

As operações do AEM Forms podem ser executadas usando a API altamente tipada do AEM Forms e o modo de conexão deve ser definido como SOAP.

O Quick Start da API do Java™ altamente digitado fornece uma lista de arquivos JAR necessários para executar a aplicação Java™. A maioria das inicializações rápidas do Java™ é de aplicativos de console executados no `main`. No entanto, o Quick Start da API do Forms Java™ altamente digitado é implementado como um servlet Java™ que é executado em uma aplicação Web.

A listagem de arquivos JAR está em uma seção de comentários no início do Início rápido. Por exemplo, o comentário a seguir está em um Início rápido de saída e é uma lista de arquivos JAR típica encontrada em cada Início rápido do Java™.

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

Início mais rápido em *Programação com o AEM Forms no JEE* chame um serviço específico para executar uma operação. No entanto, alguns Inícios rápidos invocam vários serviços da AEM Forms para executar um determinado fluxo de trabalho. A lista a seguir fornece inicializações rápidas do Java™ que chamam mais de um serviço AEM Forms:

[Início rápido (modo SOAP): Passar um documento no Repositório do AEM Forms para o serviço de saída usando a API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (chama o serviço de Repositório e Saída)

[Início rápido (modo SOAP): criação de um documento PDF com base em fragmentos usando a API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (invoca o serviço Assembler e Output)

[Início rápido (modo SOAP): Criação de documentos PDF com dados XML enviados usando a API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (invoca o serviço Forms, Output, e Document Management )

[Início rápido (modo SOAP): passar documentos para o serviço Forms usando a API Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (invoca o serviço Forms e Gerenciamento de documentos)

[Início rápido (modo SOAP): assinatura digital de um formulário baseado em XFA usando a API Java™](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (invoca o serviço Forms e Signature)

[Início rápido (modo SOAP): gerenciamento de funções e permissões usando a API Java™](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (invoca o DiretoryManager e o serviço AuthorizationManager )

[Início rápido (modo SOAP): passar documentos para o serviço de saída usando a API Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (chame o serviço Output and Document Management)

>[!NOTE]
>
>Os Quick Starts na programação com o AEM Forms são baseados no AEM Forms sendo implantado no JBoss® Application Server e no sistema operacional Microsoft® Windows®. No entanto, se você estiver usando outro sistema operacional, como o UNIX®, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se estiver usando outro servidor de aplicações J2EE, certifique-se de especificar propriedades de conexão válidas. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
A maioria dos serviços Web de início rápido é escrita em C# e usa o .NET framework. No entanto, é possível criar uma lógica de aplicativo cliente que possa chamar serviços da AEM Forms em qualquer ambiente de desenvolvimento compatível com os padrões SOAP. (Consulte [Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
