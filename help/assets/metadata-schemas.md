---
title: 'Schemas de metadados para definir o layout da página de propriedades de metadados [!DNL Adobe Experience Manager Assets]. '
description: O schema de metadados define o layout da página de propriedades e as propriedades de metadados exibidas para ativos. Saiba como criar schemas de metadados personalizados, editar schemas de metadados e como aplicar schemas de metadados a ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2cccbdea594bb9ba61e8c0f7884b724aab10b5da
workflow-type: tm+mt
source-wordcount: '3601'
ht-degree: 7%

---


# Esquemas de metadados {#metadata-schemas}

As organizações vêm com um modelo de metadados que aprimora a descoberta de ativos, o uso, a interoperabilidade e assim por diante. A aplicação correta de metadados é sacrossanta para manter workflows e processos orientados por metadados. Para aderir à estratégia e aos padrões de metadados de toda a organização, você pode usar schemas de metadados que ajudam os usuários do DAM a se alinhar. [!DNL Adobe Experience Manager] permite que métodos fáceis e flexíveis criem, mantenham e apliquem schemas de metadados.

Em [!DNL Adobe Experience Manager Assets], os schemas contêm campos específicos para informações específicas a serem preenchidas. Ele também contém informações de layout para exibir campos de metadados de uma forma fácil de usar. As propriedades de metadados incluem título, descrição, tipos MIME, tags e muito mais. Você pode usar o editor Forms [!UICONTROL do Schema] Metadados para modificar os schemas existentes ou adicionar schemas de metadados personalizados.

Para visualização e edição da página de propriedades de um ativo, siga estas etapas:

1. Clique na opção Propriedades **[!UICONTROL da]** Visualização nas ações rápidas no mosaico do ativo na visualização do cartão. Como alternativa, selecione um ativo e clique em **[!UICONTROL Propriedades]** das propriedades ![de](assets/do-not-localize/info-circle-icon.png) visualização na barra de ferramentas.

1. É possível editar as várias propriedades de metadados editáveis nas guias disponíveis. No entanto, não é possível modificar o [!UICONTROL Tipo] de ativo na guia [!UICONTROL Básico] da página de propriedades.

   ![Guia Básica de Propriedades do ativo, na qual o tipo de ativo não pode ser alterado](assets/asset-properties-basic-tab.png)

*Figura: Guia Básico em[!UICONTROL Propriedades]do ativo.*

Para modificar o tipo MIME de um ativo, use um formulário de schema de metadados personalizado ou modifique um formulário existente. Consulte [Editar Schema de metadados Forms](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) para obter mais informações. Se você modificar o schema de metadados de um tipo MIME, o layout da página de propriedades dos ativos e todos os subtipos serão modificados. Por exemplo, modificar um schema jpeg em `default/image` modifica somente o layout de metadados (propriedades do ativo) para ativos com tipo MIME `image/jpeg`. No entanto, se você editar o schema padrão, suas alterações modificarão o layout de metadados de todos os tipos de ativos.

## Metadata Schema forms {#default-metadata-schema-forms}

Para visualização de uma lista de formulários ou modelos, na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados.

[!DNL Experience Manager] fornece os seguintes modelos de formulário de Schema de metadados.

| Modelos |  | Descrição |
|---|---|---|
| [!UICONTROL default] |  | O formulário de schema de metadados base para ativos. |
|  | Os seguintes formulários filho herdam as propriedades do formulário [!UICONTROL padrão] : |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Formulário de schema para vídeos do Dynamic Media. |
|  | <ul><li>[!UICONTROL imagem]</li></ul> | Formulário de schema para imagens com o tipo MIME, como `image/jpeg` e `image/png`. <br> O formulário de [!UICONTROL imagem] tem os seguintes modelos de formulário filho: <ul><li> [!UICONTROL jpeg]: Formulário de schema para ativos com subtipo [!UICONTROL jpeg].</li> <li>[!UICONTROL TIFF]: Formulário de schema para os ativos com subtipo TIFF.</li></ul> |
|  | <ul><li>[!UICONTROL aplicativo]</li></ul> | Formulário de schema para ativos com tipo MIME, como `application/pdf` e `application/zip`. <br>[!UICONTROL pdf]: Formulário de schema para ativos com subtipo PDF. |
|  | <ul><li>[!UICONTROL vídeo]</li></ul> | Formulário de schema para ativos de vídeo com tipo MIME, como `video/avi` e `video/mp4`. |
| [!UICONTROL collection] |  | Formulário de schema para coleções. |
| [!UICONTROL contentfragment] |  | [Formulário de schema para fragmentos](/help/sites-developing/customizing-content-fragments.md)de conteúdo. |
| [!UICONTROL formulários] |  | Este formulário de schema está relacionado ao [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] |  | Formulário de schema para itens de conteúdo e ativos gerados pelo usuário integrados ao Experience Manager a partir de redes sociais. |

>[!NOTE]
>
>Para visualização dos formulários filho de um formulário de schema, clique no nome do formulário do schema.

## Adicionar um formulário de schema de metadados {#add-a-metadata-schema-form}

Para adicionar um formulário de schema de metadados, siga estas etapas:

1. Para adicionar um modelo personalizado à lista, clique em **[!UICONTROL Criar]** na barra de ferramentas.

   >[!NOTE]
   >
   >Um símbolo de cadeado é exibido com os modelos não editados. Se você personalizar um modelo, ele não será bloqueado ![bloqueado](assets/do-not-localize/lock_closed_icon.svg).

1. Na caixa de diálogo, forneça o título do formulário de schema e clique em **[!UICONTROL Criar]** para concluir o processo de criação do formulário.

## Editar formulários de schema de metadados {#edit-metadata-schema-forms}

É possível editar um formulário de schema de metadados recém-adicionado ou existente. O formulário de schema de metadados inclui guias e itens de formulário dentro de guias. Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar guias ou itens de formulário ao formulário de schema de metadados. As guias e os itens de formulário derivados do pai estão no estado bloqueado. Não é possível alterá-los no nível da criança.

1. Na página Forms [!UICONTROL do Schema de] metadados, selecione um formulário e clique em **[!UICONTROL Editar]** na barra de ferramentas.

1. Na página Editor **[!UICONTROL de formulário de Schema de]** metadados, personalize o formulário de metadados. Arraste os componentes necessários da guia **[!UICONTROL Criar formulário]** para uma das guias.

   ![Editor de Schemas de metadados para personalizar a página Propriedades do ativo](assets/metadata-schema-editor.png)

   *Figura: Uma página do Editor[!UICONTROL de formulário de Schema de]metadados com guias disponíveis.*

1. Para configurar um componente, selecione-o e modifique suas propriedades na guia **[!UICONTROL Configurações]** .

### Componentes na guia [!UICONTROL Criar formulário] {#components-within-the-build-form-tab}

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

#### Editar o componente de metadados {#edit-the-metadata-component}

Para editar as propriedades de um componente de metadados no formulário, clique no componente para editar todas ou um subconjunto das seguintes propriedades na guia **[!UICONTROL Configurações]** .

**Rótulo** do campo: O nome da propriedade de metadados que é exibida na página de propriedades do ativo.

**Mapear para propriedade**: Essa propriedade especifica o caminho relativo ou o nome do nó do ativo no qual ele é salvo no repositório CRX. Ele é start `./` para indicar que o caminho está sob o nó do ativo.

Estes são os valores válidos para esta propriedade:

* `./jcr:content/metadata/dc:title`: armazena o valor no nó de metadados do ativo como a propriedade `dc:title`.

* `./jcr:created`: Armazena a data e a hora de criação de um ativo. É uma propriedade protegida. Se você configurar essas propriedades, o Adobe recomenda marcá-las como Desativar edição.

Para garantir que o componente seja exibido corretamente no formulário de schema de metadados, o caminho da propriedade não deve incluir espaços.

* **Espaço reservado**: Use essa propriedade para especificar o texto relevante do espaço reservado para a propriedade metadata.
* **Obrigatório**: Use essa propriedade para marcar uma propriedade de metadados como obrigatória na página de propriedades.
* **Desabilitar edição**: Use essa propriedade para proibir qualquer edição em uma propriedade na página de propriedades.
* **Mostrar campo vazio em somente** leitura: Marque essa propriedade para exibir uma propriedade de metadados na página de propriedades, mesmo que ela não tenha valor. Por padrão, quando uma propriedade de metadados não tem valor, ela não é listada na página de propriedades.
* **Mostrar lista ordenada**: Use essa propriedade para exibir uma lista ordenada de opções.
* **Opções**: Use essa propriedade para especificar opções em uma lista.
* **Descrição** : Use essa propriedade para adicionar uma breve descrição para o componente de metadados.
* **Classe**: Classe de objeto à qual a propriedade está associada.
* **Excluir**: Clique em [!UICONTROL Excluir] para excluir um componente do formulário de schema.

>[!NOTE]
>
>O componente Campo  oculto não inclui esses atributos. Em vez disso, inclui propriedades, como Nome dos atributos, Valor, Rótulo do campo e Descrição. Os valores do componente Campo oculto são enviados como um parâmetro POST sempre que o ativo é salvo. Ele não é salvo como metadados para o ativo.

Se você selecionar a opção **[!UICONTROL Obrigatório]**, poderá pesquisar por ativos sem metadados obrigatórios. No painel **[!UICONTROL Filtros]**, expanda o predicado **[!UICONTROL Validação de metadados]** e selecione a opção **[!UICONTROL Inválido]**. Os resultados de pesquisa exibem ativos que não têm metadados obrigatórios configurados por meio do formulário de esquema.

![Opção selecionada no predicado Validação de metadados do painel Filtros](assets/invalid-metadata-predicate.png)

Se você adicionar o componente Metadados contextuais a qualquer guia de qualquer formulário de schema, o componente aparecerá como uma lista na página de propriedades dos ativos aos quais o schema específico é aplicado. A lista inclui todas as outras guias, exceto a guia à qual você aplicou o componente Metadados contextuais. Atualmente, esse recurso fornece funcionalidade básica para controlar a exibição de metadados com base no contexto.

![Guias de listagem de componentes de metadados contextuais das propriedades do ativo](assets/metadata-contextual-component-list.png)

Para exibir qualquer guia na página de propriedades, além da guia na qual o componente Metadados contextuais é aplicado, selecione a guia na lista. A guia é adicionada à página de propriedades.

![A guia selecionada na lista de metadados contextuais é exibida na página de propriedades do ativo](assets/contextual-metadata-asset-properties.png)

*Figura: Metadados contextuais na página de propriedades do ativo.*

### Especificar propriedades no arquivo JSON {#specify-properties-in-json-file}

Em vez de especificar propriedades para as opções na guia **[!UICONTROL Configurações]**, defina as opções em um arquivo JSON especificando pares de valores chave correspondentes. Especifique o caminho do arquivo JSON no campo **[!UICONTROL Caminho JSON]**.

#### Adicionar ou excluir uma guia no formulário de schema {#adding-deleting-a-tab-in-the-schema-form}

O editor de esquema permite adicionar ou excluir uma guia. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![Guias padrão no formulário Schema de metadados](assets/metadata-schema-form-tabs.png)

Clique em `+` para adicionar uma guia em um formulário de schema. Por padrão, a nova guia tem o nome `Unnamed-1`. É possível modificar o nome na guia **[!UICONTROL Configurações]** . Clique `X` para excluir uma guia.

![Adicionar ou excluir uma guia usando o Editor de Schemas de metadados](assets/metadata-schema-form-new-tab.png)

## Metadados em cascata {#cascading-metadata}

Ao capturar as informações de metadados de um ativo, os usuários fornecem informações nos vários campos disponíveis. É possível exibir campos de metadados específicos ou valores de campos que dependem das opções selecionadas nos outros campos. Essa exibição condicional de metadados é chamada de metadados em cascata. Em outras palavras, é possível criar uma dependência entre um campo/valor de metadados específico e um ou mais campos e/ou seus valores.

Use schemas de metadados para definir regras para exibir metadados em cascata. Por exemplo, se o schema de metadados incluir um campo de tipo de ativo, você pode definir um conjunto pertinente de campos a serem exibidos com base no tipo de ativo selecionado pelo usuário.

>[!CAUTION]
>
>Metadados em cascata não são compatíveis com Fragmentos de conteúdo.

Estes são alguns casos de uso para os quais você pode definir metadados em cascata:

* Quando a localização do usuário for obrigatória, exiba os nomes relevantes da cidade com base na escolha do país e estado pelo usuário.
* Carregue nomes de marcas pertinentes em uma lista com base na escolha do usuário para a categoria do produto.
* Alterna a visibilidade de um campo específico com base no valor especificado em outro campo. Por exemplo, exiba campos de endereço de entrega separados se o usuário desejar que a entrega seja entregue em um endereço diferente.
* Designar um campo como obrigatório com base no valor especificado em outro campo.
* Opções de alteração exibidas para um campo específico com base no valor especificado em outro campo.
* Defina o valor de metadados padrão em um campo específico com base no valor especificado em outro campo.

### Configurar metadados em cascata em [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Considere um cenário em que você deseja exibir metadados em cascata com base no tipo de ativo selecionado. Alguns exemplos

* Para um vídeo, exiba campos aplicáveis, como formato, codec, duração e assim por diante.
* Para um documento do Word ou PDF, exiba campos, como contagem de páginas, autor e assim por diante.

Independentemente do tipo de ativo escolhido, exiba as informações de direitos autorais como um campo obrigatório.

1. Na [!DNL Experience Manager] interface, vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados.
1. In the **[!UICONTROL Schema Forms]** page, select a schema form and then click **[!UICONTROL Edit]** from the toolbar to edit the schema.

   ![select_form](assets/select_form.png)

1. (Opcional) No editor de schemas de metadados, crie um novo campo para condicionalizar. Especifique um nome e um caminho de propriedade na guia **[!UICONTROL Configurações]** .

   Para criar uma nova guia, clique `+` para adicionar uma guia e, em seguida, adicionar um campo de metadados.

   ![add_tab](assets/add_tab.png)

1. Adicionar um campo Suspenso para o tipo de ativo. Especifique um nome e um caminho de propriedade na guia **[!UICONTROL Configurações]** . Adicione uma descrição opcional.

   ![asset_type_field](assets/asset_type_field.png)

1. Os pares de valores-chave são as opções fornecidas a um usuário de formulário. Você pode fornecer os pares de valor chave manualmente ou de um arquivo JSON.

   * Para especificar os valores manualmente, selecione **[!UICONTROL Adicionar manualmente]** e clique em **[!UICONTROL Adicionar escolha]** e especifique o texto e o valor da opção. Por exemplo, especifique os tipos de ativos Vídeo, PDF, Word e Imagem.

   * Para obter os valores de um arquivo JSON dinamicamente, selecione **[!UICONTROL Adicionar pelo caminho]** JSON e forneça o caminho do arquivo JSON. [!DNL Experience Manager] busca os pares de valores chave em tempo real quando o formulário é apresentado ao usuário.

   Ambas as opções são mutuamente exclusivas. Não é possível importar as opções de um arquivo JSON e editá-las manualmente.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Quando você adiciona um arquivo JSON, os pares de valor chave não são exibidos no editor de schemas de metadados, mas estão disponíveis no formulário publicado.

   >[!NOTE]
   >
   >Ao adicionar opções, se você clicar no campo Suspenso, a interface fica distorcida e a opção Excluir das opções para de funcionar. Não clique na lista suspensa até salvar as alterações. Se você enfrentar esse problema, salve o schema e abra-o novamente para continuar a edição.

1. (Opcional) Adicione os outros campos obrigatórios. Por exemplo, formato, codec e duração do tipo de ativo de vídeo.

   Da mesma forma, adicione campos dependentes para outros tipos de ativos. Por exemplo, adicione campos de contagem de páginas e autor para ativos de documento, como arquivos PDF e do Word.

   ![video_dependence_fields](assets/video_dependent_fields.png)

1. Para criar uma dependência entre o campo de tipo de ativo e outros campos, escolha o campo dependente e abra a guia **[!UICONTROL Regras]** .

   ![select_depenentfield](assets/select_dependentfield.png)

1. Under **[!UICONTROL Requirement]**, choose the **[!UICONTROL Required, based on new rule]** option.
1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >A lista suspensa com valores predefinidos manualmente pode ser usada com regras. Menus suspensos com caminho JSON configurado não podem ser usados com regras que usam valores predefinidos para aplicar condições. Se os valores forem carregados do JSON no tempo de execução, não será possível aplicar uma regra predefinida.

1. Em **[!UICONTROL Visibilidade]**, escolha **[!UICONTROL Visível, com base na nova opção de regra]**.

1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. Também escolha o valor do campo no qual criar a dependência. Nesse caso, escolha **[!UICONTROL Vídeo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Clicar em um espaço em branco (ou em qualquer outro lugar que não os valores) redefine os valores. Se isso acontecer, selecione novamente os valores.

   >[!NOTE]
   >
   >É possível aplicar as condições de **[!UICONTROL Requisito]** e **[!UICONTROL Visibilidade]** independentemente umas das outras.

1. Da mesma forma, crie uma dependência entre o valor Vídeo no campo Tipo de ativo e outros campos, como Codec e Duração.
1. Repita as etapas para criar dependência entre os ativos do documento (PDF e Word) no campo Tipo [!UICONTROL de] ativo e campos como Contagem [!UICONTROL de] página e [!UICONTROL Autor].
1. Clique em **[!UICONTROL Salvar]**. Aplique o schema de metadados a uma pasta.

1. Navegue até a pasta na qual você aplicou o Schema Metadados e abra a página de propriedades de um ativo. Dependendo de sua escolha no campo Tipo de ativo, os campos de metadados em cascata pertinentes são exibidos.

   ![Metadados em cascata para o ativo Vídeo](assets/video_asset.png)

   *Figura: Metadados em cascata para um vídeo.*

   ![Metadados em cascata para ativos de documento](assets/doc_type_fields.png)

   *Figura: Metadados em cascata para um documento.*

## Excluir formulários de schema de metadados {#delete-metadata-schema-forms}

[!DNL Experience Manager] permite que você exclua somente formulários de schema personalizados. Isso não permite que você exclua os formulários/modelos de schema padrão. No entanto, é possível excluir quaisquer alterações personalizadas nesses formulários.

Para excluir um formulário, selecione-o e clique em Excluir.

>[!NOTE]
>
>* Depois que você excluir alterações personalizadas em um formulário padrão, o bloqueio ![fechado](assets/do-not-localize/lock_closed_icon.svg) reaparecerá antes do formulário. Indica que o formulário é revertido para seu estado padrão.
>* Não é possível excluir os formulários de schema de metadados padrão em [!DNL Assets].


## Formulários de schema para tipos MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] fornece formulários padrão para vários tipos MIME prontos para uso. No entanto, você pode adicionar formulários personalizados para ativos de vários tipos MIME.

### Adicionar novos formulários para tipos MIME {#add-new-forms-for-mime-types}

Crie um formulário no tipo de formulário apropriado. For example, to add a template for the `image/png` subtype, create the form under the &quot;image&quot; forms. O título do formulário de esquema é o nome do subtipo. Nesse caso, o título é `png`.

#### Usar um modelo de schema existente para vários tipos MIME {#use-an-existing-schema-template-for-various-mime-types}

Você pode usar um modelo existente para um tipo MIME diferente. Por exemplo, use o `image/jpeg` formulário para ativos do tipo MIME `image/png`.

Nesse caso, crie um nó `/etc/dam/metadataeditor/mimetypemappings` no repositório CRX. Especifique um nome para o nó e defina as seguintes propriedades:

| Nome | Descrição | Tipo | Valor |
|------|-------------|------|-------|
| `exposedmimetype` | Nome do formulário existente a ser mapeado | `String` | `image/jpeg` |
| `mimetypes` | Lista de tipos MIME que usam o formulário definido no `exposedmimetype` atributo | `String` | `image/png` |

[!DNL Assets] mapeia os seguintes tipos MIME e formulários de schema:

| Formulário de schema | Tipos MIME |
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

O recurso Schema de metadados está disponível somente para administradores. No entanto, os administradores podem fornecer acesso a não administradores modificando algumas permissões. Forneça aos usuários não administradores permissões para criar, modificar e excluir na `/conf` pasta.

## Aplicar metadados específicos da pasta {#apply-folder-specific-metadata}

[!DNL Assets] permite definir uma variante de um schema de metadados e aplicá-la a uma pasta específica.

Por exemplo, você pode definir uma variante do schema de metadados padrão e aplicá-la a uma pasta. Quando você aplica o schema modificado, ele substitui o schema de metadados padrão original aplicado aos ativos dentro da pasta.

Somente os ativos carregados na pasta à qual esse schema é aplicado estão em conformidade com os metadados modificados definidos no schema de metadados da variante. [!DNL Assets] em outras pastas onde o schema original é aplicado, continue em conformidade com os metadados definidos no schema original.

A herança de metadados por ativos baseia-se no schema aplicado à pasta de primeiro nível na hierarquia. Em outras palavras, se uma pasta não contiver subpastas, os ativos dentro dela herdarão os metadados do schema aplicado à pasta.

Você pode aplicar um schema diferente na subpasta. Os ativos dentro de uma subpasta herdam o schema de metadados da subpasta imediata. Se nenhum schema ou mesmo schema for aplicado no nível da subpasta, seus ativos herdarão o schema da pasta pai.

1. Na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Marque a caixa de seleção antes de um formulário, por exemplo, o formulário de metadados padrão, clique em **[!UICONTROL Copiar]** e salve-o como um formulário personalizado. Especifique um nome personalizado para o formulário, por exemplo `my_default`. Como alternativa, é possível criar um formulário personalizado.

1. Na página Forms **[!UICONTROL do Schema de]** metadados, selecione o `my_default` formulário e clique em **[!UICONTROL Editar]**.

1. Na página Editor **[!UICONTROL de Schemas de]** metadados, adicione um campo de texto ao formulário de schema. Por exemplo, adicione um campo com a **[!UICONTROL Categoria]** do rótulo.

   ![Campo de texto adicionado ao Editor de formulário de Schema de metadados](assets/text-field-metadata-schema-editor.png)

   *Figura: Campo de texto adicionado ao editor de formulário de schema de metadados.*

1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página Forms **[!UICONTROL do Schema de]** metadados.
1. Clique em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.

1. Selecione a pasta na qual aplicar o schema modificado e clique em **[!UICONTROL Aplicar]**.

   ![Selecione a pasta para aplicar o Schema de metadados](assets/metadata-schema-select-folder.png)

1. Se a pasta tiver o outro schema de metadados aplicado, será exibida uma mensagem avisando que você está prestes a substituir o schema de metadados existente. Clique em **Substituir**.
1. Clique em **OK** para fechar a mensagem de sucesso.
1. Navegue até a pasta na qual você aplicou o schema de metadados modificado.

## Definir metadados obrigatórios {#define-mandatory-metadata}

Você pode definir campos obrigatórios em nível de pasta, que é imposto aos ativos que são carregados na pasta. Se você carregar ativos com metadados ausentes para os campos obrigatórios definidos anteriormente, uma indicação visual para metadados ausentes será exibida nos ativos na visualização do cartão.

>[!NOTE]
>
>Um campo de metadados pode ser definido como obrigatório com base no valor de outro campo. Na visualização do cartão, [!DNL Experience Manager] não exibe a mensagem de aviso sobre metadados ausentes para esses campos de metadados obrigatórios.

1. Na [!DNL Experience Manager] interface, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > Schemas **** de metadados. A página **[!UICONTROL Formulários de esquema de metadados]** é exibida.
1. Salve o formulário de metadados padrão como um formulário personalizado. Por exemplo, salve-o como `my_default`.

1. Edite o formulário personalizado. Adicione um campo obrigatório. Por exemplo, adicione um campo de **[!UICONTROL Categoria]** e torne-o obrigatório.

   ![Adicionar campo obrigatório ao formulário de metadados selecionando Obrigatório na guia Regras no Editor de formulário de Schema de metadados](assets/mandatory-field-metadata-schema-editor.png)

   *Figura: Campo obrigatório no editor de formulário de schema de metadados.*

1. Clique em **[!UICONTROL Salvar]**. O formulário modificado é listado na página Forms **[!UICONTROL do Schema de]** metadados. Selecione o formulário e clique em **[!UICONTROL Aplicar às pastas]** na barra de ferramentas para aplicar os metadados personalizados a uma pasta.

1. Navegue até a pasta e carregue alguns ativos com metadados ausentes para o campo obrigatório adicionado ao formulário personalizado. Uma mensagem para os metadados ausentes do campo obrigatório é exibida na visualização do cartão do ativo.

   ![Mensagem para metadados obrigatórios ausentes na visualização do cartão de ativos ao fazer upload de ativos na pasta](assets/metadata-missing-info-card-view.png)

1. (Opcional) Acesso `https://[aem_server]:[port]/system/console/components/`. Configure e ative `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` o componente que está desativado por padrão. Defina uma frequência na qual [!DNL Experience Manager] verifica a validade dos metadados nos ativos. Essa configuração adiciona uma propriedade `hasValidMetadata` a `jcr:content` ativos. [!DNL Experience Manager] usa essa propriedade para filtrar os ativos inválidos em um resultado de pesquisa. Se você adicionar um ativo após uma verificação, o ativo não será sinalizado `hasValidMetadata` até a próxima verificação programada. Portanto, os ativos não aparecem nos filtros de pesquisa para metadados inválidos até após a próxima verificação programada.

   >[!CAUTION]
   >
   >As verificações de validação de metadados consomem muitos recursos e podem afetar o desempenho do seu sistema. Agendar as verificações em conformidade. Se o servidor não conseguir lidar com a carga, tente desativar esta tarefa.

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
