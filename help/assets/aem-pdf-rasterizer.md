---
title: Usar o rasterizador de PDF para gerar execuções
description: Este artigo descreve como gerar miniaturas e execuções de alta qualidade usando a biblioteca do Adobe PDF Rasterizer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Usar o rasterizador de PDF {#using-pdf-rasterizer}

Às vezes, ao carregar arquivos PDF ou AI grandes e com grande quantidade de conteúdo para os ativos Adobe Experience Manager (AEM), a biblioteca padrão pode não gerar uma saída precisa. Nesses casos, a biblioteca do Adobe PDF Rasterizer pode gerar uma saída mais confiável e precisa em relação à saída de uma biblioteca padrão.

A Adobe recomenda usar a biblioteca do PDF Rasterizer para o seguinte:

* Arquivos AI/PDF pesados e com grande quantidade de conteúdo
* Arquivos AI/PDF com miniaturas não gerados na caixa
* Arquivos AI com cores Pantone Matching System (PMS)

As miniaturas e visualizações geradas usando o PDF Rasterizer têm melhor qualidade em relação à saída predefinida e, portanto, proporcionam uma experiência de visualização consistente em todos os dispositivos. A biblioteca do Adobe PDF Rasterizer não suporta nenhuma conversão de espaço de cor. Sempre resulta em RGB independentemente do espaço de cor do arquivo de origem.

1. Instale o pacote PDF Rasterizer na instância do AEM a partir do Compartilhamento [de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg)pacotes.

   >[!NOTE]
   >
   >A biblioteca do PDF Rasterizer está disponível somente para Windows e Linux.

1. Acesse o console de fluxo de trabalho dos ativos AEM em `https://[server]:[port]/workflow`.

   Abra a página de fluxo de trabalho Atualizar ativo do DAM.

1. Para impedir a geração de miniaturas e renderizações da Web para arquivos PDF e AI usando os métodos padrão, siga estas etapas:

   * Abra a etapa **[!UICONTROL Processar miniaturas]** e adicione `application/pdf` ou `application/postscript` no campo **[!UICONTROL Ignorar tipos]** MIME na guia **[!UICONTROL Miniaturas]** , conforme necessário.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Na guia Imagem **[!UICONTROL habilitada para a]** Web, adicione `application/pdf` ou `application/postscript` em **[!UICONTROL Lista]** ignorada, dependendo de seus requisitos.
   ![Configuração para ignorar o processamento de miniaturas para um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra a etapa **[!UICONTROL Rasterizar representação de visualização]** de imagem PDF/AI e remova o tipo MIME para o qual você deseja ignorar a geração padrão de representações de imagem de visualização. Por exemplo, remova o tipo MIME `application/pdf`, `application/postscript`ou `application/illustrator` da lista Tipos **** MIME.

   ![process_argumentos](assets/process_arguments.png)

1. Arraste a etapa Manipulador **[!UICONTROL do Rasterizer de]** PDF do painel lateral para baixo da etapa **[!UICONTROL Processar miniaturas]** .
1. Configure os seguintes argumentos para a etapa do **[!UICONTROL PDF Rasterizer Handler]** :

   * Tipos MIME: `application/pdf` ou `application/postscript`

   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: 319:319, 140:100, 48:48. Adicione uma configuração de miniatura personalizada, se necessário.
   Os argumentos da linha de comando para o `PDFRasterizer` comando podem incluir o seguinte:

   * `-d`: Sinalizador para ativar a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-p`: Número da página. O valor padrão é todas as páginas. &#39;*&#39; indica todas as páginas.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada por quantidade diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para entrada de PDF. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que PDF Rasterize gere renderizações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações na guia Imagem **[!UICONTROL ativada pela]** Web.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Salve o fluxo de trabalho.
1. Para permitir que o PDF Rasterizer processe páginas PDF com bibliotecas de PDF, abra o modelo **[!UICONTROL DAM Process Subasset]** no console Fluxo de trabalho.
1. No painel lateral, arraste a etapa Manipulador do rasterizador de PDF na etapa **[!UICONTROL Criar representação de imagem]** habilitada para a Web.
1. Configure os seguintes argumentos para a etapa do **[!UICONTROL PDF Rasterizer Handler]** :

   * Tipos MIME: `application/pdf` ou `application/postscript`

   * Comandos: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: 319:319, 140:100, 48:48. Adicione uma configuração de miniatura personalizada, se necessário.
   Os argumentos da linha de comando para o comando PDFRasterizer podem incluir o seguinte:

   * `-d`: Sinalizador para ativar a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-p`: Número da página. O valor padrão é todas as páginas. `*` indica todas as páginas.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas tiverem um tamanho diferente, cada página poderá ser dimensionada por quantidade diferente. O padrão é o tamanho real da página.

   * `-t`: Tipo de imagem de saída. Tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para entrada de PDF. É um parâmetro obrigatório.

   * `-h`: Ajuda


1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir representação gerada]**.
1. Para permitir que PDF Rasterize gere renderizações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações na guia Imagem **[!UICONTROL ativada pela]** Web.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Salve o fluxo de trabalho.
1. Carregue um arquivo PDF ou AI para os ativos AEM. O PDF Rasterizer gera miniaturas e representações da Web para o arquivo.
