---
title: Otimizando o desempenho do serviço Forms
seo-title: Otimizando o desempenho do serviço Forms
description: Defina opções de tempo de execução ao renderizar um formulário e armazenar arquivos XDP no repositório para otimizar o desempenho do serviço Forms.
seo-description: Defina opções de tempo de execução ao renderizar um formulário e armazenar arquivos XDP no repositório para otimizar o desempenho do serviço Forms.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---


# Otimizando o desempenho do serviço Forms {#optimizing-the-performance-of-theforms-service}

## Otimizando o desempenho do serviço Forms {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, é possível definir opções de tempo de execução que otimizem o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Invocar um serviço usando uma biblioteca de cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para otimizar o desempenho do serviço Forms ao renderizar um formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Defina as opções de tempo de execução de desempenho.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de executar programaticamente uma operação de API do cliente de serviço da Forms, você deve criar um cliente de serviço da Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço da Web da Forms, crie um objeto `FormsService`.

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Armazenamento de formulários em cache**: É possível armazenar em cache um formulário renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache depois de ser gerado pela primeira vez. Em uma renderização subsequente, se o formulário em cache for mais recente do que o carimbo de data e hora do design de formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você aprimora o desempenho do serviço Forms, pois ele não precisa recuperar o design de formulário de um repositório.
* Guias de formulário (obsoletos) podem levar mais tempo para renderizar do que outros tipos de transformação. É recomendável colocar em cache os Guias de formulário (obsoletos) para melhorar o desempenho.
* **Opção** independente: Se você não exigir que o serviço Forms execute cálculos no lado do servidor, poderá definir a opção Autônomo como  `true`, o que resultará na renderização de formulários sem informações de estado. As informações de estado são necessárias se você deseja renderizar um formulário interativo para um usuário final que digita as informações no formulário e envia o formulário de volta ao serviço da Forms. Em seguida, o serviço Forms realiza uma operação de cálculo e renderiza o formulário de volta ao usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for enviado de volta ao serviço Forms, somente os dados XML estarão disponíveis e os cálculos do lado do servidor não serão executados.
* **PDF** linearizado: Um arquivo PDF linearizado é organizado para permitir um acesso incremental eficiente em um ambiente de rede. O arquivo PDF é um PDF válido em todos os aspectos e é compatível com todos os visualizadores e outros aplicativos PDF existentes. Ou seja, um PDF linearizado pode ser visualizado enquanto ainda está sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção** GuideRSL: Habilita a geração do Guia de formulário (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação da Flex.
* Também é possível melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderizando o Forms no Client](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir as opções de desempenho, use a mesma lógica de aplicativo que renderizar um formulário sem opções de desempenho.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Depois que o serviço Forms renderiza um formulário, ele retorna um fluxo de dados do formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizando Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Otimizar o desempenho usando a API Java {#optimize-the-performance-using-the-java-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o método `PDFFormRenderSpec` do objeto `setCacheEnabled` e transmitindo `true`.
   * Defina a opção linearizada chamando o método `PDFFormRenderSpec` do objeto `setLinearizedPDF` e transmitindo `true.`

1. Renderizar o formulário

   Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução para melhorar o desempenho.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, invocando o método `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Start rápido (modo SOAP): Otimização do desempenho usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Otimizar o desempenho usando a API de serviço da Web {#optimize-the-performance-using-the-web-service-api}

Renderize um formulário com desempenho otimizado usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o método `PDFFormRenderSpec` do objeto `setCacheEnabled` e transmitindo true.
   * Configure a opção independente chamando o método `PDFFormRenderSpec` do objeto `setStandAlone` e transmitindo true.
   * Defina a opção linearizada chamando o método `PDFFormRenderSpec` do objeto `setLinearizedPDF` e transmitindo true.

1. Renderizar o formulário

   Chame o método `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe `null`.
   * Um objeto `PDFFormRenderSpecc` que armazena opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método. Isso é usado para armazenar o formulário PDF renderizado.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método. (Esse argumento armazenará o valor da localidade).
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
