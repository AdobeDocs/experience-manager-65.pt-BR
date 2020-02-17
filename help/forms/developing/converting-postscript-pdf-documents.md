---
title: Convertendo o Postscript em documentos PDF
seo-title: Convertendo o Postscript em documentos PDF
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Convertendo o Postscript em documentos PDF {#converting-postscript-to-pdf-documents}

## Sobre o Distiller Service {#about-the-distiller-service}

O serviço Distiller® converte arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller é frequentemente usado para converter grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações. A conversão de documentos em PDF também permite que as empresas enviem aos seus clientes uma versão em papel e uma versão eletrônica de um documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Converter PostScript em documentos PDF {#converting-postscript-to-pdf-documents-inner}

Este tópico descreve como você pode usar a Distiller Service API (Java e serviço da Web) para converter programaticamente arquivos PostScript (PS), Encapsulated PostScript (EPS) e PRN em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para converter arquivos PostScript em documentos PDF, é necessário instalar um dos seguintes arquivos no servidor que hospeda o AEM Forms: Pacote redistribuível Acrobat 9 ou Microsoft Visual C++ 2005.

### Resumo das etapas {#summary-of-steps}

Para converter qualquer um dos tipos suportados em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Distiller.
1. Recupere o arquivo para converter.
1. Chame a operação de criação de PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente de serviço Distiller**

Antes de executar programaticamente uma operação de serviço do Distiller, você deve criar um cliente de serviço do Distiller. Se você estiver usando a API Java, crie um `DistillerServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `DistillerServiceService` objeto.

**Recuperar o arquivo a ser convertido**

Você deve recuperar o arquivo que deseja converter. Por exemplo, para converter um arquivo PS em um documento PDF, é necessário recuperar o arquivo PS.

**Chamar a operação de criação de PDF**

Depois de criar o cliente de serviço, você pode invocar a operação de criação de PDF. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o caminho para o documento de destino.

**Salvar o documento PDF**

É possível salvar o documento PDF como um arquivo PDF.

**Consulte também:**

[Converter um arquivo PostScript em PDF usando a API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Converter um arquivo PostScript em PDF usando a API de serviço da Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço de saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Converter um arquivo PostScript em PDF usando a API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converta um arquivo PostScript em documento PDF usando a API do Distiller Service (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-dicler-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente de serviço Distiller.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DistillerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o arquivo para converter.

   * Crie um `java.io.FileInputStream` objeto que represente o arquivo a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Chame a operação de criação de PDF.

   Chame o método do `DistillerServiceClient` objeto `createPDF` e passe os seguintes valores:

   * O `com.adobe.idp.Document` objeto que representa o arquivo PS, EPS ou PRN a ser convertido
   * Um `java.lang.String` objeto que contém o nome do arquivo a ser convertido
   * Um `java.lang.String` objeto que contém o nome das configurações do Adobe PDF a serem usadas
   * Um `java.lang.String` objeto que contém o nome das configurações de segurança a serem usadas
   * Um `com.adobe.idp.Document` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF
   * Um `com.adobe.idp.Document` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF
   O `createPDF` método retorna um `CreatePDFResult` objeto que contém o novo documento PDF e um arquivo de log que pode ser gerado. O arquivo de log geralmente contém mensagens de erro ou aviso geradas pela solicitação de conversão.

1. Salve o documento PDF.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `CreatePDFResult` método do `getCreatedDocument` objeto. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o documento PDF.
   Da mesma forma, para obter o documento de log, execute as seguintes ações.

   * Chame o `CreatePDFResult` método do `getLogDocument` objeto. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o método do `com.adobe.idp.Document` objeto para extrair o documento `copyToFile` de log.


**Consulte também:**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Converter um arquivo PostScript em um documento PDF usando a API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um arquivo PostScript em PDF usando a API de serviço da Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converta um arquivo PostScript em documento PDF usando a Distiller Service API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente de serviço Distiller.

   * Crie um `DistillerServiceClient` objeto usando seu construtor padrão.
   * Crie um `DistillerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `DistillerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo para converter.

   * Crie um `BLOB` objeto usando seu construtor. Esse `BLOB` objeto é usado para armazenar o arquivo a ser convertido em um documento PDF.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Chame a operação de criação de PDF.

   Chame o `DistillerServiceService` método do `CreatePDF2` objeto e passe os seguintes valores obrigatórios:

   * O `BLOB` objeto que representa o arquivo PS a ser convertido
   * Uma string que contém o nome do caminho do arquivo a ser convertido
   * Um objeto de string que contém as configurações do Adobe PDF a serem usadas (por exemplo, `Standard`)
   * Um objeto de string que contém as configurações de segurança a serem usadas (por exemplo, `No Securit`y)
   * Um `BLOB` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF
   * Um `BLOB` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF
   * Um parâmetro de `BLOB` saída usado para armazenar o documento PDF
   * Um parâmetro `BLOB` de saída usado para armazenar o log

1. Salve o documento PDF.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `BLOB` objeto retornado pelo `CreatePDF2` método (o parâmetro de saída). Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
