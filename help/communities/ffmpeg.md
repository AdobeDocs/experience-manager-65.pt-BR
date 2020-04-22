---
title: FFmpeg para Comunidades
seo-title: FFmpeg para Comunidades
description: Como instalar e configurar o FFmpeg para Comunidades
seo-description: Como instalar e configurar o FFmpeg para Comunidades
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: bb523ecf97ea18d8e8d5afa238fdf9e95fa58ab4

---


# FFmpeg para Comunidades {#ffmpeg-for-communities}

## Visão geral {#overview}

FFmpeg é uma solução para conversão e streaming de áudio e vídeo e, quando instalada, é usada para transcodificação adequada de ativos [de](../../help/sites-authoring/default-components-foundation.md#video) vídeo, bem como para o recurso de ativação do AEM Communities.

FFmpeg é usado no ambiente do autor para obter metadados para recursos de ativação carregados, bem como para gerar uma miniatura para exibição ao listar o recurso de ativação.

## Instalar FFmpeg {#installing-ffmpeg}

FFmpeg deve ser instalado nos servidores que hospedam as instâncias de *autor* do AEM.

1. Vá para [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. Baixe a versão mais recente do FFmpeg para seu ambiente específico (Macintosh, Windows ou Linux).

   * É importante manter o FFmpeg atualizado devido a vulnerabilidades de segurança em versões mais antigas.

1. Instale o FFmpeg seguindo as instruções para o SO.

1. Verifique se o executável FFmpeg está definido no caminho do sistema.

   Você deve ser capaz de executar FFmpeg a partir de qualquer diretório no seu sistema.

   * Por exemplo, `ffmpeg -version`.

## Configurar o serviço de transcodificação FFmpeg {#configure-ffmpeg-transcoding-service}

Por padrão, quando FFmpeg é instalado, várias renderizações são configuradas (transcodificações) de acordo com a definição do fluxo de trabalho do Ativo  de atualização do DAM.

Como as transcodificações exigem muito da CPU, é recomendável modificar a lista das execuções do público alvo. Na maioria dos casos, a transcodificação não é necessária.

Para modificar o fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM e, neste exemplo, desativar a transcodificação:

* Entre na instância do autor com privilégios administrativos.
* Na navegação global, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
* Localize o ativo **[!UICONTROL de atualização do]** DAM.
* Clique com o Duplo para abrir o fluxo de trabalho para edição na interface clássica.

   Local resultante: [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* Clique com o Duplo na etapa de transcodificação **[!UICONTROL do]** FFmpeg para acessar a caixa de diálogo Propriedades da etapa.
* Na guia **[!UICONTROL Processo]** :

   * **[!UICONTROL Argumentos]**: Apagar todas as entradas para desativar a transcodificação Valores padrão: `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* Selecione **[!UICONTROL OK]** para fechar a `Step Properties` caixa de diálogo.

* Selecione **[!UICONTROL Salvar]** para salvar o `DAM Update Asset` fluxo de trabalho.



