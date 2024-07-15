---
title: Conversão de Postscript em documentos PDF
description: Use o serviço Distiller para converter arquivos PostScript®, Encapsulated PostScript (EPS) e PRN para arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller converte grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# Conversão de Postscript em documentos PDF {#converting-postscript-to-pdf-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

## Sobre o serviço Distiller {#about-the-distiller-service}

O serviço Distiller® converte arquivos PostScript®, Encapsulated PostScript (EPS) e PRN para arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller é frequentemente usado para converter grandes volumes de documentos impressos em documentos eletrônicos, como faturas e demonstrativos. A conversão de documentos em PDF também permite que as empresas enviem aos seus clientes uma versão em papel e uma versão eletrônica de um documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de PostScript em documentos PDF {#converting-postscript-to-pdf-documents-inner}

Este tópico descreve como você pode usar a API de serviço do Distiller (Java e serviço da Web) para converter programaticamente arquivos PostScript (PS), Encapsulated PostScript (EPS) e PRN em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para converter arquivos PostScript em documentos PDF, um dos seguintes itens precisa ser instalado no servidor que hospeda o AEM Forms: Acrobat 9 ou Microsoft Visual C++ 2005 pacote redistribuível.

### Resumo das etapas {#summary-of-steps}

Para converter qualquer um dos tipos suportados em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Distiller.
1. Recupere o arquivo a ser convertido.
1. Chame a operação de criação de PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente de serviço Distiller**

Antes de executar programaticamente uma operação de serviço Distiller, você deve criar um cliente de serviço Distiller. Se você estiver usando a API Java, crie um objeto `DistillerServiceClient`. Se você estiver usando a API de serviço Web, crie um objeto `DistillerServiceService`.

**Recuperar o arquivo para converter**

Recupere o arquivo que deseja converter. Por exemplo, para converter um arquivo PS em um documento PDF, você deve recuperar o arquivo PS.

**Invocar a operação de criação de PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de criação de PDF. Esta operação precisará de informações sobre o documento a ser convertido, incluindo o caminho para o documento de destino.

**Salvar o documento do PDF**

Você pode salvar o documento PDF como um arquivo PDF.

**Consulte também**

[Converter um arquivo PostScript em PDF usando a API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversão de um arquivo PostScript em PDF usando a API do serviço Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Converter um arquivo PostScript em PDF usando a API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converta um arquivo PostScript em um documento PDF usando a API de serviço do Distiller (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-destiller-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente de serviço Distiller.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DistillerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o arquivo a ser convertido.

   * Crie um objeto `java.io.FileInputStream` que represente o arquivo a ser convertido usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Chame a operação de criação de PDF.

   Chame o método `createPDF` do objeto `DistillerServiceClient` e passe os seguintes valores:

   * O objeto `com.adobe.idp.Document` que representa o arquivo PS, EPS ou PRN a ser convertido
   * Um objeto `java.lang.String` que contém o nome do arquivo a ser convertido
   * Um objeto `java.lang.String` que contém o nome das configurações do Adobe PDF a serem usadas
   * Um objeto `java.lang.String` que contém o nome das configurações de segurança a serem usadas
   * Um objeto `com.adobe.idp.Document` opcional que contém configurações a serem aplicadas durante a geração do documento PDF
   * Um objeto `com.adobe.idp.Document` opcional que contém informações de metadados a serem aplicadas ao documento PDF

   O método `createPDF` retorna um objeto `CreatePDFResult` que contém o novo documento PDF e um arquivo de log que pode ser gerado. O arquivo de log geralmente contém mensagens de erro ou aviso que são geradas pela solicitação de conversão.

1. Salve o documento PDF.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Invoque o método `getCreatedDocument` do objeto `CreatePDFResult`. Isso retorna um objeto `com.adobe.idp.Document`.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento PDF.

   Da mesma forma, para obter o documento de log, execute as ações a seguir.

   * Invoque o método `getLogDocument` do objeto `CreatePDFResult`. Isso retorna um objeto `com.adobe.idp.Document`.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento de log.

**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): conversão de um arquivo PostScript em um documento PDF usando a API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversão de um arquivo PostScript em PDF usando a API do serviço Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converta um arquivo PostScript em um documento PDF usando a API de serviço do Distiller (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente de serviço Distiller.

   * Crie um objeto `DistillerServiceClient` usando seu construtor padrão.
   * Crie um objeto `DistillerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DistillerServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo a ser convertido.

   * Crie um objeto `BLOB` usando seu construtor. Este objeto `BLOB` é usado para armazenar o arquivo a ser convertido em um documento PDF.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Chame a operação de criação de PDF.

   Chame o método `CreatePDF2` do objeto `DistillerServiceService` e passe os seguintes valores obrigatórios:

   * O objeto `BLOB` que representa o arquivo PS a ser convertido
   * Uma string que contém o nome do caminho do arquivo a ser convertido
   * Um objeto de cadeia de caracteres que contém as configurações de Adobe PDF a serem usadas (por exemplo, `Standard`)
   * Um objeto de cadeia de caracteres que contém as configurações de segurança a serem usadas (por exemplo, `No Securit`a)
   * Um objeto `BLOB` opcional que contém configurações a serem aplicadas durante a geração do documento PDF
   * Um objeto `BLOB` opcional que contém informações de metadados a serem aplicadas ao documento PDF
   * Um parâmetro de saída `BLOB` usado para armazenar o documento PDF
   * Um parâmetro de saída `BLOB` usado para armazenar o log

1. Salve o documento PDF.

   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `CreatePDF2` (o parâmetro de saída). Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
