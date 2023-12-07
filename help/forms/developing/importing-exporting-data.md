---
title: Importação e Exportação de Dados
description: Use o serviço de Integração de dados de formulário para importar dados em um formulário PDF e exportar dados de um formulário PDF usando a API Java e a API do serviço Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2754'
ht-degree: 0%

---

# Importação e Exportação de Dados {#importing-and-exporting-data}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Sobre o serviço de integração de dados de formulário {#about-the-form-data-integration-service}

O serviço de Integração de dados de formulário pode importar dados para um formulário PDF e exportar dados de um formulário PDF. As operações de importação e exportação suportam dois tipos de PDF forms:

* Um formulário do Acrobat (criado no Acrobat) é um documento PDF que contém campos de formulário.
* Um formulário XML Adobe (criado no Designer) é um documento PDF que está em conformidade com a XML Adobe XML XML Forms Architecture (XFA).

Dependendo do tipo de formulário PDF, os dados de formulário podem existir em um dos seguintes formatos:

* Um arquivo XFDF, que é uma versão XML do formato de dados de formulário do Acrobat.
* Um arquivo XDP, que é um arquivo XML que contém definições de campo de formulário. Ele também pode conter dados de campo de formulário e um arquivo PDF incorporado. Um arquivo XDP gerado pelo Designer só pode ser usado se ele transportar um documento PDF incorporado codificado em base 64.

Você pode realizar essas tarefas usando o serviço de Integração de dados de formulário:

* Importar dados para o PDF forms. Para obter informações, consulte [Importação de dados do formulário](importing-exporting-data.md#importing-form-data).
* Exportar dados do PDF forms. Para obter informações, consulte [Exportar dados do formulário](importing-exporting-data.md#exporting-form-data).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Importação de dados do formulário {#importing-form-data}

Você pode importar dados de formulário para PDF forms interativos usando o serviço de Integração de dados de formulário. Um formulário PDF interativo é um documento PDF que contém um ou mais campos para coletar informações de um usuário ou exibir informações personalizadas. O serviço de Integração de dados de formulário não oferece suporte a cálculos, validação ou scripts de formulário.

Para importar dados para um formulário criado no Designer, você deve fazer referência a uma fonte de dados XDP XML válida. Considere o exemplo de formulário de solicitação de hipoteca a seguir.

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

Para importar valores de dados para este formulário, você deve ter uma fonte de dados XDP XML válida que corresponda ao formulário. Não é possível usar uma fonte de dados XML arbitrária para importar dados em um formulário usando o serviço de Integração de dados de formulário. A diferença entre uma fonte de dados XML arbitrária e uma fonte de dados XML XDP é que uma fonte de dados XDP está em conformidade com a XML Forms Architecture (XFA). O XML a seguir representa uma fonte de dados XML XDP que corresponde ao exemplo de formulário de aplicativo de hipoteca.

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

1. Incluir arquivos de projeto.
1. Criar um cliente do serviço de Integração de dados de formulário.
1. Referencie um formulário de PDF.
1. Fazer referência a uma fonte de dados XML.
1. Importe dados no formulário PDF.
1. Salve o formulário PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do serviço de Integração de dados de formulário**

Antes de importar dados programaticamente para uma API do cliente do formulário PDF, você deve criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário de PDF**

Para importar dados para um formulário PDF, você deve fazer referência a um formulário XML criado no Designer ou a um formulário Acrobat criado no Acrobat.

**Fazer referência a uma fonte de dados XML**

Para importar dados de formulário, você deve consultar uma fonte de dados válida. Para importar dados para um formulário XML XFA criado no Designer, você deve usar uma fonte de dados XML XDP. Se você fizer referência a um formulário do Acrobat, deverá usar uma fonte de dados XFDF. Para cada campo para o qual você deseja importar dados, um valor deve ser especificado. Se um elemento na fonte de dados XML não corresponder a um campo no formulário, então o elemento será ignorado.

**Importar dados para o formulário PDF**

Depois de referenciar um formulário PDF e uma fonte de dados XML válida, você pode importar os dados para o formulário PDF.

**Salve o formulário de PDF como um arquivo PDF**

Após importar os dados para um formulário, você pode salvá-lo como um arquivo PDF. Depois de salvo como um arquivo PDF, um usuário pode abrir o formulário no Adobe Reader ou Acrobat e vê-lo com os dados importados.

**Consulte também**

[Importar dados do formulário usando a API Java](importing-exporting-data.md#import-form-data-using-the-java-api)

[Importar dados do formulário usando a API do serviço Web](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Integração de Dados de Formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Exportar dados do formulário](importing-exporting-data.md#exporting-form-data)

### Importar dados do formulário usando a API Java {#import-form-data-using-the-java-api}

Importe dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente do serviço de Integração de dados de formulário.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormDataIntegrationClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referencie um formulário de PDF.

   * Criar um `java.io.FileInputStream` usando seu construtor. Transmita um valor de string que especifique o local do formulário PDF.
   * Criar um `com.adobe.idp.Document` objeto que armazena o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém a forma PDF para o construtor.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML que contém dados a serem importados para o formulário.
   * Criar um `com.adobe.idp.Document` objeto que armazena dados de formulário usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém dados de formulário para o construtor.

1. Importe dados no formulário PDF.

   Importe dados para o formulário PDF invocando o `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que armazena o formulário PDF.
   * A variável `com.adobe.idp.Document` objeto que armazena dados de formulário.

   A variável `importData` o método retorna um `com.adobe.idp.Document` objeto que armazena um formulário PDF que contém os dados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é &quot;.PDF&quot;.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `importData` método).

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Início rápido (modo SOAP): importação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Importar dados do formulário usando a API do serviço Web {#import-form-data-using-the-web-service-api}

Importe dados de formulário usando a API de integração de dados de formulário (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente do serviço de Integração de dados de formulário.

   * Criar um `FormDataIntegrationClient` usando seu construtor padrão.
   * Criar um `FormDataIntegrationClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `FormDataIntegrationClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Referencie um formulário de PDF.

   * Criar um `BLOB` usando seu construtor. Este `BLOB` é usado para armazenar o formulário PDF.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que especifique o local do formulário PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. Este `BLOB` objeto é usado para armazenar os dados importados no formulário.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que especifique o local do arquivo XML que contém os dados a serem importados e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Importe dados no formulário PDF.

   Importe dados para o formulário PDF invocando o `FormDataIntegrationClient` do objeto `importData` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que armazena o formulário PDF.
   * A variável `BLOB` objeto que armazena dados de formulário.

   A variável `importData` o método retorna um `BLOB` objeto que armazena um formulário PDF que contém os dados na fonte de dados XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo PDF.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `importData` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Exportar dados do formulário {#exporting-form-data}

Você pode exportar dados de formulário de um formulário PDF interativo usando o serviço Integração de dados de formulário. O formato dos dados exportados depende do tipo de formulário. Se o tipo de formulário for um formulário do Acrobat criado no Acrobat, os dados exportados serão XFDF. Se o tipo de formulário for um formulário XML criado no Designer, os dados exportados serão XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Integração de dados de formulário, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para exportar dados de formulário de um formulário PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Criar um cliente do serviço de Integração de dados de formulário.
1. Referencie um formulário de PDF.
1. Exporte dados do formulário PDF.
1. Salve os dados exportados como um arquivo XML.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente do serviço de Integração de dados de formulário**

Antes de importar dados programaticamente para uma API formClient de PDF, você deve criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço. Para obter informações, [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

**Referência a um formulário de PDF**

Para exportar dados de um formulário PDF, você deve referenciar o formulário PDF que foi criado no Designer ou no Acrobat e que contém dados de formulário. Se tentar exportar dados de um formulário PDF vazio, você obterá um esquema XML vazio.

**Exportar dados do formulário PDF**

Depois de referenciar um formulário PDF que contém dados de formulário, você pode exportar os dados do formulário. Os dados são exportados em um esquema XML baseado no formulário.

**Salvar os dados do formulário como um arquivo XML**

Após exportar os dados do formulário, você pode salvá-los como um arquivo XML. Depois de salvo como um arquivo XML, você pode abrir o arquivo XML em um visualizador de XML para exibir os dados do formulário.

**Consulte também**

[Exportar dados do formulário usando a API Java](importing-exporting-data.md#export-form-data-using-the-java-api)

[Exportar dados do formulário usando a API do serviço Web](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Integração de Dados de Formulário](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[Importação de dados do formulário](importing-exporting-data.md#importing-form-data)

### Exportar dados do formulário usando a API Java {#export-form-data-using-the-java-api}

Exporte dados de formulário usando a API de integração de dados de formulário (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-formdataintegration-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente do serviço de Integração de dados de formulário.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormDataIntegrationClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referencie um formulário de PDF.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo um valor de string que especifica o local do formulário PDF que contém os dados a serem exportados.
   * Criar um `com.adobe.idp.Document` objeto que armazena o formulário PDF usando o `com.adobe.idp.Document` construtor. Passe o `java.io.FileInputStream` objeto que contém a forma PDF para o construtor.

1. Exporte dados do formulário PDF.

   Exporte dados do formulário invocando o `FormDataIntegrationClient` do objeto `exportData` e transmita o `com.adobe.idp.Document` objeto que armazena o formulário PDF. Este método retorna um valor de `com.adobe.idp.Document` objeto que armazena dados de formulário como um esquema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é XML.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `exportData` método).

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Início rápido (modo SOAP): exportação de dados de formulário usando a API Java](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Exportar dados do formulário usando a API do serviço Web {#export-form-data-using-the-web-service-api}

Exporte dados de formulário usando a API de integração de dados de formulário (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente do serviço de Integração de dados de formulário.

   * Criar um `FormDataIntegrationClient` usando seu construtor padrão.
   * Criar um `FormDataIntegrationClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `FormDataIntegrationClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormDataIntegrationClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `FormDataIntegrationClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Referencie um formulário de PDF.

   * Criar um `BLOB` usando seu construtor. Este `BLOB` é usado para armazenar o formulário de PDF do qual os dados são exportados.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que especifique o local do formulário PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Exporte dados do formulário PDF.

   Importe dados para o formulário PDF invocando o `FormDataIntegrationClient` do objeto `exportData` e transmita o `BLOB` objeto que armazena o formulário PDF. Este método retorna um valor de `BLOB` objeto que armazena dados de formulário como um esquema XML.

1. Salve o formulário PDF como um arquivo PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `exportData` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](importing-exporting-data.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
