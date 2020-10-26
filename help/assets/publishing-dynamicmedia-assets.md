---
title: Publicação de ativos de mídia dinâmica
description: Como publicar ativos de mídia dinâmica
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Você publica seus ativos de Mídia dinâmica selecionando os ativos que já carregou e tocando em **[!UICONTROL Publicar]** ou Publicar **[!UICONTROL rapidamente.]** Depois que seus ativos de Mídia dinâmica forem publicados, eles estarão disponíveis para você incluir em uma página da Web por meio de um URL ou da incorporação do código na página.

Você também pode publicar instantaneamente ativos que você carrega, sem nenhuma intervenção do usuário. Consulte [Configuração do Dynamic Media - Modo Scene7.](config-dms7.md)
Ou você pode publicar seletivamente ativos no Dynamic Media ou AEM, mutuamente exclusivos entre si, usando Publicação **** seletiva no nível da pasta. See [Working with Selective Publish in Dynamic Media.](/help/assets/selective-publishing.md)

Na Visualização **[!UICONTROL de]** cartão, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já estiver publicado, você usará AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para AEM e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após a codificação, certifique-se de que a codificação esteja concluída. Quando os vídeos ainda estão sendo codificados, o sistema permite que você saiba que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você poderá pré-visualização as execuções de vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para o delivery ao vivo.

>



Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicação de ativos.](manage-assets.md)

## DELIVERY HTTP/2 de ativos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM agora suporta o delivery de todo o conteúdo de Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Este método de delivery melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos de Dynamic Media.

Consulte Perguntas frequentes sobre o delivery [HTTP/2 sobre conteúdo](/help/sites-administering/scene7-http2faq.md) para saber mais.
