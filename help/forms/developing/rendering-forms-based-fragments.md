---
title: Renderização do Forms com base em fragmentos
description: Use o serviço Forms para renderizar formulários com base em fragmentos criados usando o Designer.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2189'
ht-degree: 0%

---

# Renderização do Forms com base em fragmentos {#rendering-forms-based-on-fragments}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

## Renderização do Forms com base em fragmentos {#rendering-forms-based-on-fragments-inner}

O serviço Forms pode renderizar formulários com base em fragmentos criados usando o Designer. Um *fragmento* é uma parte reutilizável de um formulário e é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso de fragmentos simplifica e acelera a criação e a manutenção de um grande número de formulários. Ao criar um formulário, você insere uma referência ao fragmento necessário e o fragmento aparece no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico. Para obter informações sobre como criar designs de formulário com base em fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Um fragmento pode incluir vários subformulários que são envolvidos em um conjunto de subformulários de escolha. Os conjuntos de subformulários de escolha controlam a exibição de subformulários com base no fluxo de dados de uma conexão de dados. Use declarações condicionais para determinar qual subformulário do conjunto aparece no formulário entregue. Por exemplo, cada subformulário em um conjunto pode incluir informações de uma localização geográfica específica, e o subformulário exibido pode ser determinado com base na localização do usuário.

Um *fragmento de script* contém funções ou valores JavaScript reutilizáveis que são armazenados separadamente de qualquer objeto específico, como um analisador de datas ou uma invocação de serviço Web. Esses fragmentos incluem um único objeto de script que aparece como filho de variáveis na paleta Hierarquia. Os fragmentos não podem ser criados a partir de scripts que são propriedades de outros objetos, como scripts de evento como validar, calcular ou inicializar.

Estas são as vantagens de usar fragmentos:

* **Reutilização de conteúdo**: você pode usar fragmentos para reutilizar conteúdo em vários designs de formulário. Quando é necessário usar parte do mesmo conteúdo em vários formulários, é mais rápido e simples usar um fragmento do que copiar ou recriar o conteúdo. O uso de fragmentos também garante que as partes usadas com frequência de um design de formulário tenham conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações globais**: você pode usar fragmentos para fazer alterações globais em vários formulários apenas uma vez, em um único arquivo. Você pode alterar o conteúdo, os objetos de script, as associações de dados, o layout ou os estilos em um fragmento e todos os formulários XDP que fazem referência ao fragmento refletirão as alterações.
* Por exemplo, um elemento comum em muitos formulários pode ser um bloco de endereço que inclui um objeto de lista suspensa para o país. Se precisar atualizar os valores do objeto da lista suspensa, abra vários formulários para fazer as alterações. Se você incluir o bloco de endereços em um fragmento, só será necessário abrir um arquivo de fragmento para fazer as alterações.
* Para atualizar um fragmento em um formulário PDF, é necessário salvar novamente o formulário no Designer.
* **Criação de formulário compartilhado**: você pode usar fragmentos para compartilhar a criação de formulários entre vários recursos. Desenvolvedores de formulários com experiência em script ou outros recursos avançados do Designer podem desenvolver e compartilhar fragmentos que aproveitam os scripts e as propriedades dinâmicas. Os designers de formulário podem usar esses fragmentos para criar designs de formulário e garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em vários formulários criados por várias pessoas.

### Montagem de um design de formulário montado usando fragmentos {#assembling-a-form-design-assembled-using-fragments}

Você pode montar um design de formulário para passá-lo para o serviço Forms com base em vários fragmentos. Para montar vários fragmentos, use o serviço Assembler. Para ver um exemplo de uso do serviço de Montagem para criar um design de formulário usado por outros serviços do Forms (o serviço de Saída), consulte [Criação de Documentos de PDF usando Fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Em vez de usar o Serviço de saída, você pode executar o mesmo fluxo de trabalho usando o serviço Forms.

Ao usar o serviço Assembler, você está transmitindo um design de formulário que foi montado usando fragmentos. O design do formulário criado não faz referência a outros fragmentos. Por outro lado, este tópico discute a transmissão de um design de formulário que faz referência a outros fragmentos para o serviço do Forms. No entanto, o design do formulário não foi montado pela Assembler. Ele foi criado no Designer.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo baseado na Web que renderize formulários com base em fragmentos, consulte [Criação de Aplicativos Web que Renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário com base em fragmentos, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Especifique valores de URI.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms.

**Especificar valores de URI**

Para renderizar com êxito um formulário com base em fragmentos, você deve garantir que o serviço do Forms possa localizar o formulário e os fragmentos (os arquivos XDP) aos quais o design do formulário faz referência. Por exemplo, suponha que o formulário seja chamado PO.xdp e esse formulário use dois fragmentos chamados FooterUS.xdp e FooterCanada.xdp. Nessa situação, o serviço Forms deve ser capaz de localizar todos os três arquivos XDP.

Você pode organizar um formulário e seus fragmentos colocando o formulário em um local e os fragmentos em outro local, ou pode colocar todos os arquivos XDP no mesmo local. Para os fins desta seção, considere que todos os arquivos XDP estão no repositório do AEM Forms. Para obter informações sobre como colocar arquivos XDP no repositório do AEM Forms, consulte [Recursos de Escrita](/help/forms/developing/aem-forms-repository.md#writing-resources).

Ao renderizar um formulário com base em fragmentos, você deve fazer referência somente ao próprio formulário e não aos fragmentos. Por exemplo, você deve fazer referência a PO.xdp e não a FooterUS.xdp ou FooterCanada.xdp. Certifique-se de colocar os fragmentos em um local em que o serviço do Forms possa localizá-los.

**Renderizar o formulário**

Um formulário baseado em fragmentos pode ser renderizado da mesma maneira que formulários não fragmentados. Ou seja, você pode renderizar o formulário como PDF, HTML ou Guias de formulário (obsoleto). O exemplo nesta seção renderiza um formulário com base em fragmentos como um formulário PDF interativo. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Renderizar formulários com base em fragmentos usando a API Java](#render-forms-based-on-fragments-using-the-java-api)

[Renderizar formulários com base em fragmentos usando a API do serviço Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar formulários com base em fragmentos usando a API Java {#render-forms-based-on-fragments-using-the-java-api}

Renderize um formulário com base em fragmentos usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Crie um objeto `URLSpec` que armazene valores de URI usando seu construtor.
   * Invoque o método `setApplicationWebRoot` do objeto `URLSpec` e passe um valor de cadeia de caracteres que represente a raiz da Web do aplicativo.
   * Invoque o método `setContentRootURI` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor de URI da raiz do conteúdo. Verifique se o design do formulário e os fragmentos estão no URI da raiz de conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository://`.
   * Invoque o método `setTargetURL` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor da URL de destino para onde os dados de formulário são postados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Renderizar o formulário

   Chame o método `renderPDFForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário com base em fragmentos.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms com base em fragmentos](#rendering-forms-based-on-fragments)

[Início rápido (modo SOAP): renderização de um formulário com base em fragmentos usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar formulários com base em fragmentos usando a API do serviço Web {#render-forms-based-on-fragments-using-the-web-service-api}

Renderize um formulário com base em fragmentos usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Especificar valores de URI

   * Crie um objeto `URLSpec` que armazene valores de URI usando seu construtor.
   * Invoque o método `setApplicationWebRoot` do objeto `URLSpec` e passe um valor de cadeia de caracteres que represente a raiz da Web do aplicativo.
   * Invoque o método `setContentRootURI` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor de URI da raiz do conteúdo. Verifique se o design do formulário está no URI da raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository://`.
   * Invoque o método `setTargetURL` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor da URL de destino para onde os dados de formulário são postados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Renderizar o formulário

   Chame o método `renderPDFForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. A opção PDF marcado não poderá ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF com tags poderá ser definida.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Esse parâmetro é usado para armazenar o formulário renderizado.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. Esse argumento armazenará o número de páginas no formulário.
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. Esse argumento armazenará o valor do local.
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms com base em fragmentos](#rendering-forms-based-on-fragments)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
