---
title: Renderização de PDF forms interativos
description: Use o serviço Forms para renderizar PDF forms interativos em dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Você pode usar o serviço Forms para renderizar formulários interativos usando a API Java e a API do serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2455'
ht-degree: 0%

---

# Renderização de PDF forms interativos {#rendering-interactive-pdf-forms}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

O serviço Forms renderiza PDF forms interativos em dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Depois que um formulário interativo é renderizado, um usuário pode inserir dados em campos de formulário e clicar em um botão de envio localizado no formulário para enviar informações de volta para o serviço Forms. O Adobe Reader ou o Acrobat devem estar instalados no computador que hospeda o navegador da Web do cliente para que um formulário PDF interativo fique visível.

>[!NOTE]
>
>Antes de renderizar um formulário usando o serviço Forms, crie um design de formulário. Normalmente, um design de formulário é criado no Designer e salvo como um arquivo XDP. Para obter informações sobre como criar um design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exemplo de aplicativo de empréstimo**

Um exemplo de aplicativo de empréstimo é apresentado para demonstrar como o serviço Forms usa formulários interativos para coletar informações dos usuários. Esse aplicativo permite que um usuário preencha um formulário com os dados necessários para garantir um empréstimo e, em seguida, envie dados para o serviço do Forms. O diagrama a seguir mostra o fluxo lógico do aplicativo de empréstimo.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

A tabela a seguir descreve as etapas deste diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>O Servlet Java <code>GetLoanForm</code> é chamado de uma página de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O Servlet Java <code>GetLoanForm</code> usa a API do cliente do serviço Forms para renderizar o formulário de empréstimo para o navegador Web do cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Renderizar um formulário PDF interativo usando a API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Depois que o usuário preenche o formulário de empréstimo e clica no botão enviar, os dados são enviados para o Servlet Java <code>HandleData</code>. (Consulte <i>"Formulário de empréstimo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O Servlet Java <code>HandleData</code> usa a API do cliente de serviço Forms para processar o envio e recuperar dados de formulário. Os dados são armazenados em um banco de dados empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Manipulação de Forms Enviada</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Um formulário de confirmação é renderizado no navegador da Web. Dados como o nome e sobrenome do usuário são mesclados com o formulário antes de serem renderizados. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Preenchimento prévio de Forms com Layouts Fluxáveis</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Formulário de empréstimo**

Este formulário de empréstimo interativo é renderizado pelo Servlet Java `GetLoanForm` do aplicativo de empréstimo de amostra.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulário de confirmação**

Este formulário é renderizado pelo Servlet Java `HandleData` do aplicativo de empréstimo de exemplo.

![ri_ri_confirm](assets/ri_ri_confirm.png)

O Servlet Java `HandleData` preenche este formulário com o nome e sobrenome do usuário e a quantidade. Depois que o formulário é pré-preenchido, ele é enviado para o navegador da Web do cliente. (Consulte [Preenchimento prévio de Forms com Layouts Fluxáveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlets Java**

O exemplo de aplicativo de empréstimo é um exemplo de um aplicativo de serviço do Forms que existe como um Servlet Java. Um Java Servlet é um programa Java em execução em um servidor de aplicativos J2EE, como o WebSphere, e contém o código da API do cliente do serviço Forms.

O código a seguir mostra a sintaxe de um Servlet Java chamado GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, você não colocaria o código da API do cliente de serviço do Forms dentro de um método `doGet` ou `doPost` do Java Servlet. É uma prática de programação melhor colocar esse código em uma classe separada, instanciar a classe de dentro do método `doPost` (ou método `doGet`) e chamar os métodos apropriados. No entanto, para abreviar o código, os exemplos de código nesta seção são mantidos no mínimo e os exemplos de código são colocados no método `doPost`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumo das etapas**

Para renderizar um formulário PDF interativo, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Especifique valores de URI.
1. Anexe arquivos ao formulário (Opcional).
1. Renderize um formulário PDF interativo.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um objeto da API do cliente do Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço Web Forms, crie um objeto `FormsService`.

**Especificar valores de URI**

Você pode especificar valores de URI exigidos pelo serviço Forms para renderizar um formulário. Um design de formulário salvo como parte de um aplicativo do Forms pode ser referenciado usando o valor de URI da raiz de conteúdo `repository:///`. Por exemplo, considere o seguinte design de formulário chamado *Loan.xdp* localizado em um aplicativo do Forms chamado *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acessar este design de formulário, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como o nome do formulário (o primeiro parâmetro passado para o método `renderPDFForm`) e `repository:///` como o valor de URI da raiz do conteúdo.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo do Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

O caminho para um recurso em um aplicativo do Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Os seguintes valores mostram alguns exemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Ao renderizar um formulário interativo, você pode definir valores de URI, como a URL de destino na qual os dados do formulário são publicados. O URL de destino pode ser definido de uma das seguintes maneiras:

* No botão Enviar ao projetar o design do formulário no Designer
* Ao usar a API do cliente de serviço do Forms

Se o URL de destino for definido no design do formulário, não o substitua pela API do cliente de serviço do Forms. Ou seja, definir o URL de destino usando a API do Forms redefine o URL especificado no design do formulário para o especificado usando a API. Se desejar enviar o formulário PDF para a URL de destino especificada no design do formulário, defina programaticamente a URL de destino como uma cadeia de caracteres vazia.

Se você tiver um formulário que contenha um botão Enviar e um botão Calcular (com um script correspondente executado no servidor), será possível definir programaticamente a URL para onde o formulário é enviado para executar o script. Use o botão enviar no design do formulário para especificar a URL na qual os dados do formulário são publicados. (Consulte [Calcular Dados De Formulário](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Em vez de especificar um valor de URL para fazer referência a um arquivo XDP, você também pode passar uma instância `com.adobe.idp.Document` para o serviço Forms. A instância `com.adobe.idp.Document` contém um design de formulário. (Consulte [Passando documentos para o serviço Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Anexar arquivos ao formulário**

Você pode anexar arquivos a um formulário. Quando você renderiza um formulário PDF com anexos de arquivo, os usuários podem recuperar os anexos de arquivo no Acrobat usando o painel de anexos de arquivo. Você pode anexar diferentes tipos de arquivo a um formulário, como um arquivo de texto, ou a um arquivo binário, como um arquivo JPG/.

>[!NOTE]
>
>Anexar anexos de arquivo a um formulário é opcional.

**Renderizar um formulário de PDF interativo**

Para renderizar um formulário, use um design de formulário criado no Designer e salvo como um arquivo XDP ou PDF. Além disso, é possível renderizar um formulário criado com o Acrobat e salvo como um arquivo PDF. Para renderizar um formulário PDF interativo, chame o método `renderPDFForm` ou o método `renderPDFForm2` do objeto `FormsServiceClient`.

O `renderPDFForm` usa um objeto `URLSpec`. A raiz de conteúdo para o arquivo XDP é passada para o serviço Forms usando o método `setContentRootURI` do objeto `URLSpec`. O nome de design do Formulário ( `formQuery`) é passado como um valor de parâmetro separado. Os dois valores são concatenados para obter a referência absoluta para o design do formulário.

O método `renderPDFForm2` aceita uma instância `com.adobe.idp.Document` que contém o documento XDP ou PDF a ser renderizado.

>[!NOTE]
>
>A opção de tempo de execução de PDF marcado não pode ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF com tags poderá ser definida.

## Renderize um formulário PDF interativo usando a API Java {#render-an-interactive-pdf-form-using-the-java-api}

Renderize um formulário PDF interativo usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Especificar valores de URI

   * Crie um objeto `URLSpec` que armazene valores de URI usando seu construtor.
   * Invoque o método `setApplicationWebRoot` do objeto `URLSpec` e passe um valor de cadeia de caracteres que represente a raiz da Web do aplicativo.
   * Invoque o método `setContentRootURI` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor de URI da raiz de conteúdo. Verifique se o design do formulário está no URI da raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository:///`.
   * Invoque o método `setTargetURL` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor da URL de destino para onde os dados de formulário são postados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Anexar arquivos ao formulário

   * Crie um objeto `java.util.HashMap` para armazenar anexos de arquivo usando seu construtor.
   * Invoque o método `put` do objeto `java.util.HashMap` para cada arquivo a ser anexado ao formulário renderizado. Transmita os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo de arquivo, incluindo a extensão do nome do arquivo.

   * Um objeto `com.adobe.idp.Document` que contém o anexo de arquivo.

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário. Esta etapa é opcional e você pode passar `null` se não quiser enviar anexos de arquivo.

1. Renderizar um formulário PDF interativo

   Invoque o método `renderPDFForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

## Renderize um formulário PDF interativo usando a API do serviço Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Renderize um formulário PDF interativo usando a API (serviço da Web) do Forms:

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Especificar valores de URI

   * Crie um objeto `URLSpec` que armazene valores de URI usando seu construtor.
   * Invoque o método `setApplicationWebRoot` do objeto `URLSpec` e passe um valor de cadeia de caracteres que represente a raiz da Web do aplicativo.
   * Invoque o método `setContentRootURI` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor de URI da raiz de conteúdo. Verifique se o design do formulário está no URI da raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository:///`.
   * Invoque o método `setTargetURL` do objeto `URLSpec` e passe um valor de cadeia de caracteres que especifique o valor da URL de destino para onde os dados de formulário são postados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Anexar arquivos ao formulário

   * Crie um objeto `java.util.HashMap` para armazenar anexos de arquivo usando seu construtor.
   * Invoque o método `put` do objeto `java.util.HashMap` para cada arquivo a ser anexado ao formulário renderizado. Transmita os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo de arquivo, incluindo a extensão do nome do arquivo

   * Um objeto `BLOB` que contém o anexo de arquivo

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário.

1. Renderizar um formulário PDF interativo

   Invoque o método `renderPDFForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário.)
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. (Esse argumento armazenará o valor do local.)
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.
