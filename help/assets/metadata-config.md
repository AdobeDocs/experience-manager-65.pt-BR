---
title: Configuração e administração da funcionalidade de metadados.
description: Configuração e administração de [!DNL Experience Manager Assets] relacionada à adição e gerenciamento de metadados.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 56c92b7f-e687-4ab5-a376-afa58bdb6ee0
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 4%

---

# Configuração e administração da funcionalidade de metadados no [!DNL Assets] {#config-metadata}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-profiles.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/metadata-profiles.html?lang=en) |

<!-- Scope of metadata articles:
* metadata.md: The scope of this article is basic metadata updates, changes, etc. operations that end-users can do.
* metadata-concepts.md: All conceptual information. Minor instructions are OK but it is an FYI article about support and standards.
* metadata-config.md: New article. Contains all configuration and administration how-to info related to metadata of assets.
-->

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ela facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando por um ativo específico. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base em seus metadados. [!DNL Adobe Experience Manager Assets] permite que os administradores configurem e personalizem a funcionalidade de metadados para modificar a oferta de Adobe padrão.

## Editar esquema de metadados {#metadata-schema}

Para obter detalhes, consulte [editar formulários de esquema de metadados](metadata-schemas.md#edit-metadata-schema-forms).

## Registre um namespace personalizado em [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Você pode adicionar seus próprios namespaces no [!DNL Experience Manager]. Assim como há namespaces predefinidos, como `cq`, `jcr`e `sling`, você pode ter um namespace para os metadados do repositório e o processamento XML.

1. Acesse a página de administração do tipo de nó `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Para acessar a página de administração do namespace, clique em **[!UICONTROL Namespaces]** na parte superior da página.
1. Para adicionar um namespace, clique em **[!UICONTROL Novo]** na parte inferior da página.
1. Especifique um namespace personalizado na convenção de namespace XML. Especifique a ID no formato de um URI e um prefixo associado para a ID. Clique em **[!UICONTROL Salvar]**.

## Configurar limites para atualização de metadados em massa {#bulk-metadata-update-limit}

Para evitar uma situação semelhante à negação de serviço (DOS), [!DNL Enterprise Manager] limita o número de parâmetros suportados em uma solicitação do Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O Enterprise Manager gera o seguinte aviso nos logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para alterar o limite, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e alterar o valor de **[!UICONTROL Parâmetros de POST máximo]** em **[!UICONTROL Manuseio de parâmetro da solicitação do Apache Sling]** Configuração do OSGi.

## Perfis de metadados {#metadata-profiles}

Um perfil de metadados permite aplicar metadados padrão a ativos em uma pasta. Crie um perfil de metadados e aplique-o a uma pasta. Qualquer ativo carregado posteriormente na pasta herda os metadados padrão configurados no perfil de metadados.

### Adicionar um perfil de metadados {#adding-a-metadata-profile}

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de metadados]** e clique em **[!UICONTROL Criar]**.
1. Insira um título para o perfil, por exemplo `Sample Metadata`e clique em **[!UICONTROL Criar]**. O [!UICONTROL Editar formulário] para o perfil de metadados é exibido.

   ![Editar um formulário de metadados](assets/metadata-edit-form.png)

1. Clique em um componente e configure suas propriedades no **[!UICONTROL Configurações]** guia . Por exemplo, clique no botão **[!UICONTROL Descrição]** e edite suas propriedades.

   ![Configuração de um componente no perfil de metadados](assets/metadata-profile-component-setting.png)

   Edite as seguintes propriedades para o **[!UICONTROL Descrição]** componente:

   * **[!UICONTROL Rótulo do campo]**: O nome de exibição da propriedade de metadados. É somente para a referência do usuário.

   * **[!UICONTROL Mapear para propriedade]**: O valor dessa propriedade fornece o caminho relativo ou o nome para o nó do ativo, onde é salvo no repositório. O valor deve sempre começar com `./` porque indica que o caminho está sob o nó do ativo.

   ![Mapear para configuração de propriedade no perfil de metadados](assets/metadata-profile-setting-map-property.png)

   O valor especificado para **[!UICONTROL Mapear para propriedade]** é armazenado como uma propriedade no nó de metadados do ativo. Por exemplo, se você especificar `./jcr:content/metadata/dc:desc` como o nome de **[!UICONTROL Mapear para propriedade]**, [!DNL Assets] armazena o valor `dc:desc` no nó de metadados do ativo. O Adobe recomenda mapear apenas um campo para uma determinada propriedade no esquema de metadados. Caso contrário, o campo adicionado mais recente mapeado para a propriedade será escolhido pelo sistema.

   * **[!UICONTROL Valor padrão]**: Use essa propriedade para adicionar um valor padrão para o componente de metadados. Por exemplo, se você especificar &quot;Minha descrição&quot;, esse valor será atribuído à propriedade `dc:desc` no nó de metadados do ativo.

   ![Definir a descrição padrão no perfil de metadados](assets/metadata-profile-setting-default-value.png)

   >[!NOTE]
   >
   >Adicionar um valor padrão a uma nova propriedade de metadados (que não existe em `/jcr:content/metadata` nó ) não exibe a propriedade e seu valor no [!UICONTROL Propriedades] por padrão. Para exibir a nova propriedade nos ativos [!UICONTROL Propriedades] modifique o formulário de esquema correspondente.

1. (Opcional) Na seção **[!UICONTROL Criar formulário]** , adicione mais componentes a [!UICONTROL Editar formulário]e configure suas propriedades no **[!UICONTROL Configurações]** guia . As seguintes propriedades estão disponíveis na variável **[!UICONTROL Criar formulário]** guia :

| Componente | Propriedades |
| ----------------------------- | ----------------------------------------------------------------------- |
| [!UICONTROL Título da seção] | Rótulo do campo, <br> Descrição |
| [!UICONTROL Texto de linha única] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Texto multivalor] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Número] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Data] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão |
| [!UICONTROL Tags padrão] | Rótulo do campo, <br> Mapear para propriedade, <br> Valor padrão, <br> Descrição |

1. Clique em **[!UICONTROL Concluído]**. O Perfil de metadados é adicionado à lista de perfis no **[!UICONTROL Perfis de metadados]** página.<br>

   ![Perfil de metadados adicionado na página Perfis de metadados](assets/MetadataProfiles-page.png)

### Copiar um perfil de metadados {#copying-a-metadata-profile}

1. No **[!UICONTROL Perfis de metadados]** selecione um perfil de metadados para fazer uma cópia dele.

   ![Copiar um perfil de metadados](assets/metadata-profile-edit-copy-option.png)

1. Clique em **[!UICONTROL Copiar]** na barra de ferramentas.
1. No **[!UICONTROL Copiar perfil de metadados]** , insira um título para a nova cópia do Perfil de metadados.
1. Clique em **[!UICONTROL Copiar]**. A cópia do Perfil de metadados aparece na lista de perfis na página **[!UICONTROL Perfis de metadados]**.

   ![Uma cópia do perfil de metadados adicionada na página Perfis de metadados](assets/copy-metadata-profile.png)

### Excluir um perfil de metadados {#deleting-a-metadata-profile}

1. No **[!UICONTROL Perfis de metadados]** selecione um perfil a ser excluído.

1. Clique em **[!UICONTROL Excluir perfis de metadados]** na barra de ferramentas.
1. Na caixa de diálogo , clique em **[!UICONTROL Excluir]** para confirmar a operação de exclusão. O perfil de metadados é excluído da lista.

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

1. Em [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados da pasta]**.
1. No [!UICONTROL Forms do esquema de metadados da pasta] página, clique em **[!UICONTROL Criar]**.
1. Especifique um nome para o formulário e clique em **[!UICONTROL Criar]**. O novo formulário de esquema é listado na variável [!UICONTROL Schema Forms] página.

### Editar formulários de esquema de metadados de pastas {#edit-folder-metadata-schema-forms}

É possível editar um formulário de esquema de metadados recém-adicionado ou existente, incluindo o seguinte:

* Guias
* Itens de formulário nas guias.

Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar novas guias ou itens de formulário ao formulário de esquema de metadados.

1. Na página Schema Forms , selecione o formulário criado e selecione o **[!UICONTROL Editar]** na barra de ferramentas.
1. Na página Editor de esquema de metadados da pasta , clique em `+` para adicionar uma guia ao formulário. Para renomear a guia , clique no nome padrão e especifique o novo nome em **[!UICONTROL Configurações]**.

   ![custom_tab](assets/custom_tab.png)

   Para adicionar mais guias, clique em `+`. Para excluir, clique em `X` em uma guia .

1. Na guia ativa , adicione um ou mais componentes do **[!UICONTROL Criar formulário]** guia .

   ![adicionar_componentes](assets/adding_components.png)

   Se você criar várias guias, clique em uma determinada guia para adicionar componentes.

1. Para configurar um componente, selecione-o e modifique suas propriedades no **[!UICONTROL Configurações]** guia .

   Se necessário, exclua um componente do **[!UICONTROL Configurações]** guia .

   ![configure_properties](assets/configure_properties.png)

1. Para salvar as alterações, selecione **[!UICONTROL Salvar]** na barra de ferramentas.

#### Componentes para criar formulários {#components-to-build-forms}

O **[!UICONTROL Criar formulário]** lista itens de formulário que você usa no formulário de esquema de metadados da pasta. O **[!UICONTROL Configurações]** A guia exibe os atributos para cada item selecionado na variável **[!UICONTROL Criar formulário]** guia . Esta é uma lista com os itens de formulário disponíveis no **[!UICONTROL Criar formulário]** guia :

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

Para editar as propriedades dos itens de formulário, clique no componente e edite todas ou um subconjunto das seguintes propriedades na **[!UICONTROL Configurações]** guia .

**[!UICONTROL Rótulo do campo]**: O nome da propriedade de metadados exibida na página de propriedades da pasta.

**[!UICONTROL Mapear para propriedade]**: Essa propriedade especifica o caminho relativo do nó da pasta no repositório CRX, onde é salva. Começa com &quot;**./**&quot;, que indica que o caminho está sob o nó da pasta.

A seguir estão os valores válidos para essa propriedade:

* `./jcr:content/metadata/dc:title`: Armazena o valor no nó de metadados da pasta como a propriedade `dc:title`.

* `./jcr:created`: Exibe a propriedade JCR no nó da pasta. Se você configurar essas propriedades no CRXDE, o Adobe recomenda marcá-las como Desativar edição, pois elas estão protegidas. Caso contrário, o erro &#39; `Asset(s) failed to modify`&#39; ocorre ao salvar as propriedades do ativo.

Para garantir que o componente seja exibido corretamente no formulário de esquema de metadados, não inclua um espaço no caminho da propriedade.

**[!UICONTROL Caminho JSON]**: Use-o para especificar o caminho do arquivo JSON, onde você especifica pares de valores chave para opções.

**[!UICONTROL Espaço reservado]**: Use essa propriedade para especificar o texto de espaço reservado relevante em relação à propriedade de metadados.

**[!UICONTROL Opções]**: Use essa propriedade para especificar opções em uma lista.

**[!UICONTROL Descrição]**: Use essa propriedade para adicionar uma breve descrição para o componente de metadados.

**[!UICONTROL Classe]**: Classe de objeto à qual a propriedade está associada.

### Excluir formulários de esquema de metadados da pasta {#delete-folder-metadata-schema-forms}

É possível excluir formulários de esquema de metadados de pastas da página Forms do Esquema de Metadados da Pasta. Para excluir um formulário, selecione-o e clique na opção excluir na barra de ferramentas.

![delete_form](assets/delete_form.png)

### Atribuir um esquema de metadados de pasta {#assign-a-folder-metadata-schema}

Você pode atribuir um esquema de metadados de pasta a uma pasta na página Forms do Esquema de Metadados da Pasta ou ao criar uma pasta.

Se um esquema de metadados for configurado para uma pasta, o caminho para o formulário de esquema será armazenado no `folderMetadataSchema` propriedade do nó da pasta em `./jcr:content`.

#### Atribuir a um schema a partir da página Esquema de metadados da pasta {#assign-to-a-schema-from-the-folder-metadata-schema-page}

1. Em [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados da pasta]**.
1. Na página Forms do Esquema de metadados da pasta , selecione o formulário de esquema que deseja aplicar a uma pasta.
1. Na barra de ferramentas, clique em **[!UICONTROL Aplicar às pastas]**.

1. Selecione a pasta na qual aplicar o esquema e clique em **[!UICONTROL Aplicar]**. Se um esquema de metadados já estiver aplicado na pasta, uma mensagem de aviso informará que você está prestes a substituir o esquema de metadados existente. Clique em **[!UICONTROL Substituir]**.
1. Abra as propriedades dos metadados da pasta na qual você aplicou o esquema de metadados.

   ![folder_properties](assets/folder_properties.png)

   Para exibir os campos de metadados da pasta, clique no botão **[!UICONTROL Metadados da pasta]** guia .

   ![folder_metadata_properties](assets/folder_metadata_properties.png)

#### Atribuir um schema ao criar uma pasta {#assign-a-schema-when-creating-a-folder}

Você pode atribuir um esquema de metadados de pasta ao criar uma pasta. Se pelo menos um esquema de metadados de pasta existir no sistema, uma lista extra será exibida no **[!UICONTROL Criar pasta]** caixa de diálogo. Você pode selecionar o schema desejado. Por padrão, nenhum esquema é selecionado.

1. No [!DNL Experience Manager Assets] interface do usuário, clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Especifique um título e nome para a pasta.
1. Na lista Esquema de metadados da pasta, selecione o esquema desejado. Em seguida, clique em **[!UICONTROL Criar]**.

   ![select_schema](assets/select_schema.png)

1. Abra as propriedades dos metadados da pasta na qual você aplicou o esquema de metadados.
1. Para exibir os campos de metadados da pasta, clique no botão **[!UICONTROL Metadados da pasta]** guia .

### Usar o esquema de metadados da pasta {#use-the-folder-metadata-schema}

Abra as propriedades de uma pasta configurada com um esquema de metadados de pasta. A **[!UICONTROL Metadados da pasta]** é exibida na pasta [!UICONTROL Propriedades] página. Para exibir o formulário de esquema de metadados da pasta, selecione essa guia.

Insira os valores de metadados nos vários campos e clique em **[!UICONTROL Salvar]** para armazenar os valores. Os valores especificados são armazenados no nó folder no repositório CRX.

![folder_metadata_properties-1](assets/folder_metadata_properties-1.png)

## Dicas e limitações {#best-practices-limitations}

* Para importar metadados em namespaces personalizados, primeiro registre os namespaces.
* O Seletor de propriedades exibe propriedades que são usadas em editores de esquema e formulários de pesquisa. O Seletor de propriedades não seleciona propriedades de metadados de um ativo.
* Você pode ter perfis de metadados pré-existentes desde antes de atualizar para o [!DNL Experience Manager] 6.5. Após a atualização, aplique esse perfil na pasta [!UICONTROL Propriedades] em [!UICONTROL Perfis de metadados] , os campos de formulário de metadados não são exibidos. No entanto, se você aplicar um perfil de metadados recém-criado, os campos do formulário serão exibidos, mas não estarão disponíveis conforme esperado. Não há perda de funcionalidade, mas se você quiser ver os campos de formulário (indisponíveis), edite e salve os perfis de metadados existentes.

>[!MORELIKETHIS]
>
>* [Conceitos e noções básicas sobre metadados](metadata-concepts.md).
>* [Editar propriedades de metadados de várias coleções](manage-collections.md#editing-collection-metadata-in-bulk).
>* [Importação e exportação de metadados no Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/metadata-import-export.html).
>* [Perfis para processar metadados, imagens e vídeos](processing-profiles.md).
>* [Práticas recomendadas para organizar ativos digitais para usar perfis de processamento](/help/assets/organize-assets.md).
>* [Writeback XMP](/help/assets/xmp-writeback.md).

