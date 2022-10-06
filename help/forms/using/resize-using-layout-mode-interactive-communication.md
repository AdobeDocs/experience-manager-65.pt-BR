---
title: Usar o modo Layout para redimensionar componentes para Comunicação interativa
description: Definir a posição dos componentes usando a grade responsiva disponível no modo Layout
feature: Interactive Communication
exl-id: 9534fcb2-4260-4dd0-9f7e-779b10fd3a22
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 1%

---

# Usar o modo Layout para redimensionar componentes {#use-layout-mode-to-resize-components}

A interface de criação do canal Web de Comunicação interativa permite redimensionar componentes usando o modo Layout . Arraste e solte pontos azuis nas colunas para definir os pontos inicial e final para posicionar os componentes. Os pontos azuis são exibidos após tocar no componente dentro da grade responsiva. A grade responsiva consiste em 12 colunas iguais. O sombreamento de cores branco e azul em colunas alternativas diferencia uma coluna da outra.

Você pode usar o modo Layout para redimensionar componentes para todos os tipos de dispositivos, como desktop, tablet, telefone e outros dispositivos menores. O tablet deriva automaticamente a configuração de layout da versão de desktop e os dispositivos menores derivam a configuração de layout do telefone. No entanto, é possível substituir as configurações derivadas automaticamente para definir uma configuração diferente para cada tipo de dispositivo.

>[!NOTE]
>
>Se você estiver criando o canal Web usando [Imprimir canal como principal](../../forms/using/create-interactive-communication.md) para uma Comunicação interativa, os componentes disponíveis para redimensionamento também incluem os subformulários e campos gerados automaticamente no canal da Web usando o canal Imprimir. O canal da Web retém o layout dos elementos do canal de impressão no modo Layout.

## Modo de layout de acesso {#access-layout-mode}

Selecionar **Layout** na lista suspensa que aparece na parte superior da interface de criação do Interative Communication próxima ao **Visualizar** opção. O formulário é exibido no modo Layout .

1. Faça logon na instância do autor do AEM e navegue até **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Crie um novo ou abra um [Comunicação interativa](../../forms/using/create-interactive-communication.md).
1. Selecionar **Layout** na lista suspensa que aparece na parte superior ao lado do **Visualizar** opção. O formulário é exibido no modo Layout .

   ![Modo de layout para Comunicações interativas](assets/layout_mode_ic_new.png)

## Redimensionar componentes {#resize-components}

1. No modo Layout , toque no componente para redimensionar. Os pontos azuis são exibidos no início e no fim da grade responsiva.
1. Arraste e solte os pontos azuis para definir a posição do componente na grade responsiva.

   ![Redimensionamento usando o modo Layout](assets/layout_mode_resize_new_updated.png)

   A barra de ferramentas que é exibida após tocar nos componentes consiste nas seguintes opções:

   * **Pai:** Selecione o pai de um componente.
   * **Flutuar para a nova linha:** Deslocar o componente para a linha seguinte se houver vários componentes na mesma linha.

   Você pode desfazer todas as alterações de redimensionamento e aplicar o layout padrão ao painel que contém componentes redimensionados usando o **[!UICONTROL Reverter layout do ponto de interrupção]** ( ![Reverter ponto de interrupção](assets/reverttopreviouslypublishedversion.png)). Toque no pai do componente redimensionado para exibir a opção.

   >[!NOTE]
   >
   >Não é possível redimensionar a coluna da tabela, a barra de ferramentas, o botão da barra de ferramentas e os componentes da área de destino usando o modo Layout . Use o modo Estilo para redimensionar esses componentes.

### Exemplo {#example}

**Objetivo:** Você deseja inserir um componente de tabela e um componente de Imagem e posicioná-los em paralelo um ao outro em uma Comunicação interativa.

1. Insira os componentes de tabela e imagem usando o modo Editar no canal da Web de uma Comunicação interativa. O componente de imagem é exibido depois do componente de tabela.
1. Alterne para o modo Layout e toque no componente Tabela . Os pontos azuis para redimensionar a exibição do componente nas colunas 1 e 12.
1. Arraste e solte o ponto azul na coluna 12 para a coluna 6 da grade responsiva.

   ![Definir o ponto final da tabela](assets/layout_mode_end_point_table_new.png)

1. Da mesma forma, selecione o componente Imagem e arraste e solte o ponto azul na coluna 1 até a coluna 7 da grade responsiva. Os componentes de tabela e imagem são exibidos em paralelo.

   ![Tabela e imagem em paralelo no modo Layout](assets/table_image_parallel_new.png)

   Você pode selecionar o componente Imagem e tocar no componente **Flutuar para a nova linha** opção disponível na barra de ferramentas para deslocar o componente de Imagem para a próxima linha.

## Redimensionar painéis {#resize-panels-layout-mode}

Execute as seguintes etapas se quiser redimensionar todo o painel em vez de componentes individuais:

1. Toque em qualquer um dos componentes no painel que você deseja redimensionar, selecione ![Selecionar Pai](assets/select_parent_icon.svg)e selecione a primeira opção na lista suspensa, se o painel for o pai imediato do componente.

   Os pontos azuis são exibidos no início e no fim da grade responsiva.

1. Arraste e solte os pontos azuis para definir a posição do painel na grade responsiva.
Você pode repetir as etapas 1 e 2 e selecionar ![Selecionar Pai](assets/float_to_new_line_icon.svg) para transferir o painel redimensionado para a linha seguinte.

## Definir o layout de várias colunas para um painel

Execute as seguintes etapas para definir o número de colunas para um painel:

1. Em **[!UICONTROL Editar]** , toque no painel , selecione ![Configurar](assets/configure_icon.png)e selecione **[!UICONTROL Responsivo - tudo na página sem navegação]** da **[!UICONTROL Layout do painel]** lista suspensa.

1. Toque ![Salvar](assets/save_icon.svg) para salvar as propriedades.

1. No **[!UICONTROL Layout]** , toque em qualquer um dos componentes no painel , selecione ![Selecionar Pai](assets/select_parent_icon.svg)e selecione o painel .

1. Toque ![várias colunas](assets/multi-column.svg) e selecione o número de colunas na lista suspensa. O número de colunas pode variar de 1 a 12. O painel é dividido em um layout de várias colunas.

![várias colunas no modo de layout](assets/multi-column-layout.png)

## Desativar o modo Layout para formulários com layout responsivo antigo {#disable-layout-mode-for-forms-with-old-responsive-layout}

Você pode desativar o modo Layout para formulários com layout responsivo antigo editando as propriedades do modelo usado no formulário.

Execute as seguintes etapas para desativar o modo Layout :

1. Selecionar **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]** e abra o modelo usado no formulário em **[!UICONTROL Editar]** modo.
1. Selecione o Contêiner de documento no painel esquerdo e toque em **[!UICONTROL Política.]**

   ![Desativar modo Layout](assets/policy_disable_layout_mode.png)

1. Toque no **[!UICONTROL Configurações de layout]** e selecione **[!UICONTROL Desativar modo de layout]**.
1. Toque ![Salvar alterações](assets/save_icon.png) para salvar as propriedades do template.
