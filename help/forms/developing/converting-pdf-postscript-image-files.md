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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 0%

---

# Conversão de PDF para arquivos Postscript e de imagem {#converting-pdf-to-postscript-andimage-files}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o serviço de conversão de PDF**

O serviço Convert PDF converte documentos PDF para PostScript e para vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para impressão autônoma baseada em servidor em qualquer impressora PostScript. A conversão de um documento de PDF em um arquivo de TIFF de várias páginas é prática ao arquivar documentos em sistemas de gerenciamento de conteúdo que não sejam compatíveis com documentos de PDF.

Você pode realizar essas tarefas usando o serviço Converter PDF:

* Converta documentos PDF em PostScript.
* Converta documentos PDF em formatos de imagem.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos PDF em PostScript {#converting-pdf-documents-to-postscript}

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
1. Salve o arquivo PostScript.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de serviço Converter PDF, você deve criar um cliente de serviço Converter PDF. Se estiver usando a API Java, crie uma `ConvertPdfServiceClient` objeto. Se estiver usando a API do serviço Web, crie uma `ConvertPDFServiceService` objeto.

Esta seção usa a funcionalidade de serviço Web introduzida no AEM Forms. Para acessar a nova funcionalidade, é necessário construir o objeto proxy usando o `lc_version` atributo. (Consulte &quot;Acessar novas funcionalidades usando serviços da Web&quot; em [Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Referencie o documento PDF a ser convertido em um arquivo PostScript**

Referencie o documento PDF que você deseja converter em um arquivo PostScript. Conforme dito anteriormente neste tópico, o documento PDF deve ser um documento PDF não interativo. Se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

**Definir opções de tempo de execução de conversão**

Ao converter um documento PDF em um arquivo PostScript, você pode definir opções de tempo de execução que especifiquem o tipo PostScript que é criado. Por exemplo, você pode definir um arquivo PostScript nível 3.

Normalmente, o arquivo PostScript gerado refletirá o tamanho do documento PDF de entrada. Se você selecionar a variável `ShrinkToFit` (que reduz a saída do arquivo PostScript para caber na página), você não verá uma diferença entre o documento PDF de entrada e o arquivo PostScript gerado. A variável `ShrinkToFit` A opção só terá efeito se você optar por imprimir em um tamanho de página menor do que o documento PDF de entrada. Para selecionar um tamanho de página menor, defina o `PageSize` opção. Além disso, é recomendável que você defina o `RotateAndCenter` opção para `true` para obter a saída PostScript correta.

Da mesma forma, se você selecionar a variável `ExpandToFit` (que expande a saída do arquivo PostScript para caber na página), só terá efeito se você optar por imprimir em um tamanho de página maior que o documento PDF de entrada. Para selecionar um tamanho de página maior, defina o `PageSize` opção. Além disso, é recomendável que você defina o `RotateAndCenter` opção para `true` para obter a saída PostScript correta.

>[!NOTE]
>
>Para obter informações sobre os valores de tempo de execução que podem ser definidos, consulte `ToPSOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o documento PDF em um arquivo PostScript**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, você pode chamar a operação de conversão PostScript. Esta operação precisará de informações sobre o documento a ser convertido, incluindo o nível de PostScript preferencial para o documento de destino.

**Salve o arquivo PostScript**

Depois de converter o documento PDF em PostScript, você pode salvar a saída como um arquivo PostScript.

**Consulte também**

[Converter um documento PDF em PS usando a API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Converter um documento PDF em PS usando a API do serviço Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da conversão da API de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em PS usando a API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Converta um documento PDF em PostScript usando a API de serviço Converter PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente Converter PDF.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `ConvertPdfServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte o documento PDF para converter em um arquivo PostScript.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF a ser convertido.
   * Criar um `com.adobe.idp.Document` objeto que armazena o documento PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Definir opções de tempo de execução de conversão.

   * Criar um `ToPSOptionsSpec` invocando seu construtor.
   * Defina as opções de tempo de execução chamando um método apropriado que pertença à `ToPSOptionsSpec` objeto. Por exemplo, para definir o nível PostScript que é criado, chame o `ToPSOptionsSpec` do objeto `setPsLevel` e transmita um `PSLevel` valor de enumeração que especifica o nível PostScript. Para obter informações sobre todos os valores de tempo de execução que podem ser definidos, consulte `ToPSOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converta o documento PDF em um arquivo PostScript.

   Chame o `ConvertPdfServiceClient`do objeto `toPS2` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF a ser convertido em um arquivo PostScript.
   * A `ToPSOptionsSpec` objeto que especifica as opções de tempo de execução PostScript.

   A variável `toPS2` o método retorna um `Document` objeto que contém o novo documento PostScript.

1. Salve o arquivo PostScript.

   * Criar um `java.io.File` e certifique-se de que a extensão do nome do arquivo seja .ps.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `toPS2` método).

**Consulte também**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Início rápido (modo SOAP): conversão de um documento PDF em PostScript usando a API do Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento PDF em PS usando a API do serviço Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Converta um documento PDF em PostScript usando a API de serviço de conversão de PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Converter PDF.

   * Criar um `ConvertPdfServiceClient` usando seu construtor padrão.
   * Criar um `ConvertPdfServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `ConvertPdfServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte o documento PDF para converter em um arquivo PostScript.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar um documento PDF convertido em um arquivo PostScript.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser convertido e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de conversão.

   * Criar um `ToPSOptionsSpec` invocando seu construtor.
   * Defina as opções de tempo de execução atribuindo um valor ao `ToPSOptionsSpec` membro de dados do objeto. Por exemplo, para definir o nível PostScript que é criado, atribua um `PSLevel` valor de enumeração para o `ToPSOptionsSpec` do objeto `psLevel` membro de dados.

1. Converta o documento PDF em um arquivo PostScript.

   Chame o `GeneratePDFServiceService` do objeto `toPS2` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF a ser convertido em um arquivo PostScript
   * A `ToPSOptionsSpec` objeto que especifica as opções de tempo de execução

   Após a conclusão da conversão, extraia os dados binários que representam o documento PostScript, acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que pode ser gravada em um arquivo PostScript.

1. Salve o arquivo PostScript.

   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo PS.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `encryptPDFUsingPassword` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo PostScript, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

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

Antes de executar programaticamente uma operação de serviço Converter PDF, você deve criar um cliente de serviço Converter PDF. Se estiver usando a API Java, crie uma `ConvertPdfServiceClient` objeto. Se estiver usando a API do serviço Web, crie uma `ConvertPDFServiceService` objeto.

**Recuperar o documento PDF para converter**

Recupere o documento PDF para converter em uma imagem. Não é possível converter um documento PDF interativo em uma imagem. Se você tentar fazer isso, uma exceção será lançada. Para converter um documento PDF interativo em um arquivo de imagem, é necessário nivelar o documento PDF antes de convertê-lo. (Consulte [Nivelamento de documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Definir opções de tempo de execução**

Defina opções de tempo de execução, como o formato da imagem e os valores de resolução. Para obter informações sobre os valores de tempo de execução, consulte `ToImageOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Conversão do PDF em uma imagem**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, você pode converter o documento PDF em uma imagem. Um objeto de coleção que contém as imagens é retornado.

**Recuperar os arquivos de imagem de uma coleção**

Você pode recuperar arquivos de imagem de um objeto de coleção que o serviço Converter PDF retorna. Cada elemento na coleção é um `com.adobe.idp.Document` instância (ou um `BLOB` caso esteja usando serviços da web) que você pode salvar como um arquivo de imagem, como um arquivo JPG.

O formato do arquivo de imagem depende da variável `ImageConvertFormat` opção de tempo de execução. Ou seja, se você definir a variável `ImageConvertFormat` opção de tempo de execução para `ImageConvertFormat.JPEG`, é possível salvar arquivos de imagem como arquivos JPG.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da conversão da API de serviço do PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em arquivos de imagem usando a API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Converta um documento PDF em um formato de imagem usando a API de serviço Converter PDF (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente Converter PDF.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `ConvertPdfServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o documento PDF para converter.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução.

   * Criar um `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o `setImageConvertFormat` e transmitindo um `ImageConvertFormat` valor de enumeração que especifica o tipo de formato.

   >[!NOTE]
   >
   >Definição de `ImageConvertFormat` o valor de enumeração é obrigatório.

1. Converta o PDF em uma imagem.

   Chame o `ConvertPdfServiceClient` do objeto `toImage2` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o arquivo PDF a ser convertido.
   * A `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` objeto que contém as várias preferências sobre o formato de imagem de destino.

   A variável `toImage2` o método retorna um `java.util.List` objeto que contém imagens. Cada elemento na coleção é um `com.adobe.idp.Document` instância.

1. Recupera os arquivos de imagem de uma coleção.

   Repita através do `java.util.List` para determinar se as imagens estão presentes. Cada elemento é um `com.adobe.idp.Document` instância. Salve a imagem invocando o `com.adobe.idp.Document` do objeto `copyToFile` e passar um `java.io.File` objeto.

**Consulte também**

[Início rápido (modo SOAP): conversão de um documento PDF em arquivos JPEG usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Converter um documento PDF em arquivos de imagem usando a API do serviço Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converta um documento PDF em um formato de imagem usando a API de serviço de conversão de PDF (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF de conversão.

   * Criar um `ConvertPdfServiceClient` usando seu construtor padrão.
   * Criar um `ConvertPdfServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. No entanto, especifique `?blob=mtom`.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `ConvertPdfServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF para converter.

   * Criar um `BLOB` usando seu construtor. Este `BLOB` é usado para armazenar o formulário PDF.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que especifique o local do formulário de PDF e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Criar um `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o `setImageConvertFormat` e transmitindo um `ImageConvertFormat` valor de enumeração que especifica o tipo de formato.

   >[!NOTE]
   >
   >Definição de `ImageConvertFormat` o valor de enumeração é obrigatório.

1. Converta o PDF em uma imagem.

   Chame o `ConvertPDFServiceService` do objeto `toImage2` e passe os seguintes valores:

   * A `BLOB` objeto que representa o arquivo a ser convertido
   * A `ToImageOptionsSpec` objeto que contém as várias preferências sobre o formato de imagem de destino

   A variável `toImage2` o método retorna um `MyArrayOfBLOB` objeto que contém os arquivos de imagem recém-criados.

1. Recupera os arquivos de imagem de uma coleção.

   * Determine o número de elementos na variável `MyArrayOfBLOB` obtendo o valor de seu `Count` campo. Cada elemento é um `BLOB` objeto que contém a imagem.
   * Repita através do `MyArrayOfBLOB` e salve cada arquivo de imagem.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
