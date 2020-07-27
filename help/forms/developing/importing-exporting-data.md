---
title: Importação e exportação de dados
seo-title: Importação e exportação de dados
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 0%

---


# Importação e exportação de dados {#importing-and-exporting-data}

## Sobre o serviço de integração de dados de formulário {#about-the-form-data-integration-service}

O serviço de Integração de dados de formulário pode importar dados para um formulário PDF e exportar dados de um formulário PDF. As operações de importação e de exportação suportam dois tipos de PDF forms:

* Um formulário do Acrobat (criado no Acrobat) é um documento PDF que contém campos de formulário.
* Um formulário Adobe XML (criado no Designer) é um documento PDF que está em conformidade com o XML Adobe XML Forms Architecture (XFA).

Os dados do formulário podem existir em um dos seguintes formatos, dependendo do tipo de formulário PDF:

* Um arquivo XFDF, que é uma versão XML do formato de dados de formulário do Acrobat.
* Um arquivo XDP, que é um arquivo XML que contém definições de campos de formulário. Ele também pode conter dados de campo de formulário e um arquivo PDF incorporado. Um arquivo XDP gerado pelo Designer só pode ser usado se ele tiver um documento PDF codificado em base 64 incorporado.

É possível realizar essas tarefas usando o serviço de Integração de dados de formulário:

* Importe dados para PDF forms. Para obter informações, consulte [Importação de dados](importing-exporting-data.md#importing-form-data)do formulário.
* Exportar dados de PDF forms. Para obter informações, consulte [Exportação de dados](importing-exporting-data.md#exporting-form-data)de formulário.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de dados de formulário {#importing-form-data}

É possível importar dados de formulário para PDF forms interativos usando o serviço de Integração de dados de formulário. Um formulário PDF interativo é um documento PDF que contém um ou mais campos para coletar informações de um usuário ou para exibir informações personalizadas. O serviço de Integração de dados de formulário não oferece suporte a cálculos de formulário, validação ou script.

Para importar dados para um formulário criado no Designer, é necessário referenciar uma fonte de dados XML XDP válida. Considere o seguinte formulário de aplicativo hipotecário de exemplo.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de dados para esse formulário, é necessário ter uma fonte de dados XML XDP válida que corresponda ao formulário. Não é possível usar uma fonte de dados XML arbitrária para importar dados para um formulário usando o serviço de Integração de dados de formulário. A diferença entre uma fonte de dados XML arbitrária e uma fonte de dados XML XDP é que uma fonte de dados XDP está em conformidade com a Arquitetura de formulários XML (XFA). O XML a seguir representa uma fonte de dados XML XDP que corresponde ao formulário de aplicativo hipotecário de exemplo.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para importar dados de formulário para um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de Integração de Dados de Formulário.
1. Consulte um formulário PDF.
1. Referência a uma fonte de dados XML.
1. Importe dados para o formulário PDF.
1. Salve o formulário PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se AEM Forms forem implantados em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um cliente de serviço de Integração de Dados de Formulário**

Antes de poder importar dados de forma programática para uma API do cliente de formulário PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Configuração de propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.

**Referência a um formulário PDF**

Para importar dados para um formulário PDF, é necessário fazer referência a um formulário XML criado no Designer ou a um formulário do Acrobat criado no Acrobat.

**Referência a uma fonte de dados XML**

Para importar dados de formulário, é necessário referenciar uma fonte de dados válida. Para importar dados para um formulário XML XFA criado no Designer, é necessário usar uma fonte de dados XML XDP. Se você fizer referência a um formulário do Acrobat, deverá usar uma fonte de dados XFDF. Para cada campo para o qual você deseja importar dados, um valor deve ser especificado. Se um elemento localizado na fonte de dados XML não corresponder a um campo no formulário, o elemento será ignorado.

**Importar dados para o formulário PDF**

Depois de referenciar um formulário PDF e uma fonte de dados XML válida, é possível importar os dados para o formulário PDF.

**Salvar o formulário PDF como um arquivo PDF**

Depois de importar dados para um formulário, é possível salvar o formulário como um arquivo PDF. Depois de salvo como um arquivo PDF, um usuário pode abrir o formulário no Adobe Reader ou no Acrobat e ver o formulário com os dados importados.

**Consulte também:**

[Importar dados do formulário usando a API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportação de dados de formulário](importing-exporting-data.md#exporting-form-data)

### Importar dados do formulário usando a API Java {#import-form-data-using-the-java-api}

Importe dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormDataIntegrationClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um formulário PDF.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor. Passe um valor de string que especifica o local do formulário PDF.
   * Crie um `com.adobe.idp.Document` objeto que armazene o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o formulário PDF para o construtor.

1. Referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e passe um valor de string que especifique o local do arquivo XML que contém os dados a serem importados para o formulário.
   * Crie um `com.adobe.idp.Document` objeto que armazene dados de formulário usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém dados de formulário para o construtor.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o método do `FormDataIntegrationClient` objeto `importData` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que armazena o formulário PDF.
   * O `com.adobe.idp.Document` objeto que armazena dados de formulário.

   O `importData` método retorna um `com.adobe.idp.Document` objeto que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é &quot;.PDF&quot;.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `importData` método).

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Start rápido (modo SOAP): Importação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar dados de formulário usando a API de serviço da Web {#import-form-data-using-the-web-service-api}

Importe dados de formulário usando a API de integração de dados de formulário (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um `FormDataIntegrationClient` objeto usando seu construtor padrão.
   * Crie um `FormDataIntegrationClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `FormDataIntegrationClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um formulário PDF.

   * Crie um `BLOB` objeto usando seu construtor. Esse `BLOB` objeto é usado para armazenar o formulário PDF.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Referência a uma fonte de dados XML.

   * Crie um `BLOB` objeto usando seu construtor. Esse `BLOB` objeto é usado para armazenar os dados importados no formulário.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que especifica o local do arquivo XML que contém os dados a serem importados e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o método do `FormDataIntegrationClient` objeto `importData` e transmitindo os seguintes valores:

   * O `BLOB` objeto que armazena o formulário PDF.
   * O `BLOB` objeto que armazena dados de formulário.

   O `importData` método retorna um `BLOB` objeto que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa a localização do arquivo do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `importData` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportação de dados de formulário {#exporting-form-data}

É possível exportar dados de formulário de um formulário PDF interativo usando o serviço de Integração de dados de formulário. O formato dos dados exportados depende do tipo de formulário. Se o tipo de formulário for um formulário do Acrobat criado no Acrobat, os dados exportados serão XFDF. Se o tipo de formulário for um formulário XML criado no Designer, os dados exportados serão XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar dados de formulário de um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Criar um cliente de serviço de Integração de Dados de Formulário.
1. Consulte um formulário PDF.
1. Exporte dados do formulário PDF.
1. Salve os dados exportados como um arquivo XML.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se AEM Forms forem implantados em JBoss)

**Criar um cliente de serviço de Integração de Dados de Formulário**

Antes de poder importar dados de forma programática para uma API FormClient do PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, [defina as propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.

**Referência a um formulário PDF**

Para exportar dados de um formulário PDF, é necessário fazer referência a um formulário PDF criado no Designer ou Acrobat e que contenha dados de formulário. Se você tentar exportar dados de um formulário PDF vazio, receberá um schema XML vazio.

**Exportar dados do formulário PDF**

Depois de referenciar um formulário PDF que contém dados de formulário, é possível exportar os dados do formulário. Os dados são exportados dentro de um schema XML baseado no formulário.

**Salvar os dados do formulário como um arquivo XML**

Depois de exportar dados de formulário, é possível salvar os dados como um arquivo XML. Depois de salvo como um arquivo XML, é possível abrir o arquivo XML em um visualizador XML para visualização dos dados do formulário.

**Consulte também:**

[Exportar dados de formulário usando a API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importação de dados de formulário](importing-exporting-data.md#importing-form-data)

### Exportar dados de formulário usando a API Java {#export-form-data-using-the-java-api}

Exporte dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormDataIntegrationClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um formulário PDF.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e passe um valor de string que especifique o local do formulário PDF que contém os dados a serem exportados.
   * Crie um `com.adobe.idp.Document` objeto que armazene o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o formulário PDF para o construtor.

1. Exporte dados do formulário PDF.

   Exporte dados de formulário chamando o `FormDataIntegrationClient` método do objeto `exportData` e passe o `com.adobe.idp.Document` objeto que armazena o formulário PDF. Esse método retorna um `com.adobe.idp.Document` objeto que armazena dados de formulário como um schema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `java.io.File` objeto e verifique se a extensão do arquivo é XML.
   * Chame o `Document` método do `copyToFile` objeto para copiar o conteúdo do `Document` objeto para o arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `exportData` método).

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Start rápido (modo SOAP): Exportação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar dados de formulário usando a API de serviço da Web {#export-form-data-using-the-web-service-api}

Exporte dados de formulário usando a API de integração de dados de formulário (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um `FormDataIntegrationClient` objeto usando seu construtor padrão.
   * Crie um `FormDataIntegrationClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `FormDataIntegrationClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um formulário PDF.

   * Crie um `BLOB` objeto usando seu construtor. Esse `BLOB` objeto é usado para armazenar o formulário PDF a partir do qual os dados são exportados.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Exporte dados do formulário PDF.

   Importe dados para o formulário PDF chamando o `FormDataIntegrationClient` método do `exportData` objeto e passe o `BLOB` objeto que armazena o formulário PDF. Esse método retorna um `BLOB` objeto que armazena dados de formulário como um schema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `exportData` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo XML, chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
