---
title: Conversão entre formatos de arquivo e PDF
seo-title: Conversão entre formatos de arquivo e PDF
description: 'null'
seo-description: 'null'
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Conversão entre formatos de arquivo e PDF {#converting-between-file-formatsand-pdf}

**Sobre o serviço Gerar PDF**

O serviço Gerar PDF converte formatos de arquivo nativos em PDF. Também converte PDF em outros formatos de arquivo e otimiza o tamanho dos documentos PDF.

O serviço Gerar PDF usa aplicativos nativos para converter os seguintes formatos de arquivo em PDF. Salvo indicação em contrário, somente as versões em alemão, francês, inglês e japonês desses aplicativos são compatíveis. *O Windows indica apenas* suporte para Windows Server® 2003 e Windows Server 2008.

* Microsoft Office 2003 e 2007 para converter DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS e PUB (somente Windows)

   **Observação**: O Acrobat® 9.2 ou posterior é necessário para converter o formato Microsoft XPS em PDF.*

* Autodesk AutoCAD 2005, 2006, 2007, 2008 e 2009 para converter DWF, DWG e DXW (somente em inglês)
* Corel WordPerfect 12 e X4 para converter WPD, QPW, SHW (somente em inglês)
* OpenOffice 2.0, 2.4, 3.0.1 e 3.1 para converter ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOC, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX e PUB

   ***Observação **: O serviço Gerar PDF não suporta as versões de 64 bits do OpenOffice.*

* Adobe Photoshop® CS2 para converter PSD (somente Windows)

   ***Observação**: O Photoshop CS3 e CS4 não são suportados porque não são compatíveis com o Windows Server 2003 ou o Windows Server 2008. *

* Adobe FrameMaker® 7.2 e 8 para converter FM (somente Windows)
* Adobe PageMaker® 7.0 para converter PMD, PM6, P65 e PM (somente Windows)
* Formatos nativos suportados por aplicativos de terceiros (requer o desenvolvimento de arquivos de configuração específicos para o aplicativo) (somente Windows)

O serviço Gerar PDF converte os seguintes formatos de arquivo baseados em padrões em PDF.

* Formatos de vídeo: SWF, FLV (somente Windows)
* Formatos de imagem: JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ e Linux®)

O serviço Gerar PDF converte PDF nos seguintes formatos de arquivo (somente Windows):

* Encapsulated PostScript (EPS)
* HTML 3.2
* HTML 4.01 com CSS 1.0
* DOC (formato do Microsoft Word)
* RTF
* Texto (acessível e simples)
* XML
* PDF/A-1a que usa apenas o espaço de cor DeviceRGB
* PDF/A-1b que usa apenas o espaço de cor DeviceRGB

O serviço Gerar PDF exige que você execute estas tarefas administrativas:

* Instale os aplicativos nativos necessários no computador que hospeda o AEM Forms
* Instale o Adobe Acrobat Professional ou o Acrobat Pro Extended 9.2 no computador que hospeda o AEM Forms
* Execute tarefas de configuração pós-instalação

Essas tarefas são descritas em Instalar e implantar formulários do AEM usando o recurso JavaScript Turnkey.

É possível realizar essas tarefas usando o serviço Gerar PDF:

* Converter de formatos de arquivo nativos em PDF.
* Converta documentos HTML em documentos PDF.
* Converta documentos PDF em formatos de arquivo.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Gerar PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Converter Documentos do Word em Documentos PDF {#converting-word-documents-to-pdf-documents}

Esta seção descreve como você pode usar a API Gerar PDF para converter programaticamente um documento do Microsoft Word em um documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre formatos de arquivo adicionais, consulte [Adicionar suporte para formatos](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)de arquivo nativos adicionais.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Gerar PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para converter um documento do Microsoft Word em um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente Gerar PDF.
1. Recupere o arquivo para convertê-lo em um documento PDF.
1. Converta o arquivo em um documento PDF.
1. Recupere os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Gerar PDF**

Antes de executar programaticamente uma operação Gerar PDF, crie um cliente de serviço Gerar PDF. Se você estiver usando a API Java, crie um `GeneratePdfServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `GeneratePDFServiceService` objeto.

**Recuperar o arquivo para converter em um documento PDF**

Recupere o documento do Microsoft Word para converter em um documento PDF.

**Converter o arquivo em um documento PDF**

Depois de criar o cliente de serviço Gerar PDF, você pode chamar o `createPDF2` método. Esse método precisa de informações sobre o documento a ser convertido, incluindo a extensão do arquivo.

**Recuperar os resultados**

Depois que o arquivo for convertido em um documento PDF, você poderá recuperar os resultados. Por exemplo, depois de converter um arquivo do Word em um documento PDF, é possível recuperar e salvar o documento PDF.

**Consulte também:**

[Converter documentos do Word em documentos PDF usando a API Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Converter documentos do Word em documentos PDF usando a API de serviço da Web](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Gerar Start rápidos da API do serviço PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Converter documentos do Word em documentos PDF usando a API Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Converta um documento do Microsoft Word em um documento PDF usando a API Gerar PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-generatepdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Gerar PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `GeneratePdfServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o arquivo para convertê-lo em um documento PDF.

   * Crie um `java.io.FileInputStream` objeto que represente o arquivo do Word a ser convertido usando seu construtor. Passe um valor de string que especifica o local do arquivo.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Converta o arquivo em um documento PDF.

   Converta o arquivo em um documento PDF chamando o método do `GeneratePdfServiceClient` objeto `createPDF2` e transmitindo os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o arquivo a ser convertido.
   * Um `java.lang.String` objeto que contém a extensão de arquivo.
   * Um `java.lang.String` objeto que contém as configurações de tipo de arquivo a serem usadas na conversão. As configurações de tipo de arquivo fornecem configurações de conversão para diferentes tipos de arquivo, como .doc ou .xls.
   * Um `java.lang.String` objeto que contém o nome das configurações do PDF a serem usadas. For example, you can specify `Standard`.
   * Um `java.lang.String` objeto que contém o nome das configurações de segurança a serem usadas.
   * Um `com.adobe.idp.Document` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF.
   * Um `com.adobe.idp.Document` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF.
   O `createPDF2` método retorna um `CreatePDFResult` objeto que contém o novo documento PDF e as informações de um registro. O arquivo de log geralmente contém mensagens de erro ou aviso geradas pela solicitação de conversão.

1. Recupere os resultados.

   Para obter o documento PDF, execute as seguintes ações:

   * Chame o `CreatePDFResult` método do `getCreatedDocument` objeto, que retorna um `com.adobe.idp.Document` objeto.
   * Chame o método do `com.adobe.idp.Document` `copyToFile` objeto para extrair o documento PDF do objeto criado na etapa anterior.
   Se você usou o `createPDF2` método para obter o documento de log (não aplicável às conversões HTML), execute as seguintes ações:

   * Chame o `CreatePDFResult` método do `getLogDocument` objeto. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o método `com.adobe.idp.Document` `copyToFile` do objeto para extrair o documento de log.


**Consulte também:**

[Resumo das etapas](converting-file-formats-pdf.md#summary-of-steps)

[Start rápido (modo SOAP): Converter um documento do Microsoft Word em um documento PDF usando a API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos do Word em documentos PDF usando a API de serviço da Web {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Converta um documento do Microsoft Word em um documento PDF usando a API Gerar PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Gerar PDF.

   * Crie um `GeneratePDFServiceClient` objeto usando seu construtor padrão.
   * Crie um `GeneratePDFServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `GeneratePDFServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o arquivo para convertê-lo em um documento PDF.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o arquivo que você deseja converter em um documento PDF.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo a ser convertido e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo à sua `MTOM` propriedade o conteúdo da matriz de bytes.

1. Converta o arquivo em um documento PDF.

   Converta o arquivo em um documento PDF chamando o método do `GeneratePDFServiceService` objeto `CreatePDF2` e transmitindo os seguintes valores:

   * Um `BLOB` objeto que representa o arquivo a ser convertido.
   * Uma string que contém a extensão do arquivo.
   * Um `java.lang.String` objeto que contém as configurações de tipo de arquivo a serem usadas na conversão. As configurações de tipo de arquivo fornecem configurações de conversão para diferentes tipos de arquivo, como .doc ou .xls.
   * Um objeto de string que contém as configurações de PDF a serem usadas. Você pode especificar `Standard`.
   * Um objeto de string que contém as configurações de segurança a serem usadas. Você pode especificar `No Security`.
   * Um `BLOB` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF.
   * Um `BLOB` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF.
   * Um parâmetro de saída do tipo `BLOB` que é preenchido pelo `CreatePDF2` método. O `CreatePDF2` método preenche esse objeto com o documento convertido. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * Um parâmetro de saída do tipo `BLOB` que é preenchido pelo `CreatePDF2` método. O `CreatePDF2` método preenche esse objeto com o documento de log. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

1. Recupere os resultados.

   * Recupere o documento PDF convertido atribuindo o campo do `BLOB` objeto `MTOM` a uma matriz de bytes. A matriz de bytes representa o documento PDF convertido. Certifique-se de usar o `BLOB` objeto usado como parâmetro de saída para o `createPDF2` método.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF convertido.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-file-formats-pdf.md#summary-of-steps)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Converter Documentos HTML em Documentos PDF {#converting-html-documents-to-pdf-documents}

Esta seção descreve como você pode usar a API Gerar PDF para converter programaticamente documentos HTML em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Gerar PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento HTML em um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente Gerar PDF.
1. Recupere o conteúdo HTML para converter em um documento PDF.
1. Converta o conteúdo HTML em um documento PDF.
1. Recupere os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Gerar PDF**

Antes de executar programaticamente uma operação Gerar PDF, é necessário criar um cliente de serviço Gerar PDF. Se você estiver usando a API Java, crie um `GeneratePdfServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `GeneratePDFServiceService`.

**Recuperar o conteúdo HTML para converter em um documento PDF**

Faça referência ao conteúdo HTML que você deseja converter em um documento PDF. Você pode fazer referência a conteúdo HTML, como um arquivo HTML ou conteúdo HTML que esteja acessível usando um URL.

**Converter o conteúdo HTML em um documento PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de criação de PDF apropriada. Esta operação precisa de informações sobre o documento a ser convertido, incluindo o caminho para o documento do público alvo.

**Recuperar os resultados**

Depois que o conteúdo HTML é convertido em um documento PDF, você pode recuperar os resultados e salvar o documento PDF.

**Consulte também:**

[Converter conteúdo HTML em um documento PDF usando a API Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Converter conteúdo HTML em um documento PDF usando a API de serviço da Web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Gerar Start rápidos da API do serviço PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Converter conteúdo HTML em um documento PDF usando a API Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Converta um documento HTML em um documento PDF usando a API Gerar PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-generatepdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Gerar PDF.

   Crie um `GeneratePdfServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Recupere o conteúdo HTML para converter em um documento PDF.

   Recupere o conteúdo HTML criando uma variável de string e atribuindo um URL que aponte para o conteúdo HTML.

1. Converta o conteúdo HTML em um documento PDF.

   Chame o método do `GeneratePdfServiceClient` objeto `htmlToPDF2` e passe os seguintes valores:

   * Um `java.lang.String` objeto que contém o URL do arquivo HTML a ser convertido.
   * Um `java.lang.String` objeto que contém as configurações de tipo de arquivo a serem usadas na conversão. As configurações de tipo de arquivo podem incluir níveis de aranha.
   * Um `java.lang.String` objeto que contém o nome das configurações de segurança a serem usadas.
   * Um `com.adobe.idp.Document` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF. Se essas informações não forem fornecidas, as configurações serão escolhidas automaticamente com base nos três parâmetros anteriores.
   * Um `com.adobe.idp.Document` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF.

1. Recupere os resultados.

   O `htmlToPDF2` método retorna um `HtmlToPdfResult` objeto que contém o novo documento PDF que foi gerado. Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `HtmlToPdfResult` método do `getCreatedDocument` objeto. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o método do `com.adobe.idp.Document` `copyToFile` objeto para extrair o documento PDF do objeto criado na etapa anterior.

**Consulte também:**

[Converter Documentos HTML em Documentos PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Start rápido (modo SOAP): Converter conteúdo HTML em um documento PDF usando a API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Start rápido (modo SOAP): Converter conteúdo HTML em um documento PDF usando a API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter conteúdo HTML em um documento PDF usando a API de serviço da Web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Converta o conteúdo HTML em um documento PDF usando a API Gerar PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Gerar PDF.

   * Crie um `GeneratePDFServiceClient` objeto usando seu construtor padrão.
   * Crie um `GeneratePDFServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `GeneratePDFServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o conteúdo HTML para converter em um documento PDF.

   Recupere o conteúdo HTML criando uma variável de string e atribuindo um URL que aponte para o conteúdo HTML.

1. Converta o conteúdo HTML em um documento PDF.

   Converta o conteúdo HTML em um documento PDF chamando o método do `GeneratePDFServiceService` objeto `HtmlToPDF2` e transmita os seguintes valores:

   * Uma string que contém o conteúdo HTML a ser convertido.
   * Um `java.lang.String` objeto que contém as configurações de tipo de arquivo a serem usadas na conversão.
   * Um objeto de string que contém as configurações de segurança a serem usadas.
   * Um `BLOB` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF.
   * Um `BLOB` objeto opcional que contém informações de metadados a serem aplicadas ao documento PDF.
   * Um parâmetro de saída do tipo `BLOB` que é preenchido pelo `CreatePDF2` método. O `CreatePDF2` método preenche esse objeto com o documento convertido. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

1. Recupere os resultados.

   * Recupere o documento PDF convertido atribuindo o campo do `BLOB` objeto `MTOM` a uma matriz de bytes. A matriz de bytes representa o documento PDF convertido. Certifique-se de usar o `BLOB` objeto usado como parâmetro de saída para o `HtmlToPDF2` método.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF convertido.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Converter Documentos HTML em Documentos PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Converter Documentos PDF em formatos que não sejam de imagem {#converting-pdf-documents-to-non-image-formats}

Esta seção descreve como você pode usar a API Gerar PDF Java e a API de serviço da Web para converter programaticamente um documento PDF em um arquivo RTF, que é um exemplo de um formato que não seja de imagem. Outros formatos que não sejam de imagem incluem HTML, texto, DOC e EPS. Ao converter um documento PDF em RTF, verifique se o documento PDF não contém elementos de formulário, como um botão Enviar. Elementos de formulário não são convertidos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Gerar PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-2}

Para converter um documento PDF em qualquer um dos tipos suportados, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente Gerar PDF.
1. Recupere o documento PDF a ser convertido.
1. Converta o documento PDF.
1. Salve o arquivo convertido.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Gerar PDF**

Antes de executar programaticamente uma operação Gerar PDF, é necessário criar um cliente de serviço Gerar PDF. Se você estiver usando a API Java, crie um `GeneratePdfServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `GeneratePDFServiceService` objeto.

**Recuperar o documento PDF a ser convertido**

Recupere o documento PDF para convertê-lo em um formato que não seja de imagem.

**Converter o documento PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de exportação de PDF. Esta operação precisa de informações sobre o documento a ser convertido, incluindo o caminho para o documento do público alvo.

**Salvar o arquivo convertido**

Salve o arquivo convertido. Por exemplo, se você converter um documento PDF em um arquivo RTF, salve o documento convertido em um arquivo RTF.

**Consulte também:**

[Converter um documento PDF em um arquivo RTF usando a API Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Converter um documento PDF em um arquivo RTF usando a API de serviço da Web](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Gerar Start rápidos da API do serviço PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em um arquivo RTF usando a API Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Converta um documento PDF em um arquivo RTF usando a API Gerar PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-generatepdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Gerar PDF.

   Crie um `GeneratePdfServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Recupere o documento PDF a ser convertido.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF a ser convertido usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Converta o documento PDF.

   Chame o método do `GeneratePdfServiceClient` objeto `exportPDF2` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o arquivo PDF a ser convertido.
   * Um `java.lang.String` objeto que contém o nome do arquivo a ser convertido.
   * Um `java.lang.String` objeto que contém o nome das configurações do Adobe PDF.
   * Um `ConvertPDFFormatType` objeto que especifica o tipo de arquivo de público alvo para a conversão.
   * Um `com.adobe.idp.Document` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF.
   O `exportPDF2` método retorna um `ExportPDFResult` objeto que contém o arquivo convertido.

1. Converta o documento PDF.

   Para obter o arquivo recém-criado, execute as seguintes ações:

   * Chame o `ExportPDFResult` método do `getConvertedDocument` objeto. Isso retorna um `com.adobe.idp.Document` objeto.
   * Chame o método do `com.adobe.idp.Document` objeto para extrair o novo `copyToFile` documento.

**Consulte também:**

[Resumo das etapas](converting-file-formats-pdf.md#summary-of-steps)

[Start rápido (modo SOAP): Converter conteúdo HTML em um documento PDF usando a API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento PDF em um arquivo RTF usando a API de serviço da Web {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Converta um documento PDF em um arquivo RTF usando a API Gerar PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Generate PDf.

   * Crie um `GeneratePDFServiceClient` objeto usando seu construtor padrão.
   * Crie um `GeneratePDFServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `GeneratePDFServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF a ser convertido.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF que é convertido.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo à sua `MTOM` propriedade o conteúdo da matriz de bytes.

1. Converta o documento PDF.

   Chame o método do `GeneratePDFServiceServiceWse` objeto `ExportPDF2` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o arquivo PDF a ser convertido.
   * Uma string que contém o nome do caminho do arquivo a ser convertido.
   * Um `java.lang.String` objeto que especifica o local do arquivo.
   * Um objeto de string que especifica o tipo de arquivo de público alvo para a conversão. Especifique `RTF`.
   * Um `BLOB` objeto opcional que contém configurações a serem aplicadas ao gerar o documento PDF.
   * Um parâmetro de saída do tipo `BLOB` que é preenchido pelo `ExportPDF2` método. O `ExportPDF2` método preenche esse objeto com o documento convertido. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

1. Salve o arquivo convertido.

   * Recupere o documento RTF convertido atribuindo o campo do `BLOB` objeto `MTOM` a uma matriz de bytes. A matriz de bytes representa o documento RTF convertido. Certifique-se de usar o `BLOB` objeto usado como parâmetro de saída para o `ExportPDF2` método.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa a localização do arquivo RTF.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo RTF, chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-file-formats-pdf.md#summary-of-steps)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Adicionar suporte para formatos de arquivo nativos adicionais {#adding-support-for-additional-native-file-formats}

Esta seção explica como adicionar suporte para formatos de arquivo nativos adicionais. Ele fornece uma visão geral das interações entre o serviço Gerar PDF e os aplicativos nativos que esse serviço usa para converter formatos de arquivo nativos em PDF.

Esta seção também explica o seguinte:

* Como modificar a resposta que o serviço Gerar PDF fornece aos aplicativos nativos que este produto já usa para converter formatos de arquivos nativos em PDF
* As interações entre o serviço Gerar PDF, o componente Gerar monitor de aplicativo do serviço PDF (AppMon) e os aplicativos nativos, como o Microsoft Word
* As funções que as gramáticas XML desempenham nessas interações

### Interações de componentes {#component-interactions}

O serviço Gerar PDF converte formatos de arquivo nativos chamando o aplicativo associado ao formato de arquivo e interagindo com o aplicativo para imprimir o documento usando a impressora padrão. A impressora padrão deve ser configurada como a impressora Adobe PDF.

Esta ilustração mostra os componentes e drivers envolvidos com o suporte a aplicativos nativos. Também menciona as gramáticas XML que influenciam as interações.

Interações de componentes para conversão de arquivos nativos

Esse documento usa o termo aplicativo ** nativo para indicar o aplicativo usado para produzir um formato de arquivo nativo, como o Microsoft Word.

*O AppMon* é um componente corporativo que interage com um aplicativo nativo da mesma forma que um usuário navegaria pelas caixas de diálogo apresentadas por esse aplicativo. As gramáticas XML usadas pelo AppMon para instruir um aplicativo, como o Microsoft Word, a abrir e imprimir um arquivo envolvem estas tarefas sequenciais:

1. Abrir o arquivo selecionando Arquivo > Abrir
1. Garantir que a caixa de diálogo Abrir seja exibida; se não, manipular o erro
1. Fornecimento do nome do arquivo no campo Nome do arquivo e clique no botão Abrir
1. Assegurar que o ficheiro seja aberto
1. Abrir a caixa de diálogo Imprimir selecionando Arquivo > Imprimir
1. Verificar se a caixa de diálogo Imprimir é exibida

O AppMon usa APIs Win32 padrão para interagir com aplicativos de terceiros a fim de transferir eventos de interface como pressionamentos de teclas e cliques do mouse, o que é útil para controlar esses aplicativos para produzir arquivos PDF deles.

Devido a uma limitação com essas APIs do Win32, o AppMon não é capaz de despachar esses eventos de interface para alguns tipos específicos de janelas, como barras de menu flutuantes (encontradas em alguns aplicativos, como o TextPad), e certos tipos de caixas de diálogo cujo conteúdo não pode ser recuperado usando as APIs do Win32.

É fácil identificar visualmente uma barra de menus flutuante; no entanto, talvez não seja possível identificar os tipos especiais de diálogos apenas por inspeção visual. Você precisaria de um aplicativo de terceiros, como o Microsoft Spy++ (parte do ambiente de desenvolvimento do Microsoft Visual C++) ou seu WinID equivalente (que pode ser baixado gratuitamente em [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) para examinar uma caixa de diálogo para determinar se o AppMon seria capaz de interagir com ele usando APIs Win32 padrão.

Se o WinID for capaz de extrair o conteúdo da caixa de diálogo, como texto, subjanelas, ID de classe de janela e assim por diante, o AppMon também será capaz de fazer o mesmo.

Esta tabela lista o tipo de informações usadas na impressão de formatos de arquivo nativos.

<table>
 <thead>
  <tr>
   <th><p>Tipo de informação</p></th>
   <th><p>Descrição</p></th>
   <th><p>Modificação/criação de entradas relacionadas a arquivos nativos </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Configurações administrativas </p></td>
   <td><p>Inclui configurações de PDF, configurações de segurança e configurações de tipo de arquivo. </p><p>As configurações de tipo de arquivo associam extensões de nome de arquivo aos aplicativos nativos correspondentes. As configurações de tipo de arquivo também especificam as configurações nativas do aplicativo usadas para imprimir arquivos nativos. </p></td>
   <td><p>Para alterar as configurações de um aplicativo nativo já compatível, o administrador do sistema define as Configurações de tipo de arquivo no console de administração. </p><p>Para adicionar suporte para um novo formato de arquivo nativo, edite o arquivo manualmente. (Consulte <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Adicionar ou modificar o suporte para um formato</a>de arquivo nativo.) </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Especifica interações entre o serviço Gerar PDF e um aplicativo nativo. Tais interações normalmente direcionam o aplicativo para imprimir um arquivo no driver Adobe PDF. </p><p>O script contém instruções que direcionam o aplicativo nativo para abrir caixas de diálogo específicas e que fornecem respostas específicas a campos e botões nessas caixas de diálogo. </p></td>
   <td><p>O serviço Gerar PDF inclui arquivos de script para todos os aplicativos nativos suportados. É possível modificar esses arquivos usando um aplicativo de edição XML.</p><p>Para adicionar suporte a um novo aplicativo nativo, é necessário criar um novo arquivo de script. (Consulte <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Criar ou modificar um arquivo XML de diálogo adicional para um aplicativo</a>nativo.) </p></td>
  </tr>
  <tr>
   <td><p>Instruções da caixa de diálogo genérica </p></td>
   <td><p>Especifica como responder a caixas de diálogo comuns a vários aplicativos. Essas caixas de diálogo são geradas por sistemas operacionais, aplicativos auxiliares (como o PDFMaker) e drivers. </p><p>O arquivo que contém essas informações é appmon.global.en_US.xml.</p></td>
   <td><p>Não modifique este arquivo. </p></td>
  </tr>
  <tr>
   <td><p>Instruções da caixa de diálogo específica do aplicativo</p></td>
   <td><p>Especifica como responder a caixas de diálogo específicas do aplicativo. </p><p>O arquivo que contém essas informações é appmon.<i>`[appname]`</i>.dialog.<i>`[locale]`</i>.xml (por exemplo, appmon.word.en_US.xml).</p></td>
   <td><p>Não modifique este arquivo. </p><p>Para adicionar instruções de caixa de diálogo para um novo aplicativo nativo, consulte <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Criar ou modificar um arquivo XML de diálogo adicional para um aplicativo</a>nativo.</p></td>
  </tr>
  <tr>
   <td><p>Instruções adicionais da caixa de diálogo específica do aplicativo </p></td>
   <td><p>Especifica substituições e adições às instruções da caixa de diálogo específica do aplicativo. A seção apresenta um exemplo dessas informações. </p><p>O arquivo que contém essas informações é appmon.<i>'[appname]`</i>.add.<i>`[locale]`</i>.xml. Um exemplo é appmon.add.en_US.xml.</p></td>
   <td><p>Arquivos desse tipo podem ser criados e modificados usando um aplicativo de edição XML. (Consulte <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Criar ou modificar um arquivo XML de diálogo adicional para um aplicativo</a>nativo.) </p><p><strong>Importante</strong>: Você deve criar instruções adicionais de caixa de diálogo específicas ao aplicativo para cada aplicativo nativo que seu servidor suportará. </p></td>
  </tr>
 </tbody>
</table>

### Sobre os arquivos XML de script e caixa de diálogo {#about-the-script-and-dialog-xml-files}

Arquivos XML de script direcionam o serviço Gerar PDF para navegar pelas caixas de diálogo do aplicativo da mesma forma que um usuário navegava pelas caixas de diálogo do aplicativo. Arquivos XML de script também direcionam o serviço Gerar PDF para responder às caixas de diálogo, executando ações como pressionar botões, marcar ou desmarcar caixas de seleção ou selecionar itens de menu.

Por outro lado, os arquivos XML de diálogo simplesmente respondem às caixas de diálogo com os mesmos tipos de ações usadas em arquivos XML de script.

#### Terminologia da caixa de diálogo e do elemento da janela {#dialog-box-and-window-element-terminology}

Esta seção e a próxima seção usam terminologia diferente para caixas de diálogo e os componentes que contêm, dependendo da perspectiva que está sendo descrita. Os componentes da caixa de diálogo são itens como botões, campos e caixas de combinação.

Quando esta seção e a próxima seção descrevem as caixas de diálogo e seus componentes da perspectiva de um usuário, termos como caixa *de* diálogo, *botão*, *campo* e caixa *de* combinação são usados.

Quando esta seção e a próxima seção descrevem as caixas de diálogo e seus componentes da perspectiva de sua representação interna, o termo elemento *de* janela é usado. A representação interna dos elementos da janela é uma hierarquia, na qual cada instância do elemento da janela é identificada por rótulos. A instância do elemento window também descreve suas características físicas e seu comportamento.

Na perspectiva de um usuário, as caixas de diálogo e seus componentes mostram comportamentos diferentes, onde alguns elementos da caixa de diálogo ficam ocultos até serem ativados. De uma perspectiva de representação interna, não existe essa questão de comportamento. Por exemplo, a representação interna de uma caixa de diálogo é semelhante à dos componentes que ela contém, com a exceção de que os componentes estão aninhados dentro da caixa de diálogo.

Esta seção descreve elementos XML que fornecem instruções ao AppMon. Esses elementos têm nomes como o `dialog` elemento e o `window` elemento. Esse documento usa uma fonte monoespaçada para distinguir elementos XML. O `dialog` elemento identifica uma caixa de diálogo que um arquivo de script XML pode fazer com que seja exibido, intencionalmente ou não. O `window` elemento identifica um elemento de janela (caixa de diálogo ou os componentes de uma caixa de diálogo).

#### Hierarquia {#hierarchy}

Este diagrama mostra a hierarquia do script e do XML da caixa de diálogo. Um arquivo XML de script está em conformidade com o schema script.xsd, que inclui (no sentido XML) o schema window.xsd. Da mesma forma, um arquivo XML de diálogo está em conformidade com o schema dialogs.xsd, que também inclui o schema window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Hierarquia do XML de script e caixa de diálogo

#### Arquivos XML de script {#script-xml-files}

Um arquivo *XML de* script especifica uma série de etapas que direcionam o aplicativo nativo para navegar até determinados elementos de janela e, em seguida, fornecer respostas a esses elementos. A maioria das respostas são textos ou pressionamentos de teclas que correspondem à entrada que um usuário fornece a um campo, caixa de combinação ou botão na caixa de diálogo correspondente.

O objetivo do suporte do serviço Gerar PDF para arquivos XML de script é direcionar um aplicativo nativo para imprimir um arquivo nativo. No entanto, os arquivos XML de script podem ser usados para realizar qualquer tarefa que um usuário possa executar ao interagir com as caixas de diálogo do aplicativo nativo.

As etapas em um arquivo XML de script são executadas em ordem, sem nenhuma oportunidade de ramificação. O único teste condicional suportado é para tempo limite/nova tentativa, o que faz com que um script seja encerrado se uma etapa não for concluída com êxito dentro de um período específico e após um número específico de tentativas.

Além das etapas sendo sequenciais, as instruções em uma etapa também são executadas em ordem. Você deve garantir que as etapas e instruções reflitam a ordem na qual um usuário executaria essas mesmas etapas.

Cada etapa em um arquivo XML de script identifica o elemento de janela que deve aparecer se as instruções da etapa forem executadas com êxito. Se uma caixa de diálogo inesperada for exibida durante a execução de uma etapa de script, o serviço Gerar PDF pesquisará os arquivos XML da caixa de diálogo conforme descrito na próxima seção.

#### Arquivos XML de diálogo {#dialog-xml-files}

A execução de aplicativos nativos exibe caixas de diálogo diferentes, que são exibidas independentemente de os aplicativos nativos estarem em um modo visível ou invisível. As caixas de diálogo podem ser geradas pelo sistema operacional ou pelo próprio aplicativo. Quando os aplicativos nativos estão sendo executados sob controle do serviço Gerar PDF, as caixas de diálogo do sistema e do aplicativo nativo são exibidas em uma janela invisível.

Um arquivo *XML de* diálogo especifica como o serviço Gerar PDF responde às caixas de diálogo do sistema ou do aplicativo nativo. Os arquivos XML da caixa de diálogo permitem que o serviço Gerar PDF responda a caixas de diálogo não solicitadas de uma forma que facilita o processo de conversão.

Quando o sistema ou aplicativo nativo exibe uma caixa de diálogo que não é manipulada pelo arquivo XML de script em execução no momento, o serviço Gerar PDF pesquisa os arquivos XML de diálogo nessa ordem, parando quando encontra uma correspondência:

* Apmon.`[appname]`.adicional.`[locale]`.xml
* Apmon.`[appname]`.`[locale]`.xml (não modifique este arquivo.)
* appmon.global.`[locale]`.xml (não modifique este arquivo.)

Se o serviço Gerar PDF encontrar uma correspondência para a caixa de diálogo, ele a rejeitará enviando o pressionamento de tecla ou outra ação especificada para a caixa de diálogo. Se as instruções para a caixa de diálogo especificarem uma mensagem de cancelamento, o serviço Gerar PDF finalizará o trabalho em execução no momento e gerará uma mensagem de erro. Essa mensagem de anulação seria especificada no `abortMessage` elemento na gramática XML do script.

Se o serviço Gerar PDF encontrar uma caixa de diálogo que não está descrita em nenhum dos arquivos listados anteriormente, o serviço Gerar PDF incorpora a legenda da caixa de diálogo à entrada do arquivo de log. O trabalho em execução no momento expira. Você pode usar as informações no arquivo de log para compor novas instruções no arquivo XML da caixa de diálogo adicional para o aplicativo nativo.

### Adicionar ou modificar o suporte para um formato de arquivo nativo {#adding-or-modifying-support-for-a-native-file-format}

Esta seção descreve as tarefas que você deve executar para suportar outros formatos de arquivo nativos ou para modificar o suporte para um formato de arquivo nativo já suportado.

Antes de poder adicionar ou modificar o suporte, você deve concluir as seguintes tarefas.

#### Escolha de uma ferramenta para identificar elementos de janela {#choosing-a-tool-for-identifying-window-elements}

Os arquivos XML de diálogo e script exigem que você identifique o elemento de janela (caixa de diálogo, campo ou outro componente de diálogo) ao qual a caixa de diálogo ou o elemento de script está respondendo. Por exemplo, depois que um script chama um menu para um aplicativo nativo, o script deve identificar o elemento de janela nesse menu ao qual os pressionamentos de tecla ou uma ação devem ser aplicados.

É possível identificar facilmente uma caixa de diálogo pela legenda que ela exibe em sua barra de título. No entanto, você deve usar uma ferramenta como o Microsoft Spy++ para identificar elementos de janela de nível inferior. Os elementos de janela de nível inferior podem ser identificados por meio de uma variedade de atributos, que não são óbvios. Além disso, cada aplicativo nativo pode identificar seu elemento de janela de forma diferente. Como resultado, há várias maneiras de identificar um elemento de janela. Esta é a ordem sugerida para considerar a identificação do elemento da janela:

1. Legenda se for exclusiva
1. ID de controle, que pode ou não ser exclusiva para uma determinada caixa de diálogo
1. Nome da classe, que pode ou não ser exclusivo

Qualquer um ou uma combinação desses três atributos pode ser usada para identificar uma janela.

Se os atributos não identificarem uma legenda, você poderá identificar um elemento de janela usando seu índice em relação ao pai. Um *índice* especifica a posição do elemento de janela em relação aos elementos de janela irmãos. Frequentemente, os índices são a única maneira de identificar caixas de combinação.

Esteja ciente destes problemas:

* O Microsoft Spy++ exibe legendas usando um E comercial (&amp;) para identificar a tecla de atalho da legenda. Por exemplo, Spy++ mostra a legenda de uma caixa de diálogo Imprimir como `Pri&nt`, o que indica que a tecla de atalho está *n*. Os títulos de legenda em arquivos XML de script e caixa de diálogo devem omitir os E comercial.
* Algumas legendas incluem quebras de linha. o serviço Gerar PDF não pode identificar quebras de linha. Se uma legenda incluir uma quebra de linha, inclua uma parte suficiente da legenda para diferenciá-la dos outros itens de menu e, em seguida, use expressões regulares para a parte omitida. Um exemplo é ( `^Long caption title$`).]. (Consulte [Uso de expressões regulares em atributos](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)de legenda.)
* Use entidades de caractere (também chamadas de sequências de escape) para caracteres XML reservados. Por exemplo, use `&` para o E comercial `<` e `>` para menos que e maior que símbolos, `&apos;` para apóstrofos e `&quot;` para aspas.

Se você planeja trabalhar em arquivos XML de diálogo ou script, instale o aplicativo Microsoft Spy++.

#### Desempacotar a caixa de diálogo e os arquivos de script {#unpackaging-the-dialog-and-script-files}

Os arquivos de diálogo e script residem no arquivo appmondata.jar. Antes de poder modificar qualquer um desses arquivos ou adicionar novo script ou arquivos de diálogo, você deve desempacotar esse arquivo JAR. Por exemplo, suponha que você deseja adicionar suporte ao aplicativo EditPlus. Você cria dois arquivos XML, chamados appmon.editplus.script.en_US.xml e appmon.editplus.script.add.en_US.xml. Esses scripts XML devem ser adicionados ao arquivo adobe-appmondata.jar em dois locais, conforme especificado abaixo:

* adobe-livecycle-native-jHead-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. O arquivo adobe-livecycle-native-jpatrão-x86_win32.ear está na pasta de exportação em `[AEM forms install directory]\configurationManager`. (se o AEM Forms for implantado em outro servidor de aplicativos J2EE, substitua o arquivo adobe-livecycle-native-jHead-x86_win32.ear pelo arquivo EAR que corresponde ao servidor de aplicativos J2EE.)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (o arquivo adobe-appmondata.jar está no arquivo adobe-generatepdf-dsc.jar). O arquivo adobe-generatepdf-dsc.jar está na `[AEM forms install directory]\deploy` pasta.

Depois de adicionar esses arquivos XML ao arquivo adobe-appmondata.jar, é necessário reimplantar o componente GeneratePDF. Para adicionar arquivos XML de diálogo e script ao arquivo adobe-appmondata.jar, execute estas tarefas:

1. Usando uma ferramenta como WinZip ou WinRAR, abra o arquivo adobe-livecycle-native-jHead-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > arquivo adobe-appmondata.jar.
1. Adicione a caixa de diálogo e os arquivos XML de script ao arquivo appmondata.jar ou modifique os arquivos XML existentes nesse arquivo. (Consulte [Criar ou modificar um arquivo XML de script para um](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)aplicativo nativo e [Criar ou modificar um arquivo XML de diálogo adicional para um aplicativo](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)nativo.)
1. Usando uma ferramenta como WinZip ou WinRAR, abra adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Adicione a caixa de diálogo e os arquivos XML de script ao arquivo appmondata.jar ou modifique os arquivos XML existentes nesse arquivo. (Consulte [Criar ou modificar um arquivo XML de script para um](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)aplicativo nativo e [Criar ou modificar um arquivo XML de diálogo adicional para um aplicativo](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)nativo.) Depois de adicionar os arquivos XML ao arquivo adobe-appmondata.jar, coloque o novo arquivo adobe-appmondata.jar no arquivo adobe-generatepdf-dsc.jar.
1. Se você tiver adicionado suporte para um formato de arquivo nativo adicional, crie uma variável de ambiente do sistema que forneça o caminho do aplicativo (Consulte [Criação de uma variável de ambiente para localizar o aplicativo](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)nativo.)

**Para reimplantar o componente GeneratePDF**

1. Faça logon no Workbench.
1. Selecione **Janela** > **Mostrar Visualizações** > **Componentes**. Essa ação adiciona a visualização Componentes ao Workbench.
1. Clique com o botão direito do mouse no componente GeneratePDF e selecione **Parar componente**.
1. Quando o componente tiver parado, clique com o botão direito do mouse e selecione Desinstalar componente para removê-lo.
1. Clique com o botão direito do mouse no ícone **Componentes** e selecione **Instalar componente**.
1. Procure e selecione o arquivo adobe-generatepdf-dsc.jar modificado e clique em Abrir. Observe que um quadrado vermelho aparece ao lado do componente GeneratePDF.
1. Expanda o componente GeneratePDF, selecione Service Descriptors e clique com o botão direito do mouse em GeneratePDFService e selecione Ativate Service.
1. Na caixa de diálogo de configuração que é exibida, digite os valores de configuração aplicáveis. Se esses valores ficarem em branco, os valores de configuração padrão serão usados.
1. Clique com o botão direito do mouse em Gerar PDF e selecione Componente do Start.
1. Expanda Ative Services. Uma seta verde é exibida ao lado do nome do serviço, se ele estiver em execução. Caso contrário, o serviço está em um estado parado.
1. Se o serviço estiver em um estado parado, clique com o botão direito do mouse no nome do serviço e selecione Serviço de Start.

### Criação ou modificação de um arquivo XML de script para um aplicativo nativo {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Se quiser direcionar arquivos para um novo aplicativo nativo, você deve criar um arquivo XML de script para esse aplicativo. Se quiser modificar como o serviço Gerar PDF interage com um aplicativo nativo que já é suportado, você deve modificar o script desse aplicativo.

O script contém instruções que navegam pelos elementos de janela do aplicativo nativo e fornecem respostas específicas a esses elementos. O arquivo que contém essas informações é `appmon.`[appname]&quot; `.script.`[locale]`.xml`. Um exemplo é appmon.notepad.script.en_US.xml.

#### Como identificar etapas que o script deve executar {#identifying-steps-the-script-must-execute}

Usando o aplicativo nativo, determine os elementos da janela que devem ser navegados e cada resposta que deve ser executada para imprimir o documento. Observe as caixas de diálogo que resultam de qualquer resposta. As etapas serão semelhantes a estas:

1. Selecione Arquivo > Abrir.
1. Especifique o caminho e clique em Abrir.
1. Selecione Arquivo > Imprimir na barra de menus.
1. Especifique as propriedades necessárias para a impressora.
1. Selecione Imprimir e aguarde até que a caixa de diálogo Salvar como seja exibida. A caixa de diálogo Salvar como é necessária para que o serviço Gerar PDF especifique o destino do arquivo PDF.

#### Identificação das caixas de diálogo especificadas nos atributos da legenda {#identifying-the-dialogs-specified-in-caption-attributes}

Use o Microsoft Spy++ para obter as identidades das propriedades de elementos de janela no aplicativo nativo. Você deve ter essas identidades para escrever scripts.

#### Uso de expressões regulares em atributos de legenda {#using-regular-expressions-in-caption-attributes}

É possível usar expressões regulares nas especificações de legenda. O serviço Gerar PDF usa a `java.util.regex.Matcher` classe para suportar expressões regulares. Esse utilitário suporta as expressões regulares descritas em `java.util.regex.Pattern`. (Vá para o site Java em [https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html).)

**expressão regular que acomoda o nome do arquivo prefixado ao Bloco de notas no banner Bloco de notas**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**expressão regular diferenciando Impressão da configuração de impressão**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordenar os elementos window e windowList {#ordering-the-window-and-windowlist-elements}

Você deve ordenar `window` e `windowList` os elementos da seguinte maneira:

* Quando vários `window` elementos aparecem como filhos em um `windowList` elemento ou `dialog` , ordene esses `window` elementos em ordem decrescente, com os comprimentos dos `caption` nomes indicando a posição na ordem.
* Quando vários `windowList` elementos aparecerem em um `window` elemento, ordene esses `windowList` elementos em ordem decrescente, com os comprimentos dos `caption` atributos do primeiro `indexes/`elemento indicando a posição na ordem.

**Ordenar elementos da janela em um arquivo de diálogo**

```as3
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**Ordenação de elementos de janela em um elemento windowList**

```as3
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### Criação ou modificação de um arquivo XML de diálogo adicional para um aplicativo nativo {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Se você criar um script para um aplicativo nativo que não era suportado anteriormente, também deverá criar um arquivo XML de diálogo adicional para esse aplicativo. Cada aplicativo nativo que o AppMon usa deve ter apenas um arquivo XML de diálogo adicional. O arquivo XML da caixa de diálogo adicional é necessário mesmo se nenhuma caixa de diálogo não solicitada for esperada. A caixa de diálogo adicional deve ter pelo menos um `window` elemento, mesmo que esse `window` elemento seja apenas um espaço reservado.

>[!NOTE]
>
>Neste contexto, o termo adicional significa o conteúdo do arquivo `appmon.[applicationname].addition.[locale]`.xml. Esse arquivo especifica substituições e adições ao arquivo XML de diálogo.

Você também pode modificar o arquivo XML de diálogo adicional para um aplicativo nativo para esses fins:

* Substituição do arquivo XML de diálogo para um aplicativo com uma resposta diferente
* Para adicionar uma resposta a uma caixa de diálogo que não é abordada no arquivo XML de diálogo desse aplicativo

O nome do arquivo que identifica um arquivo dialogXML adicional é `appmon.[appname].addition.[locale].xml`. Um exemplo é appmon.excel.add.en_US.xml.

O nome do arquivo XML da caixa de diálogo adicional deve usar o formato `appmon.[applicationname].addition.[locale].xml`, no qual o nome do *aplicativo* deve corresponder exatamente ao nome do aplicativo usado no arquivo de configuração XML e no script.

>[!NOTE]
>
>Nenhum dos aplicativos genéricos especificados no arquivo de configuração native2pdfconfig.xml tem um arquivo XML de diálogo primário. A seção [Adicionar ou modificar o suporte para um formato](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) de arquivo nativo descreve essas especificações.

Você deve ordenar `windowList` elementos que aparecem como filhos em um `window` elemento. (Consulte [Ordenar os elementos](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)window e windowList.)

### Modificação do arquivo XML da caixa de diálogo geral {#modifying-the-general-dialog-xml-file}

É possível modificar o arquivo XML da caixa de diálogo geral para responder às caixas de diálogo geradas pelo sistema ou para responder às caixas de diálogo comuns a vários aplicativos.

#### Adicionar uma entrada de tipo de arquivo no arquivo de configuração XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

Este procedimento explica como atualizar o arquivo de configuração do serviço Gerar PDF para associar tipos de arquivos a aplicativos nativos. Para atualizar esse arquivo de configuração, é necessário usar o console de administração para exportar os dados de configuração para um arquivo. O nome de arquivo padrão para os dados de configuração é native2pdfconfig.xml.

**Atualizar o arquivo de configuração Gerar serviço PDF**

1. Selecione **Início** > **Serviços** > **Adobe PDF Generator** > Arquivos **** de configuração e selecione **Exportar configuração**.
1. Modifique o `filetype-settings` elemento no arquivo native2pdfconfig.xml, conforme necessário.
1. Selecione **Início** > **Serviços** > **Adobe PDF Generator** > Arquivos **** de configuração e selecione **Importar configuração**. Os dados de configuração são importados para o serviço Gerar PDF, substituindo as configurações anteriores.

>[!NOTE]
>
>O nome do aplicativo é especificado como o valor do atributo do `GenericApp` elemento `name` . Esse valor deve corresponder exatamente ao nome correspondente especificado no script que você desenvolve para esse aplicativo. Da mesma forma, o `GenericApp` atributo do elemento `displayName` deve corresponder exatamente à legenda da `expectedWindow` janela do script correspondente. Essa equivalência é avaliada após a resolução de quaisquer expressões regulares que aparecem nos atributos `displayName` ou `caption` .

Neste exemplo, os dados de configuração padrão fornecidos com o serviço Gerar PDF foram modificados para especificar que o Bloco de notas (não o Microsoft Word) deve ser usado para processar arquivos com a extensão de nome de arquivo .txt. Antes dessa modificação, o Microsoft Word era especificado como o aplicativo nativo que deveria processar esses arquivos.

**Modificações para direcionar arquivos de texto para o Bloco de notas (native2pdfconfig.xml)**

```as3
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### Criação de uma variável de ambiente para localizar o aplicativo nativo {#creating-an-environment-variable-to-locate-the-native-application}

Crie uma variável de ambiente que especifique o local do executável do aplicativo nativo. A variável deve usar o formato `[applicationname]_PATH`, no qual o *nome* do aplicativo deve corresponder exatamente ao nome do aplicativo usado no arquivo de configuração XML e no script, e no qual o caminho contém o caminho para o executável entre aspas de duplo. Um exemplo dessa variável de ambiente é `Photoshop_PATH`.

Depois de criar a nova variável de ambiente, você deve reiniciar o servidor no qual o serviço Gerar PDF está implantado.

**Criar uma variável do sistema no ambiente do Windows XP**

1. Selecione **Painel de controle > Sistema**.
1. Na caixa de diálogo Propriedades do sistema, clique na guia **Avançado** e, em seguida, clique em Variáveis **de** Ambiente.
1. Em Variáveis do sistema na caixa de diálogo Variáveis de Ambiente, clique em **Novo**.
1. Na caixa de diálogo Nova variável do sistema, na caixa Nome **da** variável, digite um nome que use o formato `[applicationname]_PATH`.
1. Na caixa Valor **da** variável, digite o caminho completo e o nome do arquivo executável do aplicativo e clique em **OK**. For example, type: `c:\windows\Notepad.exe`
1. Na caixa de diálogo Variáveis de Ambiente, clique em **OK**.

**Criar uma variável do sistema a partir da linha de comando**

1. Em uma janela de linha de comando, digite a definição da variável, usando este formato:

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   For example, type: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Start um novo prompt de linha de comando para a variável do sistema entrar em vigor.

#### Arquivos XML {#xml-files}

O AEM Forms inclui arquivos XML de amostra que fazem com que o serviço Gerar PDF use o Bloco de notas para processar quaisquer arquivos com a extensão de nome de arquivo .txt. Este código está incluído nesta seção. Além disso, você deve fazer as outras modificações descritas nesta seção.

#### Arquivo XML de diálogo adicional {#additional-dialog-xml-file}

Este exemplo contém as caixas de diálogo adicionais para o aplicativo Bloco de notas. Essas caixas de diálogo podem ser adicionadas às especificadas pelo serviço Gerar PDF.

**Caixas de diálogo do Bloco de notas(appmon.notpad.add.en_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### Arquivo XML de script {#script-xml-file}

Este exemplo especifica como o serviço Gerar PDF deve interagir com o Bloco de notas para imprimir arquivos usando a impressora Adobe PDF.

**Arquivo XML de script do Bloco de notas (appmon.notepad.script.en_US.xml)**

```as3
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```

