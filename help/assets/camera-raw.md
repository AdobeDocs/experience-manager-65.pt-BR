---
title: Suporte do [!DNL Adobe Camera Raw] para processar ativos digitais
description: Saiba como habilitar o suporte ao [!DNL Adobe Camera Raw] no [!DNL Adobe Experience Manager Assets]
contentOwner: AG
role: Admin
feature: Developer Tools
exl-id: 7159a908-4c36-42b4-bbb4-d7fb1be4ee1b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%
---
# Processar imagens usando [!DNL Adobe Camera Raw] {#camera-raw-support}

Você pode habilitar o suporte do [!DNL Adobe Camera Raw] para processar formatos de arquivo brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade tem suporte no [!DNL Adobe Experience Manager Assets] usando o [pacote Camera Raw](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) disponível na Distribuição de Software.

>[!NOTE]
>
>A funcionalidade aceita somente representações do JPEG. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para habilitar o suporte ao [!DNL Camera Raw] em [!DNL Experience Manager Assets], siga estas etapas:

1. Baixe o [[!DNL Camera Raw] pacote](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-cameraraw-pkg-1.4.8.zip) de [!DNL Software Distribution].
1. Acessar `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**.
1. Edite a etapa **[!UICONTROL Processar Miniaturas]**.
1. Forneça a seguinte configuração na guia **[!UICONTROL Miniaturas]**:

   * **[!UICONTROL Miniaturas]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos MIME]**: `skip:image/dng, skip:image/x-raw-(.*)`

   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Na guia **[!UICONTROL Imagem Habilitada para Web]**, no campo **[!UICONTROL Ignorar Lista]**, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione a etapa **[!UICONTROL Camera Raw/DNG Handler]** abaixo da etapa **[!UICONTROL Processar Miniaturas]**.
1. Na etapa **[!UICONTROL Camera Raw/DNG Handler]**, adicione a seguinte configuração na guia **[!UICONTROL Argumentos]**:

   * **[!UICONTROL Tipos MIME]**: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

     * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
     * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
     * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
     * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`

   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Certifique-se de que a configuração acima seja a mesma que o **[!UICONTROL Amostra do ativo de atualização do DAM com a configuração Camera Raw e DNG Etapa de manuseio]**.

Agora você pode importar arquivos camera raw para o Assets. Depois de instalar o pacote do Camera Raw e configurar o fluxo de trabalho necessário, a opção **[!UICONTROL Ajuste da imagem]** aparece na lista de painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral.*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: use a opção para fazer edições mais leves em suas imagens.*

Depois de salvar as edições em uma imagem [!DNL Camera Raw], uma nova representação `AdjustedPreview.jpg` é gerada para a imagem. Para outros tipos de imagem, exceto [!DNL Camera Raw], as alterações são refletidas em todas as representações.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade aceita somente representações do JPEG. Ele é compatível com Windows 64 bits, Mac OS e RHEL 7.x.
* O write-back de metadados não é compatível com formatos RAW e DNG.
* A biblioteca [!DNL Camera Raw] tem limitações em torno do total de pixels que pode processar de cada vez. Atualmente, ele pode processar no máximo 65.000 pixels no lado longo de um arquivo ou 512 MP em qualquer critério encontrado primeiro.
