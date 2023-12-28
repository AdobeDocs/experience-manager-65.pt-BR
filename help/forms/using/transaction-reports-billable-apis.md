---
title: APIs de relatórios de transação faturáveis
description: Lista de todas as APIs contabilizadas como transações
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
source-git-commit: 744cfcee691ea71f33cd56509f65d4f640d4c6e3
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 7%

---

# APIs de relatórios de transação faturáveis{#transaction-reports-billable-apis}

O AEM Forms fornece várias APIs para enviar formulários, processar documentos e renderizar documentos. Algumas APIs são contabilizadas como transações e outras são livres para uso. Este documento fornece uma lista de todas as APIs que são contabilizadas como transações em um relatório de transações. Estes são alguns cenários comuns em que uma API faturável é usada:

* Envio de um formulário adaptável, formulário HTML5 e conjunto de formulários
* Renderização de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato para outro
* Nivelamento de um documento PDF dinâmico
* Gerar um documento de registro
* Mesclar um documento PDF interativo com outro documento PDF
* Usando a etapa atribuir tarefa e as etapas serviços de documento dos fluxos de trabalho do AEM
* Uso de formulário adaptável em um formulário adaptável

As APIs de faturamento não levam em conta o número de páginas, o comprimento de um documento ou formulário ou o formato final do documento renderizado. Um relatório de transações divide as transações em duas categorias: Documentos Renderizados e Forms Submetidos.

* **Forms enviado:** Quando os dados são enviados de qualquer tipo de formulário criado com o AEM Forms e os dados são enviados para qualquer repositório ou banco de dados de armazenamento de dados, é considerado o envio do formulário. Por exemplo, o envio de um formulário adaptável, o Formulário HTML, os PDF forms e o conjunto de formulários são contabilizados como formulários enviados. Cada formulário em um conjunto de formulários é considerado um envio. Por exemplo, se um conjunto de formulários tiver 5 formulários, quando o conjunto for enviado, o serviço de relatório de transações o contará como 5 envios.

* **Documentos renderizados:** Gerar um documento combinando um modelo e dados, assinando ou certificando digitalmente um documento, usando uma API de serviços de documento faturável para serviços de documento ou convertendo um documento de um formato para outro são considerados documentos renderizados.

>[!NOTE]
>
>A interface dos Relatórios de Transação exibe três categorias: Forms Submetido, Documentos Renderizados e Documentos Processados. Tanto os Documentos renderizados quanto os Documentos processados são contabilizados como Documentos renderizados.

## APIs de serviços de documento faturáveis {#billable-document-services-apis}

### Gerar serviço de PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
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
   <td>Converte o Adobe PDF em tipos de arquivos compatíveis. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converte o Adobe PDF em tipos de arquivos compatíveis. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converte o Adobe PDF em tipos de arquivos compatíveis. </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Cria PDF a partir de páginas de HTML.</p> </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Cria PDF a partir de URLs que apontam para uma página de HTML.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Cria PDF a partir de URLs que apontam para uma página de HTML.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">otimizarPDF</a></td>
   <td>Otimiza o PDF para reduzir o tamanho do arquivo, removendo metadados desnecessários sem afetar a qualidade.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
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
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-" target="_blank">secureDocument</a><br /> </td>
   <td>Essa API permite que você proteja seu documento. Você pode usar a API para assinar, certificar, estender o leitor ou criptografar um documento PDF.</td>
   <td>Documentos processados</td>
   <td>Somente assinar e certificar a operação do secureDocument são cobrados.</td>
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

### Documento do serviço de registro (serviço DoR) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">renderizar</a></td>
   <td>Chama o método de renderização especificado para gerar um documento de registro usando os parâmetros fornecidos.</td>
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
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>Mescla dados e modelos para criar um conjunto de documentos PDF.</td>
   <td>Documentos processados</td>
   <td> A API generatePDFOutputBatch combina um modelo de formulário com um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatório de transações conta cada registro como uma representação de PDF separada. <br> Você pode usar o <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> sinalizador para combinar várias representações em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma representação de PDF separada. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte um conjunto de documentos XDP e PDF em um conjunto de formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> A API generatePDFOutputBatch combina um modelo de formulário com um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatório de transações conta cada registro como uma representação de PDF separada. <br> Você pode usar o <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> sinalizador para combinar várias representações em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma representação de PDF separada. </td>
  </tr>
 </tbody>
</table>

### Serviço do Forms {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renderiza o formulário de PDF a partir de modelos XDP. Os modelos do XP são criados no Forms Designer.</td>
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
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converte um documento PDF em uma lista de documentos de imagem. Os formatos de imagem compatíveis são JPEG, JPEG2K, PNG e TIFF.</td>
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
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decodificar</a></td>
   <td>Decodifica todos os códigos de barras em um objeto Documento e retorna um objeto org.w3c.dom.Document que contém os dados recuperados do código de barras.</td>
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
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> objeto que contém os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>As seguintes operações não são contabilizadas como transações:
    <ul>
     <li>Criação de pacotes ou portfólio</li>
     <li>Compilação de vários XDPs </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> objeto que contém os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>Todos os formatos de arquivo de entrada compatíveis com os serviços PDF Generator, Forms e Output, o serviço Assembler é compatível com todos esses formatos como formatos de arquivo de saída. </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

O uso da API de chamada é contado como uma transação, quando você executa uma ou mais das seguintes operações:
1. Conversão de formatos sem PDF para formatos PDF. Por exemplo, a conversão do formato XDP para o formato PDF, atendendo a formas de comunicação interativas e não interativas e a conversão do Word para o PDF.
1. Conversão do formato PDF para o formato PDF/A.
1. Conversão do formato PDF para formatos não PDF. Os exemplos englobam a transformação do formato PDF para o formato Imagem ou a conversão do formato PDF para Texto.

>[!NOTE]
>
>* A API de chamada do serviço do montador pode chamar internamente uma API faturável de outro serviço, dependendo da entrada. Portanto, a API invoke pode ser contabilizada como nenhuma, uma única ou várias transações. O número de transações contadas depende da entrada e das APIs internas chamadas.
>* Um único documento de PDF produzido usando o serviço de montagem pode ser contabilizado como nenhuma, uma única ou várias transações. O número de transações contadas depende do código DDX fornecido.

### Serviço do utilitário PDF  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converte um documento PDF em um arquivo XDP. Para que um documento PDF seja convertido com êxito em um arquivo XDP, o documento PDF deve conter um fluxo XFA no dicionário AcroForm.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## APIs de captura de dados faturáveis {#billable-data-capture-apis}

Todos os eventos de envio de formulários adaptáveis, HTML5 Forms e conjunto de formulários são contabilizados como transações. Por padrão, o envio de um Formulário de PDF não é contabilizado como uma transação. Usar o fornecido [API do gravador de transações](record-transaction-custom-implementation.md) para registrar um envio de PDF forms como uma transação.

### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um formulário adaptável</td>
   <td>Envia um formulário adaptável para a ação de envio configurada. </td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>Os envios bem-sucedidos levam em conta uma ou duas transações. O número de transações contadas depende do tipo de ação de envio usado para envio. Por exemplo, o envio de PDF por meio de ações de envio de email contabiliza duas contagens de transações. Uma transação para envio de formulário e outra para PDF gerado usando o serviço de Documento de registro (DOR). </li>
     <li>O uso do formulário adaptável em um formulário adaptável (conjunto de formulários de formulário adaptável) contabiliza apenas uma transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Formulários HTML5 {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Descrição </td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um formulário HTML5</td>
   <td>Envia um formulário HTML5 para enviar a URL configurada no formulário.</td>
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
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um conjunto de formulários</td>
   <td>Envia o conjunto de formulários para a URL de envio configurada no conjunto de formulários.</td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>O uso do formulário adaptável em um formulário adaptável (conjunto de formulários de formulário adaptável) contabiliza apenas uma transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
     <li>Todos os formulários em um conjunto de formulários HTML5 Forms são considerados uma transação separada. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Comunicação interativa faturável e fluxos de trabalho do AEM centrados em formulário nas APIs OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Atribua etapas de serviços de tarefa e documento de Workflows do AEM centrados em formulário no OSGi e todas as representações de comunicação interativa e são contabilizadas como transações. A visualização de uma comunicação interativa na instância do autor e a visualização na instância de publicação usando a interface do usuário do agente não são contabilizadas como transações. Se uma etapa do fluxo de trabalho contabilizar uma transação e o fluxo de trabalho não for concluído, a contagem da transação não será revertida.

### Comunicação interativa - Canal da Web {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
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
   <td>Categoria do relatório de transações</td>
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

### Workflows do AEM centrados em formulários no OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Submetendo uma etapa Atribuir Tarefa</td>
   <td>Formulários enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envio de um ponto de partida de aplicativo de fluxo de trabalho </td>
   <td>Formulários enviados</td>
   <td> </td>
  </tr>
  <tr>
   <td>Envio de uma comunicação interativa (canal de impressão) da interface do usuário do agente para um fluxo de trabalho</td>
   <td>Documentos renderizados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrando APIs faturáveis como transações para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Ações como enviar um Formulário PDF, usar a interface do usuário do agente para visualizar uma comunicação interativa, usar o envio de formulários não padrão e implementações personalizadas não são contabilizadas como transações. O AEM Forms fornece uma API para registrar ações como transações. Você pode chamar a API de suas implementações personalizadas para [registrar uma transação](/help/forms/using/record-transaction-custom-implementation.md).

## Artigos relacionados {#related-articles}

* [Visão Geral dos Relatórios de Transação](../../forms/using/transaction-reports-overview.md)
* [Visualização e noções básicas de relatórios de transações](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
