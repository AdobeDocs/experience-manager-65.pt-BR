---
title: Invocar o AEM Forms usando a JavaAPI
seo-title: Invocar o AEM Forms usando a JavaAPI
description: 'null'
seo-description: 'null'
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41

---


# Invocar o AEM Forms usando a API Java {#invoking-aem-forms-using-the-javaapi}

O AEM Forms pode ser chamado usando a AEM Forms Java API. Ao usar a API Java do AEM Forms, você pode usar a API de chamada ou as bibliotecas do cliente Java. As bibliotecas do cliente Java estão disponíveis para serviços como o serviço Rights Management. Essas APIs altamente digitadas permitem desenvolver aplicativos Java que chamam AEM Forms.

A API de chamada são classes localizadas no `com.adobe.idp.dsc` pacote. Usando essas classes, você pode enviar uma solicitação de invocação diretamente para um serviço e manipular uma resposta de invocação que é retornada. Use a API de invocação para chamar processos de duração curta ou longa que foram criados usando o Workbench.

A maneira recomendada para chamar programaticamente um serviço é usar uma biblioteca de cliente Java que corresponda ao serviço, em vez da API de chamada. Por exemplo, para chamar o serviço de criptografia, use a biblioteca do cliente do serviço de criptografia. Para executar uma operação do serviço de criptografia, chame um método que pertence ao objeto do cliente do serviço de criptografia. É possível criptografar um documento PDF com uma senha, invocando o `EncryptionServiceClient` método do `encryptPDFUsingPassword` objeto.

A API Java suporta os seguintes recursos:

* Protocolo de transporte RMI para invocação remota
* Transporte de VM para invocação local
* SOAP para invocação remota
* Autenticação diferente, como nome de usuário e senha
* Solicitações de invocação síncronas e assíncronas

**Site do Adobe Developer**

O site do Adobe Developer contém os seguintes artigos que discutem como chamar os serviços do AEM Forms usando a API Java:

[Usar servlets Java para chamar processos do AEM Forms](https://www.adobe.com/devnet/livecycle/articles/java_servlets.html)

[Invocar a API do AEM Forms Distiller do Java](https://www.adobe.com/devnet/livecycle/articles/distiller_java_03.html)

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](#including-aem-forms-java-library-files)

[Invocando processos de vida longa centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#main-pars-text-0)

[Invocar o AEM Forms usando Serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Configuração das propriedades de conexão](#setting-connection-properties)

[Transmissão de dados para os serviços do AEM Forms usando a API Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](#invoking-a-service-using-a-java-client-library)

[Invocar um processo de duração curta usando a API de chamada](#invoking-a-short-lived-process-using-the-invocation-api)

[Criação de um aplicativo da Web Java que chama um processo de vida longa centrado em humanos](/help/forms/developing/invoking-human-centric-long-lived.md)

## Incluir arquivos da biblioteca Java do AEM Forms {#including-aem-forms-java-library-files}

Para chamar programaticamente um serviço AEM Forms usando a API Java, inclua os arquivos de biblioteca necessários (arquivos JAR) no classpath do seu projeto Java. Os arquivos JAR incluídos no classpath do aplicativo cliente dependem de vários fatores:

* O serviço AEM Forms para chamar. Um aplicativo cliente pode chamar um ou mais serviços.
* O modo no qual você deseja chamar um serviço de Formulários AEM. Você pode usar o modo EJB ou SOAP. (Consulte [Configuração das propriedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)

>[!NOTE]
>
>(Somente chave) Start o servidor AEM Forms com comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar um IP de servidor para EJB

* O servidor de aplicativos J2EE no qual o AEM Forms é implantado.

### Arquivos JAR específicos do serviço {#service-specific-jar-files}

A tabela a seguir lista os arquivos JAR necessários para chamar os serviços do AEM Forms.

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
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk//client-libs/&lt;servidor de aplicativos&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Application Manager.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Assembler. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necessário para chamar a API de serviço de Backup e Restauração.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de formulários com códigos de barras. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Converter PDF. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Distiller.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necessário para chamar o serviço DocConverter.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Gerenciamento de Documentos.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Criptografia.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de Formulários.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Integração de dados de formulário.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF 3D.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Jobs. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Saída.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Utilitários PDF ou Utilitários XMP.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de extensões do Acrobat Reader DC.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Repositório.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs\thirdparty</p></td>
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
   <td><p>Necessário para chamar o serviço Rights Management.</p><p>Se o AEM Forms for implantado em JBoss, inclua todos esses arquivos. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p><p>Diretório lib específico do JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de assinatura.</p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Tarefas. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Armazenamento de Confiança. </p></td>
   <td><p>&lt;diretório<i></i>de instalação&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexão e arquivos JAR do aplicativo J2EE {#connection-mode-and-j2ee-application-jar-files}

A tabela a seguir lista os arquivos JAR que dependem do modo de conexão e do servidor de aplicativos J2EE nos quais o AEM Forms é implantado.

<table>
 <thead>
  <tr>
   <th><p>Arquivo</p> </th>
   <th><p>Descrição</p> </th>
   <th><p>Local</p> </th>
  </tr>
 &lt;/thead alignment="left"&gt;
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
   <td><p>&lt;diretório<em></em>de instalação&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se o AEM Forms for implantado no JBoss Application Server, inclua esse arquivo JAR.</p> <p>As classes necessárias não serão encontradas pelo classloader se jEFP-client.jar e os jars referenciados não estiverem co-localizados.</p> </td>
   <td><p>Diretório de biblioteca do cliente JBoss</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não será necessário incluir esse arquivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se o AEM Forms for implantado no BEA WebLogic Server®, inclua esse arquivo JAR.</p> </td>
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
     <li><p>se o AEM Forms for implantado no WebSphere Application Server, inclua esses arquivos JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar é necessário para a invocação do serviço da Web).</p> </li>
    </ul> </td>
   <td><p>Diretório de biblioteca específico do WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não precisará incluir esses arquivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocação de cenários {#invoking-scenarios}

A tabela a seguir especifica a chamada de cenários e lista os arquivos JAR necessários para chamar com êxito os formulários AEM.

<table>
 <thead>
  <tr>
   <th><p>Serviços</p> </th>
   <th><p>Modo de chamada</p> </th>
   <th><p>Servidor de aplicativos J2EE</p> </th>
   <th><p>Arquivos JAR necessários</p> </th>
  </tr>
 &lt;/thead alignment="left"&gt;
 <tbody>
  <tr>
   <td><p>Serviço de formulários</p> </td>
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
   <td><p>Serviço de formulários</p> <p>Serviço de extensões do Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
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
   <td><p>Serviço de formulários</p> </td>
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
   <td><p>Serviço de formulários</p> <p>Serviço de extensões do Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
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

Se você estiver atualizando do LiveCycle para o AEM Forms, é recomendável incluir os arquivos AEM Forms JAR no caminho de classe do seu projeto Java. Por exemplo, se você estiver usando serviços como o Rights Management, você encontrará um problema de compatibilidade se não incluir arquivos JAR AEM Forms no caminho da classe.

Supondo que você esteja atualizando para o AEM Forms. Para usar um aplicativo Java que chame o serviço Rights Management, inclua as versões do AEM Forms dos seguintes arquivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

[Transmissão de dados para os serviços do AEM Forms usando a API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Configuração das propriedades de conexão {#setting-connection-properties}

Você define as propriedades de conexão para chamar os formulários AEM ao usar a API Java. Ao definir as propriedades de conexão, especifique se os serviços devem ser chamados remotamente ou localmente e também especifique o modo de conexão e os valores de autenticação. Os valores de autenticação são necessários se a segurança do serviço estiver ativada. No entanto, se a segurança do serviço estiver desativada, não será necessário especificar valores de autenticação.

O modo de conexão pode ser o modo SOAP ou EJB. O modo EJB usa o protocolo RMI/IIOP e o desempenho do modo EJB é melhor do que o desempenho do modo SOAP. O modo SOAP é usado para eliminar uma dependência do servidor de aplicativos J2EE ou quando um firewall está localizado entre o AEM Forms e o aplicativo cliente. O modo SOAP usa o protocolo https como o transporte subjacente e pode se comunicar entre os limites do firewall. Se nenhuma dependência do servidor de aplicativos J2EE ou um firewall for um problema, é recomendável usar o modo EJB.

Para chamar com êxito um serviço AEM Forms, defina as seguintes propriedades de conexão:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se você estiver usando o modo de conexão EJB, esse valor representa o URL do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para chamar remotamente o AEM Forms, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você poderá especificar `localhost`. Dependendo de em qual servidor de aplicativos J2EE Forms é implantado, especifique um dos seguintes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se você estiver usando o modo de conexão SOAP, esse valor representa o ponto final para o qual uma solicitação de invocação é enviada. Para chamar remotamente o AEM Forms, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você pode especificar `localhost` (por exemplo, `http://localhost:8080`.)

   * O valor da porta `8080` é aplicável se o aplicativo J2EE for JBoss. Se o servidor de aplicativos J2EE for IBM® WebSphere®, use a porta `9080`. Da mesma forma, se o servidor de aplicativos J2EE for WebLogic, use a porta `7001`. (Esses valores são valores de porta padrão. Se você alterar o valor da porta, use o número da porta aplicável.)

* **DSC_TRANSPORT_PROTOCOL**: Se você estiver usando o modo de conexão EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` esse valor. Se você estiver usando o modo de conexão SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Os valores válidos são `JBoss`, `WebSphere`, `WebLogic`.

   * Se você definir essa propriedade de conexão como `WebSphere`, o `java.naming.factory.initial` valor será definido como `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se você definir essa propriedade de conexão como `WebLogic`, o `java.naming.factory.initial` valor será definido como `weblogic.jndi.WLInitialContextFactory`.
   * Da mesma forma, se você definir essa propriedade de conexão como `JBoss`, o `java.naming.factory.initial` valor será definido como `org.jnp.interfaces.NamingContextFactory`.
   * Você pode definir a `java.naming.factory.initial` propriedade como um valor que atenda aos seus requisitos se não quiser usar os valores padrão.
   ***Observação**: Em vez de usar uma string para definir a propriedade de `DSC_SERVER_TYPE` conexão, você pode usar um membro estático da `ServiceClientFactoryProperties` classe. Os seguintes valores podem ser usados: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`ou `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica o nome de usuário dos formulários AEM. Para que um usuário chame com êxito um serviço AEM Forms, ele precisa da função Usuário de serviços. Um usuário também pode ter outra função que inclui a permissão Chamada de serviço. Caso contrário, uma exceção será lançada quando eles tentarem invocar um serviço. Se a segurança do serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_CREDENTIAL_PASSWORD:** Especifica o valor da senha correspondente. Se a segurança do serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_REQUEST_TIMEOUT:** O limite de tempo limite de solicitação padrão para a solicitação SOAP é de 1200000 milissegundos (20 minutos). Em algum momento, uma solicitação pode exigir mais tempo para concluir a operação. Por exemplo, uma solicitação SOAP que recupera um grande conjunto de registros pode exigir um limite de tempo limite mais longo. Você pode usar o para aumentar o limite de tempo limite de chamada de solicitação para as solicitações SOAP. `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT`

   **observação**: Somente invocações baseadas em SOAP suportam a propriedade DSC_REQUEST_TIMEOUT.

Para definir as propriedades de conexão, execute as seguintes tarefas:

1. Crie um `java.util.Properties` objeto usando seu construtor.
1. Para definir a propriedade de `DSC_DEFAULT_EJB_ENDPOINT` conexão, chame o método do `java.util.Properties` `setProperty` objeto e transmita os seguintes valores:

   * O valor da `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` lista discriminada
   * Um valor de string que especifica o URL do servidor de aplicativos J2EE que hospeda o AEM Forms
   >[!NOTE]
   >
   >Se você estiver usando o modo de conexão SOAP, especifique o valor da `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` lista discriminada em vez do valor da `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` lista discriminada.

1. Para definir a propriedade de `DSC_TRANSPORT_PROTOCOL` conexão, chame o método do `java.util.Properties` `setProperty` objeto e transmita os seguintes valores:

   * O valor da `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` lista discriminada
   * O valor da `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` lista discriminada
   >[!NOTE]
   >
   >Se você estiver usando o modo de conexão SOAP, especifique o valor da `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`lista discriminada em vez do valor da `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` lista discriminada.

1. Para definir a propriedade de `DSC_SERVER_TYPE` conexão, chame o método do `java.util.Properties` `setProperty` objeto e transmita os seguintes valores:

   * O valor da `ServiceClientFactoryProperties.DSC_SERVER_TYPE`lista discriminada
   * Um valor de string que especifica o servidor de aplicativos J2EE que hospeda os formulários AEM (por exemplo, se os formulários AEM estiverem implantados no JBoss, especifique `JBoss`).

      1. Para definir a propriedade de `DSC_CREDENTIAL_USERNAME` conexão, chame o método do `java.util.Properties` `setProperty` objeto e transmita os seguintes valores:
   * O valor da `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` lista discriminada
   * Um valor de string que especifica o nome de usuário necessário para chamar o AEM Forms

      1. Para definir a propriedade de `DSC_CREDENTIAL_PASSWORD` conexão, chame o método do `java.util.Properties` `setProperty` objeto e transmita os seguintes valores:
   * O valor da `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` lista discriminada
   * Um valor de string que especifica o valor de senha correspondente



**Configuração do modo de conexão EJB para JBoss**

O exemplo de código Java a seguir define as propriedades de conexão para chamar os formulários AEM implantados em JBoss e usando o modo de conexão EJB.

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

O exemplo de código Java a seguir define as propriedades de conexão para chamar os formulários AEM implantados no WebLogic e usando o modo de conexão EJB.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuração do modo de conexão EJB para WebSphere**

O exemplo de código Java a seguir define as propriedades de conexão para chamar os formulários AEM implantados no WebSphere e usando o modo de conexão EJB.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuração do modo de conexão SOAP**

O exemplo de código Java a seguir define as propriedades de conexão no modo SOAP para chamar os formulários AEM implantados no JBoss.

```as3
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

O exemplo de código Java a seguir define as propriedades de conexão necessárias para chamar os formulários AEM implantados no JBoss Application Server e quando a segurança do serviço está desativada.

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos os Start rápidos de Java associados à Programação com o AEM Forms mostram as configurações de conexão EJB e SOAP.

**Configuração do modo de conexão SOAP com o limite de tempo limite de solicitação personalizado**

```as3
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Usar um objeto de contexto para chamar os formulários AEM**

Você pode usar um `com.adobe.idp.Context` objeto para chamar um serviço AEM Forms com um usuário autenticado (o `com.adobe.idp.Context` objeto representa um usuário autenticado). Ao usar um `com.adobe.idp.Context` objeto, não é necessário definir as `DSC_CREDENTIAL_USERNAME` propriedades ou `DSC_CREDENTIAL_PASSWORD` . Você pode obter um `com.adobe.idp.Context` objeto ao autenticar usuários usando o `AuthenticationManagerServiceClient` método do `authenticate` objeto.

O `authenticate` método retorna um `AuthResult` objeto que contém os resultados da autenticação. Você pode criar um `com.adobe.idp.Context` objeto chamando seu construtor. Em seguida, chame o `com.adobe.idp.Context` método do `initPrincipal` objeto e passe o `AuthResult` objeto, conforme mostrado no seguinte código:

```as3
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Em vez de definir as propriedades `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` , você pode chamar o método do `ServiceClientFactory` objeto `setContext` e passar pelo `com.adobe.idp.Context` objeto. Ao usar um usuário de formulários AEM para chamar um serviço, verifique se ele tem a função nomeada `Services User` necessária para chamar um serviço de formulários AEM.

O exemplo de código a seguir mostra como usar um `com.adobe.idp.Context` objeto nas configurações de conexão usadas para criar um `EncryptionServiceClient` objeto.

```as3
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
>Para obter detalhes completos sobre como autenticar um usuário, consulte [Autenticando usuários](/help/forms/developing/users.md#authenticating-users).

### Invocação de cenários {#invoking_scenarios-1}

Os seguintes cenários de invocação são discutidos nesta seção:

* Um aplicativo cliente em execução em sua própria máquina virtual Java (JVM) chama uma instância independente do AEM Forms.
* Um aplicativo cliente em execução em sua própria JVM chama instâncias de AEM Forms clusterizadas.

### Aplicativo cliente que chama uma instância independente de AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

O diagrama a seguir mostra um aplicativo cliente executando em sua própria JVM e chamando uma instância independente do AEM Forms.

Nesse cenário, um aplicativo cliente está sendo executado em seu próprio JVM e chama os serviços do AEM Forms.

>[!NOTE]
>
>Esse cenário é o cenário de invocação em que todos os Start Rápidos se baseiam.

### O aplicativo cliente que chama instâncias de AEM Forms em cluster {#client-application-invoking-clustered-aem-forms-instances}

O diagrama a seguir mostra um aplicativo cliente executando em sua própria JVM e chamando instâncias do AEM Forms localizadas em um cluster.

Esse cenário é semelhante a um aplicativo cliente que chama uma instância independente do AEM Forms. No entanto, o URL do provedor é diferente. Se um aplicativo cliente quiser se conectar a um servidor de aplicativos J2EE específico, o aplicativo deverá alterar o URL para fazer referência ao servidor de aplicativos J2EE específico.

Não é recomendado referenciar um servidor de aplicativos J2EE específico porque a conexão entre o aplicativo cliente e o AEM Forms é encerrada se o servidor de aplicativos parar. Recomenda-se que o URL do provedor faça referência a um gerenciador JNDI no nível da célula, em vez de um servidor de aplicativos J2EE específico.

Os aplicativos clientes que usam o modo de conexão SOAP podem usar a porta do balanceador de carga HTTP para o cluster. Aplicativos cliente que usam o modo de conexão EJB podem se conectar à porta EJB de um servidor de aplicativos J2EE específico. Esta ação trata do Balanceamento de Carga entre nós do cluster.

**WebSphere**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com formulários AEM implantados no WebSphere.

```as3
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com formulários AEM implantados no WebLogic.

```as3
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com formulários AEM implantados no JBoss.

```as3
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte o administrador para determinar o nome e o número da porta do servidor de aplicativos J2EE.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Transmissão de dados para os serviços do AEM Forms usando a API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Transmissão de dados para os serviços do AEM Forms usando a API Java {#passing-data-to-aem-forms-services-using-the-java-api}

Geralmente, as operações do serviço AEM Forms consomem ou produzem documentos PDF. Ao chamar um serviço, às vezes é necessário enviar um documento PDF (ou outros tipos de documento, como dados XML) para o serviço. Da mesma forma, às vezes é necessário manipular um documento PDF que é retornado do serviço. A classe Java que permite que você passe dados de e para os serviços do AEM Forms é `com.adobe.idp.Document`.

Os serviços do AEM Forms não aceitam um documento PDF como outros tipos de dados, como um `java.io.InputStream` objeto ou uma matriz de bytes. Um `com.adobe.idp.Document` objeto também pode ser usado para passar outros tipos de dados, como dados XML, para serviços.

Um `com.adobe.idp.Document` objeto é um tipo serializável Java, portanto, ele pode ser passado por uma chamada RMI. O lado de recebimento pode ser localizado (mesmo host, mesmo carregador de classe), local (mesmo host, carregador de classe diferente) ou remoto (host diferente). A transmissão do conteúdo do documento é otimizada para cada caso. Por exemplo, se o remetente e o destinatário estiverem localizados no mesmo host, o conteúdo será passado por um sistema de arquivos local. (Em alguns casos, documentos podem ser passados na memória.)

Dependendo do tamanho do `com.adobe.idp.Document` objeto, os dados são transportados dentro do `com.adobe.idp.Document` objeto ou armazenados no sistema de arquivos do servidor. Quaisquer recursos temporários de armazenamento ocupados pelo `com.adobe.idp.Document` objeto são removidos automaticamente após a `com.adobe.idp.Document` eliminação. (Consulte [Disposição de objetos](invoking-aem-forms-using-java.md#disposing-document-objects)de Documento.)

Às vezes, é necessário saber o tipo de conteúdo de um `com.adobe.idp.Document` objeto antes de passá-lo para um serviço. Por exemplo, se uma operação exigir um tipo de conteúdo específico, como `application/pdf`, é recomendável determinar o tipo de conteúdo. (Consulte [Determinando o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

O `com.adobe.idp.Document` objeto tenta determinar o tipo de conteúdo usando os dados fornecidos. Se o tipo de conteúdo não puder ser recuperado dos dados fornecidos (por exemplo, quando os dados forem fornecidos como uma matriz de bytes), defina o tipo de conteúdo. Para definir o tipo de conteúdo, chame o `com.adobe.idp.Document` método do `setContentType` objeto. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se os arquivos de garantia residirem no mesmo sistema de arquivos, a criação de um `com.adobe.idp.Document` objeto será mais rápida. Se os arquivos de garantia residirem em sistemas de arquivos remotos, uma operação de cópia deve ser feita, o que afeta o desempenho.

Um aplicativo pode conter tipos de dados `com.adobe.idp.Document` e `org.w3c.dom.Document` . No entanto, certifique-se de qualificar totalmente o tipo de `org.w3c.dom.Document` dados. Para obter informações sobre como converter um `org.w3c.dom.Document` objeto em um `com.adobe.idp.Document` objeto, consulte Start [rápido (modo EJB): Pré-preencher formulários com layouts flutuantes usando a API](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)Java.

>[!NOTE]
>
>Para evitar um vazamento de memória no WebLogic ao usar um `com.adobe.idp.Document` objeto, leia as informações do documento em blocos de 2048 bytes ou menos. Por exemplo, o código a seguir lê as informações do documento em blocos de 2048 bytes:

```as3
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

### Criação de documentos {#creating-documents}

Crie um `com.adobe.idp.Document` objeto antes de chamar uma operação de serviço que exija um documento PDF (ou outros tipos de documento) como um valor de entrada. A `com.adobe.idp.Document` classe fornece construtores que permitem criar um documento dos seguintes tipos de conteúdo:

* Uma matriz de bytes
* Um `com.adobe.idp.Document` objeto existente
* Um `java.io.File` objeto
* Um `java.io.InputStream` objeto
* Um `java.net.URL` objeto

#### Criação de um documento com base em uma matriz de bytes {#creating-a-document-based-on-a-byte-array}

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto com base em uma matriz de bytes.

**Criação de um objeto de Documento baseado em uma matriz de bytes**

```as3
 Document myPDFDocument = new Document(myByteArray);
```

#### Criação de um documento com base em outro documento {#creating-a-document-based-on-another-document}

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto que se baseia em outro `com.adobe.idp.Document` objeto.

**Criação de um objeto de Documento com base em outro documento**

```as3
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

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto com base em um arquivo PDF chamado *map.pdf*. Esse arquivo está localizado na raiz do disco rígido C. Esse construtor tenta definir o tipo de conteúdo MIME do `com.adobe.idp.Document` objeto usando a extensão de nome de arquivo.

O `com.adobe.idp.Document` construtor que aceita um `java.io.File` objeto também aceita um parâmetro Booliano. Ao definir esse parâmetro como `true`, o `com.adobe.idp.Document` objeto exclui o arquivo. Essa ação significa que você não precisa remover o arquivo depois de passá-lo para o `com.adobe.idp.Document` construtor.

Configurar esse parâmetro para `false` significa que você mantém a propriedade desse arquivo. A configuração desse parâmetro para `true` é mais eficiente. O motivo é que o `com.adobe.idp.Document` objeto pode mover o arquivo diretamente para a área gerenciada local em vez de copiá-lo (que é mais lento).

**Criação de um objeto de Documento com base em um arquivo PDF**

```as3
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Criação de um documento com base em um objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto que se baseia em um `java.io.InputStream` objeto.

**Criação de um documento com base em um objeto InputStream**

```as3
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Criação de um documento com base em conteúdo acessível de um URL {#creating-a-document-based-on-content-accessible-from-an-url}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto baseado em um arquivo PDF chamado *map.pdf*. Esse arquivo está localizado em um aplicativo da Web chamado `WebApp` que está sendo executado em `localhost`. Esse construtor tenta definir o tipo de conteúdo MIME do `com.adobe.idp.Document` objeto usando o tipo de conteúdo retornado com o protocolo URL.

O URL fornecido ao `com.adobe.idp.Document` objeto é sempre lido no lado em que o `com.adobe.idp.Document` objeto original é criado, como mostra este exemplo:

```as3
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

O arquivo c:/temp/input.pdf deve estar localizado no computador cliente (não no computador servidor). O computador cliente é onde o URL é lido e onde o `com.adobe.idp.Document` objeto foi criado.

**Criação de um documento com base em conteúdo acessível de um URL**

```as3
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Tratamento de documentos devolvidos {#handling-returned-documents}

As operações de serviço que retornam um documento PDF (ou outros tipos de dados, como dados XML) como um valor de saída retornam um `com.adobe.idp.Document` objeto. Depois de receber um `com.adobe.idp.Document` objeto, é possível convertê-lo para os seguintes formatos:

* Um `java.io.File` objeto
* Um `java.io.InputStream` objeto
* Uma matriz de bytes

A linha de código a seguir converte um `com.adobe.idp.Document` objeto em um `java.io.InputStream` objeto. Suponha que isso `myPDFDocument` represente um `com.adobe.idp.Document` objeto:

```as3
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Da mesma forma, é possível copiar o conteúdo de um arquivo `com.adobe.idp.Document` para um arquivo local executando as seguintes tarefas:

1. Create a `java.io.File` object.
1. Chame o `com.adobe.idp.Document` método do objeto `copyToFile` e passe o `java.io.File`objeto.

O exemplo de código a seguir copia o conteúdo de um `com.adobe.idp.Document` objeto para um arquivo chamado *AnotherMap.pdf*.

**Copiando o conteúdo de um objeto de documento para um arquivo**

```as3
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Como determinar o tipo de conteúdo de um documento {#determining-the-content-type-of-a-document}

Determine o tipo MIME de um `com.adobe.idp.Document` objeto chamando o `com.adobe.idp.Document` método do `getContentType` objeto. Esse método retorna um valor de string que especifica o tipo de conteúdo do `com.adobe.idp.Document` objeto. A tabela a seguir descreve os diferentes tipos de conteúdo retornados pelo AEM Forms.

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
   <td><p>documento PDF</p></td>
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
   <td><p>FDF (Forms Data Format), que é usado para formulários exportados do Acrobat</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), que é usado para formulários exportados do Acrobat</p></td>
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

O exemplo de código a seguir determina o tipo de conteúdo de um `com.adobe.idp.Document` objeto.

**Como determinar o tipo de conteúdo de um objeto de Documento**

```as3
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Como descartar objetos de Documento {#disposing-document-objects}

Quando não precisar mais de um `Document` objeto, é recomendável que você o descarte invocando seu `dispose` método. Cada `Document` objeto consome um descritor de arquivo e até 75 MB de espaço de RAM na plataforma de host do seu aplicativo. Se um `Document` objeto não for descartado, o processo de coleta do Java Garage o eliminará. No entanto, ao descartá-la mais cedo usando o `dispose` método, você pode liberar a memória ocupada pelo `Document` objeto.

**Consulte também:**

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Invocar um serviço usando uma biblioteca de cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Invocar um serviço usando uma biblioteca de cliente Java {#invoking-a-service-using-a-java-client-library}

As operações do serviço do AEM Forms podem ser chamadas usando uma API altamente digitada de um serviço, conhecida como uma biblioteca de cliente Java. Uma biblioteca *cliente* Java é um conjunto de classes concretas que fornecem acesso aos serviços implantados no container de serviço. Instancie um objeto Java que representa o serviço a ser chamado em vez de criar um `InvocationRequest` objeto usando a API de chamada. A API de invocação é usada para invocar processos, como processos de longa duração, criados no Workbench. (Consulte [Invocando Processos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)De Vida Longa Centrados Em Pessoas.)

Para executar uma operação de serviço, chame um método que pertence ao objeto Java. Uma biblioteca de cliente Java contém métodos que geralmente mapeiam um para um com operações de serviço. Ao usar uma biblioteca de cliente Java, defina as propriedades de conexão necessárias. (Consulte [Configuração das propriedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)

Depois de definir as propriedades de conexão, crie um `ServiceClientFactory` objeto usado para instanciar um objeto Java que permite chamar um serviço. Cada serviço que tem uma biblioteca de cliente Java tem um objeto de cliente correspondente. Por exemplo, para chamar o serviço Repositório, crie um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto. O `ServiceClientFactory` objeto é responsável por manter as configurações de conexão necessárias para chamar os serviços de formulários AEM.

Embora a obtenção de um produto `ServiceClientFactory` seja geralmente rápida, algumas despesas gerais são afetadas quando a fábrica é utilizada pela primeira vez. Esse objeto é otimizado para reutilização e, portanto, quando possível, use o mesmo `ServiceClientFactory` objeto ao criar vários objetos do cliente Java. Ou seja, não crie um `ServiceClientFactory` objeto separado para cada objeto de biblioteca do cliente que você criar.

Há uma configuração do Gerenciador de usuários que controla a duração da asserção SAML dentro do `com.adobe.idp.Context` objeto que afeta o `ServiceClientFactory` objeto. Essa configuração controla todas as vidas do contexto de autenticação em todo o AEM Forms, incluindo todas as invocações executadas usando a API Java. Por padrão, o período em que um `ServiceCleintFactory` objeto pode ser usado é de duas horas.

>[!NOTE]
>
>Para explicar como chamar um serviço usando a API Java, a operação do serviço Repositório é `writeResource` chamada. Esta operação coloca um novo recurso no repositório.

Você pode chamar o serviço Repositório usando uma biblioteca de cliente Java e executando as seguintes etapas:

1. Inclua arquivos JAR do cliente, como o adobe-repository-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.
1. Defina as propriedades de conexão necessárias para chamar um serviço.
1. Crie um `ServiceClientFactory` objeto chamando o `ServiceClientFactory` método estático do `createInstance` objeto e transmitindo o `java.util.Properties` objeto que contém as propriedades de conexão.
1. Crie um `ResourceRepositoryClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto. Use o `ResourceRepositoryClient` objeto para chamar operações de serviço do Repositório.
1. Crie um `RepositoryInfomodelFactoryBean` objeto usando seu construtor e passe `null`. Esse objeto permite criar um `Resource` objeto que representa o conteúdo adicionado ao repositório.
1. Crie um `Resource` objeto chamando o `RepositoryInfomodelFactoryBean` método do `newImage` objeto e transmitindo os seguintes valores:

   * Um valor de ID exclusivo ao especificar `new Id()`.
   * Um valor UUID exclusivo ao especificar `new Lid()`.
   * O nome do recurso. Você pode especificar o nome do arquivo XDP.
   Converta o valor de retorno em `Resource`.

1. Crie um `ResourceContent` objeto chamando o método do `RepositoryInfomodelFactoryBean` objeto e `newImage` atribuindo o valor de retorno ao `ResourceContent`. Este objeto representa o conteúdo adicionado ao repositório.
1. Crie um `com.adobe.idp.Document` objeto transmitindo um `java.io.FileInputStream` objeto que armazene o arquivo XDP a ser adicionado ao repositório. (Consulte [Criação de um documento com base em um objeto](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object)InputStream.)
1. Adicione o conteúdo do `com.adobe.idp.Document` objeto ao `ResourceContent` objeto, chamando o `ResourceContent` método do `setDataDocument` objeto. Passe o `com.adobe.idp.Document` objeto.
1. Defina o tipo MIME do arquivo XDP a ser adicionado ao repositório, chamando o método do `ResourceContent` objeto `setMimeType` e transmitindo `application/vnd.adobe.xdp+xml`.
1. Adicione o conteúdo do `ResourceContent` objeto ao `Resource` objeto, chamando o método `Resource` &#39;s `setContent` e transmitindo o `ResourceContent` objeto.
1. Adicione uma descrição do recurso chamando o método do `Resource` objeto `setDescription` e transmitindo um valor de string que representa uma descrição do recurso.
1. Adicione o design de formulário ao repositório, chamando o método do `ResourceRepositoryClient` objeto `writeResource` e transmitindo os seguintes valores:

   * Um valor de string que especifica o caminho para a coleção de recursos que contém o novo recurso
   * O `Resource` objeto que foi criado

**Consulte também:**

[Start rápido (modo EJB): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Invocar o AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Invocar um processo de duração curta usando a API de chamada {#invoking-a-short-lived-process-using-the-invocation-api}

Você pode chamar um processo de duração curta usando a API de chamada Java. Ao chamar um processo de duração curta usando a API de chamada, você passa os valores de parâmetro obrigatórios usando um `java.util.HashMap` objeto. Para que cada parâmetro passe para um serviço, chame o método do `java.util.HashMap` objeto `put` e especifique o par nome-valor necessário para o serviço executar a operação especificada. Especifique o nome exato dos parâmetros que pertencem ao processo de duração curta.

>[!NOTE]
>
>Para obter informações sobre como invocar um processo de longa duração, consulte [Invocando processos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)de longa vida centrados em humanos.

A discussão aqui é sobre o uso da API de chamada para chamar o seguinte processo de duração curta do AEM Forms chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Esse processo não se baseia em um processo de formulários AEM existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na `SetValue` operação. O parâmetro de entrada desse processo é uma variável de `document` processo chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na `PasswordEncryptPDF` operação. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

### Chame o processo de duração curta MyApplication/EncryptDocument usando a API de invocação Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Chame o processo de duração `MyApplication/EncryptDocument` curta usando a API de invocação do Java:

1. Inclua arquivos JAR do cliente, como o adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. (Consulte [Inclusão de arquivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.)
1. Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
1. Crie um `ServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto. Um `ServiceClient` objeto permite que você chame uma operação de serviço. Ele lida com tarefas como localização, despacho e solicitações de invocação de roteamentos.
1. Crie um `java.util.HashMap` objeto usando seu construtor.
1. Chame o método `java.util.HashMap` `put` do objeto para cada parâmetro de entrada a ser passado para o processo de longa duração. Como o processo de duração `MyApplication/EncryptDocument` curta requer um parâmetro de entrada do tipo `Document`, você só precisa chamar o `put` método uma vez, como mostrado no exemplo a seguir.

   ```as3
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Crie um `InvocationRequest` objeto chamando o `ServiceClientFactory` método do `createInvocationRequest` objeto e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do processo de longa duração a ser chamado. Para invocar o `MyApplication/EncryptDocument` processo, especifique `MyApplication/EncryptDocument`.
   * Um valor de string que representa o nome da operação do processo. Geralmente, o nome de uma operação de processo com duração curta é `invoke`.
   * O `java.util.HashMap` objeto que contém os valores de parâmetro exigidos pela operação de serviço.
   * Um valor booliano que especifica `true`, o que cria uma solicitação síncrona (esse valor é aplicável para chamar um processo de duração curta).

1. Envie a solicitação de invocação para o serviço chamando o método do `ServiceClient` objeto `invoke` e transmitindo o `InvocationRequest` objeto. O `invoke` método retorna um `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Um processo de longa duração pode ser chamado transmitindo o valor `false`como o quarto parâmetro do `createInvocationRequest` método. Passar o valor `false`*cria uma solicitação assíncrona.*

1. Recupere o valor de retorno do processo chamando o método do `InvocationReponse` objeto `getOutputParameter` e transmitindo um valor de string que especifica o nome do parâmetro de saída. Nessa situação, especifique `outDoc` ( `outDoc` é o nome do parâmetro de saída para o `MyApplication/EncryptDocument` processo). Converta o valor de retorno para `Document`, como mostrado no exemplo a seguir.

   ```as3
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Crie um `java.io.File` objeto e verifique se a extensão do arquivo é .pdf.
1. Chame o método do `com.adobe.idp.Document` objeto para copiar o conteúdo do `copyToFile` `com.adobe.idp.Document` objeto para o arquivo. Certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getOutputParameter` método.

**Consulte também:**

[Start rápido: Invocar um processo de duração curta usando a API de chamada](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocando processos de vida longa centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Incluir arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)