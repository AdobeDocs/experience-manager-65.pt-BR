---
title: Use o rasterizador de PDF para gerar execuções de arquivos PDF.
description: Gere miniaturas e execuções de alta qualidade usando a biblioteca do Adobe PDF Rasterizer no [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5d66bf75a6751e41170e6297d26116ad33c2df44
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# Usar o PDF Rasterizer {#using-pdf-rasterizer}

Ao fazer upload de arquivos PDF ou AI grandes e com grande quantidade de conteúdo para [!DNL Adobe Experience Manager Assets], a conversão padrão pode não gerar uma saída precisa. A biblioteca do PDF Rasterizer da Adobe pode gerar uma saída mais confiável e precisa quando comparada à saída de uma biblioteca padrão. A Adobe recomenda usar a biblioteca do PDF Rasterizer para os seguintes cenários:

* Arquivos AI ou PDF com grande quantidade de conteúdo.
* Arquivos AI e arquivos PDF com miniaturas que não são geradas por padrão.
* Arquivos AI com cores Pantone Matching System (PMS).

As miniaturas e pré-visualizações geradas usando o PDF Rasterizer têm melhor qualidade em comparação com a saída predefinida e, portanto, proporcionam uma experiência de visualização consistente em todos os dispositivos. A biblioteca do Adobe PDF Rasterizer não suporta nenhuma conversão de espaço de cor. Sempre resulta em RGB independentemente do espaço de cor do arquivo de origem.

1. Instale o pacote PDF Rasterizer na sua [!DNL Experience Manager] implantação a partir do Compartilhamento [de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)pacotes.

   >[!NOTE]
   >
   >A biblioteca do PDF Rasterizer está disponível somente para Windows e Linux.

1. Acesse o console de [!DNL Assets] fluxo de trabalho em `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM.

1. Para impedir a geração de miniaturas e execuções da Web para arquivos PDF e arquivos AI usando os métodos padrão, siga estas etapas:

   * Abra a etapa **[!UICONTROL Processar miniaturas]** e adicione `application/pdf` ou `application/postscript` no campo **[!UICONTROL Ignorar tipos]** MIME na guia **[!UICONTROL Miniaturas]** , conforme necessário.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Na guia Imagem **[!UICONTROL ativada pela]** Web, adicione `application/pdf` ou `application/postscript` em **[!UICONTROL Ignorar Lista]** , dependendo de seus requisitos.
   ![Configuração para ignorar o processamento de miniaturas para um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra a etapa **[!UICONTROL Rasterizar representação de Pré-visualização]** de imagem PDF/AI e remova o tipo MIME para o qual você deseja ignorar a geração padrão de representações de imagem de pré-visualização. Por exemplo, remova o tipo MIME `application/pdf`, `application/postscript`ou `application/illustrator` da lista **[!UICONTROL MIME Types]** .

   ![process_argumentos](assets/process_arguments.png)

1. Arraste a etapa Manipulador **[!UICONTROL do Rasterizer de]** PDF do painel lateral para baixo da etapa **[!UICONTROL Processar miniaturas]** .
1. Configure os seguintes argumentos para a etapa do **[!UICONTROL PDF Rasterizer Handler]** :

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: 319:319, 140:100, 48:48. Adicione uma configuração de miniatura personalizada, se necessário.
   Os argumentos da linha de comando para o `PDFRasterizer` comando podem incluir o seguinte:

   * `-d`: Sinalizador para ativar a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-p`: Número da página. O valor padrão é todas as páginas. Para indicar todas as páginas, use `*`.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada por quantidade diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para entrada de PDF. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.

1. Para permitir que o PDF Rasterizer gere renderizações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações na guia Imagem **[!UICONTROL ativada pela]** Web.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salve o fluxo de trabalho.

1. Para permitir que o PDF Rasterizer processe páginas PDF com bibliotecas de PDF, abra o modelo **[!UICONTROL DAM Process Subasset]** no console [!UICONTROL Fluxo de trabalho] .

1. No painel lateral, arraste a etapa Manipulador do rasterizador de PDF na etapa **[!UICONTROL Criar representação de imagem]** habilitada para a Web.

1. Configure os seguintes argumentos para a etapa do **[!UICONTROL PDF Rasterizer Handler]** :

   * Tipos MIME: `application/pdf` ou `application/postscript`

   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: `319:319`, `140:100`, `48:48`. Adicione uma configuração de miniatura personalizada, conforme necessário.
   Os argumentos da linha de comando para o `PDFRasterizer` comando podem incluir o seguinte:

   * `-d`: Sinalizador para ativar a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-p`: Número da página. O valor padrão é todas as páginas. `*` indica todas as páginas.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada por quantidade diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para entrada de PDF. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que o PDF Rasterizer gere renderizações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações na guia Imagem **[!UICONTROL ativada pela]** Web.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salve o fluxo de trabalho.
1. Faça upload de um arquivo PDF ou AI para [!DNL Experience Manager Assets]. O PDF Rasterizer gera miniaturas e representações da Web para o arquivo.
