---
title: Uso de xtypes (interface clássica)
seo-title: Using xtypes (Classic UI)
description: Saiba mais sobre todos os xtypes disponíveis no AEM
seo-description: Learn about all the xtypes that are available with AEM
uuid: 6497caa4-2f9b-4f21-9023-88d485fd1d78
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: adb70b43-1b0b-4302-905a-c7612675dabb
exl-id: 06ca4e6d-9ab7-4c5b-905c-07c448632f2b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '6400'
ht-degree: 0%

---

# Uso de xtypes (interface clássica){#using-xtypes-classic-ui}

Esta página descreve todos os xtypes disponíveis com o Adobe Experience Manager (AEM).

Na linguagem ExtJS, um xtype é um nome simbólico dado a uma classe. Você pode ler o parágrafo &quot;Component XTypes&quot; do [Visão geral do ExtJS 2](https://www.sencha.com/learn/overview-of-extjs-2) para obter uma explicação detalhada sobre o que é um xtype e como ele pode ser usado.

Para obter informações completas sobre todos os widgets disponíveis no AEM consulte [documentação da API do widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

Para descobrir em quais componentes um determinado xtype é usado no AEM, você pode usar a seguinte consulta Xpath no CRXDE, substituindo &quot;caixa de seleção&quot; pelo xtype em que você está interessado:

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>Esta página descreve o uso de xtypes ExtJS na interface clássica.
>
>O Adobe recomenda que você aproveite o padrão, moderno, [interface habilitada para toque](/help/sites-developing/touch-ui-concepts.md) baseado em [Interface do usuário do Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

## xtypes {#xtypes}

Encontre abaixo uma lista dos xtypes disponíveis no Adobe Experience Manager:

* anotação

   [CQ.wcm.Annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Annotation)

   A caixa de diálogo é um tipo especial de janela com um formulário no corpo e um grupo de botões no rodapé. Normalmente, é usado para editar conteúdo, mas também pode apenas exibir informações.

* arraystore

   [CQ.Ext.data.ArrayStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayStore)

   Anteriormente conhecido como &quot;SimpleStore&quot;.

   Pequena classe auxiliar para criar [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)Os dados da matriz são mais fáceis. Um ArrayStore será configurado automaticamente com um [CQ.Ext.data.ArrayReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.ArrayReader).

* asseteditor

   [CQ.dam.AssetEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.AssetEditor)

   O Editor de ativos usado no Administrador do DAM.

* assetreferencesearchdialog

   [CQ.wcm.AssetReferenceSearchDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.AssetReferenceSearchDialog)

   AssetReferenceSearchDialog é uma caixa de diálogo que aparece caso uma página faça referência a ativos ou tags.

* blueprintconfig

   [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig)

   O BlueprintConfig fornece um painel para exibir as Live Copies de um Blueprint e editar essas propriedades do Blueprint ( sincronizar ações de disparo e sincronização ).

* status de blueprintstatus

   [CQ.wcm.msm.BlueprintStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus)

   O BlueprintStatus fornece um painel para exibir e editar um Blueprint e seus relacionamentos de Live Copies. A navegação é feita por meio de um [CQ.wcm.msm.BlueprintStatus.Tree](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintStatus.Tree), edição por meio de [CQ.wcm.msm.BlueprintConfig](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.BlueprintConfig) e a [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties).

* caixa

   [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent)

   Classe base para qualquer [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component) que deve ser dimensionado como uma caixa, usando largura e altura.

   BoxComponent fornece ajustes automáticos de modelo de caixa para dimensionamento e posicionamento e funcionará corretamente no modelo de renderização de Componente.

* janela de navegação

   [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog)

   A caixa de diálogo Procurar permite que o usuário navegue pelo repositório para selecionar um caminho. Normalmente é usado por meio de um [BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField).

* browsefield

   [CQ.form.BrowseField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.BrowseField)

   **Obsoleto: Use [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) instead**

* bulkeditor

   [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor)

   O BulkEditor fornece um mecanismo de pesquisa e uma grade para editar resultados de pesquisa.

   O BulkEditor deve ser inserido em um formulário HTML (exigido pela funcionalidade de importação). Isso funciona perfeitamente com uma [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* bulkeditorform

   [CQ.wcm.BulkEditorForm](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditorForm)

   O BulkEditorForm fornece [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor) cercada por uma HTML. Esta é a versão independente do [CQ.wcm.BulkEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.BulkEditor), o formulário HTML é necessário para o botão importar.

* botão

   [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button)

   Classe de Botão Simples

* buttongroup

   [CQ.Ext.ButtonGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ButtonGroup)

   Contêiner de um grupo de botões.

* gráfico

   [CQ.Ext.chart.Chart](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart)

   O pacote CQ.Ext.chart fornece a capacidade de visualizar dados com gráficos baseados em flash. Cada gráfico é vinculado diretamente a um CQ.Ext.data.Store permitindo atualizações automáticas do gráfico. Para alterar a aparência de um gráfico, consulte [chartStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) e [extraStyle](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.chart.Chart) opções de configuração.

* caixa de seleção

   [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox)

   Campo de caixa de seleção única. Pode ser usado como uma substituição direta para campos de caixa de seleção tradicionais.

* checkboxgroup

   [CQ.Ext.form.CheckboxGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.CheckboxGroup)

   Um contêiner de agrupamento para [CQ.Ext.form.Checkbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Checkbox) controles.

* clearcombo

   [CQ.form.ClearableComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ClearableComboBox)

   ClearableComboBox é uma caixa de combinação não editável com um acionador para limpar seu valor.

* colorfield

   [CQ.form.ColorField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorField)

   O ColorField permite que o usuário insira um valor hexadecimal de cor diretamente ou usando um [CQ.Ext.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorMenu).

* colorlist

   [CQ.form.ColorList](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ColorList)

   A ColorList permite que o usuário escolha uma cor de uma lista editável.

* colormenu

   [CQ.Ext.menu.ColorMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.ColorMenu)

   Um menu contendo um [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette) Componente.

* paleta de cores

   [CQ.Ext.ColorPalette](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ColorPalette)

   Classe da paleta de cores simples para escolher cores. A paleta pode ser renderizada em qualquer contêiner.

* combinação

   [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)

   Um controle de caixa de combinação com suporte para preenchimento automático, carregamento remoto, paginação e muitos outros recursos.

   Uma ComboBox funciona de maneira semelhante a um HTML tradicional &lt;select> campo. A diferença é que submeter a variável [valueField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox), você deve especificar um [hiddenName](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) para criar uma entrada oculta.

* componente

   [CQ.Ext.Component](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)

   Classe base para todos os componentes Ext. Todas as subclasses de Componente podem participar do ciclo de vida automatizado do componente de Saída da criação, renderização e destruição fornecido pela [Contêiner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) classe . Os componentes podem ser adicionados a um contêiner por meio da variável [items](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) opção de configuração no momento em que o Contêiner é criado.

* componente extrator

   [CQ.wcm.ComponentExtrator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ComponentExtractor)

   O ComponentExtrator permite que o usuário extraia componentes de um site/página.

* seletor de componentes

   [CQ.form.ComponentSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentSelector)

   Uma seleção agrupada e ordenada dos Componentes disponíveis.

* estilos de componentes

   [CQ.form.ComponentStyles](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ComponentStyles)

* compositefield

   [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)

   Classe base para campos de formulário complexos e baseados em painel que incluem um campo de formulário ou um grupo de campos de formulário.

* container

   [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)

   Classe base para qualquer [CQ.Ext.BoxComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.BoxComponent) que podem conter outros componentes. Os contêineres lidam com o comportamento básico de itens contêineres, ou seja, adicionar, inserir e remover itens.

   As classes de Contêiner mais usadas são [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel), [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) e [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel).

* contentfinder

   [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder)

   O ContentFinder é uma coluna especializada de duas colunas [Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport) que contém o Localizador de conteúdo real à esquerda e o Quadro de conteúdo à direita.

* contentfindertab

   [CQ.wcm.ContentFinderTab](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinderTab)

   A guia ContentFinder é um painel especializado que oferece recursos usados nos painéis de guias da [CQ.wcm.ContentFinder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder). Normalmente, ele apresenta um formulário de pesquisa - a Caixa de consulta - e uma visualização de dados para exibir a pesquisa.

* cq.workflow.model.combo

   [CQ.wcm.WorkflowModelCombo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelCombo)

   O WorkflowModelCombo é personalizado [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox) que mostra uma lista de modelos de fluxo de trabalho disponíveis.

* cq.workflow.model.selector

   [CQ.wcm.WorkflowModelSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.WorkflowModelSelector)

   O WorkflowModelSelector combina um WorkflowModelCombo com uma imagem em miniatura do fluxo de trabalho e botões para criar e editar modelos de fluxo de trabalho.

* createsitewizard

   [CQ.wcm.CreateSiteWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateSiteWizard)

   O CreateSiteWizard é um assistente passo a passo para criar sites (MSM).

* createversiondialog

   [CQ.wcm.CreateVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.CreateVersionDialog)

   CreateVersionDialog é uma caixa de diálogo que permite criar uma nova versão de uma página.

* customcontentpanel

   [CQ.CustomContentPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.CustomContentPanel)

   CustomContentPanel é um tipo especial de painel para ser usado em [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog): Seu conteúdo é recuperado de e enviado a um URL diferente dos outros campos na caixa de diálogo.

* ciclo

   [CQ.Ext.CycleButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton)

   Um SplitButton especializado que contém um menu de [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem) elementos. O botão faz o ciclo automático de cada item de menu ao clicar, elevando o botão [alterar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) ou chamar o [changeHandler](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.CycleButton) , se fornecido) para o item de menu ativo.

* visualização de dados

   [CQ.Ext.DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView)

   Um mecanismo para exibir dados usando modelos e formatação de layout personalizados. O DataView usa um [CQ.Ext.XTemplate](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.XTemplate) como seu mecanismo interno de modelização e está vinculado a um [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) para que, à medida que os dados no armazenamento forem alterados, a visualização seja atualizada automaticamente para refletir as alterações.

* datefield

   [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField)

   Fornece um campo de entrada de data com um [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) lista suspensa e validação automática de data.

* datemenu

   [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu)

   Um menu contendo um [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker) Componente.

* datepicker

   [CQ.Ext.DatePicker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DatePicker)

   Um seletor de data pop-up. Essa classe é usada pelo [DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) classe para permitir a navegação e seleção de datas válidas.

* datetime

   [CQ.form.DateTime](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DateTime)

   DateTime permite que o usuário insira uma data e uma hora ao combinar [CQ.Ext.form.DateField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DateField) e [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField).

* caixa de diálogo

   [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)

   A caixa de diálogo é um tipo especial de janela com um formulário no corpo e um grupo de botões no rodapé. Normalmente, é usado para editar conteúdo, mas também pode apenas exibir informações.

* dialog fieldset

   [CQ.form.DialogFieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.DialogFieldSet)

   O DialogFieldSet é um [FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet) para uso em [Diálogos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog).

* directstore

   [CQ.Ext.data.DirectStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectStore)

   Classe auxiliar pequena para criar uma [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store) configurado com um [CQ.Ext.data.DirectProxy](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.DirectProxy) e [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader) para fazer com que interaja com um [CQ.Ext.Direct](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Direct) Lado do servidor [Provedor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.direct.Provider) mais fácil.

* displayfield

   [CQ.Ext.form.DisplayField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.DisplayField)

   Campo de texto somente exibição que não é validado e não foi enviado.

* editor

   [CQ.wcm.EditBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar)

   A EditBar permite que o usuário edite o conteúdo usando botões em uma barra.

   Embora não esteja listado aqui, a EditBar tem todos os membros do [CQ.wcm.EditBase](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBase).

* editor

   [CQ.Ext.Editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Editor)

   Um campo do editor base que lida com a exibição/ocultação sob demanda e tem um dimensionamento integrado e uma lógica de manipulação de eventos.

* editorgrid

   [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)

   Essa classe estende a [Classe GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) para fornecer a edição de células em [columns](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column). As colunas editáveis são especificadas fornecendo um [editor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel) no [configuração da coluna](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.Column).

* edição

   [CQ.wcm.EditRolover](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover)

   O EditRolover permite que o usuário edite conteúdo por meio de um clique duplo e fornece mais ações de edição por meio de um menu de contexto. A área editável é indicada com um quadro quando o mouse está rolando sobre o conteúdo.

* feedimporter

   [CQ.wcm.FeedImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FeedImporter)

   O FeedImporter permite que o usuário importe feeds RSS ou Atom e crie páginas para cada entrada de feed.

* campo

   [CQ.Ext.form.Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Field)

   Classe base para campos de formulário que fornece tratamento de eventos padrão, dimensionamento, manipulação de valores e outras funcionalidades.

* fieldset

   [CQ.Ext.form.FieldSet](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FieldSet)

   Contêiner padrão usado para agrupar itens em um [formulário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.FormPanel). ...

* fileuploadialogbutton

   [CQ.form.FileUploadDialogButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadDialogButton)

   FileUploadDialogButton cria um botão que abre uma nova caixa de diálogo para carregar um arquivo por meio de FileUploadField. Pode ser usado dentro de caixas de diálogo de edição, onde o upload deve ocorrer em um formulário separado.

* fileuploadfield

   [CQ.form.FileUploadField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.FileUploadField)

   O FileUploadField permite que o usuário selecione um único arquivo a ser carregado.

* findreplacedialog

   [CQ.wcm.FindReplaceDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.FindReplaceDialog)

   A caixa de diálogo FindReplaceDialog é uma caixa de diálogo para localizar e substituir tokens em uma página e suas páginas filhas.

* flash

   [CQ.Ext.FlashComponent](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.FlashComponent)

* grade

   [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)

   Essa classe representa a interface principal de um controle de grade baseado em componentes para representar dados em um formato tabular de linhas e colunas.

* groupingstore

   [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)

   Uma implementação de loja especializada que fornece o agrupamento de registros por um dos campos disponíveis. Normalmente, isso é usado junto com um [CQ.Ext.grid.GroupingView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GroupingView) para provar o modelo de dados de um GridPanel agrupado.

* diálogo entre os céus

   [CQ.wcm.HeavyMoveDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.HeavyMoveDialog)

   HeavyMoveDialog é uma caixa de diálogo para mover uma página e suas páginas filhas, além de considerar a reativação de páginas ativadas anteriormente (movimentação &quot;pesada&quot;).

* oculto

   [CQ.Ext.form.Hidden](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Hidden)

   Um campo oculto básico para armazenar valores ocultos em formulários que precisam ser passados no envio do formulário.

* historybutton

   [CQ.HistoryButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.HistoryButton)

   O HistoryButton é uma pequena classe auxiliar para fornecer facilmente botões para frente e para trás. Geralmente, duas instâncias relacionadas são necessárias: A instância do botão de encaminhamento é um botão simples vinculado à instância do botão de voltar que manipula o histórico.

* htmleditor

   [CQ.Ext.form.HtmlEditor](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor)

   Fornece um componente leve do Editor de HTML. Alguns recursos da barra de ferramentas não são compatíveis com o Safari e serão ocultos automaticamente quando necessário. Elas são anotadas nas opções de configuração, quando apropriado.

   Os botões da barra de ferramentas do editor têm dicas de ferramentas definidas no [buttonTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.HtmlEditor) propriedade.

* iframedialog

   [CQ.IframeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframeDialog)

   Uma caixa de diálogo simples mostrando o conteúdo de um iframe e permitindo formulários em iframes.

* iframepanel

   [CQ.IframePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.IframePanel)

   Um painel contendo um iframe. Fornece fácil criação de iframes, um evento de carregamento de iframe e acesso fácil ao conteúdo do iframe.

* inlinetextfield

   [CQ.form.InlineTextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.InlineTextField)

   InlineField é um campo de texto exibido como rótulo quando não está em foco.

* jsonstore

   [CQ.Ext.data.JsonStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonStore)

   Pequena classe auxiliar para criar [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)A partir de dados JSON é mais fácil. Um JsonStore será configurado automaticamente com um [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader).

* label

   [CQ.Ext.form.Label](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Label)

   Campo Basic Label .

* language agecopydialog

   [CQ.wcm.LanguageCopyDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LanguageCopyDialog)

   LanguageCopyDialog é uma caixa de diálogo para copiar árvores de idioma.

* linkchecker

   [CQ.wcm.LinkChecker](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.LinkChecker)

   O LinkChecker é uma ferramenta para verificar links externos em um site.

* listview

   [CQ.Ext.list.ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView)

   CQ.Ext.list.ListView é uma implementação rápida e leve de um [Grade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) como visualização.

* livecopyproperties

   [CQ.wcm.msm.LiveCopyProperties](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.LiveCopyProperties)

   As propriedades da LiveCopy fornecem um painel para exibir e editar as propriedades da Live Copy ( herança do relacionamento, sincronização de acionadores e ações de sincronização ).

* lvbooleancolumn

   [CQ.Ext.list.BooleanColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.BooleanColumn)

   Uma classe de definição de coluna que renderiza campos de dados booleanos. Consulte a [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opção de configuração de [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* lvcolumn

   [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column)

   Essa classe encapsula os dados de configuração da coluna a serem usados na inicialização de um [ListView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.ListView).

* lvdatecolumn

   [CQ.Ext.list.DateColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn)

   Uma classe de definição de Coluna que renderiza uma data passada de acordo com a localidade padrão, ou uma [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.DateColumn). Consulte a [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opção de configuração de [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* lvnumerercolumn

   [CQ.Ext.list.NumberColumn](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn)

   Uma classe de definição de coluna que renderiza um campo de dados numéricos de acordo com uma [format](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.NumberColumn) string. Consulte a [xtype](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) opção de configuração de [CQ.Ext.list.Column](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.list.Column) para obter mais detalhes.

* mediabrowsedialog

   [CQ.MediaBrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.MediaBrowseDialog)

   **Obsoleto: Use [Localizador de conteúdo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ContentFinder) para navegar pela mídia.**

   MediaBrowseDialog é uma caixa de diálogo para navegar na biblioteca de mídia.

* menu

   [CQ.Ext.menu.Menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Menu)

   Um objeto de menu. Este é o contêiner ao qual você pode adicionar itens de menu. O menu também pode servir como uma classe base quando você deseja um menu especializado com base em outro componente (como [CQ.Ext.menu.DateMenu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.DateMenu) por exemplo).

   Os menus podem conter [itens do menu](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)ou geral [Componente](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Component)s.

* menubaseitem

   [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem)

   A classe base de todos os itens que são renderizados em menus. BaseItem fornece a renderização padrão, o gerenciamento de estado ativado e as opções de configuração básica compartilhadas por todos os componentes do menu.

* menucheckitem

   [CQ.Ext.menu.CheckItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.CheckItem)

   Adiciona um item de menu que contém uma caixa de seleção por padrão, mas que também pode fazer parte de um grupo de opções.

* menuitem

   [CQ.Ext.menu.Item](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Item)

   Uma classe base para todos os itens de menu que exigem funcionalidade relacionada a menu (como submenus) e não são itens de exibição estáticos. O item estende a funcionalidade básica de [CQ.Ext.menu.BaseItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.BaseItem) adicionando a ativação específica do menu e o manuseio de cliques.

* menuseparator

   [CQ.Ext.menu.Separator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.Separator)

   Adiciona uma barra separadora a um menu, usada para dividir grupos lógicos de itens de menu. Geralmente, você adicionará um desses ao usar &quot;-&quot; na chamada para adicionar() ou na configuração de itens, em vez de criar um diretamente.

* menutextitem

   [CQ.Ext.menu.TextItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.menu.TextItem)

   Adiciona uma string de texto estático a um menu, geralmente usado como um cabeçalho ou separador de grupo.

* metadados

   [CQ.dam.form.Metadata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.dam.form.Metadata)

   Os metadados fornecem um conjunto de campos para determinar as informações necessárias para um campo de metadados conforme usado, por exemplo, em páginas do editor de ativos.

   Ela fornece os seguintes campos:

* multifield

   [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)

   O MultiField é uma lista editável de campos de formulário para edição de propriedades de vários valores.

* mvt

   [CQ.form.MVT](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MVT)

   O componente de teste multivariado pode ser usado para definir e editar um conjunto de imagens que são apresentadas como banners alternativos. As estatísticas de taxa de cliques são coletadas por banner.

* caixa de notificação

   [CQ.wcm.NotificationInbox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.NotificationInbox)

   A NotificationInbox permite que o usuário assine ações WCM e gerencie notificações.

* numererfield

   [CQ.Ext.form.NumberField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.NumberField)

   Campo de texto numérico que fornece filtragem automática de pressionamento de tecla e validação numérica.

* offlineimporter

   [CQ.wcm.OfflineImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.OfflineImporter)

   O OfflineImporter é uma ferramenta para importar e converter documentos do Microsoft Word em páginas AEM. Esse recurso permite que o conteúdo seja editado offline usando um processador de texto.

* devaneio

   [CQ.form.OwnerDraw](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.OwnerDraw)

   O OwnerDraw pode conter código de HTML personalizado (inserido diretamente ou recuperado de um URL).

* paginação

   [CQ.Ext.PagingToolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.PagingToolbar)

   Conforme a quantidade de registros aumenta, o tempo necessário para que o navegador os renderize aumenta. A paginação é utilizada para reduzir a quantidade de dados trocados com o cliente.

* painel

   [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel)

   O Painel é um contêiner que possui funcionalidades específicas e componentes estruturais que o tornam o elemento essencial perfeito para interfaces de usuário orientadas para aplicativos.

   Os painéis são, em virtude de sua herança de [CQ.Ext.Container](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container).

* parágrafo

   [CQ.form.ParágrafoReference](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.ParagraphReference)

   O campo de referência do parágrafo permite navegar pelas páginas e selecionar um de seus parágrafos. Consiste em um campo de acionamento e uma caixa de diálogo de navegação de parágrafo associada.

* password

   [CQ.form.Password](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Password)

   A senha é como um [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) mas mantém seu valor privado, permitindo que os usuários insiram dados confidenciais.

* path

   [CQ.form.PathCompletion](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathCompletion)

   **Obsoleto: Use [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField) instead**

* pathfield

   [CQ.form.PathField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.PathField)

   PathField é um campo de entrada projetado para caminhos com conclusão de caminho e um botão para abrir um [CQ.BrowseDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.BrowseDialog) para navegar no repositório do servidor. Também pode navegar pelos parágrafos da página para geração de links avançados.

* progresso

   [CQ.Ext.ProgressBar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)

   Um componente atualizável da barra de progresso. A barra de progresso suporta dois modos diferentes: manual e automático.

   No modo manual, você é responsável por mostrar, atualizar (via [updateProgress](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ProgressBar)) e limpar a barra de progresso, conforme necessário, de seu próprio código. Esse método é mais apropriado quando você deseja mostrar o progresso.

* propertygrid

   [CQ.Ext.grid.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyGrid)

   Uma implementação de grade especializada destinada a imitar a grade de propriedade tradicional, como normalmente é visto nos IDEs de desenvolvimento. Cada linha na grade representa uma propriedade de alguns objetos, e os dados são armazenados como um conjunto de pares de nome/valor em [CQ.Ext.grid.PropertyRecord](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.PropertyRecord)s.

* progrid

   [CQ.PropertyGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.PropertyGrid)

   PropertyGrid é uma grade genérica usada para exibir e editar propriedades de objetos.

* dica rápida

   [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip)

   @xtype quickdica Uma classe de ferramenta especializada para dicas de ferramentas que podem ser especificadas na marcação e gerenciadas automaticamente pelo global [CQ.Ext.QuickTips](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTips) instância. Consulte o cabeçalho da classe QuickTips para obter detalhes e exemplos de uso adicionais.

* rádio

   [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio)

   Campo de rádio único. Igual a Caixa de seleção, mas fornecido como uma conveniência para definir automaticamente o tipo de entrada. O agrupamento de opções é manipulado automaticamente pelo navegador se você atribuir a cada rádio em um grupo o mesmo nome.

* radiogurte

   [CQ.Ext.form.RadioGroup](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.RadioGroup)

   Um contêiner de agrupamento para [CQ.Ext.form.Radio](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.Radio) controles.

* referencesdialog

   [CQ.wcm.ReferencesDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.ReferencesDialog)

   A caixa de diálogo Referências é uma caixa de diálogo para exibir referências em uma página.

* restauretreedialog

   [CQ.wcm.RestoreTreeDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreTreeDialog)

   RestoreTreeDialog é uma caixa de diálogo para restaurar uma versão anterior de uma árvore.

* caixa de diálogo de restauração

   [CQ.wcm.RestoreVersionDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.RestoreVersionDialog)

   RestoreVersionDialog é uma caixa de diálogo para restaurar uma versão anterior de uma página.

* richtext

   [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText)

   O RichText fornece um campo de formulário para editar informações de texto estilizado (rich text).

   O componente RichText fornece atualmente os seguintes recursos:

* plano de implementação

   [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan)

   O RolloutPlan fornece uma caixa de diálogo para observar o progresso de uma implantação de página. O RolloutPlan é iniciado por um [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard).

* rolloutwizard

   [CQ.wcm.msm.RolloutWizard](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutWizard)

   O RolloutWizard fornece um assistente para rolar uma página. O RolloutWizard inicia um [CQ.wcm.msm.RolloutPlan](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.msm.RolloutPlan).

* searchfield

   [CQ.form.SearchField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SearchField)

   O SearchField fornece um campo de pesquisa que fornece os resultados em uma lista suspensa que pode ser usada para pesquisar o repositório.

* seleção

   [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection)

   A Seleção permite que o usuário escolha entre várias opções. As opções podem fazer parte da configuração ou ser carregadas de uma resposta JSON. A Seleção pode ser renderizada como lista suspensa (seleção) ou como uma caixa de combinação (selecione mais entrada de texto livre).

* sidekick

   [CQ.wcm.Sidekick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Sidekick)

   O Sidekick é um auxiliar flutuante que fornece ao usuário ferramentas comuns para a edição de páginas.

* siteadmin

   [CQ.wcm.SiteAdmin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteAdmin)

   O SiteAdmin é um console que fornece funções de administração do WCM.

* siteimporter

   [CQ.wcm.SiteImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.SiteImporter)

   O SiteImporter permite que o usuário importe sites completos e crie projetos iniciais.

* sizefield

   [CQ.form.SizeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SizeField)

   O SizeField permite que o usuário insira a largura e a altura (por exemplo, para uma imagem).

* controle deslizante

   [CQ.Ext.Slider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Slider)

   Controle deslizante que suporta orientação vertical ou horizontal, ajustes do teclado, ajuste configurável, clique no eixo e animação. Pode ser adicionado como um item a qualquer contêiner. Exemplo de uso: ...

* slideshow

   [CQ.form.Slideshow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Slideshow)

   O Slideshow fornece um componente que pode ser usado para definir e editar um conjunto de imagens e títulos de imagens que podem ser exibidos como um slideshow.

   O componente de Apresentação é baseado no [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage) componente.

* smartfile

   [CQ.form.SmartFile](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartFile)

   O SmartFile é um carregador inteligente de arquivos.

   Se um plug-in do Flash (versão >= 9) estiver instalado, os uploads serão executados usando a biblioteca de upload do SWF, que fornece uma maneira conveniente de lidar com uploads.

* sabão

   [CQ.form.SmartImage](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SmartImage)

   O SmartImage é um carregador inteligente de imagens. Ele fornece ferramentas para processar uma imagem carregada, por exemplo, uma ferramenta para definir mapas de imagem e um corpper de imagem.

   Observe que o componente foi projetado principalmente para uso em uma guia de diálogo separada.

* espaçador

   [CQ.Ext.Spacer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Spacer)

   Usada para fornecer um espaço dimensionável em um layout.

* ponteiro

   [CQ.form.Spinner](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Spinner)

   O Spinner é um campo de acionador para valores numéricos, de data ou de hora. O valor pode ser aumentado e diminuído usando os acionadores de cima e de baixo fornecidos, o botão de rolagem ou as teclas.

* botão

   [CQ.Ext.SplitButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.SplitButton)

   Um botão dividido que fornece uma seta suspensa integrada que pode acionar um evento separadamente do evento de clique padrão do botão. Normalmente, isso seria usado para exibir um menu suspenso que fornece opções adicionais para a ação do botão principal, mas qualquer manipulador personalizado pode fornecer a implementação de clique com a seta.

* estáticas

   [CQ.Static](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Static)

   O Static pode ser usado para exibir texto ou HTML arbitrário.

* statistics

   [CQ.wcm.Statistics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.Statistics)

   As Estatísticas exibem as impressões da página como um gráfico. O widget permite selecionar um período, as estatísticas devem ser exibidas.

* loja

   [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)

   A classe Store encapsula um cache do lado do cliente de [Registro](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Record) objetos que fornecem dados de entrada para Componentes como [GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel), o [ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)ou o [DataView](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.DataView).

* sugestfield

   [CQ.form.SuggestField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.SuggestField)

   O SuggestField fornece ao usuário sugestões com base em sua entrada.

* alternador

   [CQ.Switcher](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Switcher)

   O Alternador fornece um grupo de botões para a barra de cabeçalho em um console para alternar entre Sites, Ativos digitais, Ferramentas, Fluxo de trabalho e Segurança.

* tableedit

   [CQ.form.TableEdit](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit)

   **Obsoleto: Use [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2) em vez disso.**

* tableedit2

   [CQ.form.TableEdit2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.TableEdit2)

   O TableEdit2 fornece um widget para criar tabelas.

* painel

   [CQ.Ext.TabPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.TabPanel)

   Um contêiner de guia básico. TabPainéis podem ser usados exatamente como um padrão [CQ.Ext.Panel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Panel) para fins de layout, mas também tem suporte especial para componentes filho contêineres ([`items`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container)).

* tags

   [CQ.tagging.TagInputField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tagging.TagInputField)

   ```
   CQ.tagging.TagInputField
   ```

   é um widget de formulário para inserir tags. Ele tem um menu pop-up para selecionar entre tags existentes, inclui o preenchimento automático e muitos outros recursos.

* textarea

   [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea)

   Campo de texto de várias linhas. Pode ser usado como uma substituição direta para campos de área de texto tradicionais, além de adicionar suporte para dimensionamento automático.

* textbutton

   [CQ.TextButton](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.TextButton)

   O TextButton fornece um link de texto com os recursos de um [CQ.Ext.Button](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button).

* campo de texto

   [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)

   Campo de texto básico. Pode ser usado como uma substituição direta de entradas de texto tradicionais ou como a classe base para controles de entrada mais sofisticados (como [CQ.Ext.form.TextArea](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextArea) e [CQ.Ext.form.ComboBox](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.ComboBox)).

* miniatura

   [CQ.form.Thumbnail](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Thumbnail)

* timefield

   [CQ.Ext.form.TimeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TimeField)

   Fornece um campo de entrada de tempo com uma lista suspensa de tempo e validação automática de tempo. Exemplo de uso: ...

* dica

   [CQ.Ext.Tip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tip)

   @xtype dica Esta é a classe base para [CQ.Ext.QuickTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.QuickTip) e [CQ.Ext.Tooltip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Tooltip) que fornece o layout básico e o posicionamento necessários para todas as classes baseadas em dica. Essa classe pode ser usada diretamente para dicas simples e posicionadas estaticamente.

* titleseparator

   [CQ.menu.TitleSeparator](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.menu.TitleSeparator)

   Adiciona uma barra separadora a um menu, usada para dividir grupos lógicos de itens de menu. Além disso, o separador pode ter um título.

* toolbar

   [CQ.Ext.Toolbar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Toolbar)

   Classe Básica da Barra de Ferramentas. Embora a variável [`defaultType`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Container) para Barra de ferramentas é [`button`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Button), os elementos da barra de ferramentas (itens filhos do contêiner da barra de ferramentas) podem ser praticamente qualquer tipo de Componente. Os elementos da barra de ferramentas podem ser criados explicitamente por meio de seus construtores.

* tooltip

   [CQ.Ext.ToolTip](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.ToolTip)

   Uma implementação de dica de ferramenta padrão para fornecer informações adicionais ao passar o mouse sobre um elemento de destino. @xtype tooltip

* treegrid

   [CQ.tree.TreeGrid](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.tree.TreeGrid)

   @xtype treegrid

* treliana

   [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)

   O TreePanel fornece representação de interface de usuário estruturada em árvore de dados estruturados em árvore.

   [TreeNode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode)Adicionados ao TreePanel, cada um pode conter metadados usados pelo aplicativo em seus [atributos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreeNode) propriedade.

* acionador

   [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)

   Fornece um invólucro conveniente para TextFields que adiciona um botão de acionamento clicável (parece com uma caixa de combinação por padrão). O acionador não tem nenhuma ação padrão, portanto, você deve atribuir uma função para implementar o manipulador de cliques do acionador ao substituir [onTriggerClick](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField). Você pode criar um TriggerField diretamente, pois ele é renderizado exatamente como uma caixa de combinação.

* uploanalógico

   [CQ.UploadDialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UploadDialog)

   A caixa de diálogo Upload permite que o usuário carregue arquivos no repositório. Cria uma nova caixa de diálogo Upload.

* userinfo

   [CQ.UserInfo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.UserInfo)

   Item da barra de ferramentas para exibir o nome de usuário atual e permitir ações do usuário como editar propriedades do usuário e representação.

* visor

   [CQ.Ext.Viewport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Viewport)

   Um contêiner especializado que representa a área do aplicativo visualizável (a janela de visualização do navegador).

   A janela Viewport é renderizada para o corpo do documento e automaticamente dimensiona para o tamanho da janela de visualização do navegador e gerencia o redimensionamento da janela. Só pode haver uma janela de visualização criada.

* janela

   [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)

   Um painel especializado destinado a ser usado como uma janela de aplicativo. As janelas são flutuantes, [redimensionável](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)e [arrastável](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) por padrão. O Windows pode ser [maximizado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window) para preencher o visor, restaurado ao tamanho anterior e pode ser [minimizar](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)d.

* xmlstore

   [CQ.Ext.data.XmlStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlStore)

   Pequena classe auxiliar para criar [CQ.Ext.data.Store](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.Store)é mais fácil a partir de dados XML. Um XmlStore será configurado automaticamente com um [CQ.Ext.data.XmlReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.XmlReader).

   **cqinclude** Pseudo xtype que inclui definições de widget de um caminho diferente no repositório. Ele é usado com mais frequência em caixas de diálogo de página. Não há uma classe de widget JavaScript real para esse xtype. Ele é processado pela função formatData() da classe CQ.Util. Para obter mais informações, consulte este artigo da base de conhecimento.
