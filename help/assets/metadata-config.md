---
title: Configuração e administração da funcionalidade de metadados.
description: Configuração e administração de [!DNL Experience Manager Assets] funcionalidade relacionada à adição e ao gerenciamento de metadados.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2000'
ht-degree: 5%

---

# Configuração e administração da funcionalidade de metadados no [!DNL Assets] {#config-metadata}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | Este artigo |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, and so on, operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] O mantém metadados de cada ativo. Ele facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base nos metadados. [!DNL Adobe Experience Manager Assets] O permite que os administradores configurem e personalizem a funcionalidade de metadados para modificar a oferta de Adobe padrão.

## Editar esquema de metadados {#metadata-schema}

Para obter detalhes, consulte [editar formulários de esquema de metadados](metadata-schemas.md#edit-metadata-schema-forms).

## Registrar um namespace personalizado em [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces no [!DNL Experience Manager]. Assim como há namespaces predefinidos, como `cq`, `jcr`, e `sling`, você pode ter um namespace para os metadados do repositório e o processamento XML.

1. Acessar a página de administração do tipo de nó `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acessar a página de administração do namespace, clique em **[!UICONTROL Namespaces]** na parte superior da página.
1. Para adicionar um namespace, clique em **[!UICONTROL Novo]** na parte inferior da página.
1. Especifique um namespace personalizado na convenção de namespace XML. Especifique a ID no formato de um URI e um prefixo associado para a ID. Clique em **[!UICONTROL Salvar]**.

## Configurar limites para atualização de metadados em massa {#bulk-metadata-update-limit}

Para evitar uma situação semelhante a de negação de serviço (DOS), [!DNL Enterprise Manager] limita o número de parâmetros compatíveis em uma solicitação do Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O Enterprise Manager gera a seguinte advertência nos logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para alterar o limite, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e altere o valor de **[!UICONTROL Parâmetros de POST máximo]** in **[!UICONTROL Manipulação de parâmetro de solicitação do Apache Sling]** Configuração do OSGi.

## Perfis de metadados {#metadata-profiles}

Um perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um perfil de metadados e aplique-o a uma pasta. Qualquer ativo enviado posteriormente para a pasta herda os metadados padrão configurados no perfil de metadados.

### Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de metadados]** e clique em **[!UICONTROL Criar]**.
1. Insira um título para o perfil, por exemplo, `Sample Metadata`e clique em **[!UICONTROL Criar]**. A variável [!UICONTROL Editar formulário] para o perfil de metadados.

   ![Editar um formulário de metadados](assets/metadata-edit-form.png)

1. Clique em um componente e configure suas propriedades na **[!UICONTROL Configurações]** guia. Por exemplo, clique no link **[!UICONTROL Descrição]** componente e editar suas propriedades.

   ![Configuração de um componente no perfil de metadados](assets/metadata-profile-component-setting.png)

   Edite as seguintes propriedades para o **[!UICONTROL Descrição]** componente:

   * **[!UICONTROL Rótulo do campo]**: o nome para exibição da propriedade de metadados. É somente para referência do usuário.

   * **[!UICONTROL Mapear para a propriedade]**: o valor dessa propriedade fornece o caminho relativo ou o nome para o nó do ativo onde ele é salvo no repositório. O valor deve sempre começar com `./` porque indica que o caminho está no nó do ativo.

   ![Mapear para a configuração de propriedade no perfil de metadados](assets/metadata-profile-setting-map-property.png)

   O valor especificado para **[!UICONTROL Mapear para a propriedade]** O é armazenado como uma propriedade no nó de metadados do ativo. Por exemplo, se você especificar `./jcr:content/metadata/dc:desc` como o nome de **[!UICONTROL Mapear para a propriedade]**, [!DNL Assets] armazena o valor `dc:desc` no nó de metadados do ativo. A Adobe recomenda mapear apenas um campo para uma determinada propriedade no esquema de metadados. Caso contrário, o campo adicionado mais recente mapeado para a propriedade será escolhido pelo sistema.

   * **[!UICONTROL Valor padrão]**: use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

   ![Definir descrição padrão no perfil de metadados](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Adicionar um valor padrão a uma nova propriedade de metadados (que não existe em `/jcr:content/metadata` ) não exibe a propriedade e seu valor na variável [!UICONTROL Propriedades] por padrão. Para exibir a nova propriedade nos ativos&#39; [!UICONTROL Propriedades] modifique o formulário de esquema correspondente.

1. (Opcional) Na **[!UICONTROL Formulário de criação]** adicione mais componentes a [!UICONTROL Editar formulário]e configure as propriedades na variável **[!UICONTROL Configurações]** guia. As seguintes propriedades estão disponíveis no **[!UICONTROL Formulário de criação]** guia:

| Componente | Propriedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Cabeçalho da seção] | Rótulo do campo, <br> Descrição |
| [!UICONTROL Texto em linha única] | Rótulo do campo, <br> Mapear para a propriedade, <br> Valor padrão |
| [!UICONTROL Texto multivalor] | Rótulo do campo, <br> Mapear para a propriedade, <br> Valor padrão |
| [!UICONTROL Número] | Rótulo do campo, <br> Mapear para a propriedade, <br> Valor padrão |
| [!UICONTROL Data] | Rótulo do campo, <br> Mapear para a propriedade, <br> Valor padrão |
| [!UICONTROL Tags padrão] | Rótulo do campo, <br> Mapear para a propriedade, <br> Valor padrão, <br> Descrição |

1. Clique em **[!UICONTROL Concluído]**. O Perfil de metadados é adicionado à lista de perfis na variável **[!UICONTROL Perfis de metadados]** página.<br>

   ![Perfil de metadados adicionado na página Perfis de metadados](assets/MetadataProfiles-page.png)

### Copiar um perfil de metadados {#copying-a-metadata-profile}

1. No **[!UICONTROL Perfis de metadados]** selecione um perfil de metadados para fazer uma cópia dele.

   ![Copiar um perfil de metadados](assets/metadata-profile-edit-copy-option.png)

1. Clique em **[!UICONTROL Copiar]** na barra de ferramentas.
1. No **[!UICONTROL Copiar perfil de metadados]** , insira um título para a nova cópia do Perfil de metadados.
1. Clique em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

   ![Uma cópia do perfil de metadados adicionado na página Perfis de metadados](assets/copy-metadata-profile.png)

### Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. No **[!UICONTROL Perfis de metadados]** selecione um perfil a ser excluído.

1. Clique em **[!UICONTROL Excluir perfis de metadados]** na barra de ferramentas.
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

## Esquema de metadados para uma pasta {#folder-metadata-schema}

[!DNL Adobe Experience Manager Assets] O permite criar esquemas de metadados para pastas de ativos, que definem o layout e os metadados exibidos nas páginas de propriedades da pasta.

### Adicionar um formulário de esquema de metadados de pasta {#add-a-folder-metadata-schema-form}

Use o editor do Forms de Esquema de metadados de pasta para criar e editar esquemas de metadados para pastas.

1. Entrada [!DNL Experience Manager] , vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados de pasta]**.
1. No [!UICONTROL Forms de esquema de metadados de pasta] clique em **[!UICONTROL Criar]**.
1. Especifique um nome para o formulário e clique em **[!UICONTROL Criar]**. O novo formulário de esquema está listado no [!UICONTROL Schema Forms] página.

### Editar formulários de esquema de metadados de pasta {#edit-folder-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente, que inclui o seguinte:

* Guias
* Itens de formulário em guias.

Você pode mapear/configurar esses itens de formulário para um campo em um nó de metadados no repositório CRX. Você pode adicionar novas guias ou itens de formulário ao formulário de esquema de metadados.

1. Na página Schema Forms, selecione o formulário criado e selecione o **[!UICONTROL Editar]** na barra de ferramentas.
1. Na página Editor de esquema de metadados de pasta, clique em `+` para adicionar uma guia ao formulário. Para renomear a guia, clique no nome padrão e especifique o novo nome em **[!UICONTROL Configurações]**.

   ![custom_tab](assets/custom_tab.png)

   Para adicionar mais guias, clique em `+`. Para excluir, clique em `X` em uma guia.

1. Na guia ativa, adicione um ou mais componentes da **[!UICONTROL Formulário de criação]** guia.

   ![add_components](assets/adding_components.png)

   Se você criar várias guias, clique em uma guia específica para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades na **[!UICONTROL Configurações]** guia.

   Se necessário, exclua um componente da variável **[!UICONTROL Configurações]** guia.

   ![configure_properties](assets/configure_properties.png)

1. Para salvar as alterações, selecione **[!UICONTROL Salvar]** na barra de ferramentas.

#### Componentes para criar formulários {#components-to-build-forms}

A variável **[!UICONTROL Formulário de criação]** A guia lista os itens de formulário que você usa no formulário de esquema de metadados da pasta. A variável **[!UICONTROL Configurações]** exibe os atributos de cada item selecionado na guia **[!UICONTROL Formulário de criação]** guia. Esta é uma lista dos itens de formulário disponíveis no **[!UICONTROL Formulário de criação]** guia:

| Nome do componente | Descrição |
|---|---|
| [!UICONTROL Cabeçalho da seção] | Adicione um cabeçalho de seção para obter uma lista de componentes comuns. |
| [!UICONTROL Texto em linha única] | Adiciona uma propriedade de texto em linha única. Ele é armazenado como uma string. |
| [!UICONTROL Texto multivalor] | Adiciona uma propriedade de texto multivalor. Ele é armazenado como uma matriz de sequência. |
| [!UICONTROL Número] | Adiciona um componente de número. |
| [!UICONTROL Data] | Adiciona um componente de data. |
| [!UICONTROL Lista suspensa] | Adiciona uma lista suspensa. |
| [!UICONTROL Tags padrão] | Adicionar uma tag. |
| [!UICONTROL Campo oculto] | Adicione um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo. |

#### Edição de itens de formulário {#editing-form-items}

Para editar as propriedades dos itens de formulário, clique no componente e edite todas ou um subconjunto das seguintes propriedades na **[!UICONTROL Configurações]** guia.

**[!UICONTROL Rótulo do campo]**: o nome da propriedade de metadados que é exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para a propriedade]**: essa propriedade especifica o caminho relativo do nó da pasta no repositório CRX onde ele é salvo. Ele começa com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

A seguir estão os valores válidos para essa propriedade:

* `./jcr:content/metadata/dc:title`: armazena o valor no nó de metadados da pasta como a propriedade `dc:title`.

* `./jcr:created`: exibe a propriedade JCR no nó da pasta. Se você configurar essas propriedades no CRXDE, a Adobe recomenda marcá-las como Desativar edição, pois elas estão protegidas. Caso contrário, o erro &#39; `Asset(s) failed to modify`&#39; ocorre quando você salva as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho JSON]**: use-o para especificar o caminho do arquivo JSON onde você especifica pares de valores-chave para opções.

**[!UICONTROL Espaço reservado]**: use essa propriedade para especificar um texto de espaço reservado relevante em relação à propriedade de metadados.

**[!UICONTROL Opções]**: use essa propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: use essa propriedade para adicionar uma breve descrição do componente de metadados.

**[!UICONTROL Classe]**: classe de objeto à qual a propriedade está associada.

### Excluir formulários de esquema de metadados de pasta {#delete-folder-metadata-schema-forms}

Você pode deletar formulários de esquema de metadados de pasta da página Forms de Esquema de Metadados de Pasta. Para excluir um formulário, selecione-o e clique na opção de exclusão na barra de ferramentas.

![delete_form](assets/delete_form.png)

### Atribuir um esquema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um esquema de metadados de pasta a uma pasta na página Forms de Esquema de metadados de pasta ou ao criar uma pasta.

Se você configurar um esquema de metadados para uma pasta, o caminho para o formulário de esquema será armazenado no `folderMetadataSchema` propriedade do nó de pasta em `./jcr:content`.

#### Atribuir a um esquema a partir da página Esquema de metadados de pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Entrada [!DNL Experience Manager] , vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados de pasta]**.
1. Na página Forms do Esquema de Metadados da Pasta, selecione o formulário de esquema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Aplicar às pastas]**.

1. Selecione a pasta na qual o esquema será aplicado e clique em **[!UICONTROL Aplicar]**. Se um esquema de metadados já estiver aplicado à pasta, uma mensagem de aviso informará que você está prestes a substituir o esquema de metadados existente. Clique em **[!UICONTROL Substituir]**.
1. Abra as propriedades de metadados da pasta à qual você aplicou o esquema de metadados.

   ![folder_properties](assets/folder_properties.png)

   Para exibir os campos de metadados da pasta, clique no **[!UICONTROL Metadados da pasta]** guia.

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Atribuir um esquema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um esquema de metadados de pasta ao criar uma pasta. Se pelo menos um esquema de metadados de pasta existir no sistema, uma lista extra será exibida no **[!UICONTROL Criar pasta]** diálogo. Você pode selecionar o esquema desejado. Por padrão, nenhum schema está selecionado.

1. No [!DNL Experience Manager Assets] clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Esquema de metadados de pasta, selecione o esquema desejado. Em seguida, clique em **[!UICONTROL Criar]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades de metadados da pasta à qual você aplicou o esquema de metadados.
1. Para exibir os campos de metadados da pasta, clique no **[!UICONTROL Metadados da pasta]** guia.

### Usar o esquema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. A **[!UICONTROL Metadados da pasta]** é exibida na pasta [!UICONTROL Propriedades] página. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira os valores de metadados nos vários campos e clique em **[!UICONTROL Salvar]** para armazenar os valores. Os valores especificados são armazenados no nó da pasta no repositório CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Dicas e limitações {#best-practices-limitations}

* Para importar metadados em namespaces personalizados, primeiro registre os namespaces.
* O Seletor de propriedades exibe as propriedades que são usadas em editores de esquema e formulários de pesquisa. O Seletor de propriedades não seleciona propriedades de metadados de um ativo.
* Você pode ter perfis de metadados pré-existentes desde antes de atualizar para [!DNL Experience Manager] 6.5. Depois da atualização, se você aplicar esse perfil na pasta [!UICONTROL Propriedades] in [!UICONTROL Perfis de metadados] os campos do formulário de metadados não são exibidos. No entanto, se você aplicar um perfil de metadados recém-criado, os campos de formulário serão exibidos, mas indisponíveis conforme esperado. Não há perda de funcionalidade, mas se você quiser ver os campos de formulário (indisponíveis), edite e salve os perfis de metadados existentes.

>[!MORELIKETHIS]
>
>* [Conceitos e noções básicas sobre metadados](metadata-concepts.md).
>* [Editar propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).
>* [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).
>* [Writeback XMP](/help/assets/xmp-writeback.md).
