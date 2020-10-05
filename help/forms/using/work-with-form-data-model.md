---
title: Trabalhar com modelo de dados de formulário
seo-title: Trabalhar com modelo de dados de formulário
description: A integração de dados fornece o editor de modelo de dados de formulário para configurar e trabalhar com modelos de dados de formulário.
seo-description: A integração de dados fornece o editor de modelo de dados de formulário para configurar e trabalhar com modelos de dados de formulário.
uuid: ed78f7f7-8123-4778-9252-89924cec09d6
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c47ef627-261e-4b4b-8846-873d3d84234b
docset: aem65
translation-type: tm+mt
source-git-commit: 39ae3d8348b0c149c047c9fb3ac2eb673b610645
workflow-type: tm+mt
source-wordcount: '4162'
ht-degree: 0%

---


# Trabalhar com modelo de dados de formulário{#work-with-form-data-model}

![integração de dados](do-not-localize/data-integeration.png)

O editor de modelo de dados de formulário fornece uma interface de usuário intuitiva e ferramentas para editar e configurar um modelo de dados de formulário. Usando o editor, você pode adicionar e configurar objetos, propriedades e serviços do modelo de dados de fontes de dados associadas no modelo de dados de formulário. Além disso, permite criar objetos e propriedades de modelo de dados sem fontes de dados e vinculá-los posteriormente aos respectivos objetos e propriedades de modelo de dados. Você também pode gerar e editar dados de amostra para propriedades de objetos de modelo de dados que podem ser usados para preencher previamente formulários adaptáveis e comunicações interativas ao visualizar. É possível testar objetos e serviços de modelo de dados configurados em um modelo de dados de formulário para garantir que eles sejam integrados corretamente às fontes de dados.

Se você for novo na integração de dados da Forms e não tiver configurado uma fonte de dados ou criado um modelo de dados de formulário, consulte os seguintes tópicos:

* [Integração de dados AEM Forms](/help/forms/using/data-integration.md)
* [Configurar fontes de dados](/help/forms/using/configure-data-sources.md)
* [Criar modelo de dados de formulário](/help/forms/using/create-form-data-models.md)

Leia para obter detalhes sobre várias tarefas e configurações que você pode executar usando o editor de modelo de dados de formulário.

>[!NOTE]
>
>Você deve ser membro de grupos de **fdm-author** e de usuários **de** formulários para poder criar e trabalhar com modelo de dados de formulário. Entre em contato com o administrador do AEM para se tornar membro dos grupos.

## Adicionar objetos e serviços do modelo de dados {#add-data-model-objects-and-services}

Se você tiver criado um modelo de dados de formulário com fontes de dados, poderá usar o editor de modelo de dados de formulário para adicionar objetos e serviços de modelo de dados, configurar suas propriedades, criar associações entre objetos de modelo de dados e testar o modelo e os serviços de dados de formulário.

É possível adicionar objetos e serviços de modelo de dados de fontes de dados disponíveis no modelo de dados de formulário. Enquanto objetos de modelo de dados adicionados aparecem na guia Modelo, os serviços adicionados aparecem na guia Serviços.

Para adicionar objetos e serviços de modelo de dados:

1. Faça logon na instância AEM autor, navegue até **[!UICONTROL Forms > Integrações]** de dados e abra o modelo de dados de formulário no qual deseja adicionar objetos de modelo de dados.
1. No painel Fontes de dados, expanda as fontes de dados para visualização de objetos e serviços de modelo de dados disponíveis.
1. Selecione os objetos e serviços do modelo de dados que deseja adicionar ao modelo de dados do formulário e toque em **[!UICONTROL Adicionar selecionados]**.

   ![objetos selecionados](assets/selected-objects.png)

   Objetos e serviços do modelo de dados selecionado

   A guia Modelo exibe uma representação gráfica de todos os objetos do modelo de dados e suas propriedades adicionadas ao modelo de dados do formulário. Cada objeto de modelo de dados é representado por uma caixa no modelo de dados de formulário.

   ![guia modelo](assets/model-tab.png)

   A guia Modelo exibe objetos de modelo de dados adicionados

   >[!NOTE]
   >
   >É possível manter e arrastar caixas de objetos de modelo de dados ao redor para organizá-las na área de conteúdo. Todos os objetos de modelo de dados adicionados no modelo de dados de formulário ficam acinzentados no painel Fontes de Dados.

   A guia Serviços lista serviços adicionados.

   ![guia Serviços](assets/services-tab.png)

   A guia Serviços exibe os serviços de modelo de dados

   >[!NOTE]
   >
   >Além de objetos e serviços de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. Para obter mais informações, consulte [Trabalhar com propriedades de navegação dos serviços](#navigation-properties-odata)OData.

1. Toque em **[!UICONTROL Salvar]** para salvar o objeto de modelo de formulário.

   >[!NOTE]
   >
   >Você pode chamar os serviços configurados na guia Serviços de um modelo de dados de formulário usando as regras de formulário adaptáveis. Os serviços configurados estão disponíveis na ação Invocar serviços do editor de regras. Para obter mais informações sobre como usar esses serviços em regras de formulário adaptáveis, consulte Invocar serviços e Definir valor de regras no editor [de](/help/forms/using/rule-editor.md)regras.

## Criar objetos de modelo de dados e propriedades secundárias {#create-data-model-objects-and-child-properties}

### Criar objetos de modelo de dados {#create-data-model-objects}

Embora seja possível adicionar objetos de modelo de dados de fontes de dados configuradas, também é possível criar objetos de modelo de dados ou entidades sem fontes de dados. É útil principalmente se você não tiver configurado fontes de dados no modelo de dados de formulário.

Para criar um objeto de modelo de dados sem fontes de dados:

1. Faça logon na instância do autor AEM, navegue até **[!UICONTROL Forms > Integrações]** de dados e abra o modelo de dados do formulário no qual você deseja criar um objeto ou entidade de modelo de dados.
1. Toque em **[!UICONTROL Criar entidade]**.
1. Na caixa de diálogo Criar modelo de dados, especifique um nome para o objeto de modelo de dados e toque em **[!UICONTROL Adicionar]**. Um objeto de modelo de dados é adicionado ao modelo de dados do formulário. Observe que o objeto de modelo de dados recém-adicionado não está vinculado a uma fonte de dados e não tem nenhuma propriedade, como mostrado na imagem a seguir.

   ![nova entidade](assets/new-entity.png)

Em seguida, é possível adicionar propriedades secundárias em objetos de modelo de dados não vinculados.

### Adicionar propriedades secundárias {#child-properties}

O editor de modelo de dados de formulário permite criar propriedades secundárias em um objeto de modelo de dados. A propriedade quando criada não está vinculada a nenhuma propriedade em uma fonte de dados. Posteriormente, é possível vincular a propriedade filho a outra propriedade no objeto de modelo de dados contêiner.

Para criar uma propriedade filho:

1. Em um modelo de dados de formulário, selecione um objeto de modelo de dados e toque em **[!UICONTROL Criar propriedade]** secundária.
1. Na caixa de diálogo **[!UICONTROL Criar propriedade]** secundária, especifique um nome e um tipo de dados para a propriedade nos campos **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** , respectivamente. Como opção, você pode especificar um título e uma descrição para a propriedade.
1. Ative Calculado se a propriedade for uma propriedade calculada. O valor de uma propriedade calculada é avaliado com base em uma regra ou expressão. Para obter mais informações, consulte [Editar propriedades](#edit-properties).
1. Se o objeto de modelo de dados estiver vinculado a uma fonte de dados, a propriedade filho adicionada será automaticamente vinculada à propriedade do objeto de modelo de dados pai com o mesmo nome e tipo de dados.

   Para vincular manualmente uma propriedade filho a uma propriedade de objeto de modelo de dados, toque no ícone Procurar ao lado do campo **[!UICONTROL Vincular referência]** . A caixa de diálogo **[!UICONTROL Selecionar objeto]** lista todas as propriedades do objeto de modelo de dados pai. Selecione uma propriedade com a qual vincular e toque no ícone de marca de verificação. Observe que você só pode selecionar uma propriedade do mesmo tipo de dados que a propriedade filho.

1. Toque em **[!UICONTROL Concluído]** para salvar a propriedade filho e toque em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário. A propriedade filho agora é adicionada ao objeto de modelo de dados.

Depois de criar objetos e propriedades do modelo de dados, você pode continuar a criar formulários adaptáveis e comunicações interativas com base no modelo de dados do formulário. Posteriormente, quando fontes de dados estão disponíveis e configuradas, é possível vincular o modelo de dados de formulário a fontes de dados. O vínculo será atualizado automaticamente nos formulários adaptativos associados e nas comunicações interativas. Para obter mais informações sobre como criar formulários adaptáveis e comunicações interativas usando o modelo de dados de formulário, consulte [Usar o modelo](/help/forms/using/using-form-data-model.md)de dados de formulário.

### Vincular objetos e propriedades do modelo de dados {#bind-data-model-objects-and-properties}

Quando as fontes de dados que você deseja integrar ao modelo de dados do formulário estiverem disponíveis, é possível adicioná-las ao modelo de dados do formulário conforme descrito em [Atualizar fontes](/help/forms/using/create-form-data-models.md#update)de dados. Em seguida, faça o seguinte para vincular os objetos e as propriedades do modelo de dados não vinculados:

1. No modelo de dados de formulário, selecione a fonte de dados não vinculada que deseja vincular a uma fonte de dados.
1. Toque em **[!UICONTROL Editar propriedades]**.
1. No painel **[!UICONTROL Editar propriedades]** , toque no ícone Procurar ao lado do campo **[!UICONTROL Vínculo]** . Ele abre a caixa de diálogo **[!UICONTROL Selecionar objeto]** que lista as fontes de dados adicionadas no modelo de dados do formulário.

   ![select-object](assets/select-object.png)

1. Expanda a árvore de fontes de dados e selecione um objeto de modelo de dados ao qual vincular e toque no ícone de verificação.
1. Toque em **[!UICONTROL Concluído]** para salvar as propriedades e toque em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário. O objeto de modelo de dados agora está vinculado a uma fonte de dados. Observe que o objeto de modelo de dados não está mais marcado como Não vinculado.

   ![bound-model-object](assets/bound-model-object.png)

## Configurar serviços {#configure-services}

Para ler e gravar dados de um objeto de modelo de dados, faça o seguinte para configurar os serviços de leitura e gravação:

1. Marque a caixa de seleção na parte superior de um objeto de modelo de dados para selecioná-lo e toque em **[!UICONTROL Editar propriedades]**.

   ![edit-properties](assets/edit-properties.png)

   Editar propriedades para configurar serviços de leitura e gravação para um objeto de modelo de dados

   A caixa de diálogo Editar propriedades é aberta.

   ![edit-properties-2](assets/edit-properties-2.png)

   Caixa de diálogo Editar propriedades

   >[!NOTE]
   >
   >Além de objetos e serviços de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. Quando você adiciona uma fonte de dados de serviço OData a um Modelo de dados de formulário, há um serviço disponível no Modelo de dados de formulário para todas as propriedades de navegação em um objeto de modelo de dados. Você pode usar esse serviço para ler as propriedades de navegação do objeto de modelo de dados correspondente.
   >
   >
   >Para obter mais informações sobre como usar o serviço, consulte [Trabalhar com propriedades de navegação dos serviços](#navigation-properties-odata)OData.

1. Alterne o objeto **[!UICONTROL de nível]** superior para especificar se o objeto de modelo de dados é um objeto de modelo de nível superior.

   Objetos de modelo de dados configurados em um modelo de dados de formulário estão disponíveis para uso na guia Objetos de modelo de dados no navegador Conteúdo de um formulário adaptável com base no modelo de dados de formulário. Quando você adiciona associação entre dois objetos de modelo de dados, o objeto de modelo de dados ao qual você está associado é aninhado sob o objeto de modelo de dados ao qual você está associando na guia Objetos de modelo de dados. Se o modelo de dados aninhado for um objeto de nível superior, ele também será exibido separadamente na guia Objetos do modelo de dados. Portanto, você verá duas entradas dela, uma dentro e outra fora da hierarquia aninhada, o que pode confundir os autores de formulários. Para fazer com que o objeto de modelo de dados associado apareça apenas na hierarquia aninhada, desative a propriedade Objeto de nível superior.

1. Selecione Serviços de leitura e gravação para os objetos de modelo de dados selecionados. Os argumentos para os serviços são exibidos.

   ![serviços de leitura/gravação](assets/read-write-services.png)

   Serviços de leitura e gravação configurados para a fonte de dados do funcionário

1. Toque em ![aem_6_3_edit](assets/aem_6_3_edit.png) para que o argumento do serviço de leitura [vincule o argumento a um Atributo de Perfil do usuário, Atributo de solicitação ou valor](#bindargument) literal e especifique o valor de vínculo.
1. Toque em **[!UICONTROL Concluído]** para salvar o argumento, **[!UICONTROL Concluído]** para salvar as propriedades e, em seguida, em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

### Argumentos do serviço de Leitura de Ligação {#bindargument}

Vincule o argumento do serviço de Leitura a um Atributo do Perfil do usuário, Atributo de solicitação ou valor Literal com base em um valor de vínculo. O valor é passado para o serviço como um argumento para buscar detalhes associados ao valor especificado na fonte de dados.

#### Literal value {#literal-value}

Selecione **[!UICONTROL Literal]** no menu suspenso **[!UICONTROL Vínculo]** e insira um valor no campo Valor **[!UICONTROL de]** Vínculo. Os detalhes associados ao valor são recuperados da fonte de dados. Use essa opção para recuperar detalhes associados a um valor estático.

Neste exemplo, os detalhes associados ao **4367655678**, como o valor do `mobilenum` argumento, são recuperados da fonte de dados. Os detalhes associados se você passar o valor para um argumento de número de celular podem incluir propriedades como nome do cliente, endereço do cliente e cidade.

![Valor literal](assets/fdm_binding_literal_new.png)

#### Atributo do perfil do usuário {#user-profile-attribute}

Selecione Atributo **[!UICONTROL de Perfil de]** usuário no menu suspenso **[!UICONTROL Vínculo]** e digite o nome do atributo no campo Valor **[!UICONTROL de]** vínculo. Os detalhes do usuário conectado à instância AEM são recuperados da fonte de dados com base no nome do atributo.

O nome do atributo especificado no campo Valor **[!UICONTROL de]** Vínculo deve incluir o caminho de vínculo completo até o nome do atributo do usuário. Abra o seguinte URL para acessar os detalhes do usuário no CRXDE:

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![Perfil de usuário](assets/binding_crxde_user_profile_new.png)

Neste exemplo, especifique `profile.empid` o campo Valor **[!UICONTROL de]** vínculo para o `grios` usuário.

![Editar argumento](assets/edit_argument_user_profile_new.png)

O `id` argumento pega o valor do `empid` atributo do perfil do usuário e o envia como um argumento para o serviço de Leitura. Ele lê e retorna valores de propriedades associadas do objeto de modelo de dados do funcionário para o `empid` associado ao usuário conectado.

#### Solicitar atributo {#request-attribute}

Use o atributo request para recuperar as propriedades associadas da fonte de dados.

1. Selecione Atributo **[!UICONTROL de]** solicitação no menu suspenso **[!UICONTROL Vínculo para]** e digite o nome do atributo no campo Valor **[!UICONTROL de]** vínculo.

1. Crie uma [sobreposição](../../../help/sites-developing/overlays.md) para head.jsp. Para criar a sobreposição, abra o CRX DE e copie o arquivo para `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   > * Se você usar um modelo estático, sobreponha head.jsp em:
/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp
   > * Se você usar um modelo editável, sobreponha aftemplatedpage.jsp em:
/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp


1. Defina [!DNL paramMap] para o atributo de solicitação. Por exemplo, inclua o seguinte código no arquivo .jsp na pasta apps:

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   Por exemplo, use o código abaixo para recuperar o valor de petid da fonte de dados:


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

Os detalhes são recuperados da fonte de dados com base no nome do atributo especificado na solicitação.

Por exemplo, especificar o atributo como `petid=100` na solicitação recupera as propriedades associadas ao valor do atributo da fonte de dados.

## Adicionar associações {#add-associations}

Normalmente, há associações criadas entre objetos de modelo de dados em uma fonte de dados. A associação pode ser um para um ou um para muitos. Por exemplo, pode haver vários dependentes associados a um funcionário. É chamada de associação de um para muitos e representada por `1:n` na linha que conecta objetos de modelo de dados associados. No entanto, se uma associação retornar um nome de funcionário exclusivo para uma determinada ID de funcionário, ela será chamada de associação de um para um.

Quando objetos de modelo de dados associados são adicionados em uma fonte de dados a um modelo de dados de formulário, suas associações são mantidas e exibidas como conectadas por linhas de seta. É possível adicionar associações entre objetos de modelo de dados em diferentes fontes de dados em um modelo de dados de formulário.

>[!NOTE]
>
>As associações predefinidas em uma fonte de dados JDBC não são retidas no modelo de dados de formulário. Você deve criá-los manualmente.

Para adicionar uma associação:

1. Marque a caixa de seleção na parte superior de um objeto de modelo de dados para selecioná-lo e toque em **[!UICONTROL Adicionar associação]**. A caixa de diálogo Adicionar associação é aberta.

   ![associação de suplementos](assets/add-association.png)

   >[!NOTE]
   >
   >Além de objetos e serviços de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. É possível usar essas propriedades de navegação ao adicionar associações no Modelo de dados de formulário. Para obter mais informações, consulte [Trabalhar com propriedades de navegação dos serviços](#navigation-properties-odata)OData.

   A caixa de diálogo Adicionar associação é aberta.

   ![add-Association-2](assets/add-association-2.png)

   Caixa de diálogo Adicionar associação

1. No painel Adicionar associação:

   * Especifique um título para a associação.
   * Selecione o tipo de associação — Um para um ou um para muitos.
   * Selecione o objeto de modelo de dados ao qual associar.
   * Selecione o serviço de leitura para ler dados do objeto de modelo selecionado. O argumento read service é exibido. Edite para alterar o argumento, se necessário, e vincule-o à propriedade do objeto de modelo de dados a ser associado.

   No exemplo a seguir, o argumento padrão para o serviço de leitura do objeto de modelo de dados Dependents é `dependentid`.

   ![add-Association-example](assets/add-association-example.png)

   O argumento padrão para o serviço de leitura Dependentes é dependente

   No entanto, o argumento deve ser uma propriedade comum entre o objeto de modelo de dados associado, que neste exemplo é `Employeeid`. Portanto, o `Employeeid` argumento deve ser vinculado à `id` propriedade do objeto de modelo de dados Funcionário para buscar os detalhes dos dependentes associados do objeto de modelo de dados Dependentes.

   ![add-Association-example-2](assets/add-association-example-2.png)

   Argumento e vínculo atualizados

   Toque em **[!UICONTROL Concluído]** para salvar o argumento.

1. Toque em **[!UICONTROL Concluído]** para salvar a associação e, em seguida, em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.
1. Repita as etapas para criar mais associações, conforme necessário.

>[!NOTE]
>
>A associação adicionada é exibida na caixa de objetos de modelo de dados com o título especificado e uma linha que conecta os objetos de modelo de dados associados.
>
>Você pode editar uma associação marcando a caixa de seleção e tocando em **[!UICONTROL Editar associação]**.

![associação adicionada](assets/added-association.png)

## Editar propriedades {#properties}

É possível editar propriedades de objetos de modelo de dados, suas propriedades e serviços adicionados no modelo de dados de formulário.

Para editar propriedades:

1. Marque a caixa de seleção ao lado de um objeto de modelo de dados, uma propriedade ou um serviço no modelo de dados de formulário.
1. Toque em **[!UICONTROL Editar propriedades]**. O painel **[!UICONTROL Editar propriedades]** do objeto, propriedade ou serviço de modelo selecionado é aberto.

   * **Objeto** de modelo de dados: Especifique os serviços de leitura e gravação e edite argumentos.
   * **Propriedade**: Especifique o tipo, o subtipo e o formato da propriedade. Você também pode especificar se a propriedade selecionada é a chave primária para o objeto de modelo de dados.
   * **Serviço**: Especifique o objeto do modelo de entrada, o tipo de saída e os argumentos para o serviço. Para um serviço Get, você pode especificar se é esperado que ele retorne uma matriz.

   ![edit-properties-service](assets/edit-properties-service.png)

   Caixa de diálogo Editar propriedades para um serviço get

1. Toque em **[!UICONTROL Concluído]** para salvar as propriedades e em **[!UICONTROL Salvar]** para salvar o modelo de dados do formulário.

### Criar propriedades calculadas {#computed}

Uma propriedade calculada é aquela cujo valor é calculado com base em uma regra ou expressão. Usando uma regra, é possível definir o valor de uma propriedade calculada como uma string literal, um número, resultado de uma expressão matemática ou o valor de outra propriedade no modelo de dados de formulário.

Por exemplo, você pode criar uma propriedade calculada **FullName** cujo valor é resultado da concatenação das propriedades **FirstName** e **LastName** existentes. Para isso:

1. Crie uma nova propriedade com o nome `FullName` cujo tipo de dados é String.
1. Ative **[!UICONTROL Calculado]** e toque em **[!UICONTROL Concluído]** para criar a propriedade.

   ![calculado](assets/computed.png)

   A propriedade calculada FullName é criada. Observe o ícone ao lado da propriedade para descrever uma propriedade calculada.

   ![computed-prop](assets/computed-prop.png)

1. Selecione a propriedade FullName e toque em **[!UICONTROL Editar regra]**. Uma janela do editor de regras é aberta.
1. Na janela do editor de regras, toque em **[!UICONTROL Criar]**. Uma janela de regra **[!UICONTROL Definir valor]** é aberta.

   Na lista suspensa Selecionar opção, selecione Expressão **[!UICONTROL matemática]**. Outras opções disponíveis são Objeto **[!UICONTROL e]** String **[!UICONTROL do Modelo de dados de]** formulário.

1. Na expressão matemática, selecione **[!UICONTROL FirstName]** e **[!UICONTROL LastName]** no primeiro e segundo objetos, respectivamente. Selecione **[!UICONTROL mais]** como operador.

   Toque em **[!UICONTROL Concluído]** e, em seguida, toque em **[!UICONTROL Fechar]** para fechar a janela do editor de regras. A regra é semelhante ao seguinte.

   ![regra](assets/rule.png)

1. No modelo de dados de formulário, toque em **[!UICONTROL Salvar]**. A propriedade calculada está configurada.

## Trabalhar com propriedades de navegação de serviços OData {#work-with-navigation-properties-of-odata-services}

Nos serviços OData, as propriedades de navegação são usadas para definir associações entre dois objetos de modelo de dados. Essas propriedades são definidas em um tipo de entidade ou complexo. Por exemplo, na seguinte extração do arquivo de metadados dos serviços de amostra [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData, a entidade da pessoa contém três propriedades de navegação - Amigos, Melhor Amigo e Percursos.

Para obter mais informações sobre propriedades de navegação, consulte a documentação [](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)OData.

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

Quando você configura um serviço OData em um Modelo de dados de formulário, todas as propriedades de navegação em um container de entidade são disponibilizadas por meio de um serviço no Modelo de dados de formulário. Neste exemplo do serviço OData do TripPin, as três propriedades de navegação no container da `Person` entidade podem ser lidas usando um `GET LINK` serviço no Modelo de dados de formulário.

O seguinte destaca o `GET LINK of Person /People` serviço no Modelo de dados de formulário, que é um serviço combinado para as três propriedades de navegação na `Person` entidade do serviço OData do TripPin.

![nav-prop-service](assets/nav-prop-service.png)

Após adicionar o `GET LINK` serviço à guia Serviços no Modelo de dados de formulário, é possível editar as propriedades para escolher o objeto de modelo de saída e a propriedade de navegação a ser usada no serviço. Por exemplo, o `GET LINK of Person /People` serviço a seguir no exemplo a seguir usa o Trip como objeto de modelo de saída e a propriedade de navegação como Trips.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>Os valores disponíveis no campo Valor **** padrão do argumento **NavigationPropertyName** dependem do estado da matriz **Return?** botão de alternância. Quando ativado, mostra as propriedades de navegação do tipo Coleção.

Neste exemplo, você também pode escolher o objeto de modelo de saída como Pessoa e argumento de propriedade de navegação como Amigos ou Melhor Amigo (dependendo se a matriz **Retornar?** está ativado ou desativado).

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

Da mesma forma, você pode escolher um `GET LINK` serviço e configurar suas propriedades de navegação ao adicionar associações no Modelo de dados de formulário. No entanto, para poder selecionar uma propriedade de navegação, verifique se o campo **[!UICONTROL Vínculo a está definido como]** Literal ****.

![add-Association-nav-prop](assets/add-association-nav-prop.png)

## Gerar e editar dados de amostra {#sample}

O editor de modelo de dados de formulário permite gerar dados de amostra para todas as propriedades de objetos de modelo de dados, incluindo propriedades calculadas, em um modelo de dados de formulário. É um conjunto de valores aleatórios que está em conformidade com o tipo de dados configurado para cada propriedade. Também é possível editar e salvar dados, que são retidos mesmo se os dados de amostra forem regenerados.

Faça o seguinte para gerar e editar dados de amostra:

1. Abra um modelo de dados de formulário e toque em **[!UICONTROL Editar dados]** de amostra. Ele gera e exibe os dados de amostra na janela Editar dados de amostra.

   ![Gerar dados de amostra](assets/form_data_model_generate_sample_data_new.png)

1. Na janela **[!UICONTROL Editar dados]** de amostra, edite os dados, conforme necessário, e toque em **[!UICONTROL Salvar]**.

Em seguida, é possível usar os dados de amostra para pré-preencher e testar as comunicações interativas com base no modelo de dados do formulário. Para obter mais informações, consulte [Usar modelo](/help/forms/using/using-form-data-model.md)de dados de formulário.

## Testar objetos e serviços do modelo de dados {#test-data-model-objects-and-services}

Seu modelo de dados de formulário está configurado, mas antes de colocá-lo em uso, talvez você queira testar se os objetos e serviços do modelo de dados configurados estão funcionando como esperado. Para testar objetos e serviços do modelo de dados:

1. Selecione um objeto de modelo de dados ou um serviço no modelo de dados de formulário e toque em **[!UICONTROL Testar objeto]** de modelo ou **[!UICONTROL Testar serviço]**, respectivamente.

   A janela Testar modelo de dados do formulário é aberta.

   ![test-data-model](assets/test-data-model.png)

1. Na janela Testar modelo de dados de formulário, selecione o objeto ou serviço de modelo de dados a ser testado no painel Entrada.

1. Especifique um valor de argumento no código de teste e toque em **[!UICONTROL Testar]**. Um teste bem-sucedido retorna a saída no painel Saída.

   ![Resultados de teste](assets/test_results_form_data_model_new.png)

Da mesma forma, é possível testar outros objetos e serviços de modelo de dados no modelo de dados de formulário.

## Validação automatizada dos dados de entrada {#automated-validation-of-input-data}

O modelo de dados de formulário valida os dados recebidos como entrada enquanto invoca a API do DermisBridge (com base nos critérios de validação disponíveis no modelo de dados de formulário). A validação se baseia no sinalizador `ValidationOptions` definido no objeto de query usado para chamar a API.

O sinalizador pode ser definido para qualquer um dos seguintes valores:

* **COMPLETO**: O FDM realiza a validação com base em todas as restrições
* **DESLIGADO**: Nenhuma validação
* **BÁSICO**: O FDM realiza a validação com base em restrições &quot;obrigatórias&quot; e &quot;anuláveis&quot;

Se nenhum valor for definido para o `ValidationOptions`sinalizador, a validação **BASIC** será realizada nos dados de entrada.

Este é um exemplo de como configurar o sinalizador de validação como **FULL**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>O valor fornecido para um atributo nos dados de entrada deve corresponder ao tipo de dados definido para o atributo no documento de metadados.\
>Se o valor não corresponder ao tipo de dados definido para o atributo, a API DermisBridge exibirá uma exceção independentemente do valor do `ValidationOptions` sinalizador. Se o nível de log estiver definido como Depuração, um erro será registrado no arquivo **error.log** .

O modelo de dados de formulário valida os dados de entrada com base em uma lista de restrições de tipo de dados. A lista de restrições para dados de entrada pode variar com base na fonte de dados.

A tabela a seguir lista as restrições para dados de entrada com base na fonte de dados:

<table>
 <tbody> 
  <tr> 
   <td>Restrições</td> 
   <td>Descrição</td> 
   <td>Fonte de dados de entrada</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>Se verdadeiro, o parâmetro deve ser incluído nos dados de entrada.</td> 
   <td>Swagger, WSDL e banco de dados</td> 
  </tr> 
  <tr> 
   <td>nulo</td> 
   <td>Se verdadeiro, o valor do parâmetro pode ser definido como Nulo nos dados de entrada.</td> 
   <td>WSDL, Odata e banco de dados</td> 
  </tr> 
  <tr> 
   <td>maximum</td> 
   <td>Especifica o limite superior para valores numéricos. O valor máximo especificado como limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>mínimo</td> 
   <td>Especifica o limite inferior para valores numéricos. O valor mínimo especificado como o limite inferior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>excludeMaximum</td> 
   <td>Especifica o limite superior para valores numéricos. O valor máximo especificado como limite superior não deve ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueMinimum</td> 
   <td>Especifica o limite inferior para valores numéricos. O valor mínimo especificado como o limite inferior não deve ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>Especifica o limite inferior para o número de caracteres incluídos em uma string. O valor mínimo especificado como o limite inferior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>Especifica o limite superior para o número de caracteres incluídos em uma string. O valor máximo especificado como limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger, WSDL, Odata e banco de dados</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>Especifica uma sequência fixa de caracteres. A cadeia de caracteres de entrada é validada com êxito somente se os caracteres estiverem em conformidade com o padrão especificado.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>Especifica o número mínimo de itens em uma matriz. O valor mínimo especificado como o limite inferior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>Especifica o número máximo de itens em uma matriz. O valor máximo especificado como limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>Se verdadeiro, todos os elementos da matriz devem ser exclusivos nos dados de entrada.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum (string)<br /> <br /> </td> 
   <td>Restringe o valor de um parâmetro nos dados de entrada a um conjunto fixo de valores de string. Deve ser um storage com pelo menos um elemento, em que cada elemento é único.</td> 
   <td>Swagger, WSDL e Odata</td> 
  </tr> 
  <tr> 
   <td>enum (número)<br /> <br /> </td> 
   <td>Restringe o valor de um parâmetro nos dados de entrada a um conjunto fixo de valores numéricos. Deve ser um storage com pelo menos um elemento, em que cada elemento é único.</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

Neste exemplo, os dados de entrada são validados com base em restrições máximas, mínimas e obrigatórias definidas no arquivo Swagger. Os dados de entrada atendem aos critérios de validação somente se a ID do pedido estiver presente e seu valor estiver entre 1 e 10.

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

Uma exceção será exibida se os dados de entrada não atenderem aos critérios de validação. Se o nível de log estiver definido como **Depuração**, um erro será registrado no arquivo **error.log** . Por exemplo,

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## Próximos passos {#next-steps}

Você tem um modelo de dados de formulário que agora está pronto para uso em formulários adaptáveis e workflows de comunicação interativos. Para obter mais informações, consulte [Usar modelo](/help/forms/using/using-form-data-model.md)de dados de formulário.
