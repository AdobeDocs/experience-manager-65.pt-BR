---
title: Passar documentos para o FormsService
seo-title: Passar documentos para o FormsService
description: 'Passe um objeto com.adobe.idp.Document que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto com.adobe.idp.Document. '
seo-description: Passe um objeto com.adobe.idp.Document que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto com.adobe.idp.Document.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 0%

---


# Enviar documentos para o serviço do Forms {#passing-documents-to-the-formsservice}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço AEM Forms renderiza PDF forms interativas para dispositivos clientes, normalmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, é possível transmitir um objeto `com.adobe.idp.Document` que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto `com.adobe.idp.Document`.

Uma vantagem de transmitir um objeto `com.adobe.idp.Document` para o serviço Forms é que outras operações de serviço retornam uma instância `com.adobe.idp.Document`. Ou seja, você pode obter uma instância `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado em um nó Content Services (obsoleto) chamado `/Company Home/Form Designs`, conforme mostrado na ilustração a seguir.

Você pode recuperar programaticamente o Loan.xdp dos Serviços de conteúdo (obsoleto) e passar o arquivo XDP para o serviço Forms em um objeto `com.adobe.idp.Document`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido dos Serviços de conteúdo (obsoleto) (obsoleto) para o serviço da Forms, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um Forms e um objeto de API do cliente de gerenciamento de documentos.
1. Recupere o design de formulário do Content Services (obsoleto).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados do formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um Forms e um objeto de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação de API de serviço do Forms, crie um objeto de API do cliente Forms. Além disso, como esse workflow recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (obsoleto)**

Recupere o arquivo XDP do Content Services (obsoleto) usando a API do serviço da Web ou do Java. O arquivo XDP é retornado em uma instância `com.adobe.idp.Document` (ou em uma instância `BLOB` se você estiver usando serviços da Web). Em seguida, você pode passar a instância `com.adobe.idp.Document` para o serviço do Forms.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário interativo, passe a instância `com.adobe.idp.Document` que foi retornada do Content Services (obsoleto) para o serviço do Forms.

>[!NOTE]
>
>Você pode enviar um `com.adobe.idp.Document` que contém o design de formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitam um objeto `com.adobe.idp.Document` que contenha um design de formulário.

**Executar uma ação com o fluxo de dados do formulário**

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvar o formulário como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário no navegador da Web. No entanto, um aplicativo de desktop geralmente salva o formulário como um arquivo PDF.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Passe documentos para o serviço da Forms usando a API do Java {#pass-documents-to-the-forms-service-using-the-java-api}

Passe um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço da Forms e a API (obsoleta) dos Serviços de conteúdo (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do seu projeto Java.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar o design do formulário do Content Services (obsoleto)

   Chame o método `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   O método `retrieveContent` retorna um objeto `CRCResult` que contém o arquivo XDP. Obtenha uma instância `com.adobe.idp.Document` chamando o método `CRCResult` do objeto `getDocument`.

1. Renderizar um formulário PDF interativo

   Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e passando o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o método `InputStream` do objeto `read`. Transmita a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**

[Início rápido (modo SOAP): Passar documentos para o serviço da Forms usando a API do Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Passe documentos para o serviço da Forms usando a API do serviço da Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passe um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço da Forms e a API dos Serviços de conteúdo (obsoleto) (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Como esse aplicativo cliente chama dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição de WSDL para a referência de serviço associada ao serviço da Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como o tipo de dados `BLOB` é comum a ambas as referências de serviço, qualifique totalmente o tipo de dados `BLOB` ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as instâncias `BLOB` são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost`pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um objeto `FormsServiceClient` usando seu construtor padrão.
   * Crie um objeto `FormsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Você não precisa usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `FormsServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para o cliente de serviço `DocumentManagementServiceClient`.

1. Recuperar o design do formulário do Content Services (obsoleto)

   Recupere o conteúdo chamando o método `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída de string que armazena o valor do link de navegação.
   * Um parâmetro de saída `BLOB` que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * Um parâmetro de saída `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` que armazena atributos de conteúdo.
   * Um parâmetro de saída `CRCResult`. Em vez de usar esse objeto, você pode usar o parâmetro de saída `BLOB` para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * Um objeto `BLOB` que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `BLOB` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um objeto `Map` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um parâmetro de saída longo usado para armazenar a contagem de páginas.
   * Um parâmetro de saída da string usado para armazenar o valor da localidade.
   * Um parâmetro de saída `FormsResult` usado para armazenar o formulário PDF interativo `.`

   O método `renderPDFForm2` retorna um objeto `FormsResult` que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um objeto `BLOB` que contenha dados de formulário obtendo o valor do campo `FormsResult` do objeto `outputContent`.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF interativo e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` recuperado do objeto `FormsResult`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
