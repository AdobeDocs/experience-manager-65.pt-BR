---
title: Execuções de vídeo
description: Execuções de vídeo
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
translation-type: tm+mt
source-git-commit: 66f46a34832254af74c72da16ec8ebe3eb8cd46d
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Execuções de vídeo {#video-renditions}

O Adobe Experience Manager (AEM) Assets gera renderizações de vídeo para ativos de vídeo de vários formatos, incluindo OGG, FLV e assim por diante.

A AEM Assets oferece suporte a representações estáticas e dinâmicas (execuções codificadas por DM) para ativos de mídia.

As execuções estáticas são geradas nativamente usando FFMPEG (instalado e disponível no caminho do sistema) e armazenadas no repositório de conteúdo.

As renderizações codificadas por DM são armazenadas no servidor proxy e servidas no tempo de execução.

Os ativos AEM fornecem suporte de reprodução para essas execuções no lado do cliente.

Para visualização das representações de um ativo de vídeo específico, abra sua página de ativo e toque no ícone Navegação global. Em seguida, escolha **[!UICONTROL Representações]** na lista.

![chlimage_1-478](assets/chlimage_1-478.png)

A lista de representações de vídeo é exibida no painel **[!UICONTROL Representações]**.

![chlimage_1-479](assets/chlimage_1-479.png)

Para configurar o servidor proxy para renderizações codificadas por DM, [configure os serviços da Dynamic Media Cloud.](config-dynamic.md)

Para gerar representações de vídeo com os parâmetros desejados, [crie um perfil de vídeo correspondente](video-profiles.md).

Depois de configurar o servidor proxy e criar perfis de vídeo, é possível incluir essa predefinição de vídeo em um perfil de processamento e aplicar o perfil de processamento a uma pasta.

>[!NOTE]
>
>A reprodução de áudio não funciona para arquivos OGG e WAV no Microsoft Internet Explorer 11. Um erro `Invalid Source` é exibido na página de detalhes do ativo para ativos com extensão OGG ou WAV.
>
>No MS Edge e iPad, os arquivos OGG não são reproduzidos e geram um erro de formato não suportado.
