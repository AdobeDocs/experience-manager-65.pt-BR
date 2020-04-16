---
title: Converter PDF em arquivos Postscript e Imagem
seo-title: Converter PDF em arquivos Postscript e Imagem
description: 'null'
seo-description: 'null'
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Converter PDF em arquivos Postscript e de imagem {#converting-pdf-to-postscript-andimage-files}

**Sobre o serviço Converter PDF**

O serviço Convert PDF converte documentos PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para a impressão automática baseada em servidor em qualquer impressora PostScript. A conversão de um documento PDF em um arquivo TIFF de várias páginas é prática ao arquivar documentos em sistemas de gestão de conteúdo que não suportam documentos PDF.

É possível realizar essas tarefas usando o serviço Converter PDF:

* Converta documentos PDF em PostScript.
* Converta documentos PDF em formatos de imagem.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Converter Documentos PDF em PostScript {#converting-pdf-documents-to-postscript}

Este tópico descreve como você pode usar a Converter API do serviço PDF (Java e serviço da Web) para converter programaticamente documentos PDF em arquivos PostScript. O documento PDF convertido em um arquivo PostScript deve ser um documento PDF não interativo. Ou seja, se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um arquivo PostScript, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Converter PDF.
1. Faça referência ao documento PDF para converter em um arquivo PostScript.
1. Defina as opções de tempo de execução de conversão.
1. Converta o documento PDF em um arquivo PostScript.
1. Salve o arquivo PostScript.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de serviço Converter PDF, é necessário criar um cliente de serviço Converter PDF. Se você estiver usando a API Java, crie um `ConvertPdfServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `ConvertPDFServiceService` objeto.

Esta seção usa a funcionalidade de serviço da Web introduzida no AEM Forms. Para acessar a nova funcionalidade, é necessário construir o objeto proxy usando o `lc_version` atributo. (Consulte &quot;Acessar novas funcionalidades usando serviços da Web&quot; em [Invocar formulários AEM usando serviços](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)da Web.)

**Referência ao documento PDF a ser convertido em um arquivo PostScript**

Faça referência ao documento PDF que você deseja converter em um arquivo PostScript. Como mencionado anteriormente neste tópico, o documento PDF deve ser um documento PDF não interativo. Se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

**Definir opções de tempo de execução de conversão**

Ao converter um documento PDF em um arquivo PostScript, é possível definir opções de tempo de execução que especificam o tipo PostScript criado. Por exemplo, você pode definir um arquivo PostScript nível 3.

Normalmente, o arquivo PostScript gerado refletirá o tamanho do documento PDF de entrada. Se você selecionar a `ShrinkToFit` opção (que reduz a saída do arquivo PostScript para se ajustar à página), você não verá uma diferença entre o documento PDF de entrada e o arquivo PostScript gerado. A `ShrinkToFit` opção só terá efeito se você optar por imprimir em um tamanho de página menor do que o documento PDF de entrada. Para selecionar um tamanho de página menor, defina a `PageSize` opção. Além disso, é recomendável definir a `RotateAndCenter` opção para obter `true` a saída PostScript correta.

Da mesma forma, se você selecionar a `ExpandToFit` opção (que expande a saída do arquivo PostScript para se ajustar à página), ela entrará em vigor somente se você optar por imprimir em um tamanho de página maior que o documento PDF de entrada. Para selecionar um tamanho de página maior, defina a `PageSize` opção. Além disso, é recomendável definir a `RotateAndCenter` opção para obter `true` a saída PostScript correta.

>[!NOTE]
>
>Para obter informações sobre os valores de tempo de execução que podem ser definidos, consulte a referência de `ToPSOptionsSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Converter o documento PDF em um arquivo PostScript**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, você pode chamar a operação de conversão PostScript. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o nível PostScript preferencial para o documento do público alvo.

**Salvar o arquivo PostScript**

Depois de converter o documento PDF em PostScript, é possível salvar a saída como um arquivo PostScript.

**Consulte também:**

[Converter um documento PDF em PS usando a API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Converter um documento PDF em PS usando a API de serviço da Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converter Start rápidos da API do serviço PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em PS usando a API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Converta um documento PDF em PostScript usando a API Converter serviço PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente Converter PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `ConvertPdfServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência ao documento PDF para converter em um arquivo PostScript.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmita um valor de string que especifica o local do documento PDF a ser convertido.
   * Crie um `com.adobe.idp.Document` objeto que armazene o documento PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Defina as opções de tempo de execução de conversão.

   * Crie um `ToPSOptionsSpec` objeto chamando seu construtor.
   * Defina as opções de tempo de execução chamando um método apropriado que pertence ao `ToPSOptionsSpec` objeto. Por exemplo, para definir o nível PostScript que é criado, chame o método do `ToPSOptionsSpec` objeto `setPsLevel` e transmita um valor de `PSLevel` lista discriminada que especifique o nível PostScript. Para obter informações sobre todos os valores de tempo de execução que podem ser definidos, consulte a referência de `ToPSOptionsSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Converta o documento PDF em um arquivo PostScript.

   Chame o método do `ConvertPdfServiceClient`objeto `toPS2` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o documento PDF a ser convertido em um arquivo PostScript.
   * Um `ToPSOptionsSpec` objeto que especifica opções de tempo de execução PostScript.
   O `toPS2` método retorna um `Document` objeto que contém o novo documento PostScript.

1. Salve o arquivo PostScript.

   * Crie um `java.io.File` objeto e verifique se a extensão do nome do arquivo é .ps.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `toPS2` método).

**Consulte também:**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Start rápido (modo SOAP): Converter um documento PDF em PostScript usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento PDF em PS usando a API de serviço da Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Converta um documento PDF em PostScript usando a API Converter serviço PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Converter PDF.

   * Crie um `ConvertPdfServiceClient` objeto usando seu construtor padrão.
   * Crie um `ConvertPdfServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `ConvertPdfServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência ao documento PDF para converter em um arquivo PostScript.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF convertido em um arquivo PostScript.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser convertido e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução de conversão.

   * Crie um `ToPSOptionsSpec` objeto chamando seu construtor.
   * Defina as opções de tempo de execução atribuindo um valor ao membro de dados do `ToPSOptionsSpec` objeto. Por exemplo, para definir o nível PostScript criado, atribua um valor de `PSLevel` lista discriminada ao membro de `ToPSOptionsSpec` `psLevel` dados do objeto.

1. Converta o documento PDF em um arquivo PostScript.

   Chame o método do `GeneratePDFServiceService` objeto `toPS2` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento PDF a ser convertido em um arquivo PostScript
   * Um `ToPSOptionsSpec` objeto que especifica opções de tempo de execução
   Depois que a conversão for concluída, extraia os dados binários que representam o documento PostScript acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que pode ser gravada em um arquivo PostScript.

1. Salve o arquivo PostScript.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo PS.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingPassword` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo PostScript, chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Converter Documentos PDF em formatos de imagem {#converting-pdf-documents-to-image-formats}

Você pode usar o serviço Converter PDF para converter documentos PDF programaticamente em formatos de imagem, que incluem JPEG, JPEG 2000, TIFF e PNG. Ao converter um documento PDF em um arquivo de imagem, você pode usar o documento PDF como um arquivo de imagem. Por exemplo, você pode colocar a imagem em um sistema de gestão de conteúdo corporativo para armazenamentos.

Ao converter um documento PDF em uma imagem, o serviço Converter PDF cria uma imagem separada para cada página no documento. Ou seja, se o documento tiver 20 páginas, o serviço Converter PDF criará 20 arquivos de imagem. Ao converter um documento PDF em um formato de imagem, é possível criar imagens individuais para cada página dentro do documento PDF ou um único arquivo de imagem para todo o documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento PDF em qualquer um dos tipos suportados, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente de serviço Converter PDF.
1. Recupere o documento PDF a ser convertido.
1. Defina as opções de tempo de execução.
1. Converta o PDF em uma imagem.
1. Recupere os arquivos de imagem de uma coleção.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de serviço Converter PDF, é necessário criar um cliente de serviço Converter PDF. Se você estiver usando a API Java, crie um `ConvertPdfServiceClient` objeto. Se você estiver usando a API de serviço da Web, crie um `ConvertPDFServiceService` objeto.

**Recuperar o documento PDF a ser convertido**

É necessário recuperar o documento PDF para convertê-lo em uma imagem. Não é possível converter um documento PDF interativo em uma imagem. Se você tentar fazer isso, uma exceção é lançada. Para converter um documento PDF interativo em um arquivo de imagem, é necessário nivelar o documento PDF antes de convertê-lo. (Consulte [Achatamento de Documentos](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)PDF.)

**Definir opções de tempo de execução**

É necessário definir opções de tempo de execução, como o formato da imagem e os valores de resolução. Para obter informações sobre os valores de tempo de execução, consulte a referência da `ToImageOptionsSpec` classe em Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Converter o PDF em uma imagem**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, é possível converter o documento PDF em uma imagem. Um objeto de coleção que contém as imagens é retornado.

**Recuperar os arquivos de imagem de uma coleção**

Você pode recuperar arquivos de imagem de um objeto de coleção retornado pelo serviço Converter PDF. Cada elemento na coleção é uma `com.adobe.idp.Document` instância (ou uma `BLOB` instância se você estiver usando serviços da Web) que pode ser salva como um arquivo de imagem, como um arquivo JPG.

O formato do arquivo de imagem depende da opção de tempo de `ImageConvertFormat` execução. Ou seja, se você definir a opção de tempo de `ImageConvertFormat` execução como `ImageConvertFormat.JPEG`, poderá salvar arquivos de imagem como arquivos JPG.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converter Start rápidos da API do serviço PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em arquivos de imagem usando a API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Converta um documento PDF em um formato de imagem usando a API de serviço Converter PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente Converter PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `ConvertPdfServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o documento PDF a ser convertido.

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução.

   * Crie um `ToImageOptionsSpec` objeto usando seu construtor.
   * Chame os métodos que pertencem a esse objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o `setImageConvertFormat` método e transmitindo um valor `ImageConvertFormat` enum que especifique o tipo de formato.
   >[!NOTE]
   >
   >A definição do valor da `ImageConvertFormat` lista discriminada é obrigatória.

1. Converta o PDF em uma imagem.

   Chame o método do `ConvertPdfServiceClient` objeto `toImage2` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o arquivo PDF a ser convertido.
   * Um `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` objeto que contém as várias preferências sobre o formato de imagem do público alvo.
   O `toImage2` método retorna um `java.util.List` objeto que contém imagens. Cada elemento na coleção é uma `com.adobe.idp.Document` instância.

1. Recupere os arquivos de imagem de uma coleção.

   Itere pelo `java.util.List` objeto para determinar se as imagens estão presentes. Cada elemento é uma `com.adobe.idp.Document` instância. Salve a imagem chamando o `com.adobe.idp.Document` método do objeto `copyToFile` e transmitindo um `java.io.File` objeto.

**Consulte também:**

[Start rápido (modo SOAP): Converter um documento PDF em arquivos JPEG usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Converter um documento PDF em arquivos de imagem usando a API de serviço da Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converta um documento PDF em um formato de imagem usando a API Converter serviço PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF de conversão.

   * Crie um `ConvertPdfServiceClient` objeto usando seu construtor padrão.
   * Crie um `ConvertPdfServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar o `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `ConvertPdfServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF a ser convertido.

   * Crie um `BLOB` objeto usando seu construtor. Esse `BLOB` objeto é usado para armazenar o formulário PDF.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `ToImageOptionsSpec` objeto usando seu construtor.
   * Chame os métodos que pertencem a esse objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o `setImageConvertFormat` método e transmitindo um valor de `ImageConvertFormat` lista discriminada que especifique o tipo de formato.
   >[!NOTE]
   >
   >A definição do valor da `ImageConvertFormat` lista discriminada é obrigatória.

1. Converta o PDF em uma imagem.

   Chame o método do `ConvertPDFServiceService` objeto `toImage2` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o arquivo a ser convertido
   * Um `ToImageOptionsSpec` objeto que contém as várias preferências sobre o formato de imagem do público alvo
   O `toImage2` método retorna um `MyArrayOfBLOB` objeto que contém os arquivos de imagem recém-criados.

1. Recupere os arquivos de imagem de uma coleção.

   * Determine o número de elementos no `MyArrayOfBLOB` objeto obtendo o valor de seu `Count` campo. Cada elemento é um `BLOB` objeto que contém a imagem.
   * Iterar pelo `MyArrayOfBLOB` objeto e salvar cada arquivo de imagem.

**Consulte também:**

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
