---
title: FFmpeg para comunidades
description: Como instalar e configurar o FFmpeg para Comunidades
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 1%
---
# FFmpeg para comunidades {#ffmpeg-for-communities}

## Visão geral {#overview}

O FFmpeg é uma solução para conversão e transmissão de áudio e vídeo e, quando instalado, é usado para a transcodificação adequada de [ativos de vídeo](../../help/sites-authoring/default-components-foundation.md#video).

## Instalando O FFmpeg {#installing-ffmpeg}

O FFmpeg deve ser instalado no(s) servidor(es) que hospeda(m) a(s) instância(s) *author* do AEM.

1. Ir para [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Baixe a versão mais recente do FFmpeg para seu ambiente específico (Macintosh, Windows ou Linux).

   * É importante manter o FFmpeg atualizado devido a vulnerabilidades de segurança em versões mais antigas.

1. Instale o FFmpeg seguindo as instruções para o SO.

1. Verifique se o executável FFmpeg está definido no caminho do sistema.

   Você deve ser capaz de executar FFmpeg de qualquer diretório em seu sistema.

   * Por exemplo, `ffmpeg -version`.

## Configurar Serviço de Transcodificação FFmpeg {#configure-ffmpeg-transcoding-service}

Por padrão, quando o FFmpeg é instalado, várias representações são configuradas (transcodificações) de acordo com a definição de fluxo de trabalho [!UICONTROL Ativo de atualização do DAM].

Como as transcodificações exigem muito do CPU, é recomendável modificar a lista de representações do público-alvo. Na maioria dos casos, a transcodificação não é necessária.

Para modificar o fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] e, neste exemplo, desativar a transcodificação:

* Faça logon na instância do autor com privilégios administrativos.
* Na navegação global, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
* Localize o **[!UICONTROL Ativo de atualização do DAM]**.
* Clique duas vezes para abrir o fluxo de trabalho para edição na interface clássica.

  Local resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Clique duas vezes na etapa **[!UICONTROL Transcodificação de FFmpeg]** para acessar a caixa de diálogo Propriedades da etapa.
* Na guia **[!UICONTROL Processo]**:

  * **[!UICONTROL Argumentos]**: Limpar todas as entradas para desabilitar a transcodificação Valores padrão: `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* Selecione **[!UICONTROL OK]** para fechar a caixa de diálogo `Step Properties`.

* Selecione **[!UICONTROL Salvar]** para salvar o fluxo de trabalho `DAM Update Asset`.
