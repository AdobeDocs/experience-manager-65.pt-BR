---
title: 'schemas de metadados para definir o layout da página de propriedades de metadados [!DNL Adobe Experience Manager Assets]. '
description: O schema de metadados define o layout da página de propriedades e as propriedades de metadados exibidas para ativos. Saiba como criar schemas de metadados personalizados, editar schemas de metadados e como aplicar schemas de metadados a ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 39066500057d364ccee57f01f045c11d634b2d0e
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 10%

---


# Esquemas de metadados {#metadata-schemas}

As organizações vêm com um modelo de metadados que aprimora a descoberta de ativos, o uso, a interoperabilidade e assim por diante. A aplicação correta de metadados é sacrossanta para manter workflows e processos orientados por metadados. Para aderir à estratégia e aos padrões de metadados de toda a organização, você pode usar schemas de metadados que ajudam os usuários do DAM a se alinhar. O Adobe Experience Manager permite que métodos fáceis e flexíveis criem, mantenham e apliquem schemas de metadados.

Em [!DNL Adobe Experience Manager Assets], os schemas contêm campos específicos para informações específicas a serem preenchidas. Ele também contém informações de layout para exibir campos de metadados de uma forma fácil de usar. As propriedades de metadados incluem título, descrição, tipos MIME, tags e muito mais. Você pode usar o editor de Formulários [!UICONTROL de Schemas de] Metadados para modificar os schemas existentes ou adicionar schemas de metadados personalizados.

Para visualização e edição da página de propriedades de um ativo, siga estas etapas:

1. Clique ou toque no ícone Propriedades **[!UICONTROL da]** Visualização em Ações rápidas no bloco de ativo em visualização de cartão.

   ![Ações rápidas no bloco de ativos](assets/chlimage_1-170.png)

   Como alternativa, selecione um ativo e clique ou toque no ícone [!UICONTROL Propriedades] na barra de ferramentas.

1. É possível editar várias propriedades de metadados nas guias disponíveis. No entanto, não é possível modificar o [!UICONTROL Tipo] de ativo na guia [!UICONTROL Básico] da página de propriedades.

   ![Guia Básica de Propriedades do ativo, na qual o tipo de ativo não pode ser alterado](assets/asset-properties-basic-tab.png)

*Figura: Guia Básico em[!UICONTROL Propriedades]do ativo.*

Para modificar o tipo MIME de um ativo, use um formulário de schema de metadados personalizado ou modifique um formulário existente. Consulte [Editar formulários](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) de Schema de metadados para obter mais informações. Se você modificar o schema de metadados de um determinado tipo MIME, o layout da página de propriedades para ativos com o tipo MIME atual e todos os subtipos de ativos serão modificados. Por exemplo, modificar um schema jpeg em `default/image` modifica somente o layout de metadados (propriedades do ativo) para ativos com tipo MIME `image/jpeg`. No entanto, se você editar o schema padrão, suas alterações modificarão o layout de metadados de todos os tipos de ativos.

## Formulários de esquema de metadados {#default-metadata-schema-forms}

Para visualização de uma lista de formulários/modelos, na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados.

[!DNL Experience Manager] fornece os seguintes modelos de formulário de Schema de metadados:

| Modelos |  | Descrição |
|---|---|---|
| [!UICONTROL default] |  | O formulário de schema de metadados base para ativos. |
|  | Os seguintes formulários filho herdam as propriedades do formulário [!UICONTROL padrão] : |  |
|  | <ul><li> [!UICONTROL image]</li></ul> | Formulário de Schema para ativos com o tipo MIME &quot;image&quot;, por exemplo, image/jpeg, image/png e assim por diante. <br> O formulário de [!UICONTROL imagem] tem os seguintes modelos de formulário filho: <ul><li> [!UICONTROL jpeg]: Formulário de Schema para ativos com subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL TIFF]: Formulário de Schema para os ativos com [!UICONTROL tiff]de subtipo.</li></ul> |
|  | <ul><li> [!UICONTROL aplicativo]</li></ul> | Formulário de Schema para ativos com tipo MIME &quot;application&quot; (aplicativo), por exemplo application/ pdf, application/ zip e assim por diante. <br>[!UICONTROL pdf]: Formulário de Schema para ativos com pdf de subtipo. |
|  | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulário de Schema para ativos com MIME tipo &quot;vídeo&quot;, como vídeo/avi, vídeo/mp4 e assim por diante. |
| [!UICONTROL collection] |  | Formulário de Schema para coleções. |
| [!UICONTROL contentfragment] |  | Formulário de Schema para fragmentos de conteúdo. |
| [!UICONTROL formulários] |  | Este formulário de schema está relacionado ao [Adobe Experience Manager Forms](/help/forms/home.md). |

>[!NOTE]
>
>Para visualização dos formulários filho de um formulário de schema, clique no nome do formulário do schema.

## Adicionar um formulário de schema de metadados {#add-a-metadata-schema-form}

1. Para adicionar um modelo personalizado à lista, clique em **[!UICONTROL Criar]** na barra de ferramentas.

   >[!NOTE]
   >
   >Os modelos não editados têm um ícone de cadeado. Se você personalizar qualquer um dos modelos, o ícone de bloqueio desaparecerá antes do modelo.

1. Na caixa de diálogo, digite o título do formulário de schema e clique em **[!UICONTROL Criar]** para concluir o processo de criação do formulário.

## Editar formulários de schema de metadados {#edit-metadata-schema-forms}

É possível editar um formulário de schema de metadados recém-adicionado ou existente. O formulário de schema de metadados inclui guias e itens de formulário dentro de guias. Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar novas guias ou itens de formulário ao formulário de schema de metadados. As guias e os itens de formulário derivados do pai estão no estado bloqueado. Não é possível alterá-los no nível da criança.

1. In the Schema Forms page, select the check box before a form and then click **[!UICONTROL Edit]** on the toolbar.

1. Na página **[!UICONTROL Editor de esquema de metadados]**, personalize a página de propriedades do ativo arrastando um ou mais componentes da lista de tipos de componentes na guia **[!UICONTROL Criar formulário]** para a guia **[!UICONTROL Básico]**.

   ![Editor de Schemas de metadados para personalizar a página Propriedades do ativo](assets/metadata-schema-editor.png)

   *Figura:[!UICONTROL Guia Básico]do editor de Schemas[!UICONTROL de]Metadados.*

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Configurações]** .

### Componentes na guia Criar formulário {#components-within-the-build-form-tab}

A guia **[!UICONTROL Criar formulário]** lista itens de formulário usados no formulário do schema. A guia **[!UICONTROL Configurações]** fornece os atributos de cada item selecionado na guia **[!UICONTROL Criar formulário]** . A tabela a seguir lista os itens de formulário disponíveis na guia **[!UICONTROL Criar formulário]** :

| Nome do componente | Descrição |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL Título da seção] | Adicione um cabeçalho de seção para uma lista de componentes comuns. |
| [!UICONTROL Texto em linha única] | Adicione uma única propriedade de texto de linha. É armazenado como uma string. |
| [!UICONTROL Texto multivalor] | Adicione uma propriedade de texto de vários valores. Ele é armazenado como uma matriz de string. |
| [!UICONTROL Número] | Adicione um componente de número. |
| [!UICONTROL Data] | Adicione um componente de data. |
| [!UICONTROL Lista suspensa] | Adicione uma lista suspensa. |
| [!UICONTROL Tags padrão] | Adicionar uma tag. |
| [!UICONTROL Tags inteligentes] | Adicione para aumentar os recursos de pesquisa adicionando automaticamente tags de metadados. |
| [!UICONTROL Campo oculto] | Adicionar um campo oculto. Ele é enviado como um parâmetro POST quando o ativo é salvo. |
| [!UICONTROL Ativo referenciado por] | Adicione esse componente à lista de visualização de ativos referenciados pelo ativo. |
| [!UICONTROL Fazer referência ao ativo] | Adicionar para exibir uma lista de ativos que fazem referência ao ativo. |
| [!UICONTROL Referências de produtos] | Adicionar para mostrar a lista de produtos vinculados ao ativo. |
| [!UICONTROL Classificação do ativo] | Adicione para exibir opções para classificar o ativo. |
| [!UICONTROL Metadados do contexto] | Adicione para controlar a exibição de outras guias de metadados na página de propriedades dos ativos. |

<!-- TBD: Check against 6.5.4.0 if the list of components is complete.
-->

#### Editar o componente de metadados {#edit-the-metadata-component}

Para editar as propriedades de um componente de metadados no formulário, clique no componente e edite todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Configurações]** .

**Rótulo** do campo: O nome da propriedade de metadados que é exibida na página de propriedades do ativo.

**Mapear para propriedade**: Essa propriedade especifica o caminho/nome relativo para o nó do ativo no qual ele é salvo no repositório CRX. Ele é start por `./` indicar que o caminho está sob o nó do ativo.

Estes são os valores válidos para esta propriedade:

* `./jcr:content/metadata/dc:title`: armazena o valor no nó de metadados do ativo como a propriedade `dc:title`.

* `./jcr:created`: Exibe a propriedade JCR no nó do ativo. Se você configurar essas propriedades nas propriedades de exibição, recomendamos marcá-las como Desativar edição, pois elas estão protegidas. Otherwise, the error [!UICONTROL Asset(s) failed to modify] results when you save the asset&#39;s properties.

Para garantir que o componente seja exibido corretamente no formulário de schema de metadados, o caminho da propriedade não deve incluir espaços.

* **Espaço reservado**: Use essa propriedade para especificar o texto relevante do espaço reservado para a propriedade metadata.
* **Obrigatório**: Use essa propriedade para marcar uma propriedade de metadados como obrigatória na página de propriedades.
* **Desabilitar edição**: Use essa propriedade para tornar uma propriedade de metadados não editável na página de propriedades.
* **Mostrar campo vazio em somente** leitura: Marque essa propriedade para exibir uma propriedade de metadados na página de propriedades, mesmo que ela não tenha valor. Por padrão, quando uma propriedade de metadados não tem valor, ela não é listada na página de propriedades.
* **Mostrar lista ordenada**: Use essa propriedade para exibir uma lista ordenada de opções
* **Opções**: Use essa propriedade para especificar opções em uma lista
* **Descrição** : Use essa propriedade para adicionar uma breve descrição para o componente de metadados.
* **Classe**: Classe de objeto à qual a propriedade está associada.
* **Excluir**: Clique em [!UICONTROL Excluir] para excluir um componente do formulário de schema.

>[!NOTE]
>
>O componente Campo  oculto não inclui esses atributos. Em vez disso, inclui propriedades, como Nome dos atributos, Valor, Rótulo do campo e Descrição. Os valores do componente Campo oculto são enviados como um parâmetro POST sempre que o ativo é salvo. Ele não é salvo como metadados para o ativo.

Se você selecionar a opção **[!UICONTROL Obrigatório]**, poderá pesquisar por ativos sem metadados obrigatórios. No painel **[!UICONTROL Filtros]**, expanda o predicado **[!UICONTROL Validação de metadados]** e selecione a opção **[!UICONTROL Inválido]**. Os resultados de pesquisa exibem ativos que não têm metadados obrigatórios configurados por meio do formulário de esquema.

![Opção inválida selecionada no predicado Validação de metadados do painel Filtros ](assets/chlimage_1-178.png)

Se você adicionar o componente Metadados contextuais a qualquer guia de qualquer formulário de schema, o componente aparecerá como uma lista na página de propriedades dos ativos aos quais o schema específico é aplicado. A lista inclui todas as outras guias, exceto a guia à qual você aplicou o componente Metadados contextuais. Atualmente, esse recurso fornece funcionalidade básica para controlar a exibição de metadados com base no contexto.

![Guia de listagem do componente Metadados contextuais das Propriedades do ativo](assets/chlimage_1-179.png)

Para exibir qualquer guia na página de propriedades, além da guia na qual o componente Metadados contextuais é aplicado, selecione a guia na lista. A guia é adicionada à página de propriedades.

![A guia selecionada na lista de Metadados contextuais é exibida na página de propriedades do ativo](assets/contextual-metadata-asset-properties.png)

*Figura: Metadados contextuais na página de propriedades do ativo.*

### Especificar propriedades no arquivo JSON {#specify-properties-in-json-file}

Em vez de especificar propriedades para as opções na guia **[!UICONTROL Configurações]**, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Caminho JSON]**.

#### Adicionar ou excluir uma guia no formulário de schema {#adding-deleting-a-tab-in-the-schema-form}

O editor de esquema permite adicionar ou excluir uma guia. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![Guias padrão no formulário de Schema de metadados](assets/chlimage_1-181.png)

Clique em `+` para adicionar uma nova guia em um formulário de schema. Por padrão, a nova guia tem o nome `Unnamed-1`. É possível modificar o nome na guia **[!UICONTROL Configurações]** .

Clique `X` para excluir uma guia.

![Adicionar ou excluir uma guia usando o Editor de Schemas de metadados](assets/chlimage_1-182.png)

## Excluir formulários de schema de metadados {#delete-metadata-schema-forms}

[!DNL Experience Manager] permite que você exclua somente formulários de schema personalizados. Isso não permite que você exclua os formulários/modelos de schema padrão. No entanto, é possível excluir quaisquer alterações personalizadas nesses formulários.

Para excluir um formulário, selecione-o e clique em Excluir.

>[!NOTE]
>
>* Depois de excluir alterações personalizadas em um formulário padrão, o ícone de cadeado reaparece antes dele na interface do Schema de Metadados para indicar que o formulário reverteu para seu estado padrão.
>* Não é possível excluir os formulários de schema de metadados prontos nos Ativos.


## Formulários de Schema para tipos MIME {#schema-forms-for-mime-types}

O Assets fornece formulários padrão para vários tipos MIME prontos para uso. No entanto, você pode adicionar formulários personalizados para ativos de vários tipos MIME.

### Adicionar novos formulários para tipos MIME {#add-new-forms-for-mime-types}

Crie um novo formulário no tipo de formulário apropriado. Por exemplo, para adicionar um novo modelo para o subtipo `image/png`, crie o formulário nos formulários &quot;image&quot;. O título do formulário de esquema é o nome do subtipo. Nesse caso, o título é `png`.

#### Usar um modelo de schema existente para vários tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Você pode usar um modelo existente para um tipo MIME diferente. Por exemplo, use o `image/jpeg` formulário para ativos do tipo MIME `image/png`.

Nesse caso, crie um novo nó `/etc/dam/metadataeditor/mimetypemappings` no repositório CRX. Especifique um nome para o nó e defina as seguintes propriedades:

| Nome | Descrição | Tipo | Valor |
|------|-------------|------|-------|
| `exposedmimetype` | Nome do formulário existente a ser mapeado | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que usam o formulário definido no `exposedmimetype` atributo | `String` | `image/png` |

Os ativos mapeiam os seguintes tipos MIME e formulários de schema:

| Formulário de Schema | Tipos MIME |
| --------------------------- | --------------------------------------------------- |
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| vídeo/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Conceder acesso a schemas de metadados {#grant-access-to-metadata-schemas}

O recurso Schema de metadados está disponível somente para administradores. No entanto, os administradores podem fornecer acesso a não administradores modificando algumas permissões. O não administrador deve ter permissões para criar, modificar e excluir na `/conf` pasta.

## Aplicar metadados específicos da pasta {#apply-folder-specific-metadata}

Os ativos permitem que você defina uma variante de um schema de metadados e aplique-o a uma pasta específica.

Por exemplo, você pode definir uma variante do schema de metadados padrão e aplicá-la a uma pasta. Quando você aplica o schema modificado, ele substitui o schema de metadados padrão original aplicado aos ativos dentro da pasta.

Somente os ativos carregados na pasta à qual esse schema é aplicado estão em conformidade com os metadados modificados definidos no schema de metadados da variante. Os ativos em outras pastas onde o schema original é aplicado continuam em conformidade com os metadados definidos no schema original.

A herança de metadados por ativos baseia-se no schema aplicado à pasta de primeiro nível na hierarquia. Em outras palavras, se uma pasta não contiver subpastas, os ativos dentro dela herdarão os metadados do schema aplicado à pasta.

Se a pasta tiver uma subpasta, os ativos dentro da subpasta herdarão os metadados do schema aplicado no nível da subpasta se um schema diferente for aplicado no nível da subpasta. No entanto, se nenhum schema ou mesmo schema for aplicado no nível da subpasta, os ativos da subpasta herdarão os metadados do schema aplicado no nível da pasta pai.

1. Na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Marque a caixa de seleção antes de um formulário, por exemplo, o formulário de metadados padrão, clique em **[!UICONTROL Copiar]** e salve-o como um formulário personalizado. Especifique um nome personalizado para o formulário, por exemplo `my_default`. Como alternativa, é possível criar um formulário personalizado.

1. Na página Formulários **[!UICONTROL de Schema de]** metadados, selecione o `my_default` formulário e clique em **[!UICONTROL Editar]**.

1. Na página Editor **[!UICONTROL de Schemas de]** metadados, adicione um campo de texto ao formulário de schema. Por exemplo, adicione um campo com a **[!UICONTROL Categoria]** da etiqueta.

   ![Campo de texto adicionado ao Editor de formulário de Schema de metadados](assets/text-field-metadata-schema-editor.png)

   *Figura: Campo de texto adicionado ao editor de formulário de schema de metadados.*

1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página Formulários **[!UICONTROL de Schema de]** metadados.
1. Clique em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.

1. Selecione a pasta na qual aplicar o schema modificado e clique em **[!UICONTROL Aplicar]**.

   ![Selecione a pasta para aplicar o Schema de metadados](assets/chlimage_1-188.png)

1. Se a pasta tiver o outro schema de metadados aplicado, será exibida uma mensagem avisando que você está prestes a substituir o schema de metadados existente. Clique em **Substituir**.
1. Clique em **OK** para fechar a mensagem de sucesso.
1. Navegue até a pasta na qual você aplicou o schema de metadados modificado.

## Definir metadados obrigatórios {#define-mandatory-metadata}

Você pode definir campos obrigatórios em nível de pasta, que é imposto aos ativos que são carregados na pasta. Se você carregar ativos com metadados ausentes para os campos obrigatórios definidos anteriormente, uma indicação visual para metadados ausentes será exibida nos ativos na visualização de cartão.

>[!NOTE]
>
>Um campo de metadados pode ser definido como obrigatório com base no valor de outro campo. Na visualização do cartão, [!DNL Experience Manager] não exibe a mensagem de aviso sobre metadados ausentes para esses campos de metadados obrigatórios.

1. Na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Salve o formulário de metadados padrão como um formulário personalizado. Por exemplo, salve-o como `my_default`.

1. Edite o formulário personalizado. Adicione um campo obrigatório. Por exemplo, adicione um campo de **[!UICONTROL Categoria]** e torne-o obrigatório.

   ![Adicionar campo obrigatório ao formulário de metadados selecionando Obrigatório na guia Regras no Editor de formulário de Schema de metadados](assets/mandatory-field-metadata-schema-editor.png)

   *Figura: Campo obrigatório no editor de formulário de schema de metadados.*

1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página Formulários **[!UICONTROL de Schema de]** metadados. Selecione o formulário e clique em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.

1. Navegue até a pasta e carregue alguns ativos com metadados ausentes para o campo obrigatório adicionado ao formulário personalizado. Uma mensagem para os metadados ausentes do campo obrigatório é exibida na visualização Cartão do ativo.

   ![Mensagem para metadados obrigatórios ausentes na visualização do cartão de ativos ao fazer upload de ativos na pasta](assets/chlimage_1-192.png)

1. (Opcional) Acesso `https://[aem_server]:[port]/system/console/components/`. Configure e ative `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` o componente que está desativado por padrão. Defina uma frequência na qual [!DNL Experience Manager] verifica a validade dos metadados nos ativos. Essa configuração adiciona uma propriedade `hasValidMetadata` a `jcr:content` ativos. Ao usar essa propriedade, [!DNL Experience Manager] é possível filtrar resultados inválidos em uma pesquisa. Se você adicionar um ativo após uma verificação, o ativo não será sinalizado `hasValidMetadata` até a próxima verificação programada. Portanto, os ativos não aparecem nos filtros de pesquisa para metadados inválidos até depois da próxima verificação programada.

   >[!CAUTION]
   >
   >As verificações de validação de metadados exigem muitos recursos e podem afetar o desempenho do seu sistema. Agendar as verificações em conformidade. Se o servidor não conseguir lidar com a carga, tente desativar esta tarefa.

<!-- TBD: Add this method to find invalid metadata in the metadata article later.
-->
