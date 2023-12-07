---
title: Conjuntos de rotação
description: Saiba como criar um conjunto de rotação no Dynamic Media para simular o ato do mundo real de girar um objeto e visualizá-lo de qualquer ângulo para que você possa ver os detalhes.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Spin Sets,Asset Management
role: User, Admin
exl-id: 758ad754-15de-4e72-9b7d-ab49c51d7d4f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 8%

---

# Conjuntos de rotação{#spin-sets}

Um Conjunto de rotação simula o ato do mundo real de virar um objeto para examiná-lo. Os Conjuntos de rotação permitem a visualização de itens de qualquer ângulo, obtendo os principais detalhes visuais de qualquer ângulo.

Um Conjunto de rotação simula uma experiência de visualização de 360 graus. O Dynamic Media oferece Conjuntos de rotação de eixo único nos quais os visualizadores podem girar um item. Além disso, os usuários podem aplicar o zoom de forma &quot;livre&quot; e deslocar qualquer uma das visualizações com apenas alguns cliques. Dessa forma, os usuários podem examinar um item mais detalhadamente de um ponto de vista específico.

Os conjuntos de rotação são designados por um banner com a palavra **[!UICONTROL SPINSET]**. Além disso, se o Conjunto de rotação for publicado, a data de publicação, indicada pela variável **[!UICONTROL Mundo]** está no banner junto com a última data de modificação, indicada pela variável **[!UICONTROL Lápis]** é exibido.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Para obter informações sobre a interface do Assets, consulte [Gerenciar ativos](/help/assets/manage-assets.md).

Ao criar um Conjunto de rotação, o Adobe recomenda a seguinte prática recomendada e impõe os seguintes limites:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 |

Consulte também [Limitações do Dynamic Media](/help/assets/limitations.md).

## Início rápido: conjuntos de rotação {#quick-start-spin-sets}

Para começar a usar rapidamente os Conjuntos de rotação, siga estas etapas:

1. [Fazer upload de imagens para várias exibições](#uploading-assets-for-spin-sets).

   No mínimo, você precisa de 8 a 12 imagens de um item para um Conjunto de rotação unidimensional e 16 a 24 para um Conjunto de rotação bidimensional. As fotos devem ser tiradas em intervalos regulares para dar a impressão de que o item está girando e sendo virado. Por exemplo, se um Conjunto de rotação unidimensional incluir 12 disparos, gire o item 30° (360/12) para cada disparo.

   Consulte [Dynamic Media - Formatos de imagem rasterizada compatíveis](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) para obter uma lista de formatos compatíveis com Conjuntos de rotação.

1. [Criar um grupo de rotação](#creating-spin-sets).

   Para criar um Conjunto de rotação, selecione **[!UICONTROL Criar > Conjunto de rotação]** e, em seguida, nomeie o conjunto, escolha os ativos e escolha a ordem em que as imagens serão exibidas.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >Também é possível criar conjuntos de rotação automaticamente por meio de [predefinições de conjuntos em lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:** Os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da assimilação de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.

1. Configurar [Predefinições do visualizador de conjunto de rotação](/help/assets/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de rotação. Para ver seu conjunto de rotação com uma predefinição do visualizador, selecione o conjunto de rotação e, no menu suspenso do painel à esquerda, selecione **Visualizadores**.

   Consulte **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições do visualizador]** se quiser criar ou editar predefinições do visualizador.

   Consulte [Adicionar e editar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

1. [Exibir um grupo de rotação](#viewing-spin-sets).

   É possível visualizar e acessar conjuntos criados por meio de predefinições de conjuntos em lotes de três maneiras diferentes. (Conjuntos criados usando predefinições de conjunto de lotes, *não* aparecerão na interface do usuário.)

1. [Visualizar um conjunto de rotação](/help/assets/previewing-assets.md).

   Selecione o Conjunto de rotação e você pode visualizá-lo. Gire o grupo de rotação. Você pode escolher visualizadores diferentes da **[!UICONTROL Visualizadores]** disponível no menu suspenso do painel esquerdo.

1. [Publicar um grupo de rotação](/help/assets/publishing-dynamicmedia-assets.md).

   A publicação de um Conjunto de rotação ativa o URL e a Cadeia de caracteres incorporada. Além disso, você deve [publicar a predefinição do visualizador](/help/assets/managing-viewer-presets.md).

1. [Vincular URLs ao aplicativo da Web](/help/assets/linking-urls-to-yourwebapplication.md) ou [Incorporar o visualizador de vídeo ou imagem](/help/assets/embed-code.md).

   O Adobe Experience Manager Assets cria chamadas de URL para conjuntos de rotação e as ativa após a publicação dos conjuntos de rotação. É possível copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de rotação e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um grupo de rotação a uma página da Web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporar o visualizador de vídeo ou imagem](/help/assets/embed-code.md).

Se necessário, você pode [editar um grupo de rotação](#editing-spin-sets). Além disso, é possível exibir e modificar [Propriedades do grupo de rotação](/help/assets/manage-assets.md#editing-properties).

## Fazer upload de ativos para um Spin Set {#uploading-assets-for-spin-sets}

No mínimo, você precisa de 8 a 12 imagens de um item para um Conjunto de rotação unidimensional e 16 a 24 para um Conjunto de rotação bidimensional. As fotos devem ser tiradas em intervalos regulares para dar a impressão de que o item está girando e sendo virado. Por exemplo, se um Conjunto de rotação unidimensional incluir 12 disparos, gire o item 30° (360/12) para cada disparo.

Você pode fazer upload de imagens para os Conjuntos de rotação da mesma maneira [fazer upload de qualquer outro ativo no Experience Manager Assets](/help/assets/manage-assets.md).

Consulte [Dynamic Media - Formatos de imagem rasterizada compatíveis](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) para obter uma lista de formatos compatíveis com Conjuntos de rotação.

### Diretrizes para captura de imagens para seu Spin Set {#guidelines-for-shooting-spin-set-images}

Veja a seguir algumas práticas recomendadas para imagens do conjunto de rotação. Em geral, quanto mais imagens você tiver em um Conjunto de rotação, melhor será o efeito de rotação da imagem. No entanto, a inclusão de muitas imagens no conjunto também aumenta a quantidade de tempo que as imagens levam para serem carregadas. O Experience Manager recomenda estas diretrizes para fotografar imagens para uso em Conjuntos de rotação:

* No mínimo, use 8 a 12 imagens em um conjunto de rotação unidimensional e 16 a 24 imagens em um Conjunto de rotação bidimensional. É necessário um mínimo de 8 imagens para girar 360 graus. Os Conjuntos de rotação unidimensionais são mais comuns, pois criar Conjuntos de rotação bidimensionais é uma tarefa trabalhosa.
* Use um formato sem perdas; TIFF e PNG são recomendados.
* Mascarar todas as imagens para que o item apareça em branco puro ou em outro plano de fundo de alto contraste. Como opção, adicione sombras.
* Verifique se os detalhes do produto estão bem iluminados e em foco.
* Faça imagens giratórias para roupas de moda com um manequim ou modelo. Muitas vezes, o manequim é mascarado (usando um manequim de vidro) ou um manequim estilizado/costureira é mostrado na imagem. Você pode criar um conjunto de rotação no modelo definindo o número de ângulos. Marque cada ângulo com fita no chão para que você possa guiar o modelo para pisar e olhar na direção de cada tomada.

## Criar um grupo de rotação {#creating-spin-sets}

Esta seção descreve como criar um Conjunto de rotação no Experience Manager.

>[!NOTE]
>
>Também é possível criar conjuntos de rotação automaticamente por meio de [predefinições de conjuntos em lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). **Importante:** Os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da assimilação de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.
>
>Consulte &quot;Criação de predefinições de conjunto de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação&quot; em [Configurar o modo Dynamic Media - Scene7](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>

>[!NOTE]
>
>A ordem em que as imagens aparecem em um conjunto de rotação é importante. Certifique-se de ordená-los para que a rotação seja uma visualização suave de 360 graus.

Ao criar um Conjunto de rotação, o Adobe recomenda a seguinte prática recomendada e impõe os seguintes limites:

| Tipo de limite | Prática recomendada | Limitado imposto |
| --- | --- | --- |
| Número máximo de linhas/colunas por conjunto 2D | 12 a 18 imagens por conjunto | 1000 |

Consulte também [Limitações do Dynamic Media](/help/assets/limitations.md).

**Para criar um Conjunto de rotação:**

1. No Assets, navegue até o local em que deseja criar um conjunto de rotação, selecione **[!UICONTROL Criar]** e selecione **[!UICONTROL Grupo de rotação]**. Além disso, crie o conjunto de dentro de uma pasta que contenha seus ativos. O Editor de conjunto de rotação é exibido.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. No Editor de conjunto de rotação, no **[!UICONTROL Título]** insira um nome para o grupo de rotação. O nome aparece no banner no Spin Set. Opcionalmente, informe uma descrição.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Ao criar o conjunto de rotação, você pode alterar a miniatura do conjunto de rotação ou permitir que o Experience Manager selecione a miniatura automaticamente com base nos ativos no conjunto de rotação. Para selecionar uma miniatura, selecione **[!UICONTROL Alterar miniatura]** e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se tiver selecionado uma miniatura e decidir que deseja que o Experience Manager gere uma a partir do conjunto de rotação, selecione **[!UICONTROL Alternar para miniatura automática]**.

1. Siga um destes procedimentos:

   * Próximo ao canto superior esquerdo da página Editor de conjunto de rotação, selecione **[!UICONTROL Adicionar ativo]**.

   * Próximo ao meio da página Editor do grupo de rotação, selecione **[!UICONTROL Selecione para abrir o Seletor de ativos]**.

   Selecione para selecionar os ativos que deseja incluir no Spin Set. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar em **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e, em seguida, selecione a variável **[!UICONTROL Filtro]** na barra de ferramentas. Altere a exibição ao tocar no ícone Exibir e selecionar **[!UICONTROL Exibição em coluna]**, **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em lista]**.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Ao adicionar ativos ao conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicioná-los.

   Se necessário, arraste o ícone Reordenar de um ativo à direita do nome do arquivo do ativo para reordenar as imagens para cima, para baixo ou para cima na lista definida.

   ![Reordene o Quadro 11 no conjunto de rotação arrastando-o para um novo local](assets/6_5_spinset-reorderassets.png).

   Reordenando o Quadro 11 no conjunto de rotação arrastando-o para um novo local.

1. (Opcional) Siga qualquer um destes procedimentos:

   * Para excluir uma imagem, selecione-a e **[!UICONTROL Excluir ativo]**.

   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione **[!UICONTROL Predefinição]**, em seguida, selecione uma predefinição para aplicar a todos os ativos de uma só vez.

1. Selecionar **[!UICONTROL Salvar]**. O conjunto de rotação recém-criado aparece na pasta em que você o criou.

## Exibir um grupo de rotação {#viewing-spin-sets}

É possível criar conjuntos de rotação na interface do usuário ou automaticamente usando [predefinições de conjunto de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets). No entanto, os conjuntos criados usando predefinições de conjunto de lotes, *não* aparecerão na interface do usuário. É possível acessar conjuntos criados por meio de predefinições de conjuntos em lotes de três maneiras diferentes. (Esses métodos estão disponíveis mesmo se você tiver criado os conjuntos de rotação na interface do usuário do ).

>[!NOTE]
>
>Também é possível exibir conjuntos por meio da interface do usuário, conforme descrito em [Editar conjuntos de rotação](#editing-spin-sets).

**Para exibir um conjunto de rotação:**

1. Ao abrir as propriedades de um ativo individual. As propriedades indicam o que define o ativo selecionado como membro de (em **[!UICONTROL Membro de conjuntos]**). Selecione o nome do conjunto para que você possa ver todo o conjunto.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. A partir de uma imagem de membro de qualquer conjunto. Selecione o **[!UICONTROL Conjuntos]** para exibir os conjuntos dos quais o ativo é membro.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Na pesquisa, você pode selecionar **[!UICONTROL Filtros]**, expandir o **[!UICONTROL Dynamic Media]** e selecionar **[!UICONTROL Conjuntos]**.

   A pesquisa retorna conjuntos correspondentes que foram criados manualmente na interface do usuário ou criados automaticamente por meio de predefinições de conjunto de lotes. Para conjuntos automatizados, a consulta de pesquisa é realizada usando `Starts with` critérios de pesquisa diferentes da pesquisa de Experience Manager, que se baseia no uso de `Contains` critérios de pesquisa. Definir o filtro como **[!UICONTROL Conjuntos]** O é a única maneira de pesquisar conjuntos automatizados.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Editar um grupo de rotação {#editing-spin-sets}

É possível executar várias tarefas de edição em Conjuntos de rotação, como as seguintes:

* Adicione imagens ao Spin Set.
* Reordenar imagens no Spin Set.
* Excluir ativos no Spin Set.
* Aplicar predefinições do visualizador.
* Exclua o grupo de rotação.

**Para editar um grupo de rotação:**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo de conjunto de rotação e selecione **[!UICONTROL Editar]** (lápis).
   * Passe o mouse sobre um ativo de grupo de rotação, selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção), selecione **[!UICONTROL Editar]** na barra de ferramentas.

   * Selecione em um ativo de conjunto de rotação e selecione **[!UICONTROL Editar]** (lápis) na barra de ferramentas.

1. Para editar o Conjunto de rotação, siga um destes procedimentos:

   * Para reordenar imagens, arraste uma imagem para um novo local (selecione o ícone reordenar para mover itens).
   * Para classificar itens em ordem crescente ou decrescente, selecione o cabeçalho da coluna.
   * Para adicionar ou atualizar um ativo existente, selecione **[!UICONTROL Adicionar ativo]**. Navegue até um ativo, selecione-o e selecione **[!UICONTROL Selecionar]** próximo ao canto superior direito.
Se você excluir a imagem que o Experience Manager usa para a miniatura substituindo-a por outra imagem, o ativo original ainda será exibido.
   * Para excluir um ativo, selecione-o e **[!UICONTROL Excluir ativo]**.
   * Para aplicar uma predefinição, selecione o ícone Predefinição e selecione uma predefinição.
   * Para excluir um Conjunto de rotação inteiro, navegue até o Conjunto de rotação, selecione-o e **[!UICONTROL Excluir]**
   >[!NOTE]
   >
   >É possível editar as imagens em um Conjunto de imagens ao navegar até o conjunto e selecionar **[!UICONTROL Definir membros]** no painel à esquerda e selecione o ícone Lápis em um ativo individual para abrir a janela de edição.

1. Selecionar **[!UICONTROL Salvar]** ao concluir a edição.

## Visualizar um conjunto de rotação {#previewing-spin-sets}

Consulte [Visualizar ativos](/help/assets/previewing-assets.md).

## Publicar um grupo de rotação {#publishing-spin-sets}

Consulte [Publicar ativos](/help/assets/publishing-dynamicmedia-assets.md).
