---
title: Usar o rasterizador de PDF para gerar representações
description: Gere miniaturas e representações de alta qualidade usando a biblioteca do Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Usar o rasterizador de PDF {#using-pdf-rasterizer}

Ao fazer upload de arquivos grandes de PDF ou AI com grande volume de conteúdo para o [!DNL Adobe Experience Manager Assets], a biblioteca padrão pode não gerar uma saída precisa. A biblioteca PDF Rasterizer Adobe pode gerar uma saída mais confiável e precisa quando comparada à saída de uma biblioteca padrão. A Adobe recomenda o uso da biblioteca PDF Rasterizer para os seguintes cenários:

A Adobe recomenda o uso da biblioteca PDF Rasterizer para o seguinte:

* Arquivos AI ou arquivos PDF pesados e com uso intenso de conteúdo.
* Arquivos AI e arquivos PDF com miniaturas que não são geradas por padrão.
* Arquivos AI com cores do Sistema de correspondência Pantone (PMS).

Miniaturas e visualizações geradas usando o PDF Rasterizer são melhores em qualidade em comparação com a saída pronta para uso e, portanto, fornecem experiência de visualização consistente em todos os dispositivos. A biblioteca do Adobe PDF Rasterizer não é compatível com nenhuma conversão de espaço de cores. Ele sempre gera para o RGB independentemente do espaço de cor do arquivo de origem.

1. Instale o pacote PDF Rasterizer no [!DNL Adobe Experience Manager] implantação de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >A biblioteca PDF Rasterizer está disponível somente para Windows e Linux.

1. Acesse o [!DNL Assets] console de fluxo de trabalho em `https://[aem_server]:[port]/workflow`. Abertura [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

1. Para impedir a geração de miniaturas e representações da Web para arquivos PDF e arquivos AI usando os métodos padrão, siga estas etapas:

   * Abra o **[!UICONTROL Miniaturas do processo]** etapa e adicionar `application/pdf` ou `application/postscript` no **[!UICONTROL Ignorar tipos MIME]** sob o campo **[!UICONTROL Miniaturas]** conforme necessário.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * No **[!UICONTROL Imagem ativada pela Web]** , adicionar `application/pdf` ou `application/postscript` em **[!UICONTROL Ignorar lista]** dependendo das suas necessidades.

   ![Configuração para ignorar o processamento da miniatura para um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra o **[!UICONTROL Rasterizar representação da exibição de imagens do PDF/AI]** e remova o tipo MIME para o qual deseja ignorar a geração padrão de representações de imagem de pré-visualização. Por exemplo, remover o tipo MIME `application/pdf`, `application/postscript`ou `application/illustrator` do **[!UICONTROL Tipos MIME]** lista.

   ![process_arguments](assets/process_arguments.png)

1. Arraste o **[!UICONTROL Manipulador de rasterizador PDF]** passe do painel lateral para abaixo de **[!UICONTROL Miniaturas do processo]** etapa.
1. Configure os seguintes argumentos para o **[!UICONTROL Manipulador de rasterizador PDF]** etapa:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: 319:319, 140:100, 48:48. Adicione a configuração de miniatura personalizada, se necessário.

   Os argumentos de linha de comando para o `PDFRasterizer` pode incluir o seguinte:

   * `-d`: Sinalizador para permitir a renderização suave de texto, arte-final vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: caminho para o PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações no **[!UICONTROL Imagem ativada pela Web]** guia.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salve o workflow.
1. Para permitir que o PDF Rasterizer processe páginas de PDF com bibliotecas de PDF, abra o **[!UICONTROL Subativo do processo DAM]** do [!UICONTROL Fluxo de trabalho] console.
1. No painel lateral, arraste a etapa Manipulador de rasterizador de PDF para a **[!UICONTROL Criar representação de imagem habilitada para a Web]** etapa.
1. Configure os seguintes argumentos para o **[!UICONTROL Manipulador de rasterizador PDF]** etapa:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: `319:319`, `140:100`, `48:48`. Adicione a configuração de miniatura personalizada, conforme necessário.

   Os argumentos de linha de comando para o `PDFRasterizer` pode incluir o seguinte:

   * `-d`: Sinalizador para permitir a renderização suave de texto, arte-final vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: caminho para o PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações no **[!UICONTROL Imagem ativada pela Web]** guia.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salve o workflow.
1. Faça upload de um arquivo PDF ou AI para [!DNL Experience Manager Assets]. O PDF Rasterizer gera as miniaturas e representações da Web para o arquivo.
