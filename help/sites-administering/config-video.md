---
title: Configurar o componente Vídeo
seo-title: Configurar o componente Vídeo
description: Saiba como configurar o Componente de vídeo.
seo-description: Saiba como configurar o Componente de vídeo.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
translation-type: tm+mt
source-git-commit: 44dbabeeea4e4e8d17cc69a2d8ea791c98be2bd2
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 7%

---


# Configurar o componente Vídeo {#configure-the-video-component}

O componente [](/help/sites-authoring/default-components-foundation.md#video) Vídeo permite que você coloque um elemento de vídeo OOTB (out-of-the-box) predefinido na sua página.

Para que ocorra a transcodificação correta, o administrador deve [instalar o FFmpeg e configurar o AEM](#install-ffmpeg) separadamente. Eles também podem [Configurar os perfis de vídeo](#configure-video-profiles) para uso com elementos de HTML5.

## Configurar perfis de vídeo {#configure-video-profiles}

Talvez você queira definir perfis de vídeo para usar em elementos HTML5. Os escolhidos aqui são usados em ordem. Para acessar, use o Modo [de](/help/sites-authoring/default-components-designmode.md) design (somente Interface clássica) e selecione a guia **[!UICONTROL Perfis]** :

![chlimage_1-317](assets/chlimage_1-317.png)

Você também pode configurar o design dos componentes e parâmetros do vídeo para [!UICONTROL Reprodução], [!UICONTROL Flash]e [!UICONTROL Advanced].

## Instalar FFmpeg e configurar o AEM {#install-ffmpeg}

The Video Component relies on the third-party open-source product FFmpeg for proper transcoding of videos that can be downloaded from [https://ffmpeg.org/](https://ffmpeg.org/). Depois de instalar o FFmpeg, é necessário configurar o AEM para usar um codec de áudio específico e opções específicas de tempo de execução.

**Para instalar o FFmpeg para a sua plataforma**:

* **No Windows:**

   1. Baixar o binário compilado como `ffmpeg.zip`
   1. Descompacte para uma pasta.
   1. Defina a variável de ambiente do sistema `PATH` como `<*your-ffmpeg-locatio*n>\bin`
   1. Reinicie o AEM.

* **No Mac OS X:**

   1. Instalar Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. Instale o XQuartz/X11.
   1. Instalar MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. No console, execute o seguinte comando e siga as instruções:

      `sudo port install ffmpeg`

      `FFmpeg` deve estar em `PATH` modo que o AEM possa selecioná-lo por meio da linha de comando.

* **Usar a versão pré-compilada para o OS X 10.6:**

   1. Baixe a versão pré-compilada.
   1. Extraia-o para o `/usr/local` diretório.
   1. No terminal, execute:

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**Para configurar o AEM**:

>[!NOTE]
>
>Essas etapas só são necessárias se for necessária uma personalização adicional dos codecs.

1. Open [!UICONTROL CRXDE Lite] in your web browser. ([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
2. Selecione o `/libs/settings/dam/video/format_aac/jcr:content` nó e verifique se as propriedades do nó são as seguintes:

   * audioCodec:

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

3. Para personalizar a configuração, crie uma sobreposição no `/apps/settings/` nó e mova a mesma estrutura sob o `/conf/global/settings/` nó. Não pode ser editado no `/libs` nó. Por exemplo, para sobrepor o caminho `/libs/settings/dam/video/fullhd-bp`, crie-o em `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sobreponha e edite todo o nó do perfil e não apenas a propriedade que precisa de modificação. Tais recursos não são resolvidos através da SlingResourceFusão.

4. If you changed either of the properties, click **[!UICONTROL Save All]**.

>[!NOTE]
>
>Os modelos de fluxo de trabalho OTB não são preservados quando você atualiza sua instância do AEM. A Adobe recomenda que você copie modelos de fluxo de trabalho OOTB antes de editá-los. Por exemplo, copie o modelo de Ativo [!UICONTROL de atualização de] DAM OOTB antes de editar a etapa de Transcodificação de FFmpeg no modelo de Ativo [!UICONTROL de atualização de] DAM para escolher nomes de perfis de vídeo existentes antes da atualização. Em seguida, você pode sobrepor o `/apps` nó para permitir que o AEM recupere as alterações personalizadas no modelo OOTB.

