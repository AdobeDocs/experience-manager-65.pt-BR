---
title: Usar o rasterizador de PDF para gerar representações
description: Gere miniaturas e representações de alta qualidade usando a biblioteca do Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Usar o rasterizador de PDF {#using-pdf-rasterizer}

Ao carregar arquivos grandes de PDF ou AI que exijam muito conteúdo para [!DNL Adobe Experience Manager Assets], a biblioteca padrão pode não gerar uma saída precisa. A biblioteca PDF Rasterizer Adobe pode gerar uma saída mais confiável e precisa quando comparada à saída de uma biblioteca padrão. A Adobe recomenda o uso da biblioteca PDF Rasterizer para os seguintes cenários:

A Adobe recomenda o uso da biblioteca PDF Rasterizer para o seguinte:

* Arquivos AI ou arquivos PDF pesados e com uso intenso de conteúdo.
* Arquivos AI e arquivos PDF com miniaturas que não são geradas por padrão.
* Arquivos AI com cores do Sistema de correspondência Pantone (PMS).

Miniaturas e visualizações geradas usando o PDF Rasterizer são melhores em qualidade em comparação com a saída pronta para uso e, portanto, fornecem experiência de visualização consistente em todos os dispositivos. A biblioteca do Adobe PDF Rasterizer não é compatível com nenhuma conversão de espaço de cores. Ele sempre gera para o RGB independentemente do espaço de cor do arquivo de origem.

1. Instale o pacote PDF Rasterizer na implantação [!DNL Adobe Experience Manager] da [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip).

   >[!NOTE]
   >
   >A biblioteca PDF Rasterizer está disponível somente para Windows e Linux®.

1. Acesse o console de fluxo de trabalho [!DNL Assets] em `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho [!UICONTROL Ativo de atualização DAM].

1. Para impedir a geração de miniaturas e representações da Web para arquivos PDF e arquivos AI usando os métodos padrão, siga estas etapas:

   * Abra a etapa **[!UICONTROL Processar Miniaturas]** e adicione `application/pdf` ou `application/postscript` no campo **[!UICONTROL Ignorar Tipos MIME]** na guia **[!UICONTROL Miniaturas]**, conforme necessário.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Na guia **[!UICONTROL Imagem Habilitada para a Web]**, adicione `application/pdf` ou `application/postscript` em **[!UICONTROL Ignorar Lista]**, dependendo de suas necessidades.

   ![Configuração para ignorar o processamento de miniatura para um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra a etapa **[!UICONTROL Rasterizar Representação de Visualização de PDF/Imagem de IA]** e remova o tipo MIME para o qual você deseja ignorar a geração padrão de representações de imagens de visualização. Por exemplo, remova o tipo MIME `application/pdf`, `application/postscript` ou `application/illustrator` da lista **[!UICONTROL Tipos MIME]**.

   ![argumentos_do_processo](assets/process_arguments.png)

1. Arraste a etapa **[!UICONTROL Manipulador do rasterizador de PDF]** do painel lateral para abaixo da etapa **[!UICONTROL Processar miniaturas]**.
1. Configure os seguintes argumentos para a etapa **[!UICONTROL Manipulador Rasterizador de PDF]**:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: 319:319, 140:100, 48:48. Adicione a configuração de miniatura personalizada, se necessário.

   Os argumentos de linha de comando para o comando `PDFRasterizer` podem incluir o seguinte:

   * `-d`: sinalizador para permitir a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho do PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda

1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir Representação Gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar Representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações na guia **[!UICONTROL Imagem Habilitada para Web]**.

   ![imagem_habilitada_para_Web1](assets/web_enabled_image1.png)

1. Salve o workflow.
1. Para permitir que o Rasterizador de PDF processe páginas de PDF com bibliotecas de PDF, abra o modelo **[!UICONTROL Subativo do processo do DAM]** no console [!UICONTROL Fluxo de trabalho].
1. No painel lateral, arraste a etapa Manipulador do rasterizador de PDF para a etapa **[!UICONTROL Criar representação de imagem habilitada para a Web]**.
1. Configure os seguintes argumentos para a etapa **[!UICONTROL Manipulador Rasterizador de PDF]**:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: `319:319`, `140:100`, `48:48`. Adicione a configuração de miniatura personalizada, conforme necessário.

   Os argumentos de linha de comando para o comando `PDFRasterizer` podem incluir o seguinte:

   * `-d`: sinalizador para permitir a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho do PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda

1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir Representação Gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar Representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações na guia **[!UICONTROL Imagem Habilitada para Web]**.

   ![imagem_habilitada_para_Web-1](assets/web_enabled_image-1.png)

1. Salve o workflow.
1. Carregar um arquivo PDF ou AI para [!DNL Experience Manager Assets]. O PDF Rasterizer gera as miniaturas e representações da Web para o arquivo.
