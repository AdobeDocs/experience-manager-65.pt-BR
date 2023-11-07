---
title: Contêiner de serviço
seo-title: Service container
description: Serviços AEM Forms no contêiner de serviço
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Contêiner de serviço {#service-container}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Os serviços AEM Forms no container de serviço (incluindo serviços padrão, como o serviço de criptografia, processos de longa e curta duração) podem ser chamados usando vários provedores, como um provedor EJB. Um provedor EJB permite que os serviços AEM Forms sejam chamados por RMI/IIOP. Um provedor de serviços Web expõe serviços como serviços Web (Geração WSDL) usando padrões como SOAP/HTTP e SOAP/JMS.

A tabela a seguir descreve as diferentes maneiras de chamar programaticamente os serviços da AEM Forms.

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
   <td><p>A integração remota oferece a capacidade de os clientes do Flex chamarem operações de serviço. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Uma API Java pode chamar um serviço AEM Forms. A API Java é organizada em bibliotecas de clientes e na API de chamada Java. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Chamada de AEM Forms usando a API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Serviços da Web</p></td>
   <td><p>O AEM Forms oferece suporte a padrões de serviço da Web, como SOAP/HTTP. Um serviço pode ser exposto como um serviço Web, com o WSDL em conformidade com os padrões de serviço Web definidos pelo W3C.</p><p>Um serviço pode ser chamado de qualquer pilha de serviços da Web, incluindo o .NET Framework e o Sun™ Web Services SDK. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Chamar o AEM Forms usando serviços da Web</a>.)</p></td>
  </tr>
  <tr>
   <td><p>solicitações REST</p></td>
   <td><p>O AEM Forms oferece suporte a solicitações REST. Um serviço pode ser chamado diretamente de uma página de HTML. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Chamar o AEM Forms usando solicitações REST</a>.)</p></td>
  </tr>
 </tbody>
</table>

A ilustração a seguir fornece uma representação visual das diferentes maneiras pelas quais os serviços do AEM Forms podem ser chamados programaticamente.

>[!NOTE]
>
>Além de usar o SDK do AEM Forms para criar aplicativos clientes que podem chamar serviços da AEM Forms, você também pode criar componentes que podem ser implantados no contêiner de serviço. Por exemplo, você pode criar um componente Banco que contenha tipos de dados personalizados que possam ser usados em processos. Ou seja, você pode criar um tipo de dados como `com.adobe.idp.BankAccount`. Em seguida, é possível criar `com.adobe.idp.BankAccount` em seus aplicativos clientes.

O container de serviço fornece a seguinte funcionalidade:

* Permite que os serviços da AEM Forms sejam chamados usando métodos diferentes. Você pode configurar um serviço definindo endpoints para que ele possa ser chamado usando todos os métodos: Remoting, a API do Java, serviços da Web e REST. (Consulte [Gerenciando Endpoints Programaticamente](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte uma mensagem em um formato normalizado chamado solicitação de invocação. Uma solicitação de invocação é enviada de um aplicativo cliente (ou outro serviço) para um serviço no contêiner de serviço. Uma solicitação de chamada contém informações como o nome do serviço a ser chamado e os valores de dados necessários para executar a operação. Muitos serviços exigem um documento para executar uma operação. Portanto, uma solicitação de chamada geralmente contém um documento, que pode ser dados PDF, dados XDP, dados XML e assim por diante.
* Encaminha solicitações de invocação para serviços apropriados (o nome do serviço a ser chamado faz parte da solicitação de invocação).
* Executa tarefas, como determinar se o chamador tem permissão para invocar a operação de serviço especificada. A solicitação de invocação deve conter um nome de usuário e uma senha válidos para formulários AEM.

  Há diferentes maneiras de enviar uma solicitação de invocação para um serviço. Além disso, há diferentes maneiras de enviar valores de entrada necessários para o serviço. Por exemplo, suponha que você use a API Java para chamar um serviço que requer um documento PDF. O método Java correspondente contém um parâmetro que aceita um documento PDF. Nessa situação, o tipo de dados do parâmetro é `com.adobe.idp.Document`. (Consulte [Passagem de dados para serviços da AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

  Se você chamar um serviço usando pastas monitoradas, uma solicitação de invocação será enviada quando você colocar um arquivo em uma pasta monitorada configurada. Se você chamar um serviço usando o email, uma solicitação de invocação será enviada para um serviço quando uma mensagem de email chegar em uma caixa de entrada configurada.

  O contêiner de serviço retorna uma resposta de invocação depois que a operação é executada. Uma resposta de chamada contém informações como os resultados da operação. Por exemplo, se a operação modificar um documento PDF, a resposta de chamada conterá o documento PDF modificado. Se a operação não foi bem-sucedida, a resposta de invocação contém uma mensagem de erro.

  Uma resposta de invocação pode ser recuperada da mesma forma que uma solicitação de invocação é enviada. Ou seja, se a solicitação de chamada for enviada usando a API Java, uma resposta de chamada poderá ser recuperada usando a API Java. Suponha, por exemplo, que uma operação modifique um documento PDF. Você pode recuperar o documento de PDF modificado obtendo o valor de retorno do método Java que chamou o serviço.

  Quando um processo de longa duração é chamado, uma resposta de chamada contém um valor identificador associado à solicitação de chamada. Usando esse valor de identificador, você pode verificar o status do processo posteriormente. Por exemplo, considere o serviço de longa vida do MortgageLoan. Usando o valor do identificador, você pode verificar se o processo foi concluído com êxito. (Consulte [Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  O diagrama a seguir mostra uma aplicação cliente (que usa a API Java) chamando um serviço.

  Quando um aplicativo cliente chama um serviço, ocorrem três eventos:

   1. Um aplicativo cliente envia uma solicitação de invocação a um serviço.
   1. O serviço executa a operação especificada na solicitação de invocação.
   1. O contêiner de serviço retorna uma resposta de invocação ao aplicativo cliente.

**Consulte também**

[Noções básicas sobre processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Chamada de AEM Forms usando a API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chamar o AEM Forms usando solicitações REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
