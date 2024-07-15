---
title: Trabalhar com o modelo de dados de formulário
description: A Integração de dados fornece o editor de modelo de dados de formulário para configurar e trabalhar com modelos de dados de formulário.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 16b76265-9ec4-4993-9ac0-b7aef1b1e5f1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '4159'
ht-degree: 0%

---

# Trabalhar com o modelo de dados de formulário{#work-with-form-data-model}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model.html) |
| AEM 6.5 | Este artigo |

![integração de dados](do-not-localize/data-integeration.png)

O editor do modelo de dados de formulário fornece uma interface de usuário intuitiva e ferramentas para editar e configurar um modelo de dados de formulário. Usando o editor, você pode adicionar e configurar objetos de modelo de dados, propriedades e serviços a partir de fontes de dados associadas no modelo de dados de formulário. Além disso, permite criar objetos e propriedades de modelo de dados sem fontes de dados e vinculá-los aos respectivos objetos e propriedades de modelo de dados posteriormente. Você também pode gerar e editar dados de amostra para propriedades de objeto do modelo de dados que você pode usar para preencher previamente formulários adaptáveis e comunicações interativas ao visualizar. Você pode testar objetos e serviços do modelo de dados configurados em um modelo de dados de formulário para garantir que ele esteja integrado corretamente às fontes de dados.

Se você é novo na integração de dados do Forms e não configurou uma fonte de dados ou criou um modelo de dados de formulário, consulte os seguintes tópicos:

* [Integração de dados do AEM Forms](/help/forms/using/data-integration.md)
* [Configurar fontes de dados](/help/forms/using/configure-data-sources.md)
* [Criar modelo de dados de formulário](/help/forms/using/create-form-data-models.md)

Leia para obter detalhes sobre várias tarefas e configurações que podem ser executadas usando o editor de modelo de dados de formulário.

>[!NOTE]
>
>Você deve ser membro de ambos os grupos **fdm-author** e **forms-user** para poder criar e trabalhar com o modelo de dados de formulário. Entre em contato com o administrador do AEM para se tornar um membro dos grupos.

## Adicionar objetos e serviços de modelo de dados {#add-data-model-objects-and-services}

Se você criou um modelo de dados de formulário com fontes de dados, poderá usar o editor de modelo de dados de formulário para adicionar objetos e serviços de modelo de dados, configurar suas propriedades, criar associações entre objetos de modelo de dados e testar o modelo de dados de formulário e os serviços.

Você pode adicionar objetos e serviços de modelo de dados a partir das fontes de dados disponíveis no modelo de dados de formulário. Enquanto os objetos de modelo de dados adicionados aparecem na guia Modelo, os serviços adicionados aparecem na guia Serviços.

Para adicionar objetos e serviços de modelo de dados:

1. Faça logon na instância do autor do AEM, navegue até **[!UICONTROL Forms > Integrações de dados]** e abra o modelo de dados de formulário no qual deseja adicionar objetos de modelo de dados.
1. No painel Fontes de dados, expanda as fontes de dados para visualizar os objetos e serviços do modelo de dados disponíveis.
1. Selecione os objetos de modelo de dados e serviços que deseja adicionar ao modelo de dados de formulário e selecione **[!UICONTROL Adicionar selecionados]**.

   ![objetos-selecionados](assets/selected-objects.png)

   Objetos e serviços de modelo de dados selecionados

   >[!NOTE]
   >
   > Se o Modelo de dados do Forms contiver um objeto que seja uma palavra-chave reservada para o banco de dados relacional, ele poderá causar problemas de adição, atualização ou recuperação de dados. Portanto, evite usar esses objetos no Modelo de dados de formulário.

   A guia Modelo exibe uma representação gráfica de todos os objetos de modelo de dados e suas propriedades adicionadas ao modelo de dados de formulário. Cada objeto de modelo de dados é representado por uma caixa no modelo de dados de formulário.

   ![guia-modelo](assets/model-tab.png)

   A guia Modelo exibe objetos de modelo de dados adicionados

   >[!NOTE]
   >
   >É possível manter e arrastar as caixas do objeto de modelo de dados para organizá-las na área de conteúdo. Todos os objetos de modelo de dados adicionados ao modelo de dados de formulário estão esmaecidos no painel Fontes de dados.

   A guia Serviços lista os serviços adicionados.

   ![guia-serviços](assets/services-tab.png)

   A guia Serviços exibe serviços de modelo de dados

   >[!NOTE]
   >
   >Além dos serviços e dos objetos de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. Para obter mais informações, consulte [Trabalhando com propriedades de navegação de serviços OData](#work-with-navigation-properties-of-odata-services).

1. Selecione **[!UICONTROL Salvar]** para salvar o objeto de modelo de formulário.

   >[!NOTE]
   >
   >Você pode chamar os serviços configurados na guia Serviços de um modelo de dados de formulário usando as regras de formulário adaptáveis. Os serviços configurados estão disponíveis na ação Chamar serviços do editor de regras. Para obter mais informações sobre como usar esses serviços nas regras de formulário adaptáveis, consulte Chamar serviços e Definir valor das regras no [editor de regras](/help/forms/using/rule-editor.md).

## Criar objetos de modelo de dados e propriedades derivadas {#create-data-model-objects-and-child-properties}

### Criar objetos de modelo de dados {#create-data-model-objects}

Embora seja possível adicionar objetos de modelo de dados a partir de fontes de dados configuradas, você também pode criar objetos de modelo de dados ou entidades sem fontes de dados. É útil, especialmente se você não tiver configurado fontes de dados no modelo de dados de formulário.

Para criar um objeto de modelo de dados sem origens de dados:

1. Faça logon na instância do autor do AEM, navegue até **[!UICONTROL Forms > Integrações de dados]** e abra o modelo de dados de formulário no qual deseja criar um objeto ou entidade de modelo de dados.
1. Selecione **[!UICONTROL Criar Entidade]**.
1. Na caixa de diálogo Criar modelo de dados, especifique um nome para o objeto de modelo de dados e selecione **[!UICONTROL Adicionar]**. Um objeto de modelo de dados é adicionado ao modelo de dados de formulário. O objeto de modelo de dados recém-adicionado não está vinculado a uma fonte de dados e não tem propriedades conforme mostrado na imagem a seguir.

   ![nova-entidade](assets/new-entity.png)

Em seguida, você pode adicionar propriedades secundárias em objetos de modelo de dados desvinculados.

### Adicionar propriedades secundárias {#child-properties}

O editor do modelo de dados de formulário permite criar propriedades secundárias em um objeto de modelo de dados. Quando criada, a propriedade não está associada a nenhuma propriedade em uma fonte de dados. Posteriormente, você pode vincular a propriedade secundária a outra propriedade no objeto de modelo de dados contentor.

Para criar uma propriedade secundária:

1. Em um modelo de dados de formulário, selecione um objeto de modelo de dados e selecione **[!UICONTROL Criar Propriedade Filho]**.
1. Na caixa de diálogo **[!UICONTROL Criar Propriedade Filho]**, especifique um nome e um tipo de dados para a propriedade nos campos **[!UICONTROL Nome]** e **[!UICONTROL Tipo]**, respectivamente. Opcionalmente, você pode especificar um título e uma descrição para a propriedade.
1. Ative Calculado se a propriedade for uma propriedade calculada. O valor de uma propriedade calculada é avaliado com base em uma regra ou expressão. Para obter mais informações, consulte [Editar propriedades](#edit-properties).
1. Se o objeto de modelo de dados estiver vinculado a uma fonte de dados, a propriedade secundária adicionada será automaticamente vinculada à propriedade do objeto de modelo de dados pai com o mesmo nome e tipo de dados.

   Para vincular manualmente uma propriedade secundária a uma propriedade de objeto de modelo de dados, selecione o ícone de procura ao lado do campo **[!UICONTROL Referência de associação]**. A caixa de diálogo **[!UICONTROL Selecionar Objeto]** lista todas as propriedades do objeto de modelo de dados pai. Selecione uma propriedade para vincular e selecione o ícone de marca de verificação. Observe que você só pode selecionar uma propriedade com o mesmo tipo de dados que a propriedade secundária.

1. Selecione **[!UICONTROL Concluído]** para salvar a propriedade secundária e selecione **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário. A propriedade secundária agora é adicionada ao objeto de modelo de dados.

Depois de criar objetos e propriedades do modelo de dados, você pode continuar a criar formulários adaptáveis e comunicações interativas com base no modelo de dados de formulário. Posteriormente, quando as fontes de dados estiverem disponíveis e configuradas, você poderá vincular o modelo de dados de formulário às fontes de dados. A vinculação será atualizada automaticamente nos formulários adaptáveis associados e nas comunicações interativas. Para obter mais informações sobre como criar formulários adaptáveis e comunicações interativas usando o modelo de dados de formulário, consulte [Usar modelo de dados de formulário](/help/forms/using/using-form-data-model.md).

### Vincular objetos e propriedades do modelo de dados {#bind-data-model-objects-and-properties}

Quando as fontes de dados que você deseja integrar ao modelo de dados de formulário estiverem disponíveis, adicione-as ao modelo de dados de formulário conforme descrito em [Atualizar fontes de dados](/help/forms/using/create-form-data-models.md#update). Em seguida, faça o seguinte para vincular os objetos e propriedades do modelo de dados desvinculados:

1. No modelo de dados de formulário, selecione a fonte de dados não vinculada que deseja vincular a uma fonte de dados.
1. Selecione **[!UICONTROL Editar propriedades]**.
1. No painel **[!UICONTROL Editar Propriedades]**, selecione o ícone de procura ao lado do campo **[!UICONTROL Associação]**. Ele abre a caixa de diálogo **[!UICONTROL Selecionar Objeto]**, que lista fontes de dados adicionadas no modelo de dados de formulário.

   ![selecionar-objeto](assets/select-object.png)

1. Expanda a árvore de fontes de dados, selecione um objeto de modelo de dados para vincular e selecione o ícone de marca de verificação.
1. Selecione **[!UICONTROL Concluído]** para salvar as propriedades e **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário. O objeto de modelo de dados agora está vinculado a uma fonte de dados. Observe que o objeto de modelo de dados não está mais marcado como Desligado.

   ![objeto-modelo-associado](assets/bound-model-object.png)

## Configurar serviços {#configure-services}

Para ler e gravar dados de um objeto de modelo de dados, faça o seguinte para configurar serviços de leitura e gravação:

1. Marque a caixa de seleção na parte superior de um objeto de modelo de dados para selecioná-lo e selecione **[!UICONTROL Editar Propriedades]**.

   ![editar-propriedades](assets/edit-properties.png)

   Editar propriedades para configurar serviços de leitura e gravação para um objeto de modelo de dados

   A caixa de diálogo Editar propriedades é aberta.

   ![edit-properties-2](assets/edit-properties-2.png)

   Caixa de diálogo Editar propriedades

   >[!NOTE]
   >
   >Além dos serviços e dos objetos de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. Quando você adiciona uma fonte de dados de serviço OData a um Modelo de dados de formulário, há um serviço disponível no Modelo de dados de formulário para todas as propriedades de navegação em um objeto de modelo de dados. Você pode usar esse serviço para ler as propriedades de navegação do objeto de modelo de dados correspondente.
   >
   >
   >Para obter mais informações sobre como usar o serviço, consulte [Trabalhando com propriedades de navegação de serviços OData](#work-with-navigation-properties-of-odata-services).

1. Alterne **[!UICONTROL Objeto de Nível Superior]** para especificar se o objeto de modelo de dados é um objeto de modelo de nível superior.

   Os objetos de modelo de dados configurados em um modelo de dados de formulário estão disponíveis para uso na guia Objetos de modelo de dados no navegador de conteúdo de um formulário adaptável com base no modelo de dados de formulário. Quando você adiciona associação entre dois objetos de modelo de dados, o objeto de modelo de dados ao qual você está associando está aninhado sob o objeto de modelo de dados ao qual você está associando na guia Objetos de Modelo de Dados. Se o modelo de dados aninhado for um objeto de nível superior, ele também aparecerá separadamente na guia Objetos do modelo de dados. Portanto, você verá duas entradas dele, uma dentro e outra fora da hierarquia aninhada, o que pode confundir os autores de formulário. Para fazer com que o objeto de modelo de dados associado apareça somente na hierarquia aninhada, desative a propriedade Objeto de Nível Superior.

1. Selecione os serviços de Leitura e Gravação para os objetos de modelo de dados selecionados. Os argumentos para os serviços aparecem.

   ![serviços de leitura/gravação](assets/read-write-services.png)

   Serviços de leitura e gravação configurados para a fonte de dados do funcionário

1. Selecione ![aem_6_3_edit](assets/aem_6_3_edit.png) para o argumento do serviço de leitura para [vincular o argumento a um Atributo de Perfil de Usuário, Atributo de Solicitação ou valor Literal](#bindargument) e especifique o valor da associação.
1. Selecione **[!UICONTROL Concluído]** para salvar o argumento, **[!UICONTROL Concluído]** para salvar as propriedades e **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário.

### Associar argumentos do serviço de leitura {#bindargument}

Vincule o argumento do serviço de leitura a um atributo de perfil de usuário, atributo de solicitação ou valor literal com base em um valor de vinculação. O valor é passado para o serviço como um argumento para buscar detalhes associados ao valor especificado da fonte de dados.

#### Valor literal {#literal-value}

Selecione **[!UICONTROL Literal]** do menu suspenso **[!UICONTROL Associando a]** e insira um valor no campo **[!UICONTROL Valor de Associação]**. Os detalhes associados ao valor são recuperados da fonte de dados. Use essa opção para recuperar detalhes associados a um valor estático.

Neste exemplo, os detalhes associados a **4367655678**, como o valor do argumento `mobilenum`, são recuperados da fonte de dados. Os detalhes associados se você passar o valor para um argumento de número de celular poderão incluir propriedades como nome do cliente, endereço do cliente e cidade.

![Valor literal](assets/fdm_binding_literal_new.png)

#### Atributo do perfil do usuário {#user-profile-attribute}

Selecione **[!UICONTROL Atributo de Perfil de Usuário]** no menu suspenso **[!UICONTROL Associando a]** e digite o nome do atributo no campo **[!UICONTROL Valor de Associação]**. Os detalhes do usuário conectado à instância AEM são recuperados da fonte de dados com base no nome do atributo.

O nome do atributo especificado no campo **[!UICONTROL Valor de Associação]** deve incluir o caminho de associação completo até o nome do atributo do usuário. Abra o seguinte URL para acessar os detalhes do usuário no CRXDE:

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![Perfil de usuário](assets/binding_crxde_user_profile_new.png)

Neste exemplo, especifique `profile.empid` no campo **[!UICONTROL Valor de Ligação]** para o usuário `grios`.

![Editar argumento](assets/edit_argument_user_profile_new.png)

O argumento `id` pega o valor do atributo `empid` do perfil do usuário e passa-o como um argumento para o serviço de Leitura. Ele lê e retorna valores de propriedades associadas do objeto de modelo de dados de funcionário para o `empid` associado ao usuário conectado.

#### Solicitar atributo {#request-attribute}

Use o atributo de solicitação para recuperar as propriedades associadas da fonte de dados.

1. Selecione **[!UICONTROL Solicitar Atributo]** no menu suspenso **[!UICONTROL Associando a]** e insira o nome do atributo no campo **[!UICONTROL Valor de Associação]**.

1. Crie uma [sobreposição](../../../help/sites-developing/overlays.md) para o head.jsp. Para criar a sobreposição, abra o CRX DE e copie o arquivo `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` para `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   >* Se você usar um modelo estático, sobreponha o head.jsp em:
   >  `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   >* Se você usar um modelo editável, sobreponha o aftemplatedpage.jsp em:
   >  `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. Defina [!DNL paramMap] para o atributo de solicitação. Por exemplo, inclua o seguinte código no arquivo .jsp na pasta de aplicativos:

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

Por exemplo, especificar o atributo como `petid=100` na solicitação recupera propriedades associadas ao valor do atributo da fonte de dados.

## Adicionar associações {#add-associations}

Normalmente, há associações criadas entre objetos de modelo de dados em uma fonte de dados. A associação pode ser um para um ou um para muitos. Por exemplo, pode haver vários dependentes associados a um funcionário. É chamada de associação um para muitos e representada por `1:n` na linha que conecta objetos de modelo de dados associados. No entanto, se uma associação retornar um nome de funcionário exclusivo para uma determinada ID de funcionário, ela será chamada de associação um para um.

Ao adicionar objetos de modelo de dados associados em uma fonte de dados a um modelo de dados de formulário, suas associações são mantidas e exibidas como conectadas por linhas de seta. Você pode adicionar associações entre objetos de modelo de dados em diferentes fontes de dados em um modelo de dados de formulário.

>[!NOTE]
>
>As associações predefinidas em uma fonte de dados JDBC não são retidas no modelo de dados de formulário. Crie-os manualmente.

Para adicionar uma associação:

1. Marque a caixa de seleção na parte superior de um objeto de modelo de dados para selecioná-lo e selecione **[!UICONTROL Adicionar Associação]**. A caixa de diálogo Adicionar associação é aberta.

   ![adicionar-associação](assets/add-association.png)

   >[!NOTE]
   >
   >Além dos serviços e dos objetos de modelo de dados, o documento de metadados do serviço OData inclui propriedades de navegação que definem a associação entre dois objetos de modelo de dados. Você pode usar essas propriedades de navegação ao adicionar associações no Modelo de dados de formulário. Para obter mais informações, consulte [Trabalhando com propriedades de navegação de serviços OData](#work-with-navigation-properties-of-odata-services).

   A caixa de diálogo Adicionar associação é aberta.

   ![adicionar-associação-2](assets/add-association-2.png)

   Caixa de diálogo Adicionar associação

1. No painel Adicionar associação:

   * Especifique um título para a associação.
   * Selecione o tipo de associação — Um para Um ou Um para Muitos.
   * Selecione o objeto de modelo de dados ao qual associar.
   * Selecione o serviço de leitura para ler dados do objeto de modelo selecionado. O argumento do serviço de leitura é exibido. Edite para alterar o argumento, se necessário, e vincule-o à propriedade do objeto de modelo de dados a ser associado.

   No exemplo a seguir, o argumento padrão para o serviço de leitura do objeto de modelo de dados Dependentes é `dependentid`.

   ![adicionar-associação-exemplo](assets/add-association-example.png)

   O argumento padrão para o serviço de leitura Dependente é dependentid

   No entanto, o argumento deve ser uma propriedade comum entre o objeto de modelo de dados de associação, que neste exemplo é `Employeeid`. Portanto, o argumento `Employeeid` deve ser associado à propriedade `id` do objeto de modelo de dados Employee para buscar os detalhes dos dependentes associados do objeto de modelo de dados Dependents.

   ![adicionar-associação-exemplo-2](assets/add-association-example-2.png)

   Argumento e vinculação atualizados

   Selecione **[!UICONTROL Concluído]** para salvar o argumento.

1. Selecione **[!UICONTROL Concluído]** para salvar a associação e **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário.
1. Repita as etapas para criar mais associações conforme necessário.

>[!NOTE]
>
>A associação adicionada aparece na caixa de objeto de modelo de dados com o título especificado e uma linha que conecta os objetos de modelo de dados associados.
>
>Você pode editar uma associação marcando a caixa de seleção correspondente e selecionando **[!UICONTROL Editar Associação]**.

![associação adicionada](assets/added-association.png)

## Editar propriedades {#properties}

É possível editar propriedades de objetos de modelo de dados, suas propriedades e serviços adicionados ao modelo de dados de formulário.

Para editar propriedades:

1. Marque a caixa de seleção ao lado de um objeto de modelo de dados, uma propriedade ou um serviço no modelo de dados de formulário.
1. Selecione **[!UICONTROL Editar Propriedades]**. O painel **[!UICONTROL Editar Propriedades]** do objeto de modelo, propriedade ou serviço selecionado é aberto.

   * **Objeto do modelo de dados**: especifique os serviços de leitura e gravação e edite os argumentos.
   * **Propriedade**: especifique o tipo, subtipo e formato da propriedade. Você também pode especificar se a propriedade selecionada é a chave primária para o objeto de modelo de dados.
   * **Serviço**: especifique o objeto de modelo de entrada, o tipo de saída e os argumentos para o serviço. Para um serviço Get, você pode especificar se espera que ele retorne uma matriz.

   ![editar-propriedades-serviço](assets/edit-properties-service.png)

   Caixa de diálogo Editar Propriedades de um serviço get

1. Selecione **[!UICONTROL Concluído]** para salvar as propriedades e **[!UICONTROL Salvar]** para salvar o modelo de dados de formulário.

### Criar propriedades computadas {#computed}

Uma propriedade calculada é aquela cujo valor é calculado com base em uma regra ou expressão. Usando uma regra, você pode definir o valor de uma propriedade calculada como uma cadeia de caracteres literal, um número, o resultado de uma expressão matemática ou o valor de outra propriedade no modelo de dados de formulário.

Por exemplo, você pode criar uma propriedade computada **FullName** cujo valor é resultado da concatenação das propriedades **FirstName** e **LastName** existentes. Para fazer isso:

1. Crie uma propriedade com o nome `FullName` cujo tipo de dados seja String.
1. Habilite **[!UICONTROL Calculado]** e selecione **[!UICONTROL Concluído]** para criar a propriedade.

   ![computado](assets/computed.png)

   A propriedade computada FullName é criada. Observe o ícone ao lado da propriedade para descrever uma propriedade calculada.

   ![prop-computada](assets/computed-prop.png)

1. Selecione a propriedade FullName e selecione **[!UICONTROL Editar Regra]**. Uma janela do editor de regras é aberta.
1. Na janela do editor de regras, selecione **[!UICONTROL Criar]**. Uma janela de regra **[!UICONTROL Definir Valor]** é aberta.

   No menu suspenso Selecionar opção, selecione **[!UICONTROL Expressão matemática]**. Outras opções disponíveis são **[!UICONTROL Objeto de modelo de dados de formulário]** e **[!UICONTROL Cadeia de caracteres]**.

1. Na expressão matemática, selecione **[!UICONTROL FirstName]** e **[!UICONTROL LastName]** no primeiro e no segundo objetos, respectivamente. Selecione **[!UICONTROL mais]** como operador.

   Selecione **[!UICONTROL Concluído]** e **[!UICONTROL Fechar]** para fechar a janela do editor de regras. A regra é semelhante ao seguinte.

   ![regra](assets/rule.png)

1. No modelo de dados do formulário, selecione **[!UICONTROL Salvar]**. A propriedade computada está configurada.

## Trabalhar com propriedades de navegação de serviços OData {#work-with-navigation-properties-of-odata-services}

Nos serviços OData, as propriedades de navegação são usadas para definir associações entre dois objetos de modelo de dados. Essas propriedades são definidas em um tipo de entidade ou em um tipo complexo. Por exemplo, na seguinte extração do arquivo de metadados dos serviços de amostra do [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData, a entidade pessoa contém três propriedades de navegação - Friends, BestFriend e Trips.

Para obter mais informações sobre propriedades de navegação, consulte a [documentação OData](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536).

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

Quando você configura um serviço OData em um Modelo de dados de formulário, todas as propriedades de navegação em um contêiner de entidade são disponibilizadas por meio de um serviço no Modelo de dados de formulário. Neste exemplo de serviço TripPin OData, as três propriedades de navegação no contêiner de entidade `Person` podem ser lidas usando um serviço `GET LINK` no modelo de dados de formulário.

Os itens a seguir destacam o serviço `GET LINK of Person /People` no Modelo de Dados de Formulário, que é um serviço combinado para as três propriedades de navegação na entidade `Person` do serviço TripPin OData.

![nav-prop-service](assets/nav-prop-service.png)

Depois de adicionar o serviço `GET LINK` à guia Serviços no Modelo de Dados de Formulário, você poderá editar as propriedades para escolher o objeto de modelo de saída e a propriedade de navegação a ser usada no serviço. Por exemplo, o seguinte serviço `GET LINK of Person /People` no exemplo a seguir usa Trip como o objeto de modelo de saída e a propriedade de navegação como Trips.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>Os valores disponíveis no campo **Valor Padrão** do argumento **NavigationPropertyName** dependem do estado da matriz **Return?Botão de alternância**. Quando ativado, ele mostra as propriedades de navegação do tipo Coleção.

Neste exemplo, você também pode escolher o objeto de modelo de saída como Pessoa e o argumento de propriedade de navegação como Amigos ou Melhor Amigo (dependendo se **Retornar matriz?** está habilitado ou desabilitado).

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

Da mesma forma, você pode escolher um serviço `GET LINK` e configurar suas propriedades de navegação ao adicionar associações no Modelo de Dados de Formulário. No entanto, para poder selecionar uma propriedade de navegação, verifique se o **[!UICONTROL campo Associar a]** está definido como **Literal**.

![adicionar-associação-nav-prop](assets/add-association-nav-prop.png)

## Gerar e editar dados de amostra {#sample}

O editor do modelo de dados de formulário permite gerar dados de amostra para todas as propriedades do objeto de modelo de dados, incluindo propriedades computadas, em um modelo de dados de formulário. É um conjunto de valores aleatórios que estão em conformidade com o tipo de dados configurado para cada propriedade. Também é possível editar e salvar os dados, que são retidos mesmo que você gere novamente os dados de amostra.

Faça o seguinte para gerar e editar dados de amostra:

1. Abra um modelo de dados de formulário e selecione **[!UICONTROL Editar Dados de Exemplo]**. Ele gera e exibe os dados de amostra na janela Editar dados de amostra.

   ![Gerar Dados de Exemplo](assets/form_data_model_generate_sample_data_new.png)

1. Na janela **[!UICONTROL Editar Dados de Exemplo]**, edite os dados, conforme necessário, e selecione **[!UICONTROL Salvar]**.

Em seguida, você pode usar os dados de amostra para preencher e testar previamente as comunicações interativas com base no modelo de dados de formulário. Para obter mais informações, consulte [Usar modelo de dados de formulário](/help/forms/using/using-form-data-model.md).

## Testar objetos e serviços do modelo de dados {#test-data-model-objects-and-services}

O modelo de dados de formulário está configurado, mas antes de colocá-lo em uso, você pode testar se os objetos e serviços do modelo de dados configurado estão funcionando como esperado. Para testar objetos e serviços do modelo de dados:

1. Selecione um objeto de modelo de dados ou um serviço no modelo de dados de formulário e selecione **[!UICONTROL Testar Objeto de Modelo]** ou **[!UICONTROL Testar Serviço]**, respectivamente.

   A janela Testar modelo de dados do formulário é aberta.

   ![modelo-de-dados-de-teste](assets/test-data-model.png)

1. Na janela Testar modelo de dados do formulário, selecione o serviço ou objeto de modelo de dados a ser testado no painel Entrada.

1. Especifique um valor de argumento no código de teste e selecione **[!UICONTROL Teste]**. Um teste bem-sucedido retorna a saída no painel Saída.

   ![Resultados de teste](assets/test_results_form_data_model_new.png)

Da mesma forma, você pode testar outros objetos e serviços do modelo de dados de formulário.

## Validação automatizada dos dados de entrada {#automated-validation-of-input-data}

O modelo de dados de formulário valida os dados recebidos como entrada ao chamar a API DermisBridge (com base nos critérios de validação disponíveis no modelo de dados de formulário). A validação se baseia no sinalizador `ValidationOptions` definido no objeto de consulta que é usado para invocar a API.

O sinalizador pode ser definido como qualquer um dos seguintes valores:

* **COMPLETO**: o FDM executa a validação com base em todas as restrições
* **DESLIGADO**: sem validação
* **BÁSICO**: o FDM executa a validação com base nas restrições &#39;obrigatório&#39; e &#39;anulável&#39;

Se nenhum valor for definido para o sinalizador `ValidationOptions`, a validação **BASIC** será executada nos dados de entrada.

Este é um exemplo de definição do sinalizador de validação como **FULL**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>O valor fornecido para um atributo nos dados de entrada deve corresponder ao tipo de dados definido para o atributo no documento de metadados.\
>Se o valor não corresponder ao tipo de dados definido para o atributo, a API DermisBridge exibirá uma exceção independentemente do valor do sinalizador `ValidationOptions`. Se o nível de log estiver definido como Depurar, um erro será registrado no arquivo **error.log**.

O modelo de dados de formulário valida os dados de entrada com base em uma lista de restrições de tipo de dados. A lista de restrições para dados de entrada pode variar de acordo com a fonte de dados.

A tabela a seguir lista as restrições para dados de entrada com base na fonte de dados:

<table>
 <tbody> 
  <tr> 
   <td>Restrições</td> 
   <td>Descrição</td> 
   <td>Fonte de dados de entrada</td> 
  </tr> 
  <tr> 
   <td>obrigatório</td> 
   <td>Se true, o parâmetro deve ser incluído nos dados de entrada.</td> 
   <td>Swagger, WSDL e banco de dados</td> 
  </tr> 
  <tr> 
   <td>anulável</td> 
   <td>Se true, o valor do parâmetro pode ser definido como Null nos dados de entrada.</td> 
   <td>WSDL, Odata e banco de dados</td> 
  </tr> 
  <tr> 
   <td>máximo</td> 
   <td>Especifica o limite superior para valores numéricos. O valor máximo especificado como o limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>mínimo</td> 
   <td>Especifica o limite inferior para valores numéricos. O valor mínimo especificado como o limite inferior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>Especifica o limite superior para valores numéricos. O valor máximo especificado como o limite superior não deve ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>Especifica o limite inferior para valores numéricos. O valor mínimo especificado como o limite inferior não deve ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>Especifica o limite inferior para o número de caracteres incluídos em uma cadeia de caracteres. O valor mínimo especificado como o limite inferior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>Especifica o limite superior para o número de caracteres incluídos em uma cadeia. O valor máximo especificado como o limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger, WSDL, Odata e banco de dados</td> 
  </tr> 
  <tr> 
   <td>padrão</td> 
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
   <td>Especifica o número máximo de itens em uma matriz. O valor máximo especificado como o limite superior também pode ser atribuído ao parâmetro nos dados de entrada.</td> 
   <td>Swagger e WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>Se true, todos os elementos da matriz deverão ser exclusivos nos dados de entrada.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum (cadeia de caracteres)<br /> <br /> </td> 
   <td>Restringe o valor de um parâmetro nos dados de entrada a um conjunto fixo de valores de string. Deve ser uma matriz com pelo menos um elemento, em que cada elemento é exclusivo.</td> 
   <td>Swagger, WSDL e Odata</td> 
  </tr> 
  <tr> 
   <td>enum (número)<br /> <br /> </td> 
   <td>Restringe o valor de um parâmetro nos dados de entrada a um conjunto fixo de valores numéricos. Deve ser uma matriz com pelo menos um elemento, em que cada elemento é exclusivo.</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

Neste exemplo, os dados de entrada são validados com base nas restrições máxima, mínima e necessária definidas no arquivo Swagger. Os dados de entrada atendem aos critérios de validação somente se a ID do pedido estiver presente e seu valor estiver entre 1 e 10.

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

Uma exceção será exibida se os dados de entrada não atenderem aos critérios de validação. Se o nível de log estiver definido como **Depuração**, um erro será registrado no arquivo **error.log**. Por exemplo,

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## Próximas etapas {#next-steps}

Você tem um modelo de dados de formulário de trabalho que agora está pronto para uso em formulários adaptáveis e workflows de comunicações interativas. Para obter mais informações, consulte [Usar modelo de dados de formulário](/help/forms/using/using-form-data-model.md).
