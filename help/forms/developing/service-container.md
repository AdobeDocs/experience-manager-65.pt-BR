---
title: Contêiner de serviço
seo-title: Contêiner de serviço
description: Serviços AEM Forms localizados no contêiner de serviço
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---


# Contêiner de serviço {#service-container}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Os serviços da AEM Forms localizados no contêiner de serviço (incluindo serviços padrão como o serviço de Criptografia, processos de longa duração e de curta duração) podem ser invocados usando vários provedores, como um provedor EJB. Um provedor EJB permite que os serviços da AEM Forms sejam chamados por RMI/IIOP. Um provedor de serviços da Web expõe serviços como serviços da Web (Geração de WSDL) usando padrões como SOAP/HTTP e SOAP/JMS.

A tabela a seguir descreve as diferentes maneiras pelas quais você pode chamar programaticamente os serviços da AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Método de invocação</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integração remota</p></td>
   <td><p>A integração remota fornece a capacidade de os clientes do Flex invocarem operações de serviço. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Invocar o AEM Forms usando (Obsoleto para formulários AEM) AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Uma API Java pode chamar um serviço AEM Forms. A API Java é organizada em bibliotecas do cliente e a API de chamada do Java. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Chamar o AEM Forms usando a API do Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Serviços Web</p></td>
   <td><p>O AEM Forms oferece suporte a padrões de serviço da Web, como SOAP/HTTP. Um serviço pode ser exposto como um serviço da Web, com o WSDL em conformidade com os padrões de serviço da Web definidos pelo W3C.</p><p>Um serviço pode ser chamado de qualquer pilha de serviços da Web, incluindo o SDK do .NET Framework e Sun™ Web Services . (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Chamar o AEM Forms usando serviços da Web</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Solicitações REST</p></td>
   <td><p>O AEM Forms suporta solicitações REST. Um serviço pode ser chamado diretamente de uma página HTML. (Consulte <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Chamar o AEM Forms usando solicitações REST</a>.)</p></td>
  </tr>
 </tbody>
</table>

A ilustração a seguir fornece uma representação visual das diferentes maneiras pelas quais os serviços da AEM Forms podem ser chamados programaticamente.

>[!NOTE]
>
>Além de usar o AEM Forms SDK para criar aplicativos clientes que possam chamar serviços da AEM Forms, você também pode criar componentes que podem ser implantados no contêiner de serviço. Por exemplo, você pode criar um componente Banco que contenha tipos de dados personalizados que podem ser usados em processos. Ou seja, você pode criar um tipo de dados como `com.adobe.idp.BankAccount`. Em seguida, você pode criar instâncias `com.adobe.idp.BankAccount` em seus aplicativos clientes.

O contêiner de serviço fornece a seguinte funcionalidade:

* Permite que os serviços da AEM Forms sejam chamados usando métodos diferentes. Você pode configurar um serviço definindo endpoints para que ele possa ser chamado usando todos os métodos: Remoção, a API do Java, os serviços da Web e o REST. (Consulte [Gerenciando Programaticamente Endpoints](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte uma mensagem em um formato normalizado chamado solicitação de invocação. Uma solicitação de invocação é enviada de um aplicativo cliente (ou outro serviço) para um serviço localizado no contêiner de serviço. Uma solicitação de invocação contém informações como o nome do serviço a ser chamado e valores de dados necessários para executar a operação. Muitos serviços exigem um documento para executar uma operação. Portanto, uma solicitação de invocação geralmente contém um documento, que pode ser dados em PDF, dados XDP, dados XML e assim por diante.
* Envia solicitações de invocação a serviços apropriados (o nome do serviço a ser chamado faz parte da solicitação de invocação).
* Executa tarefas como determinar se o chamador tem permissão para invocar a operação de serviço especificada. A solicitação de invocação deve conter um nome de usuário e senha válidos para formulários AEM.

   Há diferentes maneiras de enviar uma solicitação de invocação para um serviço. Além disso, há diferentes maneiras de enviar os valores de entrada necessários para o serviço. Por exemplo, suponha que você use a API do Java para chamar um serviço que exija um documento PDF. O método Java correspondente contém um parâmetro que aceita um documento PDF. Nessa situação, o tipo de dados do parâmetro é `com.adobe.idp.Document`. (Consulte [Passar dados para serviços da AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

   Se você chamar um serviço usando pastas assistidas, uma solicitação de invocação será enviada quando você colocar um arquivo em uma pasta assistida configurada. Se você chamar um serviço usando email, uma solicitação de invocação será enviada a um serviço quando uma mensagem de email chegar em uma caixa de entrada configurada.

   O contêiner de serviço envia uma resposta de invocação depois que a operação é executada. Uma resposta de invocação contém informações como os resultados da operação. Por exemplo, se a operação modificar um documento PDF, a resposta de invocação conterá o documento PDF modificado. Se a operação não tiver sido bem-sucedida, a resposta de invocação conterá uma mensagem de erro.

   Uma resposta de invocação pode ser recuperada da mesma forma em que uma solicitação de invocação é enviada. Ou seja, se a solicitação de invocação for enviada usando a API Java, uma resposta de invocação poderá ser recuperada usando a API Java. Suponha, por exemplo, que uma operação modifique um documento PDF. Você pode recuperar o documento PDF modificado obtendo o valor de retorno do método Java que invocou o serviço.

   Quando um processo de longa duração é chamado, uma resposta de invocação contém um valor identificador associado à solicitação de invocação. Usando esse valor identificador, você pode verificar o status do processo posteriormente. Por exemplo, considere o serviço MortgaugeLoan de longa duração. Com o valor do identificador , é possível verificar se o processo foi concluído com êxito. (Consulte [Invocando processos de vida longa centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

   O diagrama a seguir mostra um aplicativo cliente (que usa a API do Java) que chama um serviço.

   Quando um aplicativo cliente chama um serviço, três eventos ocorrem:

   1. Um aplicativo cliente envia uma solicitação de invocação para um serviço.
   1. O serviço executa a operação especificada na solicitação de invocação.
   1. O contêiner de serviço retorna uma resposta de invocação para o aplicativo cliente.

**Consulte também:**

[Noções básicas sobre os processos do AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Chamar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Chamar o AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Invocando processos de longa vida centrados em seres humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chamada de AEM Forms usando solicitações REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
