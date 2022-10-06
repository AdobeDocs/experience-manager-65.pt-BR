---
title: Configurar o componente de Vídeo
seo-title: Configure the Video component
description: Saiba como configurar o Componente de vídeo.
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 9c97f99e-d6ef-4817-8b2a-201ab22f2b38
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Configurar o componente de Vídeo {#configure-the-video-component}

O [Componente de vídeo](/help/sites-authoring/default-components-foundation.md#video) permite colocar um ativo de vídeo predefinido e pronto para uso (OOTB) na sua página.

Para que ocorra a transcodificação adequada, um administrador instala o FFmpeg separadamente. Consulte [Instale o FFmpeg e configure o AEM](#install-ffmpeg). Administradores também [Configurar perfis de vídeo](#configure-video-profiles) para uso com elementos HTML5.

>[!CAUTION]
>
>Este componente fundamental foi descontinuado. A Adobe recomenda o aproveitamento da variável [Componente incorporado dos componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/embed.html) em vez disso.

>[!CAUTION]
>
>Não é mais esperado que esse componente funcione imediatamente sem uma personalização abrangente no nível do projeto.

## Configurar perfis de vídeo {#configure-video-profiles}

Para usar os elementos de HTML5, defina os perfis de vídeo. Os escolhidos aqui são usados em ordem. Para acessar, use [Modo Design](/help/sites-authoring/default-components-designmode.md) (Somente interface clássica) e selecione o **[!UICONTROL Perfis]** guia :

![chlimage_1-317](assets/chlimage_1-317.png)

Nessa caixa de diálogo, você também pode configurar o design do componente Vídeo e os parâmetros para [!UICONTROL Reprodução], [!UICONTROL Flash]e [!UICONTROL Avançado].

## Instale o FFmpeg e configure o AEM {#install-ffmpeg}

O componente Vídeo depende do produto FFmpeg de código aberto de terceiros para transcodificação de vídeos. Baixado de [https://ffmpeg.org/](https://ffmpeg.org/). Depois de instalar o FFmpeg, configure o AEM para usar um codec de áudio específico e opções específicas de tempo de execução.

Para instalar o FFmpeg em **Windows** siga estas etapas:

1. Baixe o binário compilado como `ffmpeg.zip`.
1. Desarquivar em uma pasta.
1. Definir a variável de ambiente do sistema `PATH` para &lt;*sua-localização-ffmpeg*>`\bin`.
1. Reinicie o AEM.

Para instalar o FFmpeg em **Mac OS X** siga estas etapas:

1. Instale o Xcode disponível em [developer.apple.com/xcode](https://developer.apple.com/xcode/).
1. Instalar disponível em [XQuartz](https://www.xquartz.org) para obter [X11](https://support.apple.com/en-us/HT201341).
1. Instale o MacPorts disponível em [www.macports.org](https://www.macports.org/).
1. No console, execute `sudo port install ffmpeg` e siga as instruções na tela. Certifique-se de que o caminho da variável `FFmpeg` o executável é adicionado ao `PATH` variável do sistema.

Para instalar o FFmpeg em **Mac OS X 10.6**, usando a versão pré-compilada, siga estas etapas:

1. Baixe a versão pré-compilada.
1. Desarquive-o no `/usr/local` diretório.
1. No console, execute `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`. Altere os caminhos conforme apropriado.

Para **configurar AEM** siga estas etapas:

>[!NOTE]
>
>Essas etapas só são necessárias se for necessária uma personalização adicional dos codecs.

1. Abrir [!UICONTROL CRXDE Lite] no navegador da Web. Acesso [http://localhost:4502/crx/de](http://localhost:4502/crx/de).
2. Selecione o `/libs/settings/dam/video/format_aac/jcr:content` e garanta que as propriedades do nó sejam as seguintes:

   * `audioCodec` é `aac`.
   * `customArgs` é `-flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8`.

3. Para personalizar a configuração, crie uma sobreposição em `/apps/settings/` nó e mova a mesma estrutura em `/conf/global/settings/` nó . Não pode ser editado em `/libs` nó . Por exemplo, para sobrepor o caminho `/libs/settings/dam/video/fullhd-bp`, crie-o em `/conf/global/settings/dam/video/fullhd-bp`.

   >[!NOTE]
   >
   >Sobreponha e edite todo o nó do perfil e não apenas a propriedade que precisa de modificação. Esses recursos não são resolvidos através do SlingResourceMerger.

4. Se tiver alterado qualquer uma das propriedades, clique em **[!UICONTROL Salvar tudo]**.

>[!NOTE]
>
>As alterações nos modelos de fluxo de trabalho padrão prontos para uso (OOTB) não são preservadas quando você atualiza sua instância do AEM. O Adobe recomenda copiar os modelos de fluxo de trabalho modificados antes de editá-los. Por exemplo, copie o OOTB [!UICONTROL Ativo de atualização DAM] modelo antes de editar a etapa Transcodificação FFmpeg no [!UICONTROL Ativo de atualização DAM] modelo para escolher nomes de perfil de vídeo existentes antes da atualização. Em seguida, é possível sobrepor o `/apps` nó para permitir AEM recuperar as alterações personalizadas no modelo OOTB.
