---
title: Invocar o AEM Forms usando a JavaAPI
seo-title: Invocar o AEM Forms usando a JavaAPI
description: 'null'
seo-description: nulo
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '5410'
ht-degree: 0%

---


# Invocar o AEM Forms usando a API Java {#invoking-aem-forms-using-the-javaapi}

A AEM Forms pode ser invocada usando a AEM Forms Java API. Ao usar a API Java da AEM Forms, você pode usar a API de chamada ou as bibliotecas do cliente Java. As bibliotecas do cliente Java estão disponíveis para serviços como o serviço Rights Management. Essas APIs altamente digitadas permitem desenvolver aplicativos Java que chamam a AEM Forms.

A API de chamada são classes localizadas no pacote `com.adobe.idp.dsc`. Usando essas classes, você pode enviar uma solicitação de invocação diretamente para um serviço e manipular uma resposta de invocação que é retornada. Use a API de invocação para chamar processos de duração curta ou longa que foram criados usando o Workbench.

A maneira recomendada para chamar programaticamente um serviço é usar uma biblioteca de cliente Java que corresponda ao serviço, em vez da API de chamada. Por exemplo, para chamar o serviço de criptografia, use a biblioteca do cliente do serviço de criptografia. Para executar uma operação do serviço de criptografia, chame um método que pertence ao objeto do cliente do serviço de criptografia. Você pode criptografar um documento PDF com uma senha, invocando o método `EncryptionServiceClient` do objeto `encryptPDFUsingPassword`.

A API Java suporta os seguintes recursos:

* Protocolo de transporte RMI para invocação remota
* Transporte de VM para invocação local
* SOAP para invocação remota
* Autenticação diferente, como nome de usuário e senha
* Solicitações de invocação síncronas e assíncronas

**Site do desenvolvedor do Adobe**

O site do desenvolvedor do Adobe contém os seguintes artigos que discutem como chamar os serviços da AEM Forms usando a API do Java:

[Uso de servlets Java para chamar processos da AEM Forms](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Invocar a API do AEM Forms Distiller do Java](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](#including-aem-forms-java-library-files)

[Invocando processos de vida longa centrados em humanos](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Invocar o AEM Forms usando os Serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Configuração das propriedades de conexão](#setting-connection-properties)

[Transmissão de dados para serviços da AEM Forms usando a API Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocar um processo de duração curta usando a API de chamada](#invoking-a-short-lived-process-using-the-invocation-api)

[Criação de um aplicativo da Web Java que chama um processo de vida longa centrado no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md)

## Incluindo arquivos da biblioteca Java AEM Forms {#including-aem-forms-java-library-files}

Para chamar programaticamente um serviço AEM Forms usando a API Java, inclua os arquivos de biblioteca necessários (arquivos JAR) no classpath do seu projeto Java. Os arquivos JAR incluídos no classpath do aplicativo cliente dependem de vários fatores:

* O serviço AEM Forms a ser chamado. Um aplicativo cliente pode chamar um ou mais serviços.
* O modo no qual você deseja chamar um serviço AEM Forms. Você pode usar o modo EJB ou SOAP. (Consulte [Definição das propriedades de ligação](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Somente chave) Start o servidor AEM Forms com o comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar um IP de servidor para EJB

* O servidor de aplicativos J2EE no qual o AEM Forms é implantado.

### Arquivos JAR específicos do serviço {#service-specific-jar-files}

A tabela a seguir lista os arquivos JAR necessários para chamar os serviços AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Arquivo</p></th>
   <th><p>Descrição</p></th>
   <th><p>Local</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk//client-libs/&lt;app server=""&gt;</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Application Manager.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Assembler. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necessário para chamar a API de serviço de Backup e Restauração.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de formulários com códigos de barras. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Converter PDF. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Distiller.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necessário para chamar o serviço DocConverter.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Gerenciamento de Documentos.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Criptografia.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Forms.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Integração de dados de formulário.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF 3D.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Jobs. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Saída.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Utilitários PDF ou Utilitários XMP.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de extensões do Acrobat Reader DC.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Repositório.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs\thirdparty</i></p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Necessário para chamar o serviço de Rights Management.</p><p>Se a AEM Forms estiver implantada em JBoss, inclua todos esses arquivos. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p><p>Diretório lib específico do JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de assinatura.</p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Tarefas. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Armazenamento de Confiança. </p></td>
   <td><p>&lt;&gt;diretório<i> de instalação&gt;/sdk/client-libs/common</i></p></td>
  </tr>
 </tbody>
</table>

### Modo de conexão e arquivos JAR do aplicativo J2EE {#connection-mode-and-j2ee-application-jar-files}

A tabela a seguir lista os arquivos JAR que dependem do modo de conexão e do servidor de aplicativos J2EE no qual o AEM Forms está implantado.

<table>
 <thead>
  <tr>
   <th><p>Arquivo</p> </th>
   <th><p>Descrição</p> </th>
   <th><p>Local</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>se o AEM Forms for chamado usando o modo SOAP, inclua esses arquivos JAR.</p> </td>
   <td><p>&lt;&gt;diretório<em> de instalação&gt;/sdk/client-libs/thirdparty</em></p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se a AEM Forms estiver implantada no JBoss Application Server, inclua este arquivo JAR.</p> <p>As classes necessárias não serão encontradas pelo classloader se jEFP-client.jar e os jars referenciados não estiverem co-localizados.</p> </td>
   <td><p>Diretório de biblioteca do cliente JBoss</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não será necessário incluir esse arquivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se a AEM Forms estiver implantada no BEA WebLogic Server®, inclua esse arquivo JAR.</p> </td>
   <td><p>Diretório lib específico do WebLogic</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não será necessário incluir esse arquivo.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>se o AEM Forms estiver implantado no WebSphere Application Server, inclua esses arquivos JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar é necessário para a invocação do serviço da Web).</p> </li>
    </ul> </td>
   <td><p>Diretório lib específico do WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não precisará incluir esses arquivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocando cenários {#invoking-scenarios}

A tabela a seguir especifica a chamada de cenários e lista os arquivos JAR necessários para chamar o AEM Forms com êxito.

<table>
 <thead>
  <tr>
   <th><p>Serviços</p> </th>
   <th><p>Modo de chamada</p> </th>
   <th><p>Servidor de aplicativos J2EE</p> </th>
   <th><p>Arquivos JAR necessários</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Serviço Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Serviço Forms</p> <p>Serviço de extensões da Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Serviço Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Serviço Forms</p> <p>Serviço de extensões da Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Atualização de arquivos JAR {#upgrading-jar-files}

Se você estiver atualizando do LiveCycle para o AEM Forms, é recomendável incluir os arquivos AEM Forms JAR no caminho da classe do seu projeto Java. Por exemplo, se você estiver usando serviços como o Rights Management, você encontrará um problema de compatibilidade se não incluir arquivos AEM Forms JAR no caminho da classe.

Supondo que você esteja atualizando para a AEM Forms. Para usar um aplicativo Java que chama o serviço Rights Management, inclua as versões AEM Forms dos seguintes arquivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

[Transmissão de dados para serviços da AEM Forms usando a API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Definindo propriedades de conexão {#setting-connection-properties}

Você define as propriedades de conexão para chamar o AEM Forms ao usar a API Java. Ao definir as propriedades de conexão, especifique se os serviços devem ser chamados remotamente ou localmente e também especifique o modo de conexão e os valores de autenticação. Os valores de autenticação são necessários se a segurança do serviço estiver ativada. No entanto, se a segurança do serviço estiver desativada, não será necessário especificar valores de autenticação.

O modo de conexão pode ser o modo SOAP ou EJB. O modo EJB usa o protocolo RMI/IIOP e o desempenho do modo EJB é melhor do que o desempenho do modo SOAP. O modo SOAP é usado para eliminar uma dependência do servidor de aplicativos J2EE ou quando um firewall está localizado entre a AEM Forms e o aplicativo cliente. O modo SOAP usa o protocolo https como o transporte subjacente e pode se comunicar entre os limites do firewall. Se nenhuma dependência do servidor de aplicativos J2EE ou um firewall for um problema, é recomendável usar o modo EJB.

Para chamar um serviço AEM Forms com êxito, defina as seguintes propriedades de conexão:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se você estiver usando o modo de conexão EJB, esse valor representa a URL do servidor de aplicativos J2EE no qual o AEM Forms está implantado. Para chamar remotamente o AEM Forms, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms está implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você poderá especificar `localhost`. Dependendo de em qual servidor de aplicativos J2EE o AEM Forms está implantado, especifique um dos seguintes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se você estiver usando o modo de conexão SOAP, esse valor representa o ponto final para o qual uma solicitação de invocação é enviada. Para chamar remotamente o AEM Forms, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms está implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você pode especificar `localhost` (por exemplo, `http://localhost:8080`.)

   * O valor da porta `8080` é aplicável se o aplicativo J2EE for JBoss. Se o servidor de aplicativos J2EE for IBM® WebSphere®, use a porta `9080`. Da mesma forma, se o servidor de aplicativos J2EE for WebLogic, use a porta `7001`. (Esses valores são valores de porta padrão. Se você alterar o valor da porta, use o número da porta aplicável.)

* **DSC_TRANSPORT_PROTOCOL**: Se você estiver usando o modo de conexão EJB, especifique  `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para esse valor. Se você estiver usando o modo de conexão SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Os valores válidos são `JBoss`, `WebSphere`, `WebLogic`.

   * Se você definir essa propriedade de conexão como `WebSphere`, o valor `java.naming.factory.initial` será definido como `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se você definir essa propriedade de conexão como `WebLogic`, o valor `java.naming.factory.initial` será definido como `weblogic.jndi.WLInitialContextFactory`.
   * Da mesma forma, se você definir essa propriedade de conexão como `JBoss`, o valor `java.naming.factory.initial` será definido como `org.jnp.interfaces.NamingContextFactory`.
   * Você pode definir a propriedade `java.naming.factory.initial` como um valor que atenda aos seus requisitos se não quiser usar os valores padrão.

   >[!NOTE]
   >
   >Em vez de usar uma string para definir a propriedade de conexão `DSC_SERVER_TYPE`, você pode usar um membro estático da classe `ServiceClientFactoryProperties`. Os seguintes valores podem ser usados: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE` ou `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica o nome de usuário dos formulários AEM. Para que um usuário chame com êxito um serviço AEM Forms, ele precisa da função Usuário de serviços. Um usuário também pode ter outra função que inclui a permissão Chamada de serviço. Caso contrário, uma exceção será lançada quando eles tentarem invocar um serviço. Se a segurança do serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_CREDENTIAL_PASSWORD:** Especifica o valor da senha correspondente. Se a segurança do serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_REQUEST_TIMEOUT:** O limite de tempo limite de solicitação padrão para a solicitação SOAP é de 1200000 milissegundos (20 minutos). Em algum momento, uma solicitação pode exigir mais tempo para concluir a operação. Por exemplo, uma solicitação SOAP que recupera um grande conjunto de registros pode exigir um limite de tempo limite mais longo. Você pode usar o `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar o limite de tempo limite de chamada de solicitação para as solicitações SOAP.

   **observação**: Somente invocações baseadas em SOAP suportam a propriedade DSC_REQUEST_TIMEOUT.

Para definir as propriedades de conexão, execute as seguintes tarefas:

1. Crie um objeto `java.util.Properties` usando seu construtor.
1. Para definir a propriedade de conexão `DSC_DEFAULT_EJB_ENDPOINT`, chame o método `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`
   * Um valor de string que especifica o URL do servidor de aplicativos J2EE que hospeda o AEM Forms

   >[!NOTE]
   >
   >Se você estiver usando o modo de conexão SOAP, especifique o valor de lista discriminada `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` em vez do valor de lista discriminada `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT`.

1. Para definir a propriedade de conexão `DSC_TRANSPORT_PROTOCOL`, chame o método `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL`
   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`

   >[!NOTE]
   >
   >Se você estiver usando o modo de conexão SOAP, especifique o valor de lista discriminada `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`em vez do valor de lista discriminada `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL`.

1. Para definir a propriedade de conexão `DSC_SERVER_TYPE`, chame o método `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_SERVER_TYPE`
   * Um valor de string que especifica o servidor de aplicativos J2EE que hospeda o AEM Forms (por exemplo, se o AEM Forms estiver implantado em JBoss, especifique `JBoss`).

      1. Para definir a propriedade de conexão `DSC_CREDENTIAL_USERNAME`, chame o método `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:
   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME`
   * Um valor de string que especifica o nome de usuário necessário para chamar o AEM Forms

      1. Para definir a propriedade de conexão `DSC_CREDENTIAL_PASSWORD`, chame o método `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:
   * O valor de lista discriminada `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD`
   * Um valor de string que especifica o valor de senha correspondente



**Configuração do modo de conexão EJB para JBoss**

O exemplo de código Java a seguir define as propriedades de conexão para chamar a AEM Forms implantada em JBoss e usar o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Configuração do modo de conexão EJB para WebLogic**

O exemplo de código Java a seguir define as propriedades de conexão para chamar o AEM Forms implantado no WebLogic e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuração do modo de conexão EJB para WebSphere**

O exemplo de código Java a seguir define as propriedades de conexão para chamar o AEM Forms implantado no WebSphere e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuração do modo de conexão SOAP**

O exemplo de código Java a seguir define as propriedades de conexão no modo SOAP para chamar a AEM Forms implantada em JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Se você selecionar o modo de conexão SOAP, certifique-se de incluir arquivos JAR adicionais no caminho de classe do aplicativo cliente.

**A definir propriedades de ligação quando a segurança do serviço estiver desativada**

O exemplo de código Java a seguir define as propriedades de conexão necessárias para chamar a AEM Forms implantada no JBoss Application Server e quando a segurança do serviço está desativada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos os Start rápidos de Java associados à Programação com o AEM Forms mostram as configurações de conexão EJB e SOAP.

**Configuração do modo de conexão SOAP com o limite de tempo limite de solicitação personalizado**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Uso de um objeto de contexto para chamar o AEM Forms**

Você pode usar um objeto `com.adobe.idp.Context` para chamar um serviço AEM Forms com um usuário autenticado (o objeto `com.adobe.idp.Context` representa um usuário autenticado). Ao usar um objeto `com.adobe.idp.Context`, não é necessário definir as propriedades `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD`. Você pode obter um objeto `com.adobe.idp.Context` ao autenticar usuários usando o método `AuthenticationManagerServiceClient` do objeto `authenticate`.

O método `authenticate` retorna um objeto `AuthResult` que contém os resultados da autenticação. Você pode criar um objeto `com.adobe.idp.Context` chamando seu construtor. Em seguida, chame o método `com.adobe.idp.Context` do objeto `initPrincipal` e passe o objeto `AuthResult`, conforme mostrado no seguinte código:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Em vez de definir as propriedades `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD`, você pode chamar o método `ServiceClientFactory` do objeto `setContext` e passar pelo objeto `com.adobe.idp.Context`. Ao usar um usuário de formulários AEM para chamar um serviço, verifique se ele tem a função `Services User` necessária para chamar um serviço AEM Forms.

O exemplo de código a seguir mostra como usar um objeto `com.adobe.idp.Context` nas configurações de conexão que são usadas para criar um objeto `EncryptionServiceClient`.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Para obter detalhes completos sobre a autenticação de um usuário, consulte [Autenticando usuários](/help/forms/developing/users.md#authenticating-users).

### Invocando cenários {#invoking_scenarios-1}

Os seguintes cenários de invocação são discutidos nesta seção:

* Um aplicativo cliente em execução em sua própria máquina virtual Java (JVM) chama uma instância independente do AEM Forms.
* Um aplicativo cliente em execução em seu próprio JVM chama instâncias do AEM Forms agrupadas.

### O aplicativo cliente que chama uma instância AEM Forms independente {#client-application-invoking-a-stand-alone-aem-forms-instance}

O diagrama a seguir mostra um aplicativo cliente em execução em seu próprio JVM e chamando uma instância AEM Forms independente.

Nesse cenário, um aplicativo cliente está sendo executado em seu próprio JVM e chama os serviços da AEM Forms.

>[!NOTE]
>
>Esse cenário é o cenário de invocação em que todos os Start Rápidos se baseiam.

### O aplicativo cliente que chama instâncias do AEM Forms em cluster {#client-application-invoking-clustered-aem-forms-instances}

O diagrama a seguir mostra um aplicativo cliente em execução em seu próprio JVM e chamando instâncias do AEM Forms localizadas em um cluster.

Esse cenário é semelhante a um aplicativo cliente que chama uma instância AEM Forms independente. No entanto, o URL do provedor é diferente. Se um aplicativo cliente quiser se conectar a um servidor de aplicativos J2EE específico, o aplicativo deverá alterar o URL para fazer referência ao servidor de aplicativos J2EE específico.

Não é recomendado referenciar um servidor de aplicativos J2EE específico porque a conexão entre o aplicativo cliente e o AEM Forms será encerrada se o servidor de aplicativos parar. Recomenda-se que o URL do provedor faça referência a um gerenciador JNDI no nível da célula, em vez de um servidor de aplicativos J2EE específico.

Os aplicativos clientes que usam o modo de conexão SOAP podem usar a porta do balanceador de carga HTTP para o cluster. Aplicativos cliente que usam o modo de conexão EJB podem se conectar à porta EJB de um servidor de aplicativos J2EE específico. Esta ação trata do Balanceamento de Carga entre nós do cluster.

**WebSphere**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com o AEM Forms implantado no WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com o AEM Forms implantado no WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com o AEM Forms implantado no JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte o administrador para determinar o nome e o número da porta do servidor de aplicativos J2EE.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Transmissão de dados para serviços da AEM Forms usando a API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Transmissão de dados para serviços da AEM Forms usando a API Java {#passing-data-to-aem-forms-services-using-the-java-api}

Geralmente, as operações de serviço AEM Forms consomem ou produzem documentos PDF. Ao chamar um serviço, às vezes é necessário enviar um documento PDF (ou outros tipos de documento, como dados XML) para o serviço. Da mesma forma, às vezes é necessário manipular um documento PDF que é retornado do serviço. A classe Java que permite que você passe dados de e para os serviços AEM Forms é `com.adobe.idp.Document`.

Os serviços AEM Forms não aceitam um documento PDF como outros tipos de dados, como um objeto `java.io.InputStream` ou uma matriz de bytes. Um objeto `com.adobe.idp.Document` também pode ser usado para passar outros tipos de dados, como dados XML, para serviços.

Um objeto `com.adobe.idp.Document` é um tipo serializável Java, portanto, ele pode ser passado por uma chamada RMI. O lado de recebimento pode ser localizado (mesmo host, mesmo carregador de classe), local (mesmo host, carregador de classe diferente) ou remoto (host diferente). A transmissão do conteúdo do documento é otimizada para cada caso. Por exemplo, se o remetente e o destinatário estiverem localizados no mesmo host, o conteúdo será passado por um sistema de arquivos local. (Em alguns casos, documentos podem ser passados na memória.)

Dependendo do tamanho do objeto `com.adobe.idp.Document`, os dados são transportados dentro do objeto `com.adobe.idp.Document` ou armazenados no sistema de arquivos do servidor. Todos os recursos de armazenamento temporários ocupados pelo objeto `com.adobe.idp.Document` são removidos automaticamente após a eliminação `com.adobe.idp.Document`. (Consulte [Eliminando objetos de Documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

Às vezes, é necessário saber o tipo de conteúdo de um objeto `com.adobe.idp.Document` antes de passá-lo para um serviço. Por exemplo, se uma operação exigir um tipo de conteúdo específico, como `application/pdf`, é recomendável determinar o tipo de conteúdo. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

O objeto `com.adobe.idp.Document` tenta determinar o tipo de conteúdo usando os dados fornecidos. Se o tipo de conteúdo não puder ser recuperado dos dados fornecidos (por exemplo, quando os dados forem fornecidos como uma matriz de bytes), defina o tipo de conteúdo. Para definir o tipo de conteúdo, chame o método `com.adobe.idp.Document` do objeto `setContentType`. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se os arquivos de garantia residirem no mesmo sistema de arquivos, a criação de um objeto `com.adobe.idp.Document` será mais rápida. Se os arquivos de garantia residirem em sistemas de arquivos remotos, uma operação de cópia deve ser feita, o que afeta o desempenho.

Um aplicativo pode conter os tipos de dados `com.adobe.idp.Document` e `org.w3c.dom.Document`. No entanto, certifique-se de qualificar totalmente o tipo de dados `org.w3c.dom.Document`. Para obter informações sobre como converter um objeto `org.w3c.dom.Document` em um objeto `com.adobe.idp.Document`, consulte [Start rápido (modo EJB): Pré-preencher o Forms com layouts flutuantes usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Para evitar um vazamento de memória no WebLogic ao usar um objeto `com.adobe.idp.Document`, leia as informações do documento em blocos de 2048 bytes ou menos. Por exemplo, o código a seguir lê as informações do documento em blocos de 2048 bytes:

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Criando documentos {#creating-documents}

Crie um objeto `com.adobe.idp.Document` antes de chamar uma operação de serviço que exija um documento PDF (ou outros tipos de documento) como um valor de entrada. A classe `com.adobe.idp.Document` fornece construtores que permitem criar um documento dos seguintes tipos de conteúdo:

* Uma matriz de bytes
* Um objeto `com.adobe.idp.Document` existente
* Um objeto `java.io.File`
* Um objeto `java.io.InputStream`
* Um objeto `java.net.URL`

#### Criação de um documento com base em uma matriz de bytes {#creating-a-document-based-on-a-byte-array}

O exemplo de código a seguir cria um objeto `com.adobe.idp.Document` que é baseado em uma matriz de bytes.

**Criação de um objeto de Documento baseado em uma matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Criação de um documento com base em outro documento {#creating-a-document-based-on-another-document}

O exemplo de código a seguir cria um objeto `com.adobe.idp.Document` que é baseado em outro objeto `com.adobe.idp.Document`.

**Criação de um objeto de Documento com base em outro documento**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Criação de um documento com base em um arquivo {#creating-a-document-based-on-a-file}

O exemplo de código a seguir cria um objeto `com.adobe.idp.Document` que se baseia em um arquivo PDF chamado *map.pdf*. Esse arquivo está localizado na raiz do disco rígido C. Este construtor tenta definir o tipo de conteúdo MIME do objeto `com.adobe.idp.Document` usando a extensão de nome de arquivo.

O construtor `com.adobe.idp.Document` que aceita um objeto `java.io.File` também aceita um parâmetro Booliano. Ao definir esse parâmetro como `true`, o objeto `com.adobe.idp.Document` exclui o arquivo. Essa ação significa que você não precisa remover o arquivo depois de passá-lo para o construtor `com.adobe.idp.Document`.

Definir esse parâmetro como `false` significa que você mantém a propriedade desse arquivo. A configuração desse parâmetro para `true` é mais eficiente. O motivo é que o objeto `com.adobe.idp.Document` pode mover o arquivo diretamente para a área gerenciada local em vez de copiá-lo (que é mais lento).

**Criação de um objeto de Documento com base em um arquivo PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Criação de um documento com base em um objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

O exemplo de código Java a seguir cria um objeto `com.adobe.idp.Document` baseado em um objeto `java.io.InputStream`.

**Criação de um documento com base em um objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Criação de um documento com base em conteúdo acessível em um URL {#creating-a-document-based-on-content-accessible-from-an-url}

O exemplo de código Java a seguir cria um objeto `com.adobe.idp.Document` que se baseia em um arquivo PDF chamado *map.pdf*. Este arquivo está localizado em um aplicativo da Web chamado `WebApp` que está sendo executado em `localhost`. Este construtor tenta definir o tipo de conteúdo MIME do objeto `com.adobe.idp.Document` usando o tipo de conteúdo retornado com o protocolo URL.

O URL fornecido ao objeto `com.adobe.idp.Document` é sempre lido no lado em que o objeto `com.adobe.idp.Document` original é criado, como mostra este exemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

O arquivo c:/temp/input.pdf deve estar localizado no computador cliente (não no computador servidor). O computador cliente é onde o URL é lido e onde o objeto `com.adobe.idp.Document` foi criado.

**Criação de um documento com base em conteúdo acessível de um URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Tratamento de documentos retornados {#handling-returned-documents}

As operações de serviço que retornam um documento PDF (ou outros tipos de dados, como dados XML) como um valor de saída retornam um objeto `com.adobe.idp.Document`. Depois de receber um objeto `com.adobe.idp.Document`, é possível convertê-lo nos seguintes formatos:

* Um objeto `java.io.File`
* Um objeto `java.io.InputStream`
* Uma matriz de bytes

A linha de código a seguir converte um objeto `com.adobe.idp.Document` em um objeto `java.io.InputStream`. Suponha que `myPDFDocument` represente um objeto `com.adobe.idp.Document`:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Da mesma forma, você pode copiar o conteúdo de um `com.adobe.idp.Document` para um arquivo local executando as seguintes tarefas:

1. Crie um objeto `java.io.File`.
1. Chame o método `com.adobe.idp.Document` do objeto `copyToFile` e passe o objeto `java.io.File`.

O exemplo de código a seguir copia o conteúdo de um objeto `com.adobe.idp.Document` para um arquivo chamado *AnotherMap.pdf*.

**Copiando o conteúdo de um objeto de documento para um arquivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar o tipo de conteúdo de um documento {#determining-the-content-type-of-a-document}

Determine o tipo MIME de um objeto `com.adobe.idp.Document` invocando o método `com.adobe.idp.Document` do objeto `getContentType`. Esse método retorna um valor de string que especifica o tipo de conteúdo do objeto `com.adobe.idp.Document`. A tabela a seguir descreve os diferentes tipos de conteúdo retornados pelo AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Tipo MIME</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>DOCUMENTO PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XDP (XML Data Packaging), que é usado para formulários XML Forms Architecture (XFA) exportados</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, anexos ou outros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Forms Data Format (FDF), que é usado para formulários Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), que é usado para formulários Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Formato de dados avançado e XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Formato de dados genérico</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Tipo MIME não especificado</p></td>
  </tr>
 </tbody>
</table>

O exemplo de código a seguir determina o tipo de conteúdo de um objeto `com.adobe.idp.Document`.

**Como determinar o tipo de conteúdo de um objeto de Documento**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Descartando objetos de Documento {#disposing-document-objects}

Quando não precisar mais de um objeto `Document`, é recomendável que você o descarte invocando seu método `dispose`. Cada objeto `Document` consome um descritor de arquivo e até 75 MB de espaço de RAM na plataforma host do seu aplicativo. Se um objeto `Document` não for descartado, o processo de coleta do Java Garage o eliminará. No entanto, ao descartá-la mais cedo usando o método `dispose`, você pode liberar a memória ocupada pelo objeto `Document`.

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocar um serviço usando uma biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

As operações de serviço da AEM Forms podem ser chamadas usando uma API altamente digitada de um serviço, conhecida como uma biblioteca de cliente Java. Uma *biblioteca cliente Java* é um conjunto de classes concretas que fornecem acesso aos serviços implantados no container de serviço. Instancie um objeto Java que representa o serviço a ser chamado em vez de criar um objeto `InvocationRequest` usando a API de chamada. A API de invocação é usada para invocar processos, como processos de longa duração, criados no Workbench. (Consulte [Invocando processos de longa vida centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para executar uma operação de serviço, chame um método que pertence ao objeto Java. Uma biblioteca de cliente Java contém métodos que geralmente mapeiam um para um com operações de serviço. Ao usar uma biblioteca de cliente Java, defina as propriedades de conexão necessárias. (Consulte [Definição das propriedades de ligação](invoking-aem-forms-using-java.md#setting-connection-properties).)

Depois de definir as propriedades de conexão, crie um objeto `ServiceClientFactory` que seja usado para instanciar um objeto Java que permita chamar um serviço. Cada serviço que tem uma biblioteca de cliente Java tem um objeto de cliente correspondente. Por exemplo, para chamar o serviço Repositório, crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`. O objeto `ServiceClientFactory` é responsável por manter as configurações de conexão necessárias para chamar os serviços AEM Forms.

Embora a obtenção de um `ServiceClientFactory` seja geralmente rápida, algumas despesas gerais são envolvidas quando a fábrica é usada pela primeira vez. Esse objeto é otimizado para reutilização e, portanto, quando possível, use o mesmo objeto `ServiceClientFactory` ao criar vários objetos de cliente Java. Ou seja, não crie um objeto `ServiceClientFactory` separado para cada objeto de biblioteca de cliente que você criar.

Há uma configuração do Gerenciador de usuários que controla a duração da asserção SAML dentro do objeto `com.adobe.idp.Context` que afeta o objeto `ServiceClientFactory`. Essa configuração controla todas as vidas do contexto de autenticação em todo o AEM Forms, incluindo todas as invocações executadas usando a API Java. Por padrão, o período em que um objeto `ServiceCleintFactory` pode ser usado é de duas horas.

>[!NOTE]
>
>Para explicar como chamar um serviço usando a API Java, a operação `writeResource` do serviço do Repositório é chamada. Esta operação coloca um novo recurso no repositório.

Você pode chamar o serviço Repositório usando uma biblioteca de cliente Java e executando as seguintes etapas:

1. Inclua arquivos JAR do cliente, como o adobe-repository-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Defina as propriedades de conexão necessárias para chamar um serviço.
1. Crie um objeto `ServiceClientFactory` invocando o método estático `ServiceClientFactory` do objeto `createInstance` e transmitindo o objeto `java.util.Properties` que contém propriedades de conexão.
1. Crie um objeto `ResourceRepositoryClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`. Use o objeto `ResourceRepositoryClient` para chamar operações de serviço do Repositório.
1. Crie um objeto `RepositoryInfomodelFactoryBean` usando seu construtor e passe `null`. Esse objeto permite criar um objeto `Resource` que representa o conteúdo adicionado ao repositório.
1. Crie um objeto `Resource` invocando o método `RepositoryInfomodelFactoryBean` do objeto `newImage` e transmitindo os seguintes valores:

   * Um valor de ID exclusivo especificando `new Id()`.
   * Um valor UUID exclusivo especificando `new Lid()`.
   * O nome do recurso. Você pode especificar o nome do arquivo XDP.

   Converta o valor de retorno em `Resource`.

1. Crie um objeto `ResourceContent` invocando o método `RepositoryInfomodelFactoryBean` do objeto `newImage` e atribuindo o valor de retorno a `ResourceContent`. Este objeto representa o conteúdo adicionado ao repositório.
1. Crie um objeto `com.adobe.idp.Document` transmitindo um objeto `java.io.FileInputStream` que armazene o arquivo XDP a ser adicionado ao repositório. (Consulte [Criação de um documento com base em um objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Adicione o conteúdo do objeto `com.adobe.idp.Document` ao objeto `ResourceContent` invocando o método `ResourceContent` do objeto `setDataDocument`. Passe o objeto `com.adobe.idp.Document`.
1. Defina o tipo MIME do arquivo XDP para adicioná-lo ao repositório, chamando o método `ResourceContent` do objeto `setMimeType` e transmitindo `application/vnd.adobe.xdp+xml`.
1. Adicione o conteúdo do objeto `ResourceContent` ao objeto `Resource` invocando o método `Resource` object &#39;s `setContent` e transmitindo o objeto `ResourceContent`.
1. Adicione uma descrição do recurso chamando o método `Resource` object ‘s `setDescription` e transmitindo um valor de string que representa uma descrição do recurso.
1. Adicione o design de formulário ao repositório, chamando o método `ResourceRepositoryClient` do objeto `writeResource` e transmitindo os seguintes valores:

   * Um valor de string que especifica o caminho para a coleção de recursos que contém o novo recurso
   * O objeto `Resource` que foi criado

**Consulte também:**

[Start rápido (modo EJB): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Invocando um processo de duração curta usando a API de chamada {#invoking-a-short-lived-process-using-the-invocation-api}

Você pode chamar um processo de duração curta usando a API de chamada Java. Quando você chama um processo de duração curta usando a API de chamada, passa os valores de parâmetro obrigatórios usando um objeto `java.util.HashMap`. Para que cada parâmetro passe para um serviço, chame o método `java.util.HashMap` do objeto `put` e especifique o par nome-valor que é exigido pelo serviço para executar a operação especificada. Especifique o nome exato dos parâmetros que pertencem ao processo de duração curta.

>[!NOTE]
>
>Para obter informações sobre como invocar um processo de longa duração, consulte [Invocando processos de longa vida centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

A discussão aqui é sobre o uso da API de chamada para chamar o seguinte processo AEM Forms de curta duração chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

### Chame o processo de duração curta MyApplication/EncryptDocument usando a API de invocação Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Chame o processo de curta duração `MyApplication/EncryptDocument` usando a API de invocação do Java:

1. Inclua arquivos JAR do cliente, como o adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. (Consulte [Incluindo arquivos da biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definição das propriedades de ligação](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Crie um objeto `ServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`. Um objeto `ServiceClient` permite que você chame uma operação de serviço. Ele lida com tarefas como localização, despacho e solicitações de invocação de roteamentos.
1. Crie um objeto `java.util.HashMap` usando seu construtor.
1. Chame o método `java.util.HashMap` do objeto `put` para cada parâmetro de entrada para passar ao processo de longa duração. Como o processo de curta duração `MyApplication/EncryptDocument` requer um parâmetro de entrada do tipo `Document`, você só precisa chamar o método `put` uma vez, como mostrado no exemplo a seguir.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Crie um objeto `InvocationRequest` invocando o método `ServiceClientFactory` do objeto `createInvocationRequest` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do processo de longa duração a ser chamado. Para invocar o processo `MyApplication/EncryptDocument`, especifique `MyApplication/EncryptDocument`.
   * Um valor de string que representa o nome da operação do processo. Normalmente, o nome de uma operação de processo de duração curta é `invoke`.
   * O objeto `java.util.HashMap` que contém os valores de parâmetro exigidos pela operação de serviço.
   * Um valor booliano que especifica `true`, que cria uma solicitação síncrona (esse valor é aplicável para chamar um processo de duração curta).

1. Envie a solicitação de invocação para o serviço chamando o método `ServiceClient` do objeto `invoke` e transmitindo o objeto `InvocationRequest`. O método `invoke` retorna um objeto `InvocationReponse`.

   >[!NOTE]
   >
   >Um processo de longa duração pode ser chamado transmitindo o valor `false`como o quarto parâmetro do método `createInvocationRequest`. Passar o valor `false`*cria uma solicitação assíncrona.*

1. Recupere o valor de retorno do processo chamando o método `InvocationReponse` do objeto `getOutputParameter` e transmitindo um valor de string que especifica o nome do parâmetro de saída. Nessa situação, especifique `outDoc` ( `outDoc` é o nome do parâmetro de saída para o processo `MyApplication/EncryptDocument`). Converta o valor de retorno para `Document`, como mostrado no exemplo a seguir.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
1. Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `getOutputParameter`.

**Consulte também:**

[Start rápido: Invocar um processo de duração curta usando a API de chamada](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocando processos de vida longa centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Incluindo arquivos da biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)