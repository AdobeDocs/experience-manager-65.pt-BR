---
title: Conjuntos de imagem
description: Saiba como trabalhar com conjuntos de imagens no Dynamic Media
uuid: ca2fd5b0-656e-4960-b10c-f0ec3d418760
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ccc4eb23-934c-4e67-860b-a6faa2bcaafc
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Conjuntos de imagem {#image-sets}

Os Conjuntos de imagens fornecem aos usuários uma experiência de visualização integrada, na qual eles podem ver diferentes visualizações de um item clicando em uma imagem em miniatura. Os Conjuntos de imagens permitem que você apresente exibições alternativas de um item e o visualizador oferece ferramentas de zoom para examinar as imagens de perto.

Conjuntos de imagens são designados por um banner com a palavra `IMAGESET`. Além disso, se o Conjunto de imagens for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]** , estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]** .

![chlimage_1-133](assets/chlimage_1-339.png)

No conjunto de imagens, também é possível criar amostras criando um Conjunto de imagens e adicionando miniaturas.

Esse aplicativo é especialmente útil para quando você deseja mostrar um item em uma cor, padrão ou finalização diferente. Para criar um Conjunto de imagens com amostras de cores, você precisa de uma imagem para cada cor, padrão ou acabamento diferente que deseja apresentar aos usuários. Você também precisa de uma cor, padrão ou amostra de fim para cada cor, padrão ou final.

Por exemplo, suponha que você queira apresentar imagens de maiúsculas com diferentes notas coloridas; as contas são vermelho, verde e azul. Neste caso, você precisa de três tiros do mesmo chapéu. Você precisa de um tiro com um vermelho, um com um verde, e outro com uma conta azul. Você também precisa de uma amostra de cor vermelha, verde e azul. As amostras de cores servem como miniaturas que os usuários clicam no Visualizador do conjunto de amostras para ver a tampa vermelha, com borda verde ou com borda azul.

>[!NOTE]
>
>Para obter informações sobre a interface do usuário Ativos, consulte [Gerenciamento de ativos com a interface do usuário](/help/assets/managing-assets-touch-ui.md)de toque.

## Início rápido: Conjuntos de imagens {#quick-start-image-sets}

Para começar a trabalhar rapidamente:

1. [Carregue suas imagens mestre para várias exibições.](#uploading-assets-in-image-sets)

   Comece carregando as imagens para seus Conjuntos de imagens. Como os usuários podem aplicar zoom em imagens no Visualizador do conjunto de imagens, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão. O AEM Assets suporta vários formatos de arquivo de imagem, mas as imagens TIFF, PNG e EPS sem perdas são recomendadas.

1. [Criar conjuntos de imagens.](#creating-image-sets)

   Em Conjuntos de imagens, os usuários clicam em imagens em miniatura no Visualizador do conjunto de imagens.

   Para criar um Conjunto de imagens em Ativos, toque ou clique em **[!UICONTROL Criar > Conjuntos]** de imagens. Em seguida, adicione imagens e clique em **[!UICONTROL Salvar]**.

   Também é possível criar conjuntos de imagens automaticamente por meio de predefinições [de conjuntos de](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)lotes.
   >[!IMPORTANT]
   >
   > Os conjuntos de lotes são criados pelo IPS (Image Production System) como parte da ingestão de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.

   Consulte [Preparando ativos do Conjunto de imagens para fazer upload e upload dos arquivos](#uploading-assets-in-image-sets).

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

1. Adicione predefinições [do Visualizador do conjunto de](/help/assets/managing-viewer-presets.md)imagens, conforme necessário.

   Os administradores podem criar ou modificar predefinições do visualizador do conjunto de imagens. Para ver o conjunto de imagens com uma predefinição do visualizador, selecione o conjunto de imagens e, no menu suspenso do painel esquerdo, selecione **[!UICONTROL Visualizadores]**.

   Consulte **[!UICONTROL Ferramentas > Ativos > Predefinições]** do visualizador para criar ou editar predefinições do visualizador.

1. (Opcional) [Visualizando Conjuntos](/help/assets/image-sets.md#viewing-image-sets) de Imagens que foram criados usando predefinições de conjuntos de lotes.
1. [Visualizar conjuntos de imagens.](/help/assets/previewing-assets.md)

   Selecione o Conjunto de imagens e você pode visualizá-lo. Clique nos ícones de miniatura para examinar seu Conjunto de imagens no Visualizador selecionado. Você pode escolher visualizadores diferentes no menu **[!UICONTROL Visualizadores]** , disponível no menu suspenso do painel esquerdo.

1. [Publicar conjuntos de imagens.](/help/assets/publishing-dynamicmedia-assets.md)

   A publicação de um conjunto de imagens ativa o URL e a string Incorporada. Além disso, você deve [publicar qualquer predefinição](/help/assets/managing-viewer-presets.md) do visualizador personalizado que tenha criado. As predefinições do visualizador predefinidas já estão publicadas.

1. [Vincule URLs ao aplicativo](/help/assets/linking-urls-to-yourwebapplication.md) da Web ou [Incorpore o visualizador](/help/assets/embed-code.md)de vídeo ou imagem.

   Os ativos AEM criam chamadas de URL para Conjuntos de imagens e as ativam depois que você publica os conjuntos de imagens. Você pode copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de imagens e, no menu suspenso do painel esquerdo, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um conjunto de imagens a uma página](/help/assets/linking-urls-to-yourwebapplication.md) da Web e [Incorporar o visualizador](/help/assets/embed-code.md)de vídeo ou imagem.

Para editar Conjuntos de imagens, consulte [edição de Conjuntos de imagens.](#editing-image-sets) Além disso, é possível exibir e editar as propriedades [do Conjunto de](/help/assets/managing-assets-touch-ui.md#editing-properties)imagens.

Se tiver problemas ao criar conjuntos, consulte Imagens e conjuntos no modo [Solução de](/help/assets/troubleshoot-dms7.md#images-and-sets)problemas de Dynamic Media - Scene7.

## Fazer upload de ativos em conjuntos de imagens {#uploading-assets-in-image-sets}

Comece carregando as imagens para seus Conjuntos de imagens. Como os usuários podem aplicar zoom em imagens no Visualizador do conjunto de imagens, considere o zoom ao escolher imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão. Os Conjuntos de imagens são compatíveis com vários formatos de arquivo de imagem, mas as imagens TIFF, PNG e EPS são recomendadas sem perdas.

Você pode carregar imagens para Conjuntos de imagens da mesma forma que faria [upload de qualquer outro ativo em Ativos](/help/assets/managing-assets-touch-ui.md#uploading-assets).

### Preparando ativos de Conjunto de imagens para upload {#preparing-image-set-assets-for-upload}

Antes de criar Conjuntos de imagens, verifique se as imagens têm o tamanho e o formato corretos.

Para criar um Conjunto de imagens de várias exibições, você precisa de imagens que mostrem um item de diferentes pontos de vista ou mostrem diferentes aspectos do mesmo item. O objetivo é destacar os recursos importantes de um item para que os visualizadores tenham uma imagem completa de como ele se parece ou faz.

Como os usuários podem aplicar zoom em Conjuntos de imagens, verifique se as imagens têm pelo menos 2000 pixels na maior dimensão. Os ativos oferecem suporte para vários formatos de arquivo de imagem, mas são recomendadas imagens TIFF, PNG e EPS sem perdas.

>[!NOTE]
>
>Além disso, se estiver usando miniaturas para indicar amostras de produtos, é necessário fazer o seguinte:
>
>Você precisa de vinhetas ou fotos diferentes da mesma imagem mostrando-as em cores, padrões ou finalizações diferentes. Você também precisa de arquivos em miniatura que correspondam às diferentes cores, padrões ou finalizações. Por exemplo, para apresentar miniaturas com um conjunto de imagens mostrando a mesma jaqueta em preto, marrom e verde, é necessário:
>
>* Um tiro preto, marrom e verde do mesmo casaco.
>* Uma miniatura de cor preta, marrom e verde.


## Criação de conjuntos de imagens {#creating-image-sets}

Você pode criar Conjuntos de imagens pela interface do usuário ou pela API. Esta seção descreve como criar Conjuntos de imagens na interface do usuário.

>[!NOTE]
>
>Também é possível criar conjuntos de imagens automaticamente por meio de predefinições [de conjuntos de](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets)lotes.
>****Importante: Os conjuntos de lotes são criados pelo IPS (Image Production System) como parte da ingestão de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.

Quando você adiciona ativos ao seu conjunto, eles são adicionados automaticamente em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicionados.

>[!NOTE]
>
>Os conjuntos de imagens não são suportados para ativos com &quot;&quot; (vírgula) no nome do arquivo.

**Para criar um conjunto de imagens**

1. No AEM, toque no logotipo do AEM para acessar o console de navegação global e, em seguida, toque em **[!UICONTROL Navegação > Ativos]**. Navegue até o local em que deseja criar um conjunto de imagens, em seguida, toque em **[!UICONTROL Criar > Conjunto]** de imagens para abrir a página do Editor do conjunto de imagens.

   Você também pode criar o conjunto de dentro de uma pasta que contenha seus ativos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Na página Editor do conjunto de imagens, no campo **[!UICONTROL Título]** , digite um nome para o conjunto de imagens. O nome é exibido no banner ao longo do Conjunto de imagens. Opcionalmente, informe uma descrição.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Execute um dos procedimentos a seguir:

   * Perto do canto superior esquerdo da página do Editor de conjunto de imagens, toque em **[!UICONTROL Adicionar ativo]**.

   * Próximo ao meio da página do Editor de conjunto de imagens, toque em **[!UICONTROL Tocar para abrir o Seletor]** de ativos.
   Toque para selecionar os ativos que deseja incluir no Conjunto de imagens. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, toque em **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, você pode procurar ativos digitando uma palavra-chave e tocando ou clicando em **[!UICONTROL Retornar]**. Você também pode aplicar filtros para refinar os resultados da pesquisa. Você pode filtrar por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e toque no ícone **[!UICONTROL Filtro]** na barra de ferramentas. Altere a exibição tocando no ícone Exibir e selecionando Exibição **[!UICONTROL de]** coluna, Exibição **[!UICONTROL de]** cartão ou Exibição **[!UICONTROL de]** lista.

   See [Working with Selectors.](/help/assets/working-with-selectors.md)

   ![6_5_imageset-add-assets](assets/6_5_imageset-addingassets.png)

1. Quando você adiciona ativos ao seu conjunto, eles são adicionados automaticamente em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicioná-los.

   Se necessário, arraste o ícone Reordenar de um ativo à direita do nome do arquivo do ativo para reordenar as imagens para cima ou para baixo na lista definida.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Se quiser alterar uma miniatura ou amostra, clique no ícone de **miniatura** **+** ao lado da imagem e navegue até a miniatura ou a amostra desejada. Quando terminar de selecionar todas as imagens, clique em **[!UICONTROL Salvar]**.

1. (Opcional) Execute um dos procedimentos a seguir:

   * Para excluir uma imagem, selecione-a e toque em **[!UICONTROL Excluir ativo]**.

   * Para aplicar uma predefinição, perto do canto superior direito da página, toque em **[!UICONTROL Predefinir]** e selecione uma predefinição para aplicar a todos os ativos ao mesmo tempo.
   >[!NOTE]
   >
   >Ao criar o conjunto de imagens, você pode alterar a miniatura do conjunto de imagens ou permitir que o AEM selecione a miniatura automaticamente com base nos ativos no conjunto de imagens. Para selecionar uma miniatura, toque em **[!UICONTROL Alterar miniatura]** acima do campo Título na página Editor do conjunto de imagens e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se você tiver selecionado uma miniatura e decidir que deseja que o AEM gere uma do conjunto de imagens, selecione **[!UICONTROL Alternar para]** miniatura **** automática.

1. Clique em **[!UICONTROL Salvar]**. Seu conjunto de imagens recém-criado é exibido na pasta em que você o criou.

## Visualizando conjuntos de imagens {#viewing-image-sets}

Você pode criar conjuntos de imagens na interface do usuário ou automaticamente usando predefinições [de conjuntos de](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets)lotes.

>[!IMPORTANT]
>
>Os conjuntos de lotes são criados pelo IPS [Image Production System] como parte da ingestão de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.)

No entanto, os conjuntos criados usando predefinições de conjuntos de lotes *não* são exibidos na interface do usuário. Você pode ver esses conjuntos de três maneiras diferentes. (Esses métodos estão disponíveis mesmo se você tiver criado os conjuntos de imagens na interface do usuário).

* Abra as propriedades de um ativo individual. As propriedades indicam quais conjuntos o ativo selecionado é referenciado ou um membro do. Clique no nome do conjunto para ver o conjunto inteiro.

   ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties.png)

* De uma imagem de membro de qualquer conjunto. Selecione o menu **[!Conjuntos** UICONTROL para exibir os conjuntos dos quais o ativo é membro.

   ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Na pesquisa, você pode selecionar **[!UICONTROL Filter**, depois expandir **[!UICONTROL Dynamic Media** e selecionar **[!UICONTROL Conjuntos]**.

   A pesquisa retorna conjuntos correspondentes criados manualmente na interface do usuário ou criados automaticamente por meio de predefinições de conjuntos de lotes. Para conjuntos automatizados, a consulta de pesquisa é realizada usando critérios de pesquisa &quot;Começa com&quot; diferentes da pesquisa do AEM, que se baseia no uso de critérios de pesquisa &quot;Contém&quot;. Definir o filtro como **[!UICONTROL Conjuntos]** é a única maneira de pesquisar conjuntos automatizados.

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>É possível exibir os conjuntos por meio da interface do usuário, conforme descrito em [Edição de conjuntos](#editing-image-sets)de imagens.

## Edição de conjuntos de imagens {#editing-image-sets}

Você pode executar várias tarefas de edição em Conjuntos de imagens, como:

* Adicione imagens ao conjunto de imagens.
* Reordene as imagens no Conjunto de imagens.
* Excluir ativos no Conjunto de imagens.
* Aplicar predefinições do visualizador.
* Exclua o conjunto de imagens.

**Para editar conjuntos de imagens**

1. Execute um dos procedimentos a seguir:

   * Passe o mouse sobre um ativo do Conjunto de imagens e toque em **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo do Conjunto de imagens, toque em **[!UICONTROL Selecionar]** (ícone de marca de seleção) e, em seguida, toque em **[!UICONTROL Editar]** na barra de ferramentas.
   * Toque em um ativo do Conjunto de imagens e, em seguida, toque em **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. Para editar as imagens no Conjunto de imagens, execute um dos procedimentos a seguir:

   * Para reorganizar ativos, arraste uma imagem para um novo local (selecione o ícone de reordenação para mover itens).
   * Para classificar itens em ordem crescente ou decrescente, clique no cabeçalho da coluna.
   * Para adicionar um ativo ou atualizar um ativo existente, clique em **[!UICONTROL Adicionar ativo]**. Navegue até um ativo, selecione-o e toque em **[!UICONTROL Selecionar]** próximo ao canto superior direito da página.
      >[!NOTE]
      >
      >Se você excluir a imagem que o AEM usa para a miniatura substituindo-a por outra imagem, o ativo original ainda será exibido.
   * Para excluir um ativo, selecione-o e toque ou clique em **[!UICONTROL Excluir ativo]**.
   * Para aplicar uma predefinição, perto do canto superior direito da página, toque em **[!UICONTROL Predefinir]** e selecione uma predefinição do visualizador.
   * Para adicionar ou alterar uma miniatura, selecione o ícone de miniatura ao lado direito do ativo. Navegue até a nova miniatura ou ativo de amostra, selecione-o e toque em **[!UICONTROL Selecionar]**.
   * Para excluir um conjunto de imagens inteiro, navegue até o conjunto de imagens, selecione-o e toque em **[!UICONTROL Excluir]**.
   >[!NOTE]
   >
   >Você pode editar as imagens em um Conjunto de imagens navegando até o conjunto, tocar em **[!UICONTROL Definir membros]** no painel esquerdo e tocar no ícone Lápis em um ativo individual para abrir a janela de edição.

1. Toque em **[!UICONTROL Salvar]** quando terminar a edição.

## Visualizar conjuntos de imagens {#previewing-image-sets}

Consulte [Visualizar ativos](/help/assets/previewing-assets.md).

## Publicar conjuntos de imagens {#publishing-image-sets}

Consulte [Publicação de ativos](/help/assets/publishing-dynamicmedia-assets.md).
