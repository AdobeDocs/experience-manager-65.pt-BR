---
title: Fornecer imagens otimizadas para um site responsivo
description: Como usar o recurso de código responsivo para fornecer imagens otimizadas
uuid: 7c6baef5-7513-4644-94ed-2383e8724c17
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 5edcc765-c374-4368-a0d9-e02a713a24f2
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Delivering optimized images for a responsive site {#delivering-optimized-images-for-a-responsive-site}

Use o recurso de código responsivo quando quiser compartilhar o código para serviço responsivo com seu desenvolvedor da Web. Você copia o código responsivo (**[!UICONTROL RESS]**) para a área de transferência para que possa compartilhá-lo com o desenvolvedor da Web.

Esse recurso faz sentido se o site estiver em um WCM de terceiros. No entanto, se seu site estiver no AEM, um servidor de imagem externo renderizará a imagem e a fornecerá à página da Web.

Consulte também [Incorporação do visualizador de vídeo em uma página da Web.](embed-code.md)

Consulte também [Vincular URLs ao seu aplicativo da Web.](linking-urls-to-yourwebapplication.md)

**Para fornecer imagens otimizadas para um site** responsivo:

1. Navegue até a imagem para a qual deseja fornecer o código responsivo e, no menu suspenso, toque em **[!UICONTROL Representações]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Selecione uma predefinição de imagem responsiva. Os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]** são exibidos.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >O ativo selecionado *e a predefinição de imagem ou a predefinição do visualizador selecionado devem ser publicados para disponibilizar o* URL **[!UICONTROL ou os botões]** RESS **** .
   >
   >Mídia dinâmica - o modo híbrido exige a publicação de predefinições de imagens; Dynamic Media - O modo Scene7 publica automaticamente predefinições de imagens.

1. Toque em **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Na caixa de diálogo **[!UICONTROL Incorporar imagem]** responsiva, selecione e copie o texto do código responsivo e cole-o em seu site para acessar o ativo responsivo.
1. Edite os pontos de interrupção padrão no código incorporado para corresponder aos do site responsivo diretamente no código. Além disso, teste as diferentes resoluções de imagem servidas em diferentes pontos de interrupção de página.

## Uso do HTTP/2 para fornecer ativos do Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Fornece transferência de informações mais rápida e reduz a quantidade de poder de processamento necessário. A entrega de ativos de Dynamic Media é suportada usando o HTTP/2, que oferece melhor resposta e tempo de carregamento.

Consulte Entrega [HTTP2 de conteúdo](http2.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta de Dynamic Media.
