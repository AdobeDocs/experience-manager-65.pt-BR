---
title: Entrega de ativos de Mídia dinâmica
description: Saiba como fornecer ativos de mídia dinâmica
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Entrega de ativos de Mídia dinâmica{#delivering-dynamic-media-assets}

A forma como você pode fornecer seus ativos de mídia dinâmica - vídeo e imagens - depende de como seu site é implementado.

Com a Mídia dinâmica, você tem várias opções:

* Se o seu site estiver hospedado no AEM, convém adicionar os ativos de mídia dinâmica diretamente à sua página.
* Se o seu site não estiver no AEM, você terá a opção de:

   * Incorporar seu vídeo ou imagem em seu site.
   * Vincule URLs ao aplicativo da Web. Use a vinculação quando quiser fornecer um player de vídeo como uma janela pop-up ou modal.
   * Se o site estiver respondendo, você poderá [fornecer imagens otimizadas.](/help/assets/responsive-site.md)

>[!NOTE]
>
>A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo de entrega para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte Imagens [inteligentes](/help/assets/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos de mídia dinâmica a páginas da Web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/embed-code.md)
* [Ativação da proteção de hotlink no Dynamic Media](https://helpx.adobe.com/experience-manager/6-4/help/assets/hotlink-protection.html)
* [Vincular URLs ao seu aplicativo da Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Fornecer imagens otimizadas para um site responsivo](/help/assets/responsive-site.md)
* [Entrega HTTP2 de conteúdo](/help/assets/http2.md)
* Eu [invalido seu conteúdo em cache CDN](/help/assets/invalidate-cdn-cached-content.md)
* [Uso de conjuntos de regras para transformar URLs](/help/assets/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O AEM agora oferece suporte à entrega de todo o conteúdo de Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os ativos do Dynamic Media.

Consulte [HTTP/2 Entrega de Perguntas](/help/sites-administering/scene7-http2faq.md) frequentes sobre conteúdo para saber mais.
