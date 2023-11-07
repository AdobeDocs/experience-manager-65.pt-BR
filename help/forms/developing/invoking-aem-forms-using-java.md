---
title: Chamar o AEM Forms usando a JavaAPI
description: Use a API Java do AEM Forms para protocolo de transporte RMI para invocação remota, transporte de VM para invocação local, SOAP para invocação remota, autenticação diferente, como nome de usuário e senha, e solicitações de invocação síncrona e assíncrona.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '5393'
ht-degree: 0%

---

# Chamada de AEM Forms usando a API Java {#invoking-aem-forms-using-the-javaapi}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O AEM Forms pode ser chamado usando a API Java do AEM Forms. Ao usar a API Java do AEM Forms, você pode usar a API de chamada ou as bibliotecas de cliente Java. As bibliotecas de cliente Java estão disponíveis para serviços como o serviço Rights Management. Essas APIs altamente tipificadas permitem desenvolver aplicativos Java que chamam o AEM Forms.

A API de Invocação são classes que estão no estado `com.adobe.idp.dsc` pacote. Usando essas classes, você pode enviar uma solicitação de chamada diretamente para um serviço e lidar com uma resposta de chamada retornada. Use a API de Invocação para chamar processos de vida curta ou longa criados com o Workbench.

A maneira recomendada de chamar um serviço programaticamente é usar uma biblioteca de cliente Java que corresponda ao serviço, em vez da API de chamada. Por exemplo, para chamar o Serviço de criptografia, use a biblioteca do cliente do Serviço de criptografia. Para executar uma operação do Serviço de criptografia, chame um método que pertença ao objeto cliente do Serviço de criptografia. Você pode criptografar um documento PDF com uma senha chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` método.

A API Java é compatível com os seguintes recursos:

* Protocolo de transporte RMI para invocação remota
* Transporte de VM para invocação local
* SOAP para invocação remota
* Autenticação diferente, como nome de usuário e senha
* Solicitações de invocação síncrona e assíncrona

[Inclusão de arquivos da biblioteca Java do AEM Forms](#including-aem-forms-java-library-files)

[Chamar processos de longa vida centrados no ser humano](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chamar o AEM Forms usando serviços da Web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Definindo propriedades de conexão](#setting-connection-properties)

[Passagem de dados para serviços da AEM Forms usando a API do Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Chamar um serviço usando uma biblioteca cliente Java](#invoking-a-service-using-a-java-client-library)

[Chamar um processo de vida curta usando a API de chamada](#invoking-a-short-lived-process-using-the-invocation-api)

[Criar uma aplicação Web Java que invoca um processo de longa vida centrado no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusão de arquivos da biblioteca Java do AEM Forms {#including-aem-forms-java-library-files}

Para chamar programaticamente um serviço AEM Forms usando a API Java, inclua os arquivos de biblioteca necessários (arquivos JAR) no classpath do projeto Java. Os arquivos JAR incluídos no classpath do aplicativo cliente dependem de vários fatores:

* O serviço AEM Forms a ser chamado. Um aplicativo cliente pode chamar um ou mais serviços.
* O modo no qual você deseja chamar um serviço AEM Forms. Você pode usar o modo EJB ou SOAP. (Consulte [Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Somente na chave na mão) Inicie o servidor do AEM Forms com o comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` para especificar um IP de servidor para EJB

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
   <td><p>Deve sempre ser incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve sempre ser incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve sempre ser incluído no caminho de classe de um aplicativo cliente Java.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço do Application Manager.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Assembler. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Necessário para invocar a API do serviço de Backup e Restauração.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de formulários com código de barras. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Necessário para invocar o serviço Converter PDF. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Distiller.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Necessário para chamar o serviço DocConverter.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de Gerenciamento de Documentos.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Necessário para chamar o Serviço de criptografia.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obrigatório para chamar o serviço Forms.</p></td>
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
   <td><p>Necessário para invocar o serviço Gerar PDF 3D.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Jobs. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Necessário para chamar o Serviço de saída.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de Utilitários PDF ou Utilitários XMP.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Necessário para chamar o serviço de extensões da Acrobat Reader DC.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obrigatório para chamar o serviço de Repositório.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs\third-party</p></td>
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
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p><p>diretório lib específico de JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de assinatura.</p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Necessário para chamar o serviço Gerenciador de Tarefas. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Necessário para invocar o serviço de Armazenamento de Confiança. </p></td>
   <td><p>&lt;<i>diretório de instalação</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modo de conexão e arquivos JAR da aplicação J2EE {#connection-mode-and-j2ee-application-jar-files}

A tabela a seguir lista os arquivos JAR que dependem do modo de conexão e do servidor da aplicação J2EE no qual o AEM Forms é disponibilizado.

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
   <td><p>se o AEM Forms for implantado no JBoss Application Server, inclua esse arquivo JAR.</p> <p>As classes necessárias não serão encontradas pelo carregador de classes se jboss-client.jar e os jars referenciados não forem co-localizados.</p> </td>
   <td><p>Diretório lib do cliente JBoss</p> <p>Se você implantar a aplicação cliente no mesmo servidor de aplicações J2EE, não será necessário incluir esse arquivo.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se o AEM Forms for implantado no BEA WebLogic Server®, inclua esse arquivo JAR.</p> </td>
   <td><p>Diretório de biblioteca específico do WebLogic</p> <p>Se você implantar a aplicação cliente no mesmo servidor de aplicações J2EE, não será necessário incluir esse arquivo.</p> </td>
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
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar é necessário para a invocação do serviço Web).</p> </li>
    </ul> </td>
   <td><p>Diretório de biblioteca específico do WebSphere (<em>[WAS_HOME]</em>/runtimes)</p> <p>Se você disponibilizar a aplicação cliente no mesmo servidor de aplicações J2EE, não será necessário incluir esses arquivos.</p> </td>
  </tr>
 </tbody>
</table>

### Chamar cenários {#invoking-scenarios}

A tabela a seguir especifica cenários de chamada e lista os arquivos JAR necessários para chamar o AEM Forms com êxito.

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
   <td><p>serviço Forms</p> </td>
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
   <td><p>serviço Forms</p> <p>Serviço de extensões do Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
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
   <td><p>serviço Forms</p> </td>
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
   <td><p>serviço Forms</p> <p>Serviço de extensões do Acrobat Reader DC</p> <p>Serviço de assinatura</p> </td>
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

### Atualizando arquivos JAR {#upgrading-jar-files}

Se você estiver atualizando do LiveCycle para o AEM Forms, é recomendável incluir os arquivos JAR do AEM Forms no caminho de classe do projeto Java. Por exemplo, se estiver usando serviços como o serviço Rights Management, você encontrará um problema de compatibilidade se não incluir arquivos JAR do AEM Forms no caminho da classe.

Supondo que você esteja atualizando para o AEM Forms. Para usar um aplicativo Java que chama o serviço Rights Management, inclua as versões AEM Forms dos seguintes arquivos JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulte também**

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

[Passagem de dados para serviços da AEM Forms usando a API do Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Chamar um serviço usando uma biblioteca cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Definindo propriedades de conexão {#setting-connection-properties}

Você define propriedades de conexão para chamar o AEM Forms ao usar a API Java. Ao definir as propriedades de conexão, especifique se os serviços devem ser chamados remota ou localmente e também especifique o modo de conexão e os valores de autenticação. Os valores de autenticação serão necessários se a segurança do serviço estiver habilitada. No entanto, se a segurança do serviço estiver desativada, não será necessário especificar valores de autenticação.

O modo de conexão pode ser SOAP ou EJB. O modo EJB usa o protocolo RMI/IIOP e o desempenho do modo EJB é melhor do que o desempenho do modo SOAP. O modo SOAP é usado para eliminar uma dependência do servidor de aplicativos J2EE ou quando um firewall está localizado entre o AEM Forms e o aplicativo cliente. O modo SOAP usa o protocolo https como transporte subjacente e pode se comunicar entre limites de firewall. Se nem uma dependência do servidor de aplicações J2EE nem um firewall for um problema, é recomendável usar o modo EJB.

Para chamar um serviço AEM Forms com êxito, defina as seguintes propriedades de conexão:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se você estiver usando o modo de conexão EJB, este valor representa o URL do servidor da aplicação J2EE no qual o AEM Forms é disponibilizado. Para chamar o AEM Forms remotamente, especifique o nome do servidor da aplicação J2EE no qual o AEM Forms está implantado. Se sua aplicação cliente estiver localizada no mesmo servidor de aplicações J2EE, você poderá especificar `localhost`. Dependendo do servidor de aplicações J2EE em que o AEM Forms é disponibilizado, especifique um dos seguintes valores:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se estiver usando o modo de conexão SOAP, esse valor representará o endpoint para onde uma solicitação de chamada é enviada. Para chamar o AEM Forms remotamente, especifique o nome do servidor da aplicação J2EE no qual o AEM Forms está implantado. Se sua aplicação cliente estiver localizada no mesmo servidor de aplicações J2EE, você poderá especificar `localhost` (por exemplo, `http://localhost:8080`.)

   * O valor da porta `8080` é aplicável se a aplicação J2EE for JBoss. Se o servidor de aplicativos J2EE for IBM® WebSphere®, use a porta `9080`. Da mesma forma, se o servidor de aplicativos J2EE for WebLogic, use a porta `7001`. (Esses valores são valores de porta padrão. Se você alterar o valor da porta, use o número da porta aplicável.)

* **DSC_TRANSPORT_PROTOCOL**: Se estiver usando o modo de conexão EJB, especifique `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` para este valor. Se estiver usando o modo de conexão SOAP, especifique `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Especifica o servidor da aplicação J2EE no qual o AEM Forms é disponibilizado. Os valores válidos são `JBoss`, `WebSphere`, `WebLogic`.

   * Se você definir essa propriedade de conexão como `WebSphere`, o `java.naming.factory.initial` o valor está definido como `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se você definir essa propriedade de conexão como `WebLogic`, o `java.naming.factory.initial` o valor está definido como `weblogic.jndi.WLInitialContextFactory`.
   * Da mesma forma, se você definir essa propriedade de conexão como `JBoss`, o `java.naming.factory.initial` o valor está definido como `org.jnp.interfaces.NamingContextFactory`.
   * Você pode definir a variável `java.naming.factory.initial` a um valor que atenda aos requisitos se não quiser usar os valores padrão.

  >[!NOTE]
  >
  >Em vez de usar uma string para definir o `DSC_SERVER_TYPE` propriedade de conexão, você pode usar um membro estático da variável `ServiceClientFactoryProperties` classe. Os seguintes valores podem ser usados: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`ou `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Especifica o nome de usuário dos formulários AEM. Para que um usuário chame um serviço do AEM Forms com êxito, ele precisa da função Usuário de serviços. Um usuário também pode ter outra função que inclua a permissão Chamar serviço. Caso contrário, uma exceção é lançada quando eles tentam chamar um serviço. Se a segurança do serviço estiver desabilitada, não será necessário especificar essa propriedade de conexão.
* **DSC_CREDENTIAL_PASSWORD** Especifica o valor de senha correspondente. Se a segurança do serviço estiver desabilitada, não será necessário especificar essa propriedade de conexão.
* **DSC_REQUEST_TIMEOUT:** O tempo limite de solicitação padrão para a solicitação SOAP é de 1200.000 milissegundos (20 minutos). Às vezes, uma solicitação pode exigir mais tempo para concluir a operação. Por exemplo, uma solicitação SOAP que recupera um grande conjunto de registros pode exigir um tempo limite mais longo. Você pode usar o `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` para aumentar o tempo limite da chamada de solicitação para as solicitações SOAP.

  **observação**: somente invocações baseadas em SOAP oferecem suporte à propriedade DSC_REQUEST_TIMEOUT.

Para definir propriedades de conexão, execute as seguintes tarefas:

1. Criar um `java.util.Properties` usando seu construtor.
1. Para definir a variável `DSC_DEFAULT_EJB_ENDPOINT` propriedade de conexão, chame a variável `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * A variável `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeração
   * Um valor de string que especifica o URL do servidor da aplicação J2EE que hospeda o AEM Forms

   >[!NOTE]
   >
   >Se estiver usando o modo de conexão SOAP, especifique o `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` valor de enumeração em vez de `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valor de enumeração.

1. Para definir a variável `DSC_TRANSPORT_PROTOCOL` propriedade de conexão, chame a variável `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * A variável `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` valor de enumeração
   * A variável `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeração

   >[!NOTE]
   >
   >Se estiver usando o modo de conexão SOAP, especifique o `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`valor de enumeração em vez de `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valor de enumeração.

1. Para definir a variável `DSC_SERVER_TYPE` propriedade de conexão, chame a variável `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * A variável `ServiceClientFactoryProperties.DSC_SERVER_TYPE`valor de enumeração
   * Um valor de string que especifica o servidor da aplicação J2EE que hospeda o AEM Forms (por exemplo, se o AEM Forms for disponibilizado no JBoss, especifique `JBoss`).

      1. Para definir a variável `DSC_CREDENTIAL_USERNAME` propriedade de conexão, chame a variável `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * A variável `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` valor de enumeração
   * Um valor de string que especifica o nome de usuário necessário para chamar o AEM Forms

      1. Para definir a variável `DSC_CREDENTIAL_PASSWORD` propriedade de conexão, chame a variável `java.util.Properties` do objeto `setProperty` e passe os seguintes valores:

   * A variável `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` valor de enumeração
   * Um valor de string que especifica o valor de senha correspondente

**Definindo o modo de conexão EJB para JBoss**

O exemplo de código Java a seguir define propriedades de conexão para chamar o AEM Forms implantado em JBoss e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Definindo o modo de conexão EJB para o WebLogic**

O exemplo de código Java a seguir define propriedades de conexão para chamar o AEM Forms implantado no WebLogic e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Definindo o modo de conexão EJB para o WebSphere**

O exemplo de código Java a seguir define propriedades de conexão para chamar o AEM Forms implantado no WebSphere e usando o modo de conexão EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Definindo o modo de conexão SOAP**

O exemplo de código Java a seguir define propriedades de conexão no modo SOAP para chamar o AEM Forms implantado no JBoss.

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

**Definindo propriedades de conexão quando a segurança do serviço está desabilitada**

O exemplo de código Java a seguir define as propriedades de conexão necessárias para chamar o AEM Forms implantado no JBoss Application Server e quando a segurança do serviço está desativada.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Todos os Quick Starts de Java associados à Programação com o AEM Forms mostram as configurações de conexão EJB e SOAP.

**Definindo o modo de conexão SOAP com tempo limite de solicitação personalizado**

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

Você pode usar um `com.adobe.idp.Context` objeto para chamar um serviço AEM Forms com um usuário autenticado (o `com.adobe.idp.Context` representa um usuário autenticado). Ao usar uma `com.adobe.idp.Context` objeto, não é necessário definir o `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` propriedades. Você pode obter um `com.adobe.idp.Context` ao autenticar usuários usando o `AuthenticationManagerServiceClient` do objeto `authenticate` método.

A variável `authenticate` o método retorna um `AuthResult` objeto que contém os resultados da autenticação. Você pode criar um `com.adobe.idp.Context` invocando seu construtor. Em seguida, chame o `com.adobe.idp.Context` do objeto `initPrincipal` e transmita o `AuthResult` conforme mostrado no código a seguir:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Em vez de definir o `DSC_CREDENTIAL_USERNAME` ou `DSC_CREDENTIAL_PASSWORD` propriedades, você pode chamar a variável `ServiceClientFactory` do objeto `setContext` e transmita o `com.adobe.idp.Context` objeto. Ao usar um usuário de formulários AEM para chamar um serviço, verifique se ele tem a função chamada `Services User` que é necessário para chamar um serviço AEM Forms.

O código de exemplo a seguir mostra como usar um `com.adobe.idp.Context` objeto nas configurações de conexão usadas para criar um `EncryptionServiceClient` objeto.

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

### Chamar cenários {#invoking_scenarios-1}

Os cenários de chamada a seguir são discutidos nesta seção:

* Um aplicativo cliente em execução em sua própria máquina virtual Java (JVM) chama uma instância AEM Forms independente.
* Um aplicativo cliente em execução em sua própria JVM invoca instâncias do AEM Forms em cluster.

### Aplicativo cliente que invoca uma instância autônoma do AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

O diagrama a seguir mostra uma aplicação cliente sendo executada em sua própria JVM e chamando uma instância independente do AEM Forms.

Nesse cenário, um aplicativo cliente é executado em sua própria JVM e chama os serviços da AEM Forms.

>[!NOTE]
>
>Este cenário é o cenário de chamada no qual todos os Inícios rápidos se baseiam.

### Aplicativo cliente que invoca instâncias AEM Forms clusterizadas {#client-application-invoking-clustered-aem-forms-instances}

O diagrama a seguir mostra uma aplicação cliente sendo executada em sua própria JVM e chamando instâncias do AEM Forms em um cluster.

Esse cenário é semelhante a um aplicativo cliente que chama uma instância AEM Forms independente. No entanto, o URL do provedor é diferente. Se um aplicativo cliente quiser se conectar a um servidor de aplicativos J2EE específico, o aplicativo deverá alterar o URL para fazer referência ao servidor de aplicativos J2EE específico.

Não é recomendável fazer referência a um servidor de aplicativos J2EE específico porque a conexão entre o aplicativo cliente e o AEM Forms será encerrada se o servidor de aplicativos for interrompido. Recomenda-se que o URL do provedor faça referência a um gerenciador JNDI no nível da célula, em vez de um servidor de aplicativos J2EE específico.

Os aplicativos clientes que usam o modo de conexão SOAP podem usar a porta do balanceador de carga HTTP para o cluster. As aplicações clientes que usam o modo de conexão EJB podem se conectar à porta EJB de um servidor de aplicações J2EE específico. Esta ação lida com o Balanceamento de Carga entre nós de cluster.

**WebSphere**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para se conectar ao AEM Forms que é implantado no WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**Weblogic**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para se conectar a AEM Forms que é implantado no WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**Jboss**

O exemplo a seguir mostra o conteúdo de um arquivo jndi.properties usado para se conectar a AEM Forms que é implantado no JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Consulte seu administrador para determinar o nome e o número da porta do servidor de aplicativos J2EE.

**Consulte também**

[Inclusão de arquivos biblioteca Java AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Passar dados para serviços AEM Forms usando a API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Invocando um serviço usando um biblioteca do cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Passar dados para serviços AEM Forms usando a API Java {#passing-data-to-aem-forms-services-using-the-java-api}

As operações de serviço da AEM Forms normalmente consomem ou produzem documentos PDF. Quando você chama um serviço, às vezes é necessário passar um documento PDF (ou outros tipos de documento, como dados XML) para o serviço. Da mesma forma, às vezes é necessário manipular um documento PDF que é retornado do serviço. A classe Java que permite enviar dados de e para serviços da AEM Forms é `com.adobe.idp.Document`.

Os serviços da AEM Forms não aceitam um documento PDF como outros tipos de dados, como um `java.io.InputStream` objeto ou uma matriz de bytes. A `com.adobe.idp.Document` O objeto também pode ser usado para transmitir outros tipos de dados, como dados XML, para serviços.

A `com.adobe.idp.Document` objeto é um tipo serializável Java, portanto, pode ser passado por uma chamada RMI. O lado receptor pode ser colocado (mesmo host, mesmo carregador de classe), local (mesmo host, carregador de classe diferente) ou remoto (host diferente). A transmissão do conteúdo do documento é otimizada para cada caso. Por exemplo, se o remetente e o destinatário estiverem localizados no mesmo host, o conteúdo será transmitido por um sistema de arquivos local. (Em alguns casos, os documentos podem ser transmitidos na memória.)

Dependendo do `com.adobe.idp.Document` tamanho do objeto, os dados são transportados dentro do `com.adobe.idp.Document` ou armazenado no sistema de arquivos do servidor. Quaisquer recursos de armazenamento temporário ocupados pela `com.adobe.idp.Document` objetos são removidos automaticamente após o `com.adobe.idp.Document` eliminação. (Consulte [Descartando objetos de documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

Às vezes, é necessário saber o tipo de conteúdo de um `com.adobe.idp.Document` antes de passá-lo para um serviço. Por exemplo, se uma operação exigir um tipo de conteúdo específico, como `application/pdf`, é recomendável determinar o tipo de conteúdo. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

A variável `com.adobe.idp.Document` O objeto tenta determinar o tipo de conteúdo usando os dados fornecidos. Se o tipo de conteúdo não puder ser recuperado dos dados fornecidos (por exemplo, quando os dados tiverem sido fornecidos como uma matriz de bytes), defina o tipo de conteúdo. Para definir o tipo de conteúdo, chame o `com.adobe.idp.Document` do objeto `setContentType` método. (Consulte [Determinar o tipo de conteúdo de um documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se os arquivos auxiliares residirem no mesmo sistema de arquivos, criar um `com.adobe.idp.Document` objeto é mais rápido. Se os arquivos auxiliares residirem em sistemas de arquivos remotos, uma operação de cópia deverá ser feita, o que afeta o desempenho.

Um aplicativo pode conter ambos `com.adobe.idp.Document` e `org.w3c.dom.Document` tipos de dados. No entanto, certifique-se de qualificar totalmente a `org.w3c.dom.Document` tipo de dados. Para obter informações sobre como converter um `org.w3c.dom.Document` objeto a um `com.adobe.idp.Document` objeto, consulte [Início rápido (modo EJB): pré-preenchimento do Forms com layouts fluíveis usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

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

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Criação de documentos {#creating-documents}

Criar um `com.adobe.idp.Document` antes de chamar uma operação de serviço que requer um documento PDF (ou outros tipos de documento) como um valor de entrada. A variável `com.adobe.idp.Document` A classe fornece construtores que permitem criar um documento a partir dos seguintes tipos de conteúdo:

* Uma matriz de bytes
* Um existente `com.adobe.idp.Document` objeto
* A `java.io.File` objeto
* A `java.io.InputStream` objeto
* A `java.net.URL` objeto

#### Criando um documento baseado em uma matriz de bytes {#creating-a-document-based-on-a-byte-array}

O código de exemplo a seguir cria um `com.adobe.idp.Document` objeto baseado em uma matriz de bytes.

**Criando um objeto Document baseado em uma matriz de bytes**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Criando um documento baseado em outro documento {#creating-a-document-based-on-another-document}

O código de exemplo a seguir cria um `com.adobe.idp.Document` objeto que é baseado em outro `com.adobe.idp.Document` objeto.

**Criando um objeto Documento baseado em outro documento**

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

#### Criação de um documento baseado em um arquivo {#creating-a-document-based-on-a-file}

O código de exemplo a seguir cria um `com.adobe.idp.Document` objeto baseado em um arquivo de PDF chamado *map.pdf*. Esse arquivo está na raiz do disco rígido C. Esse construtor tenta definir o tipo de conteúdo MIME do `com.adobe.idp.Document` usando a extensão de nome de arquivo.

A variável `com.adobe.idp.Document` construtor que aceita um `java.io.File` O objeto também aceita um parâmetro booleano. Ao definir esse parâmetro como `true`, o `com.adobe.idp.Document` O objeto exclui o arquivo. Essa ação significa que não é necessário remover o arquivo após passá-lo para o `com.adobe.idp.Document` construtor.

Configurar este parâmetro para `false` significa que você retém a propriedade desse arquivo. Configurar este parâmetro para `true` O é mais eficiente. O motivo é porque a variável `com.adobe.idp.Document` pode mover o arquivo diretamente para a área gerenciada local em vez de copiá-lo (que é mais lento).

**Criação de um objeto Documento baseado em um arquivo PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Criando um documento com base em um objeto InputStream {#creating-a-document-based-on-an-inputstream-object}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto baseado em um `java.io.InputStream` objeto.

**Criando um documento com base em um objeto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Criar um documento com base no conteúdo acessível de um URL {#creating-a-document-based-on-content-accessible-from-an-url}

O exemplo de código Java a seguir cria um `com.adobe.idp.Document` objeto baseado em um arquivo de PDF chamado *map.pdf*. Esse arquivo está em um aplicativo web chamado `WebApp` que está sendo executado em `localhost`. Esse construtor tenta definir o `com.adobe.idp.Document` tipo de conteúdo MIME do objeto usando o tipo de conteúdo retornado com o protocolo de URL.

O URL fornecido para o `com.adobe.idp.Document` objeto é sempre lido no lado em que o original `com.adobe.idp.Document` é criado, conforme mostrado neste exemplo:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

O arquivo c:/temp/input.pdf deve estar localizado no computador cliente (não no computador do servidor). O computador cliente é onde o URL é lido e onde o `com.adobe.idp.Document` objeto foi criado.

**Criar um documento baseado em conteúdo acessíveis a partir de uma URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulte também**

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Manuseio de documentos retornados {#handling-returned-documents}

Operações de serviço que retornam uma documento PDF (ou outros tipos de dados, como dados XML), à medida que um valor de saída retorna um `com.adobe.idp.Document` objeto. Depois de receber um `com.adobe.idp.Document` objeto, é possível converter-lo nos seguintes formatos:

* Um `java.io.File` objeto
* Um `java.io.InputStream` objeto
* Uma matriz de bytes

A linha de código a seguir converte um `com.adobe.idp.Document` objeto a um `java.io.InputStream` objeto. Suponha que `myPDFDocument` representa um `com.adobe.idp.Document` objeto:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Da mesma forma, é possível copiar o conteúdo de um `com.adobe.idp.Document` para um arquivo local, executando as seguintes tarefas:

1. Criar um `java.io.File` objeto.
1. Chame o `com.adobe.idp.Document` do objeto `copyToFile` e transmita o `java.io.File`objeto.

O exemplo de código a seguir copia o conteúdo de um `com.adobe.idp.Document` para um arquivo chamado *AnotherMap.pdf*.

**Copiando o conteúdo de um objeto de documento para um arquivo**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulte também**

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinar o tipo de conteúdo de um documento {#determining-the-content-type-of-a-document}

Determine o tipo MIME de um `com.adobe.idp.Document` ao invocar o `com.adobe.idp.Document` do objeto `getContentType` método. Esse método retorna um valor de string que especifica o tipo de conteúdo do `com.adobe.idp.Document` objeto. A tabela a seguir descreve os diferentes tipos de conteúdo que o AEM Forms retorna.

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
   <td><p>XML Data Packaging (XDP), que é usado para formulários XML Forms Architecture (XFA) exportados</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Marcadores, anexos ou outros documentos XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato de dados Forms (FDF), que é usado para formulários Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), que é usado para formulários Acrobat exportados</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Rich data format e XML</p></td>
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

O código de exemplo a seguir determina o tipo de conteúdo de um `com.adobe.idp.Document` objeto.

**Determinação do tipo de conteúdo de um objeto Documento**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulte também**

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties)

### Descartando objetos de documento {#disposing-document-objects}

Quando não precisar mais de um `Document` objeto, é recomendável descartá-lo chamando seu `dispose` método. Each `Document` O objeto do consome um descritor de arquivo e até 75 MB de espaço RAM na plataforma do host do aplicativo. Se um `Document` objeto não for descartado, o processo de coleta do Java Garage o descartará. No entanto, ao eliminá-lo mais cedo, utilizando o método `dispose` você pode liberar a memória ocupada pelo `Document` objeto.

**Consulte também**

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Chamar um serviço usando uma biblioteca cliente Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Chamar um serviço usando uma biblioteca cliente Java {#invoking-a-service-using-a-java-client-library}

As operações de serviço do AEM Forms podem ser chamadas usando uma API altamente tipada do serviço, que é conhecida como uma biblioteca de cliente Java. A *Biblioteca cliente Java* é um conjunto de classes concretas que fornecem acesso aos serviços implantados no container de serviço. Você instancia um objeto Java que representa o serviço a ser chamado em vez de criar um `InvocationRequest` usando a API de chamada. A API de chamada é usada para chamar processos, como processos de longa duração, criados no Workbench. (Consulte [Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Para executar uma operação de serviço, chame um método que pertence ao objeto Java. Uma biblioteca cliente Java contém métodos que normalmente mapeiam de um para um com operações de serviço. Ao usar uma biblioteca cliente Java, defina as propriedades de conexão necessárias. (Consulte [Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)

Depois de definir as propriedades de conexão, crie uma `ServiceClientFactory` objeto que é usado para instanciar um objeto Java que permite chamar um serviço. Cada serviço que tem uma biblioteca cliente Java tem um objeto cliente correspondente. Por exemplo, para chamar o serviço de Repositório, crie um `ResourceRepositoryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto. A variável `ServiceClientFactory` O objeto é responsável por manter as configurações de conexão necessárias para chamar os serviços da AEM Forms.

Embora a obtenção `ServiceClientFactory` normalmente é rápida, algumas despesas gerais estão envolvidas quando a fábrica é usada pela primeira vez. Esse objeto é otimizado para reutilização e, portanto, quando possível, usa o mesmo `ServiceClientFactory` quando estiver criando vários objetos de cliente Java. Ou seja, não crie uma `ServiceClientFactory` para cada objeto da biblioteca do cliente que você criar.

Há uma configuração do Gerenciador de Usuários que controla o tempo de vida da asserção SAML que está dentro do `com.adobe.idp.Context` objeto que afeta o `ServiceClientFactory` objeto. Essa configuração controla toda a vida útil do contexto de autenticação em todo o AEM Forms, incluindo todas as chamadas executadas usando a API Java. Por padrão, o período em que um `ServiceCleintFactory` pode ser usado é de duas horas.

>[!NOTE]
>
>Para explicar como chamar um serviço usando a API do Java, as funções do Serviço de repositório `writeResource` a operação é chamada. Essa operação coloca um novo recurso no repositório.

Você pode invocar o serviço de repositório usando um biblioteca do cliente Java e executando as seguintes etapas:

1. Inclua arquivos JAR do cliente, como o adobe-repositório-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão AEM Forms arquivos](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) de biblioteca Java.
1. Defina as propriedades de conexão necessárias para executar um serviço.
1. Criar um `ServiceClientFactory` ao invocar o `ServiceClientFactory` estática do objeto `createInstance` e transmitindo o `java.util.Properties` objeto que contém propriedades de conexão.
1. Criar um `ResourceRepositoryClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto. Use o `ResourceRepositoryClient` objeto para invocar as operações de serviço de repositório.
1. Criar um `RepositoryInfomodelFactoryBean` objeto usando seu construtor e passar `null`. Esse objeto permite criar um `Resource` objeto que represente o conteúdo adicionado ao repositório.
1. Criar um `Resource` objeto invocando o `RepositoryInfomodelFactoryBean` método do `newImage` objeto e passando os seguintes valores:

   * Um valor de ID exclusivo ao especificar `new Id()`.
   * Um valor de UUID exclusivo especificando `new Lid()`.
   * O nome do recurso. Você pode especificar o nome do arquivo XDP.

   Converter o valor de retorno em `Resource`.

1. Criar um `ResourceContent` ao invocar o `RepositoryInfomodelFactoryBean` do objeto `newImage` e conversão do valor de retorno em `ResourceContent`. Esse objeto representa o conteúdo adicionado ao repositório.
1. Criar um `com.adobe.idp.Document` ao passar um `java.io.FileInputStream` objeto que armazena o arquivo XDP a ser adicionado ao repositório. (Consulte [Criando um documento com base em um objeto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Adicione o conteúdo do `com.adobe.idp.Document` objeto para o `ResourceContent` ao invocar o `ResourceContent` do objeto `setDataDocument` método. Passe o `com.adobe.idp.Document` objeto.
1. Defina o tipo MIME do arquivo XDP a ser adicionado ao repositório, chamando o `ResourceContent` do objeto `setMimeType` método e transmissão `application/vnd.adobe.xdp+xml`.
1. Adicione o conteúdo do `ResourceContent` objeto para o `Resource` ao invocar o `Resource` do objeto `setContent` e transmitindo o `ResourceContent` objeto.
1. Adicione uma descrição do recurso chamando o `Resource` do objeto `setDescription` e transmitindo um valor de string que representa uma descrição do recurso.
1. Adicione o design do formulário ao repositório invocando o `ResourceRepositoryClient` do objeto `writeResource` e transmitindo os seguintes valores:

   * Um valor de string que especifica o caminho para a coleção de recursos que contém o novo recurso
   * A variável `Resource` objeto que foi criado

**Consulte também**

[Início rápido (modo EJB): Gravação de um recurso usando a API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Chamada de AEM Forms usando a API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Chamar um processo de vida curta usando a API de chamada {#invoking-a-short-lived-process-using-the-invocation-api}

Você pode chamar um processo de curta duração usando a API de chamada Java. Ao invocar um processo de curta duração usando a API de chamada, você transmite os valores de parâmetro necessários usando uma `java.util.HashMap` objeto. Para cada parâmetro passar para um serviço, chame o `java.util.HashMap` do objeto `put` e especifique o par nome-valor exigido pelo serviço para executar a operação especificada. Especifique o nome exato dos parâmetros que pertencem ao processo de vida curta.

>[!NOTE]
>
>Para obter informações sobre como invocar um processo de longa duração, consulte [Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

A discussão aqui é sobre o uso da API de chamada para invocar o seguinte processo de vida curta do AEM Forms chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este processo não se baseia em um processo AEM Forms existente. Para seguir o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação baseia-se no `SetValue` operação. O parâmetro de entrada para esse processo é um `document` variável de processo chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação baseia-se no `PasswordEncryptPDF` operação. O documento de PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

### Chame o processo de curta duração MyApplication/EncryptDocument usando a API de invocação Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Chame o `MyApplication/EncryptDocument` processo de vida curta usando a API de invocação Java:

1. Inclua arquivos JAR do cliente, como adobe-livecycle-client.jar, no caminho de classe do projeto Java. (Consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Criar um `ServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto. A `ServiceClient` object permite chamar uma operação de serviço. Ela lida com tarefas como localização, despacho e solicitações de chamada de roteamento.
1. Criar um `java.util.HashMap` usando seu construtor.
1. Chame o `java.util.HashMap` do objeto `put` para que cada parâmetro de entrada passe para o processo de longa vida. Como a variável `MyApplication/EncryptDocument` processo de vida curta requer um parâmetro de entrada do tipo `Document`, você só precisa invocar o `put` método uma vez, conforme mostrado no exemplo a seguir.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Criar um `InvocationRequest` ao invocar o `ServiceClientFactory` do objeto `createInvocationRequest` e transmitindo os seguintes valores:

   * Um valor de string que especifica o nome do processo de longa duração a ser chamado. Para invocar o `MyApplication/EncryptDocument` processo, especificar `MyApplication/EncryptDocument`.
   * Um valor de string que representa o nome da operação do processo. Normalmente, o nome de uma operação de processo de curta duração é `invoke`.
   * A variável `java.util.HashMap` objeto que contém os valores de parâmetro exigidos pela operação de serviço.
   * Um valor booliano que especifica `true`, que cria uma solicitação síncrona (esse valor é aplicável para invocar um processo de curta duração).

1. Envie a solicitação de invocação para o serviço chamando o `ServiceClient` do objeto `invoke` e transmitindo o `InvocationRequest` objeto. A variável `invoke` o método retorna um `InvocationReponse` objeto.

   >[!NOTE]
   >
   >Um processo de longa duração pode ser chamado transmitindo o valor `false`como o quarto parâmetro do `createInvocationRequest` método. Transmitindo o valor `false`*cria uma solicitação assíncrona.*

1. Recupere o valor de retorno do processo chamando o `InvocationReponse` do objeto `getOutputParameter` e transmitindo um valor de string que especifica o nome do parâmetro de saída. Nesta situação, especifique `outDoc` ( `outDoc` é o nome do parâmetro de saída para o `MyApplication/EncryptDocument` processo). Converter o valor de retorno em `Document`, conforme mostrado no exemplo a seguir.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Criar um `java.io.File` e verifique se a extensão do arquivo é .pdf.
1. Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo. Certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getOutputParameter` método.

**Consulte também**

[Início Rápido: Chamar um processo de vida curta usando a API de Chamada](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusão de arquivos da biblioteca Java do AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
