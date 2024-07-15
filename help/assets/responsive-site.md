---
title: Entrega de imagens otimizadas para um site responsivo
description: Como usar o recurso de código responsivo para fornecer imagens otimizadas
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 11%

---

# Entregar imagens otimizadas para um site responsivo {#delivering-optimized-images-for-a-responsive-site}

Use o recurso Código responsivo quando quiser compartilhar o código para veiculação responsiva com o desenvolvedor da Web. Você copia o código (**[!UICONTROL RESS]**) responsivo para a área de transferência para poder compartilhá-lo com o desenvolvedor da Web.

Esse recurso faz sentido usar se o site estiver em um WCM de terceiros. No entanto, se o site estiver no Adobe Experience Manager, um servidor de imagens externo renderiza a imagem e a fornece à página da Web.

Consulte também [Incorporar o Visualizador de Vídeo em uma Página da Web](embed-code.md).

Consulte também [Vincular URLs ao Aplicativo Web](linking-urls-to-yourwebapplication.md).

**Para fornecer imagens otimizadas para um site responsivo:**

1. Navegue até a imagem para a qual você deseja fornecer um código responsivo e, no menu suspenso, selecione **[!UICONTROL Representações]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Selecione uma predefinição de imagem responsiva. Os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]** são exibidos.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >O ativo selecionado *e* a predefinição de imagem ou a predefinição do visualizador selecionado devem ser publicados para disponibilizar os botões **[!UICONTROL URL]** ou **[!UICONTROL RESS]**.
   >
   >Dynamic Media - O modo híbrido exige a publicação de predefinições de imagens; Dynamic Media - O modo Scene7 publica predefinições de imagens automaticamente.

1. Selecione **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Na caixa de diálogo **[!UICONTROL Incorporar imagem responsiva]**, selecione, copie o texto de código responsivo e cole-o no site para acessar o ativo responsivo.
1. Edite os pontos de interrupção padrão no código incorporado para corresponder aos pontos de interrupção do site responsivo, diretamente no código. Além disso, teste as diferentes resoluções de imagem que estão sendo atendidas em diferentes pontos de interrupção de página.

## Usar HTTP/2 para entregar seus ativos do Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como navegadores e servidores se comunicam. Ele possibilita a transferência mais rápida de informações e reduz a quantidade necessária de poder de processamento. A entrega de ativos do Dynamic Media é compatível com o uso de HTTP/2, que fornece melhores tempos de resposta e carregamento.

Consulte [Entrega de conteúdo HTTP2](http2.md) para obter detalhes completos sobre a introdução ao uso de HTTP/2 com sua conta do Dynamic Media.
