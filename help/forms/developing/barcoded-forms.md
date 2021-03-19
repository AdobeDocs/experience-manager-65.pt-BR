---
title: Trabalho com formulários com códigos de barras
seo-title: Trabalho com formulários com códigos de barras
description: Decode dados de um formulário PDF ou de uma imagem que contenha um código de barras usando a API do Java e a API do serviço da Web.
seo-description: Decode dados de um formulário PDF ou de uma imagem que contenha um código de barras usando a API do Java e a API do serviço da Web.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---


# Trabalhar com formulários com códigos de barras {#working-with-barcoded-forms}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço de formulários com códigos de barras {#about-the-barcoded-forms-service}

O serviço de formulários com códigos de barras automatiza a captura de dados de formulários preenchidos e impressos e integra informações capturadas nos principais sistemas de TI de uma organização.

Usando o serviço de formulários com códigos de barras, é possível adicionar códigos de barras unidimensionais e bidimensionais a PDF forms interativos. Em seguida, você pode publicar os formulários com códigos de barras em um site ou distribuí-los por email ou CD. Quando um usuário preenche um formulário com códigos de barras usando o Adobe Reader, Acrobat Professional ou Acrobat Standard, o código de barras é atualizado automaticamente para codificar os dados de formulário fornecidos pelo usuário. O usuário pode enviar o formulário eletronicamente ou imprimi-lo em papel e enviá-lo por email, fax ou à mão. Posteriormente, é possível extrair os dados fornecidos pelo usuário como parte de um fluxo de trabalho automatizado, roteando os dados entre processos de aprovação e sistemas comerciais.

Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodificação de dados de formulário com código de barras {#decoding-barcoded-form-data}

É possível usar a API do serviço de formulários com códigos de barras para decodificar dados de um formulário PDF ou de uma imagem que contenha um código de barras. Decodificar dados de formulário significa extrair dados localizados no código de barras. Para que os dados possam ser decodificados em um formulário PDF (ou imagem), o usuário precisa preencher o formulário com dados.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de formulários com códigos de barras, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para decodificar dados de um formulário PDF, execute as seguintes etapas:

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
* xercesImpl.jar (localizado em &lt;install diretory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBOSS, será necessário substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de API do cliente de formulários com códigos de barras**

Antes de executar programaticamente uma operação de serviço de formulários com códigos de barras, é necessário criar um cliente de serviço Forms com códigos de barras. Se estiver usando a API do Java, crie um objeto `BarcodedFormsServiceClient` . Se estiver usando a API do serviço da Web de formulários com códigos de barras, crie um objeto `BarcodedFormsServiceService`.

**Obter um formulário PDF que contém dados com códigos de barras**

Você deve obter um formulário PDF que contenha um código de barras que tenha sido preenchido com dados do usuário.

**Decodificar os dados do formulário PDF**

Depois de obter um formulário PDF (ou imagem) contendo um código de barras, é possível decodificar os dados. O serviço Forms com códigos de barras oferece suporte para os seguintes tipos de códigos de barras:

* códigos de barras PDF417.
* Códigos de barras da matriz de dados.
* Códigos de barras do código QR.
* Códigos de barras Codabar.
* Códigos de barras do código 128.
* Códigos de barras do código 39.
* Códigos de barras EAN-13.
* Códigos de barras EAN-8.

A entrada do conjunto de caracteres como hexadecimal na API de decodificação implica que o conteúdo do código de barras é codificado como uma sequência de caracteres hexadecimal. Por exemplo, se UTF-8 for especificado como a Codificação de caractere no formulário e Hex for especificado na operação de decodificação, o conteúdo do código de barras será codificado como uma string hexadecimal no elemento &lt; `xb:content` na saída decodificada. Você pode converter esse valor hexadecimal para obter o conteúdo original criando a lógica do aplicativo no aplicativo cliente.

**Converter os dados em uma fonte de dados XML**

Após decodificar os dados do formulário, é possível convertê-los em dados XDP ou XFDF. Por exemplo, suponha que você deseja importar os dados para outro formulário. Para importar os dados para um formulário XFA, é necessário converter os dados em dados XDP. Para obter informações, consulte [Importando dados do formulário](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Processar os dados decodificados**

Você pode processar os dados convertidos para atender às suas necessidades de negócios. Por exemplo, após decodificar e converter os dados, é possível salvá-los em um arquivo, armazená-los em um banco de dados corporativo, preencher outro formulário e assim por diante. Esta seção discute como salvar os dados convertidos como um arquivo XML.

>[!NOTE]
>
>O serviço de formulários com códigos de barras não decodifica os dados do código de barras quando o delimitador de linha e os parâmetros delimitadores de campo têm o mesmo valor

**Consulte também:**

[Decodificar dados de formulário com código de barras usando a API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodificar dados de formulário com código de barras usando a API do serviço da Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API Java {#decode-barcoded-form-data-using-the-java-api}

Decode dados de formulário usando a API de formulários com códigos de barras (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente no caminho da classe do seu projeto Java.

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Crie um objeto `BarcodedFormsServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Obter um formulário PDF que contém dados com códigos de barras

   * Crie um objeto `java.io.FileInputStream` que represente o formulário PDF que contém dados com códigos de barras usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando o método `BarcodedFormsServiceClient` do objeto e passando os seguintes valores:`decode`

   * O objeto `com.adobe.idp.Document` que contém o formulário PDF.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras PDF417 deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras da matriz de dados deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras QR deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras de codabar deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras 128 deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras 39 deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras EAN-13 deve ser decodificado.
   * Um objeto `java.lang.Boolean` que especifica se um código de barras EAN-8 deve ser decodificado.
   * Um valor de enumeração `com.adobe.livecycle.barcodedforms.CharSet` que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   O método `decode` retorna um objeto `org.w3c.dom.Document` que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o método `BarcodedFormsServiceClient` do objeto `extractToXML` e transmitindo os seguintes valores:

   * O objeto `org.w3c.dom.Document` que contém dados decodificados (certifique-se de usar o valor de retorno do método `decode`).
   * Um valor de enumeração `com.adobe.livecycle.barcodedforms.Delimiter` que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * Um valor de enumeração `com.adobe.livecycle.barcodedforms.Delimiter` que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * Um valor de enumeração `com.adobe.livecycle.barcodedforms.XMLFormat` que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O método `extractToXML` retorna um objeto `java.util.List` em que cada elemento é um objeto `org.w3c.dom.Document`. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então haverá quatro elementos no objeto `java.util.List` retornado.

1. Processar os dados decodificados

   * Itere pelo objeto `java.util.List` para obter cada objeto `org.w3c.dom.Document` localizado na lista.
   * Para cada elemento na lista, converta o objeto `org.w3c.dom.Document` em um objeto `com.adobe.idp.Document`. (A lógica do aplicativo que converte um objeto `org.w3c.dom.Document` em um objeto `com.adobe.idp.Document` é mostrada nos dados do formulário com código de barras Decodificação usando o exemplo da API Java).
   * Salve os dados XML como um arquivo XML, chamando `com.adobe.idp.Document` o `copyToFile` do objeto e transmitindo um objeto File que representa o arquivo XML.

**Consulte também:**

[Início rápido (modo SOAP): Decodificação de dados de formulário com código de barras usando a API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificar dados de formulário com código de barras usando a API do serviço da Web {#decode-barcoded-form-data-using-the-web-service-api}

Decode dados de formulário usando a API de formulários com códigos de barras (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL do serviço de formulários com códigos de barras. Para obter informações, consulte [Chamar AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Faça referência ao assembly do cliente Microsoft .NET. Para obter informações, consulte &quot;Fazendo referência ao assembly do cliente .NET&quot; em [Invocando AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Criar um objeto de API do cliente de formulários com códigos de barras

   Usando o conjunto de clientes Microsoft .NET que consome o WSDL do serviço de formulários com códigos de barras, crie um objeto `BarcodedFormsServiceService` chamando seu construtor padrão.

1. Obter um formulário PDF que contém dados com códigos de barras

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que contém um código de barras.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` ao conteúdo da matriz de bytes.

1. Decodificar os dados do formulário PDF

   Decode os dados do formulário chamando o método `BarcodedFormsServiceService` do objeto e passando os seguintes valores:`decode`

   * O objeto `BLOB` que contém o formulário PDF.
   * Um objeto `Boolean` que especifica se um código de barras PDF417 deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras da matriz de dados deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras QR deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras de codabar deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras 128 deve ser decodificado.
   * Um objeto `Bolean` que especifica se um código de barras 39 deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras EAN-13 deve ser decodificado.
   * Um objeto `Boolean` que especifica se um código de barras EAN-8 deve ser decodificado.
   * Um valor de enumeração `CharSet` que especifica o valor de codificação do conjunto de caracteres usado no código de barras.

   O método `decode` retorna um valor de string que contém dados de formulário decodificados.

1. Converter os dados em uma fonte de dados XML

   Converta os dados decodificados em dados XDP ou XFDF chamando o método `BarcodedFormsServiceService` do objeto `extractToXML` e transmitindo os seguintes valores:

   * Um valor de string que contém dados decodificados (certifique-se de usar o valor de retorno do método `decode`).
   * Um valor de enumeração `Delimiter` que especifica o delimitador de linha. É recomendável especificar `Delimiter.Carriage_Return`.
   * Um valor de enumeração `Delimiter` que especifica o delimitador de campo. Por exemplo, especifique `Delimiter.Tab`.
   * Um valor de enumeração `XMLFormat` que especifica se os dados do código de barras devem ser convertidos em dados XML XDP ou XFDF. Por exemplo, especifique `XMLFormat.XDP` para converter os dados em dados XDP.

   >[!NOTE]
   >
   >Não especifique os mesmos valores para os parâmetros delimitador de linha e delimitador de campo.

   O método `extractToXML` retorna uma matriz `Object` onde cada elemento é uma instância `BLOB`. Há um elemento separado para cada código de barras localizado no formulário. Ou seja, se houver quatro códigos de barras no formulário, então há quatro elementos na matriz `Object` retornada.

1. Processar os dados decodificados

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `encryptPDFUsingPassword`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `binaryData`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
