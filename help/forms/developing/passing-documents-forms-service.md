---
title: Transmissão de documentos ao FormsService
seo-title: Transmissão de documentos ao FormsService
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Transmissão de documentos ao serviço Forms {#passing-documents-to-the-formsservice}

O serviço AEM Forms renderiza formulários PDF interativos para dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que geralmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, é possível passar um `com.adobe.idp.Document` objeto que contenha o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no `com.adobe.idp.Document` objeto.

Uma vantagem de passar um `com.adobe.idp.Document` objeto para o serviço Forms é que outras operações de serviço retornam uma `com.adobe.idp.Document` instância. Ou seja, você pode obter uma `com.adobe.idp.Document` instância de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado em um nó do Content Services (obsoleto) nomeado `/Company Home/Form Designs`, como mostrado na ilustração a seguir.

Você pode recuperar de forma programática o Loan.xdp do Content Services (obsoleto) e passar o arquivo XDP para o serviço Forms em um `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido do Content Services (obsoleto) (obsoleto) para o serviço do Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms e do Document Management Client.
1. Recupere o design de formulário do Content Services (obsoleto).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados do formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto de API do Forms e do Document Management Client**

Antes de executar programaticamente uma operação de API de serviço do Forms, crie um objeto de API do Forms Client. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto da API do Document Management.

**Recuperar o design de formulário do Content Services (obsoleto)**

Recupere o arquivo XDP do Content Services (obsoleto) usando o Java ou a API de serviço da Web. O arquivo XDP é retornado em uma `com.adobe.idp.Document` instância (ou em uma `BLOB` instância se você estiver usando serviços da Web). Em seguida, é possível passar a `com.adobe.idp.Document` instância para o serviço de Formulários.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário interativo, passe a `com.adobe.idp.Document` instância que foi retornada do Content Services (obsoleto) para o serviço Forms.

>[!NOTE]
>
>É possível enviar um formulário `com.adobe.idp.Document` que contenha o design de formulário para o serviço de Formulários. Dois novos métodos nomeados `renderPDFForm2` e `renderHTMLForm2` aceitam um `com.adobe.idp.Document` objeto que contém um design de formulário.

**Executar uma ação com o fluxo de dados do formulário**

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário no navegador da Web. No entanto, um aplicativo de desktop geralmente salva o formulário como um arquivo PDF.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do serviço de formulários](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Transmita documentos para o serviço de formulários usando a API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmita um documento obtido do Content Services (obsoleto) usando o serviço de Formulários e a API do Content Services (obsoleto) (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms e do Document Management Client

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Crie um `DocumentManagementServiceClientImpl` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar o design de formulário do Content Services (obsoleto)

   Chame o método do `DocumentManagementServiceClientImpl` objeto `retrieveContent` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   O `retrieveContent` método retorna um `CRCResult` objeto que contém o arquivo XDP. Obtenha uma `com.adobe.idp.Document` instância chamando o `CRCResult` método do `getDocument` objeto.

1. Renderizar um formulário PDF interativo

   Chame o método do `FormsServiceClient` objeto `renderPDFForm2` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que contém o design de formulário recuperado do Content Services (obsoleto).
   * Um `com.adobe.idp.Document` objeto que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um `com.adobe.idp.Document` objeto vazio.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não deseja especificar opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o método do `InputStream` objeto `read` . Passe a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Início rápido (modo SOAP): Transmissão de documentos ao serviço de formulários usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmita documentos para o serviço de formulários usando a API de serviço da Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmita um documento obtido do Content Services (obsoleto) usando o serviço de Formulários e a Content Services (obsoleto) API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Como esse aplicativo cliente chama dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Formulários: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como o tipo de `BLOB` dados é comum a ambas as referências de serviço, qualifice totalmente o tipo de `BLOB` dados ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as `BLOB` instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost`pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do Forms e do Document Management Client

   * Crie um `FormsServiceClient` objeto usando seu construtor padrão.
   * Crie um `FormsServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço de formulários AEM (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `FormsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.
   >[!NOTE]
   >
   >Repita essas etapas para o cliente `DocumentManagementServiceClient`de serviço.

1. Recuperar o design de formulário do Content Services (obsoleto)

   Recupere o conteúdo chamando o método do `DocumentManagementServiceClient` objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída de string que armazena o valor do link de navegação.
   * Um parâmetro de `BLOB` saída que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * Um parâmetro `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` de saída que armazena atributos de conteúdo.
   * Um parâmetro `CRCResult` de saída. Em vez de usar esse objeto, você pode usar o parâmetro de `BLOB` saída para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o método do `FormsServiceClient` objeto `renderPDFForm2` e passe os seguintes valores:

   * Um `BLOB` objeto que contém o design de formulário recuperado do Content Services (obsoleto).
   * Um `BLOB` objeto que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um `BLOB` objeto vazio.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não deseja especificar opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um `Map` objeto que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um parâmetro de saída longo que é usado para armazenar a contagem de páginas.
   * Um parâmetro de saída de string usado para armazenar o valor de localidade.
   * Um parâmetro de `FormsResult` saída usado para armazenar o formulário PDF interativo `.`
   O `renderPDFForm2` método retorna um `FormsResult` objeto que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um `BLOB` objeto que contenha dados de formulário obtendo o valor do `FormsResult` campo do `outputContent` objeto.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `BLOB` objeto recuperado do `FormsResult` objeto. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `MTOM` objeto.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
