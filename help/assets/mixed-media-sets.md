---
title: Conjuntos de mídia mista
description: Saiba como trabalhar com conjuntos de mídia mista no Dynamic Media
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Misturar conjuntos de mídia,Gerenciamento de ativos
role: Profissional de negócios, Administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 28%

---


# Conjuntos de mídia mista{#mixed-media-sets}

Os Conjuntos de mídias mistas permitem que você forneça uma combinação de imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos em uma apresentação.

Os Conjuntos de mídias mistas são designados por um banner com a palavra **[!UICONTROL MixedMediaSet.]** Além disso, se o Conjunto de mídias mistas for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]**, estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obter informações sobre a interface do usuário do Assets, consulte [Gerenciar ativos](/help/assets/manage-assets.md).

## Início rápido: Conjuntos de mídias mistas {#quick-start-mixed-media-sets}

Para ativar e executar rapidamente com Conjuntos de mídias mistas, siga estas etapas:

1. [Faça upload dos ativos](#uploading-assets).

   Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Se necessário, crie seus [Conjuntos de imagens](/help/assets/image-sets.md) e [Conjuntos de rotação](/help/assets/spin-sets.md). Como os usuários podem ampliar imagens no Visualizador de conjunto de mídias mistas, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

1. [Criar conjuntos de mídia mista.](#creating-mixed-media-sets)

   Para criar um Conjunto de mídia mista, na página Assets, toque em **[!UICONTROL Criar > Conjunto de mídias mistas]** e nomeie o conjunto, selecione os ativos e escolha a ordem em que as imagens serão exibidas.

   Consulte [Trabalhar com seletores.](/help/assets/working-with-selectors.md)

1. Configure [Mixed Media Viewer presets](/help/assets/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de mídia mista. Para ver sua mídia mista com uma predefinição do visualizador, selecione o conjunto de mídias mistas e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores.]**

   Consulte **[!UICONTROL Ferramentas > Ativos > Predefinições do visualizador]** para criar ou editar predefinições do visualizador.

   Consulte [Adicionar e editar predefinições do visualizador.](/help/assets/managing-viewer-presets.md)

1. [Visualizar conjuntos de mídia mista.](#previewing-mixed-media-sets)

   Selecione o Conjunto de mídias mistas e você pode visualizá-lo. Clique nos ícones de miniatura para examinar seu Conjunto de mídias mistas no Visualizador selecionado. Você pode escolher visualizadores diferentes do menu **[!UICONTROL Visualizadores]**, disponível no menu suspenso do painel à esquerda.

1. [Publicar Conjuntos de Mídias Mistas.](#publishing-mixed-media-sets)

   A publicação de um Conjunto de mídias mistas ativa o URL e a cadeia de caracteres de inserção. Além disso, você deve [publicar a predefinição do visualizador](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Vincule URLs ao seu ](/help/assets/linking-urls-to-yourwebapplication.md) aplicativo web ou  [Incorpore o visualizador](/help/assets/embed-code.md) de vídeo ou imagem.

   O AEM Assets cria chamadas de URL para Conjuntos de mídia mista e as ativa após publicar os conjuntos de mídia mista. Você pode copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de mídias mistas e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores.]**

   Consulte [Vincular um conjunto de mídias mistas a uma página da Web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/embed-code.md).

Se precisar, edite [Conjuntos de mídias mistas](#editing-mixed-media-sets). Além disso, você pode exibir e modificar [as propriedades do Conjunto de mídias mistas](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>Se tiver problemas ao criar conjuntos, consulte [Resolução de problemas do Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).

## Carregar ativos {#uploading-assets}

Comece carregando as imagens e os vídeos dos Conjuntos de mídias mistas. Como os usuários podem ampliar imagens no Visualizador de conjunto de mídias mistas, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

Além disso, se você quiser adicionar conjuntos de rotação ou conjuntos de imagens ao conjunto de mídia mista, crie-os também.

## Criação de conjuntos de mídia mista {#creating-mixed-media-sets}

Você pode adicionar imagens, conjuntos de imagens, conjuntos de rotação e vídeos ao seu conjunto de mídias mistas. Verifique se os arquivos, os conjuntos de imagens e os conjuntos de rotação estão prontos para publicação antes de adicioná-los ao Conjunto de mídias mistas.

Ao adicionar ativos ao seu conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reordenar ou classificar ativos manualmente após a adição.

**Para criar um Conjunto de mídias mistas**

1. No Assets, navegue até o local em que deseja criar um conjunto de mídia mista, clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Conjunto de mídia mista.]** Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos. O Editor do conjunto de mídias mistas é exibido.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. No Editor do conjunto de mídias mistas, em **[!UICONTROL Title]**, digite um nome para o conjunto de mídias mistas. O nome aparece no banner através do Conjunto de mídias mistas. Opcionalmente, informe uma descrição.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de mídias mistas, você pode alterar a miniatura do conjunto de mídias mistas ou permitir que AEM selecione a miniatura automaticamente com base nos ativos no conjunto de mídias mistas. Para selecionar uma miniatura, clique em **[!UICONTROL Change thumbnail]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se tiver selecionado uma miniatura e decidir que deseja AEM gerar uma a partir do conjunto de mídias mistas, selecione **[!UICONTROL Alternar para Miniatura Automática.]**

1. Toque no Seletor de ativos para selecionar os ativos que deseja incluir no seu Conjunto de mídias mistas. Selecione-os e clique em **[!UICONTROL Selecionar.]**

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar em **[!UICONTROL Retornar.]** Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]**, na barra de ferramentas. Altere a exibição ao clicar no ícone **[!UICONTROL Exibição]** e selecionar **[!UICONTROL Exibição em lista]**, **[!UICONTROL Exibição em coluna]** ou **[!UICONTROL Exibição de cartão.]**

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Reorganize os ativos arrastando-os para cima ou para baixo na lista (deve selecionar o ícone **[!UICONTROL Reorder]**), conforme necessário.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Se quiser adicionar miniaturas, clique no ícone de **miniatura** **[!UICONTROL +]** ao lado da imagem e navegue até a miniatura desejada. Quando terminar de selecionar todas as imagens em miniatura, clique em **[!UICONTROL Salvar.]**

   >[!NOTE]
   >
   >Se desejar adicionar ativos, toque em **[!UICONTROL Adicionar ativo.]**

1. Para excluir um ativo, marque a caixa de seleção correspondente e toque em **[!UICONTROL Excluir ativo.]**
1. Para aplicar uma predefinição, toque em **[!UICONTROL Predefinição]** no canto superior direito e selecione uma predefinição para aplicar aos ativos.
1. Clique em **[!UICONTROL Salvar.]** O Conjunto de mídias mistas recém-criado é exibido na pasta em que você o criou.

## Editar conjuntos de mídia mista {#editing-mixed-media-sets}

Você pode executar uma variedade de tarefas de edição em ativos em Conjuntos de mídias mistas diretamente na interface do usuário [da mesma forma que faria com qualquer ativo em Ativos](/help/assets/manage-assets.md). Você também pode executar as seguintes ações em Conjuntos de mídias mistas:

* Adicione ativos ao Conjunto de mídias mistas.
* Reorganize os ativos no Conjunto de mídias mistas.
* Exclua ativos no Conjunto de mídias mistas.
* Aplicar predefinições do visualizador.
* Altere a miniatura padrão.

**Para editar um conjunto de mídia mista**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo Conjunto de mídias mistas e toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo de Conjunto de mídias mistas, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e toque em **[!UICONTROL Editar]** na barra de ferramentas.

   * Toque em um ativo Conjunto de mídias mistas e toque em **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. No Editor do conjunto de mídias mistas, siga um destes procedimentos:

   * Para reorganizar ativos - No painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem), arraste um ativo para um novo local.
   * Para adicionar ativos - Na barra de ferramentas, toque em **[!UICONTROL Adicionar ativo.]** Navegue até os ativos. Para cada ativo que deseja adicionar, passe o mouse sobre a imagem do ativo (não o nome do ativo) e toque no ícone de marca de seleção. No canto superior direito, toque em **[!UICONTROL Selecionar.]**

   * Para excluir um ativo - No painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem) e selecione o ativo. Na barra de ferramentas, toque em **[!UICONTROL Excluir ativo.]**

   * Para classificar ativos pelo nome em ordem crescente ou decrescente, no painel à esquerda, toque em **[!UICONTROL Assets]** (ícone de imagem). À direita do cabeçalho **[!UICONTROL Assets]**, toque nos ícones de cursor para cima ou para baixo.

      >[!NOTE]
      >
      >* Para excluir um Conjunto de mídias mistas inteiro, a partir de qualquer modo de exibição (como **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em coluna]**), navegue até o Conjunto de mídias mistas. Passe o cursor sobre o ativo e toque no ícone de marca de seleção para selecioná-lo. Pressione **[!UICONTROL Backspace]** no teclado ou clique em **[!UICONTROL Mais]** (três pontos) na barra de ferramentas e toque em **[!UICONTROL Excluir.]**
         >
         >
      * Edite os ativos em um Conjunto de mídias mistas ao navegar até o conjunto, clicar em **[!UICONTROL Definir membros]** no painel à esquerda e tocar no ícone **[!UICONTROL Lápis]** em um ativo individual para abrir a janela de edição.


1. Toque em **[!UICONTROL Salvar]** quando terminar a edição.

   >[!NOTE]
   >
   >* Para editar os ativos em um Conjunto de mídias mistas - Navegue até o Conjunto de mídias mistas. Toque (não selecione) no conjunto para abri-lo na página Visualização do conjunto do AEM. No painel à esquerda, clique no sinal de seta para baixo para abrir a lista suspensa e toque em **[!UICONTROL Definir membros.]** Na página Definir membros , passe o mouse sobre um ativo e toque em  **[!UICONTROL Editar]**  (ícone de lápis) para abrir a página de edição.
      >
      >
   * Para excluir um conjunto de mídia mista inteiro - A partir de qualquer modo de exibição (como a Exibição de cartão ou em Coluna), navegue até o conjunto de mídias mistas. Passe o mouse sobre o conjunto e toque em **Selecionar** (ícone de marca de seleção). Pressione **[!UICONTROL Backspace]** no teclado ou toque em **[!UICONTROL Mais]** (linha de três pontos) e toque em **[!UICONTROL Excluir.]**


## Visualização de conjuntos de mídia mista {#previewing-mixed-media-sets}

Consulte [Visualização de ativos](/help/assets/previewing-assets.md) para obter detalhes sobre como visualizar conjuntos de mídia mista.

## Publicar conjuntos de mídia mista {#publishing-mixed-media-sets}

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar Conjuntos de mídias mistas.

>[!NOTE]
>
>Se o conjunto de mídia mista não terminar totalmente no serviço de delivery na primeira vez que você o publicar, talvez seja necessário publicar o conjunto de mídia mista uma segunda vez.

