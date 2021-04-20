---
title: Incorporação do visualizador de vídeo ou imagem do Dynamic Media em uma página da Web
description: Saiba como incorporar vídeos ou imagens do Dynamic Media em uma página da Web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: Viewers
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 21%

---


# Incorporação do vídeo do Dynamic Media, visualizador de imagem ou visualizador Dimensional em uma página da Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Use o recurso **[!UICONTROL Incorporar código]** quando quiser reproduzir o vídeo ou exibir um ativo incorporado em uma página da Web. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar código]**.

Você incorpora URLs somente se estiver _não_ usando AEM como WCM. Se estiver usando AEM como WCM, [você adiciona os ativos diretamente na página.](adding-dynamic-media-assets-to-pages.md)

Consulte [Vincular URLs ao seu Aplicativo Web.](linking-urls-to-yourwebapplication.md)

Consulte [Fornecer imagens otimizadas para um site responsivo.](responsive-site.md)

>[!NOTE]
>
>O código incorporado não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição de imagem.
>
>Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).
>
>Consulte [Predefinições do visualizador de publicação](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar predefinições de imagens](managing-image-presets.md#publishing-image-presets).

**Para incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web**

1. Navegue até o vídeo *publicado* ou ativo de imagem cujo código incorporado você deseja copiar.

   Lembre-se de que o código incorporado só está disponível para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicar ativos.](publishing-dynamicmedia-assets.md)

   Consulte [Predefinições do visualizador de publicação](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar predefinições de imagens](managing-image-presets.md#publishing-image-presets).

1. No painel à esquerda, selecione o menu suspenso e toque em **[!UICONTROL Visualizadores.]**
1. No painel à esquerda, toque em um nome de predefinição do visualizador. A predefinição do visualizador é aplicada ao ativo.
1. Toque em **[!UICONTROL Incorporar.]**
1. Na caixa de diálogo **[!UICONTROL Incorporar código]**, copie o código inteiro para a área de transferência e toque em **[!UICONTROL Fechar.]**
1. Cole o código incorporado nas páginas da Web.

## Usar HTTP/2 para fornecer ativos do Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Ele oferece transferência mais rápida de informações e reduz a quantidade de poder de processamento necessário. A entrega de ativos do Dynamic Media agora pode ser feita via HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte [HTTP2 Delivery of Content](http2.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta Dynamic Media.
