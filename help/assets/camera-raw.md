---
title: "[!DNL Adobe Camera Raw] suporte para processar ativos digitais"
description: Saiba como habilitar [!DNL Adobe Camera Raw] suporte no [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# Processar imagens usando [!DNL Adobe Camera Raw] {#camera-raw-support}

Você pode ativar a variável [!DNL Adobe Camera Raw] suporte para processar formatos de arquivo brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade é compatível com o [!DNL Adobe Experience Manager Assets] usando o [Pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponível na Distribuição de software.

>[!NOTE]
>
>A funcionalidade suporta apenas JPEG renditions. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para ativar [!DNL Camera Raw] suporte no [!DNL Experience Manager Assets]siga estas etapas:

1. Baixe o [[!DNL Camera Raw] pacote](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) from [!DNL Software Distribution].
1. Acesso `https://[aem_server]:[port]/workflow`. Abra o **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho.
1. Edite o **[!UICONTROL Processar miniaturas]** etapa.
1. Forneça a seguinte configuração no **[!UICONTROL Miniaturas]** guia :

   * **[!UICONTROL Miniaturas]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos Mime]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. No **[!UICONTROL Imagem ativada na Web]** na guia , no **[!UICONTROL Ignorar Lista]** , especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione o **[!UICONTROL Manipulador Camera Raw/DNG]** etapa abaixo do **[!UICONTROL Processar miniaturas]** etapa.
1. No **[!UICONTROL Manipulador Camera Raw/DNG]** adicione a seguinte configuração no **[!UICONTROL Argumentos]** guia :

   * **[!UICONTROL Tipos Mime]**: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Certifique-se de que a configuração acima seja a mesma que a **[!UICONTROL Exemplo de ativo de atualização do DAM com etapa de manuseio de DNG e Camera Raw]** configuração.

Agora é possível importar arquivos brutos da câmera para o Assets. Depois de instalar o pacote Camera Raw e configurar o workflow necessário, **[!UICONTROL Ajuste da imagem]** é exibida na lista de painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Use a opção para fazer edições leves em suas imagens.*

Depois de salvar as edições em um [!DNL Camera Raw] imagem, uma nova representação `AdjustedPreview.jpg` é gerada para a imagem. Para outros tipos de imagens, exceto [!DNL Camera Raw], as alterações são refletidas em todas as representações.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade suporta apenas JPEG renditions. Ele é compatível com Windows 64 Bit, Mac OS e RHEL 7.x.
* Não há suporte para o write-back de metadados para formatos RAW e DNG.
* O [!DNL Camera Raw] A biblioteca tem limitações em relação ao total de pixels que pode ser processado de cada vez. Atualmente, ele pode processar no máximo 65000 pixels no lado longo de um arquivo ou 512 MP, independentemente dos critérios encontrados primeiro.
