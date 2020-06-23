---
title: Vincular URLs ao aplicativo da Web.
description: Como vincular URLs ao aplicativo da Web em mídia dinâmica
uuid: cf599e66-b1f9-40c0-b572-cea19f2e6793
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: d12e6ea3-aaf4-4672-9679-3c16c76d7d5b
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 11%

---


# Vincular URLs ao aplicativo da Web.{#linking-urls-to-your-web-application}

Seus sites e aplicativos acessam os serviços da Dynamic Media por meio de chamadas de URL. Depois de publicar um ativo, a Dynamic Media ativa uma string de URL que faz referência ao ativo. Você pode colar esses URLs em um navegador da Web para teste.

Você vincula a URLs somente se *não* estiver usando o AEM como seu WCM. A vinculação versus incorporação é usada quando você deseja fornecer um player de vídeo como uma janela pop-up ou modal. Se você estiver usando o AEM como seu WCM, [adicione os ativos diretamente na sua página.](adding-dynamic-media-assets-to-pages.md)

Para colocar essas strings de URL em suas páginas da Web e aplicativos, copie-as do Dynamic Media.

>[!NOTE]
>
>As strings de URL estão disponíveis somente para representações dinâmicas de ativos. No momento, eles não estão disponíveis para ativos estáticos que residem no DAM e não no servidor de mídia dinâmica. O botão URL não é exibido para execuções estáticas.

See also [Embedding the Video or Image Viewer on a Web Page.](embed-code.md)

See also [Linking YouTube URLs to your Web Application.](video.md)

See also [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

See also [Uploading Assets.](managing-assets-touch-ui.md#uploading-assets)

## Obter um URL para um ativo {#obtaining-a-url-for-an-asset}

Você pode obter uma string de URL gerada por uma predefinição de imagem ou por uma predefinição do visualizador. Depois de copiar o URL, ele aterrissa na Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL não estará disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição da imagem.
>
>Consulte [Publicação de ativos](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

Existem várias maneiras diferentes de obter uma string de URL. No entanto, as etapas abaixo mostram apenas um método que você pode usar.

**Para obter um URL para um ativo**

1. Navegue até o ativo *publicado* cujo URL predefinido de imagem ou URL predefinido do visualizador você deseja copiar e toque no ativo para abri-lo.

   Lembre-se de que os URLs só estão disponíveis para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicação de ativos.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. Com base no ativo selecionado, execute um dos procedimentos a seguir:

   * Se você selecionou uma imagem, no menu suspenso, toque em **[!UICONTROL Representações.]**

      No cabeçalho **[!UICONTROL Dinâmico]** , toque em um nome predefinido para visualização sua execução no quadro direito. Talvez seja necessário rolar a lista Representações para ver o cabeçalho Dinâmico.

      Na parte inferior do painel esquerdo, toque em **[!UICONTROL URL.]**

      ![chlimage_1-270](assets/chlimage_1-270.png)

   * Se você selecionou um conjunto de rotação, um conjunto de imagens, um conjunto de carrossel ou um vídeo, no menu suspenso, toque em **[!UICONTROL Visualizadores.]**

      No painel esquerdo, toque no nome predefinido do visualizador. Uma pré-visualização do conjunto ou do vídeo é aberta em uma página separada.

      No painel esquerdo, na parte inferior, toque em **[!UICONTROL URL.]**

      ![chlimage_1-271](assets/chlimage_1-271.png)

1. Selecione e copie o texto no navegador da Web para pré-visualização do ativo ou para adicionar à página de conteúdo da Web.

   Para sair da janela URL, toque no **[!UICONTROL X]** ou em **[!UICONTROL Fechar.]**

## Obter um URL para um ativo estático {#obtaining-a-url-for-a-static-asset}

A Dynamic Media suporta o delivery de ativos estáticos, que são ativos adicionais além de imagens e vídeos. Os formatos de ativos estáticos suportados para o delivery incluem:

* arquivos 3D
* GIF animado
* Arquivos de áudio
* CSS
* JavaScript (quando sua empresa é configurada com seu próprio domínio)
* PDF
* SVG
* XML
* ZIP

**Para obter um URL para um ativo estático**

1. Navegue até o ativo estático *publicado* cujo URL você deseja copiar e toque no ativo para abri-lo.

   Remember that URLs are only available to copy *after* you have first *published* the static asset.

   Consulte [Publicação de ativos](publishing-dynamicmedia-assets.md).

1. Use qualquer um dos seguintes métodos para obter o URL do ativo estático publicado:

   * `The URL of the published static is the following:`

      * `https://*<server_name>*/is/content/*<company_name>*/*<static_asset_filename>*.*<extension>*`

         Por exemplo, `https://aem.com/is/content/adobe/image.gif`.
   * Toque em **[!UICONTROL Ativo > Representações]** dinâmicas e, em seguida, toque em uma representação dinâmica do ativo estático e copie o URL.

      Altere o URL copiado para usar `is/content` no caminho em vez de `is/image/`.


## Obter um URL de vídeo para uma execução de vídeo publicada {#obtaining-a-video-url-for-a-published-video-rendition}

1. No AEM, navegue até **[!UICONTROL Ferramentas > Implantação > Nuvem > Cloud Service.]**
1. Na página **[!UICONTROL Serviços da nuvem]**, role até o cabeçalho **[!UICONTROL Serviços de nuvem do Dynamic Media]** e toque em **[!UICONTROL Mostrar configurações.]**
1. Em **[!UICONTROL Configurações disponíveis]**, toque no nome da configuração desejada.

1. Na página Configurações **[!UICONTROL da]** Dynamic Media Cloud, em URL **[!UICONTROL do serviço de]** vídeo, copie todo o caminho do URL. Você precisará do caminho do URL copiado posteriormente nas etapas.

   Por exemplo, o caminho do URL pode ser exibido da seguinte maneira:

   `https://s7athens.macromedia.com:9090/DMGateway/`

   (O caminho acima serve apenas para fins ilustrativos; não é o caminho real que você copia.)

1. Em **[!UICONTROL ID de registro]**, copie o nome do cliente encontrado na última parte da ID.

   Por exemplo, se a ID de registro fosse `87654321|MyCompany`, o nome do cliente seria `MyCompany`.

1. Perto do canto superior esquerdo da página, toque em **[!UICONTROL Cloud Service**, toque no logotipo Experience Manager e navegue até **[!UICONTROL General > CRXDE Lite.]**
1. Copie todo o caminho de execução do vídeo do JCR (Java Content Repository).

   Por exemplo, o caminho de renderização do vídeo pode aparecer de maneira semelhante ao seguinte:

   `/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112f/avs/Momentum_1080-0x720-2600k.mp4`

   (O caminho acima serve apenas para fins ilustrativos; não é o caminho real que você copia.)

1. Organize as informações copiadas na seguinte ordem para formar um caminho de URL completo:

   `<Video_Service_URL>/public/<Customer_name_from_Registration_ID>/<Video_rendition_path>`

   Por exemplo, usando os caminhos de exemplo e o nome de exemplo do cliente das etapas acima, o caminho completo é exibido da seguinte maneira:

   `https://s7athens.macromedia.com:9090/DMGateway/public/MyCompany/_renditions_/0bd/0bd28743-a616-4fe6-92aa-6eae7c2112ff/avs/Momentum_1080-0x720-2600k.mp4`

   Este é o URL completo do vídeo para uma execução de vídeo publicada.

## Obter um URL de vídeo para transmissão adaptável (HLS) {#obtaining-a-video-url-for-adaptive-streaming-hls}

1. No AEM, navegue até **[!UICONTROL Ferramentas > Implantação > Nuvem > Cloud Service.]**
1. Na página **[!UICONTROL Serviços da nuvem]**, role até o cabeçalho **[!UICONTROL Serviços de nuvem do Dynamic Media]** e toque em **[!UICONTROL Mostrar configurações.]**
1. Em **[!UICONTROL Configurações disponíveis]**, toque no nome da configuração desejada.
1. Na página Configurações **[!UICONTROL do]** Dynamic Media Cloud Service, faça o seguinte:

   * Em URL **[!UICONTROL do serviço de]** vídeo, copie o caminho do URL inteiro. Você precisará do caminho do URL copiado posteriormente nessas etapas. Por exemplo, o caminho do URL pode ser exibido da seguinte maneira:
   `https://gateway-na.assetsadobe.com/DMGateway/`

   (O caminho acima serve apenas para fins ilustrativos; não é o caminho real que você copia.)

   * Em **[!UICONTROL ID de registro]**, copie o nome do cliente encontrado na última parte da ID. Posteriormente, você precisará do nome do cliente copiado nessas etapas.

      Por exemplo, se a ID de registro fosse `87654321|demoCo`o nome do cliente que você copiar seria `demoCo`.


1. Com base no protocolo de delivery de vídeo que você está usando, copie o respectivo seletor de protocolo. Você precisará do seletor de protocolo copiado posteriormente nessas etapas.

   | Protocolo de delivery de vídeo que você está usando | Seletor de protocolo a ser usado |
   |---|---|
   | HTTP <br> Se estiver usando HTTP (delivery de vídeo não seguro), certifique-se de alterar https para http no valor do URL do Serviço de vídeo copiado anteriormente. | `public/` |
   | HTTPS | `public-ssl/` |

1. Copie o caminho completo do ativo de vídeo no AEM, conforme processado pela Dynamic Media. Você precisará desse caminho de ativo de vídeo copiado posteriormente nessas etapas.

   Por exemplo:

   `/content/dam/marketing/MyVideo.mp4`

1. Combine todas as partes copiadas anteriormente para criar uma string na seguinte ordem:

   &lt; `video service URL`>&lt; `protocol selector`>&lt; `customer name`>&lt; `video asset path`>

   Por exemplo, usando as informações copiadas dos exemplos nessas etapas, a string apareceria da seguinte maneira:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4`

1. Preencha o URL anexando `.m3u8` ao final da string. Por exemplo, anexando `.m3u8` à string da etapa anterior, o caminho de URL completo apareceria da seguinte maneira:

   `https://gateway-na.assetsadobe.com/DMGateway/public-ssl/demoCo/content/dam/marketing/MyVideo.mp4.m3u8`

## Usar HTTP/2 para fornecer seus ativos Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Fornece transferência de informações mais rápida e reduz a quantidade de poder de processamento necessário. O Delivery dos ativos Dynamic Media agora pode estar acima de HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte Delivery [HTTP2 de conteúdo](http2.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta Dynamic Media.
