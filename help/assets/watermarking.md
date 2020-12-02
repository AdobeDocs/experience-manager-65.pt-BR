---
title: Adicionar marca d'água aos seus ativos digitais
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Marque seus ativos digitais {#watermarking}

[!DNL Adobe Experience Manager Assets] permite que você adicione uma marca d&#39;água digital aos ativos que ajudam os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. [!DNL Experience Manager Assets] suporta texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar uma marca d&#39;água em ativos, adicione a etapa de marca d&#39;água no fluxo de trabalho [!UICONTROL Atualizar ativo do DAM].

1. Acesse a [!DNL Experience Manager] interface do usuário e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de Fluxo de Trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Atualizar Ativo]** do DAM e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM].

   ![Arraste a etapa  [!UICONTROL Adicionar ] marca d&#39;água e adicione-a ao  [!UICONTROL DAM Update ] Assetworkflow](assets/add_watermark_step_aem_assets.png)
2
   *Figura: Arraste a etapa  [!UICONTROL Adicionar ] marca d&#39;água e adicione ao fluxo de trabalho do  [!UICONTROL DAM Update ] Assetworkflow.*

   >[!NOTE]
   >
   >Coloque a etapa [!UICONTROL Adicionar marca d&#39;água] em qualquer lugar antes da etapa [!UICONTROL Processar miniatura].

1. Abra a etapa **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]**, especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa adicionar marca d&#39;água em Ativos](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Forneça os argumentos na etapa adicionar marca d&#39;água em  [!DNL Assets].*

1. Salve o fluxo de trabalho **[!UICONTROL DAM Update Asset]** com a etapa de marca d&#39;água.
1. Na interface do usuário [!DNL Assets], carregue um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, a cor e assim por diante, na posição configurada nas etapas acima.

Para marcar documentos PDF de forma programática ou com informações dinâmicas, considere usar a oferta [Experience Manager Documento Services](/help/forms/using/overview-aem-document-services.md).
