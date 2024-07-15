---
title: Imagens panorâmicas
description: Saiba como trabalhar com imagens panorâmicas no Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Imagens panorâmicas{#panoramic-images}

Esta seção descreve como trabalhar com o Visualizador de imagens panorâmicas para renderizar imagens panorâmicas esféricas para obter uma experiência de visualização imersiva em 360 graus de uma sala, propriedade, localização ou paisagem.

Consulte também [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

![imagem panorâmica2](assets/panoramic-image2.png)

## Fazer upload de ativos para uso com o visualizador de imagens panorâmicas {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para que um ativo carregado seja qualificado como uma imagem panorâmica esférica que você pretende usar com o visualizador de Imagem panorâmica, o ativo deve ter uma ou ambas as opções a seguir:

* Uma taxa de proporção de 2.
Você pode substituir a configuração padrão de taxa de proporção de 2 em CRXDE Lite no seguinte local:
  `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Marcado com as palavras-chave `equirectangular` ou `spherical`e `panorama` ou `spherical` e `panoramic`. Consulte [Usando Tags](/help/sites-authoring/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos da página de detalhes do ativo e o componente WCM `Panoramic Media`.

Para carregar ativos para uso com o visualizador de Imagens panorâmicas, consulte [Carregar o Assets](/help/assets/manage-assets.md#uploading-assets).

## Configurar Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Para que o visualizador de imagens panorâmicas funcione corretamente no Adobe Experience Manager, sincronize as predefinições do visualizador de imagens panorâmicas com os metadados específicos do Dynamic Media Classic e do Dynamic Media Classic para que as predefinições do visualizador sejam atualizadas no JCR. Para fazer essa sincronização, configure o Dynamic Media Classic da seguinte maneira:

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Instalação]** > **[!UICONTROL Instalação do Aplicativo]** > **[!UICONTROL Instalação do Publish]** > **[!UICONTROL Servidor de Imagens]**.
1. Na página Publish do Servidor de imagens, no menu suspenso **[!UICONTROL Publish Context]** próximo à parte superior, selecione **[!UICONTROL Servidor de imagens]**.

1. Na mesma página do Publish do Servidor de imagens, localize o cabeçalho **[!UICONTROL Solicitar atributos]**.
1. No cabeçalho Atributos da Solicitação, localize **[!UICONTROL Limite de Tamanho da Imagem de Resposta]**. Em seguida, nos campos de Largura e Altura associados, aumente o tamanho máximo permitido da imagem para imagens panorâmicas.

   O Dynamic Media Classic tem um limite de 25.000.000 pixels. O tamanho máximo permitido para imagens com uma taxa de proporção de 2:1 é 7000 x 3500. No entanto, para telas de desktop típicas, 4096 x 2048 pixels é suficiente.

   >[!NOTE]
   >
   >Somente as imagens que estão dentro do tamanho máximo de imagem permitido são suportadas. As solicitações de imagens acima do limite de tamanho resultam em uma resposta 403.

1. No cabeçalho Atributos da solicitação, faça o seguinte:

   * Defina o Modo de Ofuscação da Solicitação como **[!UICONTROL Desabilitado]**.
   * Defina o Modo de Bloqueio de Solicitação como **[!UICONTROL Desabilitado]**.

   Essas configurações são necessárias para usar o componente WCM `Panoramic Media` no Experience Manager.

1. Na parte inferior da página Publish do Servidor de imagens, no lado esquerdo, selecione **[!UICONTROL Salvar]**.

1. No canto inferior direito, selecione **[!UICONTROL Fechar]**.

### Solução de problemas do componente Panorâmica Media WCM {#troubleshooting-the-panoramic-media-wcm-component}

Se você soltar uma imagem no componente de Mídia panorâmica em seu WCM e o alocador de espaço do componente recolher, solucione o seguinte:

* Se você encontrar um erro 403 Forbidden, ele pode ser causado pelo tamanho muito grande da imagem solicitada. Revise as configurações de **[!UICONTROL Limite de Tamanho da Imagem de Resposta]** em [Configurar Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Para um &quot;Bloqueio inválido&quot; no ativo ou &quot;Erro de análise&quot; exibido na página, marque o Modo de ofuscação de solicitação e o Modo de bloqueio de solicitação para garantir que eles estejam desativados.
* Para um erro de tela contaminada, configure um Caminho do arquivo de definição do conjunto de regras e invalide a CTN para as solicitações anteriores do ativo de imagem.
* Se a qualidade da imagem se tornar baixa após uma solicitação de imagem com dimensionamento acima do limite suportado, verifique se a configuração **[!UICONTROL Atributos de Codificação de JPEG > Qualidade]** não está vazia. Uma configuração típica do campo **[!UICONTROL Qualidade]** é `95`. Você pode encontrar a configuração na página Publish do servidor de imagens. Para acessar a página, consulte [Configurar Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Visualizar imagens panorâmicas {#previewing-panoramic-images}

Consulte [Visualizar Assets](/help/assets/previewing-assets.md).

## Imagens panorâmicas do Publish {#publishing-panoramic-images}

Consulte [Publish Assets](/help/assets/publishing-dynamicmedia-assets.md).
