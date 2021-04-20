---
title: Otimizar o desempenho do serviço de formulários
seo-title: Otimizar o desempenho do serviço de formulários
description: Defina as opções de tempo de execução ao renderizar um formulário e armazenar arquivos XDP no repositório para otimizar o desempenho do serviço Forms.
seo-description: Defina as opções de tempo de execução ao renderizar um formulário e armazenar arquivos XDP no repositório para otimizar o desempenho do serviço Forms.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 0%

---


# Otimizar o desempenho do serviço Forms {#optimizing-the-performance-of-theforms-service}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Otimizar o desempenho do serviço Forms {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, é possível definir opções de tempo de execução que otimizem o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Invocar um serviço usando uma biblioteca do cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms. Se estiver usando a API do Java, crie um objeto `FormsServiceClient` . Se estiver usando a API do serviço da Web da Forms, crie um objeto `FormsService` .

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Armazenamento** de formulários em cache: É possível armazenar em cache um formulário renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache depois de ser gerado pela primeira vez. Em uma renderização subsequente, se o formulário em cache for mais recente do que o carimbo de data e hora do design de formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você aumenta o desempenho do serviço Forms, pois ele não precisa recuperar o design de formulário de um repositório.
* Guias de formulário (obsoleto) podem demorar mais para renderizar do que outros tipos de transformação. É recomendável armazenar os Guias de formulário em cache (obsoleto) para melhorar o desempenho.
* **Opção** independente: Se não for necessário que o serviço Forms execute cálculos no lado do servidor, é possível definir a opção Independente como  `true`, o que resulta na renderização dos formulários sem informações de estado. As informações de estado são necessárias se você quiser renderizar um formulário interativo para um usuário final que, em seguida, insere informações no formulário e envia o formulário de volta ao serviço da Forms. O serviço Forms realiza uma operação de cálculo e renderiza o formulário de volta para o usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for enviado de volta ao serviço da Forms, somente os dados XML estarão disponíveis e os cálculos do lado do servidor não serão executados.
* **PDF** linearizado: Um arquivo PDF linearizado é organizado para permitir um acesso incremental eficiente em um ambiente de rede. O arquivo PDF é válido em todos os aspectos e é compatível com todos os visualizadores e outros aplicativos PDF existentes. Ou seja, um PDF linearizado pode ser visualizado enquanto ainda está sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção** GuideRSL: Habilita a geração do Guia do formulário (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação do Flex.
* Você também pode melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderizar Forms no Cliente](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir opções de desempenho, use a mesma lógica de aplicativo como renderização de um formulário sem opções de desempenho.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Depois que o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Otimize o desempenho usando a API Java {#optimize-the-performance-using-the-java-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o método `PDFFormRenderSpec` do objeto e passando `true`.`setCacheEnabled`
   * Defina a opção linearizada chamando o método `PDFFormRenderSpec` do objeto `setLinearizedPDF` e passando `true.`

1. Renderizar o formulário

   Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução para melhorar o desempenho.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o método `InputStream` do objeto e transmitindo a matriz de bytes como um argumento.`read`
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**

[Início rápido (modo SOAP): Otimização do desempenho usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Otimizar o desempenho usando a API do serviço da Web {#optimize-the-performance-using-the-web-service-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulário chamando o método `PDFFormRenderSpec` do objeto e passando &quot;true&quot;.`setCacheEnabled`
   * Defina a opção independente chamando o método `PDFFormRenderSpec` do objeto `setStandAlone` e passando como true.
   * Defina a opção linearizada chamando o método `PDFFormRenderSpec` do objeto `setLinearizedPDF` e passando como true.

1. Renderizar o formulário

   Chame o método `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`.
   * Um objeto `PDFFormRenderSpecc` que armazena opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método . Usado para armazenar o formulário PDF renderizado.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método . (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método . (Esse argumento armazenará o valor da localidade).
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
