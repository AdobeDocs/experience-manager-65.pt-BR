---
title: Conversão de PDF em arquivos Postscript e Imagem
seo-title: Conversão de PDF em arquivos Postscript e Imagem
description: Use o serviço Converter PDF para converter documentos PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF) usando a API Java e a API do serviço da Web.
seo-description: Use o serviço Converter PDF para converter documentos PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF) usando a API Java e a API do serviço da Web.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2847'
ht-degree: 0%

---


# Convertendo PDF em Postscript e arquivos de imagem {#converting-pdf-to-postscript-andimage-files}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço Converter PDF**

O serviço Converter PDF converte documentos PDF em PostScript e em vários formatos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para a impressão automática baseada em servidor em qualquer impressora PostScript. A conversão de um documento PDF em um arquivo TIFF de várias páginas é prática ao arquivar documentos em sistemas de gerenciamento de conteúdo que não oferecem suporte a documentos PDF.

Você pode realizar essas tarefas usando o serviço Converter PDF:

* Converta documentos PDF em PostScript.
* Converta documentos PDF em formatos de imagem.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertendo documentos PDF em PostScript {#converting-pdf-documents-to-postscript}

Este tópico descreve como você pode usar a API de Serviço de Conversão de PDF (Java e serviço da Web) para converter documentos PDF de forma programática em arquivos PostScript. O documento PDF convertido em um arquivo PostScript deve ser um documento PDF não interativo. Ou seja, se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de Converter serviço PDF, você deve criar um cliente de serviço Converter PDF. Se estiver usando a API do Java, crie um objeto `ConvertPdfServiceClient` . Se estiver usando a API do serviço da Web, crie um objeto `ConvertPDFServiceService` .

Esta seção usa a funcionalidade de serviço da Web introduzida no AEM Forms. Para acessar uma nova funcionalidade, você precisa construir seu objeto proxy usando o atributo `lc_version` . (Consulte &quot;Acesso a nova funcionalidade usando serviços da Web&quot; em [Chamada do AEM Forms usando Serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Referencie o documento PDF a ser convertido em um arquivo PostScript**

Faça referência ao documento PDF que você deseja converter em um arquivo PostScript. Como mencionado anteriormente neste tópico, o documento PDF deve ser um documento PDF não interativo. Se você tentar converter um documento PDF interativo em um arquivo PostScript, uma exceção será lançada.

**Definir opções de tempo de execução de conversão**

Ao converter um documento PDF em um arquivo PostScript, você pode definir opções de tempo de execução que especificam o tipo PostScript que é criado. Por exemplo, você pode definir um arquivo PostScript de nível 3.

Normalmente, o arquivo PostScript gerado reflete o tamanho do documento PDF de entrada. Se você selecionar a opção `ShrinkToFit` (que reduz a saída do arquivo PostScript para ajustá-la à página), você não verá uma diferença entre o documento PDF de entrada e o arquivo PostScript gerado. A opção `ShrinkToFit` só terá efeito se você optar por imprimir em um tamanho de página menor que o documento PDF de entrada. Para selecionar um tamanho de página menor, defina a opção `PageSize`. Além disso, é recomendável definir a opção `RotateAndCenter` como `true` para obter a saída correta do PostScript.

Da mesma forma, se você selecionar a opção `ExpandToFit` (que expande a saída do arquivo PostScript para ajustá-la à página), ela só entrará em vigor se você optar por imprimir em um tamanho de página maior que o documento PDF de entrada. Para selecionar um tamanho de página maior, defina a opção `PageSize`. Além disso, é recomendável definir a opção `RotateAndCenter` como `true` para obter a saída correta do PostScript.

>[!NOTE]
>
>Para obter informações sobre os valores de tempo de execução que você pode definir, consulte a referência da classe `ToPSOptionsSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o documento PDF em um arquivo PostScript**

Depois de criar o cliente do serviço e definir as opções de tempo de execução, você pode chamar a operação de conversão de PostScript. Essa operação precisará de informações sobre o documento a ser convertido, incluindo o nível de PostScript preferencial para o documento de destino.

**Salvar o arquivo PostScript**

Após converter o documento PDF em PostScript, é possível salvar a saída como um arquivo PostScript.

**Consulte também:**

[Converter um documento PDF em PS usando a API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Converter um documento PDF em PS usando a API de serviço da Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converter início rápido da API do serviço de PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em PS usando a API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Converta um documento PDF em PostScript usando a API do serviço de conversão de PDF (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência ao documento PDF para conversão em um arquivo PostScript.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e passe um valor de string que especifique o local do documento PDF a ser convertido.
   * Crie um objeto `com.adobe.idp.Document` que armazene o documento PDF usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Defina as opções de tempo de execução da conversão.

   * Crie um objeto `ToPSOptionsSpec` chamando seu construtor.
   * Defina as opções de tempo de execução chamando um método apropriado que pertença ao objeto `ToPSOptionsSpec`. Por exemplo, para definir o nível PostScript criado, chame o método `ToPSOptionsSpec` do objeto `setPsLevel` e passe um valor de enumeração `PSLevel` que especifique o nível de PostScript. Para obter informações sobre todos os valores de tempo de execução que você pode definir, consulte a referência da classe `ToPSOptionsSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converta o documento PDF em um arquivo PostScript.

   Chame o método `ConvertPdfServiceClient`do objeto `toPS2` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser convertido em um arquivo PostScript.
   * Um objeto `ToPSOptionsSpec` que especifica as opções de tempo de execução do PostScript.

   O método `toPS2` retorna um objeto `Document` que contém o novo documento PostScript.

1. Salve o arquivo PostScript.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .ps.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `toPS2`).

**Consulte também:**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Início rápido (modo SOAP): Conversão de um documento PDF em PostScript usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter um documento PDF em PS usando a API de serviço da Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Converta um documento PDF em PostScript usando a API do serviço de conversão de PDF (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um objeto `ConvertPdfServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Você não precisa usar o atributo `lc_version`. No entanto, especifique `?blob=mtom`.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ConvertPdfServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência ao documento PDF para conversão em um arquivo PostScript.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF convertido em um arquivo PostScript.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF a ser convertido e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução da conversão.

   * Crie um objeto `ToPSOptionsSpec` chamando seu construtor.
   * Defina as opções de tempo de execução atribuindo um valor ao membro de dados do objeto `ToPSOptionsSpec`. Por exemplo, para definir o nível PostScript criado, atribua um valor de enumeração `PSLevel` ao membro de dados `ToPSOptionsSpec` do objeto `psLevel`.

1. Converta o documento PDF em um arquivo PostScript.

   Chame o método `GeneratePDFServiceService` do objeto `toPS2` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser convertido em um arquivo PostScript
   * Um objeto `ToPSOptionsSpec` que especifica as opções de tempo de execução

   Após a conclusão da conversão, extraia os dados binários que representam o documento PostScript acessando a propriedade `BLOB` do objeto `MTOM`. Isso retorna uma matriz de bytes que pode ser gravada em um arquivo PostScript.

1. Salve o arquivo PostScript.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo PS.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `encryptPDFUsingPassword`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes no arquivo PostScript chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](converting-pdf-postscript-image-files.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Converter documentos PDF em formatos de imagem {#converting-pdf-documents-to-image-formats}

Você pode usar o serviço Converter PDF para converter documentos PDF de forma programática em formatos de imagem, que incluem JPEG, JPEG 2000, TIFF e PNG. Ao converter um documento PDF em um arquivo de imagem, você pode usar o documento PDF como um arquivo de imagem. Por exemplo, você pode colocar a imagem em um sistema de gerenciamento de conteúdo corporativo para armazenamento.

Ao converter um documento PDF em uma imagem, o serviço Converter PDF cria uma imagem separada para cada página no documento. Ou seja, se o documento tiver 20 páginas, o serviço Converter PDF criará 20 arquivos de imagem. Ao converter um documento PDF em um formato de imagem, é possível criar imagens individuais para cada página no documento PDF ou um único arquivo de imagem para todo o documento PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Converter PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento PDF em qualquer um dos tipos suportados, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço Converter PDF.
1. Recupere o documento PDF para converter.
1. Defina as opções de tempo de execução.
1. Converta o PDF em uma imagem.
1. Recupere os arquivos de imagem de uma coleção.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente Converter PDF**

Antes de executar programaticamente uma operação de Converter serviço PDF, você deve criar um cliente de serviço Converter PDF. Se estiver usando a API do Java, crie um objeto `ConvertPdfServiceClient` . Se estiver usando a API do serviço da Web, crie um objeto `ConvertPDFServiceService` .

**Recuperar o documento PDF para converter**

Você deve recuperar o documento PDF para converter em uma imagem. Não é possível converter um documento PDF interativo em uma imagem. Se você tentar fazer isso, uma exceção será lançada. Para converter um documento PDF interativo em um arquivo de imagem, é necessário nivelar o documento PDF antes de convertê-lo. (Consulte [Nivelar documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Definir opções de tempo de execução**

Você deve definir opções de tempo de execução, como o formato da imagem e os valores de resolução. Para obter informações sobre os valores de tempo de execução, consulte a referência de classe `ToImageOptionsSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Converter o PDF em uma imagem**

Depois de criar o cliente de serviço e definir as opções de tempo de execução, é possível converter o documento PDF em uma imagem. Um objeto de coleção que contém as imagens é retornado.

**Recuperar os arquivos de imagem de uma coleção**

Você pode recuperar arquivos de imagem de um objeto de coleção retornado pelo serviço Converter PDF. Cada elemento na coleção é uma instância `com.adobe.idp.Document` (ou uma instância `BLOB` se você estiver usando serviços da Web) que pode ser salva como um arquivo de imagem, como um arquivo JPG.

O formato do arquivo de imagem depende da opção de tempo de execução `ImageConvertFormat`. Ou seja, se você definir a opção `ImageConvertFormat` de tempo de execução para `ImageConvertFormat.JPEG`, poderá salvar arquivos de imagem como arquivos JPG.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Converter início rápido da API do serviço de PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Converter um documento PDF em arquivos de imagem usando a API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Converta um documento PDF em um formato de imagem usando a API do serviço Converter PDF (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-convertpdf-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente Converter PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recupere o documento PDF para converter.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Defina as opções de tempo de execução.

   * Crie um objeto `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o método `setImageConvertFormat` e transmitindo um valor de enumeração `ImageConvertFormat` que especifique o tipo de formato.

   >[!NOTE]
   >
   >A configuração do valor de enumeração `ImageConvertFormat` é obrigatória.

1. Converta o PDF em uma imagem.

   Chame o método `ConvertPdfServiceClient` do objeto `toImage2` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o arquivo PDF a ser convertido.
   * Um objeto `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` que contém as várias preferências sobre o formato da imagem de destino.

   O método `toImage2` retorna um objeto `java.util.List` que contém imagens. Cada elemento na coleção é uma instância `com.adobe.idp.Document`.

1. Recupere os arquivos de imagem de uma coleção.

   Itere pelo objeto `java.util.List` para determinar se as imagens estão presentes. Cada elemento é uma instância `com.adobe.idp.Document`. Salve a imagem chamando o método `com.adobe.idp.Document` do objeto `copyToFile` e transmitindo um objeto `java.io.File`.

**Consulte também:**

[Início rápido (modo SOAP): Conversão de um documento PDF em arquivos JPEG usando a API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Converter um documento PDF em arquivos de imagem usando a API do serviço da Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Converta um documento PDF em um formato de imagem usando a API de serviço de conversão de PDF (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF de conversão.

   * Crie um objeto `ConvertPdfServiceClient` usando seu construtor padrão.
   * Crie um objeto `ConvertPdfServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.) Você não precisa usar o atributo `lc_version`. No entanto, especifique `?blob=mtom`.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `ConvertPdfServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere o documento PDF para converter.

   * Crie um objeto `BLOB` usando seu construtor. Esse objeto `BLOB` é usado para armazenar o formulário PDF.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Determine o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um objeto `ToImageOptionsSpec` usando seu construtor.
   * Chame os métodos que pertencem a este objeto, conforme necessário. Por exemplo, defina o tipo de imagem chamando o método `setImageConvertFormat` e transmitindo um valor de enumeração `ImageConvertFormat` que especifique o tipo de formato.

   >[!NOTE]
   >
   >A configuração do valor de enumeração `ImageConvertFormat` é obrigatória.

1. Converta o PDF em uma imagem.

   Chame o método `ConvertPDFServiceService` do objeto `toImage2` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o arquivo a ser convertido
   * Um objeto `ToImageOptionsSpec` que contém as várias preferências sobre o formato da imagem de destino

   O método `toImage2` retorna um objeto `MyArrayOfBLOB` que contém os arquivos de imagem recém-criados.

1. Recupere os arquivos de imagem de uma coleção.

   * Determine o número de elementos no objeto `MyArrayOfBLOB` obtendo o valor do seu campo `Count`. Cada elemento é um objeto `BLOB` que contém a imagem.
   * Itere pelo objeto `MyArrayOfBLOB` e salve cada arquivo de imagem.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
