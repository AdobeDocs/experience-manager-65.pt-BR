---
title: Container de serviço
seo-title: Container de serviço
description: 'null'
seo-description: 'null'
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---


# Container de serviço {#service-container}

Os serviços AEM Forms localizados no container de serviço (incluindo serviços padrão, como o serviço de criptografia, processos de longa duração e de curta duração) podem ser chamados usando vários provedores, como um provedor EJB. Um provedor EJB permite que os serviços AEM Forms sejam chamados por RMI/IIOP. Um provedor de serviço da Web expõe serviços como serviços da Web (Geração WSDL) usando padrões como SOAP/HTTP e SOAP/JMS.

A tabela a seguir descreve as diferentes maneiras pelas quais você pode chamar programaticamente os serviços AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Método de chamada</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integração remota</p></td>
   <td><p>A integração remota oferece a capacidade de os clientes Flex chamarem operações de serviço. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Invocar o AEM Forms usando (Obsoleto para formulários AEM) AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Uma API Java pode chamar um serviço AEM Forms. A API Java é organizada nas bibliotecas do cliente e na API de chamada do Java. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Invocando o AEM Forms usando a API</a>Java.)</p></td>
  </tr>
  <tr>
   <td><p>Serviços Web</p></td>
   <td><p>A AEM Forms oferece suporte a padrões de serviço da Web, como SOAP/HTTP. Um serviço pode ser exposto como um serviço da Web, com o WSDL em conformidade com os padrões de serviço da Web definidos pelo W3C.</p><p>Um serviço pode ser chamado a partir de qualquer pilha de serviços da Web, incluindo o .NET Framework e o Sun™ Web Services SDK. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Invocando o AEM Forms usando os Serviços</a>da Web.)</p></td>
  </tr>
  <tr>
   <td><p>Pedidos REST</p></td>
   <td><p>A AEM Forms suporta solicitações REST. Um serviço pode ser chamado diretamente de uma página HTML. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Invocando o AEM Forms usando Solicitações</a>REST.)</p></td>
  </tr>
 </tbody>
</table>

A ilustração a seguir fornece uma representação visual das diferentes maneiras pelas quais os serviços AEM Forms podem ser chamados de forma programática.

>[!NOTE]
>
>Além de usar o AEM Forms SDK para criar aplicativos clientes que possam chamar os serviços da AEM Forms, você também pode criar componentes que podem ser implantados no container de serviço. Por exemplo, você pode criar um componente Banco que contenha tipos de dados personalizados que podem ser usados em processos. Ou seja, você pode criar um tipo de dados como `com.adobe.idp.BankAccount`. Em seguida, é possível criar `com.adobe.idp.BankAccount` instâncias nos aplicativos clientes.

O container de serviço oferece a seguinte funcionalidade:

* Permite que os serviços da AEM Forms sejam chamados usando métodos diferentes. Você pode configurar um serviço definindo pontos de extremidade para que ele possa ser chamado usando todos os métodos: Remoting, a API Java, os serviços da Web e REST. (Consulte Gerenciamento [Programático de Pontos de Extremidade](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte uma mensagem em um formato normalizado chamado solicitação de invocação. Uma solicitação de invocação é enviada de um aplicativo cliente (ou de outro serviço) para um serviço localizado no container de serviço. Uma solicitação de invocação contém informações como o nome do serviço a ser chamado e valores de dados necessários para executar a operação. Muitos serviços exigem um documento para executar uma operação. Portanto, uma solicitação de invocação geralmente contém um documento, que pode ser dados PDF, dados XDP, dados XML e assim por diante.
* Encaminha solicitações de invocação para serviços apropriados (o nome do serviço a ser chamado faz parte da solicitação de invocação).
* Executa tarefas como determinar se o chamador tem permissão para chamar a operação de serviço especificada. A solicitação de invocação deve conter um nome de usuário e senha válidos para formulários AEM.

   Há maneiras diferentes de enviar uma solicitação de invocação para um serviço. Além disso, há diferentes maneiras de enviar os valores de entrada necessários para o serviço. Por exemplo, suponha que você use a API Java para chamar um serviço que exija um documento PDF. O método Java correspondente contém um parâmetro que aceita um documento PDF. Nessa situação, o tipo de dados do parâmetro é `com.adobe.idp.Document`. (Consulte [Transmissão de dados para serviços da AEM Forms usando a API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)Java.)

   Se você chamar um serviço usando pastas monitoradas, uma solicitação de invocação será enviada quando você colocar um arquivo em uma pasta assistida configurada. Se você chamar um serviço usando email, uma solicitação de invocação será enviada para um serviço quando uma mensagem de email chegar em uma caixa de entrada configurada.

   O container de serviço envia uma resposta de invocação assim que a operação é executada. Uma resposta de chamada contém informações como os resultados da operação. Por exemplo, se a operação modificar um documento PDF, a resposta de invocação conterá o documento PDF modificado. Se a operação não foi bem-sucedida, a resposta de invocação contém uma mensagem de erro.

   Uma resposta de invocação pode ser recuperada da mesma forma em que uma solicitação de invocação é enviada. Ou seja, se a solicitação de invocação for enviada usando a API Java, uma resposta de invocação poderá ser recuperada usando a API Java. Considere, por exemplo, que uma operação modifica um documento PDF. Você pode recuperar o documento PDF modificado obtendo o valor de retorno do método Java que invocou o serviço.

   Quando um processo de longa duração é chamado, uma resposta de invocação contém um valor identificador associado à solicitação de invocação. Usando esse valor identificador, você pode verificar o status do processo posteriormente. Por exemplo, considere o serviço de longa duração da MortgageLoan. Usando o valor do identificador, você pode verificar se o processo foi concluído com êxito. (Consulte [Invocando Processos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)De Vida Longa Centrados Em Pessoas.)

   O diagrama a seguir mostra um aplicativo cliente (que usa a API Java) chamando um serviço.

   Quando um aplicativo cliente chama um serviço, três eventos ocorrem:

   1. Um aplicativo cliente envia uma solicitação de invocação para um serviço.
   1. O serviço executa a operação especificada na solicitação de invocação.
   1. O container de serviço retorna uma resposta de invocação para o aplicativo cliente.

**Consulte também:**

[Como entender os processos AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Invocar o AEM Forms usando a API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Invocar o AEM Forms usando os Serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Invocando processos de vida longa centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chamada do AEM Forms usando solicitações REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
