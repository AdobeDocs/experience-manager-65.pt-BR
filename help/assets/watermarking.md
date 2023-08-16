---
title: Adicionar marca d'água aos seus ativos digitais
description: Saiba como usar o recurso de marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 2%

---

# Marca d&#39;água em seus ativos digitais {#watermarking}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Experience Manager Assets] O permite adicionar uma marca d&#39;água digital aos ativos da que ajuda os usuários a verificar a autenticidade e a propriedade de direitos autorais dos ativos. [!DNL Experience Manager Assets] O suporta texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar a marca d&#39;água em ativos, adicione a etapa de marca d&#39;água no [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

1. Acesse o [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. No **[!UICONTROL Modelos de fluxo de trabalho]** selecione a **[!UICONTROL Ativo de atualização DAM]** e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste o **[!UICONTROL Adicionar marca d&#39;água]** etapa para o [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.

   ![Arraste o [!UICONTROL Adicionar marca d&#39;água] e adicione à etapa [!UICONTROL Ativo de atualização DAM] fluxo de trabalho](assets/add_watermark_step_aem_assets.png)

   *Figura: arraste o [!UICONTROL Adicionar marca d&#39;água] e adicione à etapa [!UICONTROL Ativo de atualização DAM] fluxo de trabalho.*

   >[!NOTE]
   >
   >Coloque o [!UICONTROL Adicionar marca d&#39;água] etapa em qualquer lugar antes da [!UICONTROL Miniatura do processo] etapa.

1. Abra o **[!UICONTROL Adicionar marca d&#39;água]** etapa para exibir suas propriedades.
1. No **[!UICONTROL Argumentos]** especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa de adição de marca d&#39;água em [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: forneça os argumentos na etapa de adição de marca d&#39;água em [!DNL Assets].*

1. Salve o **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho com a etapa marca d&#39;água.
1. No [!DNL Assets] , carregue um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, cor e assim por diante, na posição configurada nas etapas acima.

Para criar uma marca d&#39;água para documentos PDF programaticamente ou com informações dinâmicas, considere usar [Serviços de documento Experience Manager](/help/forms/using/overview-aem-document-services.md) oferta.

## Dicas e limitações {#tips-limitations}

* Somente há suporte para marcas d&#39;água baseadas em texto. As imagens não são usadas como marcas d&#39;água, embora você possa carregar imagens ao criar a [!UICONTROL Adicionar processo de marca d&#39;água].
* Somente arquivos PNG e JPEG têm suporte para serem marcas d&#39;água. Outros formatos de ativos não têm marca d&#39;água.
