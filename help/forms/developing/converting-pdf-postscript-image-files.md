---
title: Conversão de PDF em arquivos Postscript e de imagem
description: Use o serviço Converter PDF para converter documentos PDF para PostScript e para vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF) usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# Conversão de PDF para arquivos Postscript e de imagem {#converting-pdf-to-postscript-andimage-files}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço Converter PDF**

O serviço Convert PDF converte documentos PDF para PostScript e para vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para impressão autônoma baseada em servidor em qualquer impressora PostScript. A conversão de um documento de PDF em um arquivo de TIFF de várias páginas é prática ao arquivar documentos em sistemas de gerenciamento de conteúdo que não sejam compatíveis com documentos de PDF.

Você pode realizar essas tarefas usando o serviço Converter PDF:

* Converta documentos PDF em PostScript.
* Converta documentos PDF em formatos de imagem.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos PDF para PostScript {#converting-pdf-documents-to-postscript}

Este tópico descreve como você pode usar a API de serviço Converter PDF (Java e serviço Web) para converter programaticamente documentos PDF em arquivos PostScript. O documento PDF que é convertido em um arquivo PostScript deve ser um documento PDF não interativo. Ou seja, se você tentar converter um documento PDF interativo em um arquivo PostScript, ocorrerá uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um arquivo PostScript, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente do serviço Convert PDF.
1. Consulte o documento PDF para converter em um arquivo PostScript.
1. Definir opções de tempo de execução de conversão.
1. Converta o documento PDF em um arquivo PostScript.
1. Salve o arquivo do PostScript.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de serviço Converter PDF, você deve criar um cliente de serviço Converter PDF. Se você estiver usando a API Java, crie um objeto `ConvertPdfServiceClient`. Se você estiver usando a API de serviço Web, crie um objeto `ConvertPDFServiceService`.

Esta seção usa a funcionalidade de serviço Web introduzida no AEM Forms. Para acessar uma nova funcionalidade, é necessário construir o objeto proxy usando o atributo `lc_version`. (Consulte &quot;Acessando nova funcionalidade usando serviços Web&quot; em [Chamando o AEM Forms usando Serviços Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Referencie o documento PDF a ser convertido em um arquivo PostScript**

Referencie o documento PDF que você deseja converter em um arquivo PostScript. Conforme dito anteriormente neste tópico, o documento PDF deve ser um documento PDF não interativo. Se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

**Definir opções de tempo de execução de conversão**

Ao converter um documento PDF em um arquivo PostScript, você pode definir opções de tempo de execução que especifiquem o tipo de PostScript criado. Por exemplo, você pode definir um arquivo PostScript de nível 3.

Normalmente, o arquivo PostScript gerado refletirá o tamanho do documento PDF de entrada. Se você selecionar a opção `ShrinkToFit` (que reduz a saída do arquivo PostScript para caber na página), você não verá uma diferença entre o documento PDF de entrada e o arquivo PostScript gerado. A opção `ShrinkToFit` só terá efeito se você optar por imprimir em um tamanho de página menor do que o documento PDF de entrada. Para selecionar uma página menor, defina a opção `PageSize`. Além disso, é recomendável que você defina a opção `RotateAndCenter` como `true` para obter a saída de PostScript correta.

Da mesma forma, se você selecionar a opção `ExpandToFit` (que expande a saída do arquivo PostScript para caber na página), ela só terá efeito se você optar por imprimir em um tamanho de página maior que o documento PDF de entrada. Para selecionar uma página maior, defina a opção `PageSize`. Além disso, é recomendável que você defina a opção `RotateAndCenter` como `true` para obter a saída de PostScript correta.

>[!NOTE]
>
>Para obter informações sobre os valores de tempo de execução que você pode definir, consulte a referência de classe `ToPSOptionsSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o documento PDF em um arquivo PostScript**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, você pode chamar a operação de conversão do PostScript. Esta operação precisará de informações sobre o documento a ser convertido, incluindo o nível de PostScript preferido para o documento de destino.

**Salvar o arquivo do PostScript**

Depois de converter o documento PDF em PostScript, você pode salvar a saída como um arquivo PostScript.

**Consulte também**

[Converter um documento PDF em PS usando a API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Converter um documento PDF em PS usando a API do serviço Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da conversão da API de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em PS usando a API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Converta um documento PDF em PostScript usando a API de serviço de conversão de PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte o documento PDF para converter em um arquivo PostScript.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e passe um valor de cadeia de caracteres que especifique o local do documento PDF a ser convertido.
   * Crie um objeto `com.adobe.idp.Document` que armazene o documento PDF usando o construtor `com.adobe.idp.Document`. Transmita o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Definir opções de tempo de execução de conversão.

   * Crie um objeto `ToPSOptionsSpec` invocando seu construtor.
   * Defina as opções de tempo de execução invocando um método apropriado que pertença ao objeto `ToPSOptionsSpec`. Por exemplo, para definir o nível PostScript que é criado, chame o método `setPsLevel` do objeto `ToPSOptionsSpec` e passe um valor de enumeração `PSLevel` que especifique o nível PostScript. Para obter informações sobre todos os valores de tempo de execução que você pode definir, consulte a referência de classe `ToPSOptionsSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converta o documento PDF em um arquivo PostScript.

   Invoque o método `toPS2` do `ConvertPdfServiceClient`objeto e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser convertido em um arquivo PostScript.
   * Um objeto `ToPSOptionsSpec` que especifica as opções de tempo de execução do PostScript.

   O método `toPS2` retorna um objeto `Document` que contém o novo documento do PostScript.

1. Salve o arquivo do PostScript.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .ps.
   * Invoque o método `copyToFile` do objeto `Document` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `toPS2`).

**Consulte também**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Início rápido (modo SOAP): conversão de um documento PDF em PostScript usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento PDF em PS usando a API do serviço Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Converta um documento PDF em PostScript usando a API de serviço de conversão de PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um objeto `ConvertPdfServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Você não precisa usar o atributo `lc_version`. No entanto, especifique `?blob=mtom`.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ConvertPdfServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte o documento PDF para converter em um arquivo PostScript.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que é convertido em um arquivo PostScript.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser convertido e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de conversão.

   * Crie um objeto `ToPSOptionsSpec` invocando seu construtor.
   * Defina as opções de tempo de execução atribuindo um valor ao membro de dados do objeto `ToPSOptionsSpec`. Por exemplo, para definir o nível de PostScript que é criado, atribua um valor de enumeração `PSLevel` ao membro de dados `psLevel` do objeto `ToPSOptionsSpec`.

1. Converta o documento PDF em um arquivo PostScript.

   Invoque o método `toPS2` do objeto `GeneratePDFServiceService` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser convertido em um arquivo PostScript
   * Um objeto `ToPSOptionsSpec` que especifica as opções de tempo de execução

   Após a conclusão da conversão, extraia os dados binários que representam o documento do PostScript acessando a propriedade `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PostScript.

1. Salve o arquivo do PostScript.

   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo PS.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `encryptPDFUsingPassword`. Popular a matriz de bytes obtendo o valor do campo `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes no arquivo PostScript chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversão de documentos PDF em formatos de imagem {#converting-pdf-documents-to-image-formats}

Você pode usar o serviço Converter PDF para converter programaticamente documentos PDF para formatos de imagem, que incluem JPEG, JPEG 2000, TIFF e PNG. Ao converter um documento PDF em um arquivo de imagem, você pode usar o documento PDF como um arquivo de imagem. Por exemplo, você pode colocar a imagem em um sistema de gerenciamento de conteúdo corporativo para armazenamento.

Ao converter um documento PDF em uma imagem, o serviço Converter PDF cria uma imagem separada para cada página no documento. Ou seja, se o documento tiver 20 páginas, o serviço Converter PDF criará 20 arquivos de imagem. Ao converter um documento PDF em um formato de imagem, você pode criar imagens individuais para cada página dentro do documento PDF ou um único arquivo de imagem para todo o documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento PDF em qualquer um dos tipos suportados, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente do serviço Convert PDF.
1. Recupere o documento PDF para converter.
1. Definir opções de tempo de execução.
1. Converta o PDF em uma imagem.
1. Recupera os arquivos de imagem de uma coleção.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de serviço Converter PDF, você deve criar um cliente de serviço Converter PDF. Se você estiver usando a API Java, crie um objeto `ConvertPdfServiceClient`. Se você estiver usando a API de serviço Web, crie um objeto `ConvertPDFServiceService`.

**Recuperar o documento PDF para converter**

Recupere o documento PDF para converter em uma imagem. Não é possível converter um documento PDF interativo em uma imagem. Se você tentar fazer isso, uma exceção será lançada. Para converter um documento PDF interativo em um arquivo de imagem, é necessário nivelar o documento PDF antes de convertê-lo. (Consulte [Nivelando Documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Definir opções de tempo de execução**

Defina opções de tempo de execução, como o formato da imagem e os valores de resolução. Para obter informações sobre os valores de tempo de execução, consulte a referência de classe `ToImageOptionsSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o PDF em uma imagem**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, você pode converter o documento PDF em uma imagem. Um objeto de coleção que contém as imagens é retornado.

**Recuperar os arquivos de imagem de uma coleção**

Você pode recuperar arquivos de imagem de um objeto de coleção que o serviço Converter PDF retorna. Cada elemento na coleção é uma instância `com.adobe.idp.Document` (ou uma instância `BLOB`, se você estiver usando serviços da Web) que você pode salvar como um arquivo de imagem, como um arquivo JPG.

O formato do arquivo de imagem depende da opção de tempo de execução `ImageConvertFormat`. Ou seja, se você definir a opção de tempo de execução `ImageConvertFormat` como `ImageConvertFormat.JPEG`, poderá salvar arquivos de imagem como arquivos de JPG.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da conversão da API de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em arquivos de imagem usando a API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Converta um documento PDF em um formato de imagem usando a API de serviço Converter PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o documento PDF para converter.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução.

   * Crie um objeto `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o método `setImageConvertFormat` e transmitindo um valor enum `ImageConvertFormat` que especifica o tipo de formato.

   >[!NOTE]
   >
   >A configuração do valor de enumeração `ImageConvertFormat` é obrigatória.

1. Converta o PDF em uma imagem.

   Invoque o método `toImage2` do objeto `ConvertPdfServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o arquivo PDF a ser convertido.
   * Um objeto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contém as várias preferências sobre o formato de imagem de destino.

   O método `toImage2` retorna um objeto `java.util.List` que contém imagens. Cada elemento na coleção é uma instância `com.adobe.idp.Document`.

1. Recupera os arquivos de imagem de uma coleção.

   Repita através do objeto `java.util.List` para determinar se as imagens estão presentes. Cada elemento é uma instância `com.adobe.idp.Document`. Salve a imagem invocando o método `copyToFile` do objeto `com.adobe.idp.Document` e transmitindo um objeto `java.io.File`.

**Consulte também**

[Início rápido (modo SOAP): conversão de um documento PDF em arquivos JPEG usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Converter um documento PDF em arquivos de imagem usando a API do serviço Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converta um documento PDF em um formato de imagem usando a API de serviço de conversão de PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF de conversão.

   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um objeto `ConvertPdfServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Você não precisa usar o atributo `lc_version`. No entanto, especifique `?blob=mtom`.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ConvertPdfServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF para converter.

   * Crie um objeto `BLOB` usando seu construtor. Este objeto `BLOB` é usado para armazenar o formulário PDF.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que especifique o local do formulário de PDF e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Determine o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Crie um objeto `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o método `setImageConvertFormat` e transmitindo um valor de enumeração `ImageConvertFormat` que especifica o tipo de formato.

   >[!NOTE]
   >
   >A configuração do valor de enumeração `ImageConvertFormat` é obrigatória.

1. Converta o PDF em uma imagem.

   Invoque o método `toImage2` do objeto `ConvertPDFServiceService` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o arquivo a ser convertido
   * Um objeto `ToImageOptionsSpec` que contém as várias preferências sobre o formato de imagem de destino

   O método `toImage2` retorna um objeto `MyArrayOfBLOB` que contém os arquivos de imagem recém-criados.

1. Recupera os arquivos de imagem de uma coleção.

   * Determine o número de elementos no objeto `MyArrayOfBLOB` obtendo o valor de seu campo `Count`. Cada elemento é um objeto `BLOB` que contém a imagem.
   * Repita através do objeto `MyArrayOfBLOB` e salve cada arquivo de imagem.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
