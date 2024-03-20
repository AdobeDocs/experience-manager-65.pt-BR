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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Otimização do desempenho do serviço Forms {#optimizing-the-performance-of-theforms-service}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Otimização do desempenho do serviço Forms {#optimizing-the-performance-of-the-forms-service}

Ao renderizar um formulário, você pode definir opções de tempo de execução que otimizarão o desempenho do serviço Forms. Outra tarefa que você pode executar para melhorar o desempenho do serviço Forms é armazenar arquivos XDP no repositório. No entanto, esta seção não descreve como executar essa tarefa. (Consulte [Chamar um serviço usando uma biblioteca cliente Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se estiver usando a API Java, crie uma `FormsServiceClient` objeto. Se estiver usando a API do serviço Web Forms, crie uma `FormsService` objeto.

**Definir opções de tempo de execução de desempenho**

Você pode definir as seguintes opções de tempo de execução de desempenho para melhorar o desempenho do serviço Forms:

* **Cache de formulários**: Você pode armazenar em cache um formulário que é renderizado como PDF no cache do servidor. Cada formulário é armazenado em cache após ser gerado pela primeira vez. Em um renderizador subsequente, se o formulário em cache for mais recente que o carimbo de data e hora do design do formulário, o formulário será recuperado do cache. Ao armazenar formulários em cache, você melhora o desempenho do serviço Forms, pois ele não precisa recuperar o design do formulário de um repositório.
* As Guias de formulário (obsoletas) podem levar mais tempo para serem renderizadas do que outros tipos de transformação. É recomendável armazenar em cache os Guias de formulário (obsoletos) para melhorar o desempenho.
* **Opção independente**: se você não precisar que o serviço Forms execute cálculos no lado do servidor, poderá definir a opção Independente como `true`, que resulta em formulários sendo renderizados sem informações de estado. As informações de estado são necessárias se você quiser renderizar um formulário interativo para um usuário final que, em seguida, insere informações no formulário e o envia de volta para o serviço Forms. O serviço Forms executa uma operação de cálculo e renderiza o formulário de volta para o usuário com os resultados exibidos no formulário. Se um formulário sem informações de estado for enviado de volta para o serviço Forms, somente os dados XML estarão disponíveis e os cálculos do lado do servidor não serão executados.
* **PDF linearizado**: um arquivo PDF linearizado é organizado para permitir o acesso incremental eficiente em um ambiente de rede. O arquivo PDF é um PDF válido em todos os aspectos e é compatível com todos os visualizadores existentes e outros aplicativos PDF. Ou seja, um PDF linearizado pode ser visualizado enquanto estiver sendo baixado.
* Essa opção não melhora o desempenho quando um formulário PDF é renderizado no cliente.
* **Opção GuideRSL**: habilita a geração do Guia de formulário (obsoleto) usando bibliotecas compartilhadas em tempo de execução. Isso significa que a primeira solicitação baixará um arquivo SWF menor, além de bibliotecas compartilhadas maiores que são armazenadas no cache do navegador. Para obter mais informações, consulte RSL na documentação do Flex.
* Você também pode melhorar o desempenho do serviço Forms renderizando um formulário no cliente. (Consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).)

**Renderizar o formulário**

Para renderizar o formulário após definir as opções de desempenho, use a mesma lógica de aplicação que renderizar um formulário sem as opções de desempenho.

**Gravar o fluxo de dados do formulário no navegador Web cliente**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de desempenho

   * Criar um `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulários chamando o `PDFFormRenderSpec` do objeto `setCacheEnabled` método e transmissão `true`.
   * Defina a opção linearizada chamando o `PDFFormRenderSpec` do objeto `setLinearizedPDF` método e transmissão `true.`

1. Renderizar o formulário

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução para melhorar o desempenho.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da web cliente.
   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` object&#39;s `getOutputContent` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário chamando o `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

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

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Definir opções de tempo de execução de desempenho

   * Criar um `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de cache de formulários chamando o `PDFFormRenderSpec` do objeto `setCacheEnabled` e transmitindo true.
   * Defina a opção independente chamando o botão `PDFFormRenderSpec` do objeto `setStandAlone` e transmitindo true.
   * Defina a opção linearizada chamando o `PDFFormRenderSpec` do objeto `setLinearizedPDF` e transmitindo true.

1. Renderizar o formulário

   Chame o `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, transmita `null`.
   * A `PDFFormRenderSpecc` objeto que armazena opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método. (Esse argumento armazenará o valor do local).
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` objeto que conterá os resultados desta operação.

   A variável `renderPDFForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `FormResult` obtendo o valor do `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da web cliente.
   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
