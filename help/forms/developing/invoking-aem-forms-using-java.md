---
title: Chamar a AEM Forms usando a JavaAPI
seo-title: Invoking AEM Forms using the JavaAPI
description: Use a API Java do AEM Forms para protocolo de transporte RMI para invocação remota, transporte de VM para invocação local, SOAP para invocação remota, autenticação diferente, como nome de usuário e senha e solicitações de invocação síncrona e assíncrona.
seo-description: Use the AEM Forms Java API for RMI transport protocol for remote invocation, VM transport for local invocation, SOAP for remote invocation, different authentication, such as user name and password, and synchronous and asynchronous invocation requests.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 0%

---

# Chamar o AEM Forms usando a API do Java {#invoking-aem-forms-using-the-javaapi}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O AEM Forms pode ser chamado usando a API do AEM Forms Java. Ao usar a API Java do AEM Forms, você pode usar a API de chamada ou as bibliotecas de clientes Java. As bibliotecas de clientes Java estão disponíveis para serviços como o serviço Rights Management. Essas APIs altamente digitadas permitem desenvolver aplicativos Java que chamam o AEM Forms.

A API de chamada são classes localizadas na variável `com.adobe.idp.dsc` pacote. Usando essas classes, você pode enviar uma solicitação de invocação diretamente a um serviço e manipular uma resposta de invocação que é retornada. Use a API de invocação para invocar processos de duração curta ou longa que foram criados usando o Workbench.

A maneira recomendada de invocar programaticamente um serviço é usar uma biblioteca do cliente Java que corresponda ao serviço, em vez da API de chamada. Por exemplo, para chamar o Serviço de criptografia, use a biblioteca do cliente do Serviço de criptografia. Para executar uma operação do Serviço de criptografia, chame um método que pertence ao objeto do cliente do Serviço de criptografia. Você pode criptografar um documento do PDF com uma senha chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` método .

A API Java é compatível com os seguintes recursos:

* Protocolo de transporte RMI para invocação remota
* Transporte de VM para invocação local
* SOAP para invocação remota
* Autenticação diferente, como nome de usuário e senha
* Solicitações de invocação síncrona e assíncrona

[Inclusão de arquivos da biblioteca Java do AEM Forms](#including-aem-forms-java-library-files)

[Invocando processos de longa vida centrados em seres humanos](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Configuração das propriedades de conexão](#setting-connection-properties)

[Passar dados para serviços da AEM Forms usando a API do Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Chamar um serviço usando uma biblioteca do cliente Java](#invoking-a-service-using-a-java-client-library)

[Chamada de um processo de duração curta usando a API de chamada](#invoking-a-short-lived-process-using-the-invocation-api)

[Criação de uma aplicação Web Java que chama um processo de vida longa centrado em humanos](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusão de arquivos da biblioteca Java do AEM Forms {#including-aem-forms-java-library-files}

Para invocar programaticamente um serviço da AEM Forms usando a API do Java, inclua os arquivos de biblioteca necessários (arquivos JAR) no classpath do seu projeto Java. Os arquivos JAR incluídos no classpath do aplicativo cliente dependem de vários fatores:

* O serviço AEM Forms a ser chamado. Um aplicativo cliente pode invocar um ou mais serviços.
* O modo no qual você deseja chamar um serviço AEM Forms. Você pode usar o modo EJB ou SOAP. (Consulte [Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Somente Turnkey) Inicie o servidor do AEM Forms com o comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar um IP de servidor para EJB

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
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve ser sempre incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Necessário para invocar o serviço Application Manager.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Necessário para invocar o serviço Assembler. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necessário para invocar a API do serviço de Backup e Restauração.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de formulários com códigos de barras. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necessário para invocar o serviço Converter PDF. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Distiller.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necessário para invocar o serviço DocConverter.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necessário para invocar o serviço Gerenciamento de Documentos.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Criptografia.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Forms.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Integração de dados de formulário.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerar PDF 3D.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necessário para invocar o serviço Gerenciador de Jobs. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Saída.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necessário para invocar o serviço Utilitários PDF ou Utilitários XMP.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de extensões do Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Necessário para invocar o Serviço de Repositório.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs\thirdparty</p></td>
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
   <td><p>Necessário para invocar o serviço Rights Management.</p><p>Se o AEM Forms for implantado no JBoss, inclua todos esses arquivos. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p><p>Diretório lib específico do JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de assinatura.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necessário para invocar o serviço Gerenciador de Tarefas. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de Armazenamento de Confiança. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexão e arquivos JAR do aplicativo J2EE {#connection-mode-and-j2ee-application-jar-files}

A tabela a seguir lista os arquivos JAR que são dependentes do modo de conexão e do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

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
   <td><p>&lt;<em>diretório de instalação</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se o AEM Forms for implantado no JBoss Application Server, inclua esse arquivo JAR.</p> <p>As classes necessárias não serão encontradas pelo carregador de classe se jboss-client.jar e os jars referenciados não estiverem co-localizados.</p> </td>
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
   <td><p>Diretório lib específico do WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Se você implantar seu aplicativo cliente no mesmo servidor de aplicativos J2EE, não será necessário incluir esses arquivos.</p> </td>
  </tr>
 </tbody>
</table>

### Invocar cenários {#invoking-scenarios}

A tabela a seguir especifica cenários de chamada e lista os arquivos JAR necessários para chamar o AEM Forms com êxito.

<table>
 <thead>
  <tr>
   <th><p>Serviços</p> </th>
   <th><p>Modo de invocação</p> </th>
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
     <li><p>jai_imagio.jar</p> </li>
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
     <li><p>jai_imagio.jar</p> </li>
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

Se estiver atualizando do LiveCycle para o AEM Forms, é recomendável incluir os arquivos JAR do AEM Forms no caminho de classe do seu projeto Java. Por exemplo, se estiver usando serviços como o Rights Management, você encontrará um problema de compatibilidade se não incluir arquivos AEM Forms JAR no caminho da classe.

Supondo que você esteja atualizando para o AEM Forms. Para usar um aplicativo Java que chame o serviço Rights Management, inclua as versões AEM Forms dos seguintes arquivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

[Passar dados para serviços da AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Chamar um serviço usando uma biblioteca do cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Configuração das propriedades de conexão {#setting-connection-properties}

Você define propriedades de conexão para chamar o AEM Forms ao usar a API do Java. Ao definir propriedades de conexão, especifique se os serviços devem ser chamados remotamente ou localmente e também especifique o modo de conexão e os valores de autenticação. Os valores de autenticação são necessários se a segurança de serviço estiver ativada. No entanto, se a segurança de serviço estiver desativada, não será necessário especificar valores de autenticação.

O modo de conexão pode ser o modo SOAP ou EJB. O modo EJB usa o protocolo RMI/IIOP e o desempenho do modo EJB é melhor do que o desempenho do modo SOAP. O modo SOAP é usado para eliminar uma dependência do servidor de aplicativos J2EE ou quando um firewall está localizado entre o AEM Forms e o aplicativo cliente. O modo SOAP usa o protocolo https como o transporte subjacente e pode se comunicar entre os limites do firewall. Se nenhuma dependência de servidor de aplicativos J2EE ou firewall for um problema, é recomendável usar o modo EJB.

Para chamar um serviço AEM Forms com êxito, defina as seguintes propriedades de conexão:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se estiver usando o modo de conexão EJB, esse valor representa o URL do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para chamar o AEM Forms remotamente, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você poderá especificar `localhost`. Dependendo do servidor de aplicativos J2EE em que o AEM Forms é implantado, especifique um dos seguintes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se estiver usando o modo de conexão SOAP, esse valor representa o ponto de extremidade para o qual uma solicitação de invocação é enviada. Para chamar o AEM Forms remotamente, especifique o nome do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Se o aplicativo cliente estiver localizado no mesmo servidor de aplicativos J2EE, você pode especificar `localhost` (por exemplo, `http://localhost:8080`.)

   * O valor da porta `8080` é aplicável se o aplicativo J2EE for JBoss. Se o servidor de aplicativos J2EE for o IBM® WebSphere®, use a porta `9080`. Da mesma forma, se o servidor de aplicativos J2EE for WebLogic, use a porta `7001`. (Esses valores são valores de porta padrão. Se você alterar o valor da porta, use o número da porta aplicável.)

* **DSC_TRANSPORT_PROTOCOL**: Se estiver usando o modo de conexão EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para esse valor. Se estiver usando o modo de conexão SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Os valores válidos são `JBoss`, `WebSphere`, `WebLogic`.

   * Se você definir essa propriedade de conexão como `WebSphere`, o `java.naming.factory.initial` é definido como `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se você definir essa propriedade de conexão como `WebLogic`, o `java.naming.factory.initial` é definido como `weblogic.jndi.WLInitialContextFactory`.
   * Da mesma forma, se você definir essa propriedade de conexão como `JBoss`, o `java.naming.factory.initial` é definido como `org.jnp.interfaces.NamingContextFactory`.
   * É possível definir a variável `java.naming.factory.initial` para um valor que atenda aos seus requisitos se não quiser usar os valores padrão.

   >[!NOTE]
   >
   >Em vez de usar uma string para definir a variável `DSC_SERVER_TYPE` propriedade de conexão, você pode usar um membro estático do `ServiceClientFactoryProperties` classe . Os seguintes valores podem ser usados: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`ou `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica o nome de usuário dos formulários AEM. Para que um usuário chame um serviço AEM Forms com êxito, ele precisa da função Usuário de serviços . Um usuário também pode ter outra função que inclui a permissão Service Invoke . Caso contrário, uma exceção será lançada quando eles tentarem invocar um serviço. Se a segurança de serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_CREDENTIAL_PASSWORD:** Especifica o valor de senha correspondente. Se a segurança de serviço estiver desativada, não é necessário especificar essa propriedade de conexão.
* **DSC_REQUEST_TIMEOUT:** O limite de tempo limite da solicitação padrão para a solicitação SOAP é de 1200000 milissegundos (20 minutos). Às vezes, uma solicitação pode exigir mais tempo para concluir a operação. Por exemplo, uma solicitação SOAP que recupera um grande conjunto de registros pode exigir um tempo limite mais longo. Você pode usar o `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar o tempo limite da chamada de solicitação para as solicitações SOAP.

   **observação**: Somente invocações baseadas em SOAP suportam a propriedade DSC_REQUEST_TIMEOUT.

Para definir propriedades de conexão, execute as seguintes tarefas:

1. Crie um `java.util.Properties` usando seu construtor.
1. Para definir a variável `DSC_DEFAULT_EJB_ENDPOINT` propriedade de conexão, chame o `java.util.Properties` do objeto `setProperty` e transmita os seguintes valores:

   * O `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeração
   * Um valor da string que especifica o URL do servidor de aplicativos J2EE que hospeda o AEM Forms

   >[!NOTE]
   >
   >Se estiver usando o modo de conexão SOAP, especifique o `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` valor de enumeração em vez de `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeração.

1. Para definir a variável `DSC_TRANSPORT_PROTOCOL` propriedade de conexão, chame o `java.util.Properties` do objeto `setProperty` e transmita os seguintes valores:

   * O `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` valor de enumeração
   * O `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeração

   >[!NOTE]
   >
   >Se estiver usando o modo de conexão SOAP, especifique o `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`valor de enumeração em vez de `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeração.

1. Para definir a variável `DSC_SERVER_TYPE` propriedade de conexão, chame o `java.util.Properties` do objeto `setProperty` e transmita os seguintes valores:

   * O `ServiceClientFactoryProperties.DSC_SERVER_TYPE`valor de enumeração
   * Um valor de string que especifica o servidor de aplicativos J2EE que hospeda o AEM Forms (por exemplo, se o AEM Forms for implantado no JBoss, especifique `JBoss`).

      1. Para definir a variável `DSC_CREDENTIAL_USERNAME` propriedade de conexão, chame o `java.util.Properties` do objeto `setProperty` e transmita os seguintes valores:
   * O `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` valor de enumeração
   * Um valor de string que especifica o nome de usuário necessário para chamar o AEM Forms

      1. Para definir a variável `DSC_CREDENTIAL_PASSWORD` propriedade de conexão, chame o `java.util.Properties` do objeto `setProperty` e transmita os seguintes valores:
   * O `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` valor de enumeração
   * Um valor de string que especifica o valor de senha correspondente



**Definindo o modo de conexão EJB para JBoss**

O exemplo de código Java a seguir define propriedades de conexão para chamar a AEM Forms implantada no JBoss e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Definindo o modo de conexão EJB para WebLogic**

O exemplo de código Java a seguir define propriedades de conexão para chamar o AEM Forms implantado no WebLogic e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Definindo o modo de conexão EJB para WebSphere**

O exemplo de código Java a seguir define propriedades de conexão para chamar o AEM Forms implantado no WebSphere e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Configuração do modo de conexão SOAP**

O exemplo de código Java a seguir define propriedades de conexão no modo SOAP para chamar a AEM Forms implantada no JBoss.

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
>Se você selecionar o modo de conexão SOAP, certifique-se de incluir arquivos JAR adicionais no caminho de classe do seu aplicativo cliente.

**Definir propriedades de ligação quando a segurança de serviço estiver desativada**

O exemplo de código Java a seguir define as propriedades de conexão necessárias para chamar o AEM Forms implantado no JBoss Application Server e quando a segurança de serviço está desativada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos os Java Quick Starts associados à Programação com o AEM Forms mostram as configurações de conexão EJB e SOAP.

**Configuração do modo de conexão SOAP com o limite de tempo limite da solicitação personalizada**

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

Você pode usar um `com.adobe.idp.Context` objeto para chamar um serviço AEM Forms com um usuário autenticado (a variável `com.adobe.idp.Context` representa um usuário autenticado). Ao usar um `com.adobe.idp.Context` não é necessário definir a variável `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` propriedades. Você pode obter um `com.adobe.idp.Context` ao autenticar usuários usando o `AuthenticationManagerServiceClient` do objeto `authenticate` método .

O `authenticate` retorna um método `AuthResult` que contém os resultados da autenticação. Você pode criar um `com.adobe.idp.Context` chamando seu construtor. Em seguida, chame o `com.adobe.idp.Context` do objeto `initPrincipal` e passe o `AuthResult` conforme mostrado no código a seguir:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Em vez de definir a variável `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` , você pode chamar a variável `ServiceClientFactory` do objeto `setContext` e passe o `com.adobe.idp.Context` objeto. Ao usar um usuário de formulários AEM para chamar um serviço, verifique se ele tem a função nomeada `Services User` que é necessário para chamar um serviço AEM Forms.

O exemplo de código a seguir mostra como usar um `com.adobe.idp.Context` nas configurações de conexão usadas para criar um `EncryptionServiceClient` objeto.

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

### Invocar cenários {#invoking_scenarios-1}

Os seguintes cenários de invocação são discutidos nesta seção:

* Um aplicativo cliente em execução em sua própria máquina virtual Java (JVM) chama uma instância autônoma do AEM Forms.
* Um aplicativo cliente em execução em sua própria JVM chama instâncias do AEM Forms em cluster.

### Aplicativo cliente chamando uma instância autônoma do AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

O diagrama a seguir mostra um aplicativo cliente em execução em sua própria JVM e chamando uma instância autônoma do AEM Forms.

Neste cenário, um aplicativo cliente está sendo executado em sua própria JVM e chama os serviços da AEM Forms.

>[!NOTE]
>
>Esse cenário é o cenário de chamada no qual todos os Início rápido são baseados.

### Aplicativo cliente chamando instâncias do AEM Forms em cluster {#client-application-invoking-clustered-aem-forms-instances}

O diagrama a seguir mostra um aplicativo cliente em execução em sua própria JVM e chamando as instâncias do AEM Forms localizadas em um cluster.

Esse cenário é semelhante a um aplicativo cliente que chama uma instância autônoma do AEM Forms. No entanto, o URL do provedor é diferente. Se um aplicativo cliente quiser se conectar a um servidor de aplicativos J2EE específico, o aplicativo deverá alterar o URL para fazer referência ao servidor de aplicativos J2EE específico.

Não é recomendado referenciar um servidor de aplicativos J2EE específico porque a conexão entre o aplicativo cliente e o AEM Forms é encerrada se o servidor de aplicativos parar. Recomenda-se que o URL do provedor faça referência a um gerenciador JNDI em nível de célula, em vez de um servidor de aplicativos J2EE específico.

Os aplicativos clientes que usam o modo de conexão SOAP podem usar a porta do balanceador de carga HTTP para o cluster. As aplicações cliente que usam o modo de conexão EJB podem se conectar à porta EJB de um servidor de aplicativos J2EE específico. Esta ação manipula o Balanceamento de Carga entre nós do cluster.

**WebSphere**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para conexão com o AEM Forms implantado no WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para se conectar ao AEM Forms implantado no WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para se conectar ao AEM Forms implantado no JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte o administrador para determinar o nome e o número da porta do servidor de aplicativos J2EE.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Passar dados para serviços da AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Chamar um serviço usando uma biblioteca do cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Passar dados para serviços da AEM Forms usando a API do Java {#passing-data-to-aem-forms-services-using-the-java-api}

As operações do serviço AEM Forms normalmente consomem ou produzem documentos PDF. Ao invocar um serviço, às vezes é necessário passar um documento PDF (ou outros tipos de documento, como dados XML) para o serviço. Da mesma forma, às vezes, é necessário manipular um documento PDF que é retornado do serviço. A classe Java que permite transmitir dados de e para os serviços da AEM Forms é `com.adobe.idp.Document`.

Os serviços da AEM Forms não aceitam um documento PDF como outros tipos de dados, como um `java.io.InputStream` objeto ou uma matriz de bytes. A `com.adobe.idp.Document` também pode ser usado para transmitir outros tipos de dados, como dados XML, para serviços.

A `com.adobe.idp.Document` é um tipo serializável Java, portanto, pode ser transmitido por uma chamada RMI. O lado de recebimento pode ser alocado (mesmo host, mesmo carregador de classe), local (mesmo host, carregador de classe diferente) ou remoto (host diferente). O envio do conteúdo do documento é otimizado para cada caso. Por exemplo, se o remetente e o destinatário estiverem localizados no mesmo host, o conteúdo será passado por um sistema de arquivos local. (Em alguns casos, os documentos podem ser passados na memória.)

Dependendo do `com.adobe.idp.Document` tamanho do objeto, os dados são transportados dentro da variável `com.adobe.idp.Document` ou armazenado no sistema de arquivos do servidor. Quaisquer recursos de armazenamento temporário ocupados pela `com.adobe.idp.Document` são removidos automaticamente na `com.adobe.idp.Document` eliminação. (Consulte [Eliminando objetos de documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

Às vezes, é necessário saber o tipo de conteúdo de um `com.adobe.idp.Document` antes de poder passá-lo para um serviço. Por exemplo, se uma operação exigir um tipo de conteúdo específico, como `application/pdf`, recomenda-se determinar o tipo de conteúdo. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

O `com.adobe.idp.Document` tenta determinar o tipo de conteúdo usando os dados fornecidos. Se o tipo de conteúdo não puder ser recuperado dos dados fornecidos (por exemplo, quando os dados foram fornecidos como uma matriz de bytes), defina o tipo de conteúdo. Para definir o tipo de conteúdo, chame a função `com.adobe.idp.Document` do objeto `setContentType` método . (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se os arquivos de garantia residirem no mesmo sistema de arquivos, criar um `com.adobe.idp.Document` é mais rápido. Se os arquivos de garantia residirem em sistemas de arquivos remotos, uma operação de cópia deve ser feita, afetando o desempenho.

Um aplicativo pode conter ambos `com.adobe.idp.Document` e `org.w3c.dom.Document` tipos de dados. No entanto, certifique-se de qualificar totalmente a variável `org.w3c.dom.Document` tipo de dados. Para obter informações sobre a conversão de um `org.w3c.dom.Document` para um `com.adobe.idp.Document` objeto, consulte [Início rápido (modo EJB): Pré-preencher o Forms com layouts flutuantes usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Para evitar um vazamento de memória no WebLogic ao usar um `com.adobe.idp.Document` , leia as informações do documento em blocos de 2048 bytes ou menos. Por exemplo, o código a seguir lê as informações do documento em blocos de 2048 bytes:

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

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Criação de documentos {#creating-documents}

Crie um `com.adobe.idp.Document` antes de invocar uma operação de serviço que exija um documento PDF (ou outros tipos de documento) como um valor de entrada. O `com.adobe.idp.Document` A classe fornece construtores que permitem criar um documento a partir dos seguintes tipos de conteúdo:

* Uma matriz de bytes
* Um `com.adobe.idp.Document` objeto
* A `java.io.File` objeto
* A `java.io.InputStream` objeto
* A `java.net.URL` objeto

#### Criar um documento com base em uma matriz de bytes {#creating-a-document-based-on-a-byte-array}

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto baseado em uma matriz de bytes.

**Criação de um objeto de documento baseado em uma matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Criação de um documento com base em outro documento {#creating-a-document-based-on-another-document}

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto que se baseia em outro `com.adobe.idp.Document` objeto.

**Criando um objeto de Documento baseado em outro documento**

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

O exemplo de código a seguir cria um `com.adobe.idp.Document` objeto baseado em um arquivo PDF chamado *map.pdf*. Esse arquivo está localizado na raiz do disco rígido C. Esse construtor tenta definir o tipo de conteúdo MIME da variável `com.adobe.idp.Document` objeto que usa a extensão do nome do arquivo.

O `com.adobe.idp.Document` construtor que aceita um `java.io.File` também aceita um parâmetro booleano. Ao definir esse parâmetro como `true`, o `com.adobe.idp.Document` exclui o arquivo. Essa ação significa que você não precisa remover o arquivo depois de passá-lo para a `com.adobe.idp.Document` construtor.

Configurar este parâmetro como `false` significa que você mantém a propriedade desse arquivo. Configurar este parâmetro como `true` é mais eficiente. O motivo é que a variável `com.adobe.idp.Document` O objeto pode mover o arquivo diretamente para a área gerenciada local, em vez de copiá-lo (o que é mais lento).

**Criação de um objeto de documento baseado em um arquivo PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Criação de um documento com base em um objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto que se baseia em um `java.io.InputStream` objeto.

**Criação de um documento com base em um objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Criar um documento com base em conteúdo acessível de um URL {#creating-a-document-based-on-content-accessible-from-an-url}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto baseado em um arquivo PDF chamado *map.pdf*. Esse arquivo está localizado em um aplicativo da Web chamado `WebApp` que está em execução `localhost`. Esse construtor tenta definir a variável `com.adobe.idp.Document` Tipo de conteúdo MIME do objeto usando o tipo de conteúdo retornado com o protocolo URL.

O URL fornecido para a `com.adobe.idp.Document` O objeto é sempre lido no lado em que o original `com.adobe.idp.Document` é criado, como mostrado neste exemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

O arquivo c:/temp/input.pdf deve estar localizado no computador cliente (não no computador servidor). O computador cliente é onde o URL é lido e onde a variável `com.adobe.idp.Document` foi criado.

**Criar um documento com base em conteúdo acessível de um URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Manuseio de documentos retornados {#handling-returned-documents}

Operações de serviço que retornam um documento PDF (ou outros tipos de dados, como dados XML) como um valor de saída retornam um `com.adobe.idp.Document` objeto. Depois de receber um `com.adobe.idp.Document` , é possível convertê-lo nos seguintes formatos:

* A `java.io.File` objeto
* A `java.io.InputStream` objeto
* Uma matriz de bytes

A linha de código a seguir converte um `com.adobe.idp.Document` para um `java.io.InputStream` objeto. Suponha que `myPDFDocument` representa um `com.adobe.idp.Document` objeto:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Da mesma forma, é possível copiar o conteúdo de um `com.adobe.idp.Document` para um arquivo local, executando as seguintes tarefas:

1. Crie um `java.io.File` objeto.
1. Chame o `com.adobe.idp.Document` do objeto `copyToFile` e passe o `java.io.File`objeto.

O exemplo de código a seguir copia o conteúdo de um `com.adobe.idp.Document` objeto para um arquivo chamado *OtherMap.pdf*.

**Copiando o conteúdo de um objeto de documento em um arquivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar o tipo de conteúdo de um documento {#determining-the-content-type-of-a-document}

Determine o tipo MIME de um `com.adobe.idp.Document` chamando o `com.adobe.idp.Document` do objeto `getContentType` método . Esse método retorna um valor de string que especifica o tipo de conteúdo da variável `com.adobe.idp.Document` objeto. A tabela a seguir descreve os diferentes tipos de conteúdo que o AEM Forms retorna.

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
   <td><p>XDP (Pacote de dados XML), que é usado para formulários XML Forms Architecture (XFA) exportados</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, anexos ou outros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de dados Forms (FDF), usado para formulários Acrobat exportados</p></td>
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

O exemplo de código a seguir determina o tipo de conteúdo de um `com.adobe.idp.Document` objeto.

**Determinar o tipo de conteúdo de um objeto de documento**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Eliminando objetos de documento {#disposing-document-objects}

Quando não precisar mais de uma `Document` , é recomendável que você o descarte invocando seu `dispose` método . Cada `Document` O objeto consome um descritor de arquivo e até 75 MB de espaço RAM na plataforma de host do seu aplicativo. Se uma `Document` não for descartado, o processo de coleta do Java Garage o eliminará. No entanto, eliminando-o mais cedo usando a variável `dispose` você pode liberar a memória ocupada pelo método `Document` objeto.

**Consulte também**

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Chamar um serviço usando uma biblioteca do cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Chamar um serviço usando uma biblioteca do cliente Java {#invoking-a-service-using-a-java-client-library}

As operações do serviço AEM Forms podem ser invocadas usando a API altamente digitada de um serviço, conhecida como uma biblioteca cliente Java. A *Biblioteca do cliente Java* é um conjunto de classes concretas que fornecem acesso a serviços implantados no contêiner de serviço. Instancie um objeto Java que representa o serviço a ser chamado em vez de criar um `InvocationRequest` usando a API de chamada. A API de invocação é usada para invocar processos, como processos de longa duração, criados no Workbench. (Consulte [Invocando processos de longa vida centrados em seres humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para executar uma operação de serviço, chame um método que pertença ao objeto Java. Uma biblioteca do cliente Java contém métodos que normalmente mapeiam um para um com operações de serviço. Ao usar uma biblioteca do cliente Java, defina as propriedades de conexão necessárias. (Consulte [Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)

Depois de definir as propriedades da conexão, crie uma `ServiceClientFactory` objeto usado para instanciar um objeto Java que permite chamar um serviço. Cada serviço que tem uma biblioteca do cliente Java tem um objeto do cliente correspondente. Por exemplo, para invocar o serviço Repositório, crie um `ResourceRepositoryClient` usando seu construtor e passando o `ServiceClientFactory` objeto. O `ServiceClientFactory` é responsável por manter as configurações de conexão necessárias para chamar os serviços da AEM Forms.

Embora a obtenção de um `ServiceClientFactory` geralmente é rápida, alguns custos indiretos são envolvidos quando a fábrica é usada pela primeira vez. Esse objeto é otimizado para reutilização e, portanto, quando possível, usa o mesmo `ServiceClientFactory` quando estiver criando vários objetos de cliente Java. Ou seja, não crie uma `ServiceClientFactory` objeto para cada objeto da biblioteca do cliente que você criar.

Há uma configuração do Gerenciador de usuários que controla o tempo de vida da asserção de SAML que está dentro do `com.adobe.idp.Context` que afeta o `ServiceClientFactory` objeto. Essa configuração controla todos os tempos de vida do contexto de autenticação em todo o AEM Forms, incluindo todas as invocações executadas usando a API do Java. Por padrão, o período em que uma `ServiceCleintFactory` pode ser usado em duas horas.

>[!NOTE]
>
>Para explicar como invocar um serviço usando a API do Java, o `writeResource` é chamada. Essa operação coloca um novo recurso no repositório.

Você pode chamar o serviço Repositório usando uma biblioteca do cliente Java e executando as seguintes etapas:

1. Inclua arquivos JAR do cliente, como adobe-repository-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Defina as propriedades de conexão necessárias para chamar um serviço.
1. Crie um `ServiceClientFactory` chamando o `ServiceClientFactory` estático do objeto `createInstance` e a aprovação do `java.util.Properties` objeto que contém propriedades de conexão.
1. Crie um `ResourceRepositoryClient` usando seu construtor e passando o `ServiceClientFactory` objeto. Use o `ResourceRepositoryClient` objeto para chamar operações do serviço Repositório.
1. Crie um `RepositoryInfomodelFactoryBean` ao usar seu construtor e passar `null`. Esse objeto permite criar um `Resource` que representa o conteúdo adicionado ao repositório.
1. Crie um `Resource` chamando o `RepositoryInfomodelFactoryBean` do objeto `newImage` e transmitindo os seguintes valores:

   * Um valor de ID exclusivo ao especificar `new Id()`.
   * Um valor UUID exclusivo ao especificar `new Lid()`.
   * O nome do recurso. Você pode especificar o nome do arquivo XDP.

   Converta o valor de retorno para `Resource`.

1. Crie um `ResourceContent` chamando o `RepositoryInfomodelFactoryBean` do objeto `newImage` e a conversão do valor de retorno em `ResourceContent`. Esse objeto representa o conteúdo adicionado ao repositório.
1. Crie um `com.adobe.idp.Document` ao passar um `java.io.FileInputStream` que armazena o arquivo XDP a ser adicionado ao repositório. (Consulte [Criação de um documento com base em um objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Adicione o conteúdo da `com.adobe.idp.Document` para `ResourceContent` chamando o `ResourceContent` do objeto `setDataDocument` método . Passe o `com.adobe.idp.Document` objeto.
1. Defina o tipo MIME do arquivo XDP para adicioná-lo ao repositório chamando a função `ResourceContent` do objeto `setMimeType` método e aprovação `application/vnd.adobe.xdp+xml`.
1. Adicione o conteúdo da `ResourceContent` para `Resource` chamando o `Resource` objeto &quot;s `setContent` e a aprovação do `ResourceContent` objeto.
1. Adicione uma descrição do recurso chamando o `Resource` objeto &quot;s `setDescription` e transmitindo um valor de string que represente uma descrição do recurso.
1. Adicione o design de formulário ao repositório, chamando o `ResourceRepositoryClient` do objeto `writeResource` e transmitindo os seguintes valores:

   * Um valor de string que especifica o caminho para a coleção de recursos que contém o novo recurso
   * O `Resource` objeto criado

**Consulte também**

[Início rápido (modo EJB): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Chamar o AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Chamada de um processo de duração curta usando a API de chamada {#invoking-a-short-lived-process-using-the-invocation-api}

Você pode invocar um processo de duração curta usando a API de chamada do Java. Ao invocar um processo de duração curta usando a API de invocação, você passa os valores de parâmetro obrigatórios usando um `java.util.HashMap` objeto. Para cada parâmetro ser enviado a um serviço, chame a função `java.util.HashMap` do objeto `put` e especifique o par nome-valor exigido pelo serviço para executar a operação especificada. Especifique o nome exato dos parâmetros que pertencem ao processo de curta duração.

>[!NOTE]
>
>Para obter informações sobre invocar um processo de longa duração, consulte [Invocando processos de longa vida centrados em seres humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

A discussão aqui é sobre o uso da API de chamada para chamar o seguinte processo de curta duração do AEM Forms chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para seguir junto com o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não seguro passado para o processo. Essa ação se baseia na variável `SetValue` operação. O parâmetro de entrada para esse processo é um `document` variável de processo nomeada `inDoc`.
1. Criptografa o documento PDF com uma senha. Essa ação se baseia na variável `PasswordEncryptPDF` operação. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

### Chame o processo de curta duração MyApplication/EncryptDocument usando a API de invocação Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Chame o `MyApplication/EncryptDocument` processo de duração curta usando a API de invocação do Java:

1. Inclua arquivos JAR do cliente, como o adobe-livecycle-client.jar, no caminho da classe do seu projeto Java. (Consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Crie um `ServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto. A `ServiceClient` permite invocar uma operação de serviço. Ele lida com tarefas como localizar, despachar e rotear solicitações de invocação.
1. Crie um `java.util.HashMap` usando seu construtor.
1. Chame o `java.util.HashMap` do objeto `put` para cada parâmetro de entrada a ser passado para o processo de duração longa. Porque a variável `MyApplication/EncryptDocument` processo de curta duração requer um parâmetro de entrada do tipo `Document`, você só precisará invocar o `put` uma vez, como mostrado no exemplo a seguir.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Crie um `InvocationRequest` chamando o `ServiceClientFactory` do objeto `createInvocationRequest` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do processo de longa duração a ser chamado. Para invocar o `MyApplication/EncryptDocument` processo, especificar `MyApplication/EncryptDocument`.
   * Um valor de string que representa o nome da operação do processo. Normalmente, o nome de uma operação de processo de curta duração é `invoke`.
   * O `java.util.HashMap` objeto que contém os valores de parâmetro necessários para a operação de serviço.
   * Um valor booleano que especifica `true`, que cria uma solicitação síncrona (esse valor é aplicável para invocar um processo de duração curta).

1. Envie a solicitação de invocação para o serviço, chamando o `ServiceClient` do objeto `invoke` e a aprovação do `InvocationRequest` objeto. O `invoke` retorna um método `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Um processo de longa duração pode ser chamado transmitindo o valor `false`como o quarto parâmetro da variável `createInvocationRequest` método . Transmissão do valor `false`*cria uma solicitação assíncrona.*

1. Recupere o valor de retorno do processo, chamando a função `InvocationReponse` do objeto `getOutputParameter` e transmitindo um valor de string que especifica o nome do parâmetro de saída. Nesta situação, especifique `outDoc` ( `outDoc` é o nome do parâmetro de saída para o `MyApplication/EncryptDocument` processo). Converta o valor de retorno para `Document`, como mostrado no exemplo a seguir.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
1. Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getOutputParameter` método .

**Consulte também**

[Início rápido: Chamada de um processo de duração curta usando a API de chamada](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Invocando processos de longa vida centrados em seres humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
