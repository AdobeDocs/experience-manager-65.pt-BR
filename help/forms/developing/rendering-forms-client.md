---
title: Renderização de formulários no cliente
seo-title: Renderização de formulários no cliente
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c

---


# Renderização de formulários no cliente {#rendering-forms-at-the-client}

## Renderização de formulários no cliente {#rendering-forms-at-the-client-inner}

Você pode otimizar o delivery do conteúdo PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do cliente do Acrobat ou Adobe Reader. Esse processo é conhecido como renderização de um formulário no cliente. Para renderizar um formulário no cliente, o dispositivo cliente (geralmente um navegador da Web) deve usar o Acrobat 7.0 ou o Adobe Reader 7.0 ou posterior.

As alterações em um formulário resultantes da execução de script no servidor não são refletidas em um formulário renderizado no cliente, a menos que o subformulário raiz contenha o `restoreState` atributo definido como `auto`. Para obter mais informações sobre esse atributo, consulte [Designer de Formulários.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário no cliente, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Defina as opções de tempo de execução de renderização do cliente.
1. Renderize um formulário no cliente.
1. Grave o formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de executar programaticamente uma operação de API do cliente do serviço Forms, é necessário criar um cliente do serviço Forms. Se você estiver usando a API Java, crie um `FormsServiceClient` objeto. Se você estiver usando a API de serviço da Web do Forms, crie um `FormsService` objeto.

**Definir opções de tempo de execução de renderização de cliente**

É necessário definir a opção de tempo de execução de renderização do cliente para renderizar um formulário no cliente, definindo a opção de tempo de `RenderAtClient` execução como `true`. Isso resulta na entrega do formulário no dispositivo cliente em que ele é renderizado. Se `RenderAtClient` for `auto` (o valor padrão), o design de formulário determinará se o formulário será renderizado no cliente. O design de formulário deve ser um design de formulário com um layout flutuante.

Uma opção opcional de tempo de execução que pode ser definida é a `SeedPDF` . A `SeedPDF` opção combina o container PDF (documento PDF semente) com o design de formulário e os dados XML. O design de formulário e os dados XML são entregues ao Acrobat ou Adobe Reader, onde o formulário é renderizado. A `SeedPDF` opção pode ser usada quando o computador cliente não tem fontes usadas no formulário, como quando um usuário final não está licenciado para usar uma fonte que o proprietário do formulário está licenciado para usar.

Você pode usar o Designer para criar um arquivo PDF dinâmico simples para uso como um arquivo PDF semente. As seguintes etapas são necessárias para executar essa tarefa:

1. Determine se é necessário incorporar quaisquer fontes no arquivo PDF semente. O arquivo PDF semente precisará conter fontes adicionais exigidas pelo formulário sendo renderizado. Ao incorporar fontes no arquivo semente PDF, certifique-se de que não esteja violando nenhum contrato de licenciamento de fontes. No Designer, é possível determinar se é possível incorporar legalmente fontes. Ao salvar, se houver fontes que não possam ser incorporadas ao formulário, o Designer exibirá uma mensagem listando as fontes que não podem ser incorporadas. Essa mensagem não é exibida no Designer para documentos PDF estáticos.
1. Se você estiver criando o arquivo semente PDF no Designer, recomenda-se que, no mínimo, você adicione um campo de texto que contenha uma mensagem. A mensagem deve ser direcionada aos usuários de versões anteriores do Adobe Reader informando que eles precisam do Acrobat 7.0 ou posterior ou do Adobe Reader 7.0 ou posterior para visualização do documento.
1. Salve o arquivo PDF semente como um arquivo PDF dinâmico com a extensão de nome de arquivo PDF.

>[!NOTE]
>
>Não é necessário definir a opção de tempo de execução de PDF semente para renderizar um formulário no cliente. Se você não especificar um PDF semente, o serviço Forms criará um PDF de shell que não conterá objetos COS, mas conterá um invólucro PDF com o conteúdo XDP real incorporado no interior. As etapas nesta seção não definem a opção semente de tempo de execução de PDF. Para obter informações sobre objetos COS, consulte o guia de referência do Adobe PDF.

**Renderizar um formulário no cliente**

Para renderizar um formulário no cliente, é necessário garantir que as opções de tempo de execução de renderização do cliente sejam incluídas na lógica do aplicativo para renderizar um formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

O serviço Forms cria um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web cliente, o formulário é renderizado pelo Acrobat 7.0 ou Adobe Reader 7.0 ou posterior e é visível para o usuário.

**Consulte também:**

[Renderizar um formulário no cliente usando a API Java](#render-a-form-at-the-client-using-the-java-api)

[Renderizar um formulário no cliente usando a API de serviço da Web](#render-a-form-at-the-client-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmissão de Documentos ao serviço de formulários](/help/forms/developing/passing-documents-forms-service.md)

[Criação de Aplicações web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário no cliente usando a API Java {#render-a-form-at-the-client-using-the-java-api}

Renderize um formulário no cliente usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de renderização de cliente

   * Crie um `PDFFormRenderSpec` objeto usando seu construtor.
   * Defina a opção de tempo de `RenderAtClient` execução chamando o método do `PDFFormRenderSpec` objeto e transmitindo o valor enum `setRenderAtClient` `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo AEM Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se você não quiser unir dados, passe um `com.adobe.idp.Document` objeto vazio.
   * Um `PDFFormRenderSpec` objeto que armazena as opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, invocando o método do `InputStream` objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` `write` do objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Start rápido (modo SOAP): Como renderizar um formulário no cliente usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar um formulário no cliente usando a API de serviço da Web {#render-a-form-at-the-client-using-the-web-service-api}

Renderize um formulário no cliente usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Definir opções de tempo de execução de renderização de cliente

   * Crie um `PDFFormRenderSpec` objeto usando seu construtor.
   * Defina a opção de tempo de `RenderAtClient` execução chamando o método do `PDFFormRenderSpec` objeto e transmitindo o valor da string `setRenderAtClient` `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método do `FormsService` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja unir dados, passe `null`. (Consulte [Pré-preenchimento de formulários com layouts](/help/forms/developing/prepopulating-forms-flowable-layouts.md)flutuantes.)
   * Um `PDFFormRenderSpec` objeto que armazena as opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço de Formulários.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo método. Esse parâmetro é usado para armazenar o formulário PDF renderizado.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o valor da localidade).
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Obtenha o tipo de conteúdo do `BLOB` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` `write` do objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Renderização de formulários no cliente](#rendering-forms-at-the-client)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
