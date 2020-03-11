---
title: Suporte ao Camera Raw
description: Saiba como ativar o suporte do Camera Raw nos ativos Adobe Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Suporte para processar imagens usando o Camera Raw {#camera-raw-support}

Você pode ativar o suporte do Camera Raw para processar formatos de arquivo brutos, como CR2, NEF e RAF, e renderizar as imagens no formato JPEG. A funcionalidade é compatível com os ativos Adobe Experience Manager usando o pacote [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) Camera Raw disponível por meio do Compartilhamento de pacotes.

>[!NOTE]
>
>A funcionalidade suporta apenas execuções JPEG. É compatível com Windows 64 bits, Mac OS e RHEL 7.x.

Para habilitar o suporte do Camera Raw nos ativos Adobe Experience Manager, siga estas etapas:

1. Baixe o pacote [](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem630/product/assets/aem-assets-cameraraw-pkg) Camera Raw do Compartilhamento de pacotes.
1. Acesso `https://[aem_server]:[port]/workflow`. Abra o fluxo de trabalho Atualizar ativo **[!UICONTROL do]** DAM.
1. Abra a etapa **[!UICONTROL Processar miniaturas]** .
1. Forneça a seguinte configuração na guia **[!UICONTROL Miniaturas]** :

   * **[!UICONTROL Miniaturas]**: `140:100:false, 48:48:false, 319:319:false`
   * **[!UICONTROL Ignorar tipos Mime]**: `skip:image/dng, skip:image/x-raw-(.*)`
   ![chlimage_1-128](assets/chlimage_1-334.png)

1. Na guia Imagem **[!UICONTROL ativada pela]** Web, no campo Lista **** ignorada, especifique `audio/mpeg, video/(.*), image/dng, image/x-raw-(.*)`.

   ![chlimage_1-129](assets/chlimage_1-335.png)

1. No painel lateral, adicione a etapa **[!UICONTROL Camera Raw/DNG Handler]** abaixo da etapa de criação **[!UICONTROL de]** Miniaturas.
1. Na etapa **[!UICONTROL Camera Raw/DNG Handler]** , adicione a seguinte configuração na guia **[!UICONTROL Argumentos]** :

   * **[!UICONTROL Tipos]** Mime: `image/dng` e `image/x-raw-(.*)`
   * **[!UICONTROL Comando]**:

      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.web.1280.1280.jpeg 1280 1280`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.319.319.jpeg 319 319`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.140.100.jpeg 140 100`
      * `DAM_Raw_Converter ${directory}/${filename} ${directory} cq5dam.thumbnail.48.48.jpeg 48 48`
   ![chlimage_1-130](assets/chlimage_1-336.png)

1. Clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Certifique-se de que a configuração acima seja a mesma do Ativo de atualização de DAM de **[!UICONTROL amostra com a Camera RAW e a configuração da Etapa]** de manuseio de DNG.

Agora você pode importar arquivos do Camera Raw para o AEM Assets. Depois de instalar o pacote Camera RAW e configurar o fluxo de trabalho necessário, a opção **[!UICONTROL Ajustar]** imagem é exibida na lista de painéis laterais.

![chlimage_1-131](assets/chlimage_1-337.png)

*Figura: Opções no painel lateral*

![chlimage_1-132](assets/chlimage_1-338.png)

*Figura: Use a opção para fazer edições leves em suas imagens*

Depois de salvar as edições em uma imagem do Camera Raw, uma nova execução `AdjustedPreview.jpg` é gerada para a imagem. Para outros tipos de imagem, exceto o Camera Raw, as alterações são refletidas em todas as execuções.

## Práticas recomendadas, problemas conhecidos e limitações {#best-practices}

A funcionalidade tem as seguintes limitações:

* A funcionalidade suporta apenas execuções JPEG. É compatível com Windows 64 Bit, Mac OS e RHEL 7.x.
* Não há suporte para o write-back de metadados nos formatos RAW e DNG.
* A biblioteca do Camera Raw tem limitações em torno do total de pixels que pode ser processado por vez. Atualmente, ele pode processar no máximo 65000 pixels no lado longo de um arquivo ou 512 MP, independentemente do critério encontrado primeiro.
