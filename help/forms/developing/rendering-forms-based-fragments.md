---
title: Renderização de formulários com base em fragmentos
seo-title: Renderização de formulários com base em fragmentos
description: 'null'
seo-description: 'null'
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Renderização de formulários com base em fragmentos {#rendering-forms-based-on-fragments}

## Renderização de formulários com base em fragmentos {#rendering-forms-based-on-fragments-inner}

O serviço de Formulários pode renderizar formulários baseados em fragmentos criados por você usando o Designer. Um *fragmento* é uma parte reutilizável de um formulário e é salvo como um arquivo XDP separado que pode ser inserido em vários designs de formulário. Por exemplo, um fragmento pode incluir um bloco de endereço ou texto legal.

O uso dos fragmentos simplifica e acelera a criação e manutenção de uma grande quantidade de formulários. Ao criar um novo formulário, você insere uma referência ao fragmento necessário e o fragmento aparece no formulário. A referência do fragmento contém um subformulário que aponta para o arquivo XDP físico. Para obter informações sobre como criar designs de formulário com base em fragmentos, consulte [Designer de Formulários](https://www.adobe.com/go/learn_aemforms_designer_63)

Um fragmento pode incluir vários subformulários vinculados em um conjunto de subformulários de escolha. Os conjuntos de subformulários de escolha controlam a exibição de subformulários com base no fluxo de dados de uma conexão de dados. Instruções condicionais são usadas para determinar qual subformulário do conjunto aparece no formulário apresentado. Por exemplo, cada subformulário em um conjunto pode incluir informações para uma localização geográfica específica e o subformulário exibido pode ser determinado com base na localização do usuário.

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. Esses fragmentos incluem um único objeto de script que aparece como um filho de variáveis na paleta Hierarquia. Os fragmentos não podem ser criados a partir de scripts que são propriedades de outros objetos, por exemplo, scripts de evento, como validar, calcular ou inicializar.

Estas são as vantagens do uso de fragmentos:

* **Reutilização** de conteúdo: É possível usar fragmentos para reutilizar o conteúdo em vários designs de formulário. Quando você precisa usar parte do mesmo conteúdo em vários formulários, é mais rápido e simples usar um fragmento do que copiar ou recriar o conteúdo. O uso de fragmentos também garante que as partes de um design de formulário usadas frequentemente possuam conteúdo e aparência consistentes em todos os formulários de referência.
* **Atualizações** globais: É possível usar fragmentos para fazer alterações globais em vários formulários apenas uma vez, em um arquivo. É possível alterar o conteúdo, objetos de script, vínculos de dados, layout ou estilos em um fragmento, e todos os formulários XDP que fazem referência ao fragmento refletirão as alterações.
* Por exemplo, um elemento comum em vários formulários pode ser um bloco de endereços que inclui um objeto de lista suspensa para o país. Se for necessário atualizar os valores para o objeto de lista suspensa, abra muitos formulários para fazer as alterações. Se você incluir o bloco de endereços em um fragmento, será necessário abrir apenas um arquivo de fragmento para fazer as alterações.
* Para atualizar um fragmento em um formulário PDF, é necessário salvar o formulário novamente no Designer.
* **Criação** de formulários compartilhados: É possível usar fragmentos para compartilhar a criação de formulários entre vários recursos. Os desenvolvedores de formulário com experiência em script ou em outros recursos avançados do Designer podem desenvolver e compartilhar fragmentos que aproveitam as propriedades dinâmicas e de script. Os desenvolvedores de formulário podem usar esses fragmentos para dispor designs de formulário e garantir que todas as partes de um formulário tenham uma aparência e funcionalidade consistentes em diversos formulários criados por diversas pessoas.

### Montagem de um design de formulário montado usando fragmentos {#assembling-a-form-design-assembled-using-fragments}

É possível reunir um design de formulário para passar para o serviço de Formulários com base em vários fragmentos. Para montar vários fragmentos, use o serviço Assembler. Para ver um exemplo de como usar o serviço Montagem para criar um design de formulário usado por outros serviços do Forms (o serviço Saída), consulte [Criação de documentos PDF usando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments). Em vez de usar o serviço de Saída, você pode executar o mesmo fluxo de trabalho usando o serviço de Formulários.

Ao usar o serviço Assembler, você está transmitindo um design de formulário que foi montado usando fragmentos. O design de formulário criado não faz referência a outros fragmentos. Por outro lado, esse tópico discute a transmissão de um design de formulário que faz referência a outros fragmentos ao serviço de Formulários. No entanto, o design de formulário não foi montado pelo Assembler. Foi criado no Designer.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo baseado na Web que renderiza formulários com base em fragmentos, consulte [Criação de aplicativos da Web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário com base em fragmentos, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Especifique valores de URI.
1. Renderize o formulário.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de executar programaticamente uma operação de API do cliente do serviço Forms, é necessário criar um cliente do serviço Forms.

**Especificar valores de URI**

Para renderizar com êxito um formulário com base em fragmentos, é necessário garantir que o serviço de Formulários possa localizar o formulário e os fragmentos (arquivos XDP) aos quais o design de formulário faz referência. Por exemplo, suponha que o formulário seja chamado de PO.xdp e que esse formulário use dois fragmentos chamados FooterUS.xdp e FooterCanada.xdp. Nessa situação, o serviço Forms deve ser capaz de localizar os três arquivos XDP.

É possível organizar um formulário e seus fragmentos colocando-o em um local e os fragmentos em outro local, ou colocar todos os arquivos XDP no mesmo local. Para os fins desta seção, considere que todos os arquivos XDP estejam localizados no repositório do AEM Forms. Para obter informações sobre como colocar arquivos XDP no repositório do AEM Forms, consulte [Gravando recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).

Ao renderizar um formulário com base em fragmentos, é necessário referenciar apenas o formulário em si e não os fragmentos. Por exemplo, você deve consultar PO.xdp e não FooterUS.xdp ou FooterCanada.xdp. Certifique-se de colocar os fragmentos em um local onde o serviço de Formulários possa localizá-los.

**Renderizar o formulário**

Um formulário baseado em fragmentos pode ser renderizado da mesma forma que formulários não fragmentados. Ou seja, é possível renderizar o formulário como PDF, HTML ou Guias de formulário (obsoleto). O exemplo nesta seção renderiza um formulário com base em fragmentos como um formulário PDF interativo. (Consulte [Renderização de formulários](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interativos.)

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados do formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Renderizar formulários com base em fragmentos usando a API Java](#render-forms-based-on-fragments-using-the-java-api)

[Renderizar formulários com base em fragmentos usando a API de serviço da Web](#render-forms-based-on-fragments-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do serviço de formulários](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Como renderizar formulários PDF interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicativos da Web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar formulários com base em fragmentos usando a API Java {#render-forms-based-on-fragments-using-the-java-api}

Renderize um formulário com base em fragmentos usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Crie um `URLSpec` objeto que armazene valores de URI usando seu construtor.
   * Chame o método do `URLSpec` objeto `setApplicationWebRoot` e passe um valor de string que representa a raiz da Web do aplicativo.
   * Chame o método do `URLSpec` objeto `setContentRootURI` e transmita um valor de string que especifica o valor do URI raiz do conteúdo. Verifique se o design de formulário e os fragmentos estão localizados no URI raiz do conteúdo. Caso contrário, o serviço Forms lança uma exceção. Para fazer referência ao repositório, especifique `repository://`.
   * Chame o método do `URLSpec` objeto `setTargetURL` e passe um valor de string que especifique o valor do URL de destino para onde os dados do formulário são postados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar o URL para o qual um formulário é enviado para executar cálculos.

1. Renderizar o formulário

   Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um `com.adobe.idp.Document` objeto que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um `com.adobe.idp.Document` objeto vazio.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário com base em fragmentos.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o `InputStream` método do `read`objeto e transmitindo a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Renderização de formulários com base em fragmentos](#rendering-forms-based-on-fragments)

[Início rápido (modo SOAP): Como renderizar um formulário com base em fragmentos usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar formulários com base em fragmentos usando a API de serviço da Web {#render-forms-based-on-fragments-using-the-web-service-api}

Renderize um formulário com base em fragmentos usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Especificar valores de URI

   * Crie um `URLSpec` objeto que armazene valores de URI usando seu construtor.
   * Chame o método do `URLSpec` objeto `setApplicationWebRoot` e passe um valor de string que representa a raiz da Web do aplicativo.
   * Chame o método do `URLSpec` objeto `setContentRootURI` e transmita um valor de string que especifica o valor do URI raiz do conteúdo. Verifique se o design de formulário está localizado no URI raiz do conteúdo. Caso contrário, o serviço Forms lança uma exceção. Para fazer referência ao repositório, especifique `repository://`.
   * Chame o método do `URLSpec` objeto `setTargetURL` e passe um valor de string que especifique o valor do URL de destino para onde os dados do formulário são postados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar o URL para o qual um formulário é enviado para executar cálculos.

1. Renderizar o formulário

   Chame o método do `FormsService` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um `BLOB` objeto que contém dados a serem unidos ao formulário. Se você não deseja unir dados, passe `null`.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Observe que a opção PDF marcado não pode ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF marcado pode ser definida.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo método. Esse parâmetro é usado para armazenar o formulário renderizado.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo método. Esse argumento armazenará o número de páginas no formulário.
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método. Esse argumento armazenará o valor de localidade.
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Obtenha o tipo de conteúdo do `BLOB` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Renderização de formulários com base em fragmentos](#rendering-forms-based-on-fragments)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
