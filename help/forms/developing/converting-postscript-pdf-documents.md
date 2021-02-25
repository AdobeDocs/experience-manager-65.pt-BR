---
title: Conversão do Postscript em Documentos PDF
seo-title: Conversão do Postscript em Documentos PDF
description: Use o serviço Distiller para converter arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller converte grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações usando a API Java e a API de serviço da Web.
seo-description: Use o serviço Distiller para converter arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller converte grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações usando a API Java e a API de serviço da Web.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---


# Conversão do Postscript em Documentos PDF {#converting-postscript-to-pdf-documents}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

## Sobre o Distiller Service {#about-the-distiller-service}

O serviço Distiller® converte arquivos PostScript®, Encapsulated PostScript (EPS) e PRN em arquivos PDF compactos, confiáveis e mais seguros em uma rede. O serviço Distiller é frequentemente usado para converter grandes volumes de documentos impressos em documentos eletrônicos, como faturas e declarações. A conversão de documentos em PDF também permite que as empresas enviem aos seus clientes uma versão em papel e uma versão eletrônica de um documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos PostScript em PDF {#converting-postscript-to-pdf-documents-inner}

Este tópico descreve como você pode usar a Distiller Service API (Java e serviço da Web) para converter programaticamente arquivos PostScript (PS), Encapsulated PostScript (EPS) e PRN em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Distiller, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para converter arquivos PostScript em documentos PDF, é necessário instalar um dos seguintes arquivos no servidor que hospeda o AEM Forms: Pacote redistribuível Acrobat 9 ou Microsoft Visual C++ 2005.

### Resumo das etapas {#summary-of-steps}

Para converter qualquer um dos tipos suportados em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Distiller.
1. Recupere o arquivo a ser convertido.
1. Chame a operação de criação de PDF.
1. Salve o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente de serviço Distiller**

Antes de executar programaticamente uma operação de serviço da Distiller, você deve criar um cliente de serviço da Distiller. Se você estiver usando a API Java, crie um objeto `DistillerServiceClient`. Se você estiver usando a API de serviço da Web, crie um objeto `DistillerServiceService`.

**Recuperar o arquivo a ser convertido**

Você deve recuperar o arquivo que deseja converter. Por exemplo, para converter um arquivo PS em um documento PDF, é necessário recuperar o arquivo PS.

**Chamar a operação de criação de PDF**

Depois de criar o cliente de serviço, você pode invocar a operação de criação de PDF. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o caminho para o documento do público alvo.

**Salvar o documento PDF**

É possível salvar o documento PDF como um arquivo PDF.

**Consulte também:**

[Converter um arquivo PostScript em PDF usando a API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Converter um arquivo PostScript em PDF usando a API de serviço da Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Converter um arquivo PostScript em PDF usando a API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Converta um arquivo PostScript em documento PDF usando a Distiller Service API (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-dicler-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente de serviço Distiller.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DistillerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o arquivo a ser convertido.

   * Crie um objeto `java.io.FileInputStream` que representa o arquivo a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Chame a operação de criação de PDF.

   Chame o método `DistillerServiceClient` do objeto `createPDF` e passe os seguintes valores:

   * O objeto `com.adobe.idp.Document` que representa o arquivo PS, EPS ou PRN a ser convertido
   * Um objeto `java.lang.String` que contém o nome do arquivo a ser convertido
   * Um objeto `java.lang.String` que contém o nome das configurações do Adobe PDF a serem usadas
   * Um objeto `java.lang.String` que contém o nome das configurações de segurança a serem usadas
   * Um objeto `com.adobe.idp.Document` opcional que contém configurações a serem aplicadas ao gerar o documento PDF
   * Um objeto opcional `com.adobe.idp.Document` que contém informações de metadados a serem aplicadas ao documento PDF

   O método `createPDF` retorna um objeto `CreatePDFResult` que contém o novo documento PDF e um arquivo de log que pode ser gerado. O arquivo de log geralmente contém mensagens de erro ou aviso geradas pela solicitação de conversão.

1. Salve o documento PDF.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o método `CreatePDFResult` do objeto `getCreatedDocument`. Isso retorna um objeto `com.adobe.idp.Document`.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

   Da mesma forma, para obter o documento de log, execute as seguintes ações.

   * Chame o método `CreatePDFResult` do objeto `getLogDocument`. Isso retorna um objeto `com.adobe.idp.Document`.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento de log.


**Consulte também:**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

[Start rápido (modo SOAP): Converter um arquivo PostScript em um documento PDF usando a API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um arquivo PostScript em PDF usando a API de serviço da Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Converta um arquivo PostScript em documento PDF usando a Distiller Service API (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente de serviço Distiller.

   * Crie um objeto `DistillerServiceClient` usando seu construtor padrão.
   * Crie um objeto `DistillerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/DistillerService?blob=mtom`.) Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `DistillerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo a ser convertido.

   * Crie um objeto `BLOB` usando seu construtor. Esse objeto `BLOB` é usado para armazenar o arquivo a ser convertido em um documento PDF.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Chame a operação de criação de PDF.

   Chame o método `DistillerServiceService` do objeto `CreatePDF2` e passe os seguintes valores obrigatórios:

   * O objeto `BLOB` que representa o arquivo PS a ser convertido
   * Uma string que contém o nome do caminho do arquivo a ser convertido
   * Um objeto de string que contém as configurações do Adobe PDF a serem usadas (por exemplo, `Standard`)
   * Um objeto de string que contém as configurações de segurança a serem usadas (por exemplo, `No Securit`y)
   * Um objeto `BLOB` opcional que contém configurações a serem aplicadas ao gerar o documento PDF
   * Um objeto opcional `BLOB` que contém informações de metadados a serem aplicadas ao documento PDF
   * Um parâmetro de saída `BLOB` usado para armazenar o documento PDF
   * Um parâmetro de saída `BLOB` usado para armazenar o log

1. Salve o documento PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `CreatePDF2` (o parâmetro de saída). Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
