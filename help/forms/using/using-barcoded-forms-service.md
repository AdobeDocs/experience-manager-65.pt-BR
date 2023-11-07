---
title: Serviço Forms com código de barras
description: Use o serviço AEM Forms Barcoded Forms para extrair dados de imagens eletrônicas de códigos de barras.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Serviço Forms com código de barras{#barcoded-forms-service}

## Visão geral {#overview}

O serviço Forms com código de barras extrai dados de imagens eletrônicas de códigos de barras. O serviço aceita arquivos TIFF e PDF que incluem um ou mais códigos de barras como entrada e extrai os dados do código de barras. Os dados do código de barras podem ser formatados de várias maneiras, incluindo XML, string delimitada ou qualquer formato personalizado criado com o JavaScript.

O serviço Forms com código de barras é compatível com o seguinte **bidimensional (2D)** simbologias fornecidas como documentos de TIFF ou PDF digitalizados:

* PDF417
* Matriz de dados
* Código QR

O serviço também oferece suporte ao seguinte **unidimensional** simbologias fornecidas como documentos de TIFF ou PDF digitalizados:

* Codabar
* Code128
* Código 3 de 9
* EAN13
* EAN8

Você pode usar o serviço Forms com código de barras para realizar as seguintes tarefas:

* Extrair dados de código de barras de imagens de código de barras (TIFF ou PDF). Os dados são armazenados como texto delimitado.
* Converter dados de texto delimitados em XML (XDP ou XFDF). Os dados XML são mais fáceis de analisar do que o texto delimitado. Além disso, os dados no formato XDP ou XFDF podem ser usados como entrada para outros serviços no AEM Forms.

Para cada código de barras em uma imagem, o serviço Forms com código de barras localiza o código de barras, decodifica-o e extrai os dados. O serviço retorna os dados do código de barras (usando a codificação de entidade quando necessário) em um elemento de conteúdo de um documento XML. Por exemplo, a seguinte imagem de TIFF digitalizada de um formulário contém dois códigos de barras:

![exemplo](assets/example.png)

O serviço Forms com código de barras retorna o seguinte documento XML após decodificar os códigos de barras:

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## Considerações para o serviço {#considerations}

### Fluxos de trabalho que usam formulários com código de barras {#workflows-that-use-barcoded-forms}

Os autores de formulários criam formulários interativos com códigos de barras usando o Designer. (Consulte [Ajuda do Designer](https://www.adobe.com/go/learn_aemforms_designer_63_pt).) Quando um usuário preenche um formulário com código de barras usando o Adobe Reader ou o Acrobat, o código de barras é atualizado automaticamente para codificar os dados do formulário.

O serviço Forms com código de barras é útil para converter dados existentes em papel em formato eletrônico. Por exemplo, quando um formulário com código de barras é preenchido e impresso, a cópia impressa pode ser digitalizada e usada como entrada para o serviço Forms com código de barras.

Os endpoints de pasta monitorados normalmente são usados para iniciar aplicativos que usam o serviço Forms com código de barras. Por exemplo, scanners de documentos podem salvar imagens de TIFF ou PDF de formulários com código de barras em uma pasta monitorada. O endpoint da pasta monitorada passa as imagens para o serviço para decodificação.

### Formatos de codificação e decodificação recomendados {#recommended-encoding-and-decoding-formats}

Os autores de formulários com código de barras são incentivados a usar um formato simples e delimitado (como delimitado por tabulação) ao codificar dados em códigos de barras. Além disso, evite usar Retorno de carro como delimitador de campo. O Designer fornece uma seleção de codificações delimitadas que geram automaticamente scripts JavaScript para codificar códigos de barras. Os dados decodificados têm os nomes de campo na primeira linha e os valores na segunda linha, com guias entre cada campo.

Ao decodificar códigos de barras, especifique o caractere usado para delimitar campos. O caractere especificado para decodificação deve ser o mesmo caractere usado para codificar o código de barras. Por exemplo, ao usar o formato delimitado por tabulação recomendado, a operação Extrair em XML deve usar o valor padrão Tab para o delimitador de campo.

### Conjuntos de caracteres especificados pelo usuário {#user-specified-character-sets}

Quando os autores de formulários adicionam objetos de código de barras a seus formulários usando o Designer, eles podem especificar uma codificação de caracteres. As codificações reconhecidas são UTF-8, ISO-8859-1, ISO-8859-2, ISO-8859-7, Shift-JIS, KSC-5601, Big-Five, GB-2312, UTF-16. Por padrão, todos os dados são codificados em códigos de barras como UTF-8.

Ao decodificar códigos de barras, você pode especificar a codificação do conjunto de caracteres a ser usada. Para garantir que todos os dados sejam decodificados corretamente, especifique o mesmo conjunto de caracteres que o autor do formulário especificou quando o formulário foi criado.

### Limitações da API {#api-limitations}

Ao usar as APIs do BCF, considere as seguintes limitações:

* Os formulários dinâmicos não são suportados.
* Os formulários interativos não são decodificados corretamente, a menos que estejam nivelados.
* Os códigos de barras 1-D devem conter apenas valores alfanuméricos (se houver suporte). Códigos de barras 1D contendo símbolos especiais não são decodificados.

### Outras limitações {#other-limitations}

Além disso, considere as seguintes limitações ao usar o serviço Forms com código de barras:

* O serviço oferece suporte total a AcroForms e formulários estáticos que contêm códigos de barras 2D salvos usando o Adobe Reader ou o Acrobat. No entanto, para códigos de barras 1D, nivele o formulário ou forneça-o como PDF ou documento TIFF digitalizado.
* Os formulários XFA dinâmicos não são totalmente compatíveis. Para decodificar corretamente códigos de barras 1D e 2D em um formulário dinâmico, nivele o formulário ou forneça-o como um documento PDF ou TIFF digitalizado.

Além disso, o serviço pode decodificar qualquer código de barras que use a simbologia compatível se as limitações acima forem observadas. Para obter mais informações sobre como criar formulários com código de barras interativos, consulte [Ajuda do Designer](https://www.adobe.com/go/learn_aemforms_designer_63_pt).

## Configurar propriedades do serviço   {#configureproperties}

Você pode usar o **Serviço Forms com código de barras AEMFD** no Console AEM para configurar as propriedades desse serviço. O URL padrão do console AEM é `https://[host]:'port'/system/console/configMgr`.

## Uso do serviço {#using}

O Serviço Forms com código de barras fornece as duas APIs a seguir:

* **[decodificar](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: decodifica todos os códigos de barras disponíveis em um documento de PDF de entrada ou imagem TIFF. Ele retorna outro documento XML que contém dados recuperados de todos os códigos de barras disponíveis no documento ou na imagem de entrada.

* **[extractToXML](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**: converta dados decodificados usando a API de decodificação em dados XML. Esses dados XML podem ser mesclados com um formulário XFA. Ele retorna uma lista de documentos XML, um para cada código de barras.

### Usando o Serviço BCF com um JSP ou Servlets {#using-bcf-service-with-a-jsp-or-servlets}

O código de amostra a seguir decodifica um código de barras em um documento e salva o XML de saída no disco.

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // See Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // See javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### Utilização do serviço BCF com fluxos de trabalho de AEM {#using-the-bcf-service-with-aem-workflows}

A execução do serviço Forms com código de barras a partir de um fluxo de trabalho é semelhante à execução do serviço a partir de JSP/Servlet. A única diferença é executar o serviço a partir do JSP/Servlet o objeto do documento recupera automaticamente uma instância do objeto ResourceResolver do objeto ResourceResolverHelper. Esse mecanismo automático não funciona quando o código é chamado de um workflow.

Para um fluxo de trabalho, passe explicitamente uma instância do objeto ResourceResolver para o construtor de classe Document. Em seguida, o objeto Documento usa o objeto ResourceResolver fornecido para ler o conteúdo do repositório.

O processo de fluxo de trabalho de amostra a seguir decodifica um código de barras em um documento e salva o resultado em disco. O código é escrito no ECMAScript e o documento é passado como carga de fluxo de trabalho:

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```
