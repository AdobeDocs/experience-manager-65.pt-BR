---
title: Usar o PDF rasterizer para gerar representações
description: Gere miniaturas e representações de alta qualidade usando a biblioteca do Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: e42ab83e-8918-43a7-98a3-62bebbd5bb3a
    internal-label: Renditions
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%
---
# Usar o PDF Rasterizer {#using-pdf-rasterizer}

Ao carregar arquivos grandes de PDF ou AI com grande volume de conteúdo para [!DNL Adobe Experience Manager Assets], a biblioteca padrão pode não gerar uma saída precisa. A biblioteca PDF Rasterizer da Adobe pode gerar uma saída mais confiável e precisa quando comparada à saída de uma biblioteca padrão. A Adobe recomenda usar a biblioteca do PDF Rasterizer para os seguintes cenários:

A Adobe recomenda usar a biblioteca PDF Rasterizer para o seguinte:

* Arquivos AI ou PDF pesados com uso intenso de conteúdo.
* Arquivos AI e arquivos PDF com miniaturas que não são geradas por padrão.
* Arquivos AI com cores do Sistema de correspondência Pantone (PMS).

Miniaturas e visualizações geradas usando o PDF Rasterizer são melhores em qualidade em comparação com a saída pronta para uso e, portanto, fornecem experiência de visualização consistente em todos os dispositivos. A biblioteca do Adobe PDF Rasterizer não é compatível com nenhuma conversão de espaço de cores. Ele sempre gera para o RGB, independentemente do espaço de cor do arquivo de origem.

1. Instale o pacote PDF Rasterizer na implantação [!DNL Adobe Experience Manager] da [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip).

   >[!NOTE]
   >
   >A biblioteca PDF Rasterizer está disponível somente para Windows e Linux®.

1. Acesse o console de fluxo de trabalho [!DNL Assets] em `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho [!UICONTROL Ativo de atualização DAM].

1. Para impedir a geração de miniaturas e representações da Web para arquivos do PDF e arquivos AI usando os métodos padrão, siga estas etapas:

   * Abra a etapa **[!UICONTROL Processar Miniaturas]** e adicione `application/pdf` ou `application/postscript` no campo **[!UICONTROL Ignorar Tipos MIME]** na guia **[!UICONTROL Miniaturas]**, conforme necessário.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Na guia **[!UICONTROL Imagem Habilitada para a Web]**, adicione `application/pdf` ou `application/postscript` em **[!UICONTROL Ignorar Lista]**, dependendo de suas necessidades.

   ![Configuração para ignorar o processamento de miniatura para um formato de imagem](assets/web_enabled_imageskiplist.png)

1. Abra a etapa **[!UICONTROL Rasterizar Representação da Visualização da Imagem do PDF/AI]** e remova o tipo MIME para o qual você deseja ignorar a geração padrão de representações da imagem de visualização. Por exemplo, remova o tipo MIME `application/pdf`, `application/postscript` ou `application/illustrator` da lista **[!UICONTROL Tipos MIME]**.

   ![argumentos_do_processo](assets/process_arguments.png)

1. Arraste a etapa **[!UICONTROL Manipulador de rasterizador do PDF]** do painel lateral para abaixo da etapa **[!UICONTROL Processar miniaturas]**.
1. Configure os seguintes argumentos para a etapa **[!UICONTROL Manipulador de rasterizador do PDF]**:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniatura: 319:319, 140:100, 48:48. Adicione a configuração de miniatura personalizada, se necessário.

   Os argumentos de linha de comando para o comando `PDFRasterizer` podem incluir o seguinte:

   * `-d`: sinalizador para permitir a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda

1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir Representação Gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Especifique as configurações na guia **[!UICONTROL Imagem Habilitada para Web]**.

   ![imagem_habilitada_para_Web1](assets/web_enabled_image1.png)

1. Salve o workflow.
1. Para permitir que o PDF Rasterizer processe páginas do PDF com bibliotecas PDF, abra o modelo **[!UICONTROL Subativo do processo do DAM]** no console [!UICONTROL Fluxo de trabalho].
1. No painel lateral, arraste a etapa Manipulador do PDF Rasterizer para a etapa **[!UICONTROL Criar representação de imagem habilitada para a Web]**.
1. Configure os seguintes argumentos para a etapa **[!UICONTROL Manipulador de rasterizador do PDF]**:

   * Tipos MIME: `application/pdf` ou `application/postscript`
   * Comandos: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Adicionar tamanhos de miniaturas: `319:319`, `140:100`, `48:48`. Adicione a configuração de miniatura personalizada, conforme necessário.

   Os argumentos de linha de comando para o comando `PDFRasterizer` podem incluir o seguinte:

   * `-d`: sinalizador para permitir a renderização suave de texto, arte vetorial e imagens. Cria imagens de melhor qualidade. No entanto, a inclusão desse parâmetro faz com que o comando seja executado lentamente e aumente o tamanho das imagens.

   * `-s`: Dimensão máxima da imagem (altura ou largura). Isso é convertido em DPI para cada página. Se as páginas forem de tamanhos diferentes, cada página poderá ser dimensionada de acordo com a quantidade. O padrão é o tamanho de página real.

   * `-t`: Tipo de imagem de saída. Os tipos válidos são JPEG, PNG, GIF e BMP. O valor padrão é JPEG.

   * `-i`: Caminho para PDF de entrada. É um parâmetro obrigatório.

   * `-h`: Ajuda

1. Para excluir representações intermediárias, selecione **[!UICONTROL Excluir Representação Gerada]**.
1. Para permitir que o PDF Rasterizer gere representações da Web, selecione **[!UICONTROL Gerar representação da Web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Especifique as configurações na guia **[!UICONTROL Imagem Habilitada para Web]**.

   ![imagem_habilitada_para_Web-1](assets/web_enabled_image-1.png)

1. Salve o workflow.
1. Carregar um arquivo PDF ou AI para [!DNL Experience Manager Assets]. O PDF Rasterizer gera as miniaturas e representações da Web do arquivo.
