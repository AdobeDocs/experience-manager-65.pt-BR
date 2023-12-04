---
title: Trabalhar com formulários com códigos de barras
seo-title: Working with barcoded forms
description: Decodifique dados de um formulário PDF ou de uma imagem que contenha um código de barras usando a API do Java e a API do serviço da Web.
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# Trabalhar com formulários com códigos de barras {#working-with-barcoded-forms}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Sobre o serviço de formulários com código de barras {#about-the-barcoded-forms-service}

O serviço de formulários com código de barras automatiza a captura de dados de formulários de preenchimento e impressão e integra as informações capturadas aos principais sistemas de TI de uma organização.

Usando o serviço de formulários com código de barras, é possível adicionar códigos de barras unidimensionais e bidimensionais aos PDF forms interativos. Em seguida, você pode publicar os formulários com código de barras em um site ou distribuí-los por email ou CD. Quando um usuário preenche um formulário com código de barras usando o Adobe Reader, o Acrobat Professional ou o Acrobat Standard, o código de barras é atualizado automaticamente para codificar os dados de formulário fornecidos pelo usuário. O usuário pode enviar o formulário eletronicamente ou imprimi-lo em papel e enviá-lo por correio, fax ou mão. Posteriormente, você pode extrair os dados fornecidos pelo usuário como parte de um fluxo de trabalho automatizado, roteando os dados entre processos de aprovação e sistemas de negócios.

Para obter mais informações sobre o serviço de formulários com código de barras, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodificação de dados de formulário com código de barras {#decoding-barcoded-form-data}

Você pode usar a API do serviço de formulários com código de barras para decodificar dados de um formulário PDF ou imagem que contenha um código de barras. Decodificar dados do formulário significa extrair dados que estão no código de barras. Antes que os dados possam ser decodificados de um formulário (ou imagem) PDF, um usuário precisa preencher o formulário com dados.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de formulários com código de barras, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para decodificar dados de um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API formsClient com código de barras.
1. Obtenha um formulário PDF que contenha dados com código de barras.
1. Decodifique os dados do formulário PDF.
1. Converta os dados em uma fonte de dados XML.
1. Processe os dados decodificados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)
* xercesImpl.jar (in &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBOSS, você deverá substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente de formulários com código de barras**

Antes de executar programaticamente uma operação do serviço de formulários com código de barras, você deve criar um cliente de serviço do Forms com código de barras. Se estiver usando a API Java, crie uma `BarcodedFormsServiceClient` objeto. Se estiver usando a API do serviço Web de formulários com código de barras, crie uma `BarcodedFormsServiceService` objeto.

**Obtenha um formulário PDF que contenha dados com código de barras**

Obtenha um formulário PDF que contenha um código de barras que tenha sido preenchido com dados do usuário.

**Decodifique os dados do formulário PDF**

Depois de obter um formulário (ou imagem) PDF que contém um código de barras, você pode decodificar os dados. O serviço Forms com código de barras é compatível com os seguintes tipos de códigos de barras:

* códigos de barras PDF417.
* Códigos de barras da matriz de dados.
* Códigos de barras do código QR.
* Códigos de barras de codabar.
* Código 128 códigos de barras.
* Código 39 códigos de barras.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

A entrada do conjunto de caracteres como hexadecimal na API de decodificação implica que o conteúdo do código de barras é codificado como uma string hexadecimal. Por exemplo, se UTF-8 for especificado como a codificação de caractere no formulário e Hex for especificado na operação de decodificação, o conteúdo do código de barras será codificado como uma cadeia de caracteres Hex no &lt; `xb:content`> na saída decodificada. É possível converter esse valor hexadecimal para obter o conteúdo original criando a lógica do aplicativo no aplicativo cliente.

**Converter os dados em uma fonte de dados XML**

Após decodificar os dados do formulário, é possível convertê-los em dados XDP ou XFDF. Por exemplo, suponha que você deseja importar os dados para outro formulário. Para importar os dados em um formulário XFA, é necessário converter os dados em dados XDP. Para obter informações, consulte [Importação de dados do formulário](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Processar os dados decodificados**

Você pode processar os dados convertidos para atender aos requisitos da sua empresa. Por exemplo, depois de decodificar e converter os dados, você pode salvá-los em um arquivo, armazená-los em um banco de dados corporativo, preencher outro formulário e assim por diante. Esta seção discute como salvar os dados convertidos em um arquivo XML.

>[!NOTE]
>
>O serviço de formulários com código de barras não decodifica os dados do código de barras quando os parâmetros delimitador de linha e delimitador de campo têm o mesmo valor

**Consulte também**

[Decodificar dados de formulário com código de barras usando a API do Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodificar dados de formulário com código de barras usando a API do serviço Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API do Java {#decode-barcoded-form-data-using-the-java-api}

Decodifique dados de formulário usando a API de formulários com código de barras (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho de classe do projeto Java.

1. Criar um objeto de API do cliente de formulários com código de barras

   Criar um `BarcodedFormsServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Obtenha um formulário PDF que contenha dados com código de barras

   * Criar um `java.io.FileInputStream` objeto que representa o formulário PDF que contém dados com código de barras usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Decodifique os dados do formulário PDF

   Decodifique os dados do formulário chamando o `BarcodedFormsServiceClient` do objeto `decode` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o formulário PDF.
   * A `java.lang.Boolean` objeto que especifica se um código de barras PDF417 deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras de matriz de dados deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras QR deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras de codabar deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras 128 deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras 39 deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras EAN-13 deve ser decodificado.
   * A `java.lang.Boolean` objeto que especifica se um código de barras EAN-8 deve ser decodificado.
   * A `com.adobe.livecycle.barcodedforms.CharSet` valor de enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   A variável `decode` o método retorna um `org.w3c.dom.Document` objeto que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF invocando o `BarcodedFormsServiceClient` do objeto `extractToXML` e transmitindo os seguintes valores:

   * A variável `org.w3c.dom.Document` objeto que contém dados decodificados (certifique-se de usar o `decode` valor de retorno do método).
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valor de enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` valor de enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   A variável `extractToXML` o método retorna um `java.util.List` objeto no qual cada elemento é um `org.w3c.dom.Document` objeto. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, haverá quatro elementos no formulário retornado `java.util.List` objeto.

1. Processar os dados decodificados

   * Repita através do `java.util.List` objeto para obter cada `org.w3c.dom.Document` objeto que está na lista.
   * Para cada elemento na lista, converta o `org.w3c.dom.Document` objeto a um `com.adobe.idp.Document` objeto. (A lógica da aplicação que converte um `org.w3c.dom.Document` em um `com.adobe.idp.Document` é mostrado na página Decodificação de dados de formulário com código de barras (usando o exemplo da API Java).
   * Salve os dados XML como um arquivo XML chamando o `com.adobe.idp.Document` do objeto `copyToFile`e transmitindo um objeto File que representa o arquivo XML.

**Consulte também**

[Início rápido (modo SOAP): decodificação de dados de formulário com código de barras usando a API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API do serviço Web {#decode-barcoded-form-data-using-the-web-service-api}

Decodifique dados de formulário usando a API de formulários com código de barras (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL do serviço de formulários com código de barras. Para obter informações, consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Referencie o assembly do cliente Microsoft .NET. Para obter informações, consulte &quot;Referenciar o assembly do cliente .NET&quot; em [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Criar um objeto de API do cliente de formulários com código de barras

   Usando o assembly cliente Microsoft .NET que consome o WSDL do serviço de formulários com código de barras, crie um `BarcodedFormsServiceService` chamando seu construtor padrão.

1. Obtenha um formulário PDF que contenha dados com código de barras

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF que contém um código de barras.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `binaryData` com o conteúdo da matriz de bytes.

1. Decodifique os dados do formulário PDF

   Decodifique os dados do formulário chamando o `BarcodedFormsServiceService` do objeto `decode` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o formulário PDF.
   * A `Boolean` objeto que especifica se um código de barras PDF417 deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras de matriz de dados deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras QR deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras de codabar deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras 128 deve ser decodificado.
   * A `Bolean` objeto que especifica se um código de barras 39 deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras EAN-13 deve ser decodificado.
   * A `Boolean` objeto que especifica se um código de barras EAN-8 deve ser decodificado.
   * A `CharSet` valor de enumeração que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   A variável `decode` O método retorna um valor de string que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF invocando o `BarcodedFormsServiceService` do objeto `extractToXML` e transmitindo os seguintes valores:

   * Um valor de string que contém dados decodificados (certifique-se de usar o `decode` valor de retorno do método).
   * A `Delimiter` valor de enumeração que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * A `Delimiter` valor de enumeração que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * A `XMLFormat` valor de enumeração que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   A variável `extractToXML` o método retorna um `Object` matriz em que cada elemento é um `BLOB` instância. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, haverá quatro elementos no formulário retornado `Object` matriz.

1. Processar os dados decodificados

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `encryptPDFUsingPassword` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `binaryData` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
