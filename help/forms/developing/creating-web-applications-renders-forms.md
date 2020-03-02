---
title: Criação de aplicativos da Web que renderizam formulários
seo-title: Criação de aplicativos da Web que renderizam formulários
description: 'null'
seo-description: 'null'
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Criação de aplicativos da Web que renderizam formulários {#creating-web-applications-thatrenders-forms}

## Criação de aplicativos da Web que renderizam formulários {#creating-web-applications-that-renders-forms}

Você pode criar um aplicativo baseado na Web que use servlets Java para chamar o serviço de Formulários e renderizar formulários. Uma vantagem de usar um servlet Java™ é que você pode gravar o valor de retorno do processo em um navegador da Web cliente. Ou seja, um servlet Java pode ser usado como o link entre o serviço Forms que retorna um formulário e um navegador da Web cliente.

>[!NOTE]
>
>Esta seção descreve como criar um aplicativo baseado na Web que usa um servlet Java que chama o serviço Forms e renderiza formulários com base em fragmentos. (Consulte [Renderização de formulários com base em fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)

Usando um servlet Java, você pode gravar um formulário em um navegador da Web do cliente para que um cliente possa visualizar e inserir dados no formulário. Depois de preencher o formulário com dados, o usuário da Web clica em um botão Enviar localizado no formulário para enviar informações de volta ao servlet Java, onde os dados podem ser recuperados e processados. Por exemplo, os dados podem ser enviados para outro processo.

Esta seção discute como criar um aplicativo baseado na Web que permite ao usuário selecionar dados de formulário baseados em EUA ou dados de formulário baseados em Canadá, conforme mostrado na ilustração a seguir.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

O formulário que é renderizado é um formulário baseado em fragmentos. Ou seja, se o usuário selecionar dados americanos, o formulário retornado usará fragmentos com base em dados americanos. Por exemplo, o rodapé do formulário contém um endereço americano, como mostrado na ilustração a seguir.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

Da mesma forma, se o usuário selecionar dados canadenses, o formulário retornado conterá um endereço canadense, como mostrado na ilustração a seguir.

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>Para obter informações sobre como criar designs de formulário com base em fragmentos, consulte [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)de Formulários.

**Arquivos de exemplo**

Esta seção usa arquivos de amostra que podem ser localizados no seguinte local:

&lt;diretório *de instalação do* Forms Designer>/Samples/Forms/Purchase Order/Form Fragments

onde &lt;diretório ** de instalação> é o caminho de instalação. Para os fins do aplicativo cliente, o arquivo Purchase Order Dynamic.xdp foi copiado desse local de instalação e implantado em um aplicativo do Forms chamado *Applications/FormsApplication*. O arquivo Purchase Order Dynamic.xdp é colocado em uma pasta chamada FormsFolder. Da mesma forma, os fragmentos são colocados na pasta denominada Fragmentos, conforme mostrado na ilustração a seguir.

![cw_cw_fragmentsrepositório](assets/cw_cw_fragmentsrepository.png)

Para acessar o design de formulário Purchase Order Dynamic.xdp, especifique `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` como o nome do formulário (o primeiro parâmetro passado para o `renderPDFForm` método) e `repository:///` como o valor do URI raiz do conteúdo.

Os arquivos de dados XML usados pelo aplicativo da Web foram movidos da pasta Dados para `C:\Adobe`(o sistema de arquivos que pertence ao servidor de aplicativos J2EE que hospeda o AEM Forms). Os nomes dos arquivos são Purchase Order *Canada.xml* e Purchase Order *US.xml*.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo de Formulários usando o Workbench, consulte Ajuda [do](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.

### Resumo das etapas {#summary-of-steps}

Para criar aplicativos baseados na Web que renderizam formulários com base em fragmentos, execute as seguintes etapas:

1. Crie um novo projeto da Web.
1. Criar lógica de aplicativo Java que representa o servlet Java.
1. Crie a página da Web para o aplicativo da Web.
1. Compacte o aplicativo da Web em um arquivo WAR.
1. Implante o arquivo WAR no servidor de aplicativos J2EE.
1. Teste seu aplicativo da Web.

>[!NOTE]
>
>Algumas dessas etapas dependem do aplicativo J2EE no qual o AEM Forms é implantado. Por exemplo, o método usado para implantar um arquivo WAR depende do servidor de aplicativos J2EE que você está usando. Esta seção supõe que o AEM Forms seja implantado no JBoss®.

### Criação de um projeto da Web {#creating-a-web-project}

A primeira etapa para criar um aplicativo da Web que contenha um servlet Java que possa chamar o serviço Forms é criar um novo projeto da Web. O Java IDE no qual este documento se baseia é o Eclipse 3.3. Usando o Eclipse IDE, crie um projeto da Web e adicione os arquivos JAR necessários ao seu projeto. Finalmente, adicione uma página HTML chamada *index.html* e um servlet Java ao seu projeto.

A lista a seguir especifica os arquivos JAR que você deve adicionar ao seu projeto da Web:

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

Para obter a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Para criar um projeto da Web:**

1. Inicie o Eclipse e clique em **Arquivo** > **Novo projeto**.
1. Na caixa de diálogo **Novo projeto** , selecione **Web** > Projeto **da Web** dinâmico.
1. Digite `FragmentsWebApplication` o nome do projeto e clique em **Concluir**.

**Para adicionar arquivos JAR necessários ao seu projeto:**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `FragmentsWebApplication` projeto e selecione **Propriedades**.
1. Clique em caminho **de compilação** Java e clique na guia **Bibliotecas** .
1. Clique no botão **Adicionar JARs** externos e navegue até os arquivos JAR a serem incluídos.

**Para adicionar um servlet Java ao seu projeto:**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `FragmentsWebApplication` projeto e selecione **Novo** > **Outro**.
1. Expanda a pasta **Web** , selecione **Servlet** e clique em **Avançar**.
1. Na caixa de diálogo Criar servlet, digite `RenderFormFragment` o nome do servlet e clique em **Concluir**.

**Para adicionar uma página HTML ao seu projeto:**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `FragmentsWebApplication` projeto e selecione **Novo** > **Outro**.
1. Expanda a pasta **Web** , selecione **HTML** e clique em **Avançar**.
1. Na caixa de diálogo Novo HTML, digite `index.html` o nome do arquivo e clique em **Concluir**.

>[!NOTE]
>
>Para obter informações sobre como criar a página HTML que chama o servlet `RenderFormFragment` Java, consulte[Criação da página](/help/forms/developing/rendering-forms.md#creating-the-web-page)da Web.

### Criando lógica de aplicativo Java para o servlet {#creating-java-application-logic-for-the-servlet}

Você cria uma lógica de aplicativo Java que chama o serviço Forms de dentro do servlet Java. O código a seguir mostra a sintaxe do `RenderFormFragment` Java Servlet:

```as3
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

Normalmente, você não coloca o código do cliente dentro de um servlet `doGet` ou método Java `doPost` . Uma prática de programação melhor é colocar esse código em uma classe separada, instanciar a classe de dentro do `doPost` método (ou `doGet` método) e chamar os métodos apropriados. No entanto, para a brevidade do código, os exemplos de código nesta seção são reduzidos ao mínimo e os exemplos de código são colocados no `doPost` método.

Para renderizar um formulário com base em fragmentos usando a API de serviço do Forms, execute as seguintes tarefas:

1. Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.
1. Recupere o valor do botão de opção enviado a partir do formulário HTML e especifique se deseja usar dados americanos ou canadenses. Se o American for enviado, crie um `com.adobe.idp.Document` que armazene os dados localizados no *Purchase Order US.xml*. Da mesma forma, se for canadense, crie um arquivo `com.adobe.idp.Document` que armazene os dados localizados no arquivo *Purchase Order Canada.xml* .
1. Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
1. Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
1. Crie um `URLSpec` objeto que armazene valores de URI usando seu construtor.
1. Chame o método do `URLSpec` objeto `setApplicationWebRoot` e passe um valor de string que representa a raiz da Web do aplicativo.
1. Chame o método do `URLSpec` objeto `setContentRootURI` e transmita um valor de string que especifica o valor do URI raiz do conteúdo. Verifique se o design de formulário e os fragmentos estão localizados no URI raiz do conteúdo. Caso contrário, o serviço Forms lança uma exceção. Para fazer referência ao repositório do AEM Forms, especifique `repository://`.
1. Chame o método do `URLSpec` objeto `setTargetURL` e passe um valor de string que especifique o valor do URL de destino para onde os dados do formulário são postados. Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar o URL para o qual um formulário é enviado para executar cálculos.
1. Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um `com.adobe.idp.Document` objeto que contém dados para unir ao formulário (criado na etapa 2).
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Para obter mais informações, consulte Referência [da API de formulários](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário com base em fragmentos.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
1. Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
1. Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
1. Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
1. Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
1. Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o `InputStream` método do `read`objeto e transmitindo a matriz de bytes como um argumento.
1. Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

O exemplo de código a seguir representa o servlet Java que chama o serviço Forms e renderiza um formulário com base em fragmentos.

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://[server]:[port]/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://[server]:[port]/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### Criação da página da Web {#creating-the-web-page}

A página da Web index.html fornece um ponto de entrada para o servlet Java e chama o serviço Forms. Esta página da Web é um formulário HTML básico que contém dois botões de opção e um botão Enviar. O nome dos botões de opção é radio. Quando o usuário clica no botão Enviar, os dados do formulário são publicados no servlet `RenderFormFragment` Java.

O servlet Java captura os dados publicados da página HTML usando o seguinte código Java:

```as3
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

O código HTML a seguir está localizado no arquivo index.html que foi criado durante a configuração do ambiente de desenvolvimento. (Consulte [Criação de um projeto](/help/forms/developing/rendering-forms.md#creating-a-web-project)da Web.)

```as3
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://[server]:[port]/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### Empacotamento do aplicativo da Web {#packaging-the-web-application}

Para implantar o servlet Java que chama o serviço Forms, empacote seu aplicativo Web em um arquivo WAR. Verifique se os arquivos JAR externos dos quais a lógica comercial do componente depende, como adobe-livecycle-client.jar e adobe-forms-client.jar, também estão incluídos no arquivo WAR.

**Para disponibilizar um aplicativo da Web em um arquivo WAR:**

1. Na janela **Project Explorer** , clique com o botão direito do mouse no `FragmentsWebApplication` projeto e selecione **Exportar** > arquivo **** WAR.
1. Na caixa de texto do módulo **da** Web, digite `FragmentsWebApplication` o nome do projeto Java.
1. Na caixa de texto **Destino** , digite `FragmentsWebApplication.war`**para **o nome do arquivo, especifique o local do arquivo WAR e clique em Concluir.

### Implantação do arquivo WAR no servidor de aplicativos J2EE {#deploying-the-war-file-to-the-j2ee-application-server}

Você pode implantar o arquivo WAR no servidor de aplicativos J2EE no qual o AEM Forms é implantado. Depois que o arquivo WAR for implantado, você poderá acessar a página da Web HTML usando um navegador da Web.

**Para implantar o arquivo WAR no servidor de aplicativos J2EE:**

* Copie o arquivo WAR do caminho de exportação para `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### Testar seu aplicativo da Web {#testing-your-web-application}

Depois de implantar o aplicativo da Web, você pode testá-lo usando um navegador da Web. Supondo que você esteja usando o mesmo computador que está hospedando o AEM Forms, você pode especificar o seguinte URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   Selecione um botão de opção e clique no botão Enviar. Um formulário baseado em fragmentos será exibido no navegador da Web. Se ocorrerem problemas, consulte o arquivo de log do servidor de aplicativos J2EE.

