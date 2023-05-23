---
title: FFmpeg para comunidades
seo-title: FFmpeg for Communities
description: Como instalar e configurar o FFmpeg para Comunidades
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# FFmpeg para comunidades {#ffmpeg-for-communities}

## Visão geral {#overview}

O FFmpeg é uma solução para conversão e transmissão de áudio e vídeo e, quando instalado, é usado para transcodificação adequada de [ativos de vídeo](../../help/sites-authoring/default-components-foundation.md#video).

## Instalando O FFmpeg {#installing-ffmpeg}

O FFmpeg deve ser instalado nos servidores que hospedam o AEM *autor* instância(s).

1. Ir para [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Baixe a versão mais recente do FFmpeg para seu ambiente específico (Macintosh, Windows ou Linux).

   * É importante manter o FFmpeg atualizado devido a vulnerabilidades de segurança em versões mais antigas.

1. Instale o FFmpeg seguindo as instruções para o SO.

1. Verifique se o executável FFmpeg está definido no caminho do sistema.

   Você deve ser capaz de executar FFmpeg de qualquer diretório em seu sistema.

   * Por exemplo, `ffmpeg -version`.

## Configurar Serviço de Transcodificação FFmpeg {#configure-ffmpeg-transcoding-service}

Por padrão, quando o FFmpeg é instalado, várias representações são configuradas (transcodificações) de acordo com [!UICONTROL Ativo de atualização DAM] definição de fluxo de trabalho.

Como as transcodificações consomem muita CPU, é recomendável modificar a lista de representações de destino. Na maioria dos casos, a transcodificação não é necessária.

Para modificar a variável [!UICONTROL Ativo de atualização DAM] e, neste exemplo, desativar a transcodificação:

* Faça logon na instância do autor com privilégios administrativos.
* Na navegação global, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
* Localizar **[!UICONTROL Ativo de atualização DAM]**.
* Clique duas vezes para abrir o fluxo de trabalho para edição na interface clássica.

   Local resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Clique duas vezes no ícone **[!UICONTROL Transcodificação FFmpeg]** etapa para acessar a caixa de diálogo Propriedades da etapa.
* No **[!UICONTROL Processo]** guia:

   * **[!UICONTROL Argumentos]**: limpe todas as entradas para desativar a transcodificação. Valores padrão: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Selecionar **[!UICONTROL OK]** para fechar o `Step Properties` diálogo.

* Selecionar **[!UICONTROL Salvar]** para salvar o `DAM Update Asset` fluxo de trabalho.
