---
title: Gerenciar coleções de ativos digitais
description: Saiba mais sobre tarefas para gerenciar coleções de ativos, como criar, visualização, excluir, editar e baixar coleções.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0d5a48be283484005013ef3ed7ad015b43f6398b
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 11%

---


# Gerenciar coleções {#managing-collections}

Uma coleção é um conjunto de ativos em [!DNL Adobe Experience Manager Assets]. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou uma coleção dinâmica baseada nos resultados da pesquisa.

Diferentemente das pastas, uma coleção pode incluir ativos de diferentes locais. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo exibição, edição e assim por diante.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida nas coleções.

As coleções são dos seguintes tipos, com base na maneira como elas coletam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui dinamicamente ativos com base em critérios de pesquisa.

## Acesse o console de coleções {#navigating-the-collections-console}

Para abrir as **[!UICONTROL Coleções]**, na interface [!DNL Experience Manager], vá para **[!UICONTROL Ativos]** > **[!UICONTROL Coleções]**.

## Criar uma coleção {#creating-a-collection}

Você pode criar uma coleção com [referências estáticas](#creating-a-collection-with-static-references) ou com base em um [filtro baseado em critérios de pesquisa](#creating-a-smart-collection). Você também pode criar uma coleção a partir de um lightbox.

### Criar uma coleção com referências estáticas {#creating-a-collection-with-static-references}

Você pode criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagens.

1. Navegue até o console **[!UICONTROL Coleções]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar coleção]**, digite um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça as permissões de leitura do grupo `dam-users` no caminho `home/users`. Conceda permissão aos usuários no local `/content/dam/collections` para permitir que eles visualizações as coleções nas listas pop-up. Como alternativa, torne o usuário parte do grupo `dam-users`.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Clique em **[!UICONTROL Criar]** e, em seguida, clique em **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] permite que você crie tarefas de revisão para uma coleção de maneira semelhante à forma como cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário [!DNL Assets]. Para obter detalhes, consulte [Adicionar ativos a uma coleção](#adding-assets-to-a-collection).

### Criar coleções usando o dropzone {#create-collections-using-dropzone}

Você pode arrastar ativos da interface do usuário [!DNL Assets] para uma coleção. Você também pode criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface do usuário [!DNL Assets], selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos para a zona **[!UICONTROL Soltar na Coleção]**. Como alternativa, clique em **[!UICONTROL Para a coleção]** na barra de ferramentas.

   ![drop_in_collection](assets/drop_in_collection.png)

1. Na página **[!UICONTROL Adicionar à coleção]**, clique em **[!UICONTROL Criar coleção]** na barra de ferramentas.

   Se desejar adicionar os ativos a uma coleção existente, selecione-a na página e clique em **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.

1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Clique em **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#creating-a-smart-collection}

Uma coleção inteligente usa um critério de pesquisa para preencher dinamicamente ativos. Você pode criar uma coleção inteligente usando apenas arquivos e não pastas ou arquivos e pastas.

Para criar uma coleção inteligente, siga as etapas:

1. Navegue até a [!DNL Assets] interface do usuário e clique em pesquisar.

1. Digite a palavra-chave de pesquisa na caixa Omnisearch e pressione `Enter`. Abra o painel Filtros e aplique um filtro de pesquisa.

1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.

   ![files_option](assets/files_option.png)

1. Clique em **[!UICONTROL Salvar coleção inteligente]**.

1. Especifique um nome para a coleção. Selecione **[!UICONTROL Public]** para adicionar o grupo Usuários DAM com a função Visualizador à coleção inteligente.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente ficará disponível para todos com a função de proprietário depois que você a criar. Se você desmarcar a opção **[!UICONTROL Public]**, o grupo de usuários do DAM não estará mais associado à coleção inteligente.

1. Clique em **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo.

   A nova coleção inteligente também é adicionada à lista **[!UICONTROL Pesquisas salvas.]**

   ![collection_list](assets/collection_listing.png)

   O rótulo da opção **[!UICONTROL Criar seleção inteligente]** muda para **[!UICONTROL Editar seleção inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Clique na opção **[!UICONTROL Editar seleção inteligente]** ![editar coleção inteligente](assets/do-not-localize/edit-smart-collection.png).

## Adicionar ativos a uma coleção {#adding-assets-to-a-collection}

Você pode adicionar ativos a uma coleção que contenha uma lista de ativos ou pastas referenciados. Coleções inteligentes usam um query de pesquisa para preencher ativos. Portanto, referências estáticas a ativos e pastas não se aplicam a eles.

1. Na interface do usuário dos ativos [!DNL A]selecione o ativo e clique em **[!UICONTROL Para a coleção]** ![adicionar à coleção](assets/do-not-localize/add-to-collection.png) na barra de ferramentas.
Como alternativa, você pode arrastar o ativo para a área **[!UICONTROL Soltar na Coleção]** na interface. Adicione os ativos quando o rótulo da região mudar para **[!UICONTROL Soltar para Adicionar]**.

1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção à qual deseja adicionar o ativo.

1. Clique em **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#editing-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar seu conteúdo modificando os parâmetros de pesquisa de [pesquisa salva](#saved-searches).

1. Na interface do usuário [!DNL Assets], clique na opção de pesquisa ![opção de pesquisa](assets/do-not-localize/search_icon.png) na barra de ferramentas.
1. Com o cursor na caixa Omnisearch, pressione a tecla Return.
1. Na interface [!DNL Experience Manager], abra o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Clique em **[!UICONTROL Editar coleção inteligente]**.

   Você também pode editar o nome da coleção inteligente.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. Clique em **[!UICONTROL Salvar]**. A caixa de diálogo **[!UICONTROL Editar coleção inteligente]** é exibida.
1. Clique em **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Salvar]** para concluir o processo.

## Visualização e edição de metadados da coleção {#view-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo quaisquer tags adicionadas.

1. No console [!UICONTROL Coleções], selecione uma coleção e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**.
1. Modifique os metadados, conforme necessário. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas.

## Editar metadados de várias coleções em massa {#editing-collection-metadata-in-bulk}

Você pode editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções, selecione duas ou mais coleções.
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Para visualização das propriedades de metadados de uma coleção específica, desmarque as coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página [!UICONTROL Propriedades], é possível remover coleções da lista de coleções desmarcando-as. A lista de coleções tem todas as coleções selecionadas por padrão. [!DNL Experience Manager] não atualiza os metadados das coleções que você remove.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Title]** para alternar entre a seleção das coleções e a limpeza da lista.


1. Clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação.
1. Para anexar os novos metadados aos metadados existentes, selecione **[!UICONTROL Modo Anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >Os metadados adicionados para as coleções selecionadas substituem os metadados anteriores para essas coleções. Use o [!UICONTROL modo Anexar] para adicionar novos valores aos metadados existentes nos campos que podem conter vários valores. Campos de valor único são sempre substituídos. Quaisquer tags adicionadas no campo [!UICONTROL Tags] serão anexadas à lista existente de tags nos metadados.

Para personalizar a página de metadados [!UICONTROL Propriedades], incluindo a adição, modificação e exclusão de propriedades de metadados, use o editor de Schemas.

>[!TIP]
>
>O método de edição em massa funciona para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível [atualizar os metadados em massa depois de pesquisar](/help/assets/search-assets.md#metadataupdates).

## Pesquisar coleções {#searching-collections}

Você pode pesquisar coleções no console Coleções. Quando você pesquisa com palavras-chave na caixa Omnisearch, [!DNL Assets] pesquisa nomes de coleção, metadados e as tags adicionadas às coleções.

Se você pesquisar por coleções do nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. [!DNL Assets] ou as pastas dentro das coleções são excluídas. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pastas), todos os ativos, pastas e coleções relevantes são retornados.

## Pesquisar em coleções {#searching-within-collections}

No console Coleções, clique em uma coleção para abri-la.

Em uma coleção, a pesquisa [!DNL Experience Manager] está restrita aos ativos (e suas tags e metadados) dentro da coleção que você está visualizando. Quando você pesquisar em uma pasta, todos os ativos correspondentes e pastas secundárias dentro da pasta atual serão retornados. Quando você pesquisa em uma coleção, somente os ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações de coleção {#editing-collection-settings}

Você pode editar configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e clique em **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Settings]** da miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, as descrições, os membros e as permissões conforme discutido em [Adicionar coleções](#creating-a-collection).

1. Para salvar as alterações, clique em **[!UICONTROL Salvar]**.

## Excluir uma coleção {#deleting-a-collection}

1. No console Coleções, selecione uma ou mais coleções e clique em excluir da barra de ferramentas.

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Também é possível excluir coleções inteligentes ao excluir [pesquisas salvas](#saved-searches).

## Baixar uma coleção {#downloading-a-collection}

Quando você baixa uma coleção, toda a hierarquia de ativos dentro dela é baixada, incluindo pastas e coleções-filho.

1. No console Coleções, selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, clique em **[!UICONTROL Download]**.
1. Na caixa de diálogo **[!UICONTROL Baixar]**, clique em **[!UICONTROL Baixar]**. Se desejar baixar as representações dos ativos dentro da coleção, selecione **[!UICONTROL Representações]**. Selecione a opção **[!UICONTROL Email]** para enviar uma notificação por email ao proprietário da coleção.

   Quando você seleciona uma coleção para download, a hierarquia completa da pasta sob a coleção é baixada. Para incluir cada coleção que você baixa (incluindo ativos em coleções secundárias aninhadas sob a coleção pai) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Criar coleções aninhadas {#creating-nested-collections}

É possível adicionar uma coleção a outra coleção, criando uma coleção aninhada.

1. No console Coleções, selecione a coleção ou o grupo de coleções desejado e clique em **[!UICONTROL Para a coleção]** na barra de ferramentas.

1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção na qual deseja adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]**.

1. Clique em **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de públicos alvos na página **[!UICONTROL Selecionar destino]**. Feche a mensagem para concluir o processo.

>[!NOTE]
>
>Coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface do usuário [!DNL Assets], você pode pesquisar ou filtrar ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

![saved_search_lista](assets/saved_searches_list.png)

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. O query [!UICONTROL Pesquisas Salvas] para a coleção é salvo na propriedade `dam:query` no CRXDE no local relativo `/content/dam/collections/`. Não há limites para as pesquisas que você pode salvar e nas pesquisas salvas exibidas na lista.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma forma que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [editar uma coleção inteligente](#editing-a-smart-collection).

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface do usuário [!DNL Assets], clique em pesquisar ![opção de pesquisa](assets/do-not-localize/search_icon.png).
1. Com o cursor no campo Omnisearch, pressione a tecla Return.
1. Na interface [!DNL Experience Manager], abra o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, clique em **[!UICONTROL Excluir]** ao lado da coleção inteligente que você deseja excluir.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#running-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos de duplicado, o fluxo de trabalho só será executado uma vez para esses ativos.

1. Abra **[!UICONTROL Ativos]** > **[!UICONTROL Coleções]**. Para executar um fluxo de trabalho em uma coleção específica, selecione-a.
1. Abra o painel **[!UICONTROL Linha do tempo]**. Clique em ![divisa para cima](assets/do-not-localize/chevron-up-icon.png) e clique em **[!UICONTROL Fluxo de trabalho do Start]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e clique em **[!UICONTROL Start]**.
1. Na caixa de diálogo, clique em **[!UICONTROL Prosseguir]**. O fluxo de trabalho processa todos os ativos na coleção selecionada.

>[!MORELIKETHIS]
>
>* [Configurar notificações por email do Experience Manager Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Criar uma tarefa de revisão para coleções](bulk-approval.md)

