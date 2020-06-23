---
title: Publicação de ativos Dynamic Media
description: Como publicar ativos de mídia dinâmica
uuid: b1bee905-86cf-4284-8d4e-067e11557899
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 99d7025f-d022-4213-83c0-815a4712c573
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 3%

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Você publica seus ativos do Dynamic Media selecionando os ativos que já carregou e tocando em **[!UICONTROL Publicar]** ou Publicação **[!UICONTROL rápida.]** Após a publicação dos ativos Dynamic Media, eles estarão disponíveis para inclusão em uma página da Web por meio de um URL ou da incorporação do código na página.

Você também pode publicar instantaneamente ativos que você carrega, sem nenhuma intervenção do usuário. Consulte [Configuração do Dynamic Media - modo](config-dms7.md)Scene7.

Na Visualização **[!UICONTROL de]** cartão, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já tiver sido publicado, você usará o AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para o AEM e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após a codificação, certifique-se de que a codificação esteja concluída. Quando os vídeos ainda estão sendo codificados, o sistema permite que você saiba que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você poderá pré-visualização as execuções de vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

See also [Embedding the Dynamic Media Video or Image viewer on a web page](embed-code.md)

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para o delivery ao vivo.

>



Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicação de ativos.](managing-assets-touch-ui.md)

## delivery HTTP/2 de ativos Dynamic Media {#http-delivery-of-dynamic-media-assets}

O AEM agora oferece suporte ao delivery de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Este método de delivery melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos Dynamic Media.

Consulte Perguntas frequentes sobre o delivery [HTTP/2 sobre conteúdo](/help/sites-administering/scene7-http2faq.md) para saber mais.
