---
title: Enviar documentos para o FormsService
description: Passe um objeto com.adobe.idp.Document que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design do formulário no objeto com.adobe.idp.Document.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Passar documentos para o serviço da Forms {#passing-documents-to-the-formsservice}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

O serviço AEM Forms renderiza PDF forms interativos em dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, você pode passar um objeto `com.adobe.idp.Document` que contenha o design do formulário para o serviço do Forms. O serviço Forms renderiza o design do formulário no objeto `com.adobe.idp.Document`.

Uma vantagem de passar um objeto `com.adobe.idp.Document` para o serviço Forms é que outras operações de serviço retornam uma instância `com.adobe.idp.Document`. Ou seja, você pode obter uma instância `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, digamos que um arquivo XDP esteja armazenado em um nó do Content Services (obsoleto) chamado `/Company Home/Form Designs`, como mostrado na ilustração a seguir.

Você pode recuperar programaticamente Loan.xdp do Content Services (desaprovado) (desaprovado) e passar o arquivo XDP para o serviço Forms em um objeto `com.adobe.idp.Document`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido do Content Services (obsoleto) (obsoleto) para o serviço Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um Forms e um objeto de API do cliente de gerenciamento de documentos.
1. Recuperar o design do formulário do Content Services (desaprovado).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados de formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um Forms e um objeto de API do Cliente de Gerenciamento de Documentos**

Antes de executar programaticamente uma operação da API de serviço do Forms, crie um objeto da API de cliente do Forms. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (desaprovado)**

Recupere o arquivo XDP do Content Services (obsoleto) usando o Java ou a API do serviço da Web. O arquivo XDP é retornado em uma instância `com.adobe.idp.Document` (ou uma instância `BLOB` se você estiver usando serviços da Web). Em seguida, você pode passar a instância `com.adobe.idp.Document` para o serviço Forms.

**Renderizar um formulário de PDF interativo**

Para renderizar um formulário interativo, passe a instância `com.adobe.idp.Document` que foi retornada do Content Services (desaprovado) para o serviço Forms.

>[!NOTE]
>
>Você pode passar um `com.adobe.idp.Document` que contenha o design do formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitam um objeto `com.adobe.idp.Document` que contém um design de formulário.

**Executar uma ação com o fluxo de dados de formulário**

Dependendo do tipo de aplicativo cliente, você pode gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário em um navegador da Web. No entanto, um aplicativo de desktop normalmente salva o formulário como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Enviar documentos para o serviço Forms usando a API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Envie um documento obtido do Content Services (desaprovado) usando o serviço do Forms e a API do Content Services (desaprovado) (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do projeto Java.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar o design do formulário do Content Services (desaprovado)

   Chame o método `retrieveContent` do objeto `DocumentManagementServiceClientImpl` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de cadeia que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   O método `retrieveContent` retorna um objeto `CRCResult` que contém o arquivo XDP. Obtenha uma instância `com.adobe.idp.Document` invocando o método `getDocument` do objeto `CRCResult`.

1. Renderizar um formulário PDF interativo

   Chame o método `renderPDFForm2` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o design de formulário recuperado do Content Services (desaprovado).
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este valor é um parâmetro opcional, e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Este valor é um parâmetro opcional, e você pode especificar `null`.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este valor é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Executar uma ação com o fluxo de dados de formulário

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream`. Transmita a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Início rápido (modo SOAP): Passar documentos para o Forms Service usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Enviar documentos para o serviço Forms usando a API do serviço Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Envie um documento obtido do Content Services (desaprovado) usando o serviço do Forms e a API (serviço da Web) do Content Services (desaprovado):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Como este aplicativo cliente invoca dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de Documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como o tipo de dados `BLOB` é comum a ambas as referências de serviço, qualifique totalmente o tipo de dados `BLOB` ao usá-lo. No início rápido do serviço Web correspondente, todas as `BLOB` instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um objeto `FormsServiceClient` usando seu construtor padrão.
   * Crie um objeto `FormsServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `FormsServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para o cliente de serviço `DocumentManagementServiceClient`.

1. Recuperar o design do formulário do Content Services (desaprovado)

   Recupere o conteúdo chamando o método `retrieveContent` do objeto `DocumentManagementServiceClient` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de cadeia que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída da string que armazena o valor do link de pesquisa.
   * Um parâmetro de saída `BLOB` que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * Um parâmetro de saída `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` que armazena atributos de conteúdo.
   * Um parâmetro de saída `CRCResult`. Em vez de usar esse objeto, você pode usar o parâmetro de saída `BLOB` para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o método `renderPDFForm2` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que contém o design de formulário recuperado do Content Services (desaprovado).
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `BLOB` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este valor é um parâmetro opcional, e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI. Este valor é um parâmetro opcional, e você pode especificar `null`.
   * Um objeto `Map` que armazena anexos de arquivo. Este valor é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um parâmetro de saída longo que é usado para armazenar a contagem de páginas.
   * Um parâmetro de saída da string que é usado para armazenar o valor do local.
   * Um parâmetro de saída `FormsResult` que é usado para armazenar o formulário de PDF interativo `.`

   O método `renderPDFForm2` retorna um objeto `FormsResult` que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados de formulário

   * Crie um objeto `BLOB` que contenha dados de formulário obtendo o valor do campo `outputContent` do objeto `FormsResult`.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` recuperado do objeto `FormsResult`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
