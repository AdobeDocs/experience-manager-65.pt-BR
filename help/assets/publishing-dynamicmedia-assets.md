---
title: Publicação de ativos Dynamic Media
description: Como publicar ativos do Dynamic Media
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 4%

---

# Publicar ativos do Dynamic Media {#publishing-dynamic-media-assets}

Publique seus ativos do Dynamic Media selecionando os ativos que você já carregou e tocando **[!UICONTROL Publicar]** ou **[!UICONTROL Publicação rápida]**. Depois que os ativos da Dynamic Media forem publicados, eles estarão disponíveis para inclusão em uma página da Web por meio de um URL ou ao incorporar o código na página.

Você também pode publicar instantaneamente os ativos que você faz upload, sem nenhuma intervenção do usuário. Consulte [Configurar o Dynamic Media - Modo Scene7](config-dms7.md).
Ou, você pode publicar ativos seletivamente na Dynamic Media ou na Adobe Experience Manager, mutuamente exclusivos entre si, usando **[!UICONTROL Publicação seletiva]** no nível da pasta. Consulte [Trabalhar com publicação seletiva no Dynamic Media](/help/assets/selective-publishing.md).

No **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já estiver publicado, use o Experience Manager para movê-lo para outra pasta e republicar de seu novo local. O local do ativo publicado original ainda está disponível, juntamente com o ativo republicado recentemente. O ativo publicado original, no entanto, é &quot;perdido&quot; para o Experience Manager e não pode ter a publicação cancelada. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após codificá-los, verifique se a codificação foi feita. Enquanto os vídeos estão sendo codificados, o sistema informa que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você poderá visualizar as representações de vídeo. Nesse momento, é seguro publicar os vídeos sem incorrer em erros de publicação.

Consulte também [Vincular URLs ao seu aplicativo web](linking-urls-to-yourwebapplication.md).

Consulte também [Incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web](embed-code.md)

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para entrega ao vivo.
>


Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicar ativos](manage-assets.md).

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/sites-administering/scene7-http2faq.md).
