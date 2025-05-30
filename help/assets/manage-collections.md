---
title: Gerenciar coleções de ativos digitais
description: Saiba mais sobre tarefas para gerenciar coleções de ativos, como criar, exibir, excluir, editar e baixar coleções.
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 14%

---

# Gerenciar coleções {#managing-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Uma coleção é um conjunto de ativos em [!DNL Adobe Experience Manager Assets]. Use coleções para compartilhar ativos entre usuários. O conjunto pode ser uma coleção estática ou dinâmica com base nos resultados da pesquisa.

Diferente de pastas, uma coleção pode incluir ativos de locais diferentes. Você pode compartilhar coleções com vários usuários aos quais são atribuídos diferentes níveis de privilégios, incluindo visualização, edição etc.

Você pode compartilhar várias coleções com um usuário. Cada coleção contém referências a ativos. A integridade referencial dos ativos é mantida entre as coleções.

As coleções são dos seguintes tipos, com base na maneira como elas agrupam ativos:

* Uma coleção que contém uma lista de referência estática de ativos, pastas e outras coleções.

* Uma coleção inteligente que inclui ativos dinamicamente com base em um critério de pesquisa.

## Acessar o console de coleções {#navigating-the-collections-console}

Para abrir as **[!UICONTROL Coleções]**, na interface [!DNL Experience Manager], vá para **[!UICONTROL Assets]** > **[!UICONTROL Coleções]**.

## Criar uma coleção {#creating-a-collection}

Você pode criar uma coleção com [referências estáticas](#creating-a-collection-with-static-references) ou com base em um [filtro baseado em critérios de pesquisa](#creating-a-smart-collection). Você também pode criar uma coleção de uma lightbox.

### Criar uma coleção com referências estáticas {#creating-a-collection-with-static-references}

É possível criar uma coleção com referências estáticas, por exemplo, uma coleção com referências a ativos, pastas, coleções, conjuntos de rotação e conjuntos de imagem.

1. Navegue até o console **[!UICONTROL Coleções]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar Coleção]**, insira um título e uma descrição opcional para a coleção.
1. Adicione membros à coleção e atribua as permissões apropriadas. Como alternativa, selecione **[!UICONTROL Coleção pública]** para permitir que todos os usuários acessem a coleção.

   >[!NOTE]
   >
   >Para permitir que os membros compartilhem coleções com outros usuários, forneça ao grupo `dam-users` permissões de leitura no caminho `home/users`. Conceda permissão aos usuários no local `/content/dam/collections` para permitir que eles exibam as Coleções em listas pop-up. Como alternativa, torne o usuário parte do grupo `dam-users`.

1. (Opcional) Adicione uma imagem em miniatura para a coleção.
1. Clique em **[!UICONTROL Criar]** e em **[!UICONTROL OK]** para fechar a caixa de diálogo. Uma coleção com o título e as propriedades especificadas é aberta no console Coleções.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] permite criar tarefas de revisão para uma coleção semelhante à maneira como você cria tarefas de revisão para uma pasta de ativos.

   Para adicionar ativos à coleção, navegue até a interface do usuário do [!DNL Assets]. Para obter detalhes, consulte [Adicionar ativos a uma coleção](#adding-assets-to-a-collection).

### Criar coleções usando a zona de destino {#create-collections-using-dropzone}

Você pode arrastar ativos da interface de usuário do [!DNL Assets] para uma coleção. Também é possível criar uma cópia de uma coleção e arrastar os ativos para lá.

1. Na interface de usuário do [!DNL Assets], selecione os ativos que deseja adicionar a uma coleção.
1. Arraste os ativos para a zona **[!UICONTROL Soltar na coleção]**. Como alternativa, clique em **[!UICONTROL Para a Coleção]** na barra de ferramentas.

   ![drop_in_collection](assets/drop_in_collection.png)

1. Na página **[!UICONTROL Adicionar à coleção]**, clique em **[!UICONTROL Criar coleção]** na barra de ferramentas.

   Para adicionar os ativos a uma coleção existente, selecione-a na página e clique em **[!UICONTROL Adicionar]**. Por padrão, a coleção atualizada mais recentemente é selecionada.

1. Na caixa de diálogo **[!UICONTROL Criar nova coleção]**, especifique o nome da coleção. Se quiser que a coleção seja acessível a todos os usuários, selecione **[!UICONTROL Coleção pública]**.
1. Clique em **[!UICONTROL Continuar]** para criar a coleção.

### Criar uma coleção inteligente {#creating-a-smart-collection}

Uma coleção inteligente usa critérios de pesquisa para preencher ativos dinamicamente. Você pode criar uma coleção inteligente usando somente arquivos e não pastas ou arquivos e pastas.

Para criar uma coleção inteligente, siga as etapas:

1. Navegue até a interface de usuário do [!DNL Assets] e clique em pesquisar.

1. Digite a palavra-chave de pesquisa na caixa Omnisearch e selecione `Enter`. Abra o painel Filtros e aplique um filtro de pesquisa.

1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.

   ![opção_de_arquivos](assets/files_option.png)

1. Clique em **[!UICONTROL Salvar coleção inteligente]**.

1. Especifique um nome para a coleção. Selecione **[!UICONTROL Público]** para adicionar o grupo Usuários DAM com a função de Visualizador à coleção inteligente.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >Se você selecionar **[!UICONTROL Público]**, a coleção inteligente ficará disponível para todos com a função de proprietário depois de criá-la. Se você cancelar a opção **[!UICONTROL Pública]**, o grupo de usuários do DAM não será mais associado à coleção inteligente.

1. Clique em **[!UICONTROL Salvar]** para criar a coleção inteligente e feche a caixa de mensagem para concluir o processo.

   A nova coleção inteligente também foi adicionada à lista **[!UICONTROL Pesquisas salvas]**.

   ![listagem_de_coleção](assets/collection_listing.png)

   O rótulo da opção **[!UICONTROL Criar Seleção Inteligente]** é alterado para **[!UICONTROL Editar Seleção Inteligente]**. Para editar as configurações da coleção inteligente, selecione **[!UICONTROL Arquivos]** na lista **[!UICONTROL Arquivos e pastas]**. Clique na opção **[!UICONTROL Editar Seleção Inteligente]** ![editar coleção inteligente](assets/do-not-localize/edit-smart-collection.png).

## Adicionar ativos a uma coleção {#adding-assets-to-a-collection}

É possível adicionar ativos a uma coleção que contém uma lista de ativos ou pastas referenciados. As coleções inteligentes usam uma consulta de pesquisa para preencher ativos. Portanto, as referências estáticas a ativos e pastas não se aplicam a eles.

1. Na interface do usuário do [!DNL A]assets, selecione o ativo e clique em **[!UICONTROL Adicionar à coleção]** ![adicionar à coleção](assets/do-not-localize/add-to-collection.png) na barra de ferramentas.
Como alternativa, você pode arrastar o ativo para a área **[!UICONTROL Soltar na coleção]** da interface. Adicione os ativos quando o rótulo da região for alterado para **[!UICONTROL Soltar para Adicionar]**.

1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção à qual deseja adicionar o ativo.

1. Clique em **[!UICONTROL Adicionar]** e feche a mensagem de confirmação. O ativo é adicionado à coleção.

## Editar uma coleção inteligente {#editing-a-smart-collection}

As coleções inteligentes são criadas salvando uma pesquisa para que você possa alterar o conteúdo modificando os parâmetros de pesquisa da [pesquisa salva](#saved-searches).

1. Na interface de usuário do [!DNL Assets], clique na opção de pesquisa ![opção de pesquisa](assets/do-not-localize/search_icon.png) na barra de ferramentas.
1. Com o cursor na caixa Omnisearch, selecione a chave `Return`.
1. Na interface [!DNL Experience Manager], abra o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, selecione a coleção inteligente que deseja modificar. O painel Pesquisar exibe os filtros configurados para a pesquisa salva.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Na lista **[!UICONTROL Arquivos e pastas]**, selecione **[!UICONTROL Arquivos]**.
1. Modifique um ou mais filtros, conforme necessário. Clique em **[!UICONTROL Editar coleção inteligente]**.

   Também é possível editar o nome da coleção inteligente.

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. Clique em **[!UICONTROL Salvar]**. A caixa de diálogo **[!UICONTROL Editar coleção inteligente]** é exibida.
1. Clique em **[!UICONTROL Substituir]** para substituir a coleção inteligente original pela coleção editada. Como alternativa, selecione **[!UICONTROL Salvar como]** para salvar a coleção editada separadamente.
1. Na caixa de diálogo de confirmação, clique em **[!UICONTROL Salvar]** para concluir o processo.

## Exibir e editar metadados da coleção {#view-edit-collection-metadata}

Os metadados da coleção incluem dados sobre a coleção, incluindo tags adicionadas.

1. No console [!UICONTROL Coleções], selecione uma coleção e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página **[!UICONTROL Metadados da coleção]**, visualize os metadados da coleção nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**.
1. Modifique os metadados, conforme necessário. Para salvar as alterações, clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas.

## Editar metadados de várias coleções em massa {#editing-collection-metadata-in-bulk}

É possível editar os metadados de várias coleções simultaneamente. Essa funcionalidade ajuda a replicar rapidamente metadados comuns em várias coleções.

1. No console Coleções, selecione duas ou mais coleções.
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Na página **[!UICONTROL Metadados da coleção]**, edite os metadados nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]**, conforme necessário.
1. Para exibir as propriedades de metadados de uma coleção específica, cancele a seleção das coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página [!UICONTROL Propriedades], é possível remover coleções da lista de coleções cancelando a seleção. A lista de coleções tem todas as coleções selecionadas por padrão. [!DNL Experience Manager] não atualiza os metadados das coleções removidas.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção das coleções e a limpeza da lista.

1. Clique em **[!UICONTROL Salvar e fechar]** na barra de ferramentas e feche a caixa de diálogo de confirmação.
1. Para anexar os novos metadados aos existentes, selecione **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >Os metadados adicionados às coleções selecionadas substituem os metadados anteriores dessas coleções. Use o [!UICONTROL Modo de acréscimo] para adicionar novos valores aos metadados existentes nos campos que podem conter vários valores. Campos de valor único são sempre substituídos. Todas as marcas adicionadas no campo [!UICONTROL Marcas] são anexadas à lista existente de marcas nos metadados.

Para personalizar a página de metadados [!UICONTROL Propriedades], incluindo adição, modificação e exclusão de propriedades de metadados, use o Editor de esquemas.

>[!TIP]
>
>O método de edição em massa funciona para ativos disponíveis em uma coleção. Para os ativos que estão disponíveis em pastas ou correspondem a um critério comum, é possível [atualizar os metadados em massa após a pesquisa](/help/assets/search-assets.md#metadataupdates).

## Pesquisar coleções {#searching-collections}

Você pode pesquisar coleções no console Coleções. Quando você pesquisa com palavras-chave na caixa Omnisearch, o [!DNL Assets] pesquisa por nomes de coleções, metadados e as tags adicionadas às coleções.

Se você pesquisar coleções no nível superior, somente coleções individuais serão retornadas nos resultados da pesquisa. [!DNL Assets] ou pastas dentro das coleções são excluídas. Em todos os outros casos (por exemplo, em uma coleção individual ou em uma hierarquia de pastas), todos os ativos, pastas e coleções relevantes são retornados.

## Pesquisar em coleções {#searching-within-collections}

No console Coleções, clique em uma coleção para abri-la.

Em uma coleção, a pesquisa do [!DNL Experience Manager] está restrita aos ativos (e suas marcas e metadados) dentro da coleção que você está visualizando. Quando você pesquisa em uma pasta, todos os ativos e pastas secundárias correspondentes na pasta atual são retornados. Quando você pesquisa em uma coleção, somente ativos, pastas e outras coleções correspondentes que são membros diretos da coleção são retornados.

## Editar configurações da coleção {#editing-collection-settings}

É possível editar as configurações da coleção, como título e descrição, ou adicionar membros a uma coleção.

1. Selecione uma coleção e clique em **[!UICONTROL Configurações]** na barra de ferramentas. Como alternativa, use a ação rápida **[!UICONTROL Configurações]** da miniatura da coleção.
1. Modifique as configurações da coleção na página **[!UICONTROL Configurações da coleção]**. Por exemplo, modifique o título da coleção, descrições, membros e permissões, conforme discutido em [Adicionando Coleções](#creating-a-collection).

1. Para salvar as alterações, clique em **[!UICONTROL Salvar]**.

## Excluir uma coleção {#deleting-a-collection}

1. No console Coleções, selecione uma ou mais coleções e clique em excluir na barra de ferramentas.

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a ação de exclusão.

   >[!NOTE]
   >
   >Você também pode excluir coleções inteligentes [excluindo pesquisas salvas](#saved-searches).

## Baixar uma coleção {#downloading-a-collection}

Ao baixar uma coleção, toda a hierarquia de ativos dentro dela é baixada, incluindo pastas e coleções secundárias.

1. No console Coleções, selecione uma ou mais coleções para baixar.
1. Na barra de ferramentas, clique em **[!UICONTROL Baixar]**.
1. Na caixa de diálogo **[!UICONTROL Download]**, clique em **[!UICONTROL Download]**. Para baixar as representações dos ativos dentro da coleção, selecione **[!UICONTROL Representações]**. Selecione a opção **[!UICONTROL Email]** para enviar uma notificação por email ao proprietário da coleção.

   Quando você seleciona uma coleção para download, a hierarquia completa de pastas na coleção é baixada. Para incluir cada coleção baixada (incluindo ativos em coleções secundárias aninhadas na coleção principal) em uma pasta individual, selecione **[!UICONTROL Criar pasta separada para cada ativo]**.

## Criar coleções aninhadas {#creating-nested-collections}

Você pode adicionar uma coleção a outra coleção para criar uma coleção aninhada.

1. No console Coleções, selecione a coleção ou o grupo de coleções desejado e clique em **[!UICONTROL Para coleção]** na barra de ferramentas.

1. Na página **[!UICONTROL Adicionar à coleção]**, selecione a coleção na qual adicionar a coleção.

   >[!NOTE]
   >
   >A coleção atualizada mais recentemente é selecionada por padrão na página **[!UICONTROL Adicionar à coleção]**.

1. Clique em **[!UICONTROL Adicionar]**. Uma mensagem confirma que a coleção é adicionada à coleção de destino na página **[!UICONTROL Selecionar destino]**. Feche a mensagem para concluir o processo.

>[!NOTE]
>
>As coleções inteligentes não podem ser aninhadas. Em outras palavras, as coleções inteligentes não podem conter nenhuma outra coleção.

## Pesquisas salvas {#saved-searches}

Na interface de usuário do [!DNL Assets], você pode pesquisar ou filtrar ativos com base em determinadas regras, critérios de pesquisa ou aspectos de pesquisa personalizados. Se salvá-los como **[!UICONTROL Pesquisas salvas]**, você poderá acessá-los posteriormente na lista **[!UICONTROL Pesquisas salvas]** do painel Filtro. Criar uma pesquisa salva também cria uma coleção inteligente.

![lista_de_pesquisas_salvas](assets/saved_searches_list.png)

Pesquisas salvas são criadas quando você cria uma coleção inteligente. As coleções inteligentes são adicionadas automaticamente à lista **[!UICONTROL Pesquisas salvas]**. A consulta [!UICONTROL Pesquisas Salvas] para a coleção está salva na propriedade `dam:query` no CRXDE no local relativo `/content/dam/collections/`. Não há limites para as pesquisas que você pode salvar e nas pesquisas salvas exibidas na lista.

>[!NOTE]
>
>Você pode compartilhar coleções inteligentes da mesma maneira que compartilha coleções estáticas.

Editar pesquisas salvas é o mesmo que editar coleções inteligentes. Para obter detalhes, consulte [editar uma coleção inteligente](#editing-a-smart-collection).

Para excluir pesquisas salvas, siga estas etapas:

1. Na interface de usuário do [!DNL Assets], clique em pesquisar ![opção de pesquisa](assets/do-not-localize/search_icon.png).
1. Com o cursor no campo Omnisearch, selecione a chave `Return`.
1. Na interface [!DNL Experience Manager], abra o painel Filtros.
1. Na lista **[!UICONTROL Pesquisas salvas]**, clique em **[!UICONTROL Excluir]** ao lado da coleção inteligente que deseja excluir.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para excluir a pesquisa salva.

## Executar um fluxo de trabalho em uma coleção {#running-a-workflow-on-a-collection}

Você pode executar um fluxo de trabalho para os ativos em uma coleção. Se a coleção contiver coleções aninhadas, o fluxo de trabalho também será executado nos ativos dentro das coleções aninhadas. No entanto, se a coleção e a coleção aninhada contiverem ativos duplicados, o fluxo de trabalho será executado apenas uma vez para esses ativos.

1. Abra **[!UICONTROL Assets]** > **[!UICONTROL Coleções]**. Para executar um workflow em uma coleção específica, selecione-a.
1. Abra o painel **[!UICONTROL Linha do tempo]**. Clique em ![divisa](assets/do-not-localize/chevron-up-icon.png) e em **[!UICONTROL Iniciar fluxo de trabalho]**.
1. Na seção **[!UICONTROL Iniciar fluxo de trabalho]**, selecione um modelo de fluxo de trabalho da lista. Por exemplo, selecione o modelo **[!UICONTROL Atualizar ativo DAM]**.
1. Insira um título para o fluxo de trabalho e clique em **[!UICONTROL Iniciar]**.
1. Na caixa de diálogo, clique em **[!UICONTROL Continuar]**. O fluxo de trabalho processa todos os ativos na coleção selecionada.

>[!MORELIKETHIS]
>
>* [Configurar notificações por email do Experience Manager Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Criar uma tarefa de revisão para Coleções](bulk-approval.md)
