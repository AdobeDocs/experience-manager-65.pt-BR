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

Você pode ativar o [!DNL Adobe Camera Raw] suporte para processar formatos de arquivos brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade é compatível com o [!DNL Adobe Experience Manager Assets] usando o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponível na Distribuição de software.

>[!NOTE]
>
>A funcionalidade suporta apenas representações de JPEG. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para habilitar [!DNL Camera Raw] suporte no [!DNL Experience Manager Assets], siga estas etapas:

1. Baixe o [[!DNL Camera Raw] pacote](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) de [!DNL Software Distribution].
1. Acesso `https://[aem_server]:[port]/workflow`. Abra o **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho.
1. Edite o **[!UICONTROL Miniaturas do processo]** etapa.
1. Forneça a seguinte configuração no **[!UICONTROL Miniaturas]** guia:

   * **[!UICONTROL Miniaturas]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos Mime]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. No **[!UICONTROL Imagem ativada pela Web]** , na guia **[!UICONTROL Ignorar lista]** campo, especificar `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione a variável **[!UICONTROL Manipulador de Camera Raw/DNG]** etapa abaixo do **[!UICONTROL Miniaturas do processo]** etapa.
1. No **[!UICONTROL Manipulador de Camera Raw/DNG]** adicione a seguinte configuração na etapa **[!UICONTROL Argumentos]** guia:

   * **[!UICONTROL Tipos de Mime]**: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Certifique-se de que a configuração acima seja a mesma da variável **[!UICONTROL Ativo de atualização de DAM de amostra com etapa de manipulação Camera Raw e DNG]** configuração.

Agora você pode importar arquivos camera raw para o Assets. Depois de instalar o pacote Camera Raw e configurar o fluxo de trabalho necessário, **[!UICONTROL Ajuste da imagem]** será exibida na lista de painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: use a opção para fazer edições mais leves em suas imagens.*

Depois de salvar as edições em uma [!DNL Camera Raw] imagem, uma nova representação `AdjustedPreview.jpg` é gerado para a imagem. Para outros tipos de imagem, exceto [!DNL Camera Raw], as alterações serão refletidas em todas as representações.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade suporta apenas representações de JPEG. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.
* O write-back de metadados não é compatível com formatos RAW e DNG.
* A variável [!DNL Camera Raw] A biblioteca tem limitações em relação ao total de pixels que pode processar de cada vez. Atualmente, ele pode processar no máximo 65.000 pixels no lado longo de um arquivo ou 512 MP em qualquer critério encontrado primeiro.
