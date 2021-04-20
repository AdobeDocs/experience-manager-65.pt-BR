---
title: Adicionar marca d'água aos ativos digitais
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Marque seus ativos digitais {#watermarking}

[!DNL Adobe Experience Manager Assets] O permite adicionar uma marca d&#39;água digital aos ativos, o que ajuda os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. [!DNL Experience Manager Assets] suporta texto a ser usado como uma marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar marca d&#39;água em ativos, adicione a etapa marca d&#39;água no fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] .

1. Acesse a interface do usuário [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]** e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM] .

   ![Arraste a etapa  [!UICONTROL Adicionar ] marca d&#39;água e adicione ao fluxo de trabalho  [!UICONTROL Atualizar ] ativo do DAM](assets/add_watermark_step_aem_assets.png)

   *Figura: Arraste a etapa  [!UICONTROL Adicionar ] marca d&#39;água e adicione ao fluxo de trabalho  [!UICONTROL Ativos de atualização do DAM ] .*

   >[!NOTE]
   >
   >Coloque a etapa [!UICONTROL Adicionar marca d&#39;água] em qualquer lugar antes da etapa [!UICONTROL Processar miniatura].

1. Abra a etapa **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]**, especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa adicionar marca d&#39;água em  [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Forneça os argumentos na etapa adicionar marca d&#39;água em  [!DNL Assets].*

1. Salve o workflow **[!UICONTROL Ativo de atualização DAM]** com a etapa de marca d&#39;água.
1. Na interface do usuário [!DNL Assets], faça upload de um ativo de amostra. A marca d&#39;água aparece com o tamanho da fonte, cor e assim por diante, na posição configurada nas etapas acima.

Para marcar documentos PDF de forma programática ou com informações dinâmicas, considere usar a oferta [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Dicas e limitações {#tips-limitations}

* Somente marcas d&#39;água baseadas em texto são suportadas. As imagens não são usadas como marcas d&#39;água, mesmo que você possa fazer upload de imagens ao criar o [!UICONTROL Adicionar processo de marca d&#39;água].
* Somente os arquivos PNG e JPEG têm suporte para marca d&#39;água. Outros formatos de ativos não são marcados com marca d&#39;água.
