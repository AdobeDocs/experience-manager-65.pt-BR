---
title: Conjuntos de imagem
description: Saiba como trabalhar com conjuntos de imagens no Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Image Sets,Asset Management
role: User, Admin
exl-id: 2a536745-fa13-4158-8761-2ac5b6e1893e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 5%

---

# Conjuntos de imagem {#image-sets}

Os Conjuntos de imagens oferecem aos usuários uma experiência de visualização integrada, em que os usuários podem ver diferentes visualizações de um item selecionando uma imagem em miniatura. Os Conjuntos de imagens permitem apresentar visualizações alternativas de um item e o visualizador oferece ferramentas de zoom para examinar as imagens de perto.

Os conjuntos de imagens são designados por um banner com a palavra `IMAGESET`. Além disso, se o Conjunto de imagens for publicado, a data de publicação, indicada pelo ícone **[!UICONTROL Mundo]**, estará no banner junto com a última data de modificação, indicada pelo ícone **[!UICONTROL Lápis]**.

![Conjunto de imagens](assets/chlimage_1-339.png)

No Conjunto de imagens, também é possível criar amostras criando um Conjunto de imagens e adicionando miniaturas.

Esse aplicativo é útil para quando você deseja mostrar um item em uma cor, padrão ou fim diferente. Para criar um Conjunto de imagens com amostras de cores, é necessário ter uma imagem para cada cor, padrão ou acabamento diferente que você deseja apresentar aos usuários. Você também precisa de uma amostra de cor, padrão ou fim para cada cor, padrão ou fim.

Por exemplo, suponha que você queira apresentar imagens de tampas com diferentes listas de cores; as listas são vermelha, verde e azul. Neste caso, você precisa de três doses do mesmo boné. Você precisa de uma foto com um vermelho, uma com verde e outra com uma nota azul. Você também precisa de uma amostra de cor vermelha, verde e azul. As amostras de cores servem como miniaturas que os usuários selecionam no Visualizador de conjuntos de amostras para ver a tampa de faturamento vermelho, verde ou azul.

>[!NOTE]
>
>Para obter informações sobre a interface do usuário do Assets, consulte [Gerenciar ativos](/help/assets/manage-assets.md).

Ao criar um Conjunto de imagens, o Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número de ativos duplicados por conjunto | Sem duplicatas | 20‡ |
| Número máximo de imagens por conjunto | De 5 a 10 imagens por conjunto | 1000 |

‡ A prática recomendada é não ter ativos duplicados em um conjunto. O limite é de 20 duplicatas para um único ativo. Se você adicionar outra duplicata para esse ativo — dentro desse conjunto — a solicitação retornará um erro ou ignorará a duplicata.

Consulte também [limitações do Dynamic Media](/help/assets/limitations.md).

## Início rápido: conjuntos de imagens {#quick-start-image-sets}

**Para que você possa começar a trabalhar rapidamente:**

1. [Faça upload das imagens de origem primária para várias exibições](#uploading-assets-in-image-sets).

   Comece fazendo upload das imagens para os seus Conjuntos de imagens. Ao escolher imagens, lembre-se de que seus clientes podem ampliar imagens no Visualizador do conjunto de imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão para obter os detalhes de zoom ideais. O Dynamic Media pode renderizar imagens de até 25 MP (megapixels) cada uma. Por exemplo, você pode usar uma imagem de 5000 x 5000 MP ou qualquer outra combinação de tamanho de até 25 MP.

   Consulte [Dynamic Media - Formatos de imagem de varredura compatíveis](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) para obter uma lista de formatos compatíveis com Conjuntos de imagens.

<!--    Adobe Experience Manager Assets supports many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

1. [Criar um Conjunto de Imagens](#creating-image-sets).

   Em Conjuntos de imagens, os usuários selecionam imagens em miniatura no Visualizador do conjunto de imagens.

   Para criar um Conjunto de Imagens no Assets, acesse **[!UICONTROL Criar]** > **[!UICONTROL Conjuntos de Imagens]**. Em seguida, adicione imagens e selecione **[!UICONTROL Salvar]**.

   Você também pode criar conjuntos de imagens automaticamente por meio de [predefinições de conjunto de lotes](/help/assets/config-dms7.md).
   >[!IMPORTANT]
   >
   >Os conjuntos em lotes são criados pelo IPS (Sistema de produção de imagem) como parte da assimilação de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.

   Consulte [Preparar ativos do Conjunto de Imagens para carregar e carregar seus arquivos](#uploading-assets-in-image-sets).

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md).

1. Adicione [predefinições do Visualizador do Conjunto de Imagens](/help/assets/managing-viewer-presets.md), conforme necessário.

   Os administradores podem criar ou modificar as Predefinições do visualizador de conjunto de imagens. Para ver seu Conjunto de imagens com uma predefinição do visualizador, selecione o Conjunto de imagens e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições do Visualizador]** se desejar criar ou editar predefinições do visualizador.

1. (Opcional) [Exibir um Conjunto de Imagens](/help/assets/image-sets.md#viewing-image-sets) que foi criado usando predefinições de conjunto de lotes.
1. [Visualizar Conjuntos de Imagens](/help/assets/previewing-assets.md).

   Selecione o Conjunto de imagens para poder visualizá-lo. Selecione os ícones de miniatura para que você possa examinar seu Conjunto de imagens no Visualizador selecionado. Você pode escolher visualizadores diferentes no menu **[!UICONTROL Visualizadores]**, disponível no menu suspenso do painel esquerdo.

1. [Publish e Conjunto de Imagens](/help/assets/publishing-dynamicmedia-assets.md).

   A publicação de um Conjunto de imagens ativa o URL e o código incorporado. Além disso, você deve [publicar qualquer predefinição do visualizador personalizado](/help/assets/managing-viewer-presets.md) que tenha criado. As predefinições do visualizador pronto para uso já estão publicadas.

1. [Vincular URLs ao Aplicativo Web](/help/assets/linking-urls-to-yourwebapplication.md) ou [Incorporar o Visualizador de Vídeo ou Imagem](/help/assets/embed-code.md).

   O Experience Manager Assets cria chamadas de URL para Conjuntos de imagens e as ativa após a publicação dos conjuntos de imagens. É possível copiar esses URLs ao visualizar ativos. Como alternativa, você pode incorporá-los ao seu site.

   Selecione o Conjunto de imagens e, no menu suspenso do painel à esquerda, selecione **[!UICONTROL Visualizadores]**.

   Consulte [Vincular um Conjunto de Imagens a uma página da Web](/help/assets/linking-urls-to-yourwebapplication.md) e [Incorporar o Visualizador de Vídeo ou Imagem](/help/assets/embed-code.md).

Para editar conjuntos de imagens, consulte [Editar conjuntos de imagens](#editing-image-sets). Além disso, você pode exibir e editar [propriedades do Conjunto de Imagens](/help/assets/manage-assets.md#editing-properties).

Se tiver problemas ao criar conjuntos, consulte Imagens e Conjuntos em [Solução de problemas do Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md#images-and-sets).

## Fazer upload de ativos em Conjuntos de imagens {#uploading-assets-in-image-sets}

Comece fazendo upload das imagens para os seus Conjuntos de imagens. Ao escolher imagens, lembre-se de que seus clientes podem ampliar imagens no Visualizador do conjunto de imagens. Verifique se as imagens têm pelo menos 2000 pixels na maior dimensão. Os Conjuntos de imagens são compatíveis com muitos formatos de arquivo de imagem, mas são recomendadas imagens de TIFF, PNG e EPS sem perdas.

Você pode carregar imagens para Conjuntos de imagens da mesma maneira que faria [ao carregar qualquer outro ativo no Assets](/help/assets/manage-assets.md#uploading-assets).

Consulte [Dynamic Media - Formatos de imagem de varredura compatíveis](/help/assets/assets-formats.md#supported-raster-image-formats-dynamic-media) para obter uma lista de formatos compatíveis com Conjuntos de imagens.

### Preparar ativos do conjunto de imagens para upload {#preparing-image-set-assets-for-upload}

Antes de criar Conjuntos de imagens, verifique se as imagens têm o tamanho e o formato corretos.

Para criar um Conjunto de imagens com várias visualizações, você precisa de imagens que mostrem um item de diferentes pontos de vista ou mostrem diferentes aspectos do mesmo item. O objetivo é destacar os recursos importantes de um item para que os visualizadores tenham uma imagem completa da aparência ou do funcionamento.

Como os usuários podem ampliar imagens em Conjuntos de imagens, verifique se as imagens têm pelo menos 2000 pixels na maior dimensão. <!-- Assets support many image file formats, but lossless TIFF, PNG, and EPS images are recommended. -->

>[!NOTE]
>
>Além disso, se estiver usando miniaturas para indicar amostras de produtos, você deve fazer o seguinte:
>
>Você precisa de vinhetas ou fotos diferentes da mesma imagem mostrando-a em cores, padrões ou acabamentos diferentes. Você também precisa de arquivos de miniatura que correspondam às diferentes cores, padrões ou acabamentos. Por exemplo, para apresentar miniaturas com um Conjunto de imagens mostrando a mesma jaqueta em preto, marrom e verde, é necessário:
>
>* Um tiro preto, marrom e verde do mesmo casaco.
>* Uma miniatura de cor preta, marrom e verde.

## Criar um conjunto de imagens {#creating-image-sets}

É possível criar Conjuntos de imagens por meio da interface do usuário ou da API. Esta seção descreve como criar conjuntos de imagens na interface do.

>[!NOTE]
>
>Você também pode criar conjuntos de imagens automaticamente por meio de [predefinições de conjunto de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).
>**Importante:** conjuntos em lotes são criados pelo IPS (Sistema de Produção de Imagens) como parte da assimilação de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.

Ao adicionar ativos ao conjunto, eles são automaticamente adicionados em ordem alfanumérica. É possível reordenar ou classificar manualmente os ativos depois de adicionados.

>[!NOTE]
>
>Os conjuntos de imagens não são compatíveis com ativos com &quot;,&quot; (vírgula) no nome do arquivo.

Ao criar um Conjunto de imagens, o Adobe recomenda as seguintes práticas recomendadas e impõe os seguintes limites:

| Tipo de limite | Prática recomendada | Limite imposto |
| --- | --- | --- |
| Número de ativos duplicados por conjunto | Sem duplicatas | 20‡ |
| Número máximo de imagens por conjunto | De 5 a 10 imagens por conjunto | 1000 |

‡ A prática recomendada é não ter ativos duplicados em um conjunto. O limite é de 20 duplicatas para um único ativo. Se você adicionar outra duplicata para esse ativo — dentro desse conjunto — a solicitação retornará um erro ou ignorará a duplicata.

Consulte também [limitações do Dynamic Media](/help/assets/limitations.md).

**Para criar um Conjunto de Imagens:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e vá para **[!UICONTROL Navegação]** > **[!UICONTROL Assets]**. Navegue até o local em que você deseja criar um Conjunto de imagens, em seguida, vá para **[!UICONTROL Criar]** > **[!UICONTROL Conjunto de imagens]** para abrir a página Editor do Conjunto de imagens.

   Você também pode criar o conjunto de dentro de uma pasta que contenha seus ativos.

   ![6_5_imagesets-createpulldown](assets/6_5_imagesets-createpulldown.png)

1. Na página Editor do conjunto de imagens, no campo **[!UICONTROL Título]**, digite um nome para o conjunto de imagens. O nome aparece no banner no Conjunto de imagens. Opcionalmente, informe uma descrição.

   ![6_5_imageset-creatingnewset](assets/6_5_imageset-creatingnewset.png)

1. Siga um destes procedimentos:

   * Próximo ao canto superior esquerdo da página Editor do conjunto de imagens, selecione **[!UICONTROL Adicionar ativo]**.

   * Próximo ao meio da página Editor do conjunto de imagens, selecione **[!UICONTROL Toque para abrir o Seletor de ativos]**.

   Selecione os ativos que deseja incluir no Conjunto de imagens. Os ativos selecionados têm um ícone de marca de seleção sobre eles. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Selecionar]**.

   Com o Seletor de ativos, procure por ativos ao digitar uma palavra-chave e tocar ou clicar em **[!UICONTROL Retornar]**. Aplique filtros para refinar os resultados da pesquisa. Filtre por caminho, coleção, tipo de arquivo e tag. Selecione o filtro e o ícone **[!UICONTROL Filtro]** na barra de ferramentas. Altere a exibição ao tocar no ícone Exibir e selecionar **[!UICONTROL Exibição em coluna]**, **[!UICONTROL Exibição de cartão]** ou **[!UICONTROL Exibição em lista]**.

   Consulte [Trabalhar com seletores](/help/assets/working-with-selectors.md).

   ![6_5_imageset-addingassets](assets/6_5_imageset-addingassets.png)

1. Ao adicionar ativos ao conjunto, eles são automaticamente adicionados em ordem alfanumérica. Você pode reordenar ou classificar manualmente os ativos depois de adicioná-los.

   Se necessário, arraste o ícone Reordenar de um ativo à direita do nome do arquivo do ativo para reordenar imagens para cima ou para baixo na lista definida.

   ![6_5_imageset-reorderassets](assets/6_5_imageset-reorderassets.png)

   Se quiser alterar uma miniatura ou amostra, selecione o ícone de **+** **miniatura** ao lado da imagem e navegue até a miniatura ou a amostra desejada. Quando terminar de selecionar todas as imagens, selecione **[!UICONTROL Salvar]**.

1. (Opcional) Siga qualquer um destes procedimentos:

   * Para excluir uma imagem, selecione-a e selecione **[!UICONTROL Excluir ativo]**.

   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione **[!UICONTROL Predefinição]** e, em seguida, selecione uma predefinição para aplicar a todos os ativos ao mesmo tempo.

   >[!NOTE]
   >
   >Ao criar o Conjunto de imagens, você pode alterar a miniatura do Conjunto de imagens ou permitir que o Experience Manager selecione a miniatura automaticamente com base nos ativos no Conjunto de imagens. Para selecionar uma miniatura, selecione **[!UICONTROL Alterar miniatura]** acima do campo Título na página Editor do conjunto de imagens e selecione qualquer imagem (você também pode navegar para outras pastas para localizar imagens). Se tiver selecionado uma miniatura e decidir que deseja que o Experience Manager gere uma a partir do Conjunto de imagens, selecione **[!UICONTROL Alternar para]** > **[!UICONTROL Miniatura automática]**.

1. Selecione **[!UICONTROL Salvar]**. O conjunto de imagens recém-criado aparece na pasta em que você o criou.

## Exibir um conjunto de imagens {#viewing-image-sets}

Você pode criar conjuntos de imagens na interface ou automaticamente usando [predefinições de conjunto de lotes](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets).

>[!IMPORTANT]
>
>Os conjuntos em lotes são criados pelo IPS [Sistema de Produção de Imagens] como parte da assimilação de ativos e estão disponíveis somente no modo Dynamic Media - Scene7.)

No entanto, conjuntos criados usando predefinições de conjunto de lotes, *não*, aparecerão na interface do usuário. Você pode visualizar esses conjuntos de três maneiras diferentes. (Esses métodos estão disponíveis mesmo se você tiver criado os conjuntos de imagens na interface do usuário do ).

* Abra as propriedades de um ativo individual. As propriedades indicam quais conjuntos o ativo selecionado é referenciado ou um membro de. Selecione o nome do conjunto se quiser ver todo o conjunto.

  ![6_5_imageset-assetproperties](assets/6_5_imageset-assetproperties2.png)

* A partir de uma imagem de membro de qualquer conjunto. Selecione o menu **[!UICONTROL Conjuntos]** para exibir os conjuntos dos quais o ativo é membro.

  ![6_5_imageset-setspulldownmenu](assets/6_5_imageset-setspulldownmenu.png)

* Na pesquisa, você pode selecionar **[!UICONTROL Filtro]**, expandir **[!UICONTROL Dynamic Media]** e selecionar **[!UICONTROL Conjuntos]**.

  A pesquisa retorna conjuntos correspondentes que foram criados manualmente na interface do usuário ou criados automaticamente por meio de predefinições de conjunto de lotes. Para conjuntos automatizados, a consulta de pesquisa é conduzida usando o critério de pesquisa &quot;Inicia com&quot;, que é diferente da pesquisa de Experience Manager, que se baseia no uso do critério de pesquisa &quot;Contém&quot;. Configurar o filtro como **[!UICONTROL Conjuntos]** é a única maneira de pesquisar conjuntos automatizados.

  ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>É possível exibir conjuntos por meio da interface de usuário, conforme descrito em [Editar conjuntos de imagens](#editing-image-sets).

## Editar um conjunto de imagens {#editing-image-sets}

É possível executar várias tarefas de edição em Conjuntos de imagens, como as seguintes:

* Adicionar imagens ao conjunto de imagens.
* Reordenar imagens no Conjunto de imagens.
* Excluir ativos no Conjunto de imagens.
* Aplicar predefinições do visualizador.
* Exclua o conjunto de imagens.

**Para editar um conjunto de imagens:**

1. Siga um destes procedimentos:

   * Passe o mouse sobre um ativo Conjunto de imagens e selecione **[!UICONTROL Editar]** (ícone de lápis).
   * Passe o mouse sobre um ativo Conjunto de imagens, selecione **[!UICONTROL Selecionar]** (ícone de marca de seleção) e **[!UICONTROL Editar]** na barra de ferramentas.
   * Selecione em um ativo Conjunto de imagens e selecione **[!UICONTROL Editar]** (ícone de lápis) na barra de ferramentas.

1. Para editar as imagens no Conjunto de imagens, siga um destes procedimentos:

   * Para reordenar ativos, arraste uma imagem para um novo local (selecione o ícone reordenar para mover itens).
   * Para classificar itens em ordem crescente ou decrescente, selecione o cabeçalho da coluna.
   * Para adicionar um ativo ou atualizar um ativo existente, selecione **[!UICONTROL Adicionar ativo]**. Navegue até um ativo, selecione-o e, em seguida, selecione **[!UICONTROL Selecionar]** próximo ao canto superior direito da página.

     >[!NOTE]
     >
     >Se você excluir a imagem que o Experience Manager usa para a miniatura substituindo-a por outra imagem, o ativo original ainda será exibido.
   * Para excluir um ativo, selecione-o e selecione **[!UICONTROL Excluir ativo]**.
   * Para aplicar uma predefinição, próximo ao canto superior direito da página, selecione **[!UICONTROL Predefinição]** e, em seguida, selecione uma predefinição do visualizador.
   * Para adicionar ou alterar uma miniatura, selecione o ícone de miniatura à direita do ativo. Navegue até a nova miniatura ou ativo de amostra, selecione-o e, em seguida, selecione **[!UICONTROL Selecionar]**.
   * Para excluir um Conjunto de Imagens inteiro, navegue até o Conjunto de Imagens, selecione-o e **[!UICONTROL Excluir]**.

   >[!NOTE]
   >
   >Edite as imagens em um Conjunto de imagens ao navegar até o conjunto, selecionar **[!UICONTROL Definir membros]** no painel à esquerda e selecionar o ícone Lápis em um ativo individual para abrir a janela de edição.

1. Selecione **[!UICONTROL Salvar]** quando terminar a edição.

## Visualizar um conjunto de imagens {#previewing-image-sets}

Consulte [Visualização de ativos](/help/assets/previewing-assets.md).

## Publish e conjunto de imagens {#publishing-image-sets}

Consulte [Publicação de Assets](/help/assets/publishing-dynamicmedia-assets.md).
