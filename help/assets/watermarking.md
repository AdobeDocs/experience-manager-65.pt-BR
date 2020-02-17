---
title: Adicione uma marca d'água aos seus ativos digitais.
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Marque com água seus ativos digitais {#watermarking}

Os ativos Adobe Experience Manager (AEM) permitem que você adicione uma marca d&#39;água digital aos ativos que ajudam os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. O AEM Assets oferece suporte para texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar marca d&#39;água em ativos, adicione a etapa de marca d&#39;água no fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM.

1. Acesse a interface do usuário do AEM e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos **[!UICONTROL de]** fluxo de trabalho, selecione o fluxo de trabalho do ativo **[!UICONTROL de atualização]** DAM e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM.

   ![Arraste a etapa Adicionar marca d&#39;água e adicione ao fluxo de trabalho do ativo de atualização do DAM](assets/add_watermark_step_aem_assets.png)

   >[!NOTE]
   >
   >Coloque a etapa [!UICONTROL Adicionar marca d&#39;água] em qualquer lugar antes da etapa [!UICONTROL Processar miniatura] .

1. Abra a etapa **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]** , especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, toque/clique no ícone Concluído.

   ![Forneça os argumentos na etapa adicionar marca d&#39;água em Ativos](assets/arguments_add_watermark_aem_assets.png)

1. Salve o fluxo de trabalho do Ativo **[!UICONTROL de atualização do]** DAM com a etapa da marca d&#39;água.
1. Na interface do usuário Ativos, faça upload de um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, a cor e assim por diante, na posição configurada nas etapas acima.
