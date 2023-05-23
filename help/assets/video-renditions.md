---
title: Representações de vídeo
description: Representações de vídeo
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Representações de vídeo {#video-renditions}

O Adobe Experience Manager Assets gera representações de vídeo para ativos de vídeo de vários formatos, incluindo OGG, FLV e assim por diante.

O Experience Manager Assets é compatível com representações estáticas e dinâmicas (representações codificadas no DM) para ativos de mídia.

As representações estáticas são geradas nativamente usando FFMPEG (instalado e disponível no caminho do sistema) e armazenadas no repositório de conteúdo.

As representações codificadas por DM são armazenadas no servidor proxy e veiculadas no tempo de execução.

A Experience Manager Assets fornece suporte à reprodução para essas representações no lado do cliente.

Para exibir as representações de um ativo de vídeo específico, abra a página de ativos e selecione o ícone Navegação global. Em seguida, escolha **[!UICONTROL Representações]** da lista.

![chlimage_1-478](assets/chlimage_1-478.png)

A lista de representações de vídeo é exibida na **[!UICONTROL Representações]** painel.

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar o servidor proxy para representações codificadas por DM, [configurar os serviços do Dynamic Media Cloud](config-dynamic.md).

Para gerar representações de vídeo com os parâmetros desejados, [criar um perfil de vídeo correspondente](video-profiles.md).

Depois de configurar o servidor proxy e criar perfis de vídeo, você pode incluir essa predefinição de vídeo em um perfil de processamento e aplicar o perfil de processamento a uma pasta.

>[!NOTE]
>
>A reprodução de áudio não funciona para arquivos OGG e WAV no Microsoft® Internet Explorer 11. Um erro `Invalid Source` é exibido na página de detalhes do ativo para ativos com extensão OGG ou WAV.
>
>No MS® Edge e no iPad, os arquivos OGG não são reproduzidos e geram um erro de formato não suportado.
