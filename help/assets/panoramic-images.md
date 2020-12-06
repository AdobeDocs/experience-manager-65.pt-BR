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
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Imagens panorâmicas{#panoramic-images}

Esta seção descreve como trabalhar com o visualizador Imagem panorâmica para renderizar imagens panorâmicas esféricas para uma experiência de visualização de 360° imersiva de uma sala, propriedade, local ou paisagem.

Consulte também [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

![panorâmica-image2](assets/panoramic-image2.png)

## Fazer upload de ativos para uso com o Visualizador de imagem panorâmica {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Para um ativo carregado se qualificar como uma imagem de panorama esférica que você pretende usar com o visualizador de Imagem panorâmica, o ativo deve ter um ou ambos os seguintes itens:

* Uma proporção largura/altura de 2.
Você pode substituir a configuração padrão de proporção de 2 no CRXDE Lite no seguinte:
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Marcado com as palavras-chave `equirectangular`, ou `spherical` e `panorama`, ou `spherical` e `panoramic`. Consulte [Usando tags](/help/sites-authoring/tags.md).

Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos para a página de detalhes do ativo e o componente `Panoramic Media` WCM.

Para fazer upload de ativos para uso com o visualizador de Imagem panorâmica, consulte [Fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).

## Configuração do Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Para que o visualizador de Imagem panorâmica funcione corretamente no AEM, é necessário sincronizar as predefinições do visualizador de Imagem panorâmica com os metadados específicos do Dynamic Media Classic e do Dynamic Media Classic para que as predefinições do visualizador sejam atualizadas no JCR. Para fazer isso, configure o Dynamic Media Classic da seguinte maneira:

1. [Faça logon na sua instância do Dynamic Media ](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) Classicpara cada conta de empresa.

1. Perto do canto superior direito da página, clique em **[!UICONTROL Configuração > Configuração de Aplicativo > Configurar Publicação > Servidor de Imagem.]**
1. Na página de Publicação do Servidor de Imagens, no menu suspenso **[!UICONTROL Publicar Contexto]** próximo ao topo, selecione **[!UICONTROL Serviço de Imagens.]**

1. Na mesma página de Publicação do Servidor de Imagens, localize o cabeçalho **[!UICONTROL Atributos de Solicitação.]**
1. No cabeçalho Request Attributes (Atributos de solicitação), localize **[!UICONTROL Reply Image Size Limit (Limite de tamanho de imagem de resposta).]** Em seguida, nos campos Largura e Altura associados, aumente o tamanho máximo permitido da imagem para imagens panorâmicas.

   O Dynamic Media Classic tem um limite de 25.000.000 pixels. O tamanho máximo permitido para imagens com uma proporção de 2:1 é 7000 x 3500. No entanto, para telas típicas de desktop, 4096 x 2048 pixels são suficientes.

   >[!NOTE]
   >
   >Somente as imagens que se encaixam no tamanho máximo permitido de imagem são suportadas. As solicitações de imagens acima do limite de tamanho resultarão em uma resposta 403.

1. Em Atributos de solicitação, faça o seguinte:

   * Defina o Modo de ofuscação de solicitação como **[!UICONTROL Desativado.]**
   * Defina o Modo de Bloqueio de Solicitação como **[!UICONTROL Desativado.]**

   Essas configurações são necessárias para usar o componente `Panoramic Media` WCM no AEM.

1. Na parte inferior da página Publicação do Servidor de Imagens, no lado esquerdo, clique em **[!UICONTROL Salvar.]**

1. No canto inferior direito, clique em **[!UICONTROL Fechar.]**

### Solução de problemas do componente WCM de mídia panorâmica {#troubleshooting-the-panoramic-media-wcm-component}

Se você soltou uma imagem no componente de Mídia panorâmica em seu WCM e o espaço reservado do componente desabou, talvez você queira solucionar o seguinte problema:

* Se você encontrar um erro 403 Proibido, ele pode ter sido causado pelo tamanho da imagem solicitada ser muito grande. Revise as configurações **[!UICONTROL Reply Image Size Limit]** em [Configuração do Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* Para um &quot;Bloqueio inválido&quot; no ativo ou &quot;Erro de análise&quot; exibido na página, marque Modo de ofuscação de solicitação e Modo de bloqueio de solicitação para garantir que eles estejam desativados.
* Para um erro de tela contaminada, configure um Caminho de arquivo de definição de conjunto de regras e Invalide o CTN para as solicitações anteriores do ativo de imagem.
* Se a qualidade da imagem ficar muito baixa depois de uma solicitação de imagem com dimensionamento acima do limite suportado, verifique se a configuração **[!UICONTROL Atributos de codificação JPEG > Quality]** não está vazia. Uma configuração típica para o campo **[!UICONTROL Quality]** é `95`. Você pode encontrar a configuração na página Publicação do Servidor de imagens. Para acessar a página, consulte [Configuração do Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Visualização de imagens panorâmicas {#previewing-panoramic-images}

Consulte [Visualizar ativos](/help/assets/previewing-assets.md).

## Publicar imagens panorâmicas {#publishing-panoramic-images}

Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).
