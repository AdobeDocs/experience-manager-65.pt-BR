---
title: Gerenciar coleções de ativos digitais
description: Saiba mais sobre tarefas para gerenciar coleções de ativos, como criar, visualização, excluir, editar e baixar coleções.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Gerenciar coleções {#managing-collections}

Uma coleção é um conjunto de ativos nos ativos Adobe Experience Manager. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou uma coleção dinâmica baseada nos resultados da pesquisa.

Diferentemente das pastas, uma coleção pode incluir ativos de diferentes locais. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo exibição, edição e assim por diante.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida nas coleções.

As coleções são dos seguintes tipos, com base na maneira como elas coletam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui dinamicamente ativos com base em critérios de pesquisa.

## Acesse o console de coleções {#navigating-the-collections-console}

Para abrir as **[!UICONTROL Coleções]**, na interface do Experience Manager, vá até **[!UICONTROL Ativos]** > **[!UICONTROL Coleções]**.

## Criar uma coleção {#creating-a-collection}

Você pode criar uma coleção com referências [](#creating-a-collection-with-static-references) estáticas ou com base em um filtro [baseado em critérios de](#creating-a-smart-collection)pesquisa. Você também pode criar uma coleção a partir de um lightbox.

### Criar uma coleção com referências estáticas {#creating-a-collection-with-static-references}

Você pode criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagens.

1. Navegue até o console **[!UICONTROL Coleções]** .
1. Na barra de ferramentas, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar coleção]** , digite um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça ao `dam-users` grupo permissões de leitura no caminho `home/users`. Conceda permissão aos usuários no `/content/dam/collections` local para permitir que eles visualizações as coleções nas listas pop-up. Como alternativa, torne o usuário parte do `dam-users` grupo.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Click **[!UICONTROL Create]**, and then click **[!UICONTROL OK]** to close the dialog. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >Os Ativos do Experience Manager permitem que você crie tarefas de revisão para uma coleção semelhantes à maneira como você cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário Ativos. Para obter detalhes, consulte [Adicionar ativos a uma coleção](#adding-assets-to-a-collection).

### Criar coleções usando o dropzone {#create-collections-using-dropzone}

Você pode arrastar ativos da interface do usuário Ativos para uma coleção. Você também pode criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface do usuário Ativos, selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos até a zona **[!UICONTROL Soltar na coleção]** . Como alternativa, clique no ícone **[!UICONTROL Para coleção]** na barra de ferramentas.

   ![drop_in_collection](assets/drop_in_collection.png)

1. In the **[!UICONTROL Add To Collection]** page, click the **[!UICONTROL Create Collection]** icon from the toolbar.

   If you want to add the assets to an existing collection, select it from the page, and click **[!UICONTROL Add]**. Por padrão, a coleção atualizada mais recentemente é selecionada.

1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Clique em **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#creating-a-smart-collection}

Uma coleção inteligente usa um critério de pesquisa para preencher dinamicamente ativos. Você pode criar uma coleção inteligente usando apenas arquivos e não pastas ou arquivos e pastas.

Para criar uma coleção inteligente, siga as etapas:

1. Navegue até a interface do usuário Ativos e clique em pesquisar.

1. Digite a palavra-chave de pesquisa na caixa Omnisearch e pressione `Enter`. Abra o painel Filtros e aplique um filtro de pesquisa.

1. Na lista **[!UICONTROL Arquivos e pastas]** , selecione **[!UICONTROL Arquivos]**.

   ![files_option](assets/files_option.png)

1. Clique em **[!UICONTROL Salvar coleção]** inteligente.

1. Especifique um nome para a coleção. Selecione **[!UICONTROL Público]** para adicionar o grupo Usuários DAM com a função Visualizador à coleção inteligente.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente ficará disponível para todos com a função de proprietário depois que você a criar. Se você desmarcar a opção **[!UICONTROL Público]** , o grupo de usuários do DAM não estará mais associado à coleção inteligente.

1. Click **[!UICONTROL Save]** to create the smart collection, and then close the message box to complete the process.

   A nova coleção inteligente também é adicionada à lista **[!UICONTROL Pesquisas salvas.]**

   ![collection_list](assets/collection_listing.png)

   O rótulo do botão **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Then, Click the **[!UICONTROL Edit Smart Selection]** button.

   ![chlimage_1-7](assets/chlimage_1-112.png)

## Adicionar ativos a uma coleção {#adding-assets-to-a-collection}

Você pode adicionar ativos a uma coleção que contenha uma lista de ativos ou pastas referenciados. Coleções inteligentes usam um query de pesquisa para preencher ativos. Portanto, referências estáticas a ativos e pastas não se aplicam a eles.

1. Na interface do usuário Ativos, selecione o ativo e clique no ícone **[!UICONTROL Para coleção]** na barra de ferramentas.

   ![chlimage_1-8](assets/chlimage_1-113.png)

   Como alternativa, você pode arrastar o ativo para a área **[!UICONTROL Soltar na coleção]** na interface. Adicione os ativos quando o rótulo da região mudar para **[!UICONTROL Soltar para Adicionar]**.

1. Na página **[!UICONTROL Adicionar à coleção]** , selecione a coleção à qual deseja adicionar o ativo.

1. Clique em **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#editing-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar seu conteúdo modificando os parâmetros de pesquisa da pesquisa [](#saved-searches)salva.

1. Na interface do usuário do Assets, clique no ícone de pesquisa na barra de ferramentas.

   ![chlimage_1-9](assets/chlimage_1-110.png)

1. Com o cursor na caixa Omnisearch, pressione a tecla Return.
1. Clique no ícone GlobalNav para exibir o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Na lista **[!UICONTROL Arquivos e pastas]** , selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Clique em **[!UICONTROL Editar coleção]** inteligente.

   Você também pode editar o nome da coleção inteligente.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. Clique em **[!UICONTROL Salvar]**. A caixa de diálogo **[!UICONTROL Editar coleção]** inteligente é exibida.
1. Clique em **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Salvar]** para concluir o processo.

## Visualização e edição de metadados da coleção {#viewing-and-editing-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo quaisquer tags adicionadas.

1. No console Coleções, selecione uma coleção e clique no ícone **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**.
1. Modifique os metadados, conforme necessário, e clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas para salvar as alterações.

## Editar metadados de várias coleções em massa {#editing-collection-metadata-in-bulk}

Você pode editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções, selecione duas ou mais coleções para as quais deseja editar metadados.
1. Na barra de ferramentas, clique no ícone **[!UICONTROL Propriedades]** .
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Para visualização das propriedades de metadados de uma coleção específica, desmarque as coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções desmarcando-as. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções que você remover não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção das coleções e a limpeza da lista.


1. Clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação para concluir o processo.
1. To append the new metadata with the existing metadata, select **[!UICONTROL Append mode]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >Os metadados adicionados para as coleções selecionadas substituem os metadados anteriores para essas coleções. Use o modo  Anexar para adicionar novos valores aos metadados existentes nos campos que podem conter vários valores. Campos de valor único são sempre substituídos. Quaisquer tags adicionadas no campo [!UICONTROL Tags] serão anexadas à lista existente de tags nos metadados.

Para personalizar a página [!UICONTROL Propriedades] de metadados, incluindo adicionar, modificar e excluir propriedades de metadados, use o editor de Schemas.

>[!TIP]
>
>O método de edição em massa funciona para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível atualizar [em massa os metadados após a pesquisa](/help/assets/search-assets.md#metadataupdates).

## Pesquisar coleções {#searching-collections}

Você pode pesquisar coleções no console Coleções. Quando você pesquisa com palavras-chave na caixa Omnisearch, o AEM Assets pesquisa nomes de coleção, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções do nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. Os ativos ou pastas dentro das coleções são excluídos. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pastas), todos os ativos, pastas e coleções relevantes são retornados.

## Pesquisar em coleções {#searching-within-collections}

No console Coleções, clique em uma coleção para abri-la.

Em uma coleção, a pesquisa do AEM Asset está restrita aos ativos (e suas tags e metadados) dentro da coleção que você está visualizando. Quando você pesquisar em uma pasta, todos os ativos correspondentes e pastas secundárias dentro da pasta atual serão retornados. Quando você pesquisa em uma coleção, somente os ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações de coleção {#editing-collection-settings}

Você pode editar configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e clique no ícone **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Configurações]** na miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. For example, modify the collection title, descriptions, members, and permissions as discussed in [Adding Collections](#creating-a-collection).

1. Para salvar as alterações, clique em **[!UICONTROL Salvar]**.

## Excluir uma coleção {#deleting-a-collection}

1. No console Coleções, selecione uma ou mais coleções e clique no ícone excluir na barra de ferramentas.

   ![chlimage_1-11](assets/chlimage_1-177.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Também é possível excluir coleções inteligentes [excluindo pesquisas](#saved-searches)salvas.

## Baixar uma coleção {#downloading-a-collection}

Quando você baixa uma coleção, toda a hierarquia de ativos dentro dela é baixada, incluindo pastas e coleções-filho.

1. No console Coleções, selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, clique no ícone de download.
1. Na caixa de diálogo **[!UICONTROL Download]** , clique em **[!UICONTROL Download]**. Se desejar baixar as representações dos ativos dentro da coleção, selecione **[!UICONTROL Representações]**. Selecione a opção **[!UICONTROL Email]** para enviar uma notificação por email ao proprietário da coleção.

   Quando você seleciona uma coleção para download, a hierarquia completa da pasta sob a coleção é baixada. Para incluir cada coleção que você baixa (incluindo ativos em coleções secundárias aninhadas sob a coleção pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Criar coleções aninhadas {#creating-nested-collections}

É possível adicionar uma coleção a outra coleção, criando uma coleção aninhada.

1. No console Coleções, selecione a coleção ou o grupo de coleções desejado e clique em **[!UICONTROL Para coleção]** na barra de ferramentas.

1. Na página **[!UICONTROL Adicionar à coleção]** , selecione a coleção na qual deseja adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]** .

1. Clique em **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de públicos alvos na página **[!UICONTROL Selecionar destino]** . Feche a mensagem para concluir o processo.

>[!NOTE]
>
>Coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface do usuário do Assets, pesquise ou filtre ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

![saved_search_lista](assets/saved_searches_list.png)

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. A consulta Pesquisas salvas da coleção é salva na propriedade `dam:query`, no CRXDE no local relativo `/content/dam/collections/`.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma forma que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [editar uma coleção](#editing-a-smart-collection)inteligente.

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface do usuário do Assets, clique no ícone de pesquisa na barra de ferramentas.

   ![chlimage_1-13](assets/chlimage_1-114.png)

1. Com o cursor no campo Omnisearch, pressione a tecla Enter.

1. Clique no ícone GlobalNav para exibir o painel Filtros.

1. From the **[!UICONTROL Saved Searches]** list, click **[!UICONTROL Delete]** next to the smart collection that you want to delete.

   ![select_smart_collection-1](assets/select_smart_collection-1.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#running-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos de duplicado, o fluxo de trabalho só será executado uma vez para esses ativos.

1. No console Coleções, selecione uma coleção na qual deseja executar um fluxo de trabalho.
1. Clique no ícone GlobalNav e escolha **[!UICONTROL Linha do tempo]** na lista.
1. From the timeline, click the Caret icon at the bottom, and then click **[!UICONTROL Start Workflow]**.

   ![chlimage_1-14](assets/chlimage_1-137.png)

1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e clique em **[!UICONTROL Start]**.
1. In the dialog, click **[!UICONTROL Proceed]**. O fluxo de trabalho é executado em todos os ativos na coleção.

>[!MORELIKETHIS]
>
>* [Configurar notificações por email dos ativos do Experience Manager](/help/sites-administering/notification.md#assetsconfig)
>* [Criar uma tarefa de revisão para coleções](bulk-approval.md)

