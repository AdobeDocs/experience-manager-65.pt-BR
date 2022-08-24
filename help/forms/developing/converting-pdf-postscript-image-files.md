---
title: Conversão do PDF para Postscript e arquivos de imagem
seo-title: Converting PDF to Postscript andImage Files
description: Use o serviço Convert PDF para converter documentos do PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF) usando a API do Java e a API do serviço da Web.
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2809'
ht-degree: 0%

---

# Conversão do PDF para Postscript e arquivos de imagem {#converting-pdf-to-postscript-andimage-files}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço Converter PDF**

O serviço Convert PDF converte documentos PDF para PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para a impressão automática baseada em servidor em qualquer impressora PostScript. A conversão de um documento PDF em um arquivo TIFF de várias páginas é prática para arquivar documentos em sistemas de gerenciamento de conteúdo que não oferecem suporte a documentos PDF.

Você pode realizar essas tarefas usando o serviço Converter PDF:

* Converta documentos PDF para PostScript.
* Converta documentos PDF em formatos de imagem.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos PDF para PostScript {#converting-pdf-documents-to-postscript}

Este tópico descreve como você pode usar a API Converter serviço de PDF (Java e serviço da Web) para converter programaticamente documentos do PDF em arquivos PostScript. O documento PDF convertido em um arquivo PostScript deve ser um documento PDF não interativo. Ou seja, se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um arquivo PostScript, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço Converter PDF.
1. Faça referência ao documento PDF para conversão em um arquivo PostScript.
1. Defina as opções de tempo de execução da conversão.
1. Converta o documento PDF em um arquivo PostScript.
1. Salve o arquivo PostScript.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDF de conversão**

Antes de executar programaticamente uma operação Convert PDF Service, você deve criar um cliente Convert PDF Service . Se estiver usando a API do Java, crie um `ConvertPdfServiceClient` objeto. Se estiver usando a API do serviço da Web, crie um `ConvertPDFServiceService` objeto.

Esta seção usa a funcionalidade de serviço da Web introduzida no AEM Forms. Para acessar a nova funcionalidade, é necessário construir o objeto proxy usando o `lc_version` atributo. (Consulte &quot;Acesso a nova funcionalidade usando serviços da Web&quot; em [Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Referência ao documento do PDF para converter em um arquivo PostScript**

Faça referência ao documento PDF que você deseja converter em um arquivo PostScript. Como mencionado anteriormente neste tópico, o documento PDF deve ser um documento PDF não interativo. Se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

**Definir opções de tempo de execução de conversão**

Ao converter um documento PDF em um arquivo PostScript, você pode definir opções de tempo de execução que especificam o tipo PostScript que é criado. Por exemplo, você pode definir um arquivo PostScript de nível 3.

Normalmente, o arquivo PostScript gerado reflete o tamanho do documento PDF de entrada. Se você selecionar a variável `ShrinkToFit` (que reduz a saída do arquivo PostScript para ajustá-la à página), você não verá uma diferença entre o documento PDF de entrada e o arquivo PostScript gerado. O `ShrinkToFit` A opção entrará em vigor somente se você optar por imprimir em um tamanho de página menor que o documento PDF de entrada. Para selecionar um tamanho de página menor, defina a variável `PageSize` opção. Além disso, é recomendável definir a variável `RotateAndCenter` para `true` para obter a saída correta do PostScript.

Da mesma forma, se você selecionar a variável `ExpandToFit` (que expande a saída do arquivo PostScript para ajustá-la à página), ela só terá efeito se você optar por imprimir em um tamanho de página maior que o documento PDF de entrada. Para selecionar um tamanho de página maior, defina o `PageSize` opção. Além disso, é recomendável definir a variável `RotateAndCenter` para `true` para obter a saída correta do PostScript.

>[!NOTE]
>
>Para obter informações sobre os valores de tempo de execução que você pode definir, consulte o `ToPSOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o documento PDF em um arquivo PostScript**

Depois de criar o cliente do serviço e definir as opções de tempo de execução, você pode chamar a operação de conversão de PostScript. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o nível de PostScript preferencial para o documento de destino.

**Salvar o arquivo PostScript**

Depois de converter o documento PDF para PostScript, é possível salvar a saída como um arquivo PostScript.

**Consulte também**

[Converter um documento do PDF em PS usando a API do Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Converter um documento do PDF em PS usando a API de serviço da Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inícios rápidos da API de conversão de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento do PDF em PS usando a API do Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Converta um documento do PDF em PostScript usando a API Convert PDF Service (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Convert PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `ConvertPdfServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência ao documento PDF para conversão em um arquivo PostScript.

   * Crie um `java.io.FileInputStream` usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF para conversão.
   * Crie um `com.adobe.idp.Document` objeto que armazena o documento PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Defina as opções de tempo de execução da conversão.

   * Crie um `ToPSOptionsSpec` chamando seu construtor.
   * Defina as opções de tempo de execução chamando um método apropriado que pertença ao `ToPSOptionsSpec` objeto. Por exemplo, para definir o nível PostScript criado, chame a função `ToPSOptionsSpec` do objeto `setPsLevel` e passe um `PSLevel` valor de enumeração que especifica o nível de PostScript. Para obter informações sobre todos os valores de tempo de execução que você pode definir, consulte o `ToPSOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converta o documento PDF em um arquivo PostScript.

   Chame o `ConvertPdfServiceClient`do objeto `toPS2` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF para converter em um arquivo PostScript.
   * A `ToPSOptionsSpec` objeto que especifica as opções de tempo de execução do PostScript.

   O `toPS2` método retorna um `Document` objeto que contém o novo documento PostScript.

1. Salve o arquivo PostScript.

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .ps.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` para o arquivo (certifique-se de usar a variável `Document` objeto retornado pelo `toPS2` método ).

**Consulte também**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Início rápido (modo SOAP): Conversão de um documento do PDF para PostScript usando a API do Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento do PDF em PS usando a API de serviço da Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Converta um documento do PDF em PostScript usando a API Convert PDF Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Convert PDF.

   * Crie um `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um `ConvertPdfServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `ConvertPdfServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência ao documento PDF para conversão em um arquivo PostScript.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF convertido em um arquivo PostScript.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser convertido e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução da conversão.

   * Crie um `ToPSOptionsSpec` chamando seu construtor.
   * Defina as opções de tempo de execução atribuindo um valor à variável `ToPSOptionsSpec` membro de dados do objeto. Por exemplo, para definir o nível de PostScript criado, atribua uma `PSLevel` valor de enumeração para a `ToPSOptionsSpec` do objeto `psLevel` membro de dados.

1. Converta o documento PDF em um arquivo PostScript.

   Chame o `GeneratePDFServiceService` do objeto `toPS2` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF para converter em um arquivo PostScript
   * A `ToPSOptionsSpec` objeto que especifica as opções de tempo de execução

   Após a conclusão da conversão, extraia os dados binários que representam o documento PostScript acessando sua `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que pode ser gravada em um arquivo PostScript.

1. Salve o arquivo PostScript.

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo PS.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingPassword` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` campo.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo PostScript chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Converter documentos do PDF em formatos de imagem {#converting-pdf-documents-to-image-formats}

Você pode usar o serviço Converter PDF para converter programaticamente documentos PDF em formatos de imagem, que incluem JPEG, JPEG 2000, TIFF e PNG. Ao converter um documento PDF em um arquivo de imagem, você pode usar o documento PDF como um arquivo de imagem. Por exemplo, você pode colocar a imagem em um sistema de gerenciamento de conteúdo corporativo para armazenamento.

Ao converter um documento PDF para uma imagem, o serviço Converter PDF cria uma imagem separada para cada página no documento. Ou seja, se o documento tiver 20 páginas, o serviço Converter PDF criará 20 arquivos de imagem. Ao converter um documento PDF para um formato de imagem, você pode criar imagens individuais para cada página no documento PDF ou um único arquivo de imagem para todo o documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento PDF em qualquer um dos tipos suportados, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço Converter PDF.
1. Recupere o documento PDF para converter.
1. Defina as opções de tempo de execução.
1. Converta a PDF em uma imagem.
1. Recupere os arquivos de imagem de uma coleção.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDF de conversão**

Antes de executar programaticamente uma operação Convert PDF Service, você deve criar um cliente Convert PDF Service . Se estiver usando a API do Java, crie um `ConvertPdfServiceClient` objeto. Se estiver usando a API do serviço da Web, crie um `ConvertPDFServiceService` objeto.

**Recuperar o documento do PDF para converter**

Você deve recuperar o documento PDF para converter em uma imagem. Não é possível converter um documento PDF interativo em uma imagem. Se você tentar fazer isso, uma exceção será lançada. Para converter um documento PDF interativo em um arquivo de imagem, você deve nivelar o documento PDF antes de convertê-lo. (Consulte [Nivelar documentos do PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Definir opções de tempo de execução**

Você deve definir opções de tempo de execução, como o formato da imagem e os valores de resolução. Para obter informações sobre os valores de tempo de execução, consulte o `ToImageOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter a PDF em uma imagem**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, é possível converter o documento do PDF em uma imagem. Um objeto de coleção que contém as imagens é retornado.

**Recuperar os arquivos de imagem de uma coleção**

Você pode recuperar arquivos de imagem de um objeto de coleção retornado pelo serviço Convert PDF. Cada elemento na coleção é um `com.adobe.idp.Document` instância (ou uma `BLOB` Se você estiver usando serviços da Web), é possível salvar como um arquivo de imagem, como um arquivo de JPG.

O formato do arquivo de imagem depende do `ImageConvertFormat` opção de tempo de execução. Ou seja, se você definir a variável `ImageConvertFormat` opção de tempo de execução para `ImageConvertFormat.JPEG`, é possível salvar arquivos de imagem como arquivos JPG.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inícios rápidos da API de conversão de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento do PDF em arquivos de imagem usando a API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Converta um documento do PDF em um formato de imagem usando a API do serviço Convert PDF (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Convert PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `ConvertPdfServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere o documento PDF para converter.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para converter usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução.

   * Crie um `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando a função `setImageConvertFormat` e a transmissão de um `ImageConvertFormat` valor enum que especifica o tipo de formato.

   >[!NOTE]
   >
   >Definir a `ImageConvertFormat` o valor de enumeração é obrigatório.

1. Converta a PDF em uma imagem.

   Chame o `ConvertPdfServiceClient` do objeto `toImage2` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o arquivo PDF a ser convertido.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contém as várias preferências sobre o formato de imagem de destino.

   O `toImage2` método retorna um `java.util.List` objeto que contém imagens. Cada elemento na coleção é um `com.adobe.idp.Document` instância.

1. Recupere os arquivos de imagem de uma coleção.

   Iterar por meio do `java.util.List` para determinar se as imagens estão presentes. Cada elemento é um `com.adobe.idp.Document` instância. Salve a imagem chamando o `com.adobe.idp.Document` do objeto `copyToFile` e a transmissão de um `java.io.File` objeto.

**Consulte também**

[Início rápido (modo SOAP): Conversão de um documento do PDF em arquivos JPEG usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Converter um documento do PDF em arquivos de imagem usando a API do serviço da Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converta um documento do PDF em um formato de imagem usando a API Convert PDF Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente PDF de conversão.

   * Crie um `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um `ConvertPdfServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `ConvertPdfServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF para converter.

   * Crie um `BLOB` usando seu construtor. Essa `BLOB` é usado para armazenar o formulário PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando a função `setImageConvertFormat` e a transmissão de um `ImageConvertFormat` valor de enumeração que especifica o tipo de formato.

   >[!NOTE]
   >
   >Definir a `ImageConvertFormat` o valor de enumeração é obrigatório.

1. Converta a PDF em uma imagem.

   Chame o `ConvertPDFServiceService` do objeto `toImage2` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o arquivo a ser convertido
   * A `ToImageOptionsSpec` objeto que contém as várias preferências sobre o formato de imagem de destino

   O `toImage2` método retorna um `MyArrayOfBLOB` objeto que contém os arquivos de imagem recém-criados.

1. Recupere os arquivos de imagem de uma coleção.

   * Determine o número de elementos no `MyArrayOfBLOB` obtendo o valor de sua `Count` campo. Cada elemento é um `BLOB` objeto que contém a imagem.
   * Iterar por meio do `MyArrayOfBLOB` e salve cada arquivo de imagem.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
