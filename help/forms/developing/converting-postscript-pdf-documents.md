---
title: Conversão de Postscript em documentos PDF
seo-title: Converting Postscript to PDF Documents
description: Use o serviço Distiller para converter arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller converte grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações usando a API do Java e a API do serviço da Web.
seo-description: Use the Distiller service to convert PostScript®, Encapsulated PostScript (EPS), and PRN files to compact, reliable, and more secure PDF files over a network. The Distiller service converts large volumes of print documents to electronic documents, such as invoices and statements using the Java API and Web Service API.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 0%

---

# Conversão de Postscript em documentos PDF {#converting-postscript-to-pdf-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço Distiller {#about-the-distiller-service}

O serviço Distiller® converte arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller é frequentemente usado para converter grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações. A conversão de documentos para o PDF também permite que as empresas enviem aos seus clientes uma versão em papel e uma versão eletrônica de um documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Converter PostScript em documentos PDF {#converting-postscript-to-pdf-documents-inner}

Este tópico descreve como você pode usar a API de serviço do Distiller (Java e serviço da Web) para converter programaticamente arquivos PostScript (PS), Encapsulated PostScript (EPS) e PRN em documentos do PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para converter arquivos PostScript em documentos PDF, um dos seguintes itens precisa ser instalado no servidor que hospeda o AEM Forms: Pacote redistribuível Acrobat 9 ou Microsoft Visual C++ 2005.

### Resumo das etapas {#summary-of-steps}

Para converter qualquer um dos tipos suportados em um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço Distiller.
1. Recupere o arquivo para converter.
1. Chame a operação de criação de PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente de serviço Distiller**

Antes de executar programaticamente uma operação de serviço do Distiller, você deve criar um cliente de serviço do Distiller. Se estiver usando a API do Java, crie um `DistillerServiceClient` objeto. Se estiver usando a API do serviço da Web, crie um `DistillerServiceService` objeto.

**Recuperar o arquivo para converter**

Você deve recuperar o arquivo que deseja converter. Por exemplo, para converter um arquivo PS em um documento PDF, você deve recuperar o arquivo PS.

**Chame a operação de criação de PDF**

Depois de criar o cliente de serviço, você pode invocar a operação de criação de PDF. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o caminho para o documento de destino.

**Salve o documento do PDF**

Você pode salvar o documento PDF como um arquivo PDF.

**Consulte também**

[Converter um arquivo PostScript para o PDF usando a API do Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversão de um arquivo PostScript para o PDF usando a API do serviço da Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Converter um arquivo PostScript para o PDF usando a API do Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converta um arquivo PostScript em um documento do PDF usando a API de serviço do Distiller (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-destiller-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente de serviço Distiller.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `DistillerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere o arquivo para converter.

   * Crie um `java.io.FileInputStream` objeto que representa o arquivo a ser convertido usando seu construtor e passando um valor de string que especifica o local do arquivo.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Chame a operação de criação de PDF.

   Chame o `DistillerServiceClient` do objeto `createPDF` e transmita os seguintes valores:

   * O `com.adobe.idp.Document` objeto que representa o arquivo PS, EPS ou PRN a ser convertido
   * A `java.lang.String` objeto que contém o nome do arquivo a ser convertido
   * A `java.lang.String` objeto que contém o nome das configurações do Adobe PDF a serem usadas
   * A `java.lang.String` objeto que contém o nome das configurações de segurança a serem usadas
   * Uma `com.adobe.idp.Document` objeto que contém configurações a serem aplicadas durante a geração do documento PDF
   * Uma `com.adobe.idp.Document` objeto que contém informações de metadados a serem aplicadas ao documento PDF

   O `createPDF` método retorna um `CreatePDFResult` objeto que contém o novo documento PDF e um arquivo de log que pode ser gerado. O arquivo de log normalmente contém mensagens de erro ou aviso geradas pela solicitação de conversão.

1. Salve o documento PDF.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `CreatePDFResult` do objeto `getCreatedDocument` método . Isso retorna uma `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

   Da mesma forma, para obter o documento de log, execute as seguintes ações.

   * Chame o `CreatePDFResult` do objeto `getLogDocument` método . Isso retorna uma `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento de log.


**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Conversão de um arquivo PostScript em um documento do PDF usando a API do Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversão de um arquivo PostScript para o PDF usando a API do serviço da Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converta um arquivo PostScript em um documento do PDF usando a API de serviço do Distiller (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente de serviço Distiller.

   * Crie um `DistillerServiceClient` usando seu construtor padrão.
   * Crie um `DistillerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `DistillerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo para converter.

   * Crie um `BLOB` usando seu construtor. Essa `BLOB` é usado para armazenar o arquivo para conversão em um documento PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Chame a operação de criação de PDF.

   Chame o `DistillerServiceService` do objeto `CreatePDF2` e passe os seguintes valores obrigatórios:

   * O `BLOB` objeto que representa o arquivo PS a ser convertido
   * Uma string que contém o nome do caminho do arquivo a ser convertido
   * Um objeto de string que contém as configurações do Adobe PDF a serem usadas (por exemplo, `Standard`)
   * Um objeto de string que contém as configurações de segurança a serem usadas (por exemplo, `No Securit`y)
   * Uma `BLOB` objeto que contém configurações a serem aplicadas durante a geração do documento PDF
   * Uma `BLOB` objeto que contém informações de metadados a serem aplicadas ao documento PDF
   * A `BLOB` parâmetro de saída usado para armazenar o documento PDF
   * A `BLOB` parâmetro de saída usado para armazenar o log

1. Salve o documento PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento de PDF assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `CreatePDF2` (o parâmetro de saída). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
