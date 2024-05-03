---
title: APIs faturáveis de relatórios de transação para o AEM Forms no JEE.
description: Lista de todas as APIs que são contabilizadas como transações para o AEM Forms no JEE.
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 3%

---

# APIs faturáveis de relatórios de transações para o AEM Forms no JEE {#transaction-reports-billable-apis}

O AEM Forms no JEE fornece várias APIs para enviar, processar e renderizar documentos. Algumas APIs são contabilizadas como transações e outras são livres para uso. Este documento fornece uma lista de todas as APIs contabilizadas como transações. Estes são alguns cenários comuns em que uma API faturável é usada:

* Conversão de um documento de um formato para outro
* Nivelamento de um documento PDF dinâmico
* Mesclar um documento PDF interativo com outro documento PDF

As APIs de faturamento não levam em conta o número de páginas, o comprimento de um documento ou formulário ou o formato final do documento renderizado.
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

Abaixo está a lista de APIs faturáveis do JEE. Encontre a lista de [APIs faturáveis para o AEM Forms no OSGi](/help/forms/using/transaction-reports-billable-apis.md).

## APIs de serviços de documento faturáveis {#billable-document-services-apis}

### Gerar serviço de PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
   <tr>
   <td><a>CriarPDF</a></td>
   <td>Cria Adobe PDF para tipos de arquivos compatíveis.</td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>CriarPDF3</a></td>
   <td>Cria Adobe PDF para tipos de arquivos compatíveis. </td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>Converte o arquivo HTML em Adobe PDF. </td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>Exporta PDF para tipos de arquivos suportados. </td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>Exporta PDF para tipos de arquivos suportados.</p> </td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>ExportarPDF3</a></td>
   <td>Exporta PDF para tipos de arquivos suportados.</td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>ArquivoHtmlParaPDF</a></td>
   <td>Converte o arquivo de HTML em PDF.</td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>Converte o arquivo de HTML em PDF.</td>
   <td>Conversão<br /> </td>
  </tr>
  <tr>
   <td><a>OtimizarPDF</a></td>
   <td>Otimiza o PDF para reduzir o tamanho do arquivo, removendo metadados desnecessários sem afetar a qualidade.</td>
   <td>Conversão<br /> </td>
  </tr>
 </tbody>
</table>

### Serviço DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td><a>Assinar/Certificar</a><br /> </td>
   <td>Essa API permite que você proteja seu documento. Você pode usar a API para assinar e certificar um documento PDF.</td>
   <td>Conversão</td>
  </tr>
 </tbody>
</table>


### Serviço Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
  <tr>
   <td><a>CriarPDF</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Conversão</td>
  </tr>
  <tr>
   <td><a>CriarPDF2</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Conversão</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Serviço de saída {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos renderizados</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos renderizados</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos renderizados</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos renderizados</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos renderizados</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>Converte um conjunto de documentos XDP e PDF em um conjunto de formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Conversão de documentos</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Converter serviço de PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>Converte um documento PDF em uma lista de documentos de imagem. Os formatos de imagem compatíveis são JPEG, JPEG2K, PNG e TIFF.</td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>Converte um arquivo de PDF simples em formato PostScript usando as opções especificadas na especificação da opção.</td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>toSWF</a></td>
   <td>Converte um arquivo de PDF simples em formato SWF usando as opções especificadas na especificação de opções.</td>
   <td>Conversão de documentos</td>
  </tr>
 </tbody>
</table>

### Serviço Forms com código de barras {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td><a>decodificar</a></td>
   <td>Decodifica todos os códigos de barras em um objeto Documento e retorna um objeto org.w3c.dom.Document que contém os dados recuperados do código de barras.</td>
   <td>Conversão de documentos</td>
  </tr>
 </tbody>
</table>

### Serviço de Assembler {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td><a>invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um objeto AssemblerResult contendo os documentos resultantes. </td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>Executa o documento DDX especificado e retorna um objeto AssemblerResult contendo os documentos resultantes. </td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Conversão de documentos</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Conversão de documentos</td>
  </tr>
 </tbody>
</table>

O uso da API de chamada é contado como uma transação, quando você executa uma ou mais das seguintes operações:
1. Conversão de formatos sem PDF para formatos PDF. Por exemplo, a conversão do formato XDP para o formato PDF.<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversão do formato PDF para o formato PDF/A.
1. Conversão do formato PDF para formatos não PDF. Os exemplos englobam a transformação do formato PDF para o formato Imagem ou a conversão do formato PDF para Texto.

>[!NOTE]
>
>* A API de chamada do serviço do montador pode chamar internamente uma API faturável de outro serviço, dependendo da entrada. Então, o `invoke API` pode ser contabilizado como nenhuma, uma única ou várias transações. O número de transações contadas depende da entrada e das APIs internas chamadas.
>* Um único documento de PDF produzido usando o serviço de montagem, como `invoke` e `invokeDDX`, podem ser contabilizadas como nenhuma, uma única ou várias transações. O número de transações contadas depende do valor fornecido <!--DDX--> código.

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## APIs de captura de dados faturáveis {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Forms {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>Envia formulário.</td>
   <td>Formulários enviados</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>Envia formulário.</td>
   <td>Formulários enviados</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>Envia formulário.</td>
   <td>Forms Renderizado</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## Artigos relacionados

* [Ativação e exibição do relatório de transações do AEM Forms no JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Registrar uma transação para APIs de componente personalizado para AEM Forms no JEE](/help/forms/using/record-transaction-custom-component-jee.md)
