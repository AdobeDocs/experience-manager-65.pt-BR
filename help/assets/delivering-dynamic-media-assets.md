---
title: Entregar ativos do Dynamic Media
description: Saiba como fornecer ativos do Dynamic Media, como vídeo e imagens, às suas páginas da Web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:05.823Z'
TQID: 'https://experienceleague.adobe.com/a5ifneRAYCIMHKCGJHGQu9aoQt3EWZu1hiGYItlPZOE'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: e42ab83e-8918-43a7-98a3-62bebbd5bb3a
    internal-label: Renditions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 9%
---
# Entregar ativos do Dynamic Media{#delivering-dynamic-media-assets}

A maneira de fornecer os ativos do Dynamic Media, como vídeo e imagens, depende de como seu site é implementado.

Com o Dynamic Media, você tem várias opções:

* Se o site estiver hospedado no Adobe Experience Manager, será necessário adicionar os ativos do Dynamic Media diretamente à página.
* Se o seu site não estiver no Experience Manager, você terá a opção de:

  * Incorporar o vídeo ou a imagem no site.
  * Vincule URLs ao aplicativo da Web. Use a vinculação quando quiser fornecer um reprodutor de vídeo como uma janela pop-up ou modal.
  * Se o seu site é responsivo, você pode [fornecer imagens otimizadas](/help/assets/responsive-site.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com suas predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Smart Imaging](/help/assets/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos do Dynamic Media a páginas da Web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporar o visualizador de vídeo ou imagem em uma página da Web](/help/assets/embed-code.md)
* [Ativar proteção de hotlink no Dynamic Media](/help/assets/hotlink-protection.md)
* [Vincular URLs ao seu aplicativo web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Entregar imagens otimizadas para um site responsivo](/help/assets/responsive-site.md)
* [Entrega de conteúdo HTTP2](/help/assets/http2.md)
* [Invalidar o cache da CDN por meio do Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Usar conjuntos de regras para transformar URLs](/help/assets/using-rulesets-to-transform-urls.md)


## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo melhores tempos de resposta e carregamento de todos os ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/sites-administering/scene7-http2faq.md).
