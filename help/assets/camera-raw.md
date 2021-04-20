---
title: '[!DNL Adobe Camera Raw] suporte.'
description: Saiba como habilitar o  [!DNL Adobe Camera Raw] suporte em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Administrator
feature: Developer Tools
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 2%

---


# Processar imagens usando {#camera-raw-support} Camera Raw

Você pode ativar o suporte [!DNL Adobe Camera Raw] para processar formatos de arquivo brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade é suportada em [!DNL Adobe Experience Manager Assets] usando o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponível na Distribuição de software.

>[!NOTE]
>
>A funcionalidade suporta apenas representações JPEG. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para ativar o suporte a [!DNL Camera Raw] em [!DNL Experience Manager Assets], siga estas etapas:

1. Baixe o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) da Distribuição de software.
1. Acesso `https://[aem_server]:[port]/workflow`. Abra o workflow **[!UICONTROL Ativo de atualização do DAM]** .
1. Abra a etapa **[!UICONTROL Processar miniaturas]** .
1. Forneça a seguinte configuração na guia **[!UICONTROL Miniaturas]**:

   * **[!UICONTROL Miniaturas]**:  `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos Mime]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Na guia **[!UICONTROL Imagem ativada pela Web]**, no campo **[!UICONTROL Ignorar lista]**, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione a etapa **[!UICONTROL Camera Raw/Manipulador de DNG]** abaixo da etapa **[!UICONTROL Criação de miniatura]**.
1. Na etapa **[!UICONTROL Camera Raw/Manipulador de DNG]**, adicione a seguinte configuração na guia **[!UICONTROL Argumentos]**:

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
>Certifique-se de que a configuração acima seja a mesma que a configuração **[!UICONTROL Amostra do Ativo de atualização do DAM com Camera Raw e DNG Handling Step]** .

Agora é possível importar arquivos brutos da câmera para o Assets. Depois de instalar o pacote Camera Raw e configurar o fluxo de trabalho necessário, a opção **[!UICONTROL Ajuste de imagem]** aparece na lista de painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Use a opção para fazer edições leves em suas imagens.*

Depois de salvar as edições em uma imagem [!DNL Camera Raw], uma nova representação `AdjustedPreview.jpg` é gerada para a imagem. Para outros tipos de imagem, exceto [!DNL Camera Raw], as alterações são refletidas em todas as representações.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade suporta apenas representações JPEG. Ele é compatível com Windows 64 Bit, Mac OS e RHEL 7.x.
* Não há suporte para o write-back de metadados para formatos RAW e DNG.
* A biblioteca [!DNL Camera Raw] tem limitações em relação ao total de pixels que pode ser processado de cada vez. Atualmente, ele pode processar no máximo 65000 pixels no lado longo de um arquivo ou 512 MP, independentemente dos critérios encontrados primeiro.
