---
title: Gerencie metadados de seus ativos digitais
description: Saiba mais sobre os tipos de metadados e como gerenciar metadados para ativos a fim de organizá-los e processá-los facilmente.
contentOwner: AG
mini-toc-levels: 1
feature: Tagging, Metadata
role: Architect, Leader
exl-id: c630709a-7e8b-417c-83a4-35ca9be832a0
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2332'
ht-degree: 10%

---

# Gerencie metadados de seus ativos digitais {#managing-metadata-for-digital-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-metadata.html?lang=en) |
| AEM 6.5 | Este artigo |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ele facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para o [!DNL Experience Manager Assets], o gerenciamento de metadados integra-se ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base nos metadados.

## Metadados e sua origem {#how-to-edit-or-add-metadata}

Os metadados são informações adicionais sobre o ativo que pode ser pesquisado. Ele é adicionado aos ativos e em [!DNL Experience Manager] é processado quando você carrega um ativo. É possível editar os metadados existentes, adicionar novas propriedades de metadados a campos existentes. As organizações precisam de vocabulários de metadados controlados e confiáveis. Portanto, [!DNL Experience Manager Assets] não permite a adição sob demanda de novas propriedades de metadados. Somente administradores e desenvolvedores podem adicionar novas propriedades ou campos que contenham metadados. Os usuários podem preencher os campos existentes com metadados.

Os métodos a seguir podem ser usados para adicionar metadados a ativos digitais:

* Para começar, os aplicativos nativos que criam ativos adicionam alguns metadados a eles. Por exemplo, o [Acrobat adiciona alguns metadados](https://helpx.adobe.com/acrobat/using/pdf-properties-metadata.html) a arquivos PDF ou uma câmera adiciona alguns metadados básicos às fotografias. Ao gerar ativos, você pode adicionar os metadados nos próprios aplicativos nativos. Por exemplo, você pode [adicionar metadados IPTC no Adobe Lightroom](https://helpx.adobe.com/lightroom-classic/help/metadata-basics-actions.html).

* Antes de carregar um ativo para [!DNL Experience Manager], você pode editar e modificar metadados usando o aplicativo nativo usado para criar um ativo ou usando algum outro aplicativo de edição de metadados. Ao fazer upload de um ativo para o Experience Manager, os metadados são processados. Por exemplo, veja como [trabalhar com metadados [!DNL Adobe Bridge]](https://helpx.adobe.com/bridge/user-guide.html/bridge/using/metadata-adobe-bridge.ug.html) e o painel [tags [!DNL Adobe Bridge]](https://exchange.adobe.com/creativecloud.details.20009.aem-tags-panel-for-bridge-cc.html) em [!DNL Adobe Exchange].

* Em [!DNL Experience Manager Assets], você pode adicionar ou editar manualmente metadados de ativos na página [!UICONTROL Propriedades].

* Você pode usar a funcionalidade [perfis de metadados](/help/assets/metadata-config.md#metadata-profiles) do [!DNL Experience Manager Assets] para adicionar metadados automaticamente quando os ativos forem carregados no DAM.

## Adicionar ou editar metadados em [!DNL Experience Manager Assets] {#add-edit-metadata}

Para editar os metadados de um ativo na interface do usuário do [!DNL Assets], siga estas etapas:

1. Siga uma das seguintes opções:

   * Na interface [!DNL Assets], selecione o ativo e clique em **[!UICONTROL Exibir Propriedades]** na barra de ferramentas.
   * Na miniatura do ativo, selecione a ação rápida **[!UICONTROL Exibir propriedades]**.
   * Na página do ativo, clique em **[!UICONTROL Exibir propriedades]** ![ícone de informações do Assets](assets/do-not-localize/info-circle-icon.png) na barra de ferramentas.

   A página do ativo exibe todos os metadados do ativo. Os metadados são extraídos quando o ativo é carregado (assimilado) no [!DNL Experience Manager].

   ![Selecione as Propriedades de um ativo para exibir seus metadados](assets/asset-metadata.png)

   *Figura: editar ou adicionar metadados na página [!UICONTROL Propriedades] do ativo.*

1. Faça edições nos metadados em várias guias, conforme necessário, e quando concluído, clique em **[!UICONTROL Salvar]** na barra de ferramentas para salvar suas alterações. Clique em **[!UICONTROL Fechar]** para retornar à interface da Web do [!DNL Assets].

   >[!NOTE]
   >
   >Se um campo de texto estiver vazio, não há conjunto de metadados existente. Você pode inserir um valor no campo e salvá-lo para adicionar essa propriedade de metadados.

Quaisquer alterações nos metadados de um ativo são gravadas no binário original como parte de seus dados de XMP. O fluxo de trabalho de gravação de metadados adiciona os metadados ao binário original. As alterações feitas nas propriedades existentes (como `dc:title`) são substituídas e novas propriedades (incluindo propriedades personalizadas como `cq:tags`) são adicionadas com o esquema.

O write-back de XMP é suportado e habilitado para as plataformas e formatos de arquivo descritos nos [requisitos técnicos.](/help/sites-deploying/technical-requirements.md)

## Editar propriedades de metadados de vários ativos {#editing-metadata-properties-of-multiple-assets}

O [!DNL Adobe Enterprise Manager Assets] permite editar os metadados de vários ativos simultaneamente para que você possa propagar rapidamente alterações comuns em metadados para ativos em massa. Também é possível editar os metadados de várias coleções em massa. Use a página de propriedades para executar alterações de metadados em vários ativos ou coleções:

* Alterar propriedades de metadados para um valor comum
* Adicionar ou modificar tags

Para personalizar a página de propriedades de metadados, incluindo adição, modificação e exclusão de propriedades de metadados, use o [editor de esquemas](metadata-config.md#folder-metadata-schema).

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou correspondem a um critério comum, é possível [atualizar os metadados em massa após a pesquisa](search-assets.md#metadataupdates).

1. Na interface do usuário do [!DNL Assets], navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]** para abrir a página de propriedades dos ativos selecionados.
1. Modifique as propriedades de metadados dos ativos selecionados nas várias guias.
1. Para exibir os metadados de um ativo específico, cancele a seleção dos ativos restantes na lista. Se você cancelar a seleção de alguns ativos na página [!UICONTROL Propriedades], os metadados desses ativos não serão atualizados.
1. Para selecionar um esquema de metadados diferente para os ativos, clique em **[!UICONTROL Configurações]** na barra de ferramentas e selecione um esquema. Clique em **[!UICONTROL Salvar e fechar]**.
1. Para anexar os novos metadados aos existentes em campos que contêm vários valores, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Clique em **[!UICONTROL Enviar]**.

![O esquema de metadados se aplica em massa a vários ativos](assets/metadata-schema-bulk-edit.gif)

>[!CAUTION]
>
>Em campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Importar metadados {#import-metadata}

O [!DNL Assets] permite importar metadados de ativos em massa usando um arquivo CSV. Você pode fazer atualizações em massa para os ativos carregados recentemente ou os ativos existentes importando um arquivo CSV. Você também pode assimilar metadados de ativos em massa de sistemas de terceiros no formato CSV.

A importação de metadados é assíncrona e não impede o desempenho do sistema. A atualização simultânea dos metadados de vários ativos pode consumir muitos recursos devido à atividade de writeback XMP se o sinalizador de fluxo de trabalho estiver marcado. Planejar essa importação durante o uso do servidor enxuto para que o desempenho de outros usuários não seja afetado.

>[!NOTE]
>
>Para importar metadados em namespaces personalizados, primeiro registre os namespaces.

1. Navegue até a interface de usuário [!DNL Assets] e clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. No menu, selecione **[!UICONTROL Metadados]**.
1. Na página **[!UICONTROL Importação de metadados]**, clique em **[!UICONTROL Selecionar arquivo]**. Selecione o arquivo CSV com os metadados.
1. Especifique os parâmetros a seguir. Consulte um arquivo CSV de exemplo em [metadata-import-sample-file.csv](/help/assets/assets/metadata-import-sample-file.csv).

   | Parâmetros de importação de metadados | Descrição |
   |:---|:---|
   | [!UICONTROL Tamanho do Lote] | Número de ativos em um lote para o qual os metadados devem ser importados. O valor padrão é 50. O valor máximo é 100. |
   | [!UICONTROL Separador de campos] | O valor padrão é `,` (uma vírgula). Você pode especificar qualquer outro caractere. |
   | [!UICONTROL Delimitador de vários valores] | Separador para valores de metadados. O valor padrão é `|`. |
   | [!UICONTROL Iniciar Fluxos de Trabalho] | Falso por padrão. Quando definido como `true` e as configurações padrão estão em vigor para o fluxo de trabalho [!UICONTROL WriteBack de Metadados do DAM] (que grava metadados nos dados binários do XMP). Habilitar os fluxos de trabalho torna o sistema lento. |
   | [!UICONTROL Nome da coluna do caminho do ativo] | Define o nome da coluna do arquivo CSV com ativos. |

1. Clique em **[!UICONTROL Importar]** na barra de ferramentas. Após a importação dos metadados, uma notificação é exibida na caixa de entrada [!UICONTROL Notificação].

1. Para verificar se a importação foi feita corretamente, navegue até a página [!UICONTROL Propriedades] de um ativo e verifique os valores nos campos.

Para adicionar data e carimbo de data e hora ao importar metadados, use o formato `YYYY-MM-DDThh:mm:ss.fff-00:00` para data e hora. A data e a hora são separadas por `T`, `hh` são horas no formato de 24 horas, `fff` são nanossegundos e `-00:00` é deslocamento de fuso horário. Por exemplo, `2020-03-26T11:26:00.000-07:00` é 26 de março de 2020 às 11:26:00.000 hora PST.

>[!CAUTION]
>
>Se o formato de data não corresponder a `YYYY-MM-DDThh:mm:ss.fff-00:00`, os valores de data não serão definidos. Os formatos de data do arquivo CSV de metadados exportado estão no formato `YYYY-MM-DDThh:mm:ss-00:00`. Se quiser importá-lo, converta-o para o formato aceitável adicionando o valor de nanossegundos denotado por `fff`.

## Exportar metadados {#export-metadata}

É possível exportar metadados de vários ativos em um formato CSV. Os metadados são exportados de forma assíncrona e não afetam o desempenho do sistema. Para exportar metadados, [!DNL Experience Manager] percorre as propriedades do nó do ativo `jcr:content/metadata` e seus nós filhos e exporta as propriedades dos metadados em um arquivo CSV.

Alguns casos de uso para exportar metadados em massa são:

* Importe os metadados em um sistema de terceiros ao migrar ativos.
* Compartilhar metadados de ativos com uma equipe de projeto maior.
* Testar ou auditar os metadados quanto à conformidade.
* Externalize os metadados para localizá-los separadamente.

1. Selecione a pasta de ativos que contém ativos para os quais deseja exportar metadados. Na barra de ferramentas, selecione **[!UICONTROL Exportar metadados]**.

1. Na caixa de diálogo [!UICONTROL Exportação de metadados], especifique um nome para o arquivo CSV. Para exportar metadados de ativos em subpastas, selecione **[!UICONTROL Incluir ativos em subpastas]**.

   ![Interface e opções para exportar metadados de todos os ativos em uma pasta](assets/export_metadata_page.png "Interface e opções para exportar metadados de todos os ativos em uma pasta")

1. Selecione as opções desejadas. Forneça um nome de arquivo e se necessário uma data.

1. No campo **[!UICONTROL Propriedades a serem exportadas]**, especifique se deseja exportar todas as propriedades ou propriedades específicas. Se você escolher Propriedades seletivas para serem exportadas, adicione as propriedades desejadas.

1. Na barra de ferramentas, clique em **[!UICONTROL Exportar]**. Uma mensagem confirma que os metadados foram exportados. Feche a mensagem.

1. Abra a notificação da caixa de entrada do trabalho de exportação. Selecione o trabalho e clique em **[!UICONTROL Abrir]** na barra de ferramentas. Para baixar o arquivo CSV com os metadados, clique em **[!UICONTROL Download de CSV]** na barra de ferramentas. Clique em **[!UICONTROL Fechar]**.

   ![Caixa de diálogo para baixar o arquivo CSV contendo metadados exportados em massa](assets/csv_download.png)

   *Figura: caixa de diálogo para baixar o arquivo CSV contendo metadados exportados em massa.*

## Editar metadados de coleções {#collections-metadata}

Para obter detalhes, consulte [exibir e editar metadados da coleção](/help/assets/manage-collections.md#view-edit-collection-metadata) e [editar metadados de várias coleções em massa](/help/assets/manage-collections.md#editing-collection-metadata-in-bulk).

## Aplicar um perfil de metadados a pastas {#applying-a-metadata-profile-to-folders}

<!-- TBD: Review this overview.
-->

Ao atribuir um perfil de metadados a uma pasta, qualquer subpasta herda automaticamente o perfil da pasta principal. Isso significa que só é possível atribuir um perfil de metadados a uma pasta. Dessa forma, considere cuidadosamente a estrutura de pastas de onde você faz upload, armazena, usa e arquiva ativos.

Se você atribuiu um perfil de metadados diferente a uma pasta, o novo perfil substitui o perfil anterior. Os ativos de pasta existentes anteriormente permanecem inalterados. O novo perfil é aplicado aos ativos que são adicionados à pasta posteriormente.

As pastas que têm um perfil atribuído a elas são indicadas na interface pelo nome do perfil que aparece no nome do cartão.

![A exibição de cartão exibe o perfil de metadados aplicado a uma pasta](assets/metadata-profile-card-view-display.png)

Aplique perfis de metadados a pastas específicas ou globalmente a todos os ativos.

É possível reprocessar ativos em uma pasta que já tenha um perfil de metadados existente que você alterou posteriormente. Consulte [Reprocessando ativos em uma pasta após editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

Aplique um perfil de metadados a uma pasta no menu **[!UICONTROL Ferramentas]** ou, se estiver na pasta, em **[!UICONTROL Propriedades]**. Esta seção descreve como aplicar perfis de metadados a pastas de ambas as maneiras.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

Você pode reprocessar ativos em uma pasta que já tenha um perfil de vídeo existente que você alterou posteriormente. Consulte [Reprocessando ativos em uma pasta após editar seu perfil de processamento](processing-profiles.md#reprocessing-assets).

### Aplicar perfis de metadados a pastas da interface do usuário [!UICONTROL Perfis] {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Siga as etapas para aplicar o perfil de metadados:

1. Clique no logotipo [!DNL Experience Manager] e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]**.
1. Selecione o perfil de metadados que deseja aplicar a uma ou várias pastas.
1. Clique em **[!UICONTROL Aplicar perfil de metadados às pastas]**, selecione uma ou várias pastas que deseja usar para receber os ativos carregados recentemente e clique em **[!UICONTROL Concluído]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

### Aplicar perfis de metadados a pastas de [!UICONTROL Propriedades] {#applying-metadata-profiles-to-folders-from-properties}

1. No painel à esquerda, clique em **[!UICONTROL Assets]** e navegue até a pasta à qual deseja aplicar um perfil de metadados.
1. Na pasta, clique na marca de seleção para selecioná-la e clique em **[!UICONTROL Propriedades]**.

1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione o perfil no menu pop-up e clique em **[!UICONTROL Salvar]**.

As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

<!-- TBD: Commenting as the topic in metadata-config.md is incomplete.

### Apply metadata profile globally {#metadata-profile-global}

For details, see [configuration to apply metadata profile globally](/help/assets/metadata-config.md#apply-a-metadata-profile-globally). -->

### Remover um perfil de metadados das pastas {#removing-a-metadata-profile-from-folders}

Ao remover um perfil de metadados de uma pasta, qualquer subpasta herda automaticamente a remoção do perfil da pasta principal. No entanto, qualquer processamento de arquivos que tenha ocorrido nas pastas permanece intacto.

Você pode remover um perfil de metadados de uma pasta no menu **[!UICONTROL Ferramentas]** ou nas **[!UICONTROL Propriedades]** da pasta.

#### Remover perfis de metadados de pastas por meio da interface do usuário Perfis {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Clique no logotipo [!DNL Experience Manager] e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Metadados]**.
1. Selecione o perfil de metadados que deseja remover de uma ou várias pastas.
1. Clique em **[!UICONTROL Remover perfil de metadados das pastas]**, selecione uma ou várias pastas que deseja usar para remover um perfil e clique em **[!UICONTROL Concluído]**.

   É possível confirmar que o perfil de metadados não é mais aplicado a uma pasta porque o nome não aparece mais abaixo do nome da pasta.

#### Remover perfis de metadados de pastas por meio de Propriedades {#removing-metadata-profiles-from-folders-via-properties}

1. Clique no logotipo [!DNL Experience Manager], navegue até **[!UICONTROL Assets]** e, em seguida, acesse a pasta da qual deseja remover um perfil de metadados.
1. Na pasta, clique na marca de seleção para selecioná-la e clique em **[!UICONTROL Propriedades]**.
1. Selecione a guia **[!UICONTROL Perfis de metadados]**, selecione **[!UICONTROL Nenhum]** no menu suspenso e clique em **[!UICONTROL Salvar]**. As pastas que têm um perfil já atribuído a elas são indicadas ao exibir do nome do perfil logo abaixo do nome da pasta.

## Dicas e limitações {#best-practices-limitations}

* As atualizações de metadados via interface do usuário alteram as propriedades de metadados no namespace `dc`. Qualquer atualização feita por meio da API HTTP altera as propriedades de metadados no namespace `jcr`. Consulte [como atualizar metadados usando a API HTTP](/help/assets/mac-api-assets.md#update-asset-metadata).

* O arquivo CSV para importar metadados de ativos está em um formato muito específico. Para economizar esforço e tempo e evitar erros não intencionais, você pode começar a criar o CSV usando o formato de um arquivo CSV exportado.

* Ao importar metadados usando um arquivo CSV, o formato de data necessário é `YYYY-MM-DDThh:mm:ss.fff-00:00`. Se qualquer outro formato for usado, os valores de data não serão definidos. Os formatos de data do arquivo CSV de metadados exportado estão no formato `YYYY-MM-DDThh:mm:ss-00:00`. Se quiser importá-lo, converta-o para o formato aceitável adicionando o valor de nanossegundos denotado por `fff`.

>[!MORELIKETHIS]
>
>* [Conceitos e noções básicas sobre metadados](metadata-concepts.md).
>* [Editar propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk)
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

<!-- TBD: Try filling the available information in these topics to the extent possible. As and when complete, publish the sections live.

## Where to find metadata of an asset or folder {#find-metadata}

What all methods to access asset Properties. More Details option in column view. Select asset and click Properties. Keyboard shortcut `p`. What else?

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

* To begin with, assets come with some metadata. The applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some other metadata editing application. When you upload an asset to Experience Manager, the metadata is processed.

* Link to PS, ID, AI, PDF, and so on, metadata-related help articles.

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

* After ingesting assets: Properties of an asset, folder, collection, and so on.

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
