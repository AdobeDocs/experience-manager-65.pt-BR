---
title: Converter serviço PDF
description: Use o serviço Adobe Experience Manager Forms ConvertPDF para converter documentos PDF em PostScript ou arquivos de imagem.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services
exl-id: 50c7a385-b56d-4573-932f-1f44eec948f8
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# Converter serviço PDF {#convertpdf-service}

## Visão geral {#overview}

O serviço Convert PDF converte documentos PDF para PostScript ou arquivos de imagem (JPEG, JPEG 2000, PNG e TIFF). A conversão de um documento PDF em PostScript é útil para impressão autônoma baseada em servidor em qualquer impressora PostScript. A conversão de um documento de PDF em um arquivo de TIFF de várias páginas é prática ao arquivar documentos em sistemas de gerenciamento de conteúdo que não sejam compatíveis com documentos de PDF.

Você pode fazer o seguinte com o serviço Converter PDF:

* Converta documentos PDF em PostScript. Ao converter em PostScript, você pode usar a operação de conversão para especificar o documento de origem e se deseja converter em PostScript nível 2 ou 3. O documento PDF que você converter em um arquivo PostScript deve ser não interativo.
* Converta documentos PDF para formatos de imagem JPEG, JPEG 2000, PNG e TIFF. Ao converter para qualquer um desses formatos de imagem, você pode usar a operação de conversão para especificar o documento de origem e uma especificação de opções de imagem. A especificação contém várias preferências, como formato de conversão de imagem, resolução de imagem e conversão de cor.

## Configurar propriedades do serviço   {#properties}

Você pode usar o **Serviço ConvertPDF do AEMFD** no Console AEM para configurar as propriedades desse serviço. O URL padrão do console AEM é `https://[host]:'port'/system/console/configMgr`.

## Uso do serviço {#using-the-service}

O serviço ConvertPDF fornece as duas APIs a seguir:

* **[toPS](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**: converte um documento PDF em um arquivo PostScript.

* **[toImage](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**: converte um documento PDF em um arquivo de imagem. Os formatos de imagem compatíveis são JPEG, JPEG2000, PNG e TIFF.

### Utilização da API toPS com um JSP ou Servlets {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### Usando a API toImage com um JSP ou Servlets {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### Utilização do serviço ConvertPDF com fluxos de trabalho de AEM {#using-convertpdf-service-with-aem-workflows}

A execução do serviço ConvertPDF a partir de um fluxo de trabalho é semelhante à execução a partir de JSP/Servlet.

A única diferença é executar o serviço a partir do JSP/Servlet o objeto do documento recupera automaticamente uma instância do objeto ResourceResolver do objeto ResourceResolverHelper. Esse mecanismo automático não funciona quando o código é chamado de um workflow. Para um fluxo de trabalho, passe explicitamente uma instância do objeto ResourceResolver para o construtor de classe Document. Em seguida, o objeto Documento usa o objeto ResourceResolver fornecido para ler o conteúdo do repositório.

O processo de fluxo de trabalho de amostra a seguir converte o documento de entrada em um documento PostScript. O código é escrito no ECMAScript e o documento é passado como carga de fluxo de trabalho:

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

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

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
