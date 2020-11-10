---
title: Configuração e administração da funcionalidade de metadados.
description: Configuração e administração [!DNL Experience Manager Assets] da funcionalidade relacionada à adição e gerenciamento de metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 5%

---


# Configuração e administração da funcionalidade de metadados em [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Permite a categorização e organização mais fáceis de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar automaticamente ativos com base em seus metadados. [!DNL Adobe Experience Manager Assets] permite que os administradores configurem e personalizem a funcionalidade de metadados para modificar a oferta de Adobe padrão.

## Editar schema de metadados {#metadata-schema}

Para obter detalhes, consulte [editar formulários](metadata-schemas.md#edit-metadata-schema-forms)de schema de metadados.

## Registrar uma namespace personalizada em [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Você pode adicionar suas próprias namespaces dentro [!DNL Experience Manager]. Assim como há namespaces predefinidas, como `cq`, `jcr`e `sling`, você pode ter uma namespace para os metadados do repositório e o processamento XML.

1. Acesse a página de administração do tipo de nó `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acessar a página de administração de namespaces, clique em **[!UICONTROL Namespaces]** na parte superior da página.
1. Para adicionar uma namespace, clique em **[!UICONTROL Novo]** na parte inferior da página.
1. Especifique uma namespace personalizada na convenção de namespace XML. Especifique a ID na forma de um URI e um prefixo associado para a ID. Clique em **[!UICONTROL Salvar]**.

## Configurar limites para atualização de metadados em massa {#bulk-metadata-update-limit}

Para evitar uma situação semelhante a DOS (negação de serviço), [!DNL Enterprise Manager] limita o número de parâmetros suportados em uma solicitação Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O Enterprise Manager gera o seguinte aviso nos registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

## Perfis de metadados {#metadata-profiles}

Um perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um perfil de metadados e aplique-o a uma pasta. Qualquer ativo carregado posteriormente para a pasta herda os metadados padrão configurados no perfil de metadados.

### Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Perfis **** de metadados e clique em **[!UICONTROL Criar]**.
1. Digite um título para o perfil, por exemplo `Sample Metadata`, e clique em **[!UICONTROL Criar]**. O formulário [!UICONTROL Editar formulário] para o perfil de metadados é exibido.

   ![Editar um formulário de metadados](assets/metadata-edit-form.png)

1. Clique em um componente e configure suas propriedades na guia **[!UICONTROL Configurações]** . Por exemplo, clique no componente **[!UICONTROL Descrição]** e edite suas propriedades.

   ![Configuração de um componente no perfil de metadados](assets/metadata-profile-component-setting.png)

   Edite as seguintes propriedades para o componente **[!UICONTROL Descrição]** :

   * **[!UICONTROL Rótulo]** do campo: O nome de exibição da propriedade de metadados. É apenas para a referência do usuário.

   * **[!UICONTROL Mapear para propriedade]**: O valor dessa propriedade fornece o caminho relativo ou o nome para o nó do ativo no qual ele é salvo no repositório. O valor deve sempre ser start `./` porque indica que o caminho está sob o nó do ativo.

   ![Configuração de mapeamento para propriedade no perfil de metadados](assets/metadata-profile-setting-map-property.png)

   The value you specify for **[!UICONTROL Map to property]** is stored as a property under the asset&#39;s metadata node. Por exemplo, se você especificar `./jcr:content/metadata/dc:desc` como o nome do **[!UICONTROL Mapa para a propriedade]**, [!DNL Assets] armazenará o valor `dc:desc` no nó de metadados do ativo.

   * **[!UICONTROL Valor]** padrão: Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

   ![Definir descrição padrão no perfil de metadados](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Adicionando um valor padrão a uma nova propriedade de metadados (que ainda não existe no . `/jcr:content/metadata` nó) não exibe a propriedade e seu valor na página Propriedades do ativo por padrão. Para visualização da nova propriedade na página [!UICONTROL Propriedades] dos ativos, modifique o formulário de schema correspondente.

1. (Opcional) Adicione mais componentes ao Formulário de edição na guia **[!UICONTROL Criar formulário]** e configure as propriedades na guia **[!UICONTROL Configurações]**. As seguintes propriedades estão disponíveis na guia **[!UICONTROL Criar formulário]**:

| Componente | Propriedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Título da seção] | Rótulo do campo, <br> Descrição |
| [!UICONTROL Texto em linha única] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Texto multivalor] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Número] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Data] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Tags padrão] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão, <br> Descrição |

1. Clique em **[!UICONTROL Concluído]**. O Perfil Metadados é adicionado à lista de perfis na página Perfis **** Metadados.<br>

   ![Perfil de metadados adicionado à página Perfis de metadados](assets/MetadataProfiles-page.png)

### Copiar um perfil de metadados {#copying-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um perfil de metadados para fazer uma cópia dele.

   ![Copiar um perfil de metadados](assets/metadata-profile-edit-copy-option.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. Na caixa de diálogo **[!UICONTROL Copiar Perfil]** de Metadados, digite um título para a nova cópia do Perfil de Metadados.
1. Clique em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

   ![Uma cópia do perfil de metadados adicionada na página Perfis de metadados](assets/copy-metadata-profile.png)

### Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. Na página Perfis **[!UICONTROL de]** metadados, selecione um perfil a ser excluído.

1. Clique em **[!UICONTROL Excluir Perfis]** de metadados na barra de ferramentas.
1. Na caixa de diálogo, clique em **[!UICONTROL Excluir]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

<!-- TBD: Revisit to find out the correct config. and update these steps. When fixed, also o
These steps have been carried forward from old AEM versions. See https://helpx.adobe.com/experience-manager/6-2/assets/using/metadata-profiles.html#ApplyingaMetadataProfiletoFolders

### Configuration to apply a metadata profile globally {#apply-a-metadata-profile-globally}

In addition to applying a profile to a folder, you can also apply one globally so that any content uploaded into [!DNL Experience Manager] assets in any folder has the selected profile applied.

You can reprocess assets in a folder that already has an existing metadata profile that you later changed. See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets).

To apply a metadata profile globally, follow these steps:

* Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and click **[!UICONTROL Save]**.

  ![Apply metadata profile to a folder globally](assets/metadata-profile-folder-setting.png)

* In CRXDE Lite, navigate to the following node: `/content/dam/jcr:content`. Add the property `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` and click **[!UICONTROL Save All]**.

  ![See applied metadata profile to a folder in the JCR in CRXDE](assets/metadata-profile-folder-setting2.png)
-->

## Schema de metadados para uma pasta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] permite criar schemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta.

### Adicionar um formulário de schema de metadados de pasta {#add-a-folder-metadata-schema-form}

Use o editor do Forms Schema de Metadados da Pasta para criar e editar schemas de metadados para pastas.

1. Na [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **[!UICONTROL de metadados]** da pasta.
1. Na página Forms [!UICONTROL do Schema de metadados da] pasta, clique em **[!UICONTROL Criar]**.
1. Specify a name for the form, and click **[!UICONTROL Create]**. O novo formulário de schema é listado na página do Forms [!UICONTROL do] Schema.

### Edit folder metadata schema forms {#edit-folder-metadata-schema-forms}

É possível editar um formulário de schema de metadados recém-adicionado ou existente, que inclui o seguinte:

* Guias
* Itens de formulário em guias.

Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar novas guias ou itens de formulário ao formulário de schema de metadados.

1. Na página Forms do Schema, selecione o formulário criado e, em seguida, selecione a opção **[!UICONTROL Editar]** na barra de ferramentas.
1. Na página Editor de Schemas de Metadados de Pastas, clique em `+` para adicionar uma guia ao formulário. Para renomear a guia, clique no nome padrão e especifique o novo nome em **[!UICONTROL Configurações]**.

   ![custom_tab](assets/custom_tab.png)

   Para adicionar mais guias, clique em `+`. Clique `X` em uma guia para excluí-la.

1. Na guia ativa, adicione um ou mais componentes da guia **[!UICONTROL Criar formulário]** .

   ![add_components](assets/adding_components.png)

   Se você criar várias guias, clique em uma guia específica para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Configurações]** .

   Se necessário, exclua um componente da guia **[!UICONTROL Configurações]** .

   ![configure_properties](assets/configure_properties.png)

1. Clique em **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações.

#### Componentes para criar formulários {#components-to-build-forms}

A guia **[!UICONTROL Criar formulário]** lista itens de formulário que você usa no formulário de schema de metadados da pasta. A guia **[!UICONTROL Configurações]** exibe os atributos para cada item selecionado na guia **[!UICONTROL Criar formulário]** . Esta é uma lista dos itens de formulário disponíveis na guia **[!UICONTROL Criar formulário]** :

| Nome do componente | Descrição |
|---|---|
| [!UICONTROL Título da seção] | Adicione um cabeçalho de seção para uma lista de componentes comuns. |
| [!UICONTROL Texto em linha única] | Adicione uma propriedade de texto de linha única. É armazenado como uma string. |
| [!UICONTROL Texto multivalor] | Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de string. |
| [!UICONTROL Número] | Adicione um componente de número. |
| [!UICONTROL Data] | Adicione um componente de data. |
| [!UICONTROL Lista suspensa] | Adicione uma lista suspensa. |
| [!UICONTROL Tags padrão] | Adicionar uma tag. |
| [!UICONTROL Campo oculto] | Adicionar um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo. |

#### Editar itens de formulário {#editing-form-items}

Para editar as propriedades dos itens de formulário, clique no componente e edite todas as propriedades ou um subconjunto das seguintes na guia **[!UICONTROL Configurações]** .

**[!UICONTROL Rótulo]** do campo: O nome da propriedade de metadados que é exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para propriedade]**: Essa propriedade especifica o caminho relativo do nó de pasta no repositório CRX onde ele é salvo. Ele start com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

Estes são os valores válidos para esta propriedade:

* `./jcr:content/metadata/dc:title`: Armazena o valor no nó de metadados da pasta como a propriedade `dc:title`.

* `./jcr:created`: Exibe a propriedade JCR no nó da pasta. Se você configurar essas propriedades no CRXDE, o Adobe recomenda marcá-las como Desativar edição, pois elas estão protegidas. Caso contrário, o erro &#39; `Asset(s) failed to modify`&#39; ocorrerá quando você salvar as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de schema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho]** JSON: Use-o para especificar o caminho do arquivo JSON no qual você especifica pares de valores chave para opções.

**[!UICONTROL Espaço reservado]**: Use essa propriedade para especificar o texto relevante do espaço reservado para a propriedade metadata.

**[!UICONTROL Opções]**: Use essa propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: Use essa propriedade para adicionar uma breve descrição para o componente de metadados.

**[!UICONTROL Classe]**: Classe de objeto à qual a propriedade está associada.

### Delete folder metadata schema forms {#delete-folder-metadata-schema-forms}

Você pode excluir formulários de schema de metadados de pasta da página Forms do Schema Metadados de pasta. Para excluir um formulário, selecione-o e clique na opção Excluir da barra de ferramentas.

![delete_form](assets/delete_form.png)

### Atribuir um schema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um schema de metadados de pasta a uma pasta na página Forms do Schema Metadados de pasta ou ao criar uma pasta.

Se você configurar um schema de metadados para uma pasta, o caminho para o formulário de schema será armazenado na `folderMetadataSchema` propriedade do nó de pasta em `./jcr:content`.

#### Atribuir a um schema da página Schema Metadados da pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Na [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **[!UICONTROL de metadados]** da pasta.
1. Na página do Forms Schema de metadados da pasta, selecione o formulário de schema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Aplicar às pastas]**.

1. Selecione a pasta na qual aplicar o schema e clique em **[!UICONTROL Aplicar]**. Se um schema de metadados já estiver aplicado na pasta, uma mensagem de aviso informará que você está prestes a substituir o schema de metadados existente. Clique em **[!UICONTROL Substituir]**.
1. Abra as propriedades de metadados da pasta na qual você aplicou o schema de metadados.

   ![folder_properties](assets/folder_properties.png)

   To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Atribuir um schema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um schema de metadados de pasta ao criar uma pasta. Se pelo menos um schema de metadados de pasta existir no sistema, uma lista extra será exibida na caixa de diálogo **[!UICONTROL Criar pasta]** . Você pode selecionar o schema desejado. Por padrão, nenhum schema é selecionado.

1. Na interface do [!DNL Experience Manager Assets] usuário, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Schema Metadados da pasta, selecione o schema desejado. Em seguida, clique em **[!UICONTROL Criar]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades de metadados da pasta na qual você aplicou o schema de metadados.
1. To view the folder metadata fields, click the **[!UICONTROL Folder Metadata]** tab.

### Usar o schema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. A **[!UICONTROL Folder Metadata]** tab is displayed in the folder [!UICONTROL Properties] page. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira os valores de metadados nos vários campos e clique em **[!UICONTROL Salvar]** para armazenar os valores. Os valores especificados são armazenados no nó da pasta no repositório CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Dicas e limitações {#best-practices-limitations}

* Para importar metadados em namespaces personalizadas, registre primeiro as namespaces.
* O Seletor de propriedades exibe as propriedades usadas em editores de schemas e formulários de pesquisa. O Seletor de propriedades não seleciona propriedades de metadados de um ativo.
* Você pode ter perfis de metadados pré-existentes desde antes de atualizar para a versão [!DNL Experience Manager] 6.5. Após a atualização, se esse perfil for aplicado nas [!UICONTROL Propriedades] da pasta na guia Perfis [!UICONTROL de] metadados, os campos do formulário de metadados não serão exibidos. No entanto, se um perfil de metadados recém-criado for aplicado, os campos do formulário serão exibidos, mas não estarão disponíveis conforme esperado. Não há perda de funcionalidade, mas se você quiser ver os campos de formulário (indisponíveis), edite e salve os perfis de metadados existentes.

>[!MORELIKETHIS]
>
>* [Conceitos de metadados e compreensão](metadata-concepts.md).
>* [Edite as propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html).
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).
>* [Práticas recomendadas para organizar seus ativos digitais para usar perfis](/help/assets/organize-assets.md)de processamento.
>* [XMP gravação](/help/assets/xmp-writeback.md).

