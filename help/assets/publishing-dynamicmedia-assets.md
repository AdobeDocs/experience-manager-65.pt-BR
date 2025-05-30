---
title: Publicação do Dynamic Media Assets
description: Saiba como publicar ativos do Dynamic Media, como vídeos e imagens, incluindo a entrega HTTP/2 desses ativos.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 750627fc-2a29-43ff-867e-55cb2e371043
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Publicar ativos do Dynamic Media {#publishing-dynamic-media-assets}

Publique seus ativos do Dynamic Media selecionando os ativos que você já carregou e tocando em **[!UICONTROL Publish]** ou **[!UICONTROL Quick Publish]**. Depois que os ativos do Dynamic Media forem publicados, eles estarão disponíveis para inclusão em uma página da Web por meio de um URL ou pela incorporação do código na página da Web.

Você também pode publicar instantaneamente os ativos que carregou, sem nenhuma intervenção do usuário. Consulte [Configurar Dynamic Media - Modo Scene7](config-dms7.md).
Ou você pode publicar seletivamente ativos no Dynamic Media ou no Adobe Experience Manager, mutuamente exclusivos entre si, usando a **[!UICONTROL Publish Seletiva]** no nível da pasta. Consulte [Trabalhar com Publish seletiva no Dynamic Media](/help/assets/selective-publishing.md).

Na **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já estiver publicado, use o Experience Manager para movê-lo para outra pasta e republicar a partir do novo local. O local do ativo original publicado ainda está disponível, juntamente com o ativo recém-republicado. No entanto, o ativo original publicado é &quot;perdido&quot; para o Experience Manager e não pode ter a publicação desfeita. Portanto, como prática recomendada, cancele a publicação de ativos antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após codificá-los, certifique-se de que a codificação foi feita. Enquanto os vídeos estão sendo codificados, o sistema permite que você saiba que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação do vídeo for concluída, você poderá pré-visualizar as representações do vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

Consulte também [Vincular URLs ao Aplicativo Web](linking-urls-to-yourwebapplication.md).

Consulte também [Incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web](embed-code.md)

>[!NOTE]
>
>* O Assets deve ser publicado para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador não funcionará.
>* As predefinições de imagem e do visualizador devem ser ativadas e publicadas para entrega em tempo real.
>

Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [ativos do Publish](manage-assets.md).

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) via HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo melhores tempos de resposta e carregamento de todos os ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/sites-administering/scene7-http2faq.md).
