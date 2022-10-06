---
title: Uso e extensão de widgets (interface de usuário clássica)
seo-title: Using and Extending Widgets (Classic UI)
description: AEM interface baseada na Web usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG do conteúdo por autores diretamente na página da Web
seo-description: AEM's web-based interface uses AJAX and other modern browser technologies to enable WYSIWYG editing and formatting of content by authors right on the web page
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4934'
ht-degree: 0%

---

# Uso e extensão de widgets (interface de usuário clássica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página descreve o uso de widgets na interface de usuário clássica, que foi descontinuada no AEM 6.4.
>
>Adobe recomenda aproveitar o moderno, [interface habilitada para toque](/help/sites-developing/touch-ui-concepts.md) baseado em [Interface do usuário do Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

A interface baseada na Web do Adobe Experience Manager usa AJAX e outras tecnologias modernas de navegador para permitir a edição e formatação WYSIWYG do conteúdo por autores diretamente na página da Web.

O Adobe Experience Manager (AEM) usa a variável [ExtJS](https://www.sencha.com/) biblioteca de widgets, que fornece os elementos da interface do usuário altamente sofisticados que funcionam em todos os navegadores mais importantes e permitem a criação de experiências de interface do usuário no nível de desktop.

Esses widgets estão incluídos no AEM e, além de serem usados pelo próprio AEM, podem ser usados por qualquer site criado usando o AEM.

Para obter uma referência completa de todos os widgets disponíveis no AEM você pode consultar o [documentação da API do widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) ou à [lista de xtypes existentes](/help/sites-developing/xtypes.md). Além disso, muitos exemplos mostrando como usar a estrutura ExtJS estão disponíveis no [Sencha](https://www.sencha.com/products/extjs/examples/) site, o proprietário da estrutura.

Esta página fornece alguns insights sobre como usar e estender widgets. Primeiro descreve como [incluir código do lado do cliente em uma página](#including-the-client-sided-code-in-a-page). Em seguida, descreve alguns componentes de amostra que foram criados para ilustrar alguns usos e extensões básicos. Esses componentes estão disponíveis na variável **Uso de widgets ExtJS** pacote em **Compartilhamento de pacotes**.

O pacote inclui exemplos de:

* [Caixas de diálogo básicas](#basic-dialogs) criado com widgets prontos para uso.
* [Caixas de diálogo dinâmicas](#dynamic-dialogs) criado com widgets prontos e lógica javascript personalizada.
* Caixas de diálogo baseadas em [widgets personalizados](#custom-widgets).
* A [painel de árvore](#tree-overview) exibindo uma árvore JCR abaixo de um determinado caminho.
* A [painel grade](#grid-overview) exibição de dados em formato tabular.

>[!NOTE]
>
>A interface clássica do Adobe Experience Manager é baseada em [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusão do código do lado do cliente em uma página {#including-the-client-sided-code-in-a-page}

O javascript do lado do cliente e o código da folha de estilos devem ser colocados em uma biblioteca do cliente.

Para criar uma biblioteca do cliente:

1. Criar um nó abaixo `/apps/<project>` com as seguintes propriedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:localizável]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependências=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Abaixo `clientlib` crie a `css` e `js` pastas (nt:folder).

1. Abaixo `clientlib` crie a `css.txt` e `js.txt` arquivos (nt:files). Esses arquivos .txt listam os arquivos incluídos na biblioteca.

1. Editar `js.txt`: precisa começar com &#39; `#base=js`&#39; seguido pela lista dos arquivos que serão agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: precisa começar com &#39; `#base=css`&#39; seguido pela lista dos arquivos que serão agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=css
    components.css
   ```

1. Abaixo do `js` coloque os arquivos javascript que pertencem à biblioteca.

1. Abaixo do `css` coloque `.css` arquivos e os recursos usados pelos arquivos css (por exemplo, `my_icon.png`).

>[!NOTE]
>
>A manipulação das folhas de estilos descritas anteriormente é opcional.

Para incluir a biblioteca do cliente no componente de página jsp:

* para incluir o código javascript e as folhas de estilos:
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
em que 
`<category-nameX>` é o nome da biblioteca do lado do cliente.

* para incluir somente o código javascript:
   `<ui:includeClientLib js="<category-name>"/>`

Para obter mais detalhes, consulte a descrição da variável [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) .

Em alguns casos, uma biblioteca do cliente deve estar disponível somente no modo de criação e deve ser excluída no modo de publicação. Pode ser obtido da seguinte forma:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introdução às amostras {#getting-started-with-the-samples}

Para seguir os tutoriais nesta página, instale o pacote chamado **Uso de widgets ExtJS** em uma instância de AEM local e crie uma página de exemplo na qual os componentes serão incluídos. Para fazer isso:

1. Na instância de AEM, baixe o pacote chamado **Uso de widgets ExtJS (v01)** do Compartilhamento de pacotes e instale o pacote. Ele cria o projeto `extjstraining` below `/apps` no repositório.
1. Inclua a biblioteca do cliente que contém os scripts (js) e a folha de estilos (css) na tag head da página geometrixx jsp, já que você incluirá os componentes de amostra em uma nova página do **Geometrixx** ramificação: em **CRXDE Lite** abra o arquivo `/apps/geometrixx/components/page/headlibs.jsp` e adicione o `cq.extjstraining` à categoria existente `<ui:includeClientLib>` da seguinte maneira:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Crie uma nova página no **Geometrixx** ramificação abaixo `/content/geometrixx/en/products` e **Uso de widgets ExtJS**.
1. Vá para o modo de design e adicione todos os componentes do grupo chamados **Uso de widgets ExtJS** à concepção do Geometrixx
1. Volte para o modo de edição: os componentes do grupo **Uso de widgets ExtJS** estão disponíveis no Sidekick.

>[!NOTE]
>
>Os exemplos nesta página são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com o AEM, tendo sido substituído por We.Retail. Consulte o documento [Implementação de referência We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

### Diálogos básicos {#basic-dialogs}

As caixas de diálogo normalmente são usadas para editar conteúdo, mas também podem exibir apenas informações. Uma maneira fácil de visualizar uma caixa de diálogo completa é acessar sua representação no formato json. Para fazer isso, aponte o navegador para:

`https://localhost:4502/<path-to-dialog>.-1.json`

O primeiro componente do **Uso de widgets ExtJS** no Sidekick é chamado **1. Noções básicas da caixa de diálogo** e inclui quatro caixas de diálogo básicas criadas com widgets prontos para uso e sem lógica personalizada de javascript. As caixas de diálogo são armazenadas abaixo `/apps/extjstraining/components/dialogbasics`. Os diálogos básicos são:

* a caixa de diálogo Completo ( `full` node): ela exibe uma janela com 3 guias, cada guia com 2 campos de texto.
* a caixa de diálogo Painel único( `singlepanel` node): ela exibe uma janela com 1 guia que tem 2 campos de texto.
* a caixa de diálogo Multicpainel( `multipanel` node): sua exibição é a mesma da caixa de diálogo Completa, mas é criada de forma diferente.
* a caixa de diálogo Design( `design` node): ela exibe uma janela com 2 guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto que pode ser recolhida. A segunda guia tem um conjunto de campos com 4 campos de texto e um conjunto de campos que pode ser recolhido com 2 campos de texto.

Inclua a **1. Noções básicas da caixa de diálogo** na página de exemplo:

1. Adicione o **1. Noções básicas da caixa de diálogo** para a página de exemplo do **Uso de widgets ExtJS** na guia no **Sidekick**.
1. O componente exibe um título, algum texto e um **PROPRIEDADES** link: clique no link para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente no link para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemplo 1: Caixa de diálogo cheia {#example-full-dialog}

O **Total** exibe uma janela com três guias, cada uma com dois campos de texto. É a caixa de diálogo padrão do **Noções básicas da caixa de diálogo** componente. As suas características são:

* É definido por um nó: tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Exibe 3 guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó :
   `/apps/extjstraining/components/dialogbasics/full`
* É renderizado no formato JSON solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

A caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Exemplo 2: Caixa de diálogo de painel único {#example-single-panel-dialog}

O **Painel único** exibe uma janela com uma guia que tem dois campos de texto. As suas características são:

* Exibe 1 guia (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* A guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* É definido pelo nó :
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Uma vantagem sobre **Caixa de diálogo cheia** é que é necessária menos configuração.
* Utilização recomendada: para caixas de diálogo simples que exibem informações ou têm apenas alguns campos.

Para usar a caixa de diálogo Painel único:

1. Substitua a caixa de diálogo do **Noções básicas da caixa de diálogo** com o **Painel único** caixa de diálogo:
   1. Em **CRXDE Lite**, exclua o nó : `/apps/extjstraining/components/dialogbasics/dialog`
   1. Clique em **Salvar tudo** para salvar as alterações.
   1. Copie o nó : `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Cole o nó copiado abaixo: `/apps/extjstraining/components/dialogbasics`
   1. Selecione o nó : `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`e renomeie-o `dialog`.
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemplo 3: Caixa de diálogo de vários painéis {#example-multi-panel-dialog}

O **Vários painéis** tem a mesma exibição da caixa de diálogo **Total** , mas é construído de forma diferente. As suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Exibe 3 guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó :
   `/apps/extjstraining/components/dialogbasics/multipanel`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Uma vantagem sobre **Caixa de diálogo cheia** é que tem uma estrutura simplificada.
* Utilização recomendada: para caixas de diálogo de várias guias.

Para usar a caixa de diálogo Vários painéis:

1. Substitua a caixa de diálogo do **Noções básicas da caixa de diálogo** com o **Vários painéis** caixa de diálogo: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemplo 4: Diálogo avançado {#example-rich-dialog}

O **Rico** exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto que pode ser recolhida. A segunda guia tem um conjunto de campos com quatro campos de texto e um conjunto de campos que pode ser recolhido com dois campos de texto. As suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 2 guias (tipo de nó = `cq:Panel`).
* A primeira guia tem um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com um ` [textfield](/help/sites-developing/xtypes.md#textfield)` e ` [selection](/help/sites-developing/xtypes.md#selection)` widget com 3 opções e um dispositivo que pode ser recolhido ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` com um ` [textarea](/help/sites-developing/xtypes.md#textarea)` widget.
* A segunda guia tem um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com 4 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets e um redutível `dialogfieldset` com 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets.
* É definido pelo nó :
   `/apps/extjstraining/components/dialogbasics/rich`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar o **Rico** caixa de diálogo:

1. Substitua a caixa de diálogo do **Noções básicas da caixa de diálogo** com o **Rico** caixa de diálogo: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Caixas de diálogo dinâmicas {#dynamic-dialogs}

O segundo componente do **Uso de widgets ExtJS** no Sidekick é chamado **2. Caixas de diálogo dinâmicas** e inclui três caixas de diálogo dinâmicas que são criadas com dispositivos prontos para uso e **com lógica personalizada do javascript**. As caixas de diálogo são armazenadas abaixo `/apps/extjstraining/components/dynamicdialogs`. As caixas de diálogo dinâmicas são:

* a caixa de diálogo Alternar guias ( `switchtabs` node): ela exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.
* o diálogo Arbitrário ( `arbitrary` node): ela exibe uma janela com uma guia. A guia tem um campo para soltar ou fazer upload de um ativo e um campo que exibe algumas informações sobre a página que o contém e sobre o ativo, se houver referência a ele.
* a caixa de diálogo Alternar campos ( `togglefield` node): ela exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando essa opção é marcada, um conjunto de campos com dois campos de texto é exibido.

Para incluir a **2. Caixas de diálogo dinâmicas** na página de exemplo:

1. Adicione o **2. Caixas de diálogo dinâmicas** para a página de exemplo do **Uso de widgets ExtJS** na guia no **Sidekick**.
1. O componente exibe um título, algum texto e um **PROPRIEDADES** link: clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique em novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemplo 1: Caixa de diálogo Alternar guias {#example-switch-tabs-dialog}

O **Guias de troca** exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 2 guias (tipo de nó = `cq:Panel`): 1 guia selection , a segunda guia depende da seleção na primeira guia (3 opções).
* Possui 3 guias opcionais (tipo de nó = `cq:Panel`), cada um tem 2 campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Somente uma guia opcional é exibida de cada vez.
* É definido pela variável `switchtabs` nó em:
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* O nó da caixa de diálogo tem um &quot; `beforeshow`&quot; que oculta todas as guias opcionais antes que a caixa de diálogo seja exibida:
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` obtém o painel de guias que contém o painel de seleção e os 3 painéis opcionais.
* O `Ejst.x2` é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.manageTabs()` , como o valor de `index` for -1, todas as guias opcionais estarão ocultas (vai de 1 a 3).
* A guia de seleção tem 2 ouvintes: uma que mostra a guia selecionada quando a caixa de diálogo é carregada (&quot; `loadcontent`&quot; e uma que mostra a guia selecionada quando a seleção é alterada (&quot; `selectionchanged`&quot;event):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* No `Ejst.x2.showTab()` método :
   `field.findParentByType('tabpanel')` obtém o painel de guias que contém todas as guias ( `field` representa o widget de seleção)
   `field.getValue()` obtém o valor da seleção, por exemplo: tab2
   `Ejst.x2.manageTabs()` exibe a guia selecionada.
* Cada guia opcional tem um ouvinte que oculta a guia em &quot; `render`&quot;event:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* No `Ejst.x2.hideTab()` método :
   `tabPanel` é o painel de guias que contém todas as guias
   `index` é o índice da guia opcional
   `tabPanel.hideTabStripItem(index)` oculta a guia

Ele é exibido da seguinte maneira:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemplo 2: Caixa de diálogo arbitrária {#example-arbitrary-dialog}

Frequentemente, uma caixa de diálogo exibe o conteúdo do componente subjacente. O diálogo descrito aqui, chamado **Arbitrário** , puxa o conteúdo de um componente diferente.

O **Arbitrário** exibe uma janela com uma guia. A guia tem dois campos: uma para soltar ou fazer upload de um ativo e outra que exibe algumas informações sobre a página que contém o ativo e sobre ele, se houver referência a ele.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) com 1 painel (tipo de nó = `cq:Panel`)
* O painel tem um widget smartfile (tipo de nó = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e um widget ownerdraw (tipo de nó = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* É definido pela variável `arbitrary` nó em:
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* O widget ownerdraw tem um &quot; `loadcontent`&quot; listener que mostra informações sobre a página que contém o componente e o ativo referenciado pelo widget smartfile quando o conteúdo é carregado:
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` é definido com o objeto ownerdraw
   `path` é definido com o caminho do conteúdo do componente (por exemplo: /content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialog)
* O `Ejst.x2` é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.showInfo()` método :
   `pagePath` é o caminho da página que contém o componente
   `pageInfo` representa as propriedades da página no formato json
   `reference` é o caminho do ativo referenciado
   `metadata` representa os metadados do ativo no formato json
   `ownerdraw.getEl().update(html);` exibe o html criado na caixa de diálogo

Para usar o **Arbitrário** caixa de diálogo:

1. Substitua a caixa de diálogo do **Caixa de diálogo dinâmica** com o **Arbitrário** caixa de diálogo: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Exemplo 3: Caixa de diálogo Alternar campos {#example-toggle-fields-dialog}

O **Alternar campos** exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando essa opção é marcada, um conjunto de campos com dois campos de texto é exibido.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) com 1 painel (tipo de nó = `cq:Panel`).
* O painel tem um widget de seleção/caixa de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e um widget de conjunto de diálogo que pode ser recolhido (tipo de nó = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que está oculta por padrão, com 2 widgets de campo de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pela variável `togglefields` nó em:
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* a guia de seleção tem 2 ouvintes: um que mostra o conjunto de campos de diálogo quando o conteúdo é carregado (&quot; `loadcontent`&quot;event) e um que mostre o conjunto de campos de diálogo quando a seleção é alterada (&quot; `selectionchanged`&quot;event):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* O `Ejst.x2` é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.toggleFieldSet()` método :
   `box` é o objeto de seleção
   `panel` é o painel que contém a seleção e os widgets de conjunto de caixas de diálogo
   `fieldSet` é o objeto dialog field
   `show` é o valor da seleção (true ou false) com base em &#39; `show`&quot; o conjunto de diálogo é exibido ou não

Para usar o **Alternar campos** caixa de diálogo:

1. Substitua a caixa de diálogo do **Caixa de diálogo dinâmica** com o **Alternar campos** caixa de diálogo: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Os widgets prontos fornecidos com o AEM devem abranger a maioria dos casos de uso. No entanto, às vezes pode ser necessário criar um widget personalizado para cobrir um requisito específico do projeto. É possível criar widgets personalizados estendendo os existentes. Para ajudar você a começar a usar essa personalização, o **Uso de widgets ExtJS** O pacote inclui três caixas de diálogo que usam três widgets personalizados diferentes:

* a caixa de diálogo Vários campos ( `multifield` ) exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que tem dois campos: um menu suspenso com duas opções e um campo de texto. Como é baseado na solução pronta para uso `multifield` widget (que tem apenas um campo de texto), ele tem todos os recursos do `multifield` widget.
* a caixa de diálogo Navegação em árvore ( `treebrowse` nó ) exibe uma janela com uma guia contendo um widget de navegação de caminho: ao clicar na seta, uma janela é aberta e você pode navegar por uma hierarquia e selecionar um item. O caminho do item é então adicionado ao campo de caminho e é mantido quando a caixa de diálogo é fechada.
* uma caixa de diálogo baseada no Plug-in do Editor de Rich Text ( `rteplugin` nó ) que adiciona um botão personalizado ao Editor de Rich Text para inserir um texto personalizado no texto principal. Consiste em um `richtext` widget (RTE) e de um recurso personalizado adicionado por meio do mecanismo de plug-in do RTE.

Os widgets personalizados e o plug-in estão incluídos no componente chamado **3. Widgets personalizados** do **Uso de widgets ExtJS** pacote. Para incluir esse componente na página de exemplo:

1. Adicione o **3. Widgets personalizados** para a página de exemplo do **Uso de widgets ExtJS** na guia no **Sidekick**.
1. O componente exibe um título, algum texto e, ao clicar no botão **PROPRIEDADES** , as propriedades do parágrafo armazenadas no repositório. Clicar novamente oculta as propriedades.
O componente é exibido da seguinte maneira:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemplo 1: Widget de vários campos personalizados {#example-custom-multifield-widget}

O **Multifield personalizado** a caixa de diálogo baseada em widget exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que, diferente do padrão, que tem um campo, tem dois campos: um menu suspenso com duas opções e um campo de texto.

O **Multifield personalizado** caixa de diálogo baseada em widget:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um `multifield` widget (tipo de nó = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* O `multifield` o widget tem um fieldconfig (tipo de nó = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) que se baseia no xtype personalizado &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; é uma opção de configuração do ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` objeto.
   * &#39; `optionsProvider`&#39; é uma configuração do `ejstcustom` widget. É definido com a variável `Ejst.x3.provideOptions` método definido em `exercises.js` em:
      `/apps/extjstraining/clientlib/js/exercises.js`
e retorna 2 opções.
* É definido pela variável `multifield` nó em:
   `/apps/extjstraining/components/customwidgets/multifield`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

O widget de vários campos personalizado (xtype = `ejstcustom`):

* É um objeto javascript chamado `Ejst.CustomWidget`.
* É definido na variável `CustomWidget.js` arquivo javascript em:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende o ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` widget.
* Possui 3 campos: `hiddenField` (Campo de texto), `allowField` (ComboBox) e `otherField` (Campo de texto)
* Substituições `CQ.Ext.Component#initComponent` para adicionar os 3 campos:
   * `allowField` é um [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) objeto do tipo &#39;select&#39;. optionsProvider é uma configuração do objeto Selection que é instanciada com a configuração optionsProvider do CustomWidget definido na caixa de diálogo
   * `otherField` é um [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField) objeto
* Substitui os métodos `setValue`, `getValue` e `getRawValue` de [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) para definir e recuperar o valor de CustomWidget com o formato:
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`.
* Registra-se como &#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

O **Multifield personalizado** a caixa de diálogo baseada em widget é exibida da seguinte maneira:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemplo 2: Widget de navegação por árvore personalizada {#example-custom-treebrowse-widget}

O **Treebrowse** a caixa de diálogo baseada em widget exibe uma janela com uma guia contendo um widget de navegação de caminho personalizado: ao clicar na seta, uma janela é aberta e você pode navegar por uma hierarquia e selecionar um item. O caminho do item é então adicionado ao campo de caminho e é mantido quando a caixa de diálogo é fechada.

A caixa de diálogo de navegação da árvore personalizada:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget personalizado (tipo de nó = `cq:Widget`, xtype = `ejstbrowse`)
* É definido pela variável `treebrowse` nó em:
   `/apps/extjstraining/components/customwidgets/treebrowse`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

O widget de navegação em árvore personalizado (xtype = `ejstbrowse`):

* É um objeto javascript chamado `Ejst.CustomWidget`.
* É definido na variável `CustomBrowseField.js` arquivo javascript em:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Estende ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define uma janela de navegação chamada `browseWindow`.
* Substituições ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar a janela de navegação quando a seta é clicada.
* Define um [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) objeto:
   * Ele obtém seus dados ao chamar o servlet registrado em `/bin/wcm/siteadmin/tree.json`.
   * Sua raiz é &quot; `apps/extjstraining`&quot;.
* Define um `window` objeto ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Baseado no painel predefinido.
   * Possui um **OK** botão que define o valor do caminho selecionado e oculta o painel.
* A janela está ancorada abaixo da **Caminho** campo.
* O caminho selecionado é passado do campo de navegação para a janela em `show` evento.
* Registra-se como &#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar o **Navegação de árvore personalizada** caixa de diálogo baseada em widget:

1. Substitua a caixa de diálogo do **Widgets personalizados** com o **Navegação de árvore personalizada** caixa de diálogo: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemplo 3: Plug-in do Editor de Rich Text (RTE) {#example-rich-text-editor-rte-plug-in}

O **Plug-in do Editor de Rich Text (RTE)** a caixa de diálogo baseada é uma caixa de diálogo baseada no Editor de Rich Text que tem um botão personalizado para inserir texto personalizado entre colchetes. O texto personalizado pode ser analisado por alguma lógica do lado do servidor (não implementada neste exemplo), por exemplo, para adicionar texto definido no caminho especificado:

O **Plug-in do RTE** caixa de diálogo baseada:

* É definido pelo nó do reteplugin em:
   `/apps/extjstraining/components/customwidgets/rteplugin`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* O `rtePlugins` o nó tem um nó filho `inserttext` (tipo de nó = `nt:unstructured`) que é nomeado após o plug-in. Ela tem uma propriedade chamada `features`, que define qual dos recursos do plug-in está disponível para o RTE.

O plug-in do RTE:

* É um objeto javascript chamado `Ejst.InsertTextPlugin`.
* É definido na variável `InsertTextPlugin.js` arquivo javascript em:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende o ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` objeto.
* Os métodos a seguir definem a variável ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` e são substituídos no plug-in de implementação:
   * `getFeatures()` retorna uma matriz de todos os recursos que o plug-in disponibiliza.
   * `initializeUI()` adiciona o novo botão à barra de ferramentas do RTE.
   * `notifyPluginConfig()` exibe título e texto quando o botão é posicionado com o mouse.
   * `execute()` é chamado quando o botão é clicado e executa a ação do plug-in: ela exibe uma janela usada para definir o texto a ser incluído.
* `insertText()` insere um texto usando o objeto de diálogo correspondente `Ejst.InsertTextPlugin.Dialog` (consulte posteriormente).
* `executeInsertText()` é chamado pelo `apply()` método da caixa de diálogo, que é acionado quando a função **OK** é clicado.
* Registra-se como &#39; `inserttext`Plug-in &#39;:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* o `Ejst.InsertTextPlugin.Dialog` O objeto define a caixa de diálogo que é aberta ao clicar no botão do plug-in. A caixa de diálogo consiste em um painel, um formulário, um campo de texto e dois botões (**OK** e **Cancelar**).

Para usar o **Plug-in do Editor de Rich Text (RTE)** caixa de diálogo baseada:

1. Substitua a caixa de diálogo do **Widgets personalizados** com o **Plug-in do Editor de Rich Text (RTE)** caixa de diálogo baseada: siga as etapas descritas para a [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente.
1. Clique no último ícone à direita (aquele com quatro setas). Insira um caminho e clique em **OK**: O caminho é exibido entre parênteses ([ ]).
1. Clique em **OK** para fechar o Editor de Rich Text.

O **Plug-in do Editor de Rich Text (RTE)** a caixa de diálogo baseada é exibida da seguinte maneira:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este exemplo mostra apenas como implementar a parte do lado do cliente da lógica: os espaços reservados (*[texto]*) devem ser analisados explicitamente no lado do servidor (por exemplo, no componente JSP).

### Visão geral da árvore {#tree-overview}

O pronto para uso ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` O objeto fornece representação de interface de usuário estruturada em árvore de dados estruturados em árvore. O componente Visão geral da árvore incluído na **Uso de widgets ExtJS** mostra como usar o `TreePanel` para exibir uma árvore JCR abaixo de um determinado caminho. A janela propriamente dita pode ser encaixada/desencaixada. Neste exemplo, a lógica da janela é incorporada no componente jsp entre &lt;script>&lt;/script> tags.

Para incluir a **Visão geral da árvore** componente para a página de exemplo:

1. Adicione o **4. Visão geral da árvore** para a página de exemplo do **Uso de widgets ExtJS** na guia no **Sidekick**.
1. O componente exibe:
   * um título, com texto
   * a **PROPRIEDADES** link: clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique em novamente para ocultar as propriedades.
   * uma janela flutuante com uma representação em árvore do repositório, que pode ser expandida.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

O componente Visão geral da árvore :

* Está definido em:
   `/apps/extjstraining/components/treeoverview`

* Sua caixa de diálogo permite definir o tamanho da janela e ancorar/desancorar a janela (veja os detalhes abaixo).

O componente jsp:

* Recupera a largura, a altura e as propriedades ancoradas do repositório.
* Exibe algum texto sobre o formato de dados da visão geral da árvore.
* Incorpora a lógica de janela no componente jsp entre tags javascript.
* Está definido em:
   `apps/extjstraining/components/treeoverview/content.jsp`

O código javascript incorporado no componente jsp:

* Define um `tree` tentando recuperar uma janela de árvore da página.
* Se a janela que exibe a árvore não existir, `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) é criada:
   * `treePanel` contém os dados usados para criar a janela .
   * Os dados são recuperados chamando o servlet registrado em:
      `/bin/wcm/siteadmin/tree.json`
* O `beforeload` o ouvinte garante que o nó clicado seja carregado.
* O `root` objeto define o caminho `apps/extjstraining` como a raiz da árvore.
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`) é definida com base em `treePanel`e é exibido com:
   `tree.show();`
* Se a janela já existir, ela será exibida com base na largura, altura e propriedades ancoradas recuperadas do repositório.

A caixa de diálogo do componente:

* Exibe 1 guia com 2 campos para definir o tamanho (largura e altura) da janela de visão geral da árvore e 1 campo para ancorar/cancelar a âncora da janela
* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget sizefield (tipo de nó = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e um widget de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) com 2 opções (true/false)
* É definido pelo nó de diálogo em:
   `/apps/extjstraining/components/treeoverview/dialog`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* É exibido da seguinte maneira:

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Visão geral da grade {#grid-overview}

Um Painel de grade representa dados em um formato tabular de linhas e colunas. Ele é composto pelo seguinte:

* Armazenar : o modelo que mantém os registros de dados (linhas).
* Modelo de coluna : a composição da coluna.
* Exibir : encapsula a interface do usuário.
* Modelo de seleção : o comportamento de seleção.

O componente Visão geral da grade incluído na **Uso de widgets ExtJS** pacote mostra como exibir dados em um formato tabular:

* O exemplo 1 usa dados estáticos.
* O exemplo 2 usa dados recuperados do repositório.

Para incluir o componente Visão geral da grade na página de exemplo:

1. Adicione o **5. Visão geral da grade** para a página de exemplo do **Uso de widgets ExtJS** na guia no **Sidekick**.
1. O componente exibe:
   * um título com texto
   * a **PROPRIEDADES** link: clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique em novamente para ocultar as propriedades.
   * uma janela flutuante contendo dados em formato tabular.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemplo 1: Grade Padrão {#example-default-grid}

Em sua versão inicial, a variável **Visão geral da grade** componente exibe uma janela com dados estáticos em um formato tabular. Neste exemplo, a lógica é incorporada no componente jsp de duas maneiras:

* a lógica genérica é definida entre &lt;script>&lt;/script> tags
* a lógica específica está disponível em um arquivo .js separado e é vinculada ao jsp. This setup enables to easily switch between the two logic (static/dynamic) by commenting the desired &lt;script> tags.

O componente Visão geral da grade:

* Está definido em:
   `/apps/extjstraining/components/gridoverview`
* Sua caixa de diálogo permite definir o tamanho da janela e ancorar/desancorar a janela.

O componente jsp:

* Recupera a largura, a altura e as propriedades ancoradas do repositório.
* Exibe algum texto como introdução ao formato de dados de visão geral da grade.
* Faz referência ao código javascript que define o objeto GridPanel:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` define alguns dados estáticos como base para o objeto GridPanel.
* Incorpora código javascript entre tags javascript que define o objeto Window consumindo o objeto GridPanel.
* Está definido em:
   `apps/extjstraining/components/gridoverview/content.jsp`

O código javascript incorporado no componente jsp:

* Define o `grid` tentando recuperar o componente da janela da página:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* If `grid` não existe, um [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) objeto ( `gridPanel`) é definido ao chamar a função `getGridPanel()` método (veja abaixo). Esse método é definido em `defaultgrid.js`.
* `grid` é um ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` objeto, com base no GridPanel predefinido e é exibido: `grid.show();`
* If `grid` já existe, ele é exibido com base na largura, altura e propriedades ancoradas recuperadas do repositório.

O arquivo javascript ( `defaultgrid.js`) referenciado no componente jsp define o `getGridPanel()` método chamado pelo script incorporado no JSP e retorna um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` , com base em dados estáticos. A lógica é a seguinte:

* `myData` é uma matriz de dados estáticos formatada como uma tabela de 5 colunas e 4 linhas.
* `store` é um `CQ.Ext.data.Store` objeto que consome `myData`.
* `store` é carregado na memória:
   `store.load();`
* `gridPanel` é um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto que consome `store`:
   * as larguras de coluna são sempre reproporcionais:
      `forceFit: true`
   * somente uma linha por vez pode ser selecionada:
      `singleSelect:true`

#### Exemplo 2: Grade de Pesquisa de Referência {#example-reference-search-grid}

Ao instalar o pacote, a variável `content.jsp` do **Visão geral da grade** componente exibe uma grade baseada em dados estáticos. É possível modificar o componente para exibir uma grade com as seguintes características:

* Tem três colunas.
* É baseado em dados recuperados do repositório chamando um servlet.
* As células da última coluna podem ser editadas. O valor é persistente em um `test` abaixo do nó definido pelo caminho exibido na primeira coluna.

Como explicado na seção anterior, o objeto da janela recebe suas ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` chamando o `getGridPanel()` definido na variável `defaultgrid.js` arquivo em `/apps/extjstraining/components/gridoverview/defaultgrid.js`. O componente **Visão geral da grade **fornece uma implementação diferente para o `getGridPanel()` , definido na variável `referencesearch.js` arquivo em `/apps/extjstraining/components/gridoverview/referencesearch.js`. Ao alternar o arquivo .js referenciado no componente jsp, a grade será baseada nos dados recuperados do repositório.

Alterne o arquivo .js mencionado no componente jsp:

1. Em **CRXDE Lite** no `content.jsp` do componente, comente a linha que inclui a `defaultgrid.js` para ter a seguinte aparência:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Remova o comentário da linha que inclui o `referencesearch.js` para ter a seguinte aparência:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salve as alterações.
1. Atualize a página de exemplo.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

O código javascript referenciado no componente jsp ( `referencesearch.js`) define a variável `getGridPanel()` método chamado do componente jsp e retorna um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` , com base em dados recuperados dinamicamente do repositório. A lógica em `referencesearch.js` define alguns dados dinâmicos como base para o Painel de grade:

* `reader` é um ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`objeto que lê a resposta do servlet no formato json para 3 colunas.
* `cm` é um ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` objeto para 3 colunas.
As células da coluna &quot;Test&quot; podem ser editadas conforme são definidas com um editor:
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* as colunas são classificáveis:
   `cm.defaultSortable = true;`
* `store` é um ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` objeto:
   * ele obtém seus dados ao chamar o servlet registrado em &quot; `/bin/querybuilder.json`&quot; com alguns parâmetros usados para filtrar o query
   * se baseia em `reader`, previamente definido
   * a tabela é classificada de acordo com o **jcr:path**&quot; em ordem crescente
* `gridPanel` é um ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` objeto que pode ser editado:
   * é baseada no `store` e no modelo de coluna `cm`
   * somente uma linha por vez pode ser selecionada:
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * o `afteredit` o ouvinte garante que, depois de uma célula no &quot;**Teste**&quot; foi editada:
      * a propriedade &#39; `test`&#39; do nó no caminho definido pelo &quot;**jcr:path**&quot; é definida no repositório com o valor da célula
      * se o POST for bem-sucedido, o valor será adicionado ao `store` objeto, caso contrário, será rejeitado
