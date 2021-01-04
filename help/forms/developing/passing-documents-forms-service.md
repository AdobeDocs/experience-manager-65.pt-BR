---
title: Transmissão de Documentos ao FormsService
seo-title: Transmissão de Documentos ao FormsService
description: 'Passe um objeto com.adobe.idp.Documento que contenha o design de formulário ao serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto com.adobe.idp.Documento. '
seo-description: Passe um objeto com.adobe.idp.Documento que contenha o design de formulário ao serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto com.adobe.idp.Documento.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 0%

---


# Transmissão de Documentos ao serviço Forms {#passing-documents-to-the-formsservice}

O serviço AEM Forms renderiza PDF forms interativos para dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que geralmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, é possível enviar um objeto `com.adobe.idp.Document` que contenha o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto `com.adobe.idp.Document`.

Uma vantagem de passar um objeto `com.adobe.idp.Document` para o serviço Forms é que outras operações de serviço retornam uma instância `com.adobe.idp.Document`. Ou seja, você pode obter uma instância `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado em um nó do Content Services (obsoleto) chamado `/Company Home/Form Designs`, como mostrado na ilustração a seguir.

Você pode recuperar de forma programática o Loan.xdp do Content Services (obsoleto) e passar o arquivo XDP para o serviço Forms em um objeto `com.adobe.idp.Document`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido do Content Services (obsoleto) (obsoleto) para o serviço Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms e do Documento Management Client.
1. Recupere o design de formulário do Content Services (obsoleto).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados do formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto de API do Forms e do Documento Management Client**

Antes de executar programaticamente uma operação de API de serviço da Forms, crie um objeto de API do Forms Client. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto da API de Gerenciamento de Documentos.

**Recuperar o design de formulário do Content Services (obsoleto)**

Recupere o arquivo XDP do Content Services (obsoleto) usando o Java ou a API de serviço da Web. O arquivo XDP é retornado em uma instância `com.adobe.idp.Document` (ou em uma instância `BLOB` se você estiver usando serviços da Web). Você pode passar a instância `com.adobe.idp.Document` para o serviço Forms.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário interativo, passe a instância `com.adobe.idp.Document` que foi retornada do Content Services (obsoleto) para o serviço Forms.

>[!NOTE]
>
>Você pode enviar um `com.adobe.idp.Document` que contenha o design de formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitam um objeto `com.adobe.idp.Document` que contém um design de formulário.

**Executar uma ação com o fluxo de dados do formulário**

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário no navegador da Web. No entanto, um aplicativo de desktop geralmente salva o formulário como um arquivo PDF.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Passe documentos para o serviço Forms usando a API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmita um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço Forms e a API do Content Services (obsoleto) (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms e do Documento Management Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definição das propriedades de ligação](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar o design de formulário do Content Services (obsoleto)

   Chame o método `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   O método `retrieveContent` retorna um objeto `CRCResult` que contém o arquivo XDP. Obtenha uma instância `com.adobe.idp.Document` invocando o método `CRCResult` do objeto `getDocument`.

1. Renderizar um formulário PDF interativo

   Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o design de formulário recuperado do Content Services (obsoleto).
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read`. Passe a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Start rápido (modo SOAP): Transmissão de documentos para o serviço Forms usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Passe documentos para o serviço Forms usando a API de serviço da Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passe um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço Forms e a Content Services (obsoleto) API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Como este aplicativo cliente chama dois serviços da AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de Documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como o tipo de dados `BLOB` é comum a ambas as referências de serviço, qualifique totalmente o tipo de dados `BLOB` ao usá-lo. No start rápido do serviço da Web correspondente, todas as instâncias `BLOB` são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost`pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do Forms e do Documento Management Client

   * Crie um objeto `FormsServiceClient` usando seu construtor padrão.
   * Crie um objeto `FormsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `FormsServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita estas etapas para o cliente de serviço `DocumentManagementServiceClient`.

1. Recuperar o design de formulário do Content Services (obsoleto)

   Recupere o conteúdo chamando o método `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída de string que armazena o valor do link de navegação.
   * Um parâmetro de saída `BLOB` que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * Um parâmetro de saída `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` que armazena atributos de conteúdo.
   * Um parâmetro de saída `CRCResult`. Em vez de usar esse objeto, você pode usar o parâmetro de saída `BLOB` para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * Um objeto `BLOB` que contém o design de formulário recuperado do Content Services (obsoleto).
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `BLOB` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um objeto `Map` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um parâmetro de saída longo que é usado para armazenar a contagem de páginas.
   * Um parâmetro de saída de string usado para armazenar o valor de localidade.
   * Um parâmetro de saída `FormsResult` usado para armazenar o formulário PDF interativo `.`

   O método `renderPDFForm2` retorna um objeto `FormsResult` que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um objeto `BLOB` que contenha dados de formulário obtendo o valor do campo `FormsResult` `outputContent` do objeto.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF interativo e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` recuperado do objeto `FormsResult`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
