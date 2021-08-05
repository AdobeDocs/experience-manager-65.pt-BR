---
title: Configuração e administração da funcionalidade de metadados.
description: Configuração e administração da funcionalidade  [!DNL Experience Manager Assets] relacionada à adição e ao gerenciamento de metadados.
contentOwner: AG
role: User, Admin
feature: Metadados
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
source-git-commit: b36448449830aa8e19f6dc29ab7fb62608bb39dd
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 5%

---

# Configuração e administração da funcionalidade de metadados em [!DNL Assets] {#config-metadata}

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ela facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando por um ativo específico. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base em seus metadados. [!DNL Adobe Experience Manager Assets] permite que os administradores configurem e personalizem a funcionalidade de metadados para modificar a oferta de Adobe padrão.

## Editar esquema de metadados {#metadata-schema}

Para obter detalhes, consulte [editar formulários de esquema de metadados](metadata-schemas.md#edit-metadata-schema-forms).

## Registre um namespace personalizado em [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces em [!DNL Experience Manager]. Assim como há namespaces predefinidos, como `cq`, `jcr` e `sling`, você pode ter um namespace para os metadados do repositório e o processamento XML.

1. Acesse a página de administração do tipo de nó `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acessar a página de administração do namespace, clique em **[!UICONTROL Namespaces]** na parte superior da página.
1. Para adicionar um namespace, clique em **[!UICONTROL New]** na parte inferior da página.
1. Especifique um namespace personalizado na convenção de namespace XML. Especifique a ID no formato de um URI e um prefixo associado para a ID. Clique em **[!UICONTROL Salvar]**.

## Configurar limites para atualização de metadados em massa {#bulk-metadata-update-limit}

Para evitar uma situação semelhante a negação de serviço (DOS), [!DNL Enterprise Manager] limita o número de parâmetros suportados em uma solicitação do Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O Enterprise Manager gera o seguinte aviso nos logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para alterar o limite, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e altere o valor de **[!UICONTROL Parâmetros de POST máximo]** em **[!UICONTROL Manipulação de parâmetro da solicitação do Apache]** configuração OSGi.

## Perfis de metadados {#metadata-profiles}

Um perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um perfil de metadados e aplique-o a uma pasta. Qualquer ativo carregado posteriormente na pasta herda os metadados padrão configurados no perfil de metadados.

### Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de metadados]** e clique em **[!UICONTROL Criar]**.
1. Insira um título para o perfil, por exemplo `Sample Metadata`, e clique em **[!UICONTROL Criar]**. O [!UICONTROL Editar formulário] para o perfil de metadados é exibido.

   ![Editar um formulário de metadados](assets/metadata-edit-form.png)

1. Clique em um componente e configure suas propriedades na guia **[!UICONTROL Settings]**. Por exemplo, clique no componente **[!UICONTROL Description]** e edite suas propriedades.

   ![Configuração de um componente no perfil de metadados](assets/metadata-profile-component-setting.png)

   Edite as seguintes propriedades para o componente **[!UICONTROL Description]**:

   * **[!UICONTROL Rótulo]** do campo: O nome de exibição da propriedade de metadados. É somente para a referência do usuário.

   * **[!UICONTROL Mapear para propriedade]**: O valor dessa propriedade fornece o caminho relativo ou o nome para o nó do ativo, onde é salvo no repositório. O valor deve sempre começar com `./` porque indica que o caminho está no nó do ativo.

   ![Mapear para configuração de propriedade no perfil de metadados](assets/metadata-profile-setting-map-property.png)

   O valor especificado para **[!UICONTROL Mapear para propriedade]** é armazenado como uma propriedade no nó de metadados do ativo. Por exemplo, se você especificar `./jcr:content/metadata/dc:desc` como o nome de **[!UICONTROL Mapear para a propriedade]**, [!DNL Assets] armazenará o valor `dc:desc` no nó de metadados do ativo. É recomendável mapear apenas um campo para uma determinada propriedade no esquema de metadados. Caso contrário, o campo adicionado mais recente mapeado para a propriedade será escolhido pelo sistema.

   * **[!UICONTROL Valor]** padrão: Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

   ![Definir a descrição padrão no perfil de metadados](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Adicionar um valor padrão a uma nova propriedade de metadados (que ainda não existe no . `/jcr:content/metadata` (nó ) não exibe a propriedade e seu valor na página Propriedades do ativo por padrão. Para exibir a nova propriedade na página [!UICONTROL Properties] dos ativos, modifique o formulário de esquema correspondente.

1. (Opcional) Adicione mais componentes ao Formulário de edição na guia **[!UICONTROL Criar formulário]** e configure as propriedades na guia **[!UICONTROL Configurações]**. As seguintes propriedades estão disponíveis na guia **[!UICONTROL Criar formulário]**:

| Componente | Propriedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Título da seção] | Rótulo do campo, <br> Descrição |
| [!UICONTROL Texto em linha única] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Texto multivalor] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Número] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Data] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Tags padrão] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão, <br> Descrição |

1. Clique em **[!UICONTROL Concluído]**. O Perfil de metadados é adicionado à lista de perfis na página **[!UICONTROL Perfis de metadados]**.<br>

   ![Perfil de metadados adicionado na página Perfis de metadados](assets/MetadataProfiles-page.png)

### Copiar um perfil de metadados {#copying-a-metadata-profile}

1. Na página **[!UICONTROL Metadata Profiles]** , selecione um perfil de metadados para fazer uma cópia dele.

   ![Copiar um perfil de metadados](assets/metadata-profile-edit-copy-option.png)

1. Clique em **[!UICONTROL Copiar]** na barra de ferramentas.
1. Na caixa de diálogo **[!UICONTROL Copiar Perfil de Metadados]**, insira um título para a nova cópia do Perfil de Metadados.
1. Clique em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

   ![Uma cópia do perfil de metadados adicionada na página Perfis de metadados](assets/copy-metadata-profile.png)

### Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. Na página **[!UICONTROL Metadata Profiles]**, selecione um perfil a ser excluído.

1. Clique em **[!UICONTROL Excluir perfis de metadados]** na barra de ferramentas.
1. Na caixa de diálogo, clique em **[!UICONTROL Delete]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

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

## Esquema de metadados para uma pasta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta.

### Adicionar um formulário de esquema de metadados de pasta {#add-a-folder-metadata-schema-form}

Use o editor do Forms do Esquema de metadados da pasta para criar e editar esquemas de metadados para pastas.

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados da pasta]**.
1. Na página [!UICONTROL Esquema de Metadados da Pasta Forms], clique em **[!UICONTROL Criar]**.
1. Especifique um nome para o formulário e clique em **[!UICONTROL Criar]**. O novo formulário de esquema é listado na página [!UICONTROL Schema Forms].

### Editar formulários de esquema de metadados de pastas {#edit-folder-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente, incluindo o seguinte:

* Guias
* Itens de formulário nas guias.

Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar novas guias ou itens de formulário ao formulário de esquema de metadados.

1. Na página Schema Forms , selecione o formulário criado e selecione a opção **[!UICONTROL Edit]** na barra de ferramentas.
1. Na página Editor de esquema de metadados da pasta , clique em `+` para adicionar uma guia ao formulário. Para renomear a guia , clique no nome padrão e especifique o novo nome em **[!UICONTROL Settings]**.

   ![custom_tab](assets/custom_tab.png)

   Para adicionar mais guias, clique em `+`. Clique em `X` em uma guia para excluí-la.

1. Na guia ativa , adicione um ou mais componentes da guia **[!UICONTROL Criar formulário]**.

   ![adicionar_componentes](assets/adding_components.png)

   Se você criar várias guias, clique em uma determinada guia para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Settings]**.

   Se necessário, exclua um componente da guia **[!UICONTROL Settings]**.

   ![configure_properties](assets/configure_properties.png)

1. Clique em **[!UICONTROL Salvar]** na barra de ferramentas para salvar as alterações.

#### Componentes para criar formulários {#components-to-build-forms}

A guia **[!UICONTROL Criar formulário]** lista os itens de formulário que você usa no formulário de esquema de metadados da pasta. A guia **[!UICONTROL Settings]** exibe os atributos para cada item selecionado na guia **[!UICONTROL Criar formulário]**. Esta é uma lista dos itens de formulário disponíveis na guia **[!UICONTROL Criar formulário]**:

| Nome do componente | Descrição |
|---|---|
| [!UICONTROL Título da seção] | Adicione um cabeçalho de seção para obter uma lista de componentes comuns. |
| [!UICONTROL Texto em linha única] | Adicione uma propriedade de texto de linha única. Ele é armazenado como uma string. |
| [!UICONTROL Texto multivalor] | Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de sequência de caracteres. |
| [!UICONTROL Número] | Adicione um componente de número. |
| [!UICONTROL Data] | Adicione um componente de data. |
| [!UICONTROL Lista suspensa] | Adicione uma lista suspensa. |
| [!UICONTROL Tags padrão] | Adicionar uma tag. |
| [!UICONTROL Campo oculto] | Adicione um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo. |

#### Edição de itens de formulário {#editing-form-items}

Para editar as propriedades dos itens de formulário, clique no componente e edite todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Settings]**.

**[!UICONTROL Rótulo]** do campo: O nome da propriedade de metadados exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para propriedade]**: Essa propriedade especifica o caminho relativo do nó da pasta no repositório CRX, onde é salva. Começa com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

A seguir estão os valores válidos para essa propriedade:

* `./jcr:content/metadata/dc:title`: Armazena o valor no nó de metadados da pasta como a propriedade  `dc:title`.

* `./jcr:created`: Exibe a propriedade JCR no nó da pasta. Se você configurar essas propriedades no CRXDE, o Adobe recomenda marcá-las como Desativar edição, pois elas estão protegidas. Caso contrário, o erro &#39; `Asset(s) failed to modify`&#39; ocorre quando você salva as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho]** JSON: Use-o para especificar o caminho do arquivo JSON, onde você especifica pares de valores chave para opções.

**[!UICONTROL Espaço reservado]**: Use essa propriedade para especificar o texto de espaço reservado relevante em relação à propriedade de metadados.

**[!UICONTROL Opções]**: Use essa propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: Use essa propriedade para adicionar uma breve descrição para o componente de metadados.

**[!UICONTROL Classe]**: Classe de objeto à qual a propriedade está associada.

### Excluir formulários de esquema de metadados da pasta {#delete-folder-metadata-schema-forms}

É possível excluir formulários de esquema de metadados de pastas da página Forms do Esquema de Metadados da Pasta. Para excluir um formulário, selecione-o e clique na opção excluir na barra de ferramentas.

![delete_form](assets/delete_form.png)

### Atribuir um esquema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um esquema de metadados de pasta a uma pasta na página Forms do Esquema de Metadados da Pasta ou ao criar uma pasta.

Se um esquema de metadados for configurado para uma pasta, o caminho para o formulário de esquema será armazenado na propriedade `folderMetadataSchema` do nó da pasta em `./jcr:content`.

#### Atribuir a um schema a partir da página Esquema de metadados da pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Na interface [!DNL Experience Manager], vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados da pasta]**.
1. Na página Forms do Esquema de metadados da pasta , selecione o formulário de esquema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Aplicar à(s) pasta(s)]**.

1. Selecione a pasta na qual aplicar o esquema e clique em **[!UICONTROL Aplicar]**. Se um esquema de metadados já estiver aplicado na pasta, uma mensagem de aviso informará que você está prestes a substituir o esquema de metadados existente. Clique em **[!UICONTROL Substituir]**.
1. Abra as propriedades dos metadados da pasta na qual você aplicou o esquema de metadados.

   ![folder_properties](assets/folder_properties.png)

   Para exibir os campos de metadados da pasta, clique na guia **[!UICONTROL Metadados da pasta]** .

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Atribuir um schema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um esquema de metadados de pasta ao criar uma pasta. Se pelo menos um esquema de metadados de pasta existir no sistema, uma lista extra será exibida na caixa de diálogo **[!UICONTROL Criar pasta]**. Você pode selecionar o schema desejado. Por padrão, nenhum esquema é selecionado.

1. Na interface do usuário [!DNL Experience Manager Assets], clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Esquema de metadados da pasta, selecione o esquema desejado. Em seguida, clique em **[!UICONTROL Create]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades dos metadados da pasta na qual você aplicou o esquema de metadados.
1. Para exibir os campos de metadados da pasta, clique na guia **[!UICONTROL Metadados da pasta]** .

### Usar o esquema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. Uma guia **[!UICONTROL Metadados da pasta]** é exibida na página [!UICONTROL Propriedades] da pasta. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira valores de metadados nos vários campos e clique em **[!UICONTROL Save]** para armazenar os valores. Os valores especificados são armazenados no nó folder no repositório CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Dicas e limitações {#best-practices-limitations}

* Para importar metadados em namespaces personalizados, primeiro registre os namespaces.
* O Seletor de propriedades exibe propriedades que são usadas em editores de esquema e formulários de pesquisa. O Seletor de propriedades não seleciona propriedades de metadados de um ativo.
* Você pode ter perfis de metadados pré-existentes desde antes de atualizar para [!DNL Experience Manager] 6.5. Após a atualização, se você aplicar esse perfil na pasta [!UICONTROL Propriedades] na guia [!UICONTROL Perfis de metadados], os campos de formulário de metadados não serão exibidos. No entanto, se você aplicar um perfil de metadados recém-criado, os campos do formulário serão exibidos, mas não estarão disponíveis conforme esperado. Não há perda de funcionalidade, mas se você quiser ver os campos de formulário (indisponíveis), edite e salve os perfis de metadados existentes.

>[!MORELIKETHIS]
>
>* [Conceitos e compreensão de metadados](metadata-concepts.md).
>* [Edite as propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html).
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).
>* [Práticas recomendadas para organizar ativos digitais para usar perfis](/help/assets/organize-assets.md) de processamento.
>* [XMP write-back](/help/assets/xmp-writeback.md).

