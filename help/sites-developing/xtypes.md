---
title: Uso de xtypes (interface clássica)
seo-title: Uso de xtypes (interface clássica)
description: Saiba mais sobre todos os xtypes disponíveis com AEM
seo-description: Saiba mais sobre todos os xtypes disponíveis com AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '6414'
ht-degree: 0%

---


# Uso de xtypes (interface clássica){#using-xtypes-classic-ui}

Esta página descreve todos os xtypes que estão disponíveis com o Adobe Experience Manager (AEM).

Na linguagem ExtJS, um xtype é um nome simbólico dado a uma classe. Você pode ler o parágrafo &quot;Component XTypes&quot; de [Overview of ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) para obter uma explicação detalhada sobre o que é um xtype e como ele pode ser usado.

Para obter informações completas sobre todos os widgets disponíveis em AEM, consulte a [documentação da API do widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Para descobrir em quais componentes um determinado xtype é usado no AEM, você pode usar o seguinte query Xpath no CRXDE, substituindo &quot;caixa de seleção&quot; pelo xtype que lhe interessa:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Esta página descreve o uso de xtypes ExtJS na interface clássica.
>
>O Adobe recomenda que você aproveite a interface de usuário padrão, moderna, [habilitada para toque](/help/sites-developing/touch-ui-concepts.md) com base em [IU Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [IU Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Encontre abaixo uma lista dos xtypes disponíveis no Adobe Experience Manager:

* anotação

   [CQ.wcm.Anotação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   A caixa de diálogo é um tipo especial de janela com um formulário no corpo e um grupo de botões no rodapé. Normalmente, é usado para editar conteúdo, mas também pode exibir informações.

* livraria

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Anteriormente conhecido como &quot;SimpleStore&quot;.

   Classe auxiliar pequena para facilitar a criação de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir dos dados da matriz. Um ArrayStore será configurado automaticamente com um [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   O Editor de ativos usado no Administrador do DAM.

* assetreferencesearchdialog

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog é uma caixa de diálogo que aparece caso uma página faça referência a ativos ou tags.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   O BlueprintConfig fornece um painel para visualização das Live Copies de um Blueprint e editar essas propriedades do Blueprint ( sincronizar ações de disparo e sincronização ).

* blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   O BlueprintStatus fornece um painel para visualização e edição de um Blueprint e seus relacionamentos de Live Copies. A navegação é feita por meio de [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), edição por meio de [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) e um [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* caixa

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Classe base para qualquer [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) que deva ser dimensionado como uma caixa, usando largura e altura.

   BoxComponent fornece ajustes automáticos de modelo de caixa para dimensionamento e posicionamento e funcionará corretamente no modelo de renderização de Componente.

* janela de navegação

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   A janela BrowseDialog permite que o usuário navegue no repositório para selecionar um caminho. Normalmente é usado por meio de [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Obsoleto: Use  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathFieldem vez disso**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   O BulkEditor fornece um mecanismo de pesquisa e uma grade para editar os resultados da pesquisa.

   O BulkEditor deve ser inserido em um formulário HTML (exigido pela funcionalidade de importação). Isso funciona perfeitamente com um [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   O BulkEditorForm fornece [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) cercado por um formulário HTML. Esta é a versão independente do [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), o formulário HTML é necessário para o botão importar.

* botão

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Classe de Botão Simples

* grupo de botões

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Container para um grupo de botões.

* gráfico

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   O pacote CQ.Ext.chart fornece a capacidade de visualizar dados com gráficos baseados em flash. Cada gráfico se vincula diretamente a um CQ.Ext.data.Store permitindo atualizações automáticas do gráfico. Para alterar a aparência de um gráfico, consulte as opções de configuração [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) e [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart).

* caixa de seleção

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Campo de caixa de seleção única. Pode ser usado como uma substituição direta para os campos de caixa de seleção tradicionais.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   Um container de agrupamento para os controles [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox).

* clear combo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   A ClearableComboBox é uma caixa de combinação não editável com um acionador para limpar seu valor.

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   O ColorField permite que o usuário insira um valor hexadecimal de cor diretamente ou usando um [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* lista de cores

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   A ColorList permite que o usuário escolha uma cor de uma lista editável.

* menu colorido

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   Um menu que contém um componente [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette).

* paleta de cores

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Classe da paleta de cores simples para escolher cores. A paleta pode ser renderizada em qualquer container.

* combinação

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   Um controle combobox com suporte para preenchimento automático, carregamento remoto, paginação e muitos outros recursos.

   Uma ComboBox funciona de maneira semelhante a um campo HTML tradicional &lt;select>. A diferença é que para enviar o [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), você deve especificar um [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) para criar uma entrada oculta.

* componente

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Classe básica para todos os componentes de Saída. Todas as subclasses do Componente podem participar do ciclo de vida do componente de Saída automatizado da criação, renderização e destruição que é fornecido pela classe [Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container). Os componentes podem ser adicionados a um Container por meio da opção de configuração [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) no momento em que o Container é criado.

* componente extrator

   [CQ.wcm.ComponentExtrator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   O ComponentExtrator permite que o usuário extraia componentes de um site/página.

* seletor de componentes

   [CQ.form.ComponentSeletor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   Uma seleção agrupada e ordenada dos Componentes disponíveis.

* componentstyles

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Classe básica para campos de formulário complexos baseados em painel que incluem um campo de formulário ou um grupo de campos de formulário.

* container

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Classe básica para qualquer [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) que possa conter outros Componentes. Os container lidam com o comportamento básico de conter itens, ou seja, adicionar, inserir e remover itens.

   As classes de Container mais usadas são [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentador

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   O ContentFinder é uma coluna especializada de duas colunas [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) que contém o Localizador de conteúdo real à esquerda e o Quadro de conteúdo à direita.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   O ContentFinderTab é um painel especializado que fornece recursos usados nos painéis de guias do [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). Normalmente, ele apresenta um formulário de pesquisa - a Caixa de Query - e uma visualização de dados para exibir a pesquisa.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   O WorkflowModelCombo é um [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) personalizado que mostra uma lista de modelos de fluxo de trabalho disponíveis.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   O WorkflowModelSelector combina um WorkflowModelCombo com uma imagem em miniatura do fluxo de trabalho e botões para criar e editar modelos de fluxo de trabalho.

* createsiteassistente

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   O CreateSiteWizard é um assistente passo a passo para criar sites (MSM).

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog é uma caixa de diálogo que permite criar uma nova versão de uma página.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel é um tipo especial de painel para ser usado em [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Seu conteúdo é recuperado e enviado para um URL diferente dos outros campos da caixa de diálogo.

* ciclo

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   Um SplitButton especializado que contém um menu de elementos [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem). O botão percorre automaticamente cada item de menu ao clicar, aumentando o evento [change](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) do botão (ou chamando a função [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) do botão, se fornecido) para o item de menu ativo.

* dataview

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   Um mecanismo para exibir dados usando modelos e formatação de layout personalizados. O DataView usa um [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) como seu mecanismo de formatação interno, e está vinculado a um [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) para que, à medida que os dados no armazenamento forem alterados, a visualização seja automaticamente atualizada para refletir as alterações.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Fornece um campo de entrada de data com uma lista suspensa [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) e validação automática de data.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   Um menu que contém um componente [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker).

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   Um seletor de data de pop-up. Essa classe é usada pela classe [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) para permitir a navegação e seleção de datas válidas.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   O DateTime permite que o usuário insira uma data e uma hora combinando [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) e [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* caixa de diálogo

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   A caixa de diálogo é um tipo especial de janela com um formulário no corpo e um grupo de botões no rodapé. Normalmente, é usado para editar conteúdo, mas também pode exibir informações.

* dialogfieldset

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   O DialogFieldSet é um [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) para uso em [Diálogos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Classe auxiliar pequena para criar um [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurado com um [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) e [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) para interagir com um [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) Server do lado [Provedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) mais fácil.

* display

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Um campo de texto somente para exibição que não é validado e não é enviado.

* editora

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   A EditBar permite que o usuário edite conteúdo usando botões em uma barra.

   Embora não esteja listado aqui, EditBar tem todos os membros de [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Um campo do editor base que lida com a exibição/ocultação sob demanda e tem uma lógica integrada de dimensionamento e manipulação de eventos.

* editorial

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Esta classe estende a [Classe GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) para fornecer edição de células em [colunas](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column) selecionadas. As colunas editáveis são especificadas fornecendo um [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) na [configuração de coluna](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* edição

   [CQ.wcm.EditRollover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   O EditRollover permite que o usuário edite o conteúdo por meio do clique no duplo e fornece mais ações de edição por meio de um menu de contexto. A área editável é indicada com um quadro quando o mouse está rolando sobre o conteúdo.

* alimentador

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   O FeedImporter permite que o usuário importe feeds RSS ou Atom e crie páginas para cada entrada de feed.

* campo

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Classe básica para campos de formulário que fornece manuseio de eventos, dimensionamento, manuseio de valores e outras funcionalidades padrão.

* fieldset

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Container padrão usado para agrupar itens em um [formulário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploaddialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   O FileUploadDialogButton cria um botão que abre uma nova caixa de diálogo para carregar um arquivo por meio de FileUploadField. Pode ser usado em caixas de diálogo de edição, onde o upload deve ocorrer em um formulário separado.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   O FileUploadField permite que o usuário selecione um único arquivo a ser carregado.

* findsubstituedialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   FindReplaceDialog é uma caixa de diálogo para localizar e substituir tokens em uma página e suas páginas filhas.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* grade

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Essa classe representa a interface primária de um controle de grade baseado em componente para representar dados em um formato tabular de linhas e colunas.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   Uma implementação de loja especializada que fornece o agrupamento de registros por um dos campos disponíveis. Normalmente, isso é usado em conjunto com um [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) para provar o modelo de dados de um GridPanel agrupado.

* diálogo celeiro

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   O HeavyMoveDialog é uma caixa de diálogo para mover uma página e suas páginas secundárias, considerando também a reativação de páginas ativadas anteriormente (&quot;movimento pesado&quot;).

* oculto

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Um campo oculto básico para armazenar valores ocultos em formulários que precisam ser passados no envio do formulário.

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   O HistoryButton é uma pequena classe auxiliar para fornecer facilmente botões para frente e para trás. Normalmente, duas instâncias relacionadas são obrigatórias: A instância do botão de avanço é um botão simples vinculado à instância do botão de retorno que lida com o histórico.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Fornece um componente leve do Editor HTML. Alguns recursos da barra de ferramentas não são suportados pelo Safari e serão automaticamente ocultos quando necessário. Esses itens são anotados nas opções de configuração, quando apropriado.

   Os botões da barra de ferramentas do editor têm dicas de ferramentas definidas na propriedade [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor).

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   Uma caixa de diálogo simples mostrando o conteúdo de um iframe e permitindo formulários em iframes.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   Um painel contendo um iframe. Fornece fácil criação de iframes, um evento de carregamento de iframe e acesso fácil ao conteúdo do iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField é um campo de texto que é exibido como um rótulo quando não está em foco.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Classe auxiliar pequena para facilitar a criação de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de dados JSON. Um JsonStore será configurado automaticamente com um [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Campo Rótulo básico.

* language agecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog é uma caixa de diálogo para copiar árvores de idioma.

* verificador

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   O LinkChecker é uma ferramenta para verificar links externos em um site.

* lista

   [CQ.Ext.lista.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.lista.ListView é uma implementação rápida e leve de peso de uma visualização semelhante a [Grid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel).

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   O LiveCopyProperties fornece um painel para visualização e edição de propriedades do Live Copy (herança de relacionamento, acionador de sincronização e ações de sincronização).

* lvbooleancolumn

   [CQ.Ext.lista.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   Uma classe de definição de coluna que renderiza campos de dados booleanos. Consulte a opção de configuração [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* lvcolumn

   [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Esta classe encapsula os dados de configuração da coluna a serem usados na inicialização de [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.lista.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   Uma classe de definição de coluna que renderiza uma data passada de acordo com a localidade padrão, ou um [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn) configurado. Consulte a opção de configuração [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* lvnumber ercolumn

   [CQ.Ext.lista.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Uma classe de definição de coluna que renderiza um campo de dados numéricos de acordo com uma string [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn). Consulte a opção de configuração [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) de [CQ.Ext.lista.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Obsoleto: Use o  [Content ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) Finderpara procurar mídia.**

   O MediaBrowseDialog é uma caixa de diálogo para navegar na biblioteca de mídia.

* menu

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Um objeto de menu. Este é o container ao qual você pode adicionar itens de menu. O menu também pode servir como uma classe base quando você deseja um menu especializado com base em outro componente (como [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) por exemplo).

   Os menus podem conter [itens de menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item) ou [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s gerais.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   A classe base para todos os itens renderizados em menus. O BaseItem fornece a renderização padrão, o gerenciamento de estado ativado e as opções de configuração básica compartilhadas por todos os componentes do menu.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Adiciona um item de menu que contém uma caixa de seleção por padrão, mas também pode fazer parte de um grupo de opções.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   Uma classe base para todos os itens de menu que exigem funcionalidade relacionada ao menu (como submenus) e não são itens de exibição estáticos. O item estende a funcionalidade básica de [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) adicionando ativações específicas de menu e manuseio de cliques.

* menuseparador

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Adiciona uma barra separadora a um menu, usada para dividir grupos lógicos de itens de menu. Geralmente, você adicionará uma dessas opções usando &quot;-&quot; em sua chamada para add() ou em sua configuração de itens, em vez de criar uma diretamente.

* menutexite

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Adiciona uma string de texto estático a um menu, geralmente usado como um cabeçalho ou separador de grupo.

* metadata

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   Os metadados fornecem um conjunto de campos para determinar as informações necessárias para um campo de metadados como usado, por exemplo, nas páginas do editor de ativos.

   Fornece os seguintes campos:

* multicampo

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   O MultiField é uma lista editável de campos de formulário para editar propriedades de vários valores.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   O componente de teste multivariado pode ser usado para definir e editar um conjunto de imagens que são apresentadas como banners alternados. As estatísticas de taxa de cliques são coletadas por banner.

* caixa de entrada de notificações

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   A NotificationInbox permite que o usuário assine ações WCM e gerencie notificações.

* campo numérico

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Campo de texto numérico que fornece filtragem automática de pressionamento de tecla e validação numérica.

* importador offline

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   O OfflineImporter é uma ferramenta para importar e converter documentos do Microsoft Word em páginas AEM. Esse recurso permite que o conteúdo seja editado offline usando um processador de texto.

* propriedade

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   O OwnerDraw pode conter código HTML personalizado (inserido diretamente ou recuperado de um URL).

* paginação

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   À medida que a quantidade de registros aumenta, o tempo necessário para que o navegador os renderize aumenta. A paginação é usada para reduzir a quantidade de dados trocados com o cliente.

* painel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   O painel é um container que tem funcionalidade específica e componentes estruturais que o tornam o elemento básico perfeito para interfaces de usuário orientadas por aplicativos.

   Os painéis são, em virtude de sua herança de [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* parágrafo

   [CQ.form.ParágrafoReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   O campo de referência de parágrafo permite navegar pelas páginas e selecionar um de seus parágrafos. Consiste em um campo de acionamento e uma caixa de diálogo de navegação de parágrafo associada.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   A Senha é como um [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField), mas mantém seu valor privado, permitindo que os usuários digitem dados confidenciais.

* conclusão

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Obsoleto: Use  [CQ.form.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) PathFieldem vez disso**

* campo

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   O PathField é um campo de entrada projetado para caminhos com conclusão de caminho e um botão para abrir um [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) para navegar no repositório do servidor. Ele também pode navegar pelos parágrafos da página para a geração de links avançados.

* progresso

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   Um componente atualizável da barra de progresso. A barra de progresso suporta dois modos diferentes: manual e automático.

   No modo manual, você é responsável por mostrar, atualizar (via [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) e limpar a barra de progresso conforme necessário do seu próprio código. Esse método é mais apropriado quando você deseja mostrar o progresso.

* propertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   Uma implementação de grade especializada destinada a imitar a grade de propriedade tradicional, como normalmente visto nos IDEs de desenvolvimento. Cada linha na grade representa uma propriedade de algum objeto, e os dados são armazenados como um conjunto de pares de nome/valor em [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* prógrade

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   A PropertyGrid é uma grade genérica usada para exibir e editar propriedades de objetos.

* dica rápida

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quicktip Uma classe especializada de dica de ferramenta para dicas de ferramentas que podem ser especificadas na marcação e gerenciadas automaticamente pela instância global [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips). Consulte o cabeçalho da classe QuickTips para obter mais detalhes e exemplos de uso.

* rádio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Campo de rádio único. Igual à caixa de seleção, mas fornecida como uma conveniência para configurar automaticamente o tipo de entrada. O agrupamento de opções é manipulado automaticamente pelo navegador se você atribuir o mesmo nome a cada rádio de um grupo.

* radiogurte

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   Um container de agrupamento para os controles [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio).

* referencesdialog

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   A caixa de diálogo Referências é uma caixa de diálogo para exibir referências em uma página.

* restaurar reedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog é uma caixa de diálogo para restaurar uma versão anterior de uma árvore.

* restore versiondialog

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog é uma caixa de diálogo para restaurar uma versão anterior de uma página.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   O RichText fornece um campo de formulário para editar informações de texto estilizado (Rich Text).

   O componente RichText atualmente fornece os seguintes recursos:

* plano de lançamento

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   O RolloutPlan fornece uma caixa de diálogo para observar o andamento de um roll-out de página. O RolloutPlan é iniciado por um [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* assistente de rollout

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   O RolloutWizard fornece um assistente para rolar uma página. RolloutWizard start [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* campo de pesquisa

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   O SearchField fornece um campo de pesquisa que fornece os resultados em uma lista suspensa que pode ser usada para pesquisar o repositório.

* seleção

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   A Seleção permite que o usuário escolha entre várias opções. As opções podem fazer parte da configuração ou ser carregadas a partir de uma resposta JSON. A Seleção pode ser renderizada como suspensa (selecionar) ou uma caixa de combinação (selecionar mais entrada de texto livre).

* ajudante

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   O Sidekick é um auxiliar flutuante que fornece ao usuário ferramentas comuns para a edição de páginas.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   O SiteAdmin é um console que fornece funções de administração de WCM.

* importador local

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   O SiteImporter permite que o usuário importe sites completos e crie projetos iniciais.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   O SizeField permite que o usuário insira a largura e a altura (por exemplo, para uma imagem).

* controle deslizante

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Controle deslizante que suporta orientação vertical ou horizontal, ajustes do teclado, ajuste configurável, clique no eixo e animação. Pode ser adicionado como um item a qualquer container. Exemplo de uso: ...

* apresentação de slides

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   A apresentação de slides fornece um componente que pode ser usado para definir e editar um conjunto de imagens e títulos de imagens que podem ser exibidos como uma apresentação de slides.

   O componente Slideshow é baseado no componente [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage).

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   O SmartFile é um carregador de arquivos inteligente.

   Se um plug-in de Flash (versão >= 9) estiver instalado, os uploads serão executados usando a biblioteca de upload do SWF que fornece uma maneira conveniente de lidar com os uploads.

* sabichão

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   O SmartImage é um carregador inteligente de imagens. Ele fornece ferramentas para processar uma imagem carregada, por exemplo, uma ferramenta para definir mapas de imagem e um corpador de imagens.

   Observe que o componente foi projetado principalmente para uso em uma guia de diálogo separada.

* espaçador

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Usado para fornecer um espaço dimensionável em um layout.

* giro

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   O Girador é um campo de disparo para valores numéricos, de data ou de hora. O valor pode ser aumentado e diminuído usando os acionadores para cima e para baixo fornecidos, a roda ou as teclas de rolagem.

* botão

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   Um botão dividido que fornece uma seta suspensa integrada que pode acionar um evento separadamente do evento click padrão do botão. Normalmente, isso seria usado para exibir um menu suspenso que fornece opções adicionais para a ação do botão principal, mas qualquer manipulador personalizado pode fornecer a implementação de cliques em seta.

* estáticas

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   O Estático pode ser usado para exibir texto arbitrário ou HTML.

* estatísticas

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   As Estatísticas exibem as impressões de página como um gráfico. O widget permite selecionar um período, as estatísticas devem ser exibidas para esse período.

* loja

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   A classe Store encapsula um cache do lado do cliente de [Record](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) objetos que fornecem dados de entrada para Componentes como [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) ou [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* sugestfield

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   O SuggestField fornece sugestões ao usuário com base em sua entrada.

* alternador

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   O Alternador fornece um grupo de botões para a barra de cabeçalho em um console para alternar entre sites, ativos digitais, ferramentas, fluxo de trabalho e segurança.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Obsoleto: Em  [vez disso, use ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) CQ.form.TableEdit2.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   O TableEdit2 fornece um widget para criar tabelas.

* tabuleiro

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   Um container básico de guias. Os TabPanels podem ser usados exatamente como um [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) padrão para fins de layout, mas também têm suporte especial para o conteúdo de Componentes filho ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* tags

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   é um widget de formulário para inserir tags. Ele tem um menu pop-up para seleção de tags existentes, inclui o preenchimento automático e muitos outros recursos.

* textarea

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Campo de texto de várias linhas. Pode ser usado como uma substituição direta para campos de texto tradicionais, além de adicionar suporte para dimensionamento automático.

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   O TextButton fornece um link de texto com os recursos de [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* textfield

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Campo de texto básico. Pode ser usado como uma substituição direta para entradas de texto tradicionais ou como a classe base para controles de entrada mais sofisticados (como [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) e [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatura

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Fornece um campo de entrada de tempo com uma lista suspensa de tempo e validação automática de hora. Exemplo de uso: ...

* ponta

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype tip Esta é a classe base para [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) e [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) que fornece o layout e o posicionamento básicos que todas as classes baseadas em dicas exigem. Essa classe pode ser usada diretamente para dicas simples e posicionadas estaticamente.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Adiciona uma barra separadora a um menu, usada para dividir grupos lógicos de itens de menu. O separador pode ainda ter um título.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Classe Basic Toolbar. Embora [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) para a Barra de ferramentas seja [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), os elementos da Barra de ferramentas (itens filhos para o container da Barra de ferramentas) podem ser praticamente qualquer tipo de Componente. Os elementos da barra de ferramentas podem ser criados explicitamente por meio de seus construtores.

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   Uma implementação padrão de dica de ferramenta para fornecer informações adicionais ao passar o mouse sobre um elemento de público alvo. @xtype tooltip

* trágico

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* painel

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   O TreePanel fornece representação de IU estruturada em árvore de dados estruturados em árvore.

   [Os ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)TreeNodes adicionados ao TreePanel podem conter cada um metadados usados pelo aplicativo em sua propriedade  [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) de atributos.

* gatilho

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Fornece um invólucro conveniente para TextFields que adiciona um botão de disparo clicável (parece com uma caixa de combinação por padrão). O acionador não tem nenhuma ação padrão, portanto, você deve atribuir uma função para implementar o manipulador de cliques do acionador ao substituir [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Você pode criar um TriggerField diretamente, pois ele é renderizado exatamente como uma caixa de combinação.

* uploaddialog

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   O UploadDialog permite que o usuário carregue arquivos no repositório Cria um novo UploadDialog.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Item da barra de ferramentas para exibir o nome de usuário atual e permitir ações do usuário como editar propriedades e representação do usuário.

* visor

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   Um container especializado que representa a área do aplicativo visualizável (o visor do navegador).

   O Viewport é renderizado para o corpo do documento e automaticamente dimensiona-se para o tamanho do visor do navegador e gerencia o redimensionamento da janela. Pode haver apenas um Viewport criado.

* janela

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   Um painel especializado destinado ao uso como uma janela do aplicativo. Por padrão, as janelas são flutuantes, [redimensionáveis](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [arrastáveis](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window). O Windows pode ser [maximizado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) para preencher a janela de visualização, restaurado ao seu tamanho anterior e pode ser [minimizar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Classe auxiliar pequena para facilitar a criação de [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)s a partir de dados XML. Um XmlStore será configurado automaticamente com um [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **** cqincludePseudo xtype que inclui definições de widget de um caminho diferente no repositório. Normalmente, é usado em caixas de diálogo de página. Não há classe de widget JavaScript real para esse xtype. É processado pela função formatData() da classe CQ.Util. Para obter mais informações, consulte este artigo da base de conhecimento.
