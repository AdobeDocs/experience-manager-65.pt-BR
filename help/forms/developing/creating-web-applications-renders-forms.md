---
title: Criando Aplicações Web que Renderiza Forms
seo-title: Criando Aplicações Web que Renderiza Forms
description: Crie um aplicativo baseado na Web que use servlets Java para chamar o serviço Forms e renderizar formulários. O servlet Java serve como o link entre o serviço Forms que retorna um formulário e um navegador da Web cliente.
seo-description: Crie um aplicativo baseado na Web que use servlets Java para chamar o serviço Forms e renderizar formulários. O servlet Java serve como o link entre o serviço Forms que retorna um formulário e um navegador da Web cliente.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Criando Aplicativos Web que Renderizam Forms {#creating-web-applications-thatrenders-forms}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Criando Aplicativos Web que Renderizam Forms {#creating-web-applications-that-renders-forms}

Você pode criar um aplicativo baseado na Web que use servlets Java para chamar o serviço Forms e renderizar formulários. Uma vantagem de usar um servlet Java™ é que você pode gravar o valor de retorno do processo em um navegador da Web cliente. Ou seja, um servlet Java pode ser usado como o link entre o serviço da Forms que retorna um formulário e um navegador da Web cliente.

>[!NOTE]
>
>Esta seção descreve como criar um aplicativo baseado na Web que use um servlet Java que chame o serviço Forms e renderize formulários baseados em fragmentos. (Consulte [Renderizar Forms com base em fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)

Usando um servlet Java, você pode gravar um formulário em um navegador da Web cliente para que um cliente possa visualizar e inserir dados no formulário. Depois de preencher o formulário com dados, o usuário da Web clica em um botão Enviar localizado no formulário para enviar informações de volta ao servlet Java, onde os dados podem ser recuperados e processados. Por exemplo, os dados podem ser enviados para outro processo.

Esta seção discute como criar um aplicativo baseado na web que permite que o usuário selecione dados de formulário com base em americano ou dados de formulário com base em Canadá, conforme mostrado na ilustração a seguir.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

O formulário renderizado é um formulário baseado em fragmentos. Ou seja, se o usuário selecionar dados americanos, o formulário retornado usará fragmentos com base em dados americanos. Por exemplo, o rodapé do formulário contém um endereço americano, como mostrado na ilustração a seguir.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

Da mesma forma, se o usuário selecionar dados canadenses, o formulário retornado conterá um endereço canadense, conforme mostrado na ilustração a seguir.

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>Para obter informações sobre como criar designs de formulário com base em fragmentos, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Arquivos de exemplo**

Esta seção usa arquivos de exemplo que podem ser localizados no seguinte local:

&lt;>Diretório de instalação do Forms Designer *>/Samples/Forms/Purchase Order/Form Fragments*

onde &lt;*diretório de instalação*> é o caminho de instalação. Para os fins do aplicativo cliente, o arquivo Purchase Order Dynamic.xdp foi copiado desse local de instalação e implantado em um aplicativo Forms chamado *Applications/FormsApplication*. O arquivo Purchase Order Dynamic.xdp é colocado em uma pasta chamada FormsFolder. Da mesma forma, os fragmentos são colocados na pasta Fragmentos, como mostrado na ilustração a seguir.

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Para acessar o design de formulário Purchase Order Dynamic.xdp, especifique `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` como o nome do formulário (o primeiro parâmetro passado para o método `renderPDFForm`) e `repository:///` como o valor do URI raiz do conteúdo.

Os arquivos de dados XML usados pelo aplicativo Web foram movidos da pasta Dados para `C:\Adobe` (o sistema de arquivos que pertence ao servidor de aplicativos J2EE que hospeda o AEM Forms). Os nomes de arquivo são Purchase Order *Canada.xml* e Purchase Order *US.xml*.

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo do Forms usando o Workbench, consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

### Resumo das etapas {#summary-of-steps}

Para criar aplicativos baseados na Web que renderizam formulários com base em fragmentos, execute as seguintes etapas:

1. Crie um novo projeto da Web.
1. Crie uma lógica de aplicativo Java que represente o servlet Java.
1. Crie a página da Web para o aplicativo da Web.
1. Compacte o aplicativo Web em um arquivo WAR.
1. Implante o arquivo WAR no servidor de aplicativos J2EE.
1. Teste seu aplicativo web.

>[!NOTE]
>
>Algumas dessas etapas dependem do aplicativo J2EE no qual o AEM Forms é implantado. Por exemplo, o método usado para implantar um arquivo WAR depende do servidor de aplicativos J2EE que você está usando. Esta seção supõe que o AEM Forms esteja implantado no JBoss®.

### Criação de um projeto da Web {#creating-a-web-project}

A primeira etapa para criar uma aplicação Web que contenha um servlet Java que possa chamar o serviço Forms é criar um novo projeto Web. O Java IDE no qual este documento se baseia é o Eclipse 3.3. Usando o Eclipse IDE, crie um projeto da Web e adicione os arquivos JAR necessários ao seu projeto. Finalmente, adicione uma página HTML chamada *index.html* e um servlet Java ao seu projeto.

A lista a seguir especifica os arquivos JAR que você deve adicionar ao seu projeto da Web:

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

Para obter a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Para criar um projeto da Web:**

1. Inicie o Eclipse e clique em **File** > **New Project**.
1. Na caixa de diálogo **Novo projeto**, selecione **Web** > **Projeto Web dinâmico**.
1. Digite `FragmentsWebApplication` para o nome do seu projeto e clique em **Concluir**.

**Para adicionar os arquivos JAR necessários ao seu projeto:**

1. Na janela Explorador de projetos, clique com o botão direito do mouse no projeto `FragmentsWebApplication` e selecione **Propriedades**.
1. Clique em **Caminho de compilação Java** e clique na guia **Bibliotecas**.
1. Clique no botão **Adicionar JARs externos** e navegue até os arquivos JAR a serem incluídos.

**Para adicionar um servlet Java ao seu projeto:**

1. Na janela Explorador de projetos, clique com o botão direito do mouse no projeto `FragmentsWebApplication` e selecione **Novo** > **Outro**.
1. Expanda a pasta **Web**, selecione **Servlet** e clique em **Próximo**.
1. Na caixa de diálogo Criar Servlet, digite `RenderFormFragment` para o nome do servlet e clique em **Concluir**.

**Para adicionar uma página HTML ao seu projeto:**

1. Na janela Explorador de projetos, clique com o botão direito do mouse no projeto `FragmentsWebApplication` e selecione **Novo** > **Outro**.
1. Expanda a pasta **Web**, selecione **HTML** e clique em **Próximo**.
1. Na caixa de diálogo Novo HTML, digite `index.html` para o nome do arquivo e clique em **Concluir**.

>[!NOTE]
>
>Para obter informações sobre como criar a página HTML que chama o `RenderFormFragment` servlet Java, consulte [Criação da página da Web](/help/forms/developing/rendering-forms.md#creating-the-web-page).

### Criando lógica de aplicativo Java para o servlet {#creating-java-application-logic-for-the-servlet}

Você cria uma lógica de aplicativo Java que chama o serviço Forms de dentro do servlet Java. O código a seguir mostra a sintaxe do `RenderFormFragment` Java Servlet:

```java
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

Normalmente, você não colocaria o código de cliente em um método `doGet` ou `doPost` do servlet Java. Uma prática de programação melhor é colocar esse código em uma classe separada, instanciar a classe do método `doPost` (ou método `doGet`) e chamar os métodos apropriados. No entanto, para a brevidade do código, os exemplos de código nesta seção são mantidos para um mínimo e os exemplos de código são colocados no método `doPost`.

Para renderizar um formulário com base em fragmentos usando a API do serviço do Forms, execute as seguintes tarefas:

1. Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Recupere o valor do botão de opção que é enviado do formulário HTML e especifica se os dados americanos ou canadenses devem ser usados. Se Americano for enviado, crie um `com.adobe.idp.Document` que armazene dados localizados em *Purchase Order US.xml*. Da mesma forma, se for canadense, crie um `com.adobe.idp.Document` que armazene dados localizados no arquivo *Purchase Order Canada.xml*.
1. Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
1. Crie um objeto `URLSpec` que armazene valores de URI usando seu construtor.
1. Chame o método `URLSpec` do objeto `setApplicationWebRoot` e transmita um valor de string que representa a raiz da Web do aplicativo.
1. Chame o método `URLSpec` do objeto e transmita um valor de string que especifica o valor do URI da raiz do conteúdo. `setContentRootURI` Verifique se o design de formulário e os fragmentos estão localizados no URI raiz do conteúdo. Caso contrário, o serviço Forms acionará uma exceção. Para fazer referência ao repositório do AEM Forms, especifique `repository://`.
1. Chame o método `URLSpec` do objeto e transmita um valor de string que especifica o valor do URL de destino para onde os dados do formulário são publicados. `setTargetURL` Se você definir o URL de destino no design de formulário, poderá passar uma string vazia. Também é possível especificar a URL para a qual um formulário é enviado para executar cálculos.
1. Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário (criado na etapa 2).
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `URLSpec` que contém valores de URI necessários para o serviço Forms renderizar um formulário com base em fragmentos.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
1. Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
1. Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e passando o tipo de conteúdo do objeto `com.adobe.idp.Document`.
1. Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
1. Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
1. Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o método `InputStream` do objeto e passando a matriz de bytes como um argumento.`read`
1. Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

O código de exemplo a seguir representa o servlet Java que chama o serviço Forms e renderiza um formulário com base em fragmentos.

```java
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
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
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
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
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

A página da Web index.html fornece um ponto de entrada para o servlet Java e chama o serviço Forms. Esta página da Web é um formulário HTML básico que contém dois botões de opção e um botão Enviar. O nome dos botões de opção é rádio. Quando o usuário clica no botão Enviar , os dados do formulário são publicados no `RenderFormFragment` servlet Java.

O servlet Java captura os dados publicados da página HTML usando o seguinte código Java:

```java
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

O código HTML a seguir está localizado no arquivo index.html que foi criado durante a configuração do ambiente de desenvolvimento. (Consulte [Criação de um projeto da Web](/help/forms/developing/rendering-forms.md#creating-a-web-project).)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
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

### Empacotando a aplicação web {#packaging-the-web-application}

Para implantar o servlet Java que chama o serviço Forms, coloque o aplicativo Web em um arquivo WAR. Certifique-se de que os arquivos JAR externos dos quais a lógica comercial do componente depende, como adobe-livecycle-client.jar e adobe-forms-client.jar, também estejam incluídos no arquivo WAR.

**Para empacotar um aplicativo Web em um arquivo WAR:**

1. Na janela **Explorador de Projetos**, clique com o botão direito do mouse no projeto `FragmentsWebApplication` e selecione **Exportar** > **Arquivo WAR**.
1. Na caixa de texto **Módulo Web**, digite `FragmentsWebApplication` para o nome do projeto Java.
1. Na caixa de texto **Destino**, digite `FragmentsWebApplication.war`**para o nome do arquivo**, especifique o local do arquivo WAR e clique em Concluir.

### Implantando o arquivo WAR no servidor de aplicativos J2EE {#deploying-the-war-file-to-the-j2ee-application-server}

Você pode implantar o arquivo WAR no servidor de aplicativos J2EE no qual o AEM Forms é implantado. Após a implantação do arquivo WAR, é possível acessar a página da Web HTML por meio de um navegador da Web.

**Para implantar o arquivo WAR no servidor de aplicativos J2EE:**

* Copie o arquivo WAR do caminho de exportação para `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### Testar sua aplicação web {#testing-your-web-application}

Depois de implantar a aplicação Web, você pode testá-la usando um navegador da Web. Supondo que você esteja usando o mesmo computador que hospeda o AEM Forms, você pode especificar o seguinte URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   Selecione um botão de opção e clique no botão Submit . Um formulário baseado em fragmentos será exibido no navegador da Web. Se ocorrerem problemas, consulte o arquivo de log do servidor de aplicativos J2EE.

