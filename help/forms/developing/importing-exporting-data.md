---
title: Importação e exportação de dados
seo-title: Importação e exportação de dados
description: Use o serviço de Integração de dados de formulário para importar dados para um formulário PDF e exportar dados de um formulário PDF usando a API Java e a API de serviço da Web.
seo-description: Use o serviço de Integração de dados de formulário para importar dados para um formulário PDF e exportar dados de um formulário PDF usando a API Java e a API de serviço da Web.
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '2810'
ht-degree: 0%

---


# Importação e exportação de dados {#importing-and-exporting-data}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

## Sobre o Form Data Integration Service {#about-the-form-data-integration-service}

O serviço de Integração de dados de formulário pode importar dados para um formulário PDF e exportar dados de um formulário PDF. As operações de importação e de exportação suportam dois tipos de PDF forms:

* Um formulário Acrobat (criado no Acrobat) é um documento PDF que contém campos de formulário.
* Um formulário Adobe XML (criado no Designer) é um documento PDF que está em conformidade com a XML Adobe XML Forms Architecture (XFA).

Os dados do formulário podem existir em um dos seguintes formatos, dependendo do tipo de formulário PDF:

* Um arquivo XFDF, que é uma versão XML do formato de dados de formulário Acrobat.
* Um arquivo XDP, que é um arquivo XML que contém definições de campos de formulário. Ele também pode conter dados de campo de formulário e um arquivo PDF incorporado. Um arquivo XDP gerado pelo Designer só pode ser usado se ele tiver um documento PDF codificado em base 64 incorporado.

É possível realizar essas tarefas usando o serviço de Integração de dados de formulário:

* Importe dados para PDF forms. Para obter informações, consulte [Importando dados do formulário](importing-exporting-data.md#importing-form-data).
* Exportar dados de PDF forms. Para obter informações, consulte [Exportando dados do formulário](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importando dados de formulário {#importing-form-data}

É possível importar dados de formulário para PDF forms interativos usando o serviço de Integração de dados de formulário. Um formulário PDF interativo é um documento PDF que contém um ou mais campos para coletar informações de um usuário ou para exibir informações personalizadas. O serviço de Integração de dados de formulário não oferece suporte a cálculos de formulário, validação ou script.

Para importar dados para um formulário criado no Designer, é necessário referenciar uma fonte de dados XML XDP válida. Considere o seguinte formulário de aplicativo hipotecário de exemplo.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de dados para esse formulário, é necessário ter uma fonte de dados XML XDP válida que corresponda ao formulário. Não é possível usar uma fonte de dados XML arbitrária para importar dados para um formulário usando o serviço de Integração de dados de formulário. A diferença entre uma fonte de dados XML arbitrária e uma fonte de dados XML XDP é que uma fonte de dados XDP está em conformidade com a Arquitetura Forms XML (XFA). O XML a seguir representa uma fonte de dados XML XDP que corresponde ao formulário de aplicativo hipotecário de exemplo.

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
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de serviço de Integração de Dados de Formulário**

Antes de poder importar dados de forma programática para uma API do cliente de formulário PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário PDF**

Para importar dados para um formulário PDF, é necessário fazer referência a um formulário XML criado no Designer ou a um formulário Acrobat criado no Acrobat.

**Referência a uma fonte de dados XML**

Para importar dados de formulário, é necessário referenciar uma fonte de dados válida. Para importar dados para um formulário XML XFA criado no Designer, é necessário usar uma fonte de dados XML XDP. Se você fizer referência a um formulário Acrobat, deverá usar uma fonte de dados XFDF. Para cada campo para o qual você deseja importar dados, um valor deve ser especificado. Se um elemento localizado na fonte de dados XML não corresponder a um campo no formulário, o elemento será ignorado.

**Importar dados para o formulário PDF**

Depois de referenciar um formulário PDF e uma fonte de dados XML válida, é possível importar os dados para o formulário PDF.

**Salvar o formulário PDF como um arquivo PDF**

Depois de importar dados para um formulário, é possível salvar o formulário como um arquivo PDF. Depois de salvo como um arquivo PDF, um usuário pode abrir o formulário no Adobe Reader ou no Acrobat e ver o formulário com os dados importados.

**Consulte também:**

[Importar dados do formulário usando a API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportação de dados de formulário](importing-exporting-data.md#exporting-form-data)

### Importar dados do formulário usando a API Java {#import-form-data-using-the-java-api}

Importe dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormDataIntegrationClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um formulário PDF.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local do formulário PDF.
   * Crie um objeto `com.adobe.idp.Document` que armazene o formulário PDF usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém o formulário PDF para o construtor.

1. Referência a uma fonte de dados XML.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmita um valor de string que especifica o local do arquivo XML que contém os dados a serem importados para o formulário.
   * Crie um objeto `com.adobe.idp.Document` que armazene dados de formulário usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém dados de formulário para o construtor.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o método `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que armazena o formulário PDF.
   * O objeto `com.adobe.idp.Document` que armazena dados de formulário.

   O método `importData` retorna um objeto `com.adobe.idp.Document` que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é &quot;.PDF&quot;.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `importData`).

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Start rápido (modo SOAP): Importação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar dados de formulário usando a API de serviço da Web {#import-form-data-using-the-web-service-api}

Importe dados de formulário usando a API de integração de dados de formulário (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um objeto `FormDataIntegrationClient` usando seu construtor padrão.
   * Crie um objeto `FormDataIntegrationClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `FormDataIntegrationClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um formulário PDF.

   * Crie um objeto `BLOB` usando seu construtor. Esse objeto `BLOB` é usado para armazenar o formulário PDF.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Referência a uma fonte de dados XML.

   * Crie um objeto `BLOB` usando seu construtor. Esse objeto `BLOB` é usado para armazenar os dados importados no formulário.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do arquivo XML que contém os dados a serem importados e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Importe dados para o formulário PDF.

   Importe dados para o formulário PDF chamando o método `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * O objeto `BLOB` que armazena o formulário PDF.
   * O objeto `BLOB` que armazena dados de formulário.

   O método `importData` retorna um objeto `BLOB` que armazena um formulário PDF que contém os dados localizados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` que foi retornado pelo método `importData`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` `MTOM` do objeto.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportar dados de formulário {#exporting-form-data}

É possível exportar dados de formulário de um formulário PDF interativo usando o serviço de Integração de dados de formulário. O formato dos dados exportados depende do tipo de formulário. Se o tipo de formulário for um formulário Acrobat criado no Acrobat, os dados exportados serão XFDF. Se o tipo de formulário for um formulário XML criado no Designer, os dados exportados serão XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

**Criar um cliente de serviço de Integração de Dados de Formulário**

Antes de poder importar dados de forma programática para uma API FormClient do PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, [Configuração de propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário PDF**

Para exportar dados de um formulário PDF, é necessário fazer referência a um formulário PDF criado no Designer ou Acrobat que contenha dados do formulário. Se você tentar exportar dados de um formulário PDF vazio, receberá um schema XML vazio.

**Exportar dados do formulário PDF**

Depois de referenciar um formulário PDF que contém dados de formulário, é possível exportar os dados do formulário. Os dados são exportados dentro de um schema XML baseado no formulário.

**Salvar os dados do formulário como um arquivo XML**

Depois de exportar dados de formulário, é possível salvar os dados como um arquivo XML. Depois de salvo como um arquivo XML, é possível abrir o arquivo XML em um visualizador XML para visualização dos dados do formulário.

**Consulte também:**

[Exportar dados de formulário usando a API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportar dados de formulário usando a API de serviço da Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de integração de dados de formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importação de dados de formulário](importing-exporting-data.md#importing-form-data)

### Exportar dados de formulário usando a API Java {#export-form-data-using-the-java-api}

Exporte dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormDataIntegrationClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um formulário PDF.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmita um valor de string que especifica o local do formulário PDF que contém os dados a serem exportados.
   * Crie um objeto `com.adobe.idp.Document` que armazene o formulário PDF usando o construtor `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém o formulário PDF para o construtor.

1. Exporte dados do formulário PDF.

   Exporte dados de formulário chamando o método `FormDataIntegrationClient` do objeto `exportData` e passe o objeto `com.adobe.idp.Document` que armazena o formulário PDF. Esse método retorna um objeto `com.adobe.idp.Document` que armazena dados de formulário como um schema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é XML.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo (certifique-se de usar o objeto `Document` retornado pelo método `exportData`).

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Start rápido (modo SOAP): Exportação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar dados de formulário usando a API de serviço da Web {#export-form-data-using-the-web-service-api}

Exporte dados de formulário usando a API de integração de dados de formulário (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de Integração de Dados de Formulário.

   * Crie um objeto `FormDataIntegrationClient` usando seu construtor padrão.
   * Crie um objeto `FormDataIntegrationClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `FormDataIntegrationClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um formulário PDF.

   * Crie um objeto `BLOB` usando seu construtor. Esse objeto `BLOB` é usado para armazenar o formulário PDF a partir do qual os dados são exportados.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do formulário PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Exporte dados do formulário PDF.

   Importe dados para o formulário PDF chamando o método `FormDataIntegrationClient` do objeto `exportData` e passe o objeto `BLOB` que armazena o formulário PDF. Esse método retorna um objeto `BLOB` que armazena dados de formulário como um schema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` que foi retornado pelo método `exportData`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` `MTOM` do objeto.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo XML chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
