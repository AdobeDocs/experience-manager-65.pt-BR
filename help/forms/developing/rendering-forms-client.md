---
title: Renderização do Forms no cliente
seo-title: Renderização do Forms no cliente
description: Otimize o delivery do conteúdo PDF e melhore a capacidade do serviço Forms de lidar com a carga da rede usando a capacidade de renderização do cliente da Acrobat ou Adobe Reader
seo-description: Otimize o delivery do conteúdo PDF e melhore a capacidade do serviço Forms de lidar com a carga da rede usando a capacidade de renderização do cliente da Acrobat ou Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 0%

---


# Renderização do Forms no cliente {#rendering-forms-at-the-client}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

## Renderização do Forms no cliente {#rendering-forms-at-the-client-inner}

Você pode otimizar o delivery do conteúdo PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando a capacidade de renderização do cliente da Acrobat ou Adobe Reader. Esse processo é conhecido como renderização de um formulário no cliente. Para renderizar um formulário no cliente, o dispositivo cliente (geralmente um navegador da Web) deve usar o Acrobat 7.0 ou o Adobe Reader 7.0 ou posterior.

As alterações em um formulário resultantes da execução de script do lado do servidor não são refletidas em um formulário renderizado no cliente, a menos que o subformulário raiz contenha o atributo `restoreState` definido como `auto`. Para obter mais informações sobre este atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário no cliente, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Defina as opções de tempo de execução de renderização do cliente.
1. Renderize um formulário no cliente.
1. Grave o formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de executar programaticamente uma operação de API do cliente de serviço da Forms, você deve criar um cliente de serviço da Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço da Web da Forms, crie um objeto `FormsService`.

**Definir opções de tempo de execução de renderização de cliente**

É necessário definir a opção de tempo de execução de renderização do cliente para renderizar um formulário no cliente, definindo a opção `RenderAtClient` de tempo de execução como `true`. Isso resulta na entrega do formulário no dispositivo cliente em que ele é renderizado. Se `RenderAtClient` for `auto` (o valor padrão), o design de formulário determinará se o formulário será renderizado no cliente. O design de formulário deve ser um design de formulário com um layout flutuante.

Uma opção opcional de tempo de execução que pode ser definida é a opção `SeedPDF`. A opção `SeedPDF` combina o container PDF (documento PDF semente) com o design de formulário e os dados XML. O design de formulário e os dados XML são entregues à Acrobat ou à Adobe Reader, onde o formulário é renderizado. A opção `SeedPDF` pode ser usada quando o computador cliente não tem fontes usadas no formulário, como quando um usuário final não está licenciado para usar uma fonte que o proprietário do formulário está licenciado para usar.

Você pode usar o Designer para criar um arquivo PDF dinâmico simples para uso como um arquivo PDF semente. As seguintes etapas são necessárias para executar essa tarefa:

1. Determine se é necessário incorporar quaisquer fontes no arquivo PDF semente. O arquivo PDF semente precisará conter fontes adicionais exigidas pelo formulário sendo renderizado. Ao incorporar fontes no arquivo semente PDF, certifique-se de que não esteja violando nenhum contrato de licenciamento de fontes. No Designer, é possível determinar se é possível incorporar legalmente fontes. Ao salvar, se houver fontes que não possam ser incorporadas ao formulário, o Designer exibirá uma mensagem listando as fontes que não podem ser incorporadas. Essa mensagem não é exibida no Designer para documentos PDF estáticos.
1. Se você estiver criando o arquivo semente PDF no Designer, recomenda-se que, no mínimo, você adicione um campo de texto que contenha uma mensagem. A mensagem deve ser dirigida aos usuários de versões anteriores do Adobe Reader declarando que eles precisam do Acrobat 7.0 ou posterior ou do Adobe Reader 7.0 ou posterior para visualização do documento.
1. Salve o arquivo PDF semente como um arquivo PDF dinâmico com a extensão de nome de arquivo PDF.

>[!NOTE]
>
>Não é necessário definir a opção de tempo de execução de PDF semente para renderizar um formulário no cliente. Se você não especificar um PDF semente, o serviço Forms criará um PDF de shell que não conterá objetos COS, mas conterá um invólucro PDF com o conteúdo XDP real incorporado no interior. As etapas nesta seção não definem a opção semente de tempo de execução de PDF. Para obter informações sobre objetos COS, consulte o Guia de referência da Adobe PDF.

**Renderizar um formulário no cliente**

Para renderizar um formulário no cliente, é necessário garantir que as opções de tempo de execução de renderização do cliente sejam incluídas na lógica do aplicativo para renderizar um formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

O serviço Forms cria um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário é renderizado pelo Acrobat 7.0 ou Adobe Reader 7.0 ou posterior e é visível para o usuário.

**Consulte também:**

[Renderizar um formulário no cliente usando a API Java](#render-a-form-at-the-client-using-the-java-api)

[Renderizar um formulário no cliente usando a API de serviço da Web](#render-a-form-at-the-client-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmissão de Documentos ao serviço Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário no cliente usando a API Java {#render-a-form-at-the-client-using-the-java-api}

Renderize um formulário no cliente usando a API da Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de renderização de cliente

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de tempo de execução `RenderAtClient` invocando o método `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor enum `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo AEM Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Start rápido (modo SOAP): Como renderizar um formulário no cliente usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar um formulário no cliente usando a API de serviço da Web {#render-a-form-at-the-client-using-the-web-service-api}

Renderize um formulário no cliente usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução de renderização de cliente

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de tempo de execução `RenderAtClient` chamando o método `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor da string `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe `null`. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método. Esse parâmetro é usado para armazenar o formulário PDF renderizado.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método. (Esse argumento armazenará o valor da localidade).
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderização do Forms no cliente](#rendering-forms-at-the-client)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
