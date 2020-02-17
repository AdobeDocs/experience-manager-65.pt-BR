---
title: Como trabalhar com formulários com códigos de barras
seo-title: Como trabalhar com formulários com códigos de barras
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Como trabalhar com formulários com códigos de barras {#working-with-barcoded-forms}

## Sobre o serviço de formulários com códigos de barras {#about-the-barcoded-forms-service}

O serviço de formulários com códigos de barras automatiza a captura de dados de formulários preenchidos e impressos e integra informações capturadas nos principais sistemas de TI de uma organização.

Usando o serviço de formulários com códigos de barras, é possível adicionar códigos de barras unidimensionais e bidimensionais a formulários PDF interativos. Em seguida, você pode publicar os formulários com códigos de barras em um site ou distribuí-los por email ou CD. Quando um usuário preenche um formulário com códigos de barras usando o Adobe Reader, o Acrobat Professional ou o Acrobat Standard, o código de barras é atualizado automaticamente para codificar os dados de formulário fornecidos pelo usuário. O usuário pode enviar o formulário eletronicamente ou imprimi-lo em papel e enviá-lo por email, fax ou à mão. Posteriormente, você pode extrair os dados fornecidos pelo usuário como parte de um fluxo de trabalho automatizado, roteando os dados entre os processos de aprovação e os sistemas de negócios.

Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Decodificação de dados de formulário com códigos de barras {#decoding-barcoded-form-data}

É possível usar a API de serviço de formulários com códigos de barras para decodificar dados de um formulário PDF ou de uma imagem que contenha um código de barras. Decodificar dados de formulário significa extrair dados localizados no código de barras. Para que os dados possam ser decodificados de um formulário PDF (ou imagem), o usuário precisa preencher o formulário com dados.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para decodificar dados de um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do cliente de formulários com códigos de barras.
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
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado em JBoss)
* xercesImpl.jar (localizado em &lt;diretório de instalação>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBOSS, será necessário substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um objeto de API do cliente de formulários com códigos de barras**

Antes de executar programaticamente uma operação de serviço de formulários com códigos de barras, é necessário criar um cliente de serviço de formulários com códigos de barras. Se você estiver usando a API Java, crie um `BarcodedFormsServiceClient` objeto. Se você estiver usando a API de serviço da Web para formulários com códigos de barras, crie um `BarcodedFormsServiceService` objeto.

**Obter um formulário PDF que contenha dados com códigos de barras**

É necessário obter um formulário PDF que contenha um código de barras que tenha sido preenchido com dados do usuário.

**Decodificar os dados do formulário PDF**

Depois de obter um formulário PDF (ou imagem) que contenha um código de barras, é possível decodificar dados. O serviço de formulários com códigos de barras oferece suporte aos seguintes tipos de códigos de barras:

* Códigos de barras PDF417.
* Códigos de barras da matriz de dados.
* Códigos de barras do código QR.
* Códigos de barras Codabar.
* Códigos de barras do código 128.
* Códigos de barras do código 39.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

A entrada do conjunto de caracteres como hexadecimal na API de decodificação implica que o conteúdo do código de barras seja codificado como uma sequência hexadecimal. Por exemplo, se UTF-8 for especificado como a codificação Caractere no formulário e Hex for especificado na operação de decodificação, o conteúdo do código de barras será codificado como uma string Hex no elemento &lt; `xb:content`> na saída decodificada. Você pode converter esse valor hexadecimal para obter o conteúdo original criando a lógica do aplicativo no aplicativo cliente.

**Converter os dados em uma fonte de dados XML**

Depois de decodificar os dados do formulário, é possível convertê-los em dados XDP ou XFDF. Por exemplo, suponha que você deseja importar os dados para outro formulário. Para importar os dados para um formulário XFA, é necessário converter os dados em dados XDP. Para obter informações, consulte [Importação de dados](/help/forms/developing/importing-exporting-data.md#importing-form-data)do formulário.

**Processar os dados decodificados**

Você pode processar os dados convertidos para atender às suas necessidades comerciais. Por exemplo, após decodificar e converter os dados, é possível salvá-los em um arquivo, armazená-los em um banco de dados corporativo, preencher outro formulário e assim por diante. Esta seção discute como salvar os dados convertidos como um arquivo XML.

>[!NOTE]
>
>O serviço de formulários com códigos de barras não consegue decodificar os dados do código de barras quando os parâmetros delimitador de linha e delimitador de campo têm o mesmo valor

**Consulte também:**

[Decodificar dados de formulário com código de barras usando a API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodificar dados de formulário com código de barras usando a API de serviço da Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API Java {#decode-barcoded-form-data-using-the-java-api}

Decodificar os dados do formulário usando a API de formulários com códigos de barras (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Crie um `BarcodedFormsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Obter um formulário PDF que contenha dados com códigos de barras

   * Crie um `java.io.FileInputStream` objeto que represente o formulário PDF que contém dados com código de barras usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando o método do `BarcodedFormsServiceClient` objeto `decode` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o formulário PDF.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras PDF417 deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras da matriz de dados deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras QR deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras codabar deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras 128 deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras 39 deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras EAN-13 deve ser decodificado.
   * Um `java.lang.Boolean` objeto que especifica se um código de barras EAN-8 deve ser decodificado.
   * Um valor de `com.adobe.livecycle.barcodedforms.CharSet` enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.
   O `decode` método retorna um `org.w3c.dom.Document` objeto que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o método do `BarcodedFormsServiceClient` objeto `extractToXML` e transmitindo os seguintes valores:

   * O `org.w3c.dom.Document` objeto que contém dados decodificados (certifique-se de usar o valor de retorno do `decode` método).
   * Um valor de `com.adobe.livecycle.barcodedforms.Delimiter` enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * Um valor de `com.adobe.livecycle.barcodedforms.Delimiter` enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * Um valor de `com.adobe.livecycle.barcodedforms.XMLFormat` enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.
   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O `extractToXML` método retorna um `java.util.List` objeto em que cada elemento é um `org.w3c.dom.Document` objeto. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então há quatro elementos no `java.util.List` objeto retornado.

1. Processar os dados decodificados

   * Itere pelo `java.util.List` objeto para obter cada `org.w3c.dom.Document` objeto localizado na lista.
   * Para cada elemento na lista, converta o `org.w3c.dom.Document` objeto em um `com.adobe.idp.Document` objeto. (A lógica do aplicativo que converte um `org.w3c.dom.Document` objeto em um `com.adobe.idp.Document` objeto é mostrada nos dados do formulário com código de barras Decoding usando o exemplo da API Java).
   * Salve os dados XML como um arquivo XML chamando os objetos `com.adobe.idp.Document` `copyToFile`e transmitindo um objeto File que representa o arquivo XML.

**Consulte também:**

[Início rápido (modo SOAP): Decodificação de dados de formulário com código de barras usando a API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API de serviço da Web {#decode-barcoded-form-data-using-the-web-service-api}

Decodificar os dados do formulário usando a API de formulários com códigos de barras (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o serviço de formulários em barras WSDL. Para obter informações, consulte [Invocar formulários AEM usando a codificação](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.
   * Consulte o assembly do cliente Microsoft .NET. Para obter informações, consulte &quot;Fazer referência ao assembly do cliente .NET&quot; em [Invocar formulários AEM usando codificação](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Usando o assembly do cliente Microsoft .NET que consome o serviço de formulários com códigos de barras WSDL, crie um `BarcodedFormsServiceService` objeto chamando seu construtor padrão.

1. Obter um formulário PDF que contenha dados com códigos de barras

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF que contém um código de barras.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `binaryData` propriedade ao conteúdo da matriz de bytes.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando o método do `BarcodedFormsServiceService` objeto `decode` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o formulário PDF.
   * Um `Boolean` objeto que especifica se um código de barras PDF417 deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras da matriz de dados deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras QR deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras codabar deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras 128 deve ser decodificado.
   * Um `Bolean` objeto que especifica se um código de barras 39 deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras EAN-13 deve ser decodificado.
   * Um `Boolean` objeto que especifica se um código de barras EAN-8 deve ser decodificado.
   * Um valor de `CharSet` enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.
   O `decode` método retorna um valor de string que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o método do `BarcodedFormsServiceService` objeto `extractToXML` e transmitindo os seguintes valores:

   * Um valor de string que contém dados decodificados (certifique-se de usar o valor de retorno do `decode` método).
   * Um valor de `Delimiter` enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * Um valor de `Delimiter` enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * Um valor de `XMLFormat` enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.
   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O `extractToXML` método retorna uma `Object` matriz em que cada elemento é uma `BLOB` instância. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então há quatro elementos no `Object` storage retornado.

1. Processar os dados decodificados

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingPassword` método. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `binaryData` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
