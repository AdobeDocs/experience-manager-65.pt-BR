---
title: Renderização do Forms com base em fragmentos
seo-title: Rendering Forms Based on Fragments
description: Use o serviço Forms para renderizar formulários baseados em fragmentos criados usando o Designer.
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 7%

---

# Renderização do Forms com base em fragmentos {#rendering-forms-based-on-fragments}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Renderização do Forms com base em fragmentos {#rendering-forms-based-on-fragments-inner}

O serviço Forms pode renderizar formulários baseados em fragmentos criados com o Designer. A *fragmento* O é uma parte reutilizável de um formulário e é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso dos fragmentos simplifica e acelera a criação e manutenção de uma grande quantidade de formulários. Ao criar um novo formulário, você insere uma referência ao fragmento necessário e o fragmento aparece no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico. Para obter informações sobre como criar designs de formulário com base em fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

Um fragmento pode incluir vários subformulários que estão vinculados em um conjunto de subformulários de escolha. Os conjuntos de subformulários de escolha controlam a exibição de subformulários com base no fluxo de dados de uma conexão de dados. Instruções condicionais são usadas para determinar qual subformulário do conjunto aparece no formulário apresentado. Por exemplo, cada subformulário em um conjunto pode incluir informações para uma localização geográfica específica e o subformulário exibido pode ser determinado com base na localização do usuário.

A *fragmento de script* contém funções ou valores JavaScript reutilizáveis armazenados separadamente de qualquer objeto específico, como analisador de data ou uma chamada de serviço da Web. Esses fragmentos incluem um único objeto de script que aparece como um filho de variáveis na paleta Hierarquia. Os fragmentos não podem ser criados a partir de scripts que são propriedades de outros objetos, por exemplo, scripts de evento, como validar, calcular ou inicializar.

Estas são as vantagens de usar fragmentos:

* **Reutilização de conteúdo**: É possível usar fragmentos para reutilizar o conteúdo em vários designs de formulário. Quando é necessário usar parte do mesmo conteúdo em vários formulários, é mais rápido e simples usar um fragmento do que copiar ou recriar o conteúdo. O uso de fragmentos também garante que as partes de um design de formulário usadas frequentemente possuam conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações globais**: É possível usar fragmentos para fazer alterações globais em vários formulários apenas uma vez, em um arquivo. É possível alterar o conteúdo, objetos de script, vínculos de dados, layout ou estilos em um fragmento, e todos os formulários XDP que fazem referência ao fragmento refletirão as alterações.
* Por exemplo, um elemento comum em vários formulários pode ser um bloco de endereços que inclui um objeto de lista suspensa para o país. Se for necessário atualizar os valores para o objeto da lista suspensa, abra vários formulários para fazer as alterações. Se você incluir o bloco de endereço em um fragmento, será necessário abrir apenas um arquivo de fragmento para fazer as alterações.
* Para atualizar um fragmento em um formulário PDF, é necessário salvar novamente o formulário no Designer.
* **Criação de formulário compartilhado**: É possível usar fragmentos para compartilhar a criação de formulários entre vários recursos. Os desenvolvedores de formulário com experiência em script ou em outros recursos avançados do Designer podem desenvolver e compartilhar fragmentos que aproveitam as propriedades dinâmicas e de script. Os desenvolvedores de formulário podem usar esses fragmentos para dispor designs de formulário e garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em diversos formulários criados por diversas pessoas.

### Montagem de um design de formulário montado com fragmentos {#assembling-a-form-design-assembled-using-fragments}

Você pode reunir um design de formulário para passar para o serviço Forms com base em vários fragmentos. Para montar vários fragmentos, use o serviço Assembler. Para ver um exemplo de uso do serviço Assemble para criar um design de formulário usado por outros serviços da Forms (o serviço Output ), consulte [Criação de documentos do PDF usando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Em vez de usar o serviço de Saída, você pode executar o mesmo fluxo de trabalho usando o serviço Forms.

Ao usar o serviço Assembler, você está transmitindo um design de formulário que foi montado usando fragmentos. O design de formulário criado não faz referência a outros fragmentos. Por outro lado, esse tópico discute a transmissão de um design de formulário que faça referência a outros fragmentos para o serviço Forms. No entanto, o design de formulário não foi montado pelo Assembler. Ele foi criado no Designer.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo baseado na Web que renderize formulários com base em fragmentos, consulte [Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário com base em fragmentos, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Especifique valores de URI.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms.

**Especificar valores de URI**

Para renderizar com êxito um formulário com base em fragmentos, é necessário garantir que o serviço Forms possa localizar o formulário e os fragmentos (os arquivos XDP) que o design de formulário faz referência. Por exemplo, suponha que o formulário seja chamado PO.xdp e que esse formulário use dois fragmentos chamados FooterUS.xdp e FooterCanada.xdp. Nessa situação, o serviço Forms deve ser capaz de localizar todos os três arquivos XDP.

Você pode organizar um formulário e seus fragmentos colocando o formulário em um local e os fragmentos em outro local, ou pode colocar todos os arquivos XDP no mesmo local. Para os fins desta seção, suponha que todos os arquivos XDP estejam localizados no repositório AEM Forms. Para obter informações sobre como colocar arquivos XDP no repositório AEM Forms, consulte [Escrever recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).

Ao renderizar um formulário com base em fragmentos, é necessário fazer referência somente ao próprio formulário e não aos fragmentos. Por exemplo, você deve referenciar PO.xdp e não FooterUS.xdp ou FooterCanada.xdp. Certifique-se de colocar os fragmentos em um local onde o serviço Forms possa localizá-los.

**Renderizar o formulário**

Um formulário baseado em fragmentos pode ser renderizado da mesma maneira que formulários não fragmentados. Ou seja, você pode renderizar o formulário como PDF, HTML ou Guias do formulário (obsoleto). O exemplo nesta seção renderiza um formulário com base em fragmentos como um formulário PDF interativo. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Renderizar formulários com base em fragmentos usando a API Java](#render-forms-based-on-fragments-using-the-java-api)

[Renderizar formulários com base em fragmentos usando a API do serviço da Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar formulários com base em fragmentos usando a API Java {#render-forms-based-on-fragments-using-the-java-api}

Renderize um formulário com base em fragmentos usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Crie um `URLSpec` que armazena valores de URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que representa a raiz da Web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifica o valor de URI da raiz de conteúdo. Verifique se o design de formulário e os fragmentos estão localizados no URI raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para fazer referência ao repositório, especifique `repository://`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmita um valor de string que especifica o valor do URL de destino para onde os dados do formulário são publicados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar a URL para a qual um formulário é enviado para executar cálculos.

1. Renderizar o formulário

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário com base em fragmentos.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderização do Forms com base em fragmentos](#rendering-forms-based-on-fragments)

[Início rápido (modo SOAP): Renderização de um formulário com base em fragmentos usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar formulários com base em fragmentos usando a API do serviço da Web {#render-forms-based-on-fragments-using-the-web-service-api}

Renderize um formulário com base em fragmentos usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Especificar valores de URI

   * Crie um `URLSpec` que armazena valores de URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que representa a raiz da Web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifica o valor de URI da raiz de conteúdo. Verifique se o design de formulário está localizado no URI raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para fazer referência ao repositório, especifique `repository://`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmita um valor de string que especifica o valor do URL de destino para onde os dados do formulário são publicados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar a URL para a qual um formulário é enviado para executar cálculos.

1. Renderizar o formulário

   Chame o `FormsService` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Observe que a opção PDF marcado não poderá ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF marcado poderá ser definida.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Esse parâmetro é usado para armazenar o formulário renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . Esse argumento armazenará o número de páginas no formulário.
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . Esse argumento armazenará o valor da localidade.
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `renderPDFForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `BLOB` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderização do Forms com base em fragmentos](#rendering-forms-based-on-fragments)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
