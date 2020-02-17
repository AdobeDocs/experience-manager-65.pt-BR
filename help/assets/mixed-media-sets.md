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
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Conjuntos de mídia mista{#mixed-media-sets}

Os Conjuntos de mídia mista permitem que você forneça uma combinação de imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos em uma única apresentação.

Os Conjuntos de mídia mista são designados por um banner com a palavra **[!UICONTROL MixedMediaSet]**. Além disso, se o Conjunto de mídias mistas for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]** , estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]** .

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Para obter informações sobre a interface do usuário Ativos, consulte [Gerenciamento de ativos com a interface do usuário](/help/assets/managing-assets-touch-ui.md)de toque.

## Início rápido: Conjuntos de mídia mista {#quick-start-mixed-media-sets}

Para iniciá-lo rapidamente com Conjuntos de mídia mista, siga estas etapas:

1. [Carregue seus ativos](#uploading-assets).

   Comece carregando as imagens e os vídeos dos seus Conjuntos de Mídias Mistas. Se necessário, crie seus Conjuntos [de](/help/assets/image-sets.md) imagens e Conjuntos de [rotação](/help/assets/spin-sets.md). Como os usuários podem aplicar zoom em imagens no Visualizador de conjunto de mídia mista, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

1. [Criar conjuntos de mídia mista.](#creating-mixed-media-sets)

   Para criar um Conjunto de mídia mista, na página Ativos, toque em **[!UICONTROL Criar > Conjunto]** de mídia mista e nomeie o conjunto, escolha os ativos e escolha a ordem em que as imagens serão exibidas.

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Configure predefinições [do visualizador de mídia](/help/assets/managing-viewer-presets.md)mista, conforme necessário.

   Os administradores podem criar ou modificar predefinições do visualizador de conjunto de mídia mista. Para ver sua mídia mista com uma predefinição do visualizador, selecione o conjunto de mídias mistas e, no menu suspenso esquerdo, selecione **[!UICONTROL Visualizadores]**.

   Consulte **[!UICONTROL Ferramentas > Ativos > Predefinições]** do visualizador para criar ou editar predefinições do visualizador.

   Consulte [Adicionar e editar predefinições do visualizador.](/help/assets/managing-viewer-presets.md)

1. [Visualizar conjuntos de mídia mista.](#previewing-mixed-media-sets)

   Selecione o Conjunto de mídia mista e você pode visualizá-lo. Clique nos ícones de miniatura para examinar seu Conjunto de mídia mista no visualizador selecionado. Você pode escolher visualizadores diferentes no menu **[!UICONTROL Visualizadores]** , disponível no menu suspenso do painel esquerdo.

1. [Publicar conjuntos de mídia mista.](#publishing-mixed-media-sets)

   A publicação de um Conjunto de mídia mista ativa o URL e a string Incorporada. Além disso, você deve [publicar a predefinição](/help/assets/managing-viewer-presets.md#publishing-viewer-presets)do visualizador.

1. [Vincule URLs ao aplicativo](/help/assets/linking-urls-to-yourwebapplication.md) da Web ou [Incorpore o visualizador](/help/assets/embed-code.md)de vídeo ou imagem.

   Os ativos AEM criam chamadas de URL para Conjuntos de mídia mista e as ativam após a publicação dos conjuntos de mídia mista. Você pode copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione Mixed Media Set e, no menu suspenso do painel esquerdo, selecione **[!UICONTROL Viewers]**.

   Consulte [Vincular um conjunto de mídia mista a uma página](/help/assets/linking-urls-to-yourwebapplication.md) da Web e [Incorporar o visualizador](/help/assets/embed-code.md)de vídeo ou imagem.

Se necessário, edite Conjuntos de mídia [mista](#editing-mixed-media-sets). Além disso, você pode exibir e modificar as propriedades [do Conjunto de mídia](/help/assets/managing-assets-touch-ui.md#editing-properties)mista.

>[!NOTE]
>
>Se tiver problemas ao criar conjuntos, consulte [Solução de problemas do Dynamic Media - modo](/help/assets/troubleshoot-dms7.md)Scene7.

## Carregar ativos {#uploading-assets}

Comece carregando as imagens e os vídeos dos seus Conjuntos de Mídias Mistas. Como os usuários podem aplicar zoom em imagens no Visualizador de conjunto de mídia mista, lembre-se de levar em conta o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão.

Além disso, se você quiser adicionar conjuntos de rotação ou conjuntos de imagens ao conjunto de mídia mista, crie-os também.

## Criação de conjuntos de mídia mista {#creating-mixed-media-sets}

Você pode adicionar imagens, Conjuntos de imagens, Conjuntos de rotação e vídeos ao seu Conjunto de mídia mista. Verifique se os arquivos, os conjuntos de imagens e os conjuntos de rotação estão prontos para publicação antes de adicioná-los ao Conjunto de Mídia Mista.

Quando você adiciona ativos ao seu conjunto, eles são adicionados automaticamente em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicionados.

**Para criar um conjunto de mídia mista**

1. Em Ativos, navegue até o local em que deseja criar um conjunto de mídia mista, clique em **[!UICONTROL Criar]** e selecione Conjunto **[!UICONTROL de mídia]** mista. Você também pode criar o conjunto de dentro de uma pasta que contenha seus ativos. O Mixed Media Set Editor é exibido.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. No Editor de conjunto de mídia mista, em **[!UICONTROL Título]**, digite um nome para o conjunto de mídia mista. O nome é exibido no banner no Conjunto de mídia mista. Opcionalmente, informe uma descrição.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de mídias mistas, você pode alterar a miniatura do conjunto de mídias mistas ou permitir que o AEM selecione a miniatura automaticamente com base nos ativos do conjunto de mídias mistas. Para selecionar uma miniatura, clique em **[!UICONTROL Alterar miniatura]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se você tiver selecionado uma miniatura e decidir que deseja que o AEM gere uma do conjunto de mídias mistas, selecione **[!UICONTROL Alternar para miniatura]** automática.

1. Toque no Seletor de ativos para selecionar os ativos que deseja incluir no Conjunto de mídias mistas. Selecione-os e clique em **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, você pode procurar ativos digitando uma palavra-chave e tocando em **[!UICONTROL Retornar]**. Você também pode aplicar filtros para refinar os resultados da pesquisa. Você pode filtrar por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]** na barra de ferramentas. Altere a exibição selecionando o ícone **[!UICONTROL Exibir]** e selecionando **[!UICONTROL Exibição]** de lista, Exibição **[!UICONTROL de]** coluna ou Exibição **[!UICONTROL de]** cartão.

   See [Working with Selectors](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Reorganize os ativos arrastando-os para cima ou para baixo na lista (deve selecionar o ícone **[!UICONTROL Reordenar]** ), conforme necessário.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Se desejar adicionar miniaturas, clique no ícone de **+** **[!UICONTROL miniatura]** ao lado da imagem e navegue até a miniatura desejada. Quando terminar de selecionar todas as imagens em miniatura, clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Se desejar adicionar ativos, toque em **[!UICONTROL Adicionar ativo]**.

1. Para excluir um ativo, marque a caixa de seleção correspondente e toque em **[!UICONTROL Excluir ativo]**.
1. Para aplicar uma predefinição, toque em **[!UICONTROL Predefinir]** no canto superior direito e selecione uma predefinição para aplicar aos ativos.
1. Clique em **[!UICONTROL Salvar]**. Seu conjunto de mídia mista recém-criado é exibido na pasta em que você o criou.

## Edição de conjuntos de mídia mista {#editing-mixed-media-sets}

Você pode executar várias tarefas de edição em ativos em Conjuntos de mídia mista diretamente na interface do usuário, [como faria com qualquer ativo em Ativos](/help/assets/managing-assets-touch-ui.md). Você também pode executar as seguintes ações em Conjuntos de mídia mista:

* Adicione ativos ao Conjunto de mídia mista.
* Resolicite ativos no Conjunto de mídia mista.
* Exclua ativos no Conjunto de mídias mistas.
* Aplicar predefinições do visualizador.
* Altere a miniatura padrão.

**Para editar um conjunto de mídia mista**

1. Execute um dos procedimentos a seguir:

   * Passe o mouse sobre um ativo de Conjunto de mídia mista e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo de Conjunto de mídia mista, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, em seguida, toque em **[!UICONTROL Editar]** na barra de ferramentas.

   * Toque em um ativo Conjunto de mídia mista e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. No Mixed Media Set Editor, execute um dos procedimentos a seguir:

   * Para reorganizar ativos - No painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem), arraste um ativo para um novo local.
   * Para adicionar ativos - Na barra de ferramentas, toque em **[!UICONTROL Adicionar ativo]**. Navegue até os ativos. Para cada ativo que você deseja adicionar, passe o mouse sobre a imagem do ativo (não o nome do ativo) e toque no ícone de marca de seleção. No canto superior direito, toque em **[!UICONTROL Selecionar]**.

   * Para excluir um ativo - no painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem) e selecione o ativo. Na barra de ferramentas, toque em **[!UICONTROL Excluir ativo]**.

   * Para classificar os ativos pelo nome em ordem crescente ou decrescente, no painel esquerdo, toque em **[!UICONTROL Ativos]** (ícone de imagem). À direita do cabeçalho **[!UICONTROL Ativos]** , toque nos ícones de cursor para cima ou para baixo.

      >[!NOTE]
      >
      >    * Para excluir um Conjunto de mídia mista inteiro, de qualquer modo de exibição (como Exibição **[!UICONTROL de]** cartão ou Exibição **[!UICONTROL de]** coluna), navegue até o Conjunto de mídia mista. Passe o mouse sobre o ativo e toque no ícone de marca de seleção para selecioná-lo. Pressione **[!UICONTROL Backspace]** no teclado ou clique em **[!UICONTROL Mais]** (três pontos) na barra de ferramentas e, em seguida, toque em **[!UICONTROL Excluir]**.
         >
         >    
      * Você pode editar os ativos em um Conjunto de mídias mistas navegando até o conjunto, clicando em **Definir membros]** no painel esquerdo e tocando no ícone **[!UICONTROL Lápis]** em um ativo individual para abrir a janela de edição.


1. Toque em **[!UICONTROL Salvar]** quando terminar a edição.

   >[!NOTE]
   >
   >* Para editar os ativos em um Conjunto de mídias mistas - navegue até o Conjunto de mídias mistas. Toque (não selecione) no conjunto para abri-lo na página Visualização do conjunto de AEM. No painel esquerdo, clique no sinal de seta para baixo para abrir a lista suspensa e toque em **[!UICONTROL Definir membros]**. Na página Definir membros, passe o mouse sobre um ativo e toque em **[!UICONTROL Editar]** (ícone de lápis) para abrir a página de edição.
      >
      >
   * Para excluir um conjunto de mídia mista inteiro - de qualquer modo de exibição (como a exibição de Cartão ou de Coluna), navegue até o conjunto de mídia mista. Passe o mouse sobre o conjunto e, em seguida, toque em **Selecionar]** (ícone de marca de seleção). Pressione **[!UICONTROL Backspace]** no teclado ou toque em **[!UICONTROL More (fileira de três pontos) e, em seguida, em]** Delete (Excluir ****).


## Visualização de conjuntos de mídia mista {#previewing-mixed-media-sets}

Consulte [Visualizar ativos](/help/assets/previewing-assets.md) para obter detalhes sobre como visualizar Conjuntos de mídia mista.

## Publicação de conjuntos de mídia mista {#publishing-mixed-media-sets}

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md) para obter detalhes sobre como publicar Conjuntos de mídia mista.

>[!NOTE]
>
>Se o conjunto de mídias mistas não terminar totalmente no serviço de entrega na primeira vez que você o publicar, talvez seja necessário publicar o conjunto de mídias mistas uma segunda vez.

