---
title: APIs faturáveis dos relatórios de transação
seo-title: Transaction Reports Billable APIs
description: Lista de todas as APIs que são contabilizadas como transações
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 7%

---

# APIs faturáveis dos relatórios de transação{#transaction-reports-billable-apis}

O AEM Forms fornece várias APIs para enviar formulários, processar documentos e renderizar documentos. Algumas APIs são contabilizadas como transações e outras podem ser usadas livremente. Este documento fornece uma lista de todas as APIs que são contabilizadas como transações em um relatório de transações. Veja alguns cenários comuns em que uma API faturável é usada:

* Envio de um formulário adaptável, formulário HTML5 e conjunto de formulários
* Renderização de uma versão impressa ou da Web de uma comunicação interativa
* Converter um documento de um formato para outro
* Nivelar um documento de PDF dinâmico
* Gerar um Documento de Registro
* Mesclar um documento PDF interativo com outro documento PDF
* Uso da etapa de atribuição de tarefa e etapas de serviços de documento de AEM Workflows
* Uso de formulários adaptáveis em um formulário adaptável

As APIs de faturamento não contabilizam o número de páginas, o comprimento de um documento ou formulário ou o formato final do documento renderizado. Um relatório de transações divide as transações em duas categorias: Documentos renderizados e Forms enviado.

* **Forms Enviada:** Quando os dados são enviados de qualquer tipo de formulário criado com o AEM Forms e os dados são enviados para qualquer repositório de armazenamento de dados ou banco de dados é considerado envio de formulário. Por exemplo, o envio de um formulário adaptável, HTML5 Form, PDF forms e conjunto de formulários são considerados como formulários enviados. Cada formulário em um conjunto de formulários é considerado um envio. Por exemplo, se um conjunto de formulários tiver 5 formulários, quando o conjunto de formulários for enviado, o serviço de relatório de transações o contará como 5 envios.

* **Documentos renderizados:** Gerar um documento combinando um modelo e dados, assinando ou certificando digitalmente um documento, usando APIs de serviços de documento faturáveis para serviços de documento ou convertendo um documento de um formato para outro são contabilizados como documentos renderizados.

>[!NOTE]
>
>A interface do usuário de Relatórios de transação exibe três categorias: Forms Enviado, Documentos Renderizados e Documentos Processados. Tanto os documentos renderizados quanto os documentos processados são contabilizados como Documentos renderizados.

## APIs de serviços de documento faturáveis {#billable-document-services-apis}

### Gerar serviço de PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converte o Adobe PDF em tipos de arquivos suportados. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converte o Adobe PDF em tipos de arquivos suportados. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converte o Adobe PDF em tipos de arquivos suportados. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Cria PDF a partir de HTML pages.</p> </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Cria PDF a partir de URLs que apontam para uma página HTML.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Cria PDF a partir de URLs que apontam para uma página HTML.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">otimizePDF</a></td>
   <td>Otimiza o PDF para reduzir o tamanho do arquivo, removendo metadados desnecessários sem afetar a qualidade.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Serviço Distiller {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos compatíveis.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Documento do Serviço de Registro (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">renderizar</a></td>
   <td>Chama o método de renderização especificado para gerar um documento de registro usando parâmetros fornecidos.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Serviço de saída {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Une dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Une dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Une dados e modelos para criar um conjunto de documentos PDF.</td>
   <td>Documentos processados</td>
   <td> A API generatePDFOutputBatch combina um modelo de formulário a um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatório de transações conta cada registro como uma representação de PDF separada. <br> Você pode usar o <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> sinalizador para combinar várias representações em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma representação de PDF separada. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte um conjunto de documentos XDP e PDF em um conjunto de formatos de arquivo PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documentos processados</td>
   <td> A API generatePDFOutputBatch combina um modelo de formulário a um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatório de transações conta cada registro como uma representação de PDF separada. <br> Você pode usar o <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> sinalizador para combinar várias representações em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma representação de PDF separada. </td>
  </tr>
 </tbody>
</table>

### Serviço do Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renderiza o PDF Form a partir de modelos XDP. Os modelos XP são criados no Forms Designer.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extrai dados de um formulário PDF ou modelos XDP</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Converter serviço de PDF {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converte um documento PDF em uma lista de documentos de imagem. Os formatos de imagem suportados são JPEG, JPEG2K, PNG e TIFF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converte um arquivo de PDF simples em formato PostScript usando as opções especificadas na especificação da opção.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Serviço Forms com código de barras {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decodificação</a></td>
   <td>Decodifica todos os códigos de barras em um objeto de Documento e retorna um objeto org.w3c.dom.Document que contém dados recuperados do código de barras.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Serviço de Assembler {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> objeto contendo os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>As seguintes operações não são contabilizadas como transações:
    <ul>
     <li>Criação de pacotes ou portfólio</li>
     <li>Como configurar vários XDPs </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> objeto contendo os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>Todos os formatos de arquivo de entrada que os serviços PDF Generator, Forms e Output suportam, o serviço Assembler suporta todos esses formatos como formatos de arquivo de saída. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* A API invoke do serviço de montagem pode chamar internamente uma API faturável de outro serviço, dependendo da entrada. Portanto, a API de chamada pode ser contabilizada como nenhuma, única ou várias transações. O número de transações contadas depende da entrada e das APIs internas chamadas.
>* Um único documento de PDF produzido usando o serviço de montagem pode ser contabilizado como nenhuma, única ou várias transações. O número de transações contadas depende do código DDX fornecido.
>


### Serviço Utilitário PDF  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">conversionPDFtoXDP</a></td>
   <td>Converte um documento PDF em um arquivo XDP. Para que um documento do PDF seja convertido com êxito em um arquivo XDP, o documento do PDF deve conter um fluxo XFA no dicionário do AcroForm.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## APIs de captura de dados faturáveis {#billable-data-capture-apis}

Todos os eventos de envio de formulários adaptáveis, HTML5 Forms e conjunto de formulários são contabilizados como transações. Por padrão, o envio de um Formulário PDF não é contabilizado como uma transação. Use o [API do gravador de transações](record-transaction-custom-implementation.md) para registrar um envio de PDF forms como uma transação.

### Formulários adaptáveis {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso </p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um formulário adaptável</td>
   <td>Envia um formulário adaptável para a ação de envio configurada. </td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>Envios bem-sucedidos de uma ou duas transações. O número de transações contadas depende do tipo de ação de envio usada para envio. Por exemplo, o envio de PDF por email para enviar contas de ação para duas contagens de transações. Uma transação para envio de formulário e outra para PDF gerada usando o serviço Document of Record (DOR) . </li>
     <li>O uso do formulário adaptável em um formulário adaptável (Adaptive Form Form Forset) conta somente uma transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Formulários HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso </p> </td>
   <td>Descrição </td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um formulário HTML5</td>
   <td>Envia um Formulário HTML5 para enviar o URL configurado no formulário.</td>
   <td>Formulários enviados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Conjunto de formulários {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um conjunto de formulários</td>
   <td>Envia o formulário definido para a URL de envio configurada no conjunto de formulários.</td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>O uso do formulário adaptável em um formulário adaptável (Adaptive Form Form Forset) conta somente uma transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
     <li>Cada formulário em um conjunto de formulários HTML5 Forms é contabilizado como uma transação separada. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Comunicação interativa faturável e fluxos de trabalho de AEM centrados em formulários nas APIs OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Atribua etapas de tarefas e serviços de documento de Fluxos de trabalho de AEM centrados em formulários no OSGi e todas as representações de comunicação interativa e são contabilizadas como transações. A visualização de uma comunicação interativa na instância do autor e a visualização na instância de publicação usando a interface do usuário do agente não são contabilizadas como transações. Se uma etapa do fluxo de trabalho contabilizar uma transação e o fluxo de trabalho não for concluído, a contagem de transações não será revertida.

### Comunicação interativa - Canal da Web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Renderização de um canal da Web</td>
   <td>Abre a versão da Web de uma comunicação interativa.</td>
   <td>Documentos renderizados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Comunicação interativa - Canal de impressão {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">renderizar</a> (converter em PDF)</td>
   <td>Gera a versão PDF de uma comunicação interativa.</td>
   <td>Documentos renderizados</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Fluxos de trabalho de AEM centrados em formulários no OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de uma etapa Atribuir tarefa</td>
   <td>Formulários enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envio de um ponto de partida do aplicativo de fluxo de trabalho </td>
   <td>Formulários enviados</td>
   <td> </td>
  </tr>
  <tr>
   <td>Envio de uma comunicação interativa (Canal de impressão) da interface do agente para um workflow</td>
   <td>Documentos renderizados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registro de APIs faturáveis como transações do código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Ações como enviar um Formulário PDF, usar a interface do usuário do agente para visualizar uma comunicação interativa, usar o envio de formulário não padrão e implementações personalizadas não são contabilizadas como transações. O AEM Forms fornece uma API para registrar ações como transações. Você pode chamar a API das implementações personalizadas para [registrar uma transação](/help/forms/using/record-transaction-custom-implementation.md).

## Artigos relacionados {#related-articles}

* [Visão geral dos relatórios de transação](../../forms/using/transaction-reports-overview.md)
* [Exibindo e Noções Gerais de Relatórios de Transações](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
