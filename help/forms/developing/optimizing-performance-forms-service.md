---
title: Otimizando o desempenho do serviço Forms
description: Defina as opções de tempo de execução ao renderizar um formulário e armazene arquivos XDP no repositório para otimizar o desempenho do serviço do Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Otimização do desempenho do serviço Forms {#optimizing-the-performance-of-theforms-service}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

## Otimização do desempenho do serviço Forms {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, você pode definir opções de tempo de execução que otimizarão o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Chamar um serviço usando uma biblioteca cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para otimizar o desempenho do serviço Forms ao renderizar um formulário, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Definir opções de tempo de execução de desempenho.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço Web Forms, crie um objeto `FormsService`.

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Cache de formulário**: você pode armazenar em cache um formulário que é renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache após ser gerado pela primeira vez. Em um renderizador subsequente, se o formulário em cache for mais recente que o carimbo de data e hora do design do formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você melhora o desempenho do serviço Forms, pois ele não precisa recuperar o design do formulário de um repositório.
* As Guias de formulário (obsoletas) podem levar mais tempo para serem renderizadas do que outros tipos de transformação. É recomendável armazenar em cache os Guias de formulário (obsoletos) para melhorar o desempenho.
* **Opção autônoma**: se você não precisar que o serviço Forms execute cálculos no lado do servidor, defina a opção Autônoma como `true`, o que resultará na renderização de formulários sem informações de estado. As informações de estado são necessárias se você quiser renderizar um formulário interativo para um usuário final que, em seguida, insere informações no formulário e o envia de volta para o serviço Forms. O serviço Forms executa uma operação de cálculo e renderiza o formulário de volta para o usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for enviado de volta para o serviço Forms, somente os dados XML estarão disponíveis e os cálculos do lado do servidor não serão executados.
* **PDF linearizado**: um arquivo de PDF linearizado está organizado para habilitar o acesso incremental eficiente em um ambiente de rede. O arquivo PDF é um PDF válido em todos os aspectos e é compatível com todos os visualizadores existentes e outros aplicativos PDF. Ou seja, um PDF linearizado pode ser visualizado enquanto estiver sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção GuideRSL**: habilita a geração do Guia de Formulários (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação do Flex.
* Você também pode melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir as opções de desempenho, use a mesma lógica de aplicação que renderizar um formulário sem as opções de desempenho.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Depois que o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Otimizar o desempenho usando a API Java {#optimize-the-performance-using-the-java-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulários chamando o método `setCacheEnabled` do objeto `PDFFormRenderSpec` e transmitindo `true`.
   * Defina a opção linearizada chamando o método `setLinearizedPDF` do objeto `PDFFormRenderSpec` e transmitindo `true.`

1. Renderizar o formulário

   Chame o método `renderPDFForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução para melhorar o desempenho.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário ao navegador da Web cliente.
   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Início rápido (modo SOAP): otimização do desempenho usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Otimizar o desempenho usando a API do serviço Web {#optimize-the-performance-using-the-web-service-api}

Renderize um formulário com desempenho otimizado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulários chamando o método `setCacheEnabled` do objeto `PDFFormRenderSpec` e passando true.
   * Defina a opção autônoma invocando o método `setStandAlone` do objeto `PDFFormRenderSpec` e transmitindo true.
   * Defina a opção linearizada chamando o método `setLinearizedPDF` do objeto `PDFFormRenderSpec` e passando true.

1. Renderizar o formulário

   Chame o método `renderPDFForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`.
   * Um objeto `PDFFormRenderSpecc` que armazena opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. (Esse argumento armazenará o valor do local).
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário ao navegador da Web cliente.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
