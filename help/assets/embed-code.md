---
title: Incorpore o vídeo do Dynamic Media, o visualizador de imagem ou o visualizador dimensional em uma página da Web
description: Saiba como incorporar vídeos, imagens ou imagens 3D do Dynamic Media em uma página da Web
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 20%
---
# Incorpore o vídeo do Dynamic Media, o visualizador de imagem ou o visualizador dimensional em uma página da Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Use o recurso **[!UICONTROL Código incorporado]** quando quiser reproduzir o vídeo ou exibir um ativo incorporado em uma página da Web. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Código incorporado]**.

Você incorpora URLs somente se estiver *não* usando o Adobe Experience Manager como o WCM. Se você estiver usando o Experience Manager como o WCM, [adicione os ativos diretamente na sua página](adding-dynamic-media-assets-to-pages.md).

Consulte [Vincular URLs ao Aplicativo Web](linking-urls-to-yourwebapplication.md).

Consulte [Fornecer imagens otimizadas para um site responsivo](responsive-site.md).

>[!NOTE]
>
>O código incorporado não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição da imagem.
>
>Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar Predefinições Do Visualizador](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar Predefinições De Imagem](managing-image-presets.md#publishing-image-presets).

**Para incorporar o Vídeo do Dynamic Media, o visualizador de Imagem ou o visualizador Dimensional em uma página da Web:**

1. Navegue até o ativo de vídeo ou imagem *publicado* cujo código de inserção você deseja copiar.

   Lembre-se de que o código incorporado só está disponível para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou a predefinição de imagem também deve ser publicada.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar Predefinições Do Visualizador](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar Predefinições De Imagem](managing-image-presets.md#publishing-image-presets).

1. No painel à esquerda, selecione o menu suspenso e selecione **[!UICONTROL Visualizadores]**.
1. No painel à esquerda, selecione um nome de predefinição do visualizador. A predefinição do visualizador é aplicada ao ativo.
1. Selecione **[!UICONTROL Incorporar]**.
1. Na caixa de diálogo **[!UICONTROL Incorporar código]**, copie o código inteiro para a área de transferência e selecione **[!UICONTROL Fechar]**.
1. Cole o código incorporado nas páginas da Web.

## Utilização de HTTP/2 para fornecer ativos do Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como navegadores e servidores se comunicam. Ele possibilita a transferência mais rápida de informações e reduz a quantidade necessária de poder de processamento. A entrega de ativos do Dynamic Media agora pode ser por HTTP/2, o que fornece melhores tempos de resposta e carregamento.

Consulte [Entrega de conteúdo HTTP2](http2.md) para obter detalhes completos sobre a introdução ao uso de HTTP/2 com sua conta do Dynamic Media.
