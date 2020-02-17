---
title: Otimizando o desempenho do serviço Forms
seo-title: Otimizando o desempenho do serviço Forms
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Otimizando o desempenho do serviço de formulários {#optimizing-the-performance-of-theforms-service}

## Otimizando o desempenho do serviço de formulários {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, é possível definir opções de tempo de execução que otimizem o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Invocando um serviço usando uma biblioteca](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)de cliente Java.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para otimizar o desempenho do serviço Forms ao renderizar um formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Defina as opções de tempo de execução de desempenho.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de executar programaticamente uma operação de API do cliente do serviço Forms, é necessário criar um cliente do serviço Forms. Se você estiver usando a API Java, crie um `FormsServiceClient` objeto. Se você estiver usando a API de serviço da Web do Forms, crie um `FormsService` objeto.

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Armazenamento de formulários em cache**: É possível armazenar em cache um formulário renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache depois de ser gerado pela primeira vez. Em uma renderização subsequente, se o formulário em cache for mais recente do que o carimbo de data e hora do design de formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você aprimora o desempenho do serviço Forms, pois ele não precisa recuperar o design de formulário de um repositório.
* Guias de formulário (obsoletos) podem levar mais tempo para renderizar do que outros tipos de transformação. É recomendável colocar em cache os Guias de formulário (obsoletos) para melhorar o desempenho.
* **Opção** independente: Se você não exigir que o serviço Forms execute cálculos no lado do servidor, poderá definir a opção Independente como `true`, resultando na renderização de formulários sem informações de estado. As informações de estado são necessárias se você deseja renderizar um formulário interativo para um usuário final que digita as informações no formulário e envia o formulário de volta para o serviço Forms. O serviço de Formulários executa uma operação de cálculo e renderiza o formulário de volta ao usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for submetido de volta ao serviço Forms, somente os dados XML estarão disponíveis e os cálculos do servidor não serão executados.
* **PDF** linearizado: Um arquivo PDF linearizado é organizado para permitir um acesso incremental eficiente em um ambiente de rede. O arquivo PDF é válido em todos os aspectos e é compatível com todos os visualizadores e outros aplicativos PDF existentes. Ou seja, um PDF linearizado pode ser visualizado enquanto ainda está sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção** GuideRSL: Habilita a geração do Guia de formulário (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação do Flex.
* Também é possível melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderização de formulários no cliente](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir as opções de desempenho, use a mesma lógica de aplicativo que renderizar um formulário sem opções de desempenho.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Depois que o serviço Forms renderiza um formulário, ele retorna um fluxo de dados do formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do serviço de formulários](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Como renderizar formulários PDF interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizar formulários como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicativos da Web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

### Otimizar o desempenho usando a API Java {#optimize-the-performance-using-the-java-api}

Renderize um formulário com desempenho otimizado usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de desempenho

   * Crie um `PDFFormRenderSpec` objeto usando seu construtor.
   * Defina a opção de cache de formulário chamando o método do `PDFFormRenderSpec` objeto `setCacheEnabled` e transmitindo `true`.
   * Defina a opção linearizada chamando o método do `PDFFormRenderSpec` objeto `setLinearizedPDF` e passando `true.`

1. Renderizar o formulário

   Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um `com.adobe.idp.Document` objeto que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um `com.adobe.idp.Document` objeto vazio.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução para melhorar o desempenho.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, invocando o `InputStream` método do `read`objeto e transmitindo a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Início rápido (modo SOAP): Otimização do desempenho usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Otimizar o desempenho usando a API de serviço da Web {#optimize-the-performance-using-the-web-service-api}

Renderize um formulário com desempenho otimizado usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Crie um `PDFFormRenderSpec` objeto usando seu construtor.
   * Defina a opção de cache de formulário chamando o método do `PDFFormRenderSpec` objeto `setCacheEnabled` e transmitindo true.
   * Configure a opção independente chamando o método do `PDFFormRenderSpec` objeto `setStandAlone` e transmitindo true.
   * Defina a opção linearizada chamando o método do `PDFFormRenderSpec` objeto `setLinearizedPDF` e transmitindo true.

1. Renderizar o formulário

   Chame o método do `FormsService` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um `BLOB` objeto que contém dados a serem unidos ao formulário. Se você não deseja unir dados, passe `null`.
   * Um `PDFFormRenderSpecc` objeto que armazena opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo método. Isso é usado para armazenar o formulário PDF renderizado.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o valor da localidade).
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
