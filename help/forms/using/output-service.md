---
title: Serviço de saída
seo-title: Output Service
description: Descreve o Serviço de Saída, que faz parte AEM Serviços de Documento
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# Serviço de saída{#output-service}

## Visão geral {#overview}

O serviço de saída é um serviço OSGi que faz parte AEM Document Services. O serviço de saída oferece suporte a vários formatos de saída e recursos de design de saída do AEM Forms Designer. O serviço de saída pode converter modelos XFA e dados XML para gerar documentos de impressão em vários formatos.

O serviço de saída permite criar aplicativos que permitem:

* Gere documentos de formulário finais preenchendo arquivos de modelo com dados XML.
* Gere formulários de saída em vários formatos, incluindo fluxos de impressão não interativos PDF, PostScript, PCL e ZPL.
* Gerar PDFs de impressão a partir de PDFs de formulário XFA.
* Gere documentos PDF, PostScript, PCL e ZPL em massa ao mesclar vários conjuntos de dados com modelos fornecidos.

>[!NOTE]
>
>O serviço de saída é um aplicativo de 32 bits. No Microsoft Windows, um aplicativo de 32 bits pode usar no máximo 2 GB de memória. O limite também se aplica ao serviço de saída.

## Criação de documentos de formulário não interativos {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

Normalmente, você cria modelos usando o AEM Forms Designer. O `generatePDFOutput` e `generatePrintedOutput` As APIs do serviço de Saída permitem converter esses modelos diretamente em vários formatos, incluindo PDF, PostScript, ZPL e PCL.

O `generatePDFOutput` A operação gera PDF, enquanto a variável `generatePrintedOutput` A operação gera formatos PostScript, ZPL e PCL. O primeiro parâmetro de ambas as operações aceita o nome do arquivo de modelo (por exemplo, `ExpenseClaim.xdp`) ou um objeto Document que contém o modelo. Ao especificar o nome do arquivo de modelo, especifique também a raiz de conteúdo como caminho para a pasta que contém o modelo. Você pode especificar a raiz do conteúdo usando a variável `PDFOutputOptions` ou `PrintedOutputOptions` parâmetro. Consulte Javadoc para obter detalhes sobre outras opções que você pode especificar usando esses parâmetros.

O segundo parâmetro aceita um documento XML que é unido ao template ao gerar o documento de saída.

O `generatePDFOutput` também pode aceitar um formulário PDF baseado em XFA como entrada e retornar uma versão não interativa do formulário PDF como saída.

## Geração de documentos de formulário não interativos {#generating-non-interactive-form-documents}

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo.

Use o `generatePDFOutputBatch` e `generatePrintedOutputBatch` operações do serviço Output para gerar um documento de impressão para cada registro.

Também é possível combinar os registros em um único documento. Ambas as operações têm quatro parâmetros.

O primeiro parâmetro é um Mapa que contém uma string arbitrária como a chave e o nome do arquivo de modelo como valor.

O segundo parâmetro é um Mapa diferente cujo valor é um objeto de Documento que contém dados XML. A chave é a mesma especificada para o primeiro parâmetro.

O terceiro parâmetro para `generatePDFOutputBatch` ou `generatePrintedOutputBatch` é do tipo `PDFOutputOptions` ou `PrintedOutputOptions` respectivamente.

Os tipos de parâmetros são iguais aos tipos de parâmetros para a variável `generatePDFOutput` e `generatePrintedOutput` e têm o mesmo efeito.

O quarto parâmetro é do tipo `BatchOptions`, que você usa para especificar se um arquivo separado pode ser gerado para cada registro. O valor padrão desse parâmetro é false.

Ambos `generatePrintedOutputBatch` e `generatePDFOutputBatch` retornar um valor do tipo `BatchResult`. O valor contém uma lista de documentos gerados. Ele também contém um documento de metadados no formato XML que contém informações relacionadas a cada documento gerado.
