---
title: Use o rasterizador de PDF para gerar representações
description: Gere miniaturas e representações de alta qualidade usando a biblioteca Adobe PDF Rasterizer .
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Use PDF Rasterizer {#using-pdf-rasterizer}

Ao fazer upload de arquivos grandes e com uso intenso de conteúdo de PDF ou AI para [!DNL Adobe Experience Manager Assets], a biblioteca padrão pode não gerar uma saída precisa. A biblioteca de PDF pode gerar uma saída mais confiável e precisa em comparação com uma biblioteca padrão. O Adobe recomenda usar a biblioteca PDF Rasterizer para os seguintes cenários:

O Adobe recomenda usar a biblioteca PDF Rasterizer para o seguinte:

* Arquivos AI ou PDF fartos e com uso intenso de conteúdo.
* Arquivos AI e PDF com miniaturas que não são geradas por padrão.
* Arquivos AI com cores do Pantone Matching System (PMS).

As miniaturas e visualizações geradas usando o PDF Rasterizer têm melhor qualidade em comparação à saída predefinida e, portanto, fornecem uma experiência de visualização consistente em todos os dispositivos. A biblioteca Adobe PDF Rasterizer não oferece suporte a nenhuma conversão de espaço de cores. Ele sempre resulta em RGB, independentemente do espaço de cores do arquivo de origem.

1. Instale o pacote PDF Rasterizer em seu [!DNL Adobe Experience Manager] implantação a partir de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >A biblioteca PDF Rasterizer está disponível somente para Windows e Linux.

1. Acesse o [!DNL Assets] console do fluxo de trabalho em `https://[aem_server]:[port]/workflow`. Abrir [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

1. Para impedir a geração de miniaturas e renderizações da web para arquivos PDF e arquivos AI usando os métodos padrão, siga estas etapas:

   * Abra o **[!UICONTROL Processar miniaturas]** e adicionar `application/pdf` ou `application/postscript` no **[!UICONTROL Ignorar Tipos Mime]** no campo **[!UICONTROL Miniaturas]** conforme necessário.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * No **[!UICONTROL Imagem ativada na Web]** guia , adicionar `application/pdf` ou `application/postscript` under **[!UICONTROL Ignorar Lista]** dependendo de suas necessidades.

   ![Configuração para ignorar o processamento de miniaturas em um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra o **[!UICONTROL Rasterizar representação de visualização de imagem do PDF/AI]** e remova o tipo MIME para o qual deseja ignorar a geração padrão de representações de imagem de visualização. Por exemplo, remova o tipo MIME `application/pdf`, `application/postscript`ou `application/illustrator` do **[!UICONTROL Tipos MIME]** lista.

   ![process_arguments](assets/process_arguments.png)

1. Arraste o **[!UICONTROL Manipulador de Rasterizador de PDF]** passe do painel lateral para baixo da **[!UICONTROL Processar miniaturas]** etapa.
1. Configure os seguintes argumentos para a variável **[!UICONTROL Manipulador de Rasterizador de PDF]** etapa:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: 319:319, 140:100, 48:48. Adicione a configuração personalizada de miniatura, se necessário.

   Os argumentos da linha de comando para a `PDFRasterizer` pode incluir o seguinte:

   * `-d`: Sinalizador para permitir uma renderização suave do texto, da arte-final vetorial e das imagens. Cria imagens de melhor qualidade. No entanto, incluir esse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada de forma diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para o PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que o PDF Rasterizer gere renderizações Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações no **[!UICONTROL Imagem ativada na Web]** guia .

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salve o workflow.
1. Para permitir que o PDF Rasterizer processe páginas PDF com bibliotecas PDF, abra o **[!UICONTROL Subconjunto de Processos DAM]** do [!UICONTROL Fluxo de trabalho] console.
1. No painel lateral, arraste a etapa Manipulador de rasterizador de PDF para baixo da **[!UICONTROL Criar representação de imagem ativada para a Web]** etapa.
1. Configure os seguintes argumentos para a variável **[!UICONTROL Manipulador de Rasterizador de PDF]** etapa:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: `319:319`, `140:100`, `48:48`. Adicione a configuração personalizada de miniatura, conforme necessário.

   Os argumentos da linha de comando para a `PDFRasterizer` pode incluir o seguinte:

   * `-d`: Sinalizador para permitir uma renderização suave do texto, da arte-final vetorial e das imagens. Cria imagens de melhor qualidade. No entanto, incluir esse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada de forma diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para o PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que o PDF Rasterizer gere renderizações Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações no **[!UICONTROL Imagem ativada na Web]** guia .

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salve o workflow.
1. Faça upload de um arquivo PDF ou AI para [!DNL Experience Manager Assets]. PDF Rasterizer gera as miniaturas e renderizações da Web para o arquivo.
