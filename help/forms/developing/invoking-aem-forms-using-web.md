---
title: Invocar o AEM Forms usando os Serviços da Web
seo-title: Invocar o AEM Forms usando os Serviços da Web
description: Chame os processos da AEM Forms usando serviços da Web com suporte total para a geração de WSDL.
seo-description: Chame os processos da AEM Forms usando serviços da Web com suporte total para a geração de WSDL.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '9990'
ht-degree: 0%

---


# Invocando o AEM Forms usando os Serviços Web {#invoking-aem-forms-using-web-services}

A maioria dos serviços da AEM Forms no container de serviço está configurada para expor um serviço da Web, com suporte total para a geração WSDL (Web Service Definition Language). Ou seja, você pode criar objetos proxy que consomem a pilha SOAP nativa de um serviço AEM Forms. Como resultado, os serviços da AEM Forms podem trocar e processar as seguintes mensagens SOAP:

* **Solicitação** SOAP: Enviado para um serviço Forms por um aplicativo cliente solicitando uma ação.
* **Resposta** SOAP: Enviado para um aplicativo cliente por um serviço da Forms depois que uma solicitação SOAP é processada.

Usando os serviços da Web, você pode executar as mesmas operações dos serviços da AEM Forms que pode usando a API Java. Uma vantagem de usar os serviços da Web para chamar os serviços da AEM Forms é que você pode criar um aplicativo cliente em um ambiente de desenvolvimento compatível com SOAP. Um aplicativo cliente não está vinculado a um ambiente de desenvolvimento específico ou linguagem de programação. Por exemplo, você pode criar um aplicativo cliente usando o Microsoft Visual Studio .NET e C# como linguagem de programação.

Os serviços AEM Forms são expostos através do protocolo SOAP e são compatíveis com o WSI Basic Perfil 1.1. A WSI (Web Services Interoperability) é uma organização de padrões abertos que promove a interoperabilidade do serviço da Web entre plataformas. Para obter informações, consulte [https://www.ws-i.org/](https://www.ws-i.org).

A AEM Forms suporta os seguintes padrões de serviço da Web:

* **Codificação**: Suporta somente codificação documento e literal (que é a codificação preferencial de acordo com o Perfil básico WSI). (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Representa uma maneira de codificar anexos com solicitações SOAP. (Consulte [Invocar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Representa outra maneira de codificar anexos com solicitações SOAP. (Consulte [Invocando o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP com anexos**: Suporta MIME e DIME (Direct Internet Message Encapsulation). Esses protocolos são maneiras padrão de enviar anexos por SOAP. Os aplicativos Microsoft Visual Studio .NET usam DIME. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: Suporta um perfil de token de senha de nome de usuário, que é uma maneira padrão de enviar nomes de usuário e senhas como parte do cabeçalho SOAP do WS Security. A AEM Forms também oferece suporte à autenticação básica HTTP. (Consulte [Passando credenciais usando cabeçalhos WS-Security](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html).)

Para chamar os serviços da AEM Forms usando um serviço da Web, geralmente você cria uma biblioteca de proxy que consome o serviço WSDL. A seção *Invocar o AEM Forms usando os Serviços Web* usa o JAX-WS para criar classes proxy Java para chamar serviços. (Consulte [Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Você pode recuperar um WDSL de serviço especificando a seguinte definição de URL (os itens entre colchetes são opcionais):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

em que:

* *your_* serverhostrepresenta o endereço IP do servidor de aplicativos J2EE que hospeda a AEM Forms.
* *your_* portrepresenta a porta HTTP que o servidor de aplicativos J2EE usa.
* *service_* namereapresenta o nome do serviço.
* *A* versão representa a versão de público alvo de um serviço (a versão de serviço mais recente é usada por padrão).
* `async` especifica o valor  `true` para ativar operações adicionais para invocação assíncrona ( `false` por padrão).
* *lc_* version representa a versão do AEM Forms que você deseja invocar.

A tabela a seguir lista as definições WSDL do serviço (supondo que o AEM Forms esteja implantado no host local e a publicação seja 8080).

<table>
 <thead>
  <tr>
   <th><p>Serviço</p></th>
   <th><p>Definição WSDL</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assembler</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Voltar e restaurar</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>formulários em código de barras</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Converter PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Criptografia </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integração de dados de formulário</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Gerar PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Gerar PDF 3D</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Saída</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilitários PDF </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Extensões Acrobat Reader DC</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Repositório</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Assinatura </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilitários XMP</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**Definições WSDL do processo AEM Forms**

Você deve especificar o nome do Aplicativo e o nome do Processo na definição WSDL para acessar um WSDL que pertence a um processo criado no Workbench. Suponha que o nome do aplicativo seja `MyApplication` e que o nome do processo seja `EncryptDocument`. Nessa situação, especifique a seguinte definição de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Para obter informações sobre o exemplo `MyApplication/EncryptDocument` processo de curta duração, consulte [Exemplo de processo de curta duração](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Um aplicativo pode conter pastas. Nesse caso, especifique os nomes das pastas na definição WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Acessar novas funcionalidades usando serviços da Web**

A nova funcionalidade do serviço AEM Forms pode ser acessada usando os serviços da Web. Por exemplo, no AEM Forms, é introduzida a capacidade de codificar anexos usando MTOM. (Consulte [Invocar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)

Para acessar a nova funcionalidade introduzida no AEM Forms, especifique o atributo `lc_version` na definição WSDL. Por exemplo, para acessar a nova funcionalidade do serviço (incluindo suporte a MTOM), especifique a seguinte definição de WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Ao definir o atributo `lc_version`, certifique-se de usar três dígitos. Por exemplo, 9.0.1 é igual à versão 9.0.

**Tipo de dados BLOB do serviço Web**

As WSDLs de serviço AEM Forms definem muitos tipos de dados. Um dos tipos de dados mais importantes expostos em um serviço da Web é um tipo `BLOB`. Esse tipo de dados mapeia para a classe `com.adobe.idp.Document` ao trabalhar com APIs AEM Forms Java. (Consulte [Passar dados para os serviços da AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Um objeto `BLOB` envia e recupera dados binários (por exemplo, arquivos PDF, dados XML etc.) de e para os serviços AEM Forms. O tipo `BLOB` é definido em um WSDL de serviço da seguinte maneira:

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

Os campos `MTOM` e `swaRef` são suportados apenas no AEM Forms. Você pode usar esses novos campos somente se especificar um URL que inclua a propriedade `lc_version`.

**Fornecimento de objetos BLOB em solicitações de serviço**

Se uma operação de serviço AEM Forms exigir um tipo `BLOB` como valor de entrada, crie uma instância do tipo `BLOB` na lógica do aplicativo. (Muitos dos start rápidos do serviço da Web localizados em *Programação com formulários AEM* mostram como trabalhar com um tipo de dados BLOB.)

Atribua valores aos campos que pertencem à instância `BLOB` da seguinte forma:

* **Base64**: Para transmitir dados como texto codificado em um formato Base64, defina os dados no  `BLOB.binaryData` campo e defina o tipo de dados no formato MIME (por exemplo,  `application/pdf`) no  `BLOB.contentType` campo. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Para transmitir dados binários em um anexo MTOM, defina os dados no  `BLOB.MTOM` campo. Essa configuração anexa os dados à solicitação SOAP usando a estrutura Java JAX-WS ou a API nativa da estrutura SOAP. (Consulte [Invocar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Para transmitir dados binários em um anexo SwaRef do WS-I, defina os dados no  `BLOB.swaRef` campo. Essa configuração anexa os dados à solicitação SOAP usando a estrutura Java JAX-WS. (Consulte [Invocando o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)
* **Anexo MIME ou DIME**: Para transmitir dados em um anexo MIME ou DIME, anexe os dados à solicitação SOAP usando a API nativa da estrutura SOAP. Defina o identificador do anexo no campo `BLOB.attachmentID`. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **URL** remoto: Se os dados estiverem hospedados em um servidor da Web e acessíveis por meio de um URL HTTP, defina o URL HTTP no  `BLOB.remoteURL` campo. (Consulte [Invocar o AEM Forms usando dados BLOB em HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Acessar dados em objetos BLOB retornados de serviços**

O protocolo de transmissão para objetos `BLOB` retornados depende de vários fatores, que são considerados na seguinte ordem, interrompendo quando a condição principal é atendida:

1. **O URL do público alvo especifica o protocolo** de transmissão. Se o URL do público alvo especificado na invocação SOAP contiver o parâmetro `blob="`*BLOB_TYPE*&quot;, *BLOB_TYPE* determinará o protocolo de transmissão. *BLOB_* TYPEé um espaço reservado para base64, dime, mime, http, mtom ou swaref.
1. **O terminal SOAP do serviço é Smart**. Se as seguintes condições forem verdadeiras, os documentos de saída serão retornados usando o mesmo protocolo de transmissão que os documentos de entrada:

   * O parâmetro de ponto final SOAP do serviço Protocolo padrão para objetos de blob de saída está definido como Inteligente.

      Para cada serviço com um terminal SOAP, o console de administração permite que você especifique o protocolo de transmissão para quaisquer blobs retornados. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * O serviço AEM Forms recebe um ou mais documentos como entrada.

1. **O terminal SOAP de serviço não é inteligente**. O protocolo configurado determina o protocolo de transmissão do documento e os dados são retornados no campo `BLOB` correspondente. Por exemplo, se o terminal SOAP estiver definido como DIME, o blob retornado estará no campo `blob.attachmentID` independentemente do protocolo de transmissão de qualquer documento de entrada.
1. **Caso contrário**. Se um serviço não tomar o tipo de documento como entrada, os documentos de saída serão retornados no campo `BLOB.remoteURL` sobre o protocolo HTTP.

Conforme descrito na primeira condição, é possível garantir o tipo de transmissão para qualquer documentos retornado estendendo o URL do terminal SOAP com um sufixo, da seguinte forma:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Esta é a correlação entre os tipos de transmissão e o campo a partir do qual você obtém os dados:

* **Formato** Base64: Defina o  `blob` sufixo como  `base64` para retornar os dados no  `BLOB.binaryData` campo.
* **Anexo MIME ou DIME**: Defina o  `blob` sufixo como  `DIME` ou  `MIME` para retornar os dados como um tipo de anexo correspondente com o identificador de anexo retornado no  `BLOB.attachmentID` campo. Use a API proprietária da estrutura SOAP para ler os dados do anexo.
* **URL** remoto: Defina o  `blob` sufixo  `http` para manter os dados no servidor de aplicativos e retornar o URL apontando para os dados no  `BLOB.remoteURL` campo.
* **MTOM ou SwaRef**: Defina o  `blob` sufixo como  `mtom` ou  `swaref` para retornar os dados como um tipo de anexo correspondente com o identificador de anexo retornado nos  `BLOB.MTOM` ou  `BLOB.swaRef` campos. Use a API nativa da estrutura SOAP para ler os dados do anexo.

>[!NOTE]
>
>É recomendável que você não exceda 30 MB ao preencher um objeto `BLOB` chamando seu método `setBinaryData`. Caso contrário, há a possibilidade de ocorrer uma exceção `OutOfMemory`.

>[!NOTE]
>
>Os aplicativos baseados no JAX WS que usam o protocolo de transmissão MTOM estão limitados a 25 MB de dados enviados e recebidos. Essa limitação se deve a um erro no JAX-WS. Se o tamanho combinado dos arquivos enviados e recebidos exceder 25 MB, use o protocolo de transmissão SwaRef em vez do MTOM. Caso contrário, há a possibilidade de uma exceção `OutOfMemory`.

**Transmissão MTOM de matrizes de bytes codificadas em base64**

Além do objeto `BLOB`, o protocolo MTOM suporta qualquer parâmetro de matriz de bytes ou campo de matriz de bytes de um tipo complexo. Isso significa que estruturas SOAP do cliente que oferecem suporte a MTOM podem enviar qualquer elemento `xsd:base64Binary` como um anexo MTOM (em vez de um texto codificado em base64). Os pontos de extremidade SOAP da AEM Forms podem ler esse tipo de codificação de matriz de bytes. Entretanto, o serviço AEM Forms sempre retorna um tipo de matriz de bytes como um texto codificado em base64. Os parâmetros da matriz de bytes de saída não suportam MTOM.

Os serviços AEM Forms que retornam uma grande quantidade de dados binários usam o tipo Documento/BLOB em vez do tipo de matriz de bytes. O tipo de Documento é muito mais eficiente para transmitir grandes quantidades de dados.

## Tipos de dados de serviço da Web {#web-service-data-types}

A tabela a seguir lista os tipos de dados Java e mostra o tipo de dados do serviço da Web correspondente.

<table>
 <thead>
  <tr>
   <th><p>Tipo de dados Java</p></th>
   <th><p>Tipo de dados do serviço Web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>O tipo <code>DATE</code>, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço AEM Forms usar um valor <code>java.util.Date</code> como entrada, o aplicativo cliente SOAP deverá passar a data no campo <code>DATE.date</code>. A configuração do campo <code>DATE.calendar</code> nesse caso causa uma exceção de tempo de execução. Se o serviço retornar um <code>java.util.Date</code>, a data será retornada no campo <code>DATE.date</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>O tipo <code>DATE</code>, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço AEM Forms usar um valor <code>java.util.Calendar</code> como entrada, o aplicativo cliente SOAP deverá passar a data no campo <code>DATE.caledendar</code>. A definição do campo <code>DATE.date</code> nesse caso causa uma exceção de tempo de execução. Se o serviço retornar um <code>java.util.Calendar</code>, a data será retornada no campo <code>DATE.calendar</code>. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>O <code>apachesoap:Map</code>, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>O Mapa é representado como uma sequência de pares de chave/valor.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>O tipo XML, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço AEM Forms aceitar um valor <code>org.w3c.dom.Document</code>, passe os dados XML no campo <code>XML.document</code>.</p><p>Configurar o campo <code>XML.element</code> causa uma exceção de tempo de execução. Se o serviço retornar um <code>org.w3c.dom.Document</code>, os dados XML serão retornados no campo <code>XML.document</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>O tipo XML, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço AEM Forms usar <code>org.w3c.dom.Element</code> como entrada, passe os dados XML no campo <code>XML.element</code>.</p><p>Configurar o campo <code>XML.document</code> causa uma exceção de tempo de execução. Se o serviço retornar um <code>org.w3c.dom.Element</code>, os dados XML serão retornados no campo <code>XML.element</code>.</p></td>
  </tr>
 </tbody>
</table>

**Site do desenvolvedor do Adobe**

O site do desenvolvedor do Adobe contém o seguinte artigo que discute a chamada dos serviços da AEM Forms usando a API de serviço da Web:

[Criação de formulários renderizando aplicativos ASP.NET](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[Invocar serviços da Web usando componentes personalizados](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>Invocar serviços da Web usando componentes personalizados descreve como criar um componente AEM Forms que chama serviços da Web de terceiros.

## Criação de classes proxy Java usando JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Você pode usar o JAX-WS para converter um serviço Forms WSDL em classes proxy Java. Essas classes permitem que você chame operações de serviços da AEM Forms. O Apache Ant permite que você crie um script de compilação que gera classes proxy Java referenciando um WSDL de serviço da AEM Forms. Você pode gerar arquivos proxy JAX-WS executando as seguintes etapas:

1. Instale o Apache Ant no computador cliente. (Consulte [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Adicione o diretório bin ao caminho da classe.
   * Defina a variável de ambiente `ANT_HOME` no diretório em que você instalou o Ant.

1. Instale o JDK 1.6 ou posterior.

   * Adicione o diretório JDK bin ao caminho da classe.
   * Adicione o diretório JRE bin ao caminho da classe. Este compartimento está localizado no diretório `[JDK_INSTALL_LOCATION]/jre`.
   * Defina a variável de ambiente `JAVA_HOME` no diretório em que você instalou o JDK.

   O JDK 1.6 inclui o programa wsimport usado no arquivo build.xml. O JDK 1.5 não inclui esse programa.

1. Instale o JAX-WS no computador cliente. (Consulte [API Java para XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Use JAX-WS e Apache Ant para gerar classes proxy Java. Crie um script de construção Ant para realizar essa tarefa. O script a seguir é um exemplo de script de construção Ant chamado build.xml:

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   Dentro desse script de construção Ant, observe que a propriedade `url` está definida para fazer referência ao WSDL do serviço de criptografia em execução no localhost. As propriedades `username` e `password` devem ser definidas como um nome de usuário e senha válidos para formulários AEM. Observe que o URL contém o atributo `lc_version`. Sem especificar a opção `lc_version`, não é possível chamar novas operações de serviço da AEM Forms.

   >[!NOTE]
   >
   >Substitua `EncryptionService`pelo nome do serviço AEM Forms que você deseja invocar usando classes proxy Java. Por exemplo, para criar classes proxy Java para o serviço Rights Management, especifique:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Crie um arquivo BAT para executar o script de criação Ant. O seguinte comando pode ser localizado em um arquivo BAT responsável pela execução do script de compilação Ant:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Coloque o script de criação ANT no diretório C:\Program Files\Java\jaxws-ri\bin directory. O script grava os arquivos JAVA no .pasta /classes. O script gera arquivos JAVA que podem chamar o serviço.

1. Empacote os arquivos JAVA em um arquivo JAR. Se você estiver trabalhando no Eclipse, siga estas etapas:

   * Crie um novo projeto Java que seja usado para disponibilizar os arquivos JAVA proxy em um arquivo JAR.
   * Crie uma pasta de origem no projeto.
   * Crie um pacote `com.adobe.idp.services` na pasta Origem.
   * Selecione o pacote `com.adobe.idp.services` e importe os arquivos JAVA da pasta adobe/idp/services para o pacote.
   * Se necessário, crie um pacote `org/apache/xml/xmlsoap` na pasta Origem.
   * Selecione a pasta de origem e importe os arquivos JAVA da pasta org/apache/xml/xmlsoap.
   * Defina o nível de conformidade do compilador Java como 5.0 ou superior.
   * Construa o projeto.
   * Exporte o projeto como um arquivo JAR.
   * Importe este arquivo JAR no caminho de classe de um projeto cliente. Além disso, importe todos os arquivos JAR localizados em &lt;Diretório de instalação>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Todos os start rápidos do serviço da Web Java (exceto o serviço Forms) localizados em Programação com formulários AEM criam arquivos proxy Java usando JAX-WS. Além disso, todos os start rápidos do serviço da Web Java usam SwaRef. (Consulte [Invocando o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)

**Consulte também:**

[Criação de classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis)

[Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding)

[Invocar o AEM Forms usando dados BLOB por HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Invocando o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref)

## Criação de classes proxy Java usando o Apache Axis {#creating-java-proxy-classes-using-apache-axis}

Você pode usar a ferramenta Apache Axis WSDL2Java para converter um serviço Forms em classes proxy Java. Essas classes permitem que você chame operações de serviço da Forms. Usando o Apache Ant, você pode gerar arquivos da biblioteca do Axis a partir de um WSDL de serviço. Você pode baixar o Apache Axis no URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Os start rápidos do serviço da Web associados ao serviço Forms usam classes proxy Java criadas usando o Apache Axis. Os start rápidos do serviço da Web da Forms também usam o Base64 como tipo de codificação. (Consulte [Start Rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

Você pode gerar arquivos da biblioteca Java Axis executando as seguintes etapas:

1. Instale o Apache Ant no computador cliente. Está disponível em [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Adicione o diretório bin ao caminho da classe.
   * Defina a variável de ambiente `ANT_HOME` no diretório em que você instalou o Ant.

1. Instale o Apache Axis 1.4 no computador cliente. Está disponível em [https://ws.apache.org/axis/](https://ws.apache.org/axis/.md).
1. Configure o caminho da classe para usar os arquivos Axis JAR no cliente de serviço da Web, conforme descrito nas instruções de instalação do Axis em [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Use a ferramenta Apache WSDL2Java no Axis para gerar classes proxy Java. Crie um script de construção Ant para realizar essa tarefa. O script a seguir é um exemplo de script de construção Ant chamado build.xml:

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   Dentro desse script de construção Ant, observe que a propriedade `url` está definida para fazer referência ao WSDL do serviço de criptografia em execução no localhost. As propriedades `username` e `password` devem ser definidas como um nome de usuário e senha válidos para formulários AEM.

1. Crie um arquivo BAT para executar o script de criação Ant. O seguinte comando pode ser localizado em um arquivo BAT responsável pela execução do script de compilação Ant:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   Os arquivos JAVA são gravados na propriedade C:\JavaFiles folder as specified by the `output`. Para chamar com êxito o serviço Forms, importe esses arquivos JAVA para o caminho da classe.

   Por padrão, esses arquivos pertencem a um pacote Java chamado `com.adobe.idp.services`. É recomendável colocar esses arquivos JAVA em um arquivo JAR. Em seguida, importe o arquivo JAR para o caminho de classe do aplicativo cliente.

   >[!NOTE]
   >
   >Há diferentes maneiras de colocar arquivos .JAVA em um JAR. Uma maneira é usar um Java IDE como o Eclipse. Crie um projeto Java e crie um pacote `com.adobe.idp.services`(todos os arquivos .JAVA pertencem a este pacote). Em seguida, importe todos os arquivos .JAVA para o pacote. Por fim, exporte o projeto como um arquivo JAR.

1. Altere o URL na classe `EncryptionServiceLocator` para especificar o tipo de codificação. Por exemplo, para usar base64, especifique `?blob=base64` para garantir que o objeto `BLOB` retorne dados binários. Ou seja, na classe `EncryptionServiceLocator`, localize a seguinte linha de código:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   e alterá-lo para:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Adicione os seguintes arquivos Axis JAR ao caminho de classe do seu projeto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   Esses arquivos JAR estão no diretório `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty`.

**Consulte também:**

[Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding)

[Invocar o AEM Forms usando dados BLOB por HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Invocar o AEM Forms usando a codificação Base64 {#invoking-aem-forms-using-base64-encoding}

Você pode chamar um serviço AEM Forms usando a codificação Base64. A codificação Base64 codifica anexos enviados com uma solicitação de chamada de serviço da Web. Ou seja, `BLOB` os dados são codificados em Base64, não a mensagem SOAP inteira.

&quot;Invocar o AEM Forms usando a codificação Base64&quot; discute invocar o seguinte processo de curta duração do AEM Forms chamado `MyApplication/EncryptDocument` usando a codificação Base64.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

### Criando um assembly de cliente .NET que usa a codificação Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

Você pode criar um assembly de cliente .NET para chamar um serviço Forms de um projeto do Microsoft Visual Studio .NET. Para criar um assembly de cliente .NET que use a codificação base64, execute as seguintes etapas:

1. Crie uma classe proxy com base em um URL de invocação do AEM Forms.
1. Crie um projeto do Microsoft Visual Studio .NET que produza o assembly do cliente .NET.

**Criação de uma classe proxy**

Você pode criar uma classe proxy usada para criar o assembly do cliente .NET usando uma ferramenta que acompanha o Microsoft Visual Studio. O nome da ferramenta é wsdl.exe e está localizado na pasta de instalação do Microsoft Visual Studio. Para criar uma classe proxy, abra o prompt de comando e navegue até a pasta que contém o arquivo wsdl.exe. Para obter mais informações sobre a ferramenta wsdl.exe, consulte a *Ajuda do MSDN*.

Digite o seguinte comando no prompt de comando:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Por padrão, essa ferramenta cria um arquivo CS na mesma pasta que se baseia no nome do WSDL. Nessa situação, ele cria um arquivo CS chamado *EncryptDocumentService.cs*. Use esse arquivo CS para criar um objeto proxy que permite chamar o serviço especificado no URL de invocação.

Altere o URL na classe proxy para incluir `?blob=base64` para garantir que o objeto `BLOB` retorne dados binários. Na classe proxy, localize a seguinte linha de código:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

e alterá-lo para:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

A seção *Invocar o AEM Forms usando o Base64 Encoding* usa `MyApplication/EncryptDocument` como exemplo. Se você estiver criando um assembly de cliente .NET para outro serviço Forms, substitua `MyApplication/EncryptDocument` pelo nome do serviço.

**Desenvolvendo o assembly do cliente .NET**

Crie um projeto da Biblioteca de classes do Visual Studio que produz um assembly de cliente .NET. O arquivo CS criado usando wsdl.exe pode ser importado para este projeto. Este projeto produz um arquivo DLL (o assembly do cliente .NET) que você pode usar em outros projetos do Visual Studio .NET para chamar um serviço.

1. Start Microsoft Visual Studio .NET.
1. Crie um projeto de Biblioteca de classes e nomeie-o DocumentService.
1. Importe o arquivo CS que você criou usando wsdl.exe.
1. No menu **Project**, selecione **Adicionar referência**.
1. Na caixa de diálogo Adicionar referência, selecione **System.Web.Services.dll**.
1. Clique em **Selecione** e clique em **OK**.
1. Compile e crie o projeto.

>[!NOTE]
>
>Este procedimento cria um assembly de cliente .NET chamado DocumentService.dll que você pode usar para enviar solicitações SOAP ao serviço `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Certifique-se de ter adicionado `?blob=base64` ao URL na classe proxy usada para criar o assembly do cliente .NET. Caso contrário, você não poderá recuperar dados binários do objeto `BLOB`.

**Referência ao assembly do cliente .NET**

Coloque seu assembly cliente .NET recém criado no computador onde você está desenvolvendo seu aplicativo cliente. Depois de colocar o assembly do cliente .NET em um diretório, você pode referenciá-lo a partir de um projeto. Consulte também a biblioteca `System.Web.Services` do seu projeto. Se você não fizer referência a esta biblioteca, não poderá usar o assembly do cliente .NET para chamar um serviço.

1. No menu **Project**, selecione **Adicionar referência**.
1. Clique na guia **.NET**.
1. Clique em **Procurar** e localize o arquivo DocumentService.dll.
1. Clique em **Selecione** e clique em **OK**.

**Invocar um serviço usando um assembly de cliente .NET que usa codificação Base64**

Você pode chamar o serviço `MyApplication/EncryptDocument` (que foi criado no Workbench) usando um assembly cliente .NET que usa a codificação Base64. Para chamar o serviço `MyApplication/EncryptDocument`, execute as seguintes etapas:

1. Crie um assembly de cliente Microsoft .NET que consuma o serviço `MyApplication/EncryptDocument` WSDL.
1. Crie um projeto cliente do Microsoft .NET. Faça referência ao assembly do cliente Microsoft .NET no projeto do cliente. Consulte também `System.Web.Services`.
1. Usando o assembly do cliente Microsoft .NET, crie um objeto `MyApplication_EncryptDocumentService` chamando seu construtor padrão.
1. Defina a propriedade `MyApplication_EncryptDocumentService` do objeto `Credentials` com um objeto `System.Net.NetworkCredential`. No construtor `System.Net.NetworkCredential`, especifique um nome de usuário para formulários AEM e a senha correspondente. Defina valores de autenticação para permitir que seu aplicativo cliente .NET troque mensagens SOAP com êxito com o AEM Forms.
1. Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF enviado para o processo `MyApplication/EncryptDocument`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
1. Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
1. Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
1. Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` ao conteúdo da matriz de bytes.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplication_EncryptDocumentService` do objeto `invoke` e transmitindo o objeto `BLOB` que contém o documento PDF. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento criptografado por senha.
1. Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `MyApplicationEncryptDocumentService` do objeto `invoke`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `binaryData`.
1. Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

### Invocar um serviço usando classes proxy Java e codificação Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Você pode chamar um serviço AEM Forms usando classes proxy Java e Base64. Para chamar o serviço `MyApplication/EncryptDocument` usando classes proxy Java, execute as seguintes etapas:

1. Crie classes proxy Java usando JAX-WS que consome o serviço `MyApplication/EncryptDocument` WSDL. Use o seguinte terminal WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacote as classes proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo Java proxy JAR e os arquivos JAR localizados no seguinte caminho:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `MyApplicationEncryptDocumentService` do objeto `getEncryptDocument`.
1. Defina os valores de conexão necessários para chamar o AEM Forms atribuindo valores aos seguintes membros de dados:

   * Atribua o endpoint WSDL e o tipo de codificação ao campo `javax.xml.ws.BindingProvider` `ENDPOINT_ADDRESS_PROPERTY` do objeto. Para chamar o serviço `MyApplication/EncryptDocument` usando a codificação Base64, especifique o seguinte valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Atribua o usuário de formulários AEM ao campo `javax.xml.ws.BindingProvider` do objeto `USERNAME_PROPERTY`.
   * Atribua o valor da senha correspondente ao campo `javax.xml.ws.BindingProvider` `PASSWORD_PROPERTY` do objeto.

   O exemplo de código a seguir mostra esta lógica de aplicativo:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere o documento PDF para enviar ao processo `MyApplication/EncryptDocument` criando um objeto `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
1. Crie uma matriz de bytes e preencha-a com o conteúdo do objeto `java.io.FileInputStream`.
1. Crie um objeto `BLOB` usando seu construtor.
1. Preencha o objeto `BLOB` chamando seu método `setBinaryData` e transmitindo a matriz de bytes. O `BLOB` do objeto `setBinaryData` é o método a ser chamado ao usar a codificação Base64. Consulte Fornecimento de objetos BLOB em solicitações de serviço.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplicationEncryptDocument` do objeto `invoke`. Passe o objeto `BLOB` que contém o documento PDF. O método invoke retorna um objeto `BLOB` que contém o documento PDF criptografado.
1. Crie uma matriz de bytes que contenha o documento PDF criptografado chamando o método `BLOB` do objeto `getBinaryData`.
1. Salve o documento PDF criptografado como um arquivo PDF. Grave a matriz de bytes em um arquivo.

**Consulte também:**

[Start rápido: Invocar um serviço usando arquivos proxy Java e codificação Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Criação de um assembly de cliente .NET que usa a codificação Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Invocando o AEM Forms usando MTOM {#invoking-aem-forms-using-mtom}

Você pode chamar os serviços da AEM Forms usando o MTOM padrão do serviço da Web. Esse padrão define como os dados binários, como um documento PDF, são transmitidos pela Internet ou pela intranet. Um recurso do MTOM é o uso do elemento `XOP:Include`. Esse elemento é definido na especificação XML Binary Otimized Packaging (XOP) para fazer referência aos anexos binários de uma mensagem SOAP.

A discussão aqui é sobre o uso do MTOM para chamar o seguinte processo AEM Forms de curta duração chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

>[!NOTE]
>
>O suporte MTOM foi adicionado ao AEM Forms, versão 9.

>[!NOTE]
>
>Os aplicativos baseados no JAX WS que usam o protocolo de transmissão MTOM estão limitados a 25 MB de dados enviados e recebidos. Essa limitação se deve a um erro no JAX-WS. Se o tamanho combinado dos arquivos enviados e recebidos exceder 25 MB, use o protocolo de transmissão SwaRef em vez do MTOM. Caso contrário, há a possibilidade de uma exceção `OutOfMemory`.

A discussão aqui é sobre o uso do MTOM em um projeto do Microsoft .NET para chamar os serviços do AEM Forms. A estrutura .NET usada é 3.5, e o ambiente de desenvolvimento é Visual Studio 2008. Se você tiver o WSE (Web Service Enhancements - Melhorias do serviço Web) instalado no seu computador de desenvolvimento, remova-o. A estrutura .NET 3.5 suporta uma estrutura SOAP chamada Windows Communication Foundation (WCF). Ao invocar o AEM Forms usando o MTOM, somente o WCF (não o WSE) é suportado.

### Criando um projeto .NET que chama um serviço usando MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Você pode criar um projeto do Microsoft .NET que possa chamar um serviço do AEM Forms usando serviços da Web. Primeiro, crie um projeto do Microsoft .NET usando o Visual Studio 2008. Para chamar um serviço AEM Forms, crie uma Referência de serviço para o serviço AEM Forms que você deseja chamar dentro do projeto. Ao criar uma Referência de serviço, especifique um URL para o serviço AEM Forms:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Substitua `localhost` pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms. Substitua `MyApplication/EncryptDocument` pelo nome do serviço AEM Forms a ser chamado. Por exemplo, para chamar uma operação de Rights Management, especifique:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

A opção `lc_version` garante que a funcionalidade AEM Forms, como MTOM, esteja disponível. Sem especificar a opção `lc_version`, não é possível chamar o AEM Forms usando o MTOM.

Depois de criar uma Referência de serviço, os tipos de dados associados ao serviço AEM Forms estão disponíveis para uso no seu projeto .NET. Para criar um projeto .NET que chame um serviço AEM Forms, execute as seguintes etapas:

1. Crie um projeto .NET usando o Microsoft Visual Studio 2008.
1. No menu **Project**, selecione **Adicionar Referência de Serviço**.
1. Na caixa de diálogo **Endereço**, especifique o WSDL para o serviço AEM Forms. Por exemplo,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Clique em **Ir** e, em seguida, clique em **OK**.

### Invocar um serviço usando MTOM em um projeto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Considere o processo `MyApplication/EncryptDocument` que aceita um documento PDF não protegido e retorna um documento PDF criptografado por senha. Para invocar o processo `MyApplication/EncryptDocument` (que foi criado no Workbench) usando o MTOM, execute as seguintes etapas:

1. Crie um projeto do Microsoft .NET.
1. Crie um objeto `MyApplication_EncryptDocumentClient` usando seu construtor padrão.
1. Crie um objeto `MyApplication_EncryptDocumentClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms e o tipo de codificação:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom`.

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do membro de dados `EncryptDocumentClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
1. Defina o membro de dados `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
1. Ative a autenticação HTTP básica executando as seguintes tarefas:

   * Atribua o nome de usuário dos formulários AEM ao membro de dados `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Atribua o valor da senha correspondente ao membro de dados `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Atribua o valor constante `HttpClientCredentialType.Basic` ao membro de dados `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao membro de dados `BasicHttpBindingSecurity.Security.Mode`.

   O exemplo de código a seguir mostra essas tarefas.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF para passar para o processo `MyApplication/EncryptDocument`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
1. Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
1. Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
1. Preencha o objeto `BLOB` atribuindo seu membro de dados `MTOM` ao conteúdo da matriz de bytes.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplication_EncryptDocumentClient` do objeto `invoke`. Passe o objeto `BLOB` que contém o documento PDF. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido.
1. Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` que foi retornado pelo método `invoke`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
1. Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

>[!NOTE]
>
>A maioria das operações de serviço AEM Forms tem um start rápido MTOM. Você pode visualização esses start rápidos na seção de start rápido correspondente de um serviço. Por exemplo, para ver a seção start rápido de Saída, consulte [Start rápidos da API de serviço de saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte também:**

[Start rápido: Invocar um serviço usando MTOM em um projeto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Acessar vários serviços usando serviços da Web](#accessing-multiple-services-using-web-services)

[Criação de um aplicativo da Web ASP.NET que chama um processo de vida longa centrado em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Invocando o AEM Forms usando SwaRef {#invoking-aem-forms-using-swaref}

Você pode chamar os serviços da AEM Forms usando SwaRef. O conteúdo do elemento XML `wsi:swaRef` é enviado como um anexo dentro de um corpo SOAP que armazena a referência ao anexo. Ao chamar um serviço Forms usando SwaRef, crie classes proxy Java usando a API Java para serviços da Web XML (JAX-WS). (Consulte [API Java para XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

A discussão aqui é sobre invocar o seguinte processo Forms de curta duração chamado `MyApplication/EncryptDocument` usando SwaRef.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

>[!NOTE]
>
>Suporte a SwaRef adicionado ao AEM Forms

A discussão abaixo é sobre como chamar os serviços da Forms usando SwaRef em um aplicativo cliente Java. O aplicativo Java usa classes proxy criadas usando JAX-WS.

### Chame um serviço usando arquivos da biblioteca JAX-WS que usam SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Para invocar o processo `MyApplication/EncryptDocument` usando arquivos proxy Java criados usando JAX-WS e SwaRef, execute as seguintes etapas:

1. Crie classes proxy Java usando JAX-WS que consome o serviço `MyApplication/EncryptDocument` WSDL. Use o seguinte terminal WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obter informações, consulte [Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacote as classes proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo Java proxy JAR e os arquivos JAR localizados no seguinte caminho:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `MyApplicationEncryptDocumentService` do objeto `getEncryptDocument`.
1. Defina os valores de conexão necessários para chamar o AEM Forms atribuindo valores aos seguintes membros de dados:

   * Atribua o endpoint WSDL e o tipo de codificação ao campo `javax.xml.ws.BindingProvider` `ENDPOINT_ADDRESS_PROPERTY` do objeto. Para chamar o serviço `MyApplication/EncryptDocument` usando a codificação SwaRef, especifique o seguinte valor de URL:

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Atribua o usuário de formulários AEM ao campo `javax.xml.ws.BindingProvider` do objeto `USERNAME_PROPERTY`.
   * Atribua o valor da senha correspondente ao campo `javax.xml.ws.BindingProvider` `PASSWORD_PROPERTY` do objeto.

   O exemplo de código a seguir mostra esta lógica de aplicativo:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere o documento PDF para enviar ao processo `MyApplication/EncryptDocument` criando um objeto `java.io.File` usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
1. Crie um objeto `javax.activation.DataSource` usando o construtor `FileDataSource`. Passe o objeto `java.io.File`.
1. Crie um objeto `javax.activation.DataHandler` usando seu construtor e transmitindo o objeto `javax.activation.DataSource`.
1. Crie um objeto `BLOB` usando seu construtor.
1. Preencha o objeto `BLOB` chamando seu método `setSwaRef` e transmitindo o objeto `javax.activation.DataHandler`.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplicationEncryptDocument` do objeto `invoke` e transmitindo o objeto `BLOB` que contém o documento PDF. O método invoke retorna um objeto `BLOB` que contém um documento PDF criptografado.
1. Preencha um objeto `javax.activation.DataHandler` chamando o método `BLOB` do objeto `getSwaRef`.
1. Converta o objeto `javax.activation.DataHandler` em uma instância `java.io.InputSteam` invocando o método `javax.activation.DataHandler` do objeto `getInputStream`.
1. Grave a instância `java.io.InputSteam` em um arquivo PDF que representa o documento PDF criptografado.

>[!NOTE]
>
>A maioria das operações de serviço da AEM Forms tem um start rápido SwaRef. Você pode visualização esses start rápidos na seção de start rápido correspondente de um serviço. Por exemplo, para ver a seção start rápido de Saída, consulte [Start rápidos da API de serviço de saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte também:**

[Start rápido: Invocar um serviço usando SwaRef em um projeto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Invocar o AEM Forms usando dados BLOB em HTTP {#invoking-aem-forms-using-blob-data-over-http}

Você pode chamar os serviços da AEM Forms usando os serviços da Web e passar dados BLOB por HTTP. Passar dados BLOB por HTTP é uma técnica alternativa em vez de usar codificação base64, DIME ou MIME. Por exemplo, você pode passar dados por HTTP em um projeto do Microsoft .NET que usa o Web Service Enhanced 3.0, que não é compatível com DIME ou MIME. Ao usar dados BLOB em HTTP, os dados de entrada são carregados antes que o serviço AEM Forms seja chamado.

&quot;Invocar o AEM Forms usando dados BLOB sobre HTTP&quot; discute invocar o seguinte processo AEM Forms de curta duração chamado `MyApplication/EncryptDocument` transmitindo dados BLOB sobre HTTP.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

>[!NOTE]
>
>É recomendável que você esteja familiarizado com Chamar a AEM Forms usando SOAP. (Consulte [Invocar o AEM Forms usando os Serviços Web](#invoking-aem-forms-using-web-services).)

### Criando um assembly de cliente .NET que usa dados via HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Para criar um assembly de cliente que use dados via HTTP, siga o processo especificado em [Invocando o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding). No entanto, altere o URL na classe proxy para incluir `?blob=http` em vez de `?blob=base64`. Essa ação garante que os dados sejam transmitidos por HTTP. Na classe proxy, localize a seguinte linha de código:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

e alterá-lo para:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Referência ao assembly .NET clienMyApplication/EncryptDocumentt**

Coloque seu novo assembly de cliente .NET no computador onde você está desenvolvendo seu aplicativo cliente. Depois de colocar o assembly do cliente .NET em um diretório, você pode referenciá-lo a partir de um projeto. Faça referência à biblioteca `System.Web.Services` do seu projeto. Se você não fizer referência a esta biblioteca, não poderá usar o assembly do cliente .NET para chamar um serviço.

1. No menu **Project**, selecione **Adicionar referência**.
1. Clique na guia **.NET**.
1. Clique em **Procurar** e localize o arquivo DocumentService.dll.
1. Clique em **Selecione** e clique em **OK**.

**Invocar um serviço usando um assembly de cliente .NET que usa dados BLOB em HTTP**

Você pode chamar o serviço `MyApplication/EncryptDocument` (que foi criado no Workbench) usando um assembly de cliente .NET que usa dados via HTTP. Para chamar o serviço `MyApplication/EncryptDocument`, execute as seguintes etapas:

1. Crie o assembly do cliente .NET.
1. Faça referência ao assembly do cliente Microsoft .NET. Crie um projeto cliente do Microsoft .NET. Faça referência ao assembly do cliente Microsoft .NET no projeto do cliente. Consulte também `System.Web.Services`.
1. Usando o assembly do cliente Microsoft .NET, crie um objeto `MyApplication_EncryptDocumentService` chamando seu construtor padrão.
1. Defina a propriedade `MyApplication_EncryptDocumentService` do objeto `Credentials` com um objeto `System.Net.NetworkCredential`. No construtor `System.Net.NetworkCredential`, especifique um nome de usuário para formulários AEM e a senha correspondente. Defina valores de autenticação para permitir que seu aplicativo cliente .NET troque mensagens SOAP com êxito com o AEM Forms.
1. Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para transmitir dados para o processo `MyApplication/EncryptDocument`.
1. Atribua um valor de string ao membro de dados `BLOB` do objeto `remoteURL` que especifica o local de URI de um documento PDF a ser transmitido para o serviço `MyApplication/EncryptDocument`.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplication_EncryptDocumentService` do objeto `invoke` e transmitindo o objeto `BLOB`. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Crie um objeto `System.UriBuilder` usando seu construtor e transmitindo o valor do membro de dados `BLOB` do objeto `remoteURL` retornado.
1. Converta o objeto `System.UriBuilder` em um objeto `System.IO.Stream`. (O Start rápido C# que segue esta lista ilustra como executar esta tarefa.)
1. Crie uma matriz de bytes e preencha-a com os dados localizados no objeto `System.IO.Stream`.
1. Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

### Invocar um serviço usando classes proxy Java e dados BLOB por HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Você pode chamar um serviço AEM Forms usando classes proxy Java e dados BLOB por HTTP. Para chamar o serviço `MyApplication/EncryptDocument` usando classes proxy Java, execute as seguintes etapas:

1. Crie classes proxy Java usando JAX-WS que consome o serviço `MyApplication/EncryptDocument` WSDL. Use o seguinte terminal WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obter informações, consulte [Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacote as classes proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo Java proxy JAR e os arquivos JAR localizados no seguinte caminho:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `MyApplicationEncryptDocumentService` do objeto `getEncryptDocument`.
1. Defina os valores de conexão necessários para chamar o AEM Forms atribuindo valores aos seguintes membros de dados:

   * Atribua o endpoint WSDL e o tipo de codificação ao campo `javax.xml.ws.BindingProvider` `ENDPOINT_ADDRESS_PROPERTY` do objeto. Para chamar o serviço `MyApplication/EncryptDocument` usando a codificação BLOB sobre HTTP, especifique o seguinte valor de URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Atribua o usuário de formulários AEM ao campo `javax.xml.ws.BindingProvider` do objeto `USERNAME_PROPERTY`.
   * Atribua o valor da senha correspondente ao campo `javax.xml.ws.BindingProvider` `PASSWORD_PROPERTY` do objeto.

   O exemplo de código a seguir mostra esta lógica de aplicativo:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Crie um objeto `BLOB` usando seu construtor.
1. Preencha o objeto `BLOB` chamando seu método `setRemoteURL`. Passe um valor de string que especifica o local de URI de um documento PDF a ser enviado para o serviço `MyApplication/EncryptDocument`.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `MyApplicationEncryptDocument` do objeto `invoke` e transmitindo o objeto `BLOB` que contém o documento PDF. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Crie uma matriz de bytes para armazenar o fluxo de dados que representa o documento PDF criptografado. Chame o método `BLOB` do objeto `getRemoteURL` (use o objeto `BLOB` retornado pelo método `invoke`).
1. Crie um objeto `java.io.File` usando seu construtor. Esse objeto representa o documento PDF criptografado.
1. Crie um objeto `java.io.FileOutputStream` usando seu construtor e transmitindo o objeto `java.io.File`.
1. Chame o método `java.io.FileOutputStream` do objeto `write`. Passe a matriz de bytes que contém o fluxo de dados que representa o documento PDF criptografado.

## Invocando o AEM Forms usando DIME {#invoking-aem-forms-using-dime}

Você pode chamar os serviços AEM Forms usando SOAP com anexos. A AEM Forms suporta os padrões de serviço da Web MIME e DIME. O DIME permite que você envie anexos binários, como documentos PDF, juntamente com solicitações de invocação em vez de codificar o anexo. A seção *Invocar o AEM Forms usando DIME* discute a invocação do seguinte processo AEM Forms de curta duração chamado `MyApplication/EncryptDocument` usando DIME.

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

Esse processo não se baseia em um processo AEM Forms existente. Para seguir com os exemplos de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>Invocar operações de serviço AEM Forms usando DIME está obsoleto. Recomenda-se usar MTOM. (Consulte [Invocar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)

### Criação de um projeto .NET que usa DIME {#creating-a-net-project-that-uses-dime}

Para criar um projeto .NET que possa chamar um serviço Forms usando DIME, execute as seguintes tarefas:

* Instale os Aprimoramentos 2.0 dos Serviços Web no seu computador de desenvolvimento.
* Em seu projeto .NET, crie uma referência da Web para o serviço FormsAEM Forms.

**Instalação das melhorias de serviços da Web 2.0**

Instale os Aprimoramentos 2.0 dos Serviços Web no seu computador de desenvolvimento e integre-os ao Microsoft Visual Studio .NET. Você pode baixar os Aprimoramentos 2.0 dos Serviços Web do [Centro de Download da Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Nesta página da Web, procure por Aprimoramentos de serviços da Web 2.0 e baixe-os no seu computador de desenvolvimento. Este download coloca um arquivo chamado Microsoft WSE 2.0 SPI.msi em seu computador. Execute o programa de instalação e siga as instruções on-line.

>[!NOTE]
>
>Os Aprimoramentos de serviços da Web 2.0 são compatíveis com DIME. A versão compatível do Microsoft Visual Studio é 2003 ao trabalhar com os Aprimoramentos de Serviços Web 2.0. Os Aprimoramentos de serviços da Web 3.0 não são compatíveis com DIME; no entanto, ele suporta MTOM.

**Criação de uma referência da Web para um serviço AEM Forms**

Depois de instalar o Web Services Enhancements 2.0 no computador de desenvolvimento e criar um projeto do Microsoft .NET, crie uma referência da Web para o serviço Forms. Por exemplo, para criar uma referência da Web para o processo `MyApplication/EncryptDocument` e supondo que o Forms esteja instalado no computador local, especifique o seguinte URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Depois de criar uma referência da Web, os dois tipos de dados proxy a seguir estão disponíveis para você usar em seu projeto .NET: `EncryptDocumentService` e `EncryptDocumentServiceWse`. Para chamar o processo `MyApplication/EncryptDocument` usando DIME, use o tipo `EncryptDocumentServiceWse`.

>[!NOTE]
>
>Antes de criar uma referência da Web para o serviço Forms, certifique-se de fazer referência aos Aprimoramentos de Serviços da Web 2.0 em seu projeto. (Consulte &quot;Instalando melhorias de serviços da Web 2.0&quot;.)

**Referência à biblioteca WSE**

1. No menu Projeto, selecione Adicionar referência.
1. Na caixa de diálogo Adicionar referência, selecione Microsoft.Web.Services2.dll.
1. Selecione System.Web.Services.dll.
1. Clique em Selecionar e em OK.

**Criar uma referência da Web para um serviço Forms**

1. No menu Projeto, selecione Adicionar referência da Web.
1. Na caixa de diálogo URL, especifique o URL para o serviço Forms.
1. Clique em Ir e em Adicionar referência.

>[!NOTE]
>
>Certifique-se de ativar seu projeto .NET para usar a biblioteca WSE. No Explorador de projetos, clique com o botão direito do mouse no nome do projeto e selecione Ativar WSE 2.0. Verifique se a caixa de seleção na caixa de diálogo exibida está selecionada.

**Invocar um serviço usando DIME em um projeto .NET**

Você pode chamar um serviço Forms usando DIME. Considere o processo `MyApplication/EncryptDocument` que aceita um documento PDF não protegido e retorna um documento PDF criptografado por senha. Para chamar o processo `MyApplication/EncryptDocument` usando DIME, execute as seguintes etapas:

1. Crie um projeto do Microsoft .NET que permita chamar um serviço Forms usando DIME. Certifique-se de incluir os Aprimoramentos de serviços da Web 2.0 e criar uma referência da Web para o serviço AEM Forms.
1. Depois de definir uma referência da Web para o processo `MyApplication/EncryptDocument`, crie um objeto `EncryptDocumentServiceWse` usando seu construtor padrão.
1. Defina o membro de dados `EncryptDocumentServiceWse` do objeto `Credentials` com um valor `System.Net.NetworkCredential` que especifique o valor de nome de usuário e senha dos formulários AEM.
1. Crie um objeto `Microsoft.Web.Services2.Dime.DimeAttachment` usando seu construtor e transmitindo os seguintes valores:

   * Um valor de string que especifica um valor GUID. Você pode obter um valor GUID chamando o método `System.Guid.NewGuid.ToString`.
   * Um valor de string que especifica o tipo de conteúdo. Como esse processo requer um documento PDF, especifique `application/pdf`.
   * Um valor de lista discriminada `TypeFormat`. Especifique `TypeFormat.MediaType`.
   * Um valor de string que especifica o local do documento PDF a ser passado para o processo AEM Forms.

1. Crie um objeto `BLOB` usando seu construtor.
1. Adicione o anexo DIME ao objeto `BLOB` atribuindo o valor `Microsoft.Web.Services2.Dime.DimeAttachment` do membro de dados `Id` do objeto ao membro de dados `BLOB` do objeto `attachmentID`.
1. Chame o método `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` e passe o objeto `Microsoft.Web.Services2.Dime.DimeAttachment`.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `EncryptDocumentServiceWse` do objeto `invoke` e transmitindo o objeto `BLOB` que contém o anexo DIME. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Obtenha o valor do identificador de anexo obtendo o valor do membro de dados `BLOB` do objeto `attachmentID` retornado.
1. Itere pelos anexos localizados em `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` e use o valor do identificador do anexo para obter o documento PDF criptografado.
1. Obtenha um objeto `System.IO.Stream` obtendo o valor do membro de dados `Attachment` do objeto `Stream`.
1. Crie uma matriz de bytes e passe essa matriz de bytes para o método `System.IO.Stream` do objeto `Read`. Esse método preenche a matriz de bytes com um fluxo de dados que representa o documento PDF criptografado.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo PDF. Esse objeto representa o documento PDF criptografado.
1. Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes no arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

### Criando classes proxy Java do Apache Axis que usam DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Você pode usar a ferramenta Apache Axis WSDL2Java para converter um serviço WSDL em classes proxy Java, para que você possa chamar operações de serviço. Usando o Apache Ant, você pode gerar arquivos de biblioteca do Axis a partir de um WSDL de serviço da AEM Forms que permite chamar o serviço. (Consulte [Criar classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

A ferramenta Apache Axis WSDL2Java gera arquivos JAVA que contêm métodos usados para enviar solicitações SOAP a um serviço. As solicitações SOAP recebidas por um serviço são decodificadas pelas bibliotecas geradas pelo Axis e retornadas aos métodos e argumentos.

Para chamar o serviço `MyApplication/EncryptDocument` (que foi criado no Workbench) usando arquivos de biblioteca gerados pelo Axis e DIME, execute as seguintes etapas:

1. Crie classes proxy Java que consomem o serviço `MyApplication/EncryptDocument` WSDL usando o Apache Axis. (Consulte [Criar classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)
1. Inclua as classes proxy Java no caminho da classe.
1. Crie um objeto `MyApplicationEncryptDocumentServiceLocator` usando seu construtor.
1. Crie um objeto `URL` usando seu construtor e transmitindo um valor de string que especifica a definição WSDL do serviço AEM Forms. Certifique-se de especificar `?blob=dime` no final do URL do ponto de extremidade SOAP. Por exemplo, use

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Crie um objeto `EncryptDocumentSoapBindingStub` chamando seu construtor e transmitindo o objeto `MyApplicationEncryptDocumentServiceLocator`e o objeto `URL`.
1. Defina o valor de nome de usuário e senha dos formulários AEM chamando os métodos `EncryptDocumentSoapBindingStub` e `setPassword` do objeto.`setUsername`

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recupere o documento PDF para enviar ao serviço `MyApplication/EncryptDocument` criando um objeto `java.io.File`. Passe um valor de string que especifica o local do documento PDF.
1. Crie um objeto `javax.activation.DataHandler` usando seu construtor e transmitindo um objeto `javax.activation.FileDataSource`. O objeto `javax.activation.FileDataSource` pode ser criado usando seu construtor e transmitindo o objeto `java.io.File` que representa o documento PDF.
1. Crie um objeto `org.apache.axis.attachments.AttachmentPart` usando seu construtor e transmitindo o objeto `javax.activation.DataHandler`.
1. Anexe o anexo chamando o método `EncryptDocumentSoapBindingStub` do objeto `addAttachment` e transmitindo o objeto `org.apache.axis.attachments.AttachmentPart`.
1. Crie um objeto `BLOB` usando seu construtor. Preencha o objeto `BLOB` com o valor do identificador de anexo chamando o método `BLOB` do objeto `setAttachmentID` e transmitindo o valor do identificador de anexo. Esse valor pode ser obtido chamando o método `org.apache.axis.attachments.AttachmentPart` do objeto `getContentId`.
1. Chame o processo `MyApplication/EncryptDocument` invocando o método `EncryptDocumentSoapBindingStub` do objeto `invoke`. Passe o objeto `BLOB` que contém o anexo DIME. Esse processo retorna um documento PDF criptografado dentro de um objeto `BLOB`.
1. Obtenha o valor do identificador de anexo chamando o método `BLOB` do objeto `getAttachmentID` retornado. Esse método retorna um valor de string que representa o valor identificador do anexo retornado.
1. Recupere os anexos chamando o método `EncryptDocumentSoapBindingStub` do objeto `getAttachments`. Este método retorna uma matriz de `Objects` que representa os anexos.
1. Iterar pelos anexos (a matriz `Object`) e usar o valor do identificador do anexo para obter o documento PDF criptografado. Cada elemento é um objeto `org.apache.axis.attachments.AttachmentPart`.
1. Obtenha o objeto `javax.activation.DataHandler` associado ao anexo chamando o método `org.apache.axis.attachments.AttachmentPart` `getDataHandler` do objeto.
1. Obtenha um objeto `java.io.FileStream` chamando o método `javax.activation.DataHandler` do objeto `getInputStream`.
1. Crie uma matriz de bytes e passe essa matriz de bytes para o método `java.io.FileStream` do objeto `read`. Esse método preenche a matriz de bytes com um fluxo de dados que representa o documento PDF criptografado.
1. Crie um objeto `java.io.File` usando seu construtor. Esse objeto representa o documento PDF criptografado.
1. Crie um objeto `java.io.FileOutputStream` usando seu construtor e transmitindo o objeto `java.io.File`.
1. Chame o método `java.io.FileOutputStream` do objeto `write` e passe a matriz de bytes que contém o fluxo de dados que representa o documento PDF criptografado.

**Consulte também:**

[Start rápido: Invocar um serviço usando DIME em um projeto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Uso da autenticação baseada em SAML {#using-saml-based-authentication}

A AEM Forms suporta vários modos de autenticação de serviço da Web ao invocar serviços. Um modo de autenticação está especificando um valor de nome de usuário e senha usando um cabeçalho de autorização básico na chamada de serviço da Web. A AEM Forms também oferece suporte à autenticação baseada em asserção SAML. Quando um aplicativo cliente chama um serviço da AEM Forms usando um serviço da Web, o aplicativo cliente pode fornecer informações de autenticação de uma das seguintes maneiras:

* Concessão de credenciais como parte da autorização básica
* Enviar token de nome de usuário como parte do cabeçalho WS-Security
* Transmissão de uma asserção SAML como parte do cabeçalho WS-Security
* Transmissão do token Kerberos como parte do cabeçalho WS-Security

A AEM Forms não oferece suporte à autenticação baseada em certificado padrão, mas oferece suporte à autenticação baseada em certificado em um formulário diferente.

>[!NOTE]
>
>Os start rápidos do serviço da Web em Programação com a AEM Forms especificam os valores de nome de usuário e senha para executar a autorização.

A identidade dos usuários AEM formulários pode ser representada por meio de uma asserção SAML assinada usando uma chave secreta. O código XML a seguir mostra um exemplo de uma asserção SAML.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Esta afirmação de exemplo é emitida para um usuário administrador. Esta asserção contém os seguintes itens visíveis:

* É válido por uma determinada duração.
* É emitido para um usuário específico.
* Está assinado digitalmente. Então qualquer modificação feita a ela quebraria a assinatura.
* Ele pode ser apresentado à AEM Forms como um token de identidade do usuário semelhante ao nome de usuário e senha.

Um aplicativo cliente pode recuperar a asserção de qualquer API do AEM Forms AuthenticationManager que retorna um objeto `AuthResult`. Você pode obter uma instância `AuthResult` executando um dos dois métodos a seguir:

* Autenticação do usuário usando qualquer um dos métodos de autenticação expostos pela API do AuthenticationManager. Normalmente, se usa o nome de usuário e a senha; no entanto, você também pode usar a autenticação de certificado.
* Usando o método `AuthenticationManager.getAuthResultOnBehalfOfUser`. Esse método permite que um aplicativo cliente obtenha um objeto `AuthResult` para qualquer usuário de formulários AEM.

um usuário de formulários AEM pode ser autenticado usando um token SAML obtido. Essa asserção SAML (fragmento xml) pode ser enviada como parte do cabeçalho WS-Security com a chamada de serviço da Web para autenticação do usuário. Geralmente, um aplicativo cliente autentica um usuário, mas não armazenou as credenciais do usuário. (Ou o usuário fez logon nesse cliente por meio de um mecanismo diferente de usar um nome de usuário e senha.) Nessa situação, o aplicativo cliente deve chamar o AEM Forms e representar um usuário específico que tem permissão para chamar o AEM Forms.

Para representar um usuário específico, chame o método `AuthenticationManager.getAuthResultOnBehalfOfUser` usando um serviço da Web. Este método retorna uma instância `AuthResult` que contém a asserção SAML para esse usuário.

Em seguida, use essa asserção SAML para chamar qualquer serviço que exija autenticação. Essa ação envolve enviar a asserção como parte do cabeçalho SOAP. Quando uma chamada de serviço da Web é feita com essa asserção, a AEM Forms identifica o usuário como aquele representado por essa asserção. Ou seja, o usuário especificado na asserção é o usuário que está chamando o serviço.

### Uso de classes Apache Axis e autenticação baseada em SAML {#using-apache-axis-classes-and-saml-based-authentication}

Você pode chamar um serviço AEM Forms por classes proxy Java que foram criadas usando a biblioteca Axis. (Consulte [Criar classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

Ao usar o AXIS que usa a autenticação baseada em SAML, registre o manipulador de solicitação e resposta no Axis. O Apache Axis chama o manipulador antes de enviar uma solicitação de invocação para a AEM Forms. Para registrar um manipulador, crie uma classe Java que estenda `org.apache.axis.handlers.BasicHandler`.

**Criar um AssertionHandler com Eixo**

A classe Java a seguir, chamada `AssertionHandler.java`, mostra um exemplo de uma classe Java que estende `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registrar o manipulador**

Para registrar um manipulador no Axis, crie um arquivo client-config.wsdd. Por padrão, o Axis procura um arquivo com esse nome. O código XML a seguir é um exemplo de um arquivo client-config.wsdd. Consulte a documentação do Eixo para obter mais informações.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Chamar um serviço AEM Forms**

O exemplo de código a seguir chama um serviço AEM Forms usando autenticação baseada em SAML.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Uso de um assembly de cliente .NET e autenticação baseada em SAML {#using-a-net-client-assembly-and-saml-based-authentication}

Você pode chamar um serviço Forms usando um assembly de cliente .NET e autenticação baseada em SAML. Para fazer isso, você deve usar o WSE (Web Service Enhancements 3.0). Para obter informações sobre como criar um assembly de cliente .NET que usa WSE, consulte [Criar um projeto .NET que usa DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>A seção DIME usa WSE 2.0. Para usar a autenticação baseada em SAML, siga as mesmas instruções especificadas no tópico DIME. Entretanto, substitua WSE 2.0 por WSE 3.0. Instale os Aprimoramentos do Web Services 3.0 no seu computador de desenvolvimento e integre-os ao Microsoft Visual Studio .NET. Você pode baixar os Aprimoramentos de serviços da Web 3.0 do [Centro de downloads da Microsoft](https://www.microsoft.com/downloads/search.aspx).

A arquitetura WSE usa tipos de dados Políticas, Asserções e SecurityToken. Resumidamente, para uma chamada de serviço da Web, especifique uma política. Uma política pode ter várias asserções. Cada asserção pode conter filtros. Um filtro é chamado em determinados estágios em uma chamada de serviço da Web e, nesse momento, ele pode modificar a solicitação SOAP. Para obter detalhes completos, consulte a documentação Aprimoramentos do serviço da Web 3.0.

**Criar a asserção e o filtro**

O exemplo de código C# a seguir cria classes de filtro e asserção. Este exemplo de código cria um SamlAssertionOutputFilter. Esse filtro é chamado pela estrutura WSE antes de a solicitação SOAP ser enviada para a AEM Forms.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Criar o token SAML**

Crie uma classe para representar a asserção SAML. A tarefa principal que essa classe executa é converter valores de dados de uma string para xml e preservar o espaço em branco. Esse xml de asserção é importado posteriormente para a solicitação SOAP.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Chamar um serviço AEM Forms**

O exemplo de código C# a seguir chama um serviço Forms usando autenticação baseada em SAML.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Considerações relacionadas ao usar serviços da Web {#related-considerations-when-using-web-services}

Às vezes, ocorrem problemas ao invocar determinadas operações de serviços da AEM Forms usando serviços da Web. O objetivo desta discussão é identificar essas questões e fornecer uma solução, se disponível.

### Invocando operações de serviço de forma assíncrona {#invoking-service-operations-asynchronously}

Se você tentar chamar de forma assíncrona uma operação de serviço AEM Forms, como a operação `htmlToPDF` de Gerar PDF, ocorrerá um `SoapFaultException`. Para resolver esse problema, crie um arquivo XML de vínculo personalizado que mapeie o elemento `ExportPDF_Result` e outros elementos em classes diferentes. O XML a seguir representa um arquivo de vínculo personalizado.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Use esse arquivo XML ao criar arquivos proxy Java usando JAX-WS. (Consulte [Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Consulte esse arquivo XML ao executar a ferramenta JAX-WS (wsimport.exe) usando a opção de linha de comando - `b`. Atualize o elemento `wsdlLocation` no arquivo XML de vínculo para especificar o URL do AEM Forms.

Para garantir que a invocação assíncrona funcione, modifique o valor do URL do ponto final e especifique `async=true`. Por exemplo, para arquivos proxy Java criados com JAX-WS, especifique o seguinte para `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

A lista a seguir especifica outros serviços que precisam de um arquivo de vínculo personalizado quando chamados de forma assíncrona:

* PDFG3D
* Gerenciador de tarefas
* Gerenciador de aplicativos
* Gerenciador de diretório
* Distiller
* Rights Management
* Gerenciamento de documentos

### Diferenças nos servidores de aplicativos J2EE {#differences-in-j2ee-application-servers}

Às vezes, uma biblioteca proxy criada usando um servidor de aplicativos J2EE específico não chama com êxito o AEM Forms hospedado em um servidor de aplicativos J2EE diferente. Considere uma biblioteca de proxy gerada usando o AEM Forms que é implantada no WebSphere. Esta biblioteca proxy não consegue invocar com êxito os serviços AEM Forms que estão implementados no Servidor de Aplicações JBoss.

Alguns tipos de dados complexos da AEM Forms, como `PrincipalReference`, são definidos de forma diferente quando a AEM Forms é implantada no WebSphere em comparação ao JBoss Application Server. As diferenças nos JDKs usados pelos diferentes serviços de aplicativos J2EE são a razão pela qual há diferenças nas definições de WSDL. Como resultado, use bibliotecas de proxy que são geradas do mesmo servidor de aplicativos J2EE.

### Acessar vários serviços usando serviços da Web {#accessing-multiple-services-using-web-services}

Devido a conflitos de namespace, objetos de dados não podem ser compartilhados entre vários WSDLs de serviço. Diferentes serviços podem compartilhar tipos de dados e, portanto, os serviços compartilham a definição desses tipos nas WSDLs. Por exemplo, não é possível adicionar dois assemblies cliente .NET que contêm um tipo de dados `BLOB` ao mesmo projeto cliente .NET. Se você tentar fazer isso, ocorrerá um erro de compilação.

A lista a seguir especifica tipos de dados que não podem ser compartilhados entre vários WSDLs de serviço:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Para evitar esse problema, é recomendável qualificar totalmente os tipos de dados. Por exemplo, considere um aplicativo .NET que faça referência ao serviço Forms e ao serviço de assinatura usando uma referência de serviço. Ambas as referências de serviço conterão uma classe `BLOB`. Para usar uma instância `BLOB`, qualifice totalmente o objeto `BLOB` ao declará-lo. Essa abordagem é mostrada no exemplo de código a seguir. Para obter informações sobre esse exemplo de código, consulte [Assinando digitalmente o Forms interativo](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

O exemplo de código C# a seguir assina um formulário interativo que é renderizado pelo serviço Forms. O aplicativo cliente tem duas referências de serviço. A instância `BLOB` associada ao serviço Forms pertence à namespace `SignInteractiveForm.ServiceReference2`. Da mesma forma, a instância `BLOB` associada ao serviço de assinatura pertence à namespace `SignInteractiveForm.ServiceReference1`. O formulário interativo assinado é salvo como um arquivo PDF chamado *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### Serviços que começam com a letra I produzem arquivos proxy inválidos {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

O nome de algumas classes proxy geradas pela AEM Forms está incorreto ao usar o Microsoft .Net 3.5 e o WCF. Esse problema ocorre quando as classes proxy são criadas para o IBMFilenetContentRepositoryConnector, IDPSchedulerService ou qualquer outro serviço cujo nome start com a letra I. Por exemplo, o nome do cliente gerado no caso de IBMFileNetContentRepositoryConnector é `BMFileNetContentRepositoryConnectorClient`. A letra em que estou ausente na classe proxy gerada.

