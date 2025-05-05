---
title: Configurar o componente de Vídeo
description: Saiba como usar o componente de Vídeo no Adobe Experience Manager para colocar um ativo de vídeo predefinido e pronto para uso na sua página.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---

# Configurar o componente de Vídeo {#configure-the-video-component}

O [componente de Vídeo](/help/sites-authoring/default-components-foundation.md#video) permite que você coloque um ativo de vídeo predefinido e pronto para uso na sua página.

Para que ocorra a transcodificação adequada, um administrador instala o FFmpeg separadamente. Consulte [Instalar FFmpeg e configurar AEM](#install-ffmpeg). Os administradores também [configuram perfis de vídeo](#configure-video-profiles) para usar com elementos HTML5.

>[!CAUTION]
>
>Esse componente de base foi descontinuado. A Adobe recomenda usar o [Componente de Incorporação dos Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/embed.html?lang=pt-BR).

>[!CAUTION]
>
>Não se espera mais que esse componente funcione imediatamente sem uma ampla personalização no nível do projeto.

## Configurar perfis de vídeo {#configure-video-profiles}

Para o uso de elementos HTML5, defina perfis de vídeo. Os escolhidos aqui são usados em ordem. Para acessar, use o [Modo de Design](/help/sites-authoring/default-components-designmode.md) (somente a interface clássica) e selecione a guia **[!UICONTROL Perfis]**:

![chlimage_1-317](assets/chlimage_1-317.png)

Nesta caixa de diálogo, você também pode configurar o design do componente de Vídeo e os parâmetros para [!UICONTROL Reprodução], [!UICONTROL Flash] e [!UICONTROL Avançado].

## Instale o FFmpeg e configure o AEM {#install-ffmpeg}

O componente de Vídeo depende do produto de código aberto FFmpeg de terceiros para transcodificação de vídeos. Baixado de [https://ffmpeg.org/](https://ffmpeg.org/). Após instalar o FFmpeg, configure o AEM para usar um codec de áudio específico e opções específicas de tempo de execução.

Para instalar o FFmpeg no **Windows**, siga estas etapas:

1. Baixar o binário compilado como `ffmpeg.zip`.
1. Desarquivar em uma pasta.
1. Defina a variável de ambiente do sistema `PATH` como &lt;*your-ffmpeg-location*>`\bin`.
1. Reinicie o AEM.

Para instalar o FFmpeg no **macOS X**, siga estas etapas:

1. Instale o Xcode disponível em [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Instalação disponível em [XQuartz](https://www.xquartz.org) para obter [X11](https://support.apple.com/en-us/100724).
1. Instale o MacPorts disponível em [www.macports.org](https://www.macports.org/).
1. No console, execute o comando `sudo port install ffmpeg` e siga as instruções na tela. Verifique se o caminho do executável `FFmpeg` foi adicionado à variável de sistema `PATH`.

Para instalar o FFmpeg no **macOS X 10.6** usando a versão pré-compilada, siga estas etapas:

1. Baixe a versão pré-compilada.
1. Desarquive no diretório `/usr/local`.
1. No console, execute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Altere o caminho conforme apropriado.

Para **configurar o AEM**, siga estas etapas:

>[!NOTE]
>
>Essas etapas só serão necessárias se for necessária uma personalização adicional dos codecs.

1. Abra o [!UICONTROL CRXDE Lite] no navegador da Web. Acessar [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Selecione o nó `/libs/settings/dam/video/format_aac/jcr:content` e verifique se as propriedades do nó são as seguintes:

   * `audioCodec` é `aac`.
   * `customArgs` é `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar a configuração, crie uma sobreposição no nó `/apps/settings/` e mova a mesma estrutura no nó `/conf/global/settings/`. Ele não pode ser editado no nó `/libs`. Por exemplo, para sobrepor o caminho `/libs/settings/dam/video/fullhd-bp`, crie-o em `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sobreponha e edite o nó de perfil inteiro e não apenas a propriedade que precisa de modificação. Esses recursos não são resolvidos por meio do SlingResourceMerger.

4. Se você alterou qualquer uma das propriedades, clique em **[!UICONTROL Salvar tudo]**.

>[!NOTE]
>
>As alterações nos modelos de fluxo de trabalho predefinidos não são preservadas ao atualizar a instância do AEM. A Adobe recomenda copiar os modelos de fluxo de trabalho modificados antes de editá-los. Por exemplo, copie o modelo pronto para uso [!UICONTROL Ativo de atualização do DAM] antes de editar a etapa de Transcodificação do FFmpeg no modelo [!UICONTROL Ativo de atualização do DAM] para escolher nomes de perfil de vídeo existentes antes da atualização. Em seguida, é possível sobrepor o nó `/apps` para permitir que o AEM recupere as alterações personalizadas no modelo pronto para uso.
