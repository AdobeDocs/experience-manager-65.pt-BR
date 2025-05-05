---
title: Adicionar marca d'água aos seus ativos digitais
description: Saiba como usar o recurso de marca d'água para adicionar uma marca d'água digital aos ativos.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Marca d&#39;água em seus ativos digitais {#watermarking}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

O [!DNL Adobe Experience Manager Assets] permite adicionar uma marca d&#39;água digital aos ativos que ajuda os usuários a verificar a autenticidade e os direitos autorais dos ativos. [!DNL Experience Manager Assets] dá suporte para texto a ser usado como marca d&#39;água em arquivos PNG e JPEG.

Para poder aplicar a marca d&#39;água em ativos, adicione a etapa de marca d&#39;água no fluxo de trabalho [!UICONTROL Ativo de atualização do DAM].

1. Acesse a interface de usuário do [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Na página **[!UICONTROL Modelos de fluxo de trabalho]**, selecione o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** e clique em **[!UICONTROL Editar]**.

1. No painel lateral, arraste a etapa **[!UICONTROL Adicionar marca d&#39;água]** para o fluxo de trabalho [!UICONTROL Ativo de atualização do DAM].

   ![Arraste a etapa [!UICONTROL Adicionar marca d&#39;água] e adicione ao fluxo de trabalho [!UICONTROL Ativo de atualização DAM]](assets/add_watermark_step_aem_assets.png)

   *Figura: arraste a etapa [!UICONTROL Adicionar marca d&#39;água] e adicione ao fluxo de trabalho [!UICONTROL Ativo de atualização DAM].*

   >[!NOTE]
   >
   >Coloque a etapa [!UICONTROL Adicionar Marca D&#39;Água] em qualquer lugar antes da etapa [!UICONTROL Processar Miniatura].

1. Abra a etapa **[!UICONTROL Adicionar Marca D&#39;Água]** para exibir suas propriedades.
1. Na guia **[!UICONTROL Argumentos]**, especifique valores válidos nos vários campos, incluindo texto, tipo de fonte, tamanho, cor, posição, orientação e assim por diante. Para confirmar as alterações, clique em **[!UICONTROL Concluído]**.

   ![Forneça os argumentos na etapa de adição de marca d&#39;água em [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figura: forneça os argumentos na etapa de adição de marca d&#39;água em [!DNL Assets].*

1. Salve o fluxo de trabalho do **[!UICONTROL Ativo de atualização do DAM]** com a etapa de marca d&#39;água.
1. Na interface de usuário do [!DNL Assets], carregue um ativo de amostra. A marca d&#39;água é exibida com o tamanho da fonte, cor e assim por diante, na posição configurada nas etapas acima.

Para criar uma marca d&#39;água para documentos PDF de forma programática ou com informações dinâmicas, considere usar a oferta [Serviços de Documentos Experience Manager](/help/forms/using/overview-aem-document-services.md).

## Dicas e limitações {#tips-limitations}

* Somente há suporte para marcas d&#39;água baseadas em texto. As imagens não são usadas como marcas d&#39;água, embora você possa carregar imagens ao criar o [!UICONTROL Adicionar Processo de Marca D&#39;Água].
* Somente arquivos PNG e JPEG têm suporte para serem marcas d&#39;água. Outros formatos de ativos não têm marca d&#39;água.
