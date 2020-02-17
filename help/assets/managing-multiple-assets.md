---
title: Gerenciar vários ativos e coleções
description: Saiba como editar os metadados de vários ativos e coleções simultaneamente para propagar rapidamente alterações comuns de metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gerenciar ativos e coleções {#managing-multiple-assets-and-collections}

Os ativos Adobe Enterprise Manager (AEM) permitem que você edite os metadados de vários ativos simultaneamente, para que você possa propagar rapidamente alterações comuns de metadados para ativos em massa. Você também pode editar os metadados de várias coleções em massa.

Use a página de propriedades para executar alterações de metadados em vários ativos ou coleções:

* Alterar propriedades de metadados para um valor comum
* Adicionar ou modificar tags

Para personalizar a página de propriedades de metadados, incluindo adicionar, modificar e excluir propriedades de metadados, use o editor de esquema.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível atualizar [em massa os metadados após a pesquisa](search-assets.md#metadataupdates).

## Editar propriedades de metadados de vários ativos {#editing-metadata-properties-of-multiple-assets}

1. Na interface do usuário Ativos, navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, toque/clique no ícone **[!UICONTROL Propriedades]** para abrir a página de propriedades dos ativos selecionados.

   >[!NOTE]
   >
   >Ao selecionar vários ativos, o formulário pai comum mais baixo é selecionado para os ativos. Em outras palavras, a página de propriedades exibe apenas os campos de metadados que são comuns nas páginas de propriedades de todos os ativos individuais.

1. Modifique as propriedades de metadados para ativos selecionados nas várias guias.
1. Para exibir o editor de metadados de um ativo específico, desmarque os ativos restantes na lista. Os campos do editor de metadados são preenchidos com os metadados do ativo específico.

   >[!NOTE]
   >
   >* Na página de propriedades, é possível remover ativos da lista de ativos desmarcando-os. A lista de ativos tem todos os ativos selecionados por padrão. Os metadados dos ativos que você remove da lista não são atualizados.
   >* Na parte superior da lista de ativos, marque a caixa de seleção perto de **[!UICONTROL Título]** para alternar entre a seleção dos ativos e a limpeza da lista.


1. Para selecionar um esquema de metadados diferente para os ativos, toque/clique no ícone **[!UICONTROL Configurações]** na barra de ferramentas e selecione o esquema desejado.
1. Salve as alterações.
1. Para anexar os novos metadados aos metadados existentes em campos que contêm vários valores, selecione o modo **** Anexar. Se você não selecionar essa opção, os novos metadados substituirão os metadados existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >Para campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o modo **** Anexar.

## Editar propriedades de metadados de várias coleções {#editing-metadata-properties-of-multiple-collections}

1. No console Coleções, selecione as coleções que deseja editar.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Propriedades]** para abrir a página de propriedades das coleções selecionadas.
1. Modifique as propriedades de metadados para coleções selecionadas nas várias guias.

   >[!NOTE]
   >
   >Os metadados adicionados para as coleções selecionadas substituem os metadados anteriores para essas coleções, exceto as tags. Quaisquer tags adicionadas no campo **[!UICONTROL Tags]** serão anexadas à lista existente de tags nos metadados.

1. Para exibir as propriedades de metadados de uma coleção específica, desmarque as coleções restantes na lista de coleções. Os campos do editor de metadados são preenchidos com os metadados da coleção específica.

   >[!NOTE]
   >
   >* Na página de propriedades da coleção, é possível remover coleções da lista de coleções desmarcando-as. A lista de coleções tem todas as coleções selecionadas por padrão. Os metadados das coleções que você remover não são atualizados.
   >* Na parte superior da lista, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção das coleções e a limpeza da lista.


1. Salve as alterações.

## Configurar limite para atualização de metadados em massa {#configlimit}

Para evitar uma situação semelhante ao DOS, o AEM limita o número de parâmetros suportados em uma solicitação Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O AEM gera o seguinte aviso nos registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para alterar o limite, acesse o Console da Web ( **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web) e altere o valor de Parâmetros **[!UICONTROL de POST]** Máximo na configuração **[!UICONTROL do OSGi de Tratamento]** de Parâmetro de Solicitação Sling do Apache.
