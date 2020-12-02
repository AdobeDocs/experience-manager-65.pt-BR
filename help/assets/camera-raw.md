---
title: '[!DNL Adobe Camera Raw] suporte.'
description: Saiba como ativar o suporte [!DNL Adobe Camera Raw] em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: bccc937c1e1a349ab292a748c3c7b9d0c68b6199
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# Processar imagens usando o Camera Raw {#camera-raw-support}

Você pode ativar o suporte [!DNL Adobe Camera Raw] para processar formatos de arquivo brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade é suportada em [!DNL Adobe Experience Manager Assets] usando o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponível na Distribuição de software.

>[!NOTE]
>
>A funcionalidade suporta apenas execuções JPEG. É compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para habilitar o suporte a [!DNL Camera Raw] em [!DNL Experience Manager Assets], siga estas etapas:

1. Baixe o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) da Distribuição de software.
1. Acesso `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho **[!UICONTROL DAM Update Asset]**.
1. Abra a etapa **[!UICONTROL Processar miniaturas]**.
1. Forneça a seguinte configuração na guia **[!UICONTROL Miniaturas]**:

   * **[!UICONTROL Miniaturas]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos Mime]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Na guia **[!UICONTROL Imagem ativada pela Web]**, no campo **[!UICONTROL Ignorar Lista]**, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione a etapa **[!UICONTROL Camera Raw/Manipulador de DNG]** abaixo da etapa **[!UICONTROL Criação de miniaturas]**.
1. Na etapa **[!UICONTROL Camera Raw/DNG Handler]**, adicione a seguinte configuração na guia **[!UICONTROL Argumentos]**:

   * **[!UICONTROL Tipos]** Mime:  `image/dng` e  `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Certifique-se de que a configuração acima seja a mesma que a configuração **[!UICONTROL Sample DAM Update Asset With Camera Raw and DNG Handling Step]**.

Agora você pode importar arquivos do Camera Raw para o Assets. Depois de instalar o pacote Camera Raw e configurar o fluxo de trabalho necessário, a opção **[!UICONTROL Ajustar imagem]** é exibida na lista dos painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Use a opção para fazer edições leves em suas imagens.*

Depois de salvar as edições em uma imagem [!DNL Camera Raw], uma nova representação `AdjustedPreview.jpg` é gerada para a imagem. Para outros tipos de imagem, exceto [!DNL Camera Raw], as alterações são refletidas em todas as execuções.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade suporta apenas execuções JPEG. É compatível com Windows 64 Bit, Mac OS e RHEL 7.x.
* Não há suporte para o write-back de metadados nos formatos RAW e DNG.
* A biblioteca [!DNL Camera Raw] tem limitações em torno do total de pixels que pode ser processado de cada vez. Atualmente, ele pode processar no máximo 65000 pixels no lado longo de um arquivo ou 512 MP, independentemente do critério encontrado primeiro.
