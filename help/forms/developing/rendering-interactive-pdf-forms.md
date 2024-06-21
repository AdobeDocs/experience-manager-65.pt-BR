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
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2455'
ht-degree: 0%

---

# Renderização de PDF forms interativos {#rendering-interactive-pdf-forms}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O serviço Forms renderiza PDF forms interativos em dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Depois que um formulário interativo é renderizado, um usuário pode inserir dados em campos de formulário e clicar em um botão de envio localizado no formulário para enviar informações de volta para o serviço Forms. O Adobe Reader ou o Acrobat devem estar instalados no computador que hospeda o navegador da Web do cliente para que um formulário PDF interativo fique visível.

>[!NOTE]
>
>Antes de renderizar um formulário usando o serviço Forms, crie um design de formulário. Normalmente, um design de formulário é criado no Designer e salvo como um arquivo XDP. Para obter informações sobre como criar um design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exemplo de pedido de empréstimo**

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
   <td><p>A variável <code>GetLoanForm</code> O Java Servlet é chamado de uma página de HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>A variável <code>GetLoanForm</code> O Java Servlet usa a API do cliente do serviço Forms para renderizar o formulário de empréstimo para o navegador da Web do cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Renderize um formulário PDF interativo usando a API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Depois que o usuário preenche o formulário de empréstimo e clica no botão enviar, os dados são enviados para o <code>HandleData</code> Servlet Java. (Consulte <i>"Formulário de empréstimo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>A variável <code>HandleData</code> O Java Servlet usa a API do cliente de serviço do Forms para processar o envio e a recuperação de formulários de dados. Os dados são armazenados em um banco de dados empresarial. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Manuseio de Forms enviado</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Um formulário de confirmação é renderizado no navegador da Web. Dados como o nome e sobrenome do usuário são mesclados com o formulário antes de serem renderizados. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Pré-preenchimento do Forms com layouts fluíveis</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Formulário de empréstimo**

Este formulário de empréstimo interativo é renderizado pelo aplicativo de empréstimo de amostra do `GetLoanForm` Servlet Java.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulário de confirmação**

Este formulário é renderizado pela amostra do aplicativo de empréstimo `HandleData` Servlet Java.

![ri_ri_confirm](assets/ri_ri_confirm.png)

A variável `HandleData` O Java Servlet preenche este formulário com o nome e sobrenome do usuário e a quantidade. Depois que o formulário é pré-preenchido, ele é enviado para o navegador da Web do cliente. (Consulte [Pré-preenchimento do Forms com layouts fluíveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

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

Normalmente, você não colocaria o código da API do cliente de serviço do Forms em um `doGet` ou `doPost` método. É uma prática de programação melhor colocar esse código em uma classe separada, instanciar a classe de dentro do `doPost` método (ou `doGet` ) e chame os métodos apropriados. No entanto, para abreviar o código, os exemplos de código nesta seção são reduzidos ao mínimo e os exemplos de código são colocados no `doPost` método.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um objeto da API do cliente do Forms. Se estiver usando a API Java, crie uma `FormsServiceClient` objeto. Se estiver usando a API do serviço Web Forms, crie uma `FormsService` objeto.

**Especificar valores de URI**

Você pode especificar valores de URI exigidos pelo serviço Forms para renderizar um formulário. Um design de formulário salvo como parte de um aplicativo do Forms pode ser referenciado usando o valor do URI da raiz do conteúdo `repository:///`. Por exemplo, considere o seguinte design de formulário chamado *Empréstimo.xdp* localizado em um aplicativo do Forms chamado *AplicativoFormulários*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acessar este design de formulário, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como o nome do formulário (o primeiro parâmetro passado para o `renderPDFForm` ) e `repository:///` como o valor de URI da raiz do conteúdo.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

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

Se você tiver um formulário que contenha um botão Enviar e um botão Calcular (com um script correspondente executado no servidor), será possível definir programaticamente a URL para onde o formulário é enviado para executar o script. Use o botão enviar no design do formulário para especificar a URL na qual os dados do formulário são publicados. (Consulte [Cálculo de dados de formulário](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Em vez de especificar um valor de URL para fazer referência a um arquivo XDP, você também pode passar um `com.adobe.idp.Document` para o serviço Forms. A variável `com.adobe.idp.Document` instância contém um design de formulário. (Consulte [Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Anexar arquivos ao formulário**

Você pode anexar arquivos a um formulário. Quando você renderiza um formulário PDF com anexos de arquivo, os usuários podem recuperar os anexos de arquivo no Acrobat usando o painel de anexos de arquivo. Você pode anexar diferentes tipos de arquivo a um formulário, como um arquivo de texto, ou a um arquivo binário, como um arquivo JPG/.

>[!NOTE]
>
>Anexar anexos de arquivo a um formulário é opcional.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário, use um design de formulário criado no Designer e salvo como um arquivo XDP ou PDF. Além disso, é possível renderizar um formulário criado com o Acrobat e salvo como um arquivo PDF. Para renderizar um formulário PDF interativo, chame o `FormsServiceClient` do objeto `renderPDFForm` método ou `renderPDFForm2` método.

A variável `renderPDFForm` usa um `URLSpec` objeto. A raiz de conteúdo para o arquivo XDP é passada para o serviço Forms usando o `URLSpec` do objeto `setContentRootURI` método. O nome do design do formulário ( `formQuery`) é passado como um valor de parâmetro separado. Os dois valores são concatenados para obter a referência absoluta para o design do formulário.

A variável `renderPDFForm2` o método aceita um `com.adobe.idp.Document` instância que contém o documento XDP ou PDF a ser renderizado.

>[!NOTE]
>
>A opção de tempo de execução de PDF marcado não pode ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF com tags poderá ser definida.

## Renderize um formulário PDF interativo usando a API Java {#render-an-interactive-pdf-form-using-the-java-api}

Renderize um formulário PDF interativo usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Criar um `URLSpec` objeto que armazena valores URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que represente a raiz da web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifique o valor do URI raiz do conteúdo. Verifique se o design do formulário está no URI da raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository:///`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmitem um valor de string que especifica o valor da URL de destino para onde os dados de formulário são publicados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Anexar arquivos ao formulário

   * Criar um `java.util.HashMap` objeto para armazenar anexos de arquivo usando seu construtor.
   * Chame o `java.util.HashMap` do objeto `put` para cada arquivo a ser anexado ao formulário renderizado. Transmita os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo de arquivo, incluindo a extensão do nome do arquivo.

   * A `com.adobe.idp.Document` objeto que contém o anexo de arquivo.

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário. Esta etapa é opcional e você pode passar `null` se não quiser enviar anexos de arquivo.

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

## Renderize um formulário PDF interativo usando a API do serviço Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Renderize um formulário PDF interativo usando a API (serviço da Web) do Forms:

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Especificar valores de URI

   * Criar um `URLSpec` objeto que armazena valores URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que represente a raiz da web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifique o valor do URI raiz do conteúdo. Verifique se o design do formulário está no URI da raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para referenciar o repositório, especifique `repository:///`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmitem um valor de string que especifica o valor da URL de destino para onde os dados de formulário são publicados. Se você definir o URL de destino no design do formulário, será possível passar uma cadeia de caracteres vazia. Você também pode especificar a URL para onde um formulário é enviado para realizar cálculos.

1. Anexar arquivos ao formulário

   * Criar um `java.util.HashMap` objeto para armazenar anexos de arquivo usando seu construtor.
   * Chame o `java.util.HashMap` do objeto `put` para cada arquivo a ser anexado ao formulário renderizado. Transmita os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo de arquivo, incluindo a extensão do nome do arquivo

   * A `BLOB` objeto que contém o anexo de arquivo

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário.

1. Renderizar um formulário PDF interativo

   Chame o `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, transmita `null`.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário.)
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método. (Esse argumento armazenará o valor do local.)
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` objeto que conterá os resultados desta operação.

   A variável `renderPDFForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `FormResult` obtendo o valor do `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `BLOB` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Gravar o fluxo de dados do formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.
