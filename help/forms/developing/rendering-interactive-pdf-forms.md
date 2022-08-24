---
title: Renderização de PDF forms interativos
seo-title: Rendering Interactive PDF Forms
description: Use o serviço Forms para renderizar PDF forms interativas para dispositivos cliente, normalmente navegadores da Web, para coletar informações dos usuários. Você pode usar o serviço Forms para renderizar formulários interativos usando a API do Java e a API do serviço da Web.
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# Renderização de PDF forms interativos {#rendering-interactive-pdf-forms}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms renderiza PDF forms interativas para dispositivos clientes, normalmente navegadores da Web, para coletar informações dos usuários. Depois que um formulário interativo é renderizado, o usuário pode inserir dados nos campos do formulário e clicar em um botão Enviar localizado no formulário para enviar informações de volta ao serviço da Forms. O Adobe Reader ou Acrobat deve ser instalado no computador que hospeda o navegador da Web cliente para que um formulário interativo do PDF fique visível.

>[!NOTE]
>
>Antes de renderizar um formulário usando o serviço Forms, crie um design de formulário. Normalmente, um design de formulário é criado no Designer e é salvo como um arquivo XDP. Para obter informações sobre como criar um design de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Exemplo de pedido de empréstimo**

Um exemplo de aplicativo de empréstimo é apresentado para demonstrar como o serviço Forms usa formulários interativos para coletar informações dos usuários. Esse aplicativo permite que um usuário preencha um formulário com os dados necessários para garantir um empréstimo e, em seguida, envie os dados para o serviço da Forms. O diagrama a seguir mostra o fluxo lógico do aplicativo de empréstimo.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

A tabela a seguir descreve as etapas neste diagrama.

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
   <td><p>O <code>GetLoanForm</code> O Java Servlet é chamado de uma página HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O <code>GetLoanForm</code> O Java Servlet usa a API do cliente de serviço do Forms para renderizar o formulário de empréstimo para o navegador da Web do cliente. (Consulte <a href="#render-an-interactive-pdf-form-using-the-java-api">Renderizar um formulário PDF interativo usando a API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Depois que o usuário preenche o formulário de empréstimo e clica no botão Enviar, os dados são submetidos ao <code>HandleData</code> Servlet Java. (Consulte <i>"Formulário de empréstimo"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O <code>HandleData</code> O Java Servlet usa a API do cliente de serviço do Forms para processar o envio do formulário e recuperar os dados do formulário. Os dados são armazenados em um banco de dados corporativo. (Consulte <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Manuseio de Forms Enviado</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Um formulário de confirmação é renderizado de volta ao navegador da Web. Dados como o nome e sobrenome do usuário são unidos ao formulário antes da renderização. (Consulte <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Pré-preenchimento do Forms com layouts flutuantes</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Formulário de empréstimo**

Este formulário de empréstimo interativo é renderizado pelo aplicativo de empréstimo de amostra `GetLoanForm` Servlet Java.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Formulário de confirmação**

Este formulário é renderizado pelo aplicativo de empréstimo de amostra `HandleData` Servlet Java.

![ri_ri_confirm](assets/ri_ri_confirm.png)

O `HandleData` O Java Servlet preenche este formulário com o nome e sobrenome do usuário, bem como a quantidade. Depois que o formulário é pré-preenchido, ele é enviado para o navegador da Web do cliente. (Consulte [Pré-preenchimento do Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlets Java**

O aplicativo de empréstimo de exemplo é um exemplo de um aplicativo de serviço Forms que existe como um Servlet Java. Um Servlet Java é um programa Java em execução em um servidor de aplicativos J2EE, como o WebSphere, e contém o código de API do cliente do serviço Forms.

O código a seguir mostra a sintaxe de um servlet Java chamado GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, você não colocaria o código da API do cliente de serviço do Forms em um servidor Java `doGet` ou `doPost` método . É melhor prática de programação colocar esse código em uma classe separada, instanciando a classe de dentro do `doPost` método (ou `doGet` e chame os métodos apropriados. No entanto, para a brevidade do código, os exemplos de código nesta seção são mantidos para um mínimo e os exemplos de código são colocados na variável `doPost` método .

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Resumo das etapas**

Para renderizar um formulário PDF interativo, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Especifique valores de URI.
1. Anexe arquivos ao formulário (Opcional).
1. Renderize um formulário PDF interativo.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um objeto de API do cliente do Forms. Se estiver usando a API do Java, crie um `FormsServiceClient` objeto. Se estiver usando a API do serviço da Web da Forms, crie um `FormsService` objeto.

**Especificar valores de URI**

Você pode especificar valores de URI exigidos pelo serviço Forms para renderizar um formulário. Um design de formulário que é salvo como parte de um aplicativo Forms pode ser referenciado usando o valor de URI raiz de conteúdo `repository:///`. Por exemplo, considere o seguinte design de formulário chamado *Loan.xdp* localizado em um aplicativo Forms chamado *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Para acessar esse design de formulário, especifique `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` como o nome do formulário (o primeiro parâmetro passado para a função `renderPDFForm` método) e `repository:///` como o valor do URI raiz do conteúdo.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo do Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

O caminho para um recurso localizado em um aplicativo Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Os valores a seguir mostram alguns exemplos de valores de URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Ao renderizar um formulário interativo, é possível definir valores de URI, como o URL de destino para onde os dados do formulário são postados. O URL de destino pode ser definido de uma das seguintes maneiras:

* No botão Enviar ao projetar o design de formulário no Designer
* Usando a API do cliente de serviço do Forms

Se o URL de destino for definido no design de formulário, não o substitua pela API do cliente de serviço do Forms. Ou seja, definir o URL de destino usando a API do Forms redefine o URL especificado no design de formulário para aquele especificado usando a API. Se desejar enviar o formulário PDF para o URL de destino especificado no design de formulário, defina programaticamente o URL de destino como uma string vazia.

Se você tiver um formulário que contém um botão Enviar e um botão Calcular (com um script correspondente executado no servidor), poderá definir programaticamente o URL para onde o formulário é enviado para executar o script. Use o botão Enviar no design de formulário para especificar o URL para onde os dados do formulário são publicados. (Consulte [Cálculo dos dados de formulário](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Em vez de especificar um valor de URL para fazer referência a um arquivo XDP, você também pode enviar uma `com.adobe.idp.Document` para o serviço Forms. O `com.adobe.idp.Document` A instância contém um design de formulário. (Consulte [Enviar documentos para o serviço do Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Anexar arquivos ao formulário**

É possível anexar arquivos a um formulário. Ao renderizar um formulário PDF com anexos de arquivo, os usuários podem recuperar os anexos de arquivo no Acrobat usando o painel de anexo de arquivo. É possível anexar diferentes tipos de arquivo a um formulário, como um arquivo de texto, ou a um arquivo binário, como um arquivo JPG.

>[!NOTE]
>
>Anexar anexos de arquivo a um formulário é opcional.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário, use um design de formulário criado no Designer e salvo como um arquivo XDP ou PDF. Além disso, é possível renderizar um formulário que foi criado usando o Acrobat e salvo como um arquivo PDF. Para renderizar um formulário PDF interativo, chame o `FormsServiceClient` do objeto `renderPDFForm` método ou `renderPDFForm2` método .

O `renderPDFForm` usa um `URLSpec` objeto. A raiz de conteúdo para o arquivo XDP é passada para o serviço Forms usando o `URLSpec` do objeto `setContentRootURI` método . O nome do design de formulário ( `formQuery`) é passado como um valor de parâmetro separado. Os dois valores são concatenados para obter a referência absoluta para o design de formulário.

O `renderPDFForm2` aceita um método `com.adobe.idp.Document` instância que contém o documento XDP ou PDF para renderização.

>[!NOTE]
>
>A opção de tempo de execução PDF marcado não poderá ser definida se o documento de entrada for um documento PDF. Se o arquivo de entrada for um arquivo XDP, a opção PDF marcado poderá ser definida.

## Renderizar um formulário PDF interativo usando a API Java {#render-an-interactive-pdf-form-using-the-java-api}

Renderize um formulário PDF interativo usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Especificar valores de URI

   * Crie um `URLSpec` que armazena valores de URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que representa a raiz da Web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifica o valor de URI da raiz de conteúdo. Verifique se o design de formulário está localizado no URI raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para fazer referência ao repositório, especifique `repository:///`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmita um valor de string que especifica o valor do URL de destino para onde os dados do formulário são publicados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar a URL para a qual um formulário é enviado para executar cálculos.

1. Anexar arquivos ao formulário

   * Crie um `java.util.HashMap` para armazenar anexos de arquivo usando seu construtor.
   * Chame o `java.util.HashMap` do objeto `put` para cada arquivo a ser anexado ao formulário renderizado. Passe os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo de arquivo, incluindo a extensão de nome de arquivo.
   * A `com.adobe.idp.Document` objeto que contém o anexo do arquivo.

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário. Esta etapa é opcional e você pode passar `null` se não quiser enviar anexos de arquivo.

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

## Renderizar um formulário PDF interativo usando a API do serviço da Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Renderize um formulário PDF interativo usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Especificar valores de URI

   * Crie um `URLSpec` que armazena valores de URI usando seu construtor.
   * Chame o `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que representa a raiz da Web do aplicativo.
   * Chame o `URLSpec` do objeto `setContentRootURI` e transmita um valor de string que especifica o valor de URI da raiz de conteúdo. Verifique se o design de formulário está localizado no URI raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para fazer referência ao repositório, especifique `repository:///`.
   * Chame o `URLSpec` do objeto `setTargetURL` e transmita um valor de string que especifica o valor do URL de destino para onde os dados do formulário são publicados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar a URL para a qual um formulário é enviado para executar cálculos.

1. Anexar arquivos ao formulário

   * Crie um `java.util.HashMap` para armazenar anexos de arquivo usando seu construtor.
   * Chame o `java.util.HashMap` do objeto `put` para cada arquivo a ser anexado ao formulário renderizado. Passe os seguintes valores para este método:

      * Um valor de string que especifica o nome do anexo do arquivo, incluindo a extensão de nome de arquivo
   * A `BLOB` objeto que contém o anexo de arquivo

   >[!NOTE]
   >
   >Repita essa etapa para cada arquivo a ser anexado ao formulário.

1. Renderizar um formulário PDF interativo

   Chame o `FormsService` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Isso é usado para armazenar o formulário PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . (Esse argumento armazenará o número de páginas no formulário.)
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . (Esse argumento armazenará o valor da localidade.)
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

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.
