---
title: Trabalho com formulários com códigos de barras
seo-title: Working with barcoded forms
description: Decode dados de um formulário PDF ou de uma imagem que contenha um código de barras usando a API do Java e a API do serviço da Web.
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Trabalho com formulários com códigos de barras {#working-with-barcoded-forms}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço de formulários com códigos de barras {#about-the-barcoded-forms-service}

O serviço de formulários com códigos de barras automatiza a captura de dados de formulários preenchidos e impressos e integra informações capturadas nos principais sistemas de TI de uma organização.

Usando o serviço de formulários com códigos de barras, é possível adicionar códigos de barras unidimensionais e bidimensionais a PDF forms interativos. Em seguida, você pode publicar os formulários com códigos de barras em um site ou distribuí-los por email ou CD. Quando um usuário preenche um formulário com códigos de barras usando o Adobe Reader, Acrobat Professional ou Acrobat Standard, o código de barras é atualizado automaticamente para codificar os dados de formulário fornecidos pelo usuário. O usuário pode enviar o formulário eletronicamente ou imprimi-lo em papel e enviá-lo por email, fax ou à mão. Posteriormente, é possível extrair os dados fornecidos pelo usuário como parte de um fluxo de trabalho automatizado, roteando os dados entre processos de aprovação e sistemas comerciais.

Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodificação de dados de formulário com código de barras {#decoding-barcoded-form-data}

Você pode usar a API do serviço de formulários com códigos de barras para decodificar dados de um formulário PDF ou de uma imagem que contenha um código de barras. Decodificar dados de formulário significa extrair dados localizados no código de barras. Para que os dados possam ser decodificados em um formulário PDF (ou imagem), o usuário precisa preencher o formulário com dados.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para decodificar os dados de um formulário PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente formsClient com códigos de barras.
1. Obtenha um formulário PDF que contenha dados com códigos de barras.
1. Decode os dados do formulário PDF.
1. Converta os dados em uma fonte de dados XML.
1. Processar os dados decodificados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)
* xercesImpl.jar (localizado em &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBOSS, será necessário substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente de formulários com códigos de barras**

Antes de executar programaticamente uma operação de serviço de formulários com códigos de barras, é necessário criar um cliente de serviço Forms com códigos de barras. Se estiver usando a API do Java, crie um `BarcodedFormsServiceClient` objeto. Se estiver usando a API do serviço da Web de formulários com códigos de barras, crie um `BarcodedFormsServiceService` objeto.

**Obter um formulário PDF que contenha dados com códigos de barras**

Você deve obter um formulário PDF que contenha um código de barras que tenha sido preenchido com dados do usuário.

**Decodificar os dados do formulário PDF**

Após obter um formulário PDF (ou imagem) contendo um código de barras, é possível decodificar os dados. O serviço Forms com códigos de barras oferece suporte para os seguintes tipos de códigos de barras:

* Códigos de barras PDF417.
* Códigos de barras da matriz de dados.
* Códigos de barras do código QR.
* Códigos de barras Codabar.
* Códigos de barras do código 128.
* Códigos de barras do código 39.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

A entrada do conjunto de caracteres como hexadecimal na API de decodificação implica que o conteúdo do código de barras é codificado como uma sequência de caracteres hexadecimal. Por exemplo, se UTF-8 for especificado como a Codificação de caractere no formulário e Hex for especificado na operação de decodificação, o conteúdo do código de barras será codificado como uma string hexadecimal no &lt; `xb:content`> na saída decodificada. Você pode converter esse valor hexadecimal para obter o conteúdo original criando a lógica do aplicativo no aplicativo cliente.

**Converter os dados em uma fonte de dados XML**

Após decodificar os dados do formulário, é possível convertê-los em dados XDP ou XFDF. Por exemplo, suponha que você deseja importar os dados para outro formulário. Para importar os dados para um formulário XFA, é necessário converter os dados em dados XDP. Para obter mais informações, consulte [Importação de dados de formulário](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Processar os dados decodificados**

Você pode processar os dados convertidos para atender às suas necessidades de negócios. Por exemplo, após decodificar e converter os dados, é possível salvá-los em um arquivo, armazená-los em um banco de dados corporativo, preencher outro formulário e assim por diante. Esta seção discute como salvar os dados convertidos como um arquivo XML.

>[!NOTE]
>
>O serviço de formulários com códigos de barras não decodifica os dados do código de barras quando o delimitador de linha e os parâmetros delimitadores de campo têm o mesmo valor

**Consulte também**

[Decodificar dados de formulário com código de barras usando a API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodificar dados de formulário com código de barras usando a API do serviço da Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API Java {#decode-barcoded-form-data-using-the-java-api}

Decode dados de formulário usando a API de formulários com códigos de barras (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho da classe do seu projeto Java.

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Crie um `BarcodedFormsServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Obter um formulário PDF que contenha dados com códigos de barras

   * Crie um `java.io.FileInputStream` objeto que representa o formulário PDF que contém dados com códigos de barras usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando a função `BarcodedFormsServiceClient` do objeto `decode` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o formulário PDF.
   * A `java.lang.Boolean` que especifica se um código de barras PDF417 deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras da matriz de dados deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras QR deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras de codabar deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras 128 deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras 39 deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras EAN-13 deve ser decodificado.
   * A `java.lang.Boolean` que especifica se um código de barras EAN-8 deve ser decodificado.
   * A `com.adobe.livecycle.barcodedforms.CharSet` valor de enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   O `decode` retorna um método `org.w3c.dom.Document` objeto que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o `BarcodedFormsServiceClient` do objeto `extractToXML` e transmitindo os seguintes valores:

   * O `org.w3c.dom.Document` objeto que contém dados decodificados (certifique-se de usar a variável `decode` valor de retorno do método).
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` valor de enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O `extractToXML` método retorna um `java.util.List` objeto no qual cada elemento é um `org.w3c.dom.Document` objeto. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então haverá quatro elementos no formulário retornado `java.util.List` objeto.

1. Processar os dados decodificados

   * Iterar por meio do `java.util.List` objeto para obter cada `org.w3c.dom.Document` objeto localizado na lista.
   * Para cada elemento na lista, converta o `org.w3c.dom.Document` para um `com.adobe.idp.Document` objeto. (A lógica do aplicativo que converte uma `org.w3c.dom.Document` em um `com.adobe.idp.Document` é mostrado em Decoding barcoded form data using the Java API example).
   * Salve os dados XML como um arquivo XML chamando a variável `com.adobe.idp.Document` do objeto `copyToFile`e transmitindo um objeto File que representa o arquivo XML.

**Consulte também**

[Início rápido (modo SOAP): Decodificação de dados de formulário com código de barras usando a API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API do serviço da Web {#decode-barcoded-form-data-using-the-web-service-api}

Decode dados de formulário usando a API de formulários com códigos de barras (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL do serviço de formulários com códigos de barras. Para obter mais informações, consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Faça referência ao assembly do cliente Microsoft .NET. Para obter informações, consulte &quot;Fazendo referência ao assembly do cliente .NET&quot; em [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Usando o conjunto de clientes Microsoft .NET que consome o WSDL do serviço de formulários com códigos de barras, crie um `BarcodedFormsServiceService` chamando seu construtor padrão.

1. Obter um formulário PDF que contenha dados com códigos de barras

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF que contém um código de barras.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `binaryData` com o conteúdo da matriz de bytes.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando a função `BarcodedFormsServiceService` do objeto `decode` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o formulário PDF.
   * A `Boolean` que especifica se um código de barras PDF417 deve ser decodificado.
   * A `Boolean` que especifica se um código de barras da matriz de dados deve ser decodificado.
   * A `Boolean` que especifica se um código de barras QR deve ser decodificado.
   * A `Boolean` que especifica se um código de barras de codabar deve ser decodificado.
   * A `Boolean` que especifica se um código de barras 128 deve ser decodificado.
   * A `Bolean` que especifica se um código de barras 39 deve ser decodificado.
   * A `Boolean` que especifica se um código de barras EAN-13 deve ser decodificado.
   * A `Boolean` que especifica se um código de barras EAN-8 deve ser decodificado.
   * A `CharSet` valor de enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   O `decode` retorna um valor de string que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o `BarcodedFormsServiceService` do objeto `extractToXML` e transmitindo os seguintes valores:

   * Um valor de string que contém dados decodificados (certifique-se de usar a variável `decode` valor de retorno do método).
   * A `Delimiter` valor de enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * A `Delimiter` valor de enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * A `XMLFormat` valor de enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O `extractToXML` retorna um método `Object` matriz em que cada elemento é um `BLOB` instância. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então haverá quatro elementos no formulário retornado `Object` matriz.

1. Processar os dados decodificados

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingPassword` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
