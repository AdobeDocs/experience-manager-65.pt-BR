---
title: Entregar ativos do Dynamic Media
description: Saiba como fornecer ativos do Dynamic Media
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 13%

---

# Entregar ativos do Dynamic Media{#delivering-dynamic-media-assets}

A maneira de fornecer os ativos da Dynamic Media - vídeo e imagens - depende de como o site está implementado.

Com o Dynamic Media, você tem várias opções:

* Se seu site estiver hospedado no Adobe Experience Manager, você deseja adicionar os ativos do Dynamic Media diretamente à sua página.
* Se o seu site não estiver no Experience Manager, você terá a opção de:

   * Incorporação do vídeo ou imagem ao seu site.
   * Vincule URLs ao aplicativo da Web. Use a vinculação quando desejar fornecer um reprodutor de vídeo como uma janela pop-up ou modal.
   * Se seu site for responsivo, você poderá [fornecer imagens otimizadas](/help/assets/responsive-site.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagem inteligente](/help/assets/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos do Dynamic Media às páginas da Web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporar o visualizador de vídeo ou imagem em uma página da Web](/help/assets/embed-code.md)
* [Ativar proteção de hotlink no Dynamic Media](/help/assets/hotlink-protection.md)
* [Vincular URLs ao seu aplicativo web.](/help/assets/linking-urls-to-yourwebapplication.md)
* [Entregar imagens otimizadas para um site responsivo](/help/assets/responsive-site.md)
* [Entrega de conteúdo HTTP2](/help/assets/http2.md)
* [Invalidar o cache CDN por meio do Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Usar conjuntos de regras para transformar URLs](/help/assets/using-rulesets-to-transform-urls.md)


## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/sites-administering/scene7-http2faq.md).
