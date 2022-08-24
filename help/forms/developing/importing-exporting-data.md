---
title: Importação e exportação de dados
seo-title: Importing and Exporting Data
description: Use o serviço de Integração de dados de formulário para importar dados para um formulário PDF e exportar dados de um formulário PDF usando a API do Java e a API do serviço da Web.
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 0%

---

# Importação e exportação de dados {#importing-and-exporting-data}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Sobre o serviço de integração de dados de formulário {#about-the-form-data-integration-service}

O serviço de Integração de dados de formulário pode importar dados para um formulário PDF e exportar dados de um formulário PDF. As operações de importação e exportação são compatíveis com dois tipos de PDF forms:

* Um formulário Acrobat (criado no Acrobat) é um documento PDF que contém campos de formulário.
* Um formulário Adobe XML (criado no Designer) é um documento PDF que está em conformidade com o XML Adobe XML Forms Architecture (XFA).

Os dados do formulário podem existir em um dos seguintes formatos, dependendo do tipo de formulário PDF:

* Um arquivo XFDF, que é uma versão XML do formato de dados de formulário Acrobat.
* Um arquivo XDP, que é um arquivo XML que contém definições de campos de formulário. Ele também pode conter dados de campos de formulário e um arquivo PDF incorporado. Um arquivo XDP gerado pelo Designer só poderá ser usado se ele tiver um documento de PDF codificado em base 64 incorporado.

Você pode realizar essas tarefas usando o serviço de Integração de dados de formulário :

* Importe dados para o PDF forms. Para obter mais informações, consulte [Importação de dados de formulário](importing-exporting-data.md#importing-form-data).
* Exportar dados do PDF forms. Para obter mais informações, consulte [Exportar dados de formulário](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de dados de formulário {#importing-form-data}

É possível importar dados de formulário para o PDF forms interativo usando o serviço de Integração de dados de formulário . Um formulário PDF interativo é um documento PDF que contém um ou mais campos para coletar informações de um usuário ou para exibir informações personalizadas. O serviço Integração de dados de formulário não oferece suporte a cálculos, validação ou scripts de formulários.

Para importar dados para um formulário criado no Designer, é necessário fazer referência a uma fonte de dados XML XDP válida. Considere o seguinte exemplo de formulário de aplicativo de hipoteca.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de dados para esse formulário, é necessário ter uma fonte de dados XML XDP válida que corresponda ao formulário. Não é possível usar uma fonte de dados XML arbitrária para importar dados em um formulário usando o serviço de Integração de dados de formulário . A diferença entre uma fonte de dados XML arbitrária e uma fonte de dados XML XDP é que uma fonte de dados XDP está em conformidade com a XML Forms Architecture (XFA). O XML a seguir representa uma fonte de dados XML XDP que corresponde ao formulário de aplicativo de hipoteca de exemplo.

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
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para importar dados de formulário para um formulário PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Criar um cliente de serviço de Integração de dados de formulário .
1. Referência a um formulário PDF.
1. Faça referência a uma fonte de dados XML.
1. Importe dados para o formulário PDF.
1. Salve o formulário PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de Integração de dados de formulário**

Antes de poder importar dados de forma programática para uma API do cliente do PDF, é necessário criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter mais informações, consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário PDF**

Para importar dados para um formulário PDF, é necessário fazer referência a um formulário XML criado no Designer ou a um formulário Acrobat criado no Acrobat.

**Referência a uma fonte de dados XML**

Para importar dados de formulário, é necessário referenciar uma fonte de dados válida. Para importar dados para um formulário XML XFA criado no Designer, é necessário usar uma fonte de dados XML XDP. Se você fizer referência a um formulário Acrobat, deverá usar uma fonte de dados XFDF. Para cada campo para o qual você deseja importar dados, um valor deve ser especificado. Se um elemento localizado na fonte de dados XML não corresponder a um campo no formulário, o elemento será ignorado.

**Importar dados para o formulário PDF**

Depois de fazer referência a um formulário PDF e uma fonte de dados XML válida, é possível importar os dados para o formulário PDF.

**Salve o formulário PDF como um arquivo PDF**

Depois de importar os dados para um formulário, é possível salvá-lo como um arquivo PDF. Depois de salvo como um arquivo PDF, um usuário pode abrir o formulário no Adobe Reader ou Acrobat e ver o formulário com os dados importados.

**Consulte também**

[Importar dados de formulário usando a API do Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportar dados de formulário](importing-exporting-data.md#exporting-form-data)

### Importar dados de formulário usando a API do Java {#import-form-data-using-the-java-api}

Importe dados do formulário usando a API de integração de dados de formulário (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de dados de formulário .

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormDataIntegrationClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a um formulário PDF.

   * Crie um `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local do formulário PDF.
   * Crie um `com.adobe.idp.Document` que armazena o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o PDF para o construtor.

1. Faça referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML que contém dados a serem importados para o formulário.
   * Crie um `com.adobe.idp.Document` objeto que armazena dados de formulário usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém dados de formulário para o construtor.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` que armazena o formulário PDF.
   * O `com.adobe.idp.Document` que armazena dados de formulário.

   O `importData` método retorna um `com.adobe.idp.Document` objeto que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é &quot;.PDF&quot;.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` para o arquivo (certifique-se de usar a variável `Document` objeto retornado pelo `importData` método ).

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Início rápido (modo SOAP): Importação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar dados de formulário usando a API de serviço da Web {#import-form-data-using-the-web-service-api}

Importe dados do formulário usando a API de integração de dados de formulário (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de serviço de Integração de dados de formulário .

   * Crie um `FormDataIntegrationClient` usando seu construtor padrão.
   * Crie um `FormDataIntegrationClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `FormDataIntegrationClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Referência a um formulário PDF.

   * Crie um `BLOB` usando seu construtor. Essa `BLOB` é usado para armazenar o formulário PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. Essa `BLOB` é usado para armazenar os dados importados para o formulário.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do arquivo XML que contém os dados a serem importados e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * O `BLOB` que armazena o formulário PDF.
   * O `BLOB` que armazena dados de formulário.

   O `importData` método retorna um `BLOB` objeto que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `importData` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` campo.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportar dados de formulário {#exporting-form-data}

É possível exportar dados de formulário de um formulário PDF interativo usando o serviço de Integração de dados de formulário . O formato dos dados exportados depende do tipo de formulário. Se o tipo de formulário for um formulário Acrobat criado no Acrobat, os dados exportados serão XFDF. Se o tipo de formulário for um formulário XML criado no Designer, os dados exportados serão XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar dados de formulário de um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Criar um cliente de serviço de Integração de dados de formulário .
1. Referência a um formulário PDF.
1. Exportar dados do formulário PDF.
1. Salve os dados exportados como um arquivo XML.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente de serviço de Integração de dados de formulário**

Antes de poder importar dados de forma programática para uma API do PDF formClient, é necessário criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário PDF**

Para exportar dados de um formulário PDF, é necessário fazer referência a um formulário PDF criado no Designer ou Acrobat que contenha dados de formulário. Se tentar exportar dados de um formulário PDF vazio, você receberá um esquema XML vazio.

**Exportar dados do formulário PDF**

Depois de fazer referência a um formulário PDF que contém dados de formulário, é possível exportar os dados desse formulário. Os dados são exportados dentro de um esquema XML baseado no formulário.

**Salve os dados do formulário como um arquivo XML**

Após exportar os dados do formulário, é possível salvá-los como um arquivo XML. Depois de salvo como um arquivo XML, você pode abrir o arquivo XML em um visualizador XML para exibir os dados do formulário.

**Consulte também**

[Exportar dados de formulário usando a API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importação de dados de formulário](importing-exporting-data.md#importing-form-data)

### Exportar dados de formulário usando a API Java {#export-form-data-using-the-java-api}

Exporte dados de formulário usando a API de integração de dados de formulário (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de dados de formulário .

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormDataIntegrationClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a um formulário PDF.

   * Crie um `java.io.FileInputStream` ao usar seu construtor e passar um valor de string que especifica o local do formulário PDF que contém dados para exportar.
   * Crie um `com.adobe.idp.Document` que armazena o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém o PDF para o construtor.

1. Exportar dados do formulário PDF.

   Exportar dados de formulário chamando o `FormDataIntegrationClient` do objeto `exportData` e passe o `com.adobe.idp.Document` que armazena o formulário PDF. Esse método retorna um `com.adobe.idp.Document` que armazena dados de formulário como um esquema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é XML.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` para o arquivo (certifique-se de usar a variável `Document` objeto retornado pelo `exportData` método ).

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Início rápido (modo SOAP): Exportação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar dados de formulário usando a API de serviço da Web {#export-form-data-using-the-web-service-api}

Exportar dados de formulário usando a API de integração de dados de formulário (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de serviço de Integração de dados de formulário .

   * Crie um `FormDataIntegrationClient` usando seu construtor padrão.
   * Crie um `FormDataIntegrationClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `FormDataIntegrationClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Referência a um formulário PDF.

   * Crie um `BLOB` usando seu construtor. Essa `BLOB` é usado para armazenar o formulário PDF do qual os dados são exportados.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Exportar dados do formulário PDF.

   Importe dados para o formulário PDF chamando o `FormDataIntegrationClient` do objeto `exportData` e passe o `BLOB` que armazena o formulário PDF. Esse método retorna um `BLOB` que armazena dados de formulário como um esquema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `exportData` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` campo.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
