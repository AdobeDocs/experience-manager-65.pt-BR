---
title: Gerencie metadados de seus ativos digitais no [!DNL Adobe Experience Manager].
description: Saiba mais sobre os tipos de metadados e [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] como tornar possível organizar e processar ativos automaticamente com base em seus metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d070f5dca569dfb90d3034b74c2940fd68d8ceab
workflow-type: tm+mt
source-wordcount: '2421'
ht-degree: 11%

---


# Gerenciar metadados de seus ativos digitais {#managing-metadata-for-digital-assets}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Permite a categorização e organização mais fáceis de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para [!DNL Experience Manager Assets], o gerenciamento de metadados se integra ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar automaticamente ativos com base em seus metadados.

## Metadados e sua origem {#how-to-edit-or-add-metadata}

Metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ele é adicionado aos ativos e [!DNL Experience Manager] é processado quando você carrega um ativo. É possível editar os metadados existentes, adicionar novas propriedades de metadados aos campos existentes. As organizações precisam de vocabulários de metadados controlados e confiáveis. Portanto, não [!DNL Experience Manager Assets] permite a adição sob demanda de novas propriedades de metadados. Somente administradores e desenvolvedores podem adicionar novas propriedades ou campos que contêm metadados. Os usuários podem preencher os campos existentes com metadados.

Os seguintes métodos podem ser usados para adicionar metadados a ativos digitais:

* Para começar, os aplicativos nativos que criam ativos adicionam alguns metadados a ele. Por exemplo, a [Acrobat adiciona alguns metadados](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) a arquivos PDF ou uma câmera adiciona alguns metadados básicos às fotografias. Ao gerar ativos, você pode adicionar os metadados nos próprios aplicativos nativos. Por exemplo, você pode [adicionar metadados IPTC no Adobe Lightroom](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* Antes de fazer upload de um ativo para [!DNL Experience Manager], você pode editar e modificar metadados usando o aplicativo nativo usado para criar um ativo ou usando outro aplicativo de edição de metadados. Quando você carrega um ativo no Experience Manager, os metadados são processados. Por exemplo, consulte como [trabalhar com metadados em [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) e ver o painel de [tags para [!DNL Bridge CC]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) em [!DNL Adobe Exchange].

* Em [!DNL Experience Manager Assets], você pode adicionar ou editar manualmente metadados de ativos na página [!UICONTROL Propriedades] .

* Você pode aproveitar a funcionalidade de perfis [de](/help/assets/metadata-config.md#metadata-profiles) metadados [!DNL Experience Manager Assets] para adicionar metadados automaticamente quando os ativos forem carregados no DAM.

## Adicionar ou editar metadados em [!DNL Experience Manager Assets] {#add-edit-metadata}

Para editar os metadados de um ativo na interface do [!DNL Assets] usuário, siga estas etapas:

1. Faça uma das seguintes opções:

   * Na [!DNL Assets] interface, selecione o ativo e clique em Propriedades **[!UICONTROL da]** Visualização na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida Propriedades **[!UICONTROL da]** Visualização.
   * Na página do ativo, clique no ícone **[!UICONTROL de informações Propriedades]** da ![Visualização](assets/do-not-localize/info-circle-icon.png) Ativos na barra de ferramentas.

   A página do ativo exibe todos os metadados do ativo. Os metadados são extraídos quando o ativo é carregado (assimilado) no [!DNL Experience Manager].

   ![Selecione Propriedades de um ativo para visualização de seus metadados](assets/asset-metadata.png)

   *Figura: Edite ou adicione metadados na página [!UICONTROL Propriedades] do ativo.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há metadados definidos. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas de volta no binário original como parte de seus dados XMP. O fluxo de trabalho de gravação de metadados adiciona os metadados ao binário original. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e novas propriedades (incluindo propriedades personalizadas como `cq:tags`) são adicionadas ao schema.

XMP gravação é suportada e ativada para plataformas e formatos de arquivos descritos nos requisitos [técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar propriedades de metadados de vários ativos {#editing-metadata-properties-of-multiple-assets}

[!DNL Adobe Enterprise Manager Assets] permite que você edite os metadados de vários ativos simultaneamente para que possa propagar rapidamente alterações comuns de metadados para ativos em massa. Você também pode editar os metadados de várias coleções em massa. Use a página de propriedades para executar alterações de metadados em vários ativos ou coleções:

* Alterar propriedades de metadados para um valor comum
* Adicionar ou modificar tags

Para personalizar a página de propriedades de metadados, incluindo adicionar, modificar e excluir propriedades de metadados, use o editor [de](metadata-config.md#folder-metadata-schema)schemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível atualizar [em massa os metadados após a pesquisa](search-assets.md#metadataupdates).

1. Na interface do [!DNL Assets] usuário, navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]** para abrir a página de propriedades dos ativos selecionados.

   >[!NOTE]
   >
   >Quando você seleciona vários ativos, o formulário pai comum mais baixo é selecionado para os ativos. Em outras palavras, a página de propriedades exibe apenas os campos de metadados que são comuns nas páginas de propriedades de todos os ativos individuais.

1. Modifique as propriedades de metadados para ativos selecionados nas várias guias.
1. Para visualização do editor de metadados para um ativo específico, desmarque os ativos restantes na lista. Os campos do editor de metadados são preenchidos com os metadados do ativo específico.

   >[!NOTE]
   >
   >* Na página de propriedades, é possível remover ativos da lista de ativos desmarcando-os. A lista do ativo tem todos os ativos selecionados por padrão. Os metadados dos ativos que você remove da lista não são atualizados.
   >* Na parte superior da lista de ativos, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção dos ativos e a limpeza da lista.


1. Para selecionar um schema de metadados diferente para os ativos, clique em **[!UICONTROL Configurações]** na barra de ferramentas e selecione o schema desejado.
1. Salve as alterações.
1. Para anexar os novos metadados aos existentes em campos que contêm vários valores, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Clique em **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >Em campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Importar metadados {#import-metadata}

[!DNL Assets] permite importar metadados de ativos em massa usando um arquivo CSV. É possível fazer atualizações em massa para os ativos carregados recentemente ou os ativos existentes importando um arquivo CSV. Você também pode assimilar metadados de ativos em massa de sistemas de terceiros em formato CSV.

A importação de metadados é assíncrona e não impede o desempenho do sistema. A atualização simultânea dos metadados para vários ativos pode exigir muitos recursos devido à atividade de gravação XMP caso o sinalizador de fluxo de trabalho esteja marcado. Planeje tal importação durante o uso de servidor simplificado para que o desempenho para outros usuários não seja afetado.

>[!NOTE]
>
>Para importar metadados em namespaces personalizadas, registre primeiro as namespaces.

1. Navegue até a interface do [!DNL Assets] usuário e clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. No menu, selecione **[!UICONTROL Metadados]**.
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. Selecione o arquivo CSV com os metadados.
1. Especifique os seguintes parâmetros. Consulte um arquivo CSV de amostra em [metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv).

   | Parâmetros de importação de metadados | Descrição |
   |:---|:---|
   | [!UICONTROL Tamanho do lote] | Número de ativos em um lote para os quais os metadados devem ser importados. O valor padrão é 50. O valor máximo é 100. |
   | [!UICONTROL Separador de campos] | O valor padrão é `,` (uma vírgula). É possível especificar qualquer outro caractere. |
   | [!UICONTROL Delimitador de múltiplo valor] | Separador para valores de metadados. O valor padrão é `|`. |
   | [!UICONTROL Inicializar fluxos de trabalho] | False por padrão. Quando definidas como `true` e as configurações padrão do Iniciador estiverem em vigor para o fluxo de trabalho WriteBack [!UICONTROL de metadados] DAM (que grava metadados nos dados binários XMP). Habilitar workflows de inicialização retarda o sistema. |
   | [!UICONTROL Nome de coluna do caminho do ativo] | Define o nome da coluna para o arquivo CSV com ativos. |

1. Click **[!UICONTROL Import]** from the toolbar. Depois que os metadados são importados, uma notificação é exibida na caixa de entrada [!UICONTROL Notificação] .

1. Para verificar a importação correta, navegue até a página [!UICONTROL Propriedades] de um ativo e verifique os valores nos campos.

Para adicionar data e carimbo de data e hora ao importar metadados, use o `YYYY-MM-DDThh:mm:ss.fff-00:00` formato para data e hora. A data e a hora são separadas por `T`, `hh` é horas no formato de 24 horas, `fff` é nanossegundos e `-00:00` é deslocamento de fuso horário. Por exemplo, `2020-03-26T11:26:00.000-07:00` é 26 de março de 2020 às 11:26:00.000 da hora PST.

>[!CAUTION]
>
>Se o formato de data não corresponder `YYYY-MM-DDThh:mm:ss.fff-00:00`, os valores de data não serão definidos. Os formatos de data do arquivo CSV de metadados exportados estão no formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desejar importá-lo, converta-o no formato aceitável adicionando o valor de nanossegundos indicado por `fff`.

## Export metadata {#export-metadata}

É possível exportar metadados para vários ativos em um formato CSV. Os metadados são exportados de forma assíncrona e não afetam o desempenho do sistema. Para exportar metadados, [!DNL Experience Manager] percorre as propriedades do nó do ativo `jcr:content/metadata` e seus nós filhos e exporta as propriedades de metadados em um arquivo CSV.

Alguns casos de uso para exportar metadados em massa são:

* Importe os metadados em um sistema de terceiros ao migrar ativos.
* Compartilhe metadados de ativos com uma equipe de projeto mais ampla.
* Teste ou audite os metadados para verificar a conformidade.
* Externalize os metadados para localizá-los separadamente.

1. Selecione a pasta de ativos que contém os ativos para os quais deseja exportar metadados. Na barra de ferramentas, selecione **[!UICONTROL Exportar metadados]**.

1. Na caixa de diálogo Exportação [!UICONTROL de] metadados, especifique um nome para o arquivo CSV. Para exportar metadados para ativos em subpastas, selecione **[!UICONTROL Incluir ativos em subpastas]**.

   ![Interface e opções para exportar metadados de todos os ativos em uma](assets/export_metadata_page.png "folderInterface e opções para exportar metadados de todos os ativos em uma pasta")

1. Selecione as opções desejadas. Forneça um nome de arquivo e, se necessário, uma data.

1. No campo **[!UICONTROL Propriedades a serem exportadas]** , especifique se deseja exportar todas as propriedades ou propriedades específicas. Se você escolher Propriedades seletivas a serem exportadas, adicione as propriedades desejadas.

1. Na barra de ferramentas, clique em **[!UICONTROL Exportar]**. Uma mensagem confirma que os metadados são exportados. Feche a mensagem.

1. Abra a notificação da caixa de entrada do trabalho de exportação. Selecione o trabalho e clique em **[!UICONTROL Abrir]** na barra de ferramentas. To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. Clique em **[!UICONTROL Fechar]**.

   ![Caixa de diálogo para baixar o arquivo CSV que contém os metadados exportados em massa](assets/csv_download.png)

   *Figura: Caixa de diálogo para baixar o arquivo CSV que contém os metadados exportados em massa.*

## Editar metadados de coleções {#collections-metadata}

Para obter detalhes, consulte [visualização e edição de metadados](/help/assets/manage-collections.md#view-edit-collection-metadata) de coleção e [edição de metadados de várias coleções em massa](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk).

## Aplicar um perfil de metadados a pastas {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

Quando você atribui um perfil de metadados a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta pai. Isso significa que você pode atribuir apenas um perfil de metadados a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você carrega, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de metadados diferente a uma pasta, o novo perfil substituirá o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos adicionados posteriormente à pasta.

As pastas que têm um perfil atribuído a ele são indicadas na interface do usuário pelo nome do perfil que aparece no nome do cartão.

![A visualização do cartão exibe o perfil de metadados aplicado a uma pasta](assets/metadata-profile-card-view-display.png)

Você pode aplicar perfis de metadados a pastas específicas ou globalmente a todos os ativos.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

Aplique um perfil de metadados a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de metadados a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você tenha alterado posteriormente. Consulte o [reprocessando de ativos em uma pasta após a edição do perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de metadados a pastas da interface do usuário de [!UICONTROL Perfis] {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Siga as etapas para aplicar o perfil de metadados:

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selecione o perfil de metadados que deseja aplicar a uma pasta ou várias pastas.
1. Click **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and click **[!UICONTROL Done]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

### Aplicar perfis de metadados a pastas de [!UICONTROL Propriedades] {#applying-metadata-profiles-to-folders-from-properties}

1. No painel esquerdo, clique em **[!UICONTROL Ativos]** e navegue até a pasta à qual deseja aplicar um perfil de metadados.
1. Na pasta, clique na marca de seleção para selecioná-la e clique em **[!UICONTROL Propriedades]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the popup menu and click **[!UICONTROL Save]**.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### Remover um perfil de metadados das pastas {#removing-a-metadata-profile-from-folders}

Quando você remove um perfil de metadados de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta pai. No entanto, qualquer processamento de arquivos que tenha ocorrido dentro das pastas permanece intacto.

Você pode remover um perfil de metadados de uma pasta do menu **[!UICONTROL Ferramentas]** ou das **[!UICONTROL Propriedades]** de dentro da pasta.

#### Remover perfis de metadados de pastas por meio da interface do usuário de Perfis {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Click the [!DNL Experience Manager] logo and navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]**.
1. Selecione o perfil de metadados que deseja remover de uma pasta ou de várias pastas.
1. Click **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from and click **[!UICONTROL Done]**.

   Você pode confirmar que o perfil de metadados não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

#### Remover perfis de metadados de pastas por Propriedades {#removing-metadata-profiles-from-folders-via-properties}

1. Clique no [!DNL Experience Manager] logotipo, navegue pelos **[!UICONTROL Ativos]** e, em seguida, até a pasta da qual deseja remover um perfil de metadados.
1. Na pasta, clique na marca de seleção para selecioná-la e clique em **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

## Dicas e limitações {#best-practices-limitations}

* As atualizações de metadados por meio da interface do usuário alteram as propriedades de metadados na `dc` namespace. Qualquer atualização feita por meio da API HTTP altera as propriedades de metadados na `jcr` namespace. Consulte [como atualizar metadados usando a API](/help/assets/mac-api-assets.md#update-asset-metadata)HTTP.

* O arquivo CSV para importar metadados de ativos está em um formato muito específico. Para economizar esforço e tempo e evitar erros não intencionais, você pode start na criação do CSV usando o formato de um arquivo CSV exportado.

* Ao importar metadados usando um arquivo CSV, o formato de data necessário é `YYYY-MM-DDThh:mm:ss.fff-00:00`. Se qualquer outro formato for usado, os valores de data não serão definidos. Os formatos de data do arquivo CSV de metadados exportados estão no formato `YYYY-MM-DDThh:mm:ss-00:00`. Se desejar importá-lo, converta-o no formato aceitável adicionando o valor de nanossegundos indicado por `fff`.

>[!MORELIKETHIS]
>
>* [Conceitos de metadados e compreensão](metadata-concepts.md).
>* [Editar propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk)
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)


<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, etc. metadata-related help articles.

* Link to XMP writeback.

* Manually add (or edit) metadata in AEM in Properties page.

* Metadata profiles

* Any workflows related to metadata?

* Advanced topic: Add, edit, modify, process and writeback metadata of subassets.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

Similarities and differences between metadata of asset and folder. 

Link to metadata handling of collections.

## Modify metadata of an asset, folder, or collection {#modify-metadata}

* While creating assets: Native application.

* Before ingesting assets: Metadata editors

* After ingesting assets: Properties of an asset, folder, collection, etc.

* Any supported programmatic method to bulk edit metadata directly in JCR?

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value

* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the Properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

-->
