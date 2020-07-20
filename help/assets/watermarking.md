---
title: Adicione uma marca d'água aos seus ativos digitais.
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5035d3457187f4d5fe5c2af255a1a886df7291b4
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Marque com água seus ativos digitais {#watermarking}

[!DNL Adobe Experience Manager Assets] permite que você adicione uma marca d&#39;água digital aos ativos que ajudam os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. [!DNL Experience Manager Assets] suporta texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar uma marca d&#39;água em ativos, adicione a etapa de marca d&#39;água no fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM.

1. Acesse a interface do [!DNL Experience Manager] usuário e vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos **[!UICONTROL de]** fluxo de trabalho, selecione o fluxo de trabalho do ativo **[!UICONTROL de atualização]** DAM e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho Atualizar ativo [!UICONTROL do] DAM.

   ![Arraste a etapa [!UICONTROL Adicionar marca d&#39;água] e adicione ao fluxo de trabalho [!UICONTROL Atualizar ativo] do DAM](assets/add_watermark_step_aem_assets.png)2
   *Figura: Arraste a etapa[!UICONTROL Adicionar marca d&#39;água]e adicione ao fluxo de trabalho Atualizar ativo[!UICONTROL do]DAM.*

   >[!NOTE]
   >
   >Coloque a etapa [!UICONTROL Adicionar marca d&#39;água] em qualquer lugar antes da etapa [!UICONTROL Processar miniatura] .

1. Abra a etapa **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]** , especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa adicionar marca d&#39;água em Ativos](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Forneça os argumentos na etapa adicionar marca d&#39;água em[!DNL Assets].*

1. Save the **[!UICONTROL DAM Update Asset]** workflow with the watermark step.
1. Na interface do [!DNL Assets] usuário, carregue um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, a cor e assim por diante, na posição configurada nas etapas acima.

Para marcar documentos PDF de forma programada ou com informações dinâmicas, considere usar a oferta de serviços [de Documento](/help/forms/using/overview-aem-document-services.md) AEM.
