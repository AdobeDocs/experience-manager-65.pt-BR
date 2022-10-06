---
title: Otimizar o desempenho do serviço de formulários
seo-title: Optimizing the Performance of theForms Service
description: Defina as opções de tempo de execução ao renderizar um formulário e armazenar arquivos XDP no repositório para otimizar o desempenho do serviço Forms.
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# Otimizar o desempenho do serviço Forms {#optimizing-the-performance-of-theforms-service}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Otimizar o desempenho do serviço Forms {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, é possível definir opções de tempo de execução que otimizem o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Chamar um serviço usando uma biblioteca do cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para otimizar o desempenho do serviço Forms ao renderizar um formulário, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Defina as opções de tempo de execução de desempenho.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms. Se estiver usando a API do Java, crie um `FormsServiceClient` objeto. Se estiver usando a API do serviço da Web da Forms, crie um `FormsService` objeto.

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Armazenamento de formulários em cache**: Você pode armazenar em cache um formulário renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache depois de ser gerado pela primeira vez. Em uma renderização subsequente, se o formulário em cache for mais recente do que o carimbo de data e hora do design de formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você aumenta o desempenho do serviço Forms, pois ele não precisa recuperar o design de formulário de um repositório.
* Guias de formulário (obsoleto) podem demorar mais para renderizar do que outros tipos de transformação. É recomendável armazenar os Guias de formulário em cache (obsoleto) para melhorar o desempenho.
* **Opção independente**: Se você não precisar que o serviço Forms execute cálculos no lado do servidor, poderá definir a opção Independente como `true`, o que resulta na renderização de formulários sem informações de estado. As informações de estado são necessárias se você quiser renderizar um formulário interativo para um usuário final que, em seguida, insere informações no formulário e envia o formulário de volta ao serviço da Forms. O serviço Forms realiza uma operação de cálculo e renderiza o formulário de volta para o usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for enviado de volta ao serviço da Forms, somente os dados XML estarão disponíveis e os cálculos do lado do servidor não serão executados.
* **PDF linearizado**: Um arquivo PDF linearizado é organizado para permitir um acesso incremental eficiente em um ambiente de rede. O arquivo PDF é um PDF válido em todos os aspectos e é compatível com todos os visualizadores e outros aplicativos do PDF. Ou seja, um PDF linearizado pode ser visualizado enquanto ainda está sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção GuideRSL**: Habilita a geração do Guia do formulário (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação do Flex.
* Você também pode melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir opções de desempenho, use a mesma lógica de aplicativo como renderização de um formulário sem opções de desempenho.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Depois que o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Otimizar o desempenho usando a API do Java {#optimize-the-performance-using-the-java-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de desempenho

   * Crie um `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o `PDFFormRenderSpec` do objeto `setCacheEnabled` método e aprovação `true`.
   * Defina a opção linearizada chamando o `PDFFormRenderSpec` do objeto `setLinearizedPDF` método e aprovação `true.`

1. Renderizar o formulário

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução para melhorar o desempenho.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web cliente.
   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Início rápido (modo SOAP): Otimização do desempenho usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Otimizar o desempenho usando a API do serviço da Web {#optimize-the-performance-using-the-web-service-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Crie um `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o `PDFFormRenderSpec` do objeto `setCacheEnabled` e transmitindo true.
   * Defina a opção independente chamando o `PDFFormRenderSpec` do objeto `setStandAlone` e transmitindo true.
   * Defina a opção linearizada chamando o `PDFFormRenderSpec` do objeto `setLinearizedPDF` e transmitindo true.

1. Renderizar o formulário

   Chame o `FormsService` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`.
   * A `PDFFormRenderSpecc` objeto que armazena opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Isso é usado para armazenar o formulário PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . (Esse argumento armazenará o número de páginas no formulário).
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . (Esse argumento armazenará o valor da localidade).
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `renderPDFForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web cliente.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
