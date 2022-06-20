---
title: Adicionar marca d'água aos ativos digitais
description: Saiba como usar o recurso Marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# Marque com água seus ativos digitais {#watermarking}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/watermarking.html?lang=en) |

[!DNL Adobe Experience Manager Assets] O permite adicionar uma marca d&#39;água digital aos ativos, o que ajuda os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. [!DNL Experience Manager Assets] suporta texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar marca d&#39;água em ativos, adicione a etapa marca d&#39;água no [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

1. Acesse o [!DNL Experience Manager] interface do usuário e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. No **[!UICONTROL Modelos de fluxo de trabalho]** selecione o **[!UICONTROL Ativo de atualização DAM]** e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste o **[!UICONTROL Adicionar marca d&#39;água]** para [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

   ![Arraste o [!UICONTROL Adicionar marca d&#39;água] e adicionar à [!UICONTROL Ativo de atualização DAM] workflow](assets/add_watermark_step_aem_assets.png)

   *Figura: Arraste o [!UICONTROL Adicionar marca d&#39;água] e adicionar à [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.*

   >[!NOTE]
   >
   >Coloque o [!UICONTROL Adicionar marca d&#39;água] etapa em qualquer lugar antes da [!UICONTROL Miniatura do processo] etapa.

1. Abra o **[!UICONTROL Adicionar marca d&#39;água]** para exibir suas propriedades.
1. No **[!UICONTROL Argumentos]** , especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa adicionar marca d&#39;água em [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: Forneça os argumentos na etapa adicionar marca d&#39;água em [!DNL Assets].*

1. Salve as **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho com a etapa marca d&#39;água.
1. No [!DNL Assets] interface do usuário, faça upload de um ativo de amostra. A marca d&#39;água aparece com o tamanho da fonte, cor e assim por diante, na posição configurada nas etapas acima.

Para fazer uma marca d&#39;água em documentos PDF de forma programática ou com informações dinâmicas, considere usar [Serviços de documento do Experience Manager](/help/forms/using/overview-aem-document-services.md) oferta.

## Dicas e limitações {#tips-limitations}

* Somente marcas d&#39;água baseadas em texto são suportadas. As imagens não são usadas como marcas d&#39;água, mesmo que você possa fazer upload de imagens ao criar o [!UICONTROL Adicionar processo de marca d&#39;água].
* Somente os arquivos PNG e JPEG têm suporte para marca d&#39;água. Outros formatos de ativos não são marcados com marca d&#39;água.
