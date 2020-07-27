---
title: Invocando processos de vida longa centrados em humanos
seo-title: Invocando processos de vida longa centrados em humanos
description: 'null'
seo-description: 'null'
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3669'
ht-degree: 0%

---


# Invocando processos de vida longa centrados em humanos {#invoking-human-centric-long-lived-processes}

Você pode invocar de forma programática processos de longa duração centrados em humanos que foram criados no Workbench usando estes aplicativos clientes:

* Um aplicativo cliente baseado na Web Java que usa a API de chamada. (Consulte [Invocar AEM Forms usando a API](/help/forms/developing/invoking-aem-forms-using-java.md)Java (/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)
* Um aplicativo ASP.NET que usa serviços da Web. (Consulte [Invocando AEM Forms Usando Serviços](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)da Web.)
* Um aplicativo cliente criado com Flex que usa Remoting. (Consulte [Invocar AEM Forms usando (Obsoleto para formulários AEM) AEM Forms Remota](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

O processo de longa duração chamado *FirstAppSolution/PreLoanProcess*. Você pode criar esse processo seguindo o tutorial especificado em [Criando seu primeiro aplicativo](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)de AEM Forms.

Um processo centrado no ser humano envolve uma tarefa à qual um usuário pode responder usando o Workspace. Por exemplo, usando o Workbench, você pode criar um processo que permite que um gerente bancário aprove ou negue uma aplicação de empréstimo. A ilustração a seguir mostra o processo *FirstAppSolution/PreLoanProcess*.

O processo *FirstAppSolution/PreLoanProcess* aceita um parâmetro de entrada chamado *formData* cujo tipo de dados é XML. Os dados XML são unidos a um design de formulário chamado *PreLoanForm.xdp*. A ilustração a seguir mostra um formulário que representa uma tarefa atribuída a um usuário para aprovar ou negar um aplicativo de empréstimo. O usuário aprova ou nega o aplicativo usando o Workspace. O usuário do Workspace pode aprovar a solicitação de empréstimo clicando no botão Aprovar mostrado na ilustração a seguir. Da mesma forma, o usuário pode negar a solicitação de empréstimo clicando no botão Negar.

Um processo de longa duração é chamado de forma assíncrona e não pode ser chamado de modo síncrono devido aos seguintes fatores:

* Um processo pode abranger uma quantidade significativa de tempo.
* Um processo pode estender-se por limites organizacionais.
* Um processo precisa de entrada externa para que seja concluído. Por exemplo, considere uma situação em que um formulário é enviado para um gerente que está fora do escritório. Nesse caso, o processo não é concluído até que o gerente retorne e preencha o formulário.

Quando um processo de longa duração é chamado, o AEM Forms cria um valor identificador de invocação como parte da criação de um registro. O registro rastreia o status do processo de longa duração e é armazenado no banco de dados do AEM Forms. Usando o valor do identificador de invocação, é possível rastrear o status do processo de longa duração. Além disso, você pode usar o valor do identificador de invocação do processo para executar operações do Process Manager, como encerrar uma instância de processo em execução.

>[!NOTE]
>
>Os AEM Forms não criam um valor de identificador de invocação ou um registro quando um processo de duração curta é chamado.

O `FirstAppSolution/PreLoanProcess` processo é chamado quando um candidato envia um aplicativo, que é representado como dados XML. O nome da variável do processo de entrada é `formData` e seu tipo de dados é XML. Para os fins desta discussão, suponha que os seguintes dados XML sejam usados como entrada no `FirstAppSolution/PreLoanProcess` processo.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

Os dados XML transmitidos para um processo devem corresponder aos campos localizados no formulário usado no processo. Caso contrário, os dados não serão exibidos no formulário. Todos os aplicativos que invocam o `FirstAppSolution/PreLoanProcess` processo devem passar para essa fonte de dados XML. Os aplicativos criados na *Chamada de processos* longevos centrados em humanos criam dinamicamente a fonte de dados XML a partir de valores que um usuário inseriu em um cliente da Web.

Usando um aplicativo cliente, você pode enviar os dados XML necessários ao processo *FirstAppSolution/PreLoanProcess* . Um processo de longa duração retorna um valor identificador de invocação como seu valor de retorno. A ilustração a seguir mostra os aplicativos clientes que chamam o processo de longa duração*FirstAppSolution/PreLoanProcess. Os aplicativos cliente enviam dados XML e recuperam um valor de string que representa o valor do identificador de invocação.

**Consulte também:**

[Criação de um aplicativo da Web Java que chama um processo de vida longa centrado no ser humano](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[Criação de um aplicativo da Web ASP.NET que chama um processo de vida longa centrado em humanos](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[Criação de um aplicativo cliente criado com o Flex que invoca um processo de longa duração centrado no ser humano](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## Criação de um aplicativo da Web Java que chama um processo de vida longa centrado no ser humano {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Você pode criar um aplicativo baseado na Web que use um servlet Java para chamar o `FirstAppSolution/PreLoanProcess` processo. Para chamar esse processo de um servlet Java, use a API de chamada no servlet Java. (Consulte [Invocando AEM Forms usando a API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)Java.)

A ilustração a seguir mostra um aplicativo cliente baseado na Web que publica o nome, o telefone (ou email) e os valores de quantidade. Esses valores são enviados para o servlet Java quando o usuário clica no botão Enviar aplicativo.

O servlet Java executa as seguintes tarefas:

* Recupera os valores publicados da página HTML para o servlet Java.
* Cria dinamicamente uma fonte de dados XML para passar para o processo *FirstAppSolution/PreLoanProcess* . O nome, telefone (ou email) e os valores de quantidade são especificados na fonte de dados XML.
* Chama o processo *FirstAppSolution/PreLoanProcess* usando a API Invocation do AEM Forms.
* Retorna o valor do identificador de invocação para o navegador da Web do cliente.

### Resumo das etapas {#summary-of-steps}

Para criar um aplicativo baseado na Web Java que chame o `FirstAppSolution/PreLoanProcess` processo, execute as seguintes etapas:

1. [Criar um projeto](invoking-human-centric-long-lived.md#create-a-web-project)da Web.
1. [Criar lógica do aplicativo Java para o servlet](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [Criar a página da Web para o aplicativo da Web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Compacte o aplicativo da Web em um arquivo](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)WAR.
1. [Implante o arquivo WAR para as AEM Forms](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)de hospedagem do servidor de aplicativos J2EE.
1. [Teste seu aplicativo](invoking-human-centric-long-lived.md#test-your-web-application)da Web.

>[!NOTE]
>
>Algumas dessas etapas dependem do aplicativo J2EE no qual os AEM Forms são implantados. Por exemplo, o método usado para implantar um arquivo WAR depende do servidor de aplicativos J2EE que você está usando. Pressupõe-se que os AEM Forms sejam implantados no JBoss®.

### Criar um projeto da Web {#create-a-web-project}

A primeira etapa para criar um aplicativo da Web é criar um projeto da Web. O IDE Java no qual esse documento se baseia é o Eclipse 3.3. Usando o Eclipse IDE, crie um projeto da Web e adicione os arquivos JAR necessários ao seu projeto. Adicione uma página HTML chamada *index.html* e um servlet Java ao seu projeto.

A lista a seguir especifica os arquivos JAR a serem incluídos no projeto da Web:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

Para obter a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

>[!NOTE]
>
>O arquivo J2EE.jar define os tipos de dados usados por um servlet Java. Você pode obter esse arquivo JAR do servidor de aplicativos J2EE no qual os AEM Forms são implantados.

**Criar um projeto da Web**

1. Eclipse do Start e clique em **Arquivo** > **Novo projeto**.
1. Na caixa de diálogo **Novo projeto** , selecione **Web** > Projeto **da Web** dinâmico.
1. Digite `InvokePreLoanProcess` o nome do seu projeto e clique em **Concluir**.

**Adicionar arquivos JAR necessários ao seu projeto**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `InvokePreLoanProcess` projeto e selecione **Propriedades**.
1. Clique em caminho **de compilação** Java e clique na guia **Bibliotecas** .
1. Clique no botão **Adicionar JARs** externos e navegue até os arquivos JAR a serem incluídos.

**Adicionar um servlet Java ao seu projeto**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `InvokePreLoanProcess` projeto e selecione **Novo** > **Outro**.
1. Expanda a pasta **Web** , selecione **Servlet** e clique em **Avançar**.
1. Na caixa de diálogo Criar servlet, digite `SubmitXML` o nome do servlet e clique em **Concluir**.

**Adicionar uma página HTML ao seu projeto**

1. Na janela do Project Explorer, clique com o botão direito do mouse no `InvokePreLoanProcess` projeto e selecione **Novo** > **Outro**.
1. Expanda a pasta **da Web** , selecione **HTML** e clique em **Avançar**.
1. Na caixa de diálogo Novo HTML, digite `index.html` o nome do arquivo e clique em **Concluir**.

>[!NOTE]
>
>Para obter informações sobre como criar conteúdo HTML que chama o servlet Java SubmitXML, consulte [Criar a página da Web para o aplicativo](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)da Web.

### Criar lógica do aplicativo Java para o servlet {#create-java-application-logic-for-the-servlet}

Crie uma lógica de aplicativo Java que chame o `FirstAppSolution/PreLoanProcess` processo de dentro do servlet Java. O código a seguir mostra a sintaxe do `SubmitXML` Java Servlet:

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

Normalmente, você não coloca o código do cliente dentro de um servlet `doGet` ou método Java `doPost` . Uma melhor prática de programação é colocar esse código em uma classe separada. Em seguida, instancie a classe de dentro do `doPost` método (ou `doGet` método) e chame os métodos apropriados. No entanto, para a brevidade do código, os exemplos de código são reduzidos ao mínimo e colocados no `doPost` método.

Para chamar o `FirstAppSolution/PreLoanProcess` processo usando a API de chamada, execute as seguintes tarefas:

1. Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.
1. Recupere o nome, telefone e valores de quantidade enviados da página HTML. Use esses valores para criar dinamicamente uma fonte de dados XML enviada para o `FirstAppSolution/PreLoanProcess` processo. Você pode usar `org.w3c.dom` classes para criar a fonte de dados XML (essa lógica do aplicativo é mostrada no exemplo de código a seguir).
1. Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
1. Crie um `ServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto. Um `ServiceClient` objeto permite que você chame uma operação de serviço. Ele lida com tarefas como localização, despacho e solicitações de invocação de roteamentos.
1. Crie um `java.util.HashMap` objeto usando seu construtor.
1. Chame o método `java.util.HashMap` `put` do objeto para cada parâmetro de entrada a ser passado para o processo de longa duração. Certifique-se de especificar o nome dos parâmetros de entrada do processo. Como o `FirstAppSolution/PreLoanProcess` processo requer um parâmetro de entrada do tipo `XML` (nomeado `formData`), você só precisa chamar o `put` método uma vez.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Crie um `InvocationRequest` objeto chamando o `ServiceClientFactory` método do `createInvocationRequest` objeto e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do processo de longa duração a ser chamado. Para invocar o `FirstAppSolution/PreLoanProcess` processo, especifique `FirstAppSolution/PreLoanProcess`.
   * Um valor de string que representa o nome da operação do processo. O nome da operação do processo de longa duração é `invoke`.
   * O `java.util.HashMap` objeto que contém os valores de parâmetro exigidos pela operação de serviço.
   * Um valor booliano que especifica `false`, o que cria uma solicitação assíncrona (esse valor é aplicável para chamar um processo de longa duração).

   >[!NOTE]
   >
   >*Um processo de duração curta pode ser chamado transmitindo o valor true como o quarto parâmetro do método createInvocationRequest. Passar o valor true cria uma solicitação síncrona.*

1. Envie a solicitação de invocação para AEM Forms, invocando o `ServiceClient` método do objeto `invoke` e transmitindo o `InvocationRequest` objeto. O `invoke` método retorna um `InvocationReponse` objeto.
1. Um processo de longa duração retorna um valor de string que representa um valor de identificação de invocação. Recupere esse valor chamando o `InvocationReponse` método do `getInvocationId` objeto.

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. Escreva o valor de identificação da invocação no navegador da Web do cliente. Você pode usar uma `java.io.PrintWriter` instância para gravar esse valor no navegador da Web do cliente.

### Start rápido: Invocando um processo de longa duração usando a API de chamada {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

O exemplo de código Java a seguir representa o servlet Java que chama o `FirstAppSolution/PreLoanProcess` processo.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### Criar a página da Web para o aplicativo da Web {#create-the-web-page-for-the-web-application}

A página da Web *index.html* fornece um ponto de entrada para o servlet Java que chama o `FirstAppSolution/PreLoanProcess` processo. Esta página da Web é um formulário HTML básico que contém um formulário HTML e um botão Enviar. Quando o usuário clica no botão Enviar, os dados do formulário são publicados no servlet `SubmitXML` Java.

O servlet Java captura os dados publicados da página HTML usando o seguinte código Java:

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

O código HTML a seguir representa o arquivo index.html que foi criado durante a configuração do ambiente de desenvolvimento. (Consulte [Criar um projeto](invoking-human-centric-long-lived.md#create-a-web-project)da Web.)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### Empacotar o aplicativo da Web em um arquivo WAR {#package-the-web-application-to-a-war-file}

Para implantar o servlet Java que chama o `FirstAppSolution/PreLoanProcess` processo, empacote seu aplicativo da Web em um arquivo WAR. Verifique se os arquivos JAR externos dos quais a lógica comercial do componente depende, como adobe-livecycle-client.jar e adobe-usermanager-client.jar, também estão incluídos no arquivo WAR.

A ilustração a seguir mostra o conteúdo do projeto Eclipse, que é empacotado em um arquivo WAR.

>[!NOTE]
>
>Na ilustração anterior, o arquivo JPG pode ser substituído por qualquer arquivo de imagem JPG.

**Compacte um aplicativo da Web em um arquivo WAR:**

1. Na janela **Project Explorer** , clique com o botão direito do mouse no `InvokePreLoanProcess` projeto e selecione **Exportar** > arquivo **** WAR.
1. Na caixa de texto do módulo **da** Web, digite `InvokePreLoanProcess` o nome do projeto Java.
1. Na caixa de texto **Destino** , digite `PreLoanProcess.war`**para **o nome do arquivo, especifique o local do arquivo WAR e clique em Concluir.

### Implantar o arquivo WAR nos AEM Forms de hospedagem do servidor de aplicativos J2EE {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

Implante o arquivo WAR no servidor de aplicativos J2EE no qual os AEM Forms são implantados. Para implantar o arquivo WAR no servidor de aplicativos J2EE, copie o arquivo WAR do caminho de exportação para `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>se o AEM Forms não estiver implantado no JBoss, você deverá implantar o arquivo WAR em conformidade com as AEM Forms de hospedagem do servidor de aplicativos J2EE.

### Testar seu aplicativo da Web {#test-your-web-application}

Depois de implantar o aplicativo da Web, você pode testá-lo usando um navegador da Web. Supondo que você esteja usando o mesmo computador que está hospedando AEM Forms, você pode especificar o seguinte URL:

* http://localhost:8080/PreLoanProcess/index.html

   Insira valores nos campos de formulário HTML e clique no botão Enviar aplicativo. Se ocorrerem problemas, consulte o arquivo de log do servidor de aplicativos J2EE.

>[!NOTE]
>
>Para confirmar que o aplicativo Java invocou o processo, o start Workspace e aceite o empréstimo.

## Criação de um aplicativo da Web ASP.NET que chama um processo de vida longa centrado em humanos {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

Você pode criar um aplicativo ASP.NET que chame o `FirstAppSolution/PreLoanProcess` processo. Para invocar este processo a partir de um aplicativo ASP.NET, use os serviços da Web. (Consulte [Invocando AEM Forms usando Serviços](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)da Web.)

A ilustração a seguir mostra um aplicativo cliente ASP.NET obtendo dados de um usuário final. Os dados são colocados em uma fonte de dados XML e enviados para o `FirstAppSolution/PreLoanProcess` processo quando o usuário clica no botão Enviar aplicativo.

Observe que depois que o processo é chamado, um valor identificador de invocação é exibido. Um valor identificador de invocação é criado como parte de um registro que acompanha o status do processo de longa duração.

O aplicativo ASP.NET executa as seguintes tarefas:

* Recupera os valores inseridos pelo usuário na página da Web.
* Cria dinamicamente uma fonte de dados XML transmitida para o processo* FirstAppSolution/PreLoanProcess *. Os três valores são especificados na fonte de dados XML.
* Chama o processo* FirstAppSolution/PreLoanProcess *usando os serviços da Web.
* Retorna o valor do identificador de invocação e o status da operação de longa duração para o navegador da Web do cliente.

### Resumo das etapas {#summary_of_steps-1}

Para criar um aplicativo ASP.NET capaz de invocar o processo FirstAppSolution/PreLoanProcess, execute as seguintes etapas:

1. [Crie um aplicativo](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)da Web ASP.NET.
1. [Crie uma página ASP que chame FirstAppSolution/PreLoanProcess](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [Execute o aplicativo](invoking-human-centric-long-lived.md#run-the-asp-net-application)ASP.NET.

### Criar um aplicativo da Web ASP.NET {#create-an-asp-net-web-application}

Crie uma Aplicação web do Microsoft .NET C# ASP.NET. A ilustração a seguir mostra o conteúdo do projeto ASP.NET chamado *InvokePreLoanProcess*.

Em Referências de serviço, há dois itens. O primeiro item é denominado* JobManager*. Essa referência permite que o aplicativo ASP.NET chame o serviço Gerenciador de tarefas. Este serviço retorna informações sobre o status de um processo de longa duração. Por exemplo, se o processo estiver em execução no momento, esse serviço retornará um valor numérico que especifica que o processo está em execução no momento. A segunda referência é&#x200B;*chamada de PreLoanProcess*. Esta referência de serviço representa a referência ao processo* FirstAppSolution/PreLoanProcess *. Depois de criar uma Referência de serviço, os tipos de dados associados ao serviço AEM Forms estão disponíveis para uso no seu projeto .NET.

**Criar um projeto ASP.NET:**

1. Start Microsoft Visual Studio 2008.
1. No menu **Arquivo** , selecione **Novo**, **Site**.
1. Na lista **Modelos** , selecione **ASP.NET Web Site**.
1. Na caixa **Local** , selecione um local para seu projeto. Dê um nome ao seu projeto *InvokePreLoanProcess*.
1. Na caixa **Idioma** , selecione Visual C#
1. Clique em OK.

**Adicionar referências de serviço:**

1. No menu Projeto, selecione **Adicionar referência** de serviço.
1. Na caixa de diálogo **Endereço** , especifique o WSDL para o serviço Gerenciador de tarefas.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. No campo Namespace, digite `JobManager`.
1. Click **Go** and then click **OK**.
1. No menu **Projeto** , selecione **Adicionar referência** de serviço.
1. Na caixa de diálogo **Endereço** , especifique o WSDL para o processo FirstAppSolution/PreLoanProcess.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. No campo Namespace, digite `PreLoanProcess`.
1. Click **Go** and then click **OK**.

>[!NOTE]
>
>Substitua `hiro-xp` pelo endereço IP das AEM Forms de hospedagem do servidor de aplicativos J2EE. A `lc_version` opção garante que a funcionalidade AEM Forms, como MTOM, esteja disponível. Sem especificar a `lc_version`opção, não é possível invocar AEM Forms usando MTOM. (Consulte [Invocando AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### Criar uma página ASP que chame FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

No projeto ASP.NET, adicione um formulário da Web (um arquivo ASPX) que seja responsável por exibir uma página HTML ao candidato a empréstimo. O formulário da Web se baseia em uma classe derivada de `System.Web.UI.Page`. A lógica do aplicativo C# que chama `FirstAppSolution/PreLoanProcess` está localizada no `Button1_Click` método (esse botão representa o botão Enviar aplicativo).

A ilustração a seguir mostra o aplicativo ASP.NET

A tabela a seguir lista os controles que fazem parte deste aplicativo ASP.NET.

<table>
 <thead>
  <tr>
   <th><p>Nome do controle</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>Especifica o nome e o sobrenome do cliente. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>Especifica o endereço de email ou telefone do cliente. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>Especifica a quantia do empréstimo.</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>Representa o botão Enviar aplicativo.</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>Um controle Rótulo que especifica o valor do identificador de invocação.</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>Um controle Rótulo que especifica o valor do status da tarefa. Esse valor é recuperado chamando o serviço Gerenciador de Jobs. </p></td>
  </tr>
 </tbody>
</table>

A lógica do aplicativo que faz parte do aplicativo ASP.NET deve criar dinamicamente uma fonte de dados XML para passar para o `FirstAppSolution/PreLoanProcess` processo. Os valores inseridos pelo candidato na página HTML devem ser especificados na fonte de dados XML. Esses valores de dados são mesclados no formulário quando o formulário é exibido no Workspace. As classes localizadas na `System.Xml` namespace são usadas para criar a fonte de dados XML.

Ao invocar um processo que requer dados XML de um aplicativo ASP.NET, um tipo de dados XML está disponível para você usar. Ou seja, você não pode passar uma `System.Xml.XmlDocument` instância para o processo. O nome totalmente qualificado desta instância XML a ser transmitida para o processo é `InvokePreLoanProcess.PreLoanProcess.XML`. Converta a `System.Xml.XmlDocument` instância em `InvokePreLoanProcess.PreLoanProcess.XML`. É possível executar essa tarefa usando o seguinte código.

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

Para criar uma página ASP que chame o `FirstAppSolution/PreLoanProcess` processo, execute as seguintes tarefas no `Button1_Click` método:

1. Crie um `FirstAppSolution_PreLoanProcessClient` objeto usando seu construtor padrão.
1. Crie um `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms e o tipo de codificação:

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, certifique-se de especificar `?blob=mtom`.

   >[!NOTE]
   >
   >Substitua `hiro-xp`* pelo endereço IP das AEM Forms de hospedagem do servidor de aplicativos J2EE. *

1. Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do membro de `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` dados. Converta o valor de retorno em `BasicHttpBinding`.
1. Defina o membro de `System.ServiceModel.BasicHttpBinding` dados do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
1. Ative a autenticação HTTP básica executando as seguintes tarefas:

   * Atribua o nome de usuário dos formulários AEM ao membro de dados `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * Atribua o valor da senha correspondente ao membro de dados `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * Atribua o valor constante `HttpClientCredentialType.Basic` ao membro de dados `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao membro de dados `BasicHttpBindingSecurity.Security.Mode`.

   O exemplo de código a seguir mostra essas tarefas.

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. Recupere os valores de nome, telefone e quantidade inseridos pelo usuário na página da Web. Use esses valores para criar dinamicamente uma fonte de dados XML enviada para o `FirstAppSolution/PreLoanProcess` processo. Crie uma `System.Xml.XmlDocument` que represente a fonte de dados XML a ser transmitida para o processo (essa lógica do aplicativo é mostrada no exemplo de código a seguir).
1. Converta a `System.Xml.XmlDocument` instância em `InvokePreLoanProcess.PreLoanProcess.XML` (essa lógica do aplicativo é mostrada no exemplo de código a seguir).
1. Chame o `FirstAppSolution/PreLoanProcess` processo invocando o `FirstAppSolution_PreLoanProcessClient` método do `invoke_Async` objeto. Esse método retorna um valor de string que representa o valor do identificador de invocação do processo de longa duração.
1. Crie um `JobManagerClient` usando seu construtor. (Certifique-se de ter definido uma referência de serviço para o serviço Gerenciador de tarefas.)
1. Repita as etapas 1-5. Especifique o seguinte URL para a etapa 2: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. Crie um `JobId` objeto usando seu construtor.
1. Defina o membro de `JobId` dados do `id` objeto com o valor de retorno do `FirstAppSolution_PreLoanProcessClient` método do `invoke_Async` objeto.
1. Atribua o `value` true ao membro de `JobId` dados do `persistent` objeto.
1. Crie um `JobStatus` objeto chamando o `JobManagerService` método do objeto `getStatus` e transmitindo o `JobId` .
1. Obtenha o valor de status recuperando o valor do membro de `JobStatus` dados do `statusCode` objeto.
1. Atribua o valor do identificador de invocação ao `LabelJobID.Text` campo.
1. Atribua o valor de status ao `LabelStatus.Text` campo.

### Start rápido: Invocar um processo de longa duração usando a API de serviço da Web {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

O exemplo de código C# a seguir chama o `FirstAppSolution/PreLoanProcess`processo.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>Os valores localizados no método definido pelo usuário getJobDescription correspondem aos valores retornados pelo serviço Gerenciador de Jobs.

### Executar o aplicativo ASP.NET {#run-the-asp-net-application}

Depois de compilar e implantar seu aplicativo ASP.NET, você pode executá-lo usando um navegador da Web. Supondo que o nome do projeto ASP.NET seja *InvokePreLoanProcess*, especifique o seguinte URL em um navegador da Web:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

em que localhost é o nome do servidor da Web que hospeda o projeto ASP.NET e 1629 é o número da porta. Quando você compila e cria seu aplicativo ASP.NET, o Microsoft Visual Studio o implanta automaticamente.

>[!NOTE]
>
>Para confirmar que o aplicativo ASP.NET invocou o processo, o start Workspace e aceitou o empréstimo.

## Criação de um aplicativo cliente criado com o Flex que invoca um processo de longa duração centrado no ser humano {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Você pode criar um aplicativo cliente criado com o Flex para chamar o processo *FirstAppSolution/PreLoanProcess* . Este aplicativo usa Remoting para chamar o processo *FirstAppSolution/PreLoanProcess* . (Consulte [Invocar AEM Forms usando (Obsoleto para formulários AEM) AEM Forms Remota](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

A ilustração a seguir mostra um aplicativo cliente criado com Flex coletando dados de um usuário final. Os dados são colocados em uma fonte de dados XML e enviados para o processo.

Observe que depois que o processo é chamado, um valor identificador de invocação é exibido. Um valor identificador de invocação é criado como parte de um registro que acompanha o status do processo de longa duração.

O aplicativo cliente criado com o Flex executa as seguintes tarefas:

* Recupera os valores inseridos pelo usuário na página da Web.
* Cria dinamicamente uma fonte de dados XML transmitida para o processo *FirstAppSolution/PreLoanProcess* . Os três valores são especificados na fonte de dados XML.
* Chama o processo *FirstAppSolution/PreLoanProcess* usando Remoting.
* Retorna o valor do identificador de invocação do processo de longa duração.

### Resumo das etapas {#summary_of_steps-2}

Para criar um aplicativo cliente criado com o Flex que possa invocar o processo FirstAppSolution/PreLoanProcess, execute as seguintes etapas:

1. Start um novo projeto Flex.
1. Inclua o arquivo adobe-remoting-provider.swc no caminho de classe do seu projeto. (Consulte [Inclusão do arquivo](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)da biblioteca do Flex do AEM Forms.)
1. Crie uma `mx:RemoteObject` instância por meio do ActionScript ou MXML. (Consulte [Criação de uma instância](/help/forms/developing/invoking-aem-forms-using-remoting.md)mx:RemoteObject)
1. Configure uma `ChannelSet` instância para se comunicar com AEM Forms e associe-a à `mx:RemoteObject` instância. (Consulte [Criar um Canal para AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. Chame o `login` método do ChannelSet ou o `setCredentials` método do serviço para especificar o valor e a senha do identificador do usuário. (Consulte [Uso de logon único](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Crie a fonte de dados XML para passar para o `FirstAppSolution/PreLoanProcess` processo criando uma instância XML. (Essa lógica do aplicativo é mostrada no exemplo de código a seguir.)
1. Crie um objeto do tipo Objeto usando seu construtor. Atribua o XML ao objeto especificando o nome do parâmetro de entrada do processo, conforme mostrado no seguinte código:

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. Chame o `FirstAppSolution/PreLoanProcess` processo chamando o `mx:RemoteObject` método da instância `invoke_Async` . Passe o `Object` que contém o parâmetro de entrada. (Consulte [Transmissão de valores](/help/forms/developing/invoking-aem-forms-using-remoting.md)de entrada.)
1. Recupere o valor de identificação de invocação retornado de um processo de longa duração, como mostrado no seguinte código:

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Invocar um processo de longa duração usando Remota {#invoking-a-long-lived-process-using-remoting}

O exemplo de código Flex a seguir chama o `FirstAppSolution/PreLoanProcess` processo.

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```

