---
title: Usar o modo Layout para redimensionar componentes para o Interative Communication
description: 'Definir a posição dos componentes usando a grade responsiva disponível no modo Layout '
translation-type: tm+mt
source-git-commit: c62ad355469a95db89db44c34bb6df72d8f4bf77
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---


# Usar o modo Layout para redimensionar componentes {#use-layout-mode-to-resize-components}

A interface de criação do canal da Web Interative Communication permite redimensionar componentes usando o modo Layout. Arraste e solte pontos azuis dentro de colunas para definir o start e os pontos finais para posicionar os componentes. Os pontos azuis são exibidos após tocar no componente dentro da grade responsiva. A grade responsiva consiste em 12 colunas iguais. O sombreamento de cores branco e azul em colunas alternativas diferencia uma coluna da outra.

Você pode usar o modo Layout para redimensionar componentes para todos os tipos de dispositivos, como desktop, tablet, telefone e outros dispositivos menores. O tablet deriva automaticamente a configuração do layout da versão do desktop e os dispositivos menores derivam a configuração do layout do telefone. Entretanto, é possível substituir as configurações derivadas automaticamente para definir uma configuração diferente para cada tipo de dispositivo.

>[!NOTE]
>
>Se você estiver criando o canal da Web usando o canal [Imprimir como principal](../../forms/using/create-interactive-communication.md) para uma Comunicação interativa, os componentes disponíveis para redimensionamento também incluirão os subformulários e campos gerados automaticamente no canal da Web usando o canal Imprimir. O canal da Web retém o layout dos elementos do canal Imprimir no modo Layout.

## Modo de layout de acesso {#access-layout-mode}

Selecione **Layout** na lista suspensa que aparece na parte superior da interface de criação do Interative Communication ao lado da opção **Pré-visualização** . O formulário é exibido no modo Layout.

1. Faça logon na instância do autor AEM e navegue até **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
1. Crie uma nova comunicação ou abra uma comunicação [](../../forms/using/create-interactive-communication.md)interativa existente.
1. Selecione **Layout** na lista suspensa que aparece na parte superior ao lado da opção **Pré-visualização** . O formulário é exibido no modo Layout.

   ![Modo de layout para Interative Communications](assets/layout_mode_ic_new.png)

## Redimensionar componentes {#resize-components}

1. No modo Layout, toque no componente para redimensioná-lo. Os pontos azuis são exibidos no start e no final da grade responsiva.
1. Arraste e solte os pontos azuis para definir a posição do componente na grade responsiva.

   ![Redimensionamento usando o modo Layout](assets/layout_mode_resize_new_updated.png)

   A barra de ferramentas que é exibida após tocar nos componentes consiste nas seguintes opções:

   * **Pai:** Selecione o pai de um componente.
   * **Flutuar para nova linha:** Alterne o componente para a linha seguinte se houver vários componentes dentro da mesma linha.

   Você pode desfazer todas as alterações de redimensionamento e aplicar o layout padrão ao painel que contém componentes redimensionados usando a opção **[!UICONTROL Reverter layout]** do ponto de interrupção ( ![Reverter ponto de interrupção](assets/reverttopreviouslypublishedversion.png)). Toque no pai do componente redimensionado para visualização a opção.

   >[!NOTE]
   >
   >Não é possível redimensionar a coluna da tabela, a barra de ferramentas, o botão da barra de ferramentas e os componentes da área do público alvo usando o modo Layout. Use o modo Estilo para redimensionar esses componentes.

### Exemplo {#example}

**Objetivo:** Você deseja inserir um componente de tabela e um componente de Imagem e posicioná-los paralelamente entre si em uma Comunicação interativa.

1. Insira os componentes de tabela e imagem usando o modo Editar no canal Web de uma Comunicação Interativa. O componente de imagem é exibido após o componente de tabela.
1. Alterne para o modo Layout e toque no componente Tabela. Os pontos azuis para redimensionar o componente são exibidos nas colunas 1 e 12.
1. Arraste e solte o ponto azul na coluna 12 para a coluna 6 da grade responsiva.

   ![Definir o ponto final da tabela](assets/layout_mode_end_point_table_new.png)

1. Da mesma forma, selecione o componente de Imagem e arraste e solte o ponto azul na coluna 1 para a coluna 7 da grade responsiva. Os componentes de tabela e imagem são exibidos em paralelo.

   ![Tabela e imagem em paralelo no modo Layout](assets/table_image_parallel_new.png)

   Você pode selecionar o componente de Imagem e tocar na opção **Flutuar para uma nova linha** disponível na barra de ferramentas para deslocar o componente de Imagem para a próxima linha.

## Redimensionar painéis {#resize-panels-layout-mode}

Execute as seguintes etapas se quiser redimensionar o painel inteiro em vez de componentes individuais:

1. Toque em qualquer um dos componentes no painel que você deseja redimensionar, selecione ![Selecionar pai](assets/select_parent_icon.svg)e selecione a primeira opção na lista suspensa, se o painel for o pai imediato do componente.

   Os pontos azuis são exibidos no start e no final da grade responsiva.

1. Arraste e solte os pontos azuis para definir a posição do painel na grade responsiva.
Você pode repetir as etapas 1 e 2 e selecionar ![Selecionar pai](assets/float_to_new_line_icon.svg) para deslocar o painel redimensionado para a linha seguinte.

## Definir o layout de várias colunas para um painel

Execute as seguintes etapas para definir o número de colunas de um painel:

1. No modo **[!UICONTROL Editar]** , toque no painel, selecione ![Configurar](assets/configure_icon.png)e selecione **[!UICONTROL Responsivo - tudo na página sem a opção de navegação]** na lista suspensa Layout **[!UICONTROL do]** painel.

1. Toque em ![Salvar](assets/save_icon.svg) para salvar as propriedades.

1. No modo **[!UICONTROL Layout]** , toque em qualquer um dos componentes no painel, selecione ![Selecionar pai](assets/select_parent_icon.svg)e selecione o painel.

1. Toque em ![várias colunas](assets/multi-column.svg) e selecione o número de colunas na lista suspensa. O número de colunas pode variar de 1 a 12. O painel é dividido em um layout de várias colunas.

![várias colunas no modo de layout](assets/multi-column-layout.png)

## Desativar o modo Layout para formulários com layout responsivo antigo {#disable-layout-mode-for-forms-with-old-responsive-layout}

É possível desativar o modo Layout para formulários com layout responsivo antigo editando as propriedades para o modelo usado no formulário.

Execute as seguintes etapas para desativar o modo Layout:

1. Selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]** e abra o modelo usado no formulário no modo **[!UICONTROL Editar]** .
1. Selecione o Container do Documento no painel esquerdo e toque em **[!UICONTROL Política.]**

   ![Desativar modo Layout](assets/policy_disable_layout_mode.png)

1. Toque na guia Configurações **[!UICONTROL de]** layout e selecione **[!UICONTROL Desativar modo]** de layout.
1. Toque em ![Salvar alterações](assets/save_icon.png) para salvar as propriedades do modelo.

