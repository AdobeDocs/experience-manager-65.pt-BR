---
title: Chamar o AEM Forms usando serviços da Web
description: Chame processos AEM Forms usando serviços da Web com suporte total para geração de WSDL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '9814'
ht-degree: 0%

---

# Chamar o AEM Forms usando serviços da Web {#invoking-aem-forms-using-web-services}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

A maioria dos serviços da AEM Forms no contêiner de serviço é configurada para expor um serviço Web, com suporte total para a geração de WSDL (linguagem de definição de serviço Web). Ou seja, você pode criar objetos proxy que consomem a pilha nativa de SOAP de um serviço do AEM Forms. Como resultado, os serviços da AEM Forms podem trocar e processar as seguintes mensagens SOAP:

* **Solicitação de SOAP**: enviada a um serviço Forms por um aplicativo cliente solicitando uma ação.
* **Resposta do SOAP**: enviada para um aplicativo cliente por um serviço do Forms após o processamento de uma solicitação do SOAP.

Com os serviços da Web, você pode executar as mesmas operações dos serviços da AEM Forms que pode usando a API do Java. Um benefício de usar serviços da Web para chamar serviços da AEM Forms é que você pode criar um aplicativo cliente em um ambiente de desenvolvimento que ofereça suporte ao SOAP. Um aplicativo cliente não está vinculado a um ambiente de desenvolvimento ou linguagem de programação específica. Por exemplo, você pode criar um aplicativo cliente usando o Microsoft Visual Studio .NET e C# como a linguagem de programação.

Os serviços da AEM Forms são expostos pelo protocolo SOAP e são compatíveis com o WSI Basic Profile 1.1. A Web Services Interoperability (WSI) é uma organização de padrões abertos que promove a interoperabilidade de serviços da Web entre plataformas. Para obter informações, consulte [https://www.ws-i.org/](https://www.ws-i.org).

O AEM Forms é compatível com os seguintes padrões de serviço da Web:

* **Codificação**: suporta apenas a codificação de documento e literal (que é a codificação preferida de acordo com o WSI Basic Profile). (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: representa uma maneira de codificar anexos com solicitações SOAP. (Consulte [Chamar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: representa outra maneira de codificar anexos com solicitações de SOAP. (Consulte [Invocar o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP com anexos**: suporta MIME e DIME (Direct Internet Message Encapsulation). Esses protocolos são maneiras padrão de enviar anexos por SOAP. Aplicativos Microsoft Visual Studio .NET usam DIME. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: oferece suporte a um perfil de token de senha de nome de usuário, que é uma maneira padrão de enviar nomes de usuário e senhas como parte do cabeçalho SOAP de Segurança do WS. O AEM Forms também oferece suporte à autenticação básica HTTP. s

Para chamar serviços AEM Forms usando um serviço da Web, normalmente você cria uma biblioteca de proxy que consome o serviço WSDL. A seção *Chamando o AEM Forms usando Serviços da Web* usa JAX-WS para criar classes de proxy Java para chamar serviços. (Consulte [Criação de classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Você pode recuperar um serviço WDSL especificando a seguinte definição de URL (os itens entre parênteses são opcionais):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

em que:

* *your_serverhost* representa o endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.
* *your_port* representa a porta HTTP que o servidor de aplicativos J2EE usa.
* *service_name* representa o nome do serviço.
* *version* representa a versão de destino de um serviço (a versão de serviço mais recente é usada por padrão).
* `async` especifica o valor `true` para habilitar operações adicionais para invocação assíncrona ( `false` por padrão).
* *lc_version* representa a versão do AEM Forms que você deseja invocar.

A tabela a seguir lista as definições de serviço WSDL (supondo que o AEM Forms esteja implantado no host local e a publicação seja 8080).

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
   <td><p>Voltar e Restaurar</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>formulários com código de barras</p></td>
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
   <td><p>ConversorDoc </p></td>
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
   <td><p>Extensões do Acrobat Reader DC</p></td>
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

**Definições WSDL de Processo do AEM Forms**

Especifique o nome do aplicativo e o nome do processo na definição WSDL para acessar um WSDL que pertence a um processo criado no Workbench. Suponha que o nome do aplicativo seja `MyApplication` e o nome do processo seja `EncryptDocument`. Nessa situação, especifique a seguinte definição WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Para obter informações sobre o exemplo `MyApplication/EncryptDocument` processo de vida curta, consulte [Exemplo de processo de vida curta](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Um aplicativo pode conter pasta(s). Nesse caso, especifique os nomes das pastas na definição WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Acessando nova funcionalidade usando serviços Web**

A nova funcionalidade do serviço AEM Forms pode ser acessada usando os serviços da Web. Por exemplo, no AEM Forms, é introduzida a capacidade de codificar anexos usando MTOM. (Consulte [Chamar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)

Para acessar a nova funcionalidade introduzida no AEM Forms, especifique o atributo `lc_version` na definição WSDL. Por exemplo, para acessar a nova funcionalidade de serviço (incluindo suporte a MTOM), especifique a seguinte definição WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Ao definir o atributo `lc_version`, certifique-se de usar três dígitos. Por exemplo, 9.0.1 é igual à versão 9.0.

**Tipo de dados BLOB do serviço Web**

Os WSDLs do serviço AEM Forms definem muitos tipos de dados. Um dos tipos de dados mais importantes expostos em um serviço Web é um tipo `BLOB`. Esse tipo de dados mapeia para a classe `com.adobe.idp.Document` ao trabalhar com APIs Java da AEM Forms. (Consulte [Passando dados para serviços da AEM Forms usando a API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Um objeto `BLOB` envia e recupera dados binários (por exemplo, arquivos PDF, dados XML e assim por diante) de e para os serviços da AEM Forms. O tipo `BLOB` é definido em um WSDL de serviço da seguinte maneira:

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

Os campos `MTOM` e `swaRef` têm suporte somente no AEM Forms. Você pode usar esses novos campos somente se especificar uma URL que inclua a propriedade `lc_version`.

**Fornecendo objetos BLOB em solicitações de serviço**

Se uma operação de serviço do AEM Forms exigir um tipo `BLOB` como valor de entrada, crie uma instância do tipo `BLOB` na lógica do aplicativo. (Muitos dos inícios rápidos do serviço da Web em *Programação com formulários AEM* mostram como trabalhar com um tipo de dados BLOB.)

Atribua valores aos campos que pertencem à instância `BLOB` da seguinte maneira:

* **Base64**: para passar dados como texto codificado em um formato Base64, defina os dados no campo `BLOB.binaryData` e defina o tipo de dados no formato MIME (por exemplo, `application/pdf`) no campo `BLOB.contentType`. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: para passar dados binários em um anexo MTOM, defina os dados no campo `BLOB.MTOM`. Essa configuração anexa os dados à solicitação de SOAP usando a estrutura JAX-WS do Java ou a API nativa da estrutura SOAP. (Consulte [Chamar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: para passar dados binários em um anexo WS-I SwaRef, defina os dados no campo `BLOB.swaRef`. Essa configuração anexa os dados à solicitação SOAP usando a estrutura Java JAX-WS. (Consulte [Invocar o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)
* **Anexo MIME ou DIME**: para enviar dados em um anexo MIME ou DIME, anexe os dados à solicitação SOAP usando a API nativa da estrutura SOAP. Defina o identificador do anexo no campo `BLOB.attachmentID`. (Consulte [Invocar o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding).)
* **URL remota**: se os dados estiverem hospedados em um servidor Web e acessíveis através de uma URL HTTP, defina a URL HTTP no campo `BLOB.remoteURL`. (Consulte [Chamar o AEM Forms usando dados BLOB via HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Acessando dados em objetos BLOB retornados de serviços**

O protocolo de transmissão para objetos `BLOB` retornados depende de vários fatores, que são considerados na seguinte ordem, parando quando a condição principal é atendida:

1. **A URL de destino especifica o protocolo de transmissão**. Se a URL de destino especificada na invocação SOAP contiver o parâmetro `blob="`*BLOB_TYPE*&quot;, então *BLOB_TYPE* determinará o protocolo de transmissão. *BLOB_TYPE* é um espaço reservado para base64, dime, mime, http, mtom ou swaref.
1. **O ponto de extremidade SOAP do serviço é Smart**. Se as seguintes condições forem verdadeiras, os documentos de saída serão retornados usando o mesmo protocolo de transmissão que os documentos de entrada:

   * O protocolo padrão do parâmetro de ponto de extremidade SOAP do serviço para objetos Blob de saída está definido como Inteligente.

     Para cada serviço com um endpoint SOAP, o console de administração permite especificar o protocolo de transmissão para todos os blobs retornados. (Consulte [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * O serviço AEM Forms pega um ou mais documentos como entrada.

1. **O ponto de extremidade SOAP do serviço não é Smart**. O protocolo configurado determina o protocolo de transmissão de documentos e os dados são retornados no campo `BLOB` correspondente. Por exemplo, se o ponto de extremidade SOAP estiver definido como DIME, o blob retornado estará no campo `blob.attachmentID`, independentemente do protocolo de transmissão de qualquer documento de entrada.
1. **Caso contrário**. Se um serviço não usar o tipo de documento como entrada, os documentos de saída serão retornados no campo `BLOB.remoteURL` por meio do protocolo HTTP.

Conforme descrito na primeira condição, é possível garantir o tipo de transmissão de qualquer documento retornado estendendo o URL do ponto de extremidade SOAP com um sufixo da seguinte maneira:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Esta é a correlação entre os tipos de transmissão e o campo a partir do qual você obtém os dados:

* Formato **Base64**: Defina o sufixo `blob` como `base64` para retornar os dados no campo `BLOB.binaryData`.
* **Anexo MIME ou DIME**: Defina o sufixo `blob` como `DIME` ou `MIME` para retornar os dados como um tipo de anexo correspondente com o identificador de anexo retornado no campo `BLOB.attachmentID`. Use a API proprietária da estrutura SOAP para ler os dados do anexo.
* **URL remota**: Defina o sufixo `blob` como `http` para manter os dados no servidor de aplicativos e retornar a URL que aponta para os dados no campo `BLOB.remoteURL`.
* **MTOM ou SwaRef**: Defina o sufixo `blob` como `mtom` ou `swaref` para retornar os dados como um tipo de anexo correspondente com o identificador de anexo retornado nos campos `BLOB.MTOM` ou `BLOB.swaRef`. Use a API nativa da estrutura do SOAP para ler os dados do anexo.

>[!NOTE]
>
>É recomendável que você não exceda 30 MB ao preencher um objeto `BLOB` invocando seu método `setBinaryData`. Caso contrário, existe a possibilidade de ocorrer uma exceção `OutOfMemory`.

>[!NOTE]
>
>Os aplicativos baseados em JAX WS que usam o protocolo de transmissão MTOM são limitados a 25 MB de dados enviados e recebidos. Essa limitação se deve a um erro no JAX-WS. Se o tamanho combinado dos arquivos enviados e recebidos exceder 25 MB, use o protocolo de transmissão SwaRef em vez do MTOM. Caso contrário, há a possibilidade de uma exceção `OutOfMemory`.

**Transmissão MTOM de matrizes de bytes codificadas em base64**

Além do objeto `BLOB`, o protocolo MTOM dá suporte a qualquer parâmetro de matriz de bytes ou campo de matriz de bytes de um tipo complexo. Isso significa que as estruturas SOAP do cliente com suporte para MTOM podem enviar qualquer elemento `xsd:base64Binary` como um anexo MTOM (em vez de um texto codificado em base64). Os endpoints SOAP do AEM Forms podem ler esse tipo de codificação por matriz de bytes. No entanto, o serviço AEM Forms sempre retorna um tipo de matriz de bytes como um texto codificado em base64. Os parâmetros de matriz de bytes de saída não dão suporte a MTOM.

Os serviços do AEM Forms que retornam uma grande quantidade de dados binários usam o tipo Documento/BLOB em vez do tipo de matriz de bytes. O tipo de documento é muito mais eficiente para transmitir grandes quantidades de dados.

## Tipos de dados do serviço da Web {#web-service-data-types}

A tabela a seguir lista os tipos de dados Java e mostra o tipo de dados do serviço Web correspondente.

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
   <td><p>O tipo <code>DATE</code>, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço do AEM Forms usar um valor <code>java.util.Date</code> como entrada, o aplicativo cliente SOAP deverá passar a data no campo <code>DATE.date</code>. Configurar o campo <code>DATE.calendar</code> nesse caso causa uma exceção de tempo de execução. Se o serviço retornar um <code>java.util.Date</code>, a data será retornada no campo <code>DATE.date</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>O tipo <code>DATE</code>, que é definido em um WSDL de serviço da seguinte maneira:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço do AEM Forms usar um valor <code>java.util.Calendar</code> como entrada, o aplicativo cliente SOAP deverá passar a data no campo <code>DATE.caledendar</code>. Configurar o campo <code>DATE.date</code> nesse caso causa uma exceção de tempo de execução. Se o serviço retornar um <code>java.util.Calendar</code>, a data será retornada no campo <code>DATE.calendar</code>. </p></td>
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
   <td><p>O tipo XML, que é definido em um serviço WSDL da seguinte maneira:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço do AEM Forms aceitar um valor <code>org.w3c.dom.Document</code>, passe os dados XML no campo <code>XML.document</code>.</p><p>Definir o campo <code>XML.element</code> causa uma exceção de tempo de execução. Se o serviço retornar um <code>org.w3c.dom.Document</code>, os dados XML serão retornados no campo <code>XML.document</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>O tipo XML, que é definido em um serviço WSDL da seguinte maneira:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se uma operação de serviço do AEM Forms usar <code>org.w3c.dom.Element</code> como entrada, passe os dados XML no campo <code>XML.element</code>.</p><p>Definir o campo <code>XML.document</code> causa uma exceção de tempo de execução. Se o serviço retornar um <code>org.w3c.dom.Element</code>, os dados XML serão retornados no campo <code>XML.element</code>.</p></td>
  </tr>
 </tbody>
</table>

## Criando classes proxy Java usando JAX-WS {#creating-java-proxy-classes-using-jax-ws}

Você pode usar JAX-WS para converter um serviço Forms WSDL em classes de proxy Java. Essas classes permitem que você chame as operações de serviços do AEM Forms. O Apache Ant permite criar um script de construção que gera classes de proxy Java referenciando um serviço WSDL do AEM Forms. Você pode gerar arquivos proxy JAX-WS executando as seguintes etapas:

1. Instale o Apache Ant no computador cliente. (Consulte [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Adicione o diretório bin ao caminho da classe.
   * Defina a variável de ambiente `ANT_HOME` para o diretório onde você instalou o Ant.

1. Instale o JDK 1.6 ou posterior.

   * Adicione o diretório bin do JDK ao caminho da classe.
   * Adicione o diretório bin do JRE ao caminho da classe. Este compartimento está no diretório `[JDK_INSTALL_LOCATION]/jre`.
   * Defina a variável de ambiente `JAVA_HOME` para o diretório onde você instalou o JDK.

   O JDK 1.6 inclui o programa wsimport usado no arquivo build.xml. O JDK 1.5 não inclui esse programa.

1. Instale o JAX-WS no computador cliente. (Consulte [API Java para serviços Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Use JAX-WS e Apache Ant para gerar classes de proxy Java. Crie um script de construção Ant para realizar esta tarefa. O script a seguir é um exemplo de script de construção Ant chamado build.xml:

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

   Neste script de compilação Ant, observe que a propriedade `url` está definida para fazer referência ao WSDL do serviço de criptografia em execução no host local. As propriedades `username` e `password` devem ser definidas como um nome de usuário e senha válidos para formulários AEM. Observe que a URL contém o atributo `lc_version`. Sem especificar a opção `lc_version`, não é possível invocar novas operações de serviço do AEM Forms.

   >[!NOTE]
   >
   >Substitua `EncryptionService` pelo nome de serviço do AEM Forms que você deseja chamar usando classes de proxy Java. Por exemplo, para criar classes de proxy Java para o serviço Rights Management, especifique:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Crie um arquivo BAT para executar o script de construção Ant. O comando a seguir pode estar localizado em um arquivo BAT responsável pela execução do script de construção Ant:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Coloque o script de construção ANT no diretório C:\Program Files\Java\jaxws-ri\bin. O script grava os arquivos JAVA no .pasta /classes. O script gera arquivos JAVA que podem chamar o serviço.

1. Empacote os arquivos JAVA em um arquivo JAR. Se você estiver trabalhando no Eclipse, siga estas etapas:

   * Crie um projeto Java que seja usado para empacotar os arquivos JAVA do proxy em um arquivo JAR.
   * Crie uma pasta de código-fonte no projeto.
   * Crie um pacote `com.adobe.idp.services` na pasta Source.
   * Selecione o pacote `com.adobe.idp.services` e importe os arquivos JAVA da pasta adobe/idp/services para o pacote.
   * Se necessário, crie um pacote `org/apache/xml/xmlsoap` na pasta Source.
   * Selecione a pasta de origem e importe os arquivos JAVA da pasta org/apache/xml/xmlsoap.
   * Defina o nível de conformidade do compilador Java como 5.0 ou superior.
   * Crie o projeto.
   * Exporte o projeto como um arquivo JAR.
   * Importe este arquivo JAR no caminho de classe de um projeto cliente. Além disso, importe todos os arquivos JAR no &lt;Diretório de instalação>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Todos os serviços Web Java de início rápido (exceto o serviço Forms) em Programação com AEM criam arquivos proxy Java usando JAX-WS. Além disso, todos os serviços Web Java iniciam rapidamente, use SwaRef. (Consulte [Invocar o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref).)

**Consulte também**

[Criando classes de proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis)

[Chamada de AEM Forms usando codificação Base64](#invoking-aem-forms-using-base64-encoding)

[Chamar o AEM Forms usando dados BLOB por HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Chamar o AEM Forms usando SwaRef](#invoking-aem-forms-using-swaref)

## Criando classes de proxy Java usando o Apache Axis {#creating-java-proxy-classes-using-apache-axis}

Você pode usar a ferramenta Apache Axis WSDL2Java para converter um serviço Forms em classes de proxy Java. Essas classes permitem chamar as operações de serviço do Forms. Usando o Apache Ant, você pode gerar arquivos da biblioteca do Axis de um serviço WSDL. Você pode baixar o Apache Axis no URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Os inícios rápidos do serviço da Web associados ao serviço Forms usam classes de proxy Java criadas usando o Apache Axis. Os inícios rápidos do serviço da Web do Forms também usam Base64 como tipo de codificação. (Consulte [Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

Você pode gerar arquivos da biblioteca Java do Axis executando as seguintes etapas:

1. Instale o Apache Ant no computador cliente. Está disponível em [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Adicione o diretório bin ao caminho da classe.
   * Defina a variável de ambiente `ANT_HOME` para o diretório onde você instalou o Ant.

1. Instale o Apache Axis 1.4 no computador cliente. Está disponível em [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. Configure o caminho da classe para usar os arquivos JAR do Axis no cliente de serviço Web, conforme descrito nas instruções de instalação do Axis em [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Use a ferramenta Apache WSDL2Java no Axis para gerar classes de proxy Java. Crie um script de construção Ant para realizar esta tarefa. O script a seguir é um exemplo de script de construção Ant chamado build.xml:

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

   Neste script de compilação Ant, observe que a propriedade `url` está definida para fazer referência ao WSDL do serviço de criptografia em execução no host local. As propriedades `username` e `password` devem ser definidas como um nome de usuário e senha válidos para formulários AEM.

1. Crie um arquivo BAT para executar o script de construção Ant. O comando a seguir pode estar localizado em um arquivo BAT responsável pela execução do script de construção Ant:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   Os arquivos JAVA são gravados na pasta C:\JavaFiles, conforme especificado pela propriedade `output`. Para chamar o serviço Forms com êxito, importe esses arquivos JAVA para o caminho da classe.

   Por padrão, esses arquivos pertencem a um pacote Java chamado `com.adobe.idp.services`. É recomendável colocar esses arquivos JAVA em um arquivo JAR. Em seguida, importe o arquivo JAR para o caminho de classe do aplicativo cliente.

   >[!NOTE]
   >
   >Há diferentes maneiras de colocar arquivos .JAVA em um JAR. Uma maneira é usar um Java IDE como o Eclipse. Crie um projeto Java e crie um pacote `com.adobe.idp.services` (todos os arquivos .JAVA pertencem a este pacote). Em seguida, importe todos os arquivos .JAVA para o pacote. Por fim, exporte o projeto como um arquivo JAR.

1. Corrija a URL na classe `EncryptionServiceLocator` para especificar o tipo de codificação. Por exemplo, para usar base64, especifique `?blob=base64` para garantir que o objeto `BLOB` retorne dados binários. Ou seja, na classe `EncryptionServiceLocator`, localize a seguinte linha de código:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   e altere para:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Adicione os seguintes arquivos JAR do Axis ao caminho de classe do projeto Java:

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

**Consulte também**

[Criando classes proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Chamada de AEM Forms usando codificação Base64](#invoking-aem-forms-using-base64-encoding)

[Chamar o AEM Forms usando dados BLOB por HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Chamada de AEM Forms usando codificação Base64 {#invoking-aem-forms-using-base64-encoding}

Você pode chamar um serviço AEM Forms usando a codificação Base64. A codificação Base64 codifica anexos enviados com uma solicitação de invocação de serviço Web. Ou seja, os dados de `BLOB` são codificados em Base64, não na mensagem SOAP inteira.

&quot;Chamar o AEM Forms usando a codificação Base64&quot; discute invocar o seguinte processo de vida curta do AEM Forms chamado `MyApplication/EncryptDocument` usando a codificação Base64.

>[!NOTE]
>
>Este processo não se baseia em um processo AEM Forms existente. Para seguir o exemplo do código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação é baseada na operação `SetValue`. O parâmetro de entrada para este processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação é baseada na operação `PasswordEncryptPDF`. O documento de PDF criptografado por senha é retornado em uma variável de processo denominada `outDoc`.

### Criando um assembly de cliente .NET que usa codificação Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

Você pode criar um assembly de cliente .NET para chamar um serviço Forms de um projeto do Microsoft Visual Studio .NET. Para criar um assembly de cliente .NET que use codificação base64, execute as seguintes etapas:

1. Crie uma classe proxy com base em um URL de invocação AEM Forms.
1. Crie um projeto do Microsoft Visual Studio .NET que produza o assembly cliente .NET.

**Criando uma classe de proxy**

Você pode criar uma classe proxy que seja usada para criar o assembly de cliente .NET usando uma ferramenta que acompanha o Microsoft Visual Studio. O nome da ferramenta é wsdl.exe e está na pasta de instalação do Microsoft Visual Studio. Para criar uma classe de proxy, abra o prompt de comando e navegue até a pasta que contém o arquivo wsdl.exe. Para obter mais informações sobre a ferramenta wsdl.exe, consulte a *Ajuda do MSDN*.

Digite o seguinte comando no prompt de comando:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Por padrão, essa ferramenta cria um arquivo CS na mesma pasta que é baseada no nome do WSDL. Nessa situação, ele cria um arquivo CS chamado *EncryptDocumentService.cs*. Use esse arquivo CS para criar um objeto proxy que permita chamar o serviço especificado no URL de invocação.

Corrija a URL na classe de proxy para incluir `?blob=base64` para garantir que o objeto `BLOB` retorne dados binários. Na classe proxy, localize a seguinte linha de código:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

e altere para:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

A seção *Chamando o AEM Forms usando a Codificação Base64* usa `MyApplication/EncryptDocument` como exemplo. Se você estiver criando um assembly de cliente .NET para outro serviço Forms, substitua `MyApplication/EncryptDocument` pelo nome do serviço.

**Desenvolvendo o assembly .NET client**

Crie um projeto da Biblioteca de Classes do Visual Studio que produza um assembly cliente .NET. O arquivo CS que você criou usando wsdl.exe pode ser importado para este projeto. Este projeto produz um arquivo DLL (o assembly de cliente .NET) que você pode usar em outros projetos do Visual Studio .NET para chamar um serviço.

1. Inicie o Microsoft Visual Studio .NET.
1. Crie um projeto de Biblioteca de classes e nomeie-o como DocumentService.
1. Importe o arquivo CS que você criou usando wsdl.exe.
1. No menu **Projeto**, selecione **Adicionar Referência**.
1. Na caixa de diálogo Adicionar referência, selecione **System.Web.Services.dll**.
1. Clique em **Selecionar** e em **OK**.
1. Compile e construa o projeto.

>[!NOTE]
>
>Este procedimento cria um assembly cliente .NET chamado DocumentService.dll que pode ser usado para enviar solicitações SOAP ao serviço `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Verifique se você adicionou `?blob=base64` à URL na classe de proxy usada para criar o assembly de cliente .NET. Caso contrário, você não poderá recuperar dados binários do objeto `BLOB`.

**Referenciando o assembly cliente .NET**

Coloque o assembly do cliente .NET recém-criado no computador em que você está desenvolvendo o aplicativo cliente. Depois de colocar o assembly .NET client em um diretório, você pode referenciá-lo a partir de um projeto. Também faça referência à biblioteca `System.Web.Services` do seu projeto. Se você não fizer referência a esta biblioteca, não poderá usar o assembly do cliente .NET para chamar um serviço.

1. No menu **Projeto**, selecione **Adicionar Referência**.
1. Clique na guia **.NET**.
1. Clique em **Procurar** e localize o arquivo DocumentService.dll.
1. Clique em **Selecionar** e em **OK**.

**Chamando um serviço usando um assembly cliente .NET que usa codificação Base64**

Você pode invocar o serviço `MyApplication/EncryptDocument` (que foi construído no Workbench) usando um assembly cliente .NET que usa codificação Base64. Para invocar o serviço `MyApplication/EncryptDocument`, execute as seguintes etapas:

1. Crie um assembly cliente Microsoft .NET que consuma o WSDL do serviço `MyApplication/EncryptDocument`.
1. Crie um projeto Microsoft .NET do cliente. Referencie o assembly do cliente Microsoft .NET no projeto do cliente. Também referenciar `System.Web.Services`.
1. Usando o assembly do cliente Microsoft .NET, crie um objeto `MyApplication_EncryptDocumentService` invocando seu construtor padrão.
1. Defina a propriedade `Credentials` do objeto `MyApplication_EncryptDocumentService` com um objeto `System.Net.NetworkCredential`. No construtor `System.Net.NetworkCredential`, especifique um nome de usuário de formulários AEM e a senha correspondente. Defina valores de autenticação para permitir que o aplicativo cliente .NET troque mensagens SOAP com o AEM Forms com êxito.
1. Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar uma passagem de documento PDF para o processo `MyApplication/EncryptDocument`.
1. Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
1. Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
1. Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
1. Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` com o conteúdo da matriz de bytes.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplication_EncryptDocumentService` e transmitindo o objeto `BLOB` que contém o documento PDF. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento criptografado por senha.
1. Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `invoke` do objeto `MyApplicationEncryptDocumentService`. Popular a matriz de bytes obtendo o valor do membro de dados `binaryData` do objeto `BLOB`.
1. Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

### Chamar um serviço usando classes de proxy Java e codificação Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Você pode chamar um serviço AEM Forms usando classes de proxy Java e Base64. Para chamar o serviço `MyApplication/EncryptDocument` usando classes de proxy Java, execute as seguintes etapas:

1. Crie classes de proxy Java usando JAX-WS que consome o serviço WSDL `MyApplication/EncryptDocument`. Use o seguinte ponto final WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacotar as classes de proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo JAR do proxy Java e os arquivos JAR no seguinte caminho:

   &lt;Diretório de instalação>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `getEncryptDocument` do objeto `MyApplicationEncryptDocumentService`.
1. Defina os valores de conexão necessários para chamar o AEM Forms, atribuindo valores aos seguintes membros de dados:

   * Atribua o ponto de extremidade WSDL e o tipo de codificação ao campo `ENDPOINT_ADDRESS_PROPERTY` do objeto `javax.xml.ws.BindingProvider`. Para invocar o serviço `MyApplication/EncryptDocument` usando a codificação Base64, especifique o seguinte valor de URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Atribua o usuário de formulários AEM ao campo `USERNAME_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.
   * Atribua o valor de senha correspondente ao campo `PASSWORD_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.

   O código de exemplo a seguir mostra essa lógica de aplicativo:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere o documento PDF para enviar ao processo `MyApplication/EncryptDocument` criando um objeto `java.io.FileInputStream` usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
1. Crie uma matriz de bytes e preencha-a com o conteúdo do objeto `java.io.FileInputStream`.
1. Crie um objeto `BLOB` usando seu construtor.
1. Preencha o objeto `BLOB` invocando seu método `setBinaryData` e transmitindo a matriz de bytes. O `setBinaryData` do objeto `BLOB` é o método a ser chamado quando se usa a codificação Base64. Consulte Suprimento de objetos BLOB em solicitações de serviço.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplicationEncryptDocument`. Transmita o objeto `BLOB` que contém o documento PDF. O método invoke retorna um objeto `BLOB` que contém o documento PDF criptografado.
1. Crie uma matriz de bytes que contenha o documento PDF criptografado invocando o método `getBinaryData` do objeto `BLOB`.
1. Salve o documento PDF criptografado como um arquivo PDF. Grave a matriz de bytes em um arquivo.

**Consulte também**

[Início rápido: chamar um serviço usando arquivos proxy Java e codificação Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Chamar o AEM Forms usando MTOM {#invoking-aem-forms-using-mtom}

Você pode chamar serviços da AEM Forms usando a MTOM padrão do serviço da Web. Esse padrão define como os dados binários, como um documento PDF, são transmitidos pela Internet ou pela intranet. Um recurso do MTOM é o uso do elemento `XOP:Include`. Esse elemento é definido na especificação XML Binary Otimized Packaging (XOP) para fazer referência aos anexos binários de uma mensagem SOAP.

A discussão aqui é sobre o uso de MTOM para invocar o seguinte processo de vida curta do AEM Forms chamado `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Este processo não se baseia em um processo AEM Forms existente. Para seguir o exemplo do código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação é baseada na operação `SetValue`. O parâmetro de entrada para este processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação é baseada na operação `PasswordEncryptPDF`. O documento de PDF criptografado por senha é retornado em uma variável de processo denominada `outDoc`.

>[!NOTE]
>
>O suporte a MTOM foi adicionado no AEM Forms, versão 9.

>[!NOTE]
>
>Os aplicativos baseados em JAX WS que usam o protocolo de transmissão MTOM são limitados a 25 MB de dados enviados e recebidos. Essa limitação se deve a um erro no JAX-WS. Se o tamanho combinado dos arquivos enviados e recebidos exceder 25 MB, use o protocolo de transmissão SwaRef em vez do MTOM. Caso contrário, há a possibilidade de uma exceção `OutOfMemory`.

A discussão aqui é sobre o uso do MTOM em um projeto do Microsoft .NET para chamar os serviços da AEM Forms. O .NET framework usado é o 3.5, e o ambiente de desenvolvimento é o Visual Studio 2008. Se você tiver o WSE (Web Service Enhancements) instalado no computador de desenvolvimento, remova-o. O .NET 3.5 framework suporta um framework SOAP chamado Windows Communication Foundation (WCF). Ao invocar o AEM Forms usando MTOM, somente o WCF (não o WSE) é compatível.

### Criando um projeto .NET que chama um serviço usando MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

Você pode criar um projeto Microsoft .NET que possa chamar um serviço AEM Forms usando serviços Web. Primeiro, crie um projeto do Microsoft .NET usando o Visual Studio 2008. Para chamar um serviço do AEM Forms, crie uma Referência de serviço para o serviço do AEM Forms que você deseja chamar no projeto. Ao criar uma Referência de serviço, especifique um URL para o serviço do AEM Forms:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Substitua `localhost` pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms. Substitua `MyApplication/EncryptDocument` pelo nome do serviço AEM Forms a ser chamado. Por exemplo, para chamar uma operação Rights Management, especifique:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

A opção `lc_version` garante a disponibilidade da funcionalidade do AEM Forms, como MTOM. Sem especificar a opção `lc_version`, você não pode invocar o AEM Forms usando MTOM.

Depois de criar uma Referência de serviço, os tipos de dados associados ao serviço AEM Forms ficam disponíveis para uso no projeto .NET. Para criar um projeto .NET que chame um serviço AEM Forms, execute as seguintes etapas:

1. Crie um projeto .NET usando o Microsoft Visual Studio 2008.
1. No menu **Projeto**, selecione **Adicionar Referência de Serviço**.
1. Na caixa de diálogo **Endereço**, especifique o WSDL para o serviço AEM Forms. Por exemplo,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Clique em **Ir** e em **OK**.

### Chamar um serviço usando MTOM em um projeto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Considere o processo `MyApplication/EncryptDocument` que aceita um documento PDF não seguro e retorna um documento PDF criptografado por senha. Para invocar o processo `MyApplication/EncryptDocument` (que foi criado no Workbench) usando MTOM, execute as seguintes etapas:

1. Crie um projeto do Microsoft .NET.
1. Crie um objeto `MyApplication_EncryptDocumentClient` usando seu construtor padrão.
1. Crie um objeto `MyApplication_EncryptDocumentClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms e o tipo de codificação:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço. No entanto, certifique-se de especificar `?blob=mtom`.

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do membro de dados `EncryptDocumentClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
1. Defina o membro de dados `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
1. Ative a autenticação HTTP básica executando as seguintes tarefas:

   * Atribua o nome de usuário dos formulários AEM ao membro de dados `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Atribua o valor de senha correspondente ao membro de dados `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Atribua o valor constante `HttpClientCredentialType.Basic` ao membro de dados `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao membro de dados `BasicHttpBindingSecurity.Security.Mode`.

   O código de exemplo a seguir mostra essas tarefas.

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
1. Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
1. Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
1. Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
1. Preencha o objeto `BLOB` atribuindo seu membro de dados `MTOM` com o conteúdo da matriz de bytes.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplication_EncryptDocumentClient`. Transmita o objeto `BLOB` que contém o documento PDF. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF seguro.
1. Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `invoke`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
1. Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

>[!NOTE]
>
>A maioria das operações de serviço do AEM Forms tem um início rápido MTOM. Você pode visualizar esses inícios rápidos na seção de início rápido correspondente de um serviço. Por exemplo, para ver a seção Início rápido de saída, consulte [Inícios rápidos da API de serviço de saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte também**

[Início Rápido: Chamar um serviço usando MTOM em um projeto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Acesso a vários serviços usando serviços da Web](#accessing-multiple-services-using-web-services)

[Criação de um aplicativo web ASP.NET que invoca um processo de longa vida centrado no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Chamar o AEM Forms usando SwaRef {#invoking-aem-forms-using-swaref}

Você pode chamar os serviços da AEM Forms usando SwaRef. O conteúdo do elemento XML `wsi:swaRef` é enviado como um anexo dentro de um corpo SOAP que armazena a referência ao anexo. Ao chamar um serviço Forms usando SwaRef, crie classes de proxy Java usando a API Java para Serviços Web XML (JAX-WS). (Consulte [API Java para serviços Web XML](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

A discussão aqui é sobre invocar o seguinte processo de vida curta do Forms chamado `MyApplication/EncryptDocument` usando SwaRef.

>[!NOTE]
>
>Este processo não se baseia em um processo AEM Forms existente. Para seguir o exemplo do código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação é baseada na operação `SetValue`. O parâmetro de entrada para este processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação é baseada na operação `PasswordEncryptPDF`. O documento de PDF criptografado por senha é retornado em uma variável de processo denominada `outDoc`.

>[!NOTE]
>
>Suporte a SwaRef adicionado no AEM Forms

A discussão abaixo é sobre como chamar os serviços da Forms usando o SwaRef em um aplicativo cliente Java. O aplicativo Java usa classes de proxy criadas usando JAX-WS.

### Chamar um serviço usando arquivos da biblioteca JAX-WS que usam SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Para invocar o processo `MyApplication/EncryptDocument` usando arquivos proxy Java criados com JAX-WS e SwaRef, execute as seguintes etapas:

1. Crie classes de proxy Java usando JAX-WS que consome o serviço WSDL `MyApplication/EncryptDocument`. Use o seguinte ponto final WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obter informações, consulte [Criando classes de proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacotar as classes de proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo JAR do proxy Java e os arquivos JAR no seguinte caminho:

   &lt;Diretório de instalação>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `getEncryptDocument` do objeto `MyApplicationEncryptDocumentService`.
1. Defina os valores de conexão necessários para chamar o AEM Forms, atribuindo valores aos seguintes membros de dados:

   * Atribua o ponto de extremidade WSDL e o tipo de codificação ao campo `ENDPOINT_ADDRESS_PROPERTY` do objeto `javax.xml.ws.BindingProvider`. Para invocar o serviço `MyApplication/EncryptDocument` usando a codificação SwaRef, especifique o seguinte valor de URL:

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Atribua o usuário de formulários AEM ao campo `USERNAME_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.
   * Atribua o valor de senha correspondente ao campo `PASSWORD_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.

   O código de exemplo a seguir mostra essa lógica de aplicativo:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recupere o documento PDF para enviar ao processo `MyApplication/EncryptDocument` criando um objeto `java.io.File` usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
1. Crie um objeto `javax.activation.DataSource` usando o construtor `FileDataSource`. Passar o objeto `java.io.File`.
1. Crie um objeto `javax.activation.DataHandler` usando seu construtor e transmitindo o objeto `javax.activation.DataSource`.
1. Crie um objeto `BLOB` usando seu construtor.
1. Preencha o objeto `BLOB` invocando seu método `setSwaRef` e transmitindo o objeto `javax.activation.DataHandler`.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplicationEncryptDocument` e transmitindo o objeto `BLOB` que contém o documento PDF. O método invoke retorna um objeto `BLOB` que contém um documento PDF criptografado.
1. Preencha um objeto `javax.activation.DataHandler` invocando o método `getSwaRef` do objeto `BLOB`.
1. Converta o objeto `javax.activation.DataHandler` em uma instância `java.io.InputSteam` invocando o método `getInputStream` do objeto `javax.activation.DataHandler`.
1. Grave a instância `java.io.InputSteam` em um arquivo PDF que represente o documento PDF criptografado.

>[!NOTE]
>
>A maioria das operações de serviço do AEM Forms tem um início rápido SwaRef. Você pode visualizar esses inícios rápidos na seção de início rápido correspondente de um serviço. Por exemplo, para ver a seção Início rápido de saída, consulte [Inícios rápidos da API de serviço de saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulte também**

[Início rápido: chamar um serviço usando SwaRef em um projeto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Chamar o AEM Forms usando dados BLOB por HTTP {#invoking-aem-forms-using-blob-data-over-http}

Você pode chamar serviços da AEM Forms usando serviços da Web e transmitindo dados BLOB por HTTP. Transmitir dados BLOB por HTTP é uma técnica alternativa em vez de usar codificação base64, DIME ou MIME. Por exemplo, você pode transmitir dados via HTTP em um projeto Microsoft .NET que usa o Web Service Enhancement 3.0, que não é compatível com DIME ou MIME. Ao usar dados BLOB por HTTP, os dados de entrada são carregados antes que o serviço do AEM Forms seja chamado.

&quot;Chamar o AEM Forms usando dados BLOB por HTTP&quot; discute o seguinte processo de vida curta do AEM Forms chamado `MyApplication/EncryptDocument` transmitindo dados BLOB por HTTP.

>[!NOTE]
>
>Este processo não se baseia em um processo AEM Forms existente. Para seguir o exemplo do código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação é baseada na operação `SetValue`. O parâmetro de entrada para este processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação é baseada na operação `PasswordEncryptPDF`. O documento de PDF criptografado por senha é retornado em uma variável de processo denominada `outDoc`.

>[!NOTE]
>
>É recomendável que você esteja familiarizado com a Chamada de AEM Forms usando SOAP. (Consulte [Chamar o AEM Forms usando Serviços da Web](#invoking-aem-forms-using-web-services).)

### Criando um assembly cliente .NET que usa dados por HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Para criar um assembly cliente que use dados por HTTP, siga o processo especificado em [Chamando o AEM Forms usando a codificação Base64](#invoking-aem-forms-using-base64-encoding). No entanto, corrija a URL na classe de proxy para incluir `?blob=http` em vez de `?blob=base64`. Essa ação garante que os dados sejam transmitidos via HTTP. Na classe proxy, localize a seguinte linha de código:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

e altere para:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Referenciando o assembly .NET clientMyApplication/EncryptDocument**

Coloque o novo assembly .NET client no computador em que você está desenvolvendo o aplicativo cliente. Depois de colocar o assembly .NET client em um diretório, você pode referenciá-lo a partir de um projeto. Faça referência à biblioteca `System.Web.Services` do seu projeto. Se você não fizer referência a esta biblioteca, não poderá usar o assembly do cliente .NET para chamar um serviço.

1. No menu **Projeto**, selecione **Adicionar Referência**.
1. Clique na guia **.NET**.
1. Clique em **Procurar** e localize o arquivo DocumentService.dll.
1. Clique em **Selecionar** e em **OK**.

**Chamando um serviço usando um assembly cliente .NET que usa dados BLOB via HTTP**

Você pode invocar o serviço `MyApplication/EncryptDocument` (que foi criado no Workbench) usando um assembly cliente .NET que usa dados por HTTP. Para invocar o serviço `MyApplication/EncryptDocument`, execute as seguintes etapas:

1. Crie o assembly do cliente .NET.
1. Referencie o assembly do cliente Microsoft .NET. Crie um projeto Microsoft .NET do cliente. Referencie o assembly do cliente Microsoft .NET no projeto do cliente. Também referenciar `System.Web.Services`.
1. Usando o assembly do cliente Microsoft .NET, crie um objeto `MyApplication_EncryptDocumentService` invocando seu construtor padrão.
1. Defina a propriedade `Credentials` do objeto `MyApplication_EncryptDocumentService` com um objeto `System.Net.NetworkCredential`. No construtor `System.Net.NetworkCredential`, especifique um nome de usuário de formulários AEM e a senha correspondente. Defina valores de autenticação para permitir que o aplicativo cliente .NET troque mensagens SOAP com o AEM Forms com êxito.
1. Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para passar dados para o processo `MyApplication/EncryptDocument`.
1. Atribua um valor de cadeia de caracteres ao membro de dados `remoteURL` do objeto `BLOB` que especifica o local do URI de um documento PDF a ser passado para o serviço `MyApplication/EncryptDocument`.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplication_EncryptDocumentService` e transmitindo o objeto `BLOB`. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Crie um objeto `System.UriBuilder` usando seu construtor e transmitindo o valor do membro de dados `remoteURL` do objeto `BLOB` retornado.
1. Converta o objeto `System.UriBuilder` em um objeto `System.IO.Stream`. (O Quick Start C# que segue esta lista ilustra como executar esta tarefa.)
1. Crie uma matriz de bytes e preencha-a com os dados no objeto `System.IO.Stream`.
1. Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

### Chamar um serviço usando classes de proxy Java e dados BLOB por HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Você pode chamar um serviço AEM Forms usando classes de proxy Java e dados BLOB por HTTP. Para chamar o serviço `MyApplication/EncryptDocument` usando classes de proxy Java, execute as seguintes etapas:

1. Crie classes de proxy Java usando JAX-WS que consome o serviço WSDL `MyApplication/EncryptDocument`. Use o seguinte ponto final WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Para obter informações, consulte [Criando classes de proxy Java usando JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Substitua `hiro-xp` *pelo endereço IP do servidor de aplicativos J2EE que hospeda o AEM Forms.*

1. Empacotar as classes de proxy Java criadas usando JAX-WS em um arquivo JAR.
1. Inclua o arquivo JAR do proxy Java e os arquivos JAR no seguinte caminho:

   &lt;Diretório de instalação>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   no caminho de classe do projeto do cliente Java.

1. Crie um objeto `MyApplicationEncryptDocumentService` usando seu construtor.
1. Crie um objeto `MyApplicationEncryptDocument` invocando o método `getEncryptDocument` do objeto `MyApplicationEncryptDocumentService`.
1. Defina os valores de conexão necessários para chamar o AEM Forms, atribuindo valores aos seguintes membros de dados:

   * Atribua o ponto de extremidade WSDL e o tipo de codificação ao campo `ENDPOINT_ADDRESS_PROPERTY` do objeto `javax.xml.ws.BindingProvider`. Para chamar o serviço `MyApplication/EncryptDocument` usando BLOB sobre codificação HTTP, especifique o seguinte valor de URL:

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Atribua o usuário de formulários AEM ao campo `USERNAME_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.
   * Atribua o valor de senha correspondente ao campo `PASSWORD_PROPERTY` do objeto `javax.xml.ws.BindingProvider`.

   O código de exemplo a seguir mostra essa lógica de aplicativo:

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
1. Preencha o objeto `BLOB` invocando seu método `setRemoteURL`. Transmita um valor de cadeia de caracteres que especifique o local URI de um documento PDF a ser transmitido para o serviço `MyApplication/EncryptDocument`.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `MyApplicationEncryptDocument` e transmitindo o objeto `BLOB` que contém o documento PDF. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Crie uma matriz de bytes para armazenar o fluxo de dados que representa o documento de PDF criptografado. Invoque o método `getRemoteURL` do objeto `BLOB` (use o objeto `BLOB` retornado pelo método `invoke`).
1. Crie um objeto `java.io.File` usando seu construtor. Este objeto representa o documento de PDF criptografado.
1. Crie um objeto `java.io.FileOutputStream` usando seu construtor e transmitindo o objeto `java.io.File`.
1. Invoque o método `write` do objeto `java.io.FileOutputStream`. Passe a matriz de bytes que contém o fluxo de dados que representa o documento de PDF criptografado.

## Chamada de AEM Forms usando DIME {#invoking-aem-forms-using-dime}

Você pode chamar serviços da AEM Forms usando SOAP com anexos. O AEM Forms oferece suporte aos padrões de serviço Web MIME e DIME. O DIME permite enviar anexos binários, como documentos PDF, juntamente com solicitações de chamada, em vez de codificar o anexo. A seção *Chamando o AEM Forms usando DIME* discute invocando o seguinte processo de vida curta do AEM Forms denominado `MyApplication/EncryptDocument` usando DIME.

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento de PDF não seguro passado para o processo. Esta ação é baseada na operação `SetValue`. O parâmetro de entrada para este processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação é baseada na operação `PasswordEncryptPDF`. O documento de PDF criptografado por senha é retornado em uma variável de processo denominada `outDoc`.

Este processo não se baseia em um processo AEM Forms existente. Para seguir os exemplos de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>A chamada de operações de serviço do AEM Forms usando DIME está obsoleta. É recomendável usar MTOM. (Consulte [Chamar o AEM Forms usando MTOM](#invoking-aem-forms-using-mtom).)

### Criando um projeto .NET que use DIME {#creating-a-net-project-that-uses-dime}

Para criar um projeto .NET que possa chamar um serviço Forms usando DIME, execute as seguintes tarefas:

* Instale o Web Services Enhancements 2.0 no computador de desenvolvimento.
* No projeto .NET, crie uma referência da Web para o serviço FormsAEM Forms.

**Instalando Melhorias de Serviços Web 2.0**

Instale o Web Services Enhancements 2.0 no computador de desenvolvimento e integre-o ao Microsoft Visual Studio .NET. Você pode baixar as Melhorias de Serviços Web 2.0 do [Centro de Download da Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Nessa página da Web, procure por Melhorias nos serviços da Web 2.0 e baixe-as no computador de desenvolvimento. Este download coloca um arquivo chamado Microsoft WSE 2.0 SPI.msi no seu computador. Execute o programa de instalação e siga as instruções on-line.

>[!NOTE]
>
>O recurso Melhorias nos serviços da Web 2.0 é compatível com DIME. A versão do Microsoft Visual Studio com suporte é 2003 quando você trabalha com Melhorias de serviços da Web 2.0. O Web Services Enhancements 3.0 não é compatível com o DIME; no entanto, ele é compatível com o MTOM.

**Criando uma referência da Web para um serviço AEM Forms**

Depois de instalar o Web Services Enhancements 2.0 no computador de desenvolvimento e criar um projeto Microsoft .NET, crie uma referência Web para o serviço Forms. Por exemplo, para criar uma referência da Web para o processo `MyApplication/EncryptDocument` e supondo que o Forms esteja instalado no computador local, especifique a seguinte URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Após criar uma referência da Web, os dois tipos de dados de proxy a seguir estão disponíveis para uso no projeto .NET: `EncryptDocumentService` e `EncryptDocumentServiceWse`. Para invocar o processo `MyApplication/EncryptDocument` usando DIME, use o tipo `EncryptDocumentServiceWse`.

>[!NOTE]
>
>Antes de criar uma referência da Web para o serviço Forms, certifique-se de mencionar Web Services Enhancements 2.0 no seu projeto. (Consulte &quot;Instalação do Web Services Enhancements 2.0&quot;.)

**Referência à biblioteca WSE**

1. No menu Projeto, selecione Adicionar referência.
1. Na caixa de diálogo Adicionar referência, selecione Microsoft.Web.Services2.dll.
1. Selecione System.Web.Services.dll.
1. Clique em Selecionar e em OK.

**Criar uma referência da Web para um serviço Forms**

1. No menu Projeto, selecione Adicionar referência da Web.
1. Na caixa de diálogo URL, especifique o URL para o serviço Forms.
1. Clique em Ir e em Adicionar Referência.

>[!NOTE]
>
>Certifique-se de habilitar seu projeto .NET para usar a biblioteca WSE. No Project Explorer, clique com o botão direito do mouse no nome do projeto e selecione Habilitar WSE 2.0. Certifique-se de que a caixa de seleção na caixa de diálogo exibida esteja selecionada.

**Chamando um serviço usando DIME em um projeto .NET**

Você pode chamar um serviço Forms usando DIME. Considere o processo `MyApplication/EncryptDocument` que aceita um documento PDF não seguro e retorna um documento PDF criptografado por senha. Para invocar o processo `MyApplication/EncryptDocument` usando DIME, execute as seguintes etapas:

1. Crie um projeto Microsoft .NET que permita chamar um serviço Forms usando DIME. Certifique-se de incluir as Melhorias de serviços da Web 2.0 e criar uma referência da Web para o serviço AEM Forms.
1. Depois de definir uma referência da Web para o processo `MyApplication/EncryptDocument`, crie um objeto `EncryptDocumentServiceWse` usando seu construtor padrão.
1. Defina o membro de dados `Credentials` do objeto `EncryptDocumentServiceWse` com um valor `System.Net.NetworkCredential` que especifique o nome de usuário e o valor da senha dos formulários AEM.
1. Crie um objeto `Microsoft.Web.Services2.Dime.DimeAttachment` usando seu construtor e transmitindo os seguintes valores:

   * Um valor de string que especifica um valor de GUID. Você pode obter um valor de GUID invocando o método `System.Guid.NewGuid.ToString`.
   * Um valor de string que especifica o tipo de conteúdo. Como este processo requer um documento PDF, especifique `application/pdf`.
   * Um valor de enumeração `TypeFormat`. Especifique `TypeFormat.MediaType`.
   * Um valor de string que especifica o local do documento PDF a ser transmitido para o processo AEM Forms.

1. Crie um objeto `BLOB` usando seu construtor.
1. Adicione o anexo DIME ao objeto `BLOB` atribuindo o valor do membro de dados `Id` do objeto `Microsoft.Web.Services2.Dime.DimeAttachment` ao membro de dados `attachmentID` do objeto `BLOB`.
1. Invoque o método `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` e passe o objeto `Microsoft.Web.Services2.Dime.DimeAttachment`.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `EncryptDocumentServiceWse` e transmitindo o objeto `BLOB` que contém o anexo DIME. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Obtenha o valor identificador do anexo obtendo o valor do membro de dados `attachmentID` do objeto `BLOB` retornado.
1. Repita os anexos em `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` e use o valor identificador de anexo para obter o documento PDF criptografado.
1. Obtenha um objeto `System.IO.Stream` obtendo o valor do membro de dados `Stream` do objeto `Attachment`.
1. Crie uma matriz de bytes e passe essa matriz de bytes para o método `Read` do objeto `System.IO.Stream`. Este método preenche a matriz de bytes com um fluxo de dados que representa o documento de PDF criptografado.
1. Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa um local de arquivo PDF. Este objeto representa o documento de PDF criptografado.
1. Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
1. Grave o conteúdo da matriz de bytes no arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

### Criando classes de proxy Java do Apache Axis que usam DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

Você pode usar a ferramenta Apache Axis WSDL2Java para converter um serviço WSDL em classes de proxy Java para poder chamar operações de serviço. Usando o Apache Ant, você pode gerar arquivos da biblioteca do Axis de um serviço WSDL do AEM Forms que permite chamar o serviço. (Consulte [Criação de classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

A ferramenta Apache Axis WSDL2Java gera arquivos JAVA que contêm métodos usados para enviar solicitações SOAP a um serviço. As solicitações de SOAP recebidas por um serviço são decodificadas pelas bibliotecas geradas pelo Axis e retornam aos métodos e argumentos.

Para chamar o serviço `MyApplication/EncryptDocument` (que foi criado no Workbench) usando arquivos de biblioteca gerados pelo Axis e DIME, execute as seguintes etapas:

1. Crie classes de proxy Java que consomem o WSDL do serviço `MyApplication/EncryptDocument` usando o Apache Axis. (Consulte [Criação de classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)
1. Inclua as classes de proxy Java no caminho da classe.
1. Crie um objeto `MyApplicationEncryptDocumentServiceLocator` usando seu construtor.
1. Crie um objeto `URL` usando seu construtor e transmitindo um valor de cadeia de caracteres que especifica a definição WSDL do serviço AEM Forms. Certifique-se de especificar `?blob=dime` no final da URL do ponto de extremidade SOAP. Por exemplo, use

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Crie um objeto `EncryptDocumentSoapBindingStub` invocando seu construtor e transmitindo o objeto `MyApplicationEncryptDocumentServiceLocator` e o objeto `URL`.
1. Defina o valor de nome de usuário e senha dos formulários AEM invocando os métodos `setUsername` e `setPassword` do objeto `EncryptDocumentSoapBindingStub`.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recupere o documento PDF para enviar ao serviço `MyApplication/EncryptDocument` criando um objeto `java.io.File`. Transmita um valor de string que especifique o local do documento PDF.
1. Crie um objeto `javax.activation.DataHandler` usando seu construtor e transmitindo um objeto `javax.activation.FileDataSource`. O objeto `javax.activation.FileDataSource` pode ser criado usando seu construtor e transmitindo o objeto `java.io.File` que representa o documento PDF.
1. Crie um objeto `org.apache.axis.attachments.AttachmentPart` usando seu construtor e transmitindo o objeto `javax.activation.DataHandler`.
1. Anexe o anexo chamando o método `addAttachment` do objeto `EncryptDocumentSoapBindingStub` e transmitindo o objeto `org.apache.axis.attachments.AttachmentPart`.
1. Crie um objeto `BLOB` usando seu construtor. Preencha o objeto `BLOB` com o valor do identificador de anexo chamando o método `setAttachmentID` do objeto `BLOB` e transmitindo o valor do identificador de anexo. Este valor pode ser obtido chamando o método `getContentId` do objeto `org.apache.axis.attachments.AttachmentPart`.
1. Invoque o processo `MyApplication/EncryptDocument` invocando o método `invoke` do objeto `EncryptDocumentSoapBindingStub`. Transmita o objeto `BLOB` que contém o anexo DIME. Este processo retorna um documento PDF criptografado em um objeto `BLOB`.
1. Obtenha o valor identificador do anexo invocando o método `getAttachmentID` do objeto `BLOB` retornado. Este método retorna um valor de string que representa o valor do identificador do anexo retornado.
1. Recupere os anexos invocando o método `getAttachments` do objeto `EncryptDocumentSoapBindingStub`. Este método retorna uma matriz de `Objects` que representa os anexos.
1. Repita por meio dos anexos (a matriz `Object`) e use o valor do identificador de anexo para obter o documento PDF criptografado. Cada elemento é um objeto `org.apache.axis.attachments.AttachmentPart`.
1. Obtenha o objeto `javax.activation.DataHandler` associado ao anexo chamando o método `getDataHandler` do objeto `org.apache.axis.attachments.AttachmentPart`.
1. Obtenha um objeto `java.io.FileStream` invocando o método `getInputStream` do objeto `javax.activation.DataHandler`.
1. Crie uma matriz de bytes e passe essa matriz de bytes para o método `read` do objeto `java.io.FileStream`. Este método preenche a matriz de bytes com um fluxo de dados que representa o documento de PDF criptografado.
1. Crie um objeto `java.io.File` usando seu construtor. Este objeto representa o documento de PDF criptografado.
1. Crie um objeto `java.io.FileOutputStream` usando seu construtor e transmitindo o objeto `java.io.File`.
1. Invoque o método `write` do objeto `java.io.FileOutputStream` e passe a matriz de bytes que contém o fluxo de dados que representa o documento PDF criptografado.

**Consulte também**

[Início rápido: chamar um serviço usando DIME em um projeto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Usar autenticação baseada em SAML {#using-saml-based-authentication}

O AEM Forms oferece suporte a vários modos de autenticação de serviço da Web ao chamar serviços. Um modo de autenticação é especificar um nome de usuário e um valor de senha usando um cabeçalho de autorização básico na chamada de serviço da Web. O AEM Forms também oferece suporte à autenticação baseada em asserção SAML. Quando um aplicativo cliente chama um serviço AEM Forms usando um serviço Web, o aplicativo cliente pode fornecer informações de autenticação de uma das seguintes maneiras:

* Passar credenciais como parte da Autorização básica
* Envio do token de nome de usuário como parte do cabeçalho WS-Security
* Passar uma asserção SAML como parte do cabeçalho WS-Security
* Envio do token Kerberos como parte do cabeçalho WS-Security

O AEM Forms não oferece suporte à autenticação padrão baseada em certificados, mas oferece suporte à autenticação baseada em certificados em um formato diferente.

>[!NOTE]
>
>O serviço da Web inicia rapidamente em Programação com o AEM Forms para especificar os valores de nome de usuário e senha para executar a autorização.

A identidade dos usuários de formulários AEM pode ser representada por meio de uma asserção SAML assinada usando uma chave secreta. O código XML a seguir mostra um exemplo de uma asserção SAML.

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

Esta declaração de exemplo é emitida para um usuário administrador. Esta asserção contém os seguintes itens visíveis:

* É válido por um determinado período.
* É emitido para um usuário específico.
* Ele é assinado digitalmente. Qualquer modificação feita quebraria a assinatura.
* Ele pode ser apresentado ao AEM Forms como um token da identidade do usuário semelhante ao nome de usuário e à senha.

Um aplicativo cliente pode recuperar a asserção de qualquer API AuthenticationManager do AEM Forms que retorne um objeto `AuthResult`. Você pode obter uma instância `AuthResult` executando um dos dois métodos a seguir:

* Autenticar o usuário usando qualquer um dos métodos de autenticação expostos pela API do AuthenticationManager. Normalmente, é usado o nome de usuário e a senha; no entanto, também é possível usar a autenticação de certificado.
* Usando o método `AuthenticationManager.getAuthResultOnBehalfOfUser`. Esse método permite que um aplicativo cliente obtenha um objeto `AuthResult` para qualquer usuário de formulários AEM.

Um usuário de formulários AEM pode ser autenticado usando um token SAML obtido. Essa asserção SAML (fragmento xml) pode ser enviada como parte do cabeçalho WS-Security com a chamada de serviço da Web para autenticação de usuário. Normalmente, um aplicativo cliente autenticou um usuário, mas não armazenou as credenciais do usuário. (Ou o usuário fez logon nesse cliente por meio de um mecanismo diferente do uso de um nome de usuário e senha.) Nessa situação, o aplicativo cliente tem que invocar o AEM Forms e representar um usuário específico que tem permissão para invocar o AEM Forms.

Para representar um usuário específico, chame o método `AuthenticationManager.getAuthResultOnBehalfOfUser` usando um serviço Web. Este método retorna uma instância `AuthResult` que contém a asserção SAML para esse usuário.

Em seguida, use essa asserção SAML para invocar qualquer serviço que exija autenticação. Essa ação envolve enviar a asserção como parte do cabeçalho SOAP. Quando uma chamada de serviço da Web é feita com essa asserção, o AEM Forms identifica o usuário como aquele representado por essa asserção. Ou seja, o usuário especificado na asserção é o usuário que está chamando o serviço.

### Uso de classes do Apache Axis e autenticação baseada em SAML {#using-apache-axis-classes-and-saml-based-authentication}

Você pode chamar um serviço AEM Forms por classes de proxy Java que foram criadas usando a biblioteca do Axis. (Consulte [Criação de classes proxy Java usando o Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

Ao usar o AXIS que usa autenticação baseada em SAML, registre o manipulador de solicitação e resposta com o Axis. O Apache Axis chama o manipulador antes de enviar uma solicitação de invocação para o AEM Forms. Para registrar um manipulador, crie uma classe Java que estenda `org.apache.axis.handlers.BasicHandler`.

**Criar um AssertionHandler com o Eixo**

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

Para registrar um manipulador com o Axis, crie um arquivo client-config.wsdd. Por padrão, o Axis procura um arquivo com esse nome. O código XML a seguir é um exemplo de um arquivo client-config.wsdd. Consulte a documentação do Axis para obter mais informações.

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

O código de exemplo a seguir chama um serviço AEM Forms usando autenticação baseada em SAML.

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

### Uso de um assembly cliente .NET e autenticação baseada em SAML {#using-a-net-client-assembly-and-saml-based-authentication}

Você pode chamar um serviço Forms usando um assembly cliente .NET e uma autenticação baseada em SAML. Para fazer isso, você deve usar o Web Service Enhancements 3.0 (WSE). Para obter informações sobre como criar um assembly de cliente .NET que use WSE, consulte [Criando um projeto .NET que use DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>A seção DIME usa o WSE 2.0. Para usar a autenticação baseada em SAML, siga as mesmas instruções especificadas no tópico DIME. No entanto, substitua o WSE 2.0 pelo WSE 3.0. Instale o Web Services Enhancements 3.0 no computador de desenvolvimento e integre-o ao Microsoft Visual Studio .NET. Você pode baixar o 3.0 Web Services Enhancements no [Centro de Download da Microsoft](https://www.microsoft.com/downloads/search.aspx).

A arquitetura do WSE usa tipos de dados Policies, Assertions e SecurityToken. Resumidamente, para uma chamada de serviço da Web, especifique uma política. Uma política pode ter várias asserções. Cada asserção pode conter filtros. Um filtro é chamado em determinados estágios em uma chamada de serviço da Web e, nesse momento, eles podem modificar a solicitação do SOAP. Para obter detalhes completos, consulte a documentação de Melhorias no serviço da Web 3.0.

**Criar a Asserção e o Filtro**

O exemplo de código C# a seguir cria classes de filtro e asserção. Este exemplo de código cria um SamlAssertionOutputFilter. Esse filtro é chamado pela estrutura WSE antes que a solicitação SOAP seja enviada para o AEM Forms.

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

Crie uma classe para representar a asserção SAML. A principal tarefa executada por essa classe é converter valores de dados de string em xml e preservar espaço em branco. Esse xml de asserção é importado posteriormente para a solicitação do SOAP.

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

O código C# a seguir invoca um serviço Forms usando autenticação baseada em SAML.

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

Às vezes, ocorrem problemas ao invocar determinadas operações de serviços da AEM Forms usando serviços da Web. O objetivo desta discussão é identificar esses problemas e fornecer uma solução, se disponível.

### Chamando operações de serviço de forma assíncrona {#invoking-service-operations-asynchronously}

Se você tentar invocar de forma assíncrona uma operação de serviço AEM Forms, como a operação Generate PDF `htmlToPDF`, ocorre um `SoapFaultException`. Para resolver esse problema, crie um arquivo XML de associação personalizada que mapeie o elemento `ExportPDF_Result` e outros elementos em classes diferentes. O XML a seguir representa um arquivo de associação personalizado.

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

Referencie este arquivo XML ao executar a ferramenta JAX-WS (wsimport.exe) usando a opção de linha de comando - `b`. Atualize o elemento `wsdlLocation` no arquivo XML de associação para especificar a URL do AEM Forms.

Para garantir que a invocação assíncrona funcione, modifique o valor da URL do ponto de extremidade e especifique `async=true`. Por exemplo, para arquivos proxy Java criados com JAX-WS, especifique o seguinte para o `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

A lista a seguir especifica outros serviços que precisam de um arquivo de associação personalizado quando chamados de forma assíncrona:

* PDFG3D
* Gerenciador de tarefas
* Gerenciador de aplicativos
* Gerenciador de diretórios
* Distiller
* Rights Management
* Gestão de Documentos

### Diferenças nos servidores de aplicativos J2EE {#differences-in-j2ee-application-servers}

Às vezes, uma biblioteca proxy criada usando um servidor de aplicativos J2EE específico não chama com sucesso o AEM Forms que está hospedado em um servidor de aplicativos J2EE diferente. Considere uma biblioteca de proxy gerada usando o AEM Forms implantada no WebSphere. Esta biblioteca de proxy não pode invocar com êxito os serviços do AEM Forms implantados no Servidor de Aplicativos JBoss.

Alguns tipos de dados complexos do AEM Forms, como o `PrincipalReference`, são definidos de forma diferente quando o AEM Forms é implantado no WebSphere em comparação ao JBoss Application Server. As diferenças nos JDKs usados pelos diferentes serviços da aplicação J2EE são o motivo das diferenças nas definições WSDL. Como resultado, use as bibliotecas de proxy geradas a partir do mesmo servidor de aplicativos J2EE.

### Acesso a vários serviços usando serviços da Web {#accessing-multiple-services-using-web-services}

Devido a conflitos de namespace, os objetos de dados não podem ser compartilhados entre vários WSDLs de serviço. Diferentes serviços podem compartilhar tipos de dados e, portanto, os serviços compartilham a definição desses tipos nos WSDLs. Por exemplo, não é possível adicionar dois assemblies de cliente .NET que contenham um tipo de dados `BLOB` ao mesmo projeto de cliente .NET. Se você tentar fazer isso, ocorrerá um erro de compilação.

A lista a seguir especifica tipos de dados que não podem ser compartilhados entre vários WSDLs de serviço:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Para evitar esse problema, é recomendável qualificar totalmente os tipos de dados. Por exemplo, considere um aplicativo .NET que faça referência ao serviço Forms e ao serviço Signature usando uma referência de serviço. Ambas as referências de serviço conterão uma classe `BLOB`. Para usar uma instância `BLOB`, qualifique totalmente o objeto `BLOB` ao declará-lo. Essa abordagem é mostrada no código de exemplo a seguir. Para obter informações sobre este exemplo de código, consulte [Forms Interativo de Assinatura Digital](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

O código C# a seguir assina um formulário interativo que é renderizado pelo serviço do Forms. O aplicativo cliente tem duas referências de serviço. A instância `BLOB` associada ao serviço Forms pertence ao namespace `SignInteractiveForm.ServiceReference2`. Da mesma forma, a instância `BLOB` associada ao serviço de Assinatura pertence ao namespace `SignInteractiveForm.ServiceReference1`. O formulário interativo assinado é salvo como um arquivo PDF chamado *LoanXFASigned.pdf*.

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
                    //it is necessary to fully qualify the BLOB objects
 
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
 
                    //Specify an XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify an XML form data
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

### Serviços que começam com a letra I produzem arquivos de proxy inválidos {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

O nome de algumas classes de proxy geradas pela AEM Forms está incorreto ao usar o Microsoft .Net 3.5 e o WCF. Esse problema ocorre quando classes de proxy são criadas para IBMFilenetContentRepositoryConnector, IDPSchedulerService ou qualquer outro serviço cujo nome comece com a letra I. Por exemplo, o nome do cliente gerado se houver IBMFileNetContentRepositoryConnector será `BMFileNetContentRepositoryConnectorClient`. A letra I está ausente na classe de proxy gerada.
