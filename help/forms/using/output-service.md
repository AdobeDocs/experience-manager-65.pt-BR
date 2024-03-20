---
title: Serviço de saída
description: Descreve o Serviço de saída, que faz parte dos Serviços de documento AEM
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services
exl-id: 82b0293a-711f-4769-9b11-b4cff4fec021
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Serviço de saída{#output-service}

## Visão geral {#overview}

O serviço de saída é um serviço OSGi que faz parte dos Serviços de documento AEM. O serviço de saída é compatível com vários formatos de saída e recursos de design de saída do AEM Forms Designer. O serviço de saída pode converter modelos XFA e dados XML para gerar documentos de impressão em vários formatos.

O serviço de saída permite criar aplicativos que permitem:

* Gerar documentos de formulário final preenchendo arquivos de modelo com dados XML.
* Gerar formulários de saída em vários formatos, incluindo fluxos de impressão PDF, PostScript, PCL e ZPL não interativos.
* Gerar PDFs de impressão a partir de PDFs de formulário XFA.
* Gerar documentos PDF, PostScript, PCL e ZPL em massa ao mesclar vários conjuntos de dados com os modelos fornecidos.

>[!NOTE]
>
>O serviço de saída é um aplicativo de 32 bits. No Microsoft Windows, um aplicativo de 32 bits pode usar no máximo 2 GB de memória. O limite também se aplica ao serviço de saída.

## Criação de documentos de formulário não interativos {#creating-non-interactive-form-documents}

![uso de output_modified](assets/usingoutput_modified.png)

Normalmente, você cria modelos usando o AEM Forms Designer. A variável `generatePDFOutput` e `generatePrintedOutput` As APIs do serviço de saída permitem converter diretamente esses templates em vários formatos, incluindo PDF, PostScript, ZPL e PCL.

A variável `generatePDFOutput` a operação gera PDF, enquanto a variável `generatePrintedOutput` A operação gera os formatos PostScript, ZPL e PCL. O primeiro parâmetro de ambas as operações aceita o nome do arquivo de modelo (por exemplo, `ExpenseClaim.xdp`) ou um objeto Documento que contém o modelo. Ao especificar o nome do arquivo de modelo, especifique também a raiz do conteúdo como o caminho para a pasta que contém o modelo. É possível especificar a raiz do conteúdo usando a variável `PDFOutputOptions` ou o `PrintedOutputOptions` parâmetro. Consulte Javadoc para obter detalhes de outras opções que podem ser especificadas usando esses parâmetros.

O segundo parâmetro aceita um documento XML que é mesclado com o modelo ao gerar o documento de saída.

A variável `generatePDFOutput` A operação também pode aceitar um formulário PDF baseado em XFA como entrada e retornar uma versão não interativa do formulário PDF como saída.

## Geração de documentos de formulário não interativos {#generating-non-interactive-form-documents}

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo.

Use o `generatePDFOutputBatch` e `generatePrintedOutputBatch` operações do Serviço de saída para gerar um documento de impressão para cada registro.

Você também pode combinar os registros em um único documento. Ambas as operações usam quatro parâmetros.

O primeiro parâmetro é um Mapa que contém uma string arbitrária como a chave e o nome do arquivo de modelo como valor.

O segundo parâmetro é um Map diferente cujo valor é um objeto Document que contém dados XML. A chave é a mesma especificada para o primeiro parâmetro.

O terceiro parâmetro para `generatePDFOutputBatch` ou `generatePrintedOutputBatch` é do tipo `PDFOutputOptions` ou `PrintedOutputOptions` respectivamente.

Os tipos de parâmetros são os mesmos que os tipos dos parâmetros para o `generatePDFOutput` e `generatePrintedOutput` operações e têm o mesmo efeito.

O quarto parâmetro é do tipo `BatchOptions`, que você usa para especificar se um arquivo separado pode ser gerado para cada registro. O valor padrão desse parâmetro é false.

Ambos `generatePrintedOutputBatch` e `generatePDFOutputBatch` retornar um valor do tipo `BatchResult`. O valor contém uma lista de documentos gerados. Ele também contém um documento de metadados em formato XML que contém informações relacionadas a cada documento gerado.
