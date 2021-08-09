---
title: Imagens panorâmicas
description: Saiba como trabalhar com imagens panorâmicas no Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Imagens panorâmicas,Gerenciamento de ativos
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Imagens panorâmicas{#panoramic-images}

Esta seção descreve como trabalhar com o visualizador de Imagem panorâmica para renderizar imagens panorâmicas esféricas para uma experiência de visualização imersiva de 360° de uma sala, propriedade, localização ou paisagem.

Consulte também [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

![panorâmica-imagem2](assets/panoramic-image2.png)

## Fazer upload de ativos para usar com o visualizador de Imagem panorâmica {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para que um ativo carregado seja qualificado como uma imagem panorâmica esférica que você pretende usar com o visualizador de Imagem panorâmica, o ativo deve ter um ou ambos os itens a seguir:

* Uma proporção largura/altura de 2.
Você pode substituir a configuração padrão de proporção de aspecto de 2 em CRXDE Lite no seguinte:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Marcado com as palavras-chave `equirectangular`, ou `spherical`e `panorama`, ou `spherical` e `panoramic`. Consulte [Uso de tags](/help/sites-authoring/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos da página de detalhes do ativo e do componente `Panoramic Media` WCM.

Para fazer upload de ativos para uso com o visualizador de Imagem panorâmica, consulte [Fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).

## Configurar o Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Para que o visualizador de Imagem panorâmica funcione corretamente no Adobe Experience Manager, sincronize as predefinições do visualizador de Imagem panorâmica com os metadados específicos do Dynamic Media Classic e do Dynamic Media Classic, de modo que as predefinições do visualizador sejam atualizadas no JCR. Para realizar essa sincronização, configure o Dynamic Media Classic da seguinte maneira:

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Configurar]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Publicar configuração]** > **[!UICONTROL Servidor de imagem]**.
1. Na página Publicação do servidor de imagens, no menu suspenso **[!UICONTROL Publicar contexto]** próximo à parte superior, selecione **[!UICONTROL Serviço de imagens]**.

1. Na mesma página Publicação do servidor de imagens, localize o cabeçalho **[!UICONTROL Atributos da solicitação]**.
1. No cabeçalho Atributos da solicitação , localize **[!UICONTROL Limite do tamanho da imagem de resposta]**. Em seguida, nos campos Largura e Altura associados, aumente o tamanho máximo permitido da imagem para imagens panorâmicas.

   O Dynamic Media Classic tem um limite de 25.000.000 pixels. O tamanho máximo permitido para imagens com uma proporção de aspecto de 2:1 é 7000 x 3500. No entanto, para telas típicas de desktop, 4096 x 2048 pixels é suficiente.

   >[!NOTE]
   >
   >Somente imagens que se encaixam no tamanho máximo permitido da imagem são suportadas. As solicitações de imagens acima do limite de tamanho resultam em uma resposta 403.

1. No cabeçalho Atributos da solicitação , faça o seguinte:

   * Defina o Modo de ofuscação de solicitação para **[!UICONTROL Desativado]**.
   * Defina o Modo de bloqueio de solicitação para **[!UICONTROL Desativado]**.

   Essas configurações são necessárias para usar o componente `Panoramic Media` WCM no Experience Manager.

1. Na parte inferior da página Publicação do servidor de imagens, no lado esquerdo, selecione **[!UICONTROL Salvar]**.

1. No canto inferior direito, selecione **[!UICONTROL Fechar]**.

### Solução de problemas do componente Panorâmica Media WCM {#troubleshooting-the-panoramic-media-wcm-component}

Se você soltou uma imagem no componente Mídia panorâmica no WCM e o placeholder do componente diminuiu, solucione os seguintes problemas:

* Se você passar por um erro 403 Forbidden , isso pode ser causado pelo tamanho da imagem solicitada ser muito grande. Revise as configurações do **[!UICONTROL Limite de tamanho da imagem de resposta]** em [Configurar Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Para um &quot;Bloqueio inválido&quot; no ativo ou &quot;Erro de análise&quot; exibido na página, marque Request Ofuscation Mode e Request Locking Mode para garantir que eles estejam desativados.
* Para um erro de tela contaminada, configure um Caminho de arquivo de definição de conjunto de regras e Invalide o CTN para as solicitações anteriores para o ativo de imagem.
* Se a qualidade da imagem se tornar baixa depois de uma solicitação de imagem com dimensionamento acima do limite suportado, verifique se a configuração **[!UICONTROL JPEG Encoding Attributes > Quality]** não está vazia. Uma configuração típica para o campo **[!UICONTROL Qualidade]** é `95`. Você pode encontrar a configuração na página Publicação do servidor de imagens . Para acessar a página, consulte [Configurar o Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Visualizar imagens panorâmicas {#previewing-panoramic-images}

Consulte [Visualizar ativos](/help/assets/previewing-assets.md).

## Publicar imagens panorâmicas {#publishing-panoramic-images}

Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).
