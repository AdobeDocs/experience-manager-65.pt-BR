---
title: Relatórios de transação APIs faturáveis
seo-title: Relatórios de transação APIs faturáveis
description: Lista de todas as APIs que são contabilizadas como transações
seo-description: Lista de todas as APIs que são contabilizadas como transações
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 13016df927448d93af86899f746199e1815fdfe7
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 7%

---


# Relatórios de transação APIs faturáveis{#transaction-reports-billable-apis}

A AEM Forms fornece várias APIs para enviar formulários, processar documentos e renderizar documentos. Algumas APIs são contabilizadas como transações e outras são livres de usar. Este documento fornece uma lista de todas as APIs que são contabilizadas como transações em um relatório de transação. Veja alguns cenários comuns em que uma API faturável é usada:

* Envio de um formulário adaptável, formulário HTML5 e conjunto de formulários
* Renderização de uma versão impressa ou da Web de uma comunicação interativa
* Conversão de um documento de um formato para outro
* Achatar um documento PDF dinâmico
* Gerando um Documento de Registro
* Mesclar um documento PDF interativo com outro documento PDF
* Uso da etapa de atribuição de tarefa e das etapas de serviços de doc de Workflows AEM
* Uso de formulário adaptável em um formulário adaptável

As APIs de cobrança não contabilizam o número de páginas, o comprimento de um documento ou formulário ou o formato final do documento renderizado. Um relatório de transação divide as transações em duas categorias: Documentos renderizados e Forms enviado.

* **Forms Submetido:** Quando os dados são enviados de qualquer tipo de formulário criado com a AEM Forms e os dados são enviados para qualquer repositório ou banco de dados do armazenamento de dados é considerado como envio ao formulário. Por exemplo, o envio de um formulário adaptável, formulário HTML5, PDF forms e conjunto de formulários são contabilizados como formulários enviados. Cada formulário em um conjunto de formulários é considerado um envio. Por exemplo, se um conjunto de formulários tiver 5 formulários, quando o conjunto de formulários for submetido, o serviço de relatórios de transação contará como 5 envios.

* **Documentos renderizados:** Gerar um documento combinando um modelo e dados, assinando ou certificando digitalmente um documento, usando APIs de serviços de documento faturáveis para serviços de documento ou convertendo um documento de um formato para outro são contabilizados como documentos renderizados.

>[!NOTE]
>
>A interface do usuário de Relatórios de Transação exibe três categorias: Forms Submetido, Documentos Renderizados e Documentos Processados. Os Documentos Renderizados e os Documentos Processados são contabilizados como Documentos Renderizados.

## APIs de serviços de Documento faturáveis {#billable-document-services-apis}

### Gerar serviço PDF {#generate-pdf-service}

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
   <td>Cria o Adobe PDF a partir de tipos de arquivos suportados.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos suportados.</td>
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
   <td><p>Cria PDF de páginas HTML.</p> </td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Cria PDF a partir de URLs apontando para uma página HTML.</td>
   <td>Documentos processados<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Cria PDF a partir de URLs apontando para uma página HTML.</td>
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
   <td>Cria o Adobe PDF a partir de tipos de arquivos suportados.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Cria o Adobe PDF a partir de tipos de arquivos suportados.</td>
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
   <td> A API generatePDFOutputBatch combina um modelo de formulário com um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatórios de transações conta cada registro como uma representação em PDF separada. <br> Você pode usar o sinalizador <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGeneratemanyFiles</a> para combinar várias execuções em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma execução em PDF separada. </td>
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
   <td>Converte um conjunto de documentos XDP e PDF em um conjunto de formatos PostScript (PS), PCL (Printer Command Language) e ZPL. </td>
   <td>Documentos processados</td>
   <td> A API generatePDFOutputBatch combina um modelo de formulário com um registro e gera um PDF. Quando você processa um lote de registros, o serviço de relatórios de transações conta cada registro como uma representação em PDF separada. <br> Você pode usar o sinalizador <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGeneratemanyFiles</a> para combinar várias execuções em um único arquivo PDF. Independentemente do status do sinalizador, o serviço conta cada registro como uma execução em PDF separada. </td>
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
   <td>Renderiza o formulário PDF a partir de modelos XDP. Os modelos do XP são criados no Forms Designer.</td>
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

### Converter serviço PDF {#convert-pdf-service}

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
   <td>Converte um arquivo PDF simples em formato PostScript usando as opções especificadas na especificação da opção.</td>
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
   <td>Decodifica todos os códigos de barras em um objeto de Documento e retorna um objeto org.w3c.dom.Documento que contém dados recuperados do código de barras.</td>
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
   <td>Executa o documento DDX especificado e retorna um objeto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contendo os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>As seguintes operações não são contabilizadas como transações:
    <ul>
     <li>Criação de pacotes ou portfólio</li>
     <li>Como criar vários XDPs </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">invocar</a></td>
   <td>Executa o documento DDX especificado e retorna um objeto <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> contendo os documentos resultantes. </td>
   <td>Documentos processados</td>
   <td>Todos os formatos de arquivo de entrada suportados pelos serviços de Gerador de PDF, Forms e Saída, o serviço Assembler oferece suporte a todos esses formatos como formatos de arquivo de saída. </td>
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
>* A API de chamada do serviço de montador pode chamar internamente uma API faturável de outro serviço, dependendo da entrada. Portanto, a API de chamada pode ser considerada como nenhuma, única ou várias transações. O número de transações contadas depende da entrada e das APIs internas chamadas.
>* Um único documento PDF produzido usando o serviço de montador pode ser considerado como nenhuma, única ou várias transações. O número de transações contadas depende do código DDX fornecido.

>



### Serviço de utilitário PDF  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transação</td>
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

Todos os eventos de envio de formulários adaptáveis, HTML5 Forms e conjunto de formulários são contabilizados como transações. Por padrão, o envio de um formulário PDF não é contabilizado como uma transação. Use a API [do gravador de](record-transaction-custom-implementation.md) transações fornecida para registrar uma submissão de PDF forms como uma transação.

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
   <td>Enviar um formulário adaptável</td>
   <td>Envia um formulário adaptável para a ação de envio configurada. </td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>Contrapartidas bem-sucedidas para uma ou duas transações. O número de transações contadas depende do tipo de ação de submissão usada para submissão. Por exemplo, enviar PDF por email enviando contas de ação para duas contagens de transações. Uma transação para envio de formulário e outra para PDF gerada usando o serviço Documento de registro (DOR). </li>
     <li>O uso do formulário adaptável em um formulário adaptável (Conjunto de formulários adaptáveis) conta somente uma única transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
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
   <td>Envia um formulário HTML5 para enviar o URL configurado no formulário.</td>
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
   <td>Como enviar um conjunto de formulários</td>
   <td>Envia o conjunto de formulários para o URL de envio configurado no conjunto de formulários.</td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>O uso do formulário adaptável em um formulário adaptável (Conjunto de formulários adaptáveis) conta somente uma única transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
     <li>Cada formulário em um formulário HTML5 Forms define contas como uma transação separada. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Comunicação interativa faturável e Workflows de AEM centrados em forma em APIs OSGi {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Atribua etapas de serviços de tarefa e documento a Workflows de AEM centrados em forma no OSGi e todas as execuções de comunicação interativa e são contabilizadas como transações. A visualização de uma comunicação interativa na instância do autor e a visualização na instância de publicação usando a interface do usuário do agente não são contabilizadas como transações. Se uma etapa do fluxo de trabalho contabilizar uma transação e o fluxo de trabalho não for concluído, a contagem de transações não será revertida.

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
   <td>Como renderizar um canal da Web</td>
   <td>Abre a versão da Web de uma comunicação interativa.</td>
   <td>Documentos renderizados</td>
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

### Workflows de AEM centrados em forma no OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoria do relatório de transação</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Enviando uma etapa Atribuir Tarefa</td>
   <td>Formulários enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Enviar um ponto de partida de aplicativo de fluxo de trabalho </td>
   <td>Formulários enviados</td>
   <td> </td>
  </tr>
  <tr>
   <td>Enviar uma comunicação interativa (Canal de impressão) da interface do usuário do agente para um fluxo de trabalho</td>
   <td>Documentos renderizados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrando APIs faturáveis como transações para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Ações como enviar um formulário PDF, usar a interface do usuário do agente para pré-visualização de uma comunicação interativa, usar envio de formulário não padrão e implementações personalizadas não são contabilizadas como transações. A AEM Forms fornece uma API para registrar ações como transações. Você pode chamar a API de suas implementações personalizadas para [registrar uma transação](/help/forms/using/record-transaction-custom-implementation.md).

## Artigos relacionados {#related-articles}

* [Visão geral dos relatórios de transação](../../forms/using/transaction-reports-overview.md)
* [Exibindo e Entendendo um Relatório de Transação](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)

