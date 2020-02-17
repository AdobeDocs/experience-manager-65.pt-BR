---
title: Uso e extensão de widgets (interface clássica)
seo-title: Uso e extensão de widgets (interface clássica)
description: A interface baseada na Web do AEM usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG do conteúdo pelos autores diretamente na página da Web
seo-description: A interface baseada na Web do AEM usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG do conteúdo pelos autores diretamente na página da Web
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Uso e extensão de widgets (interface clássica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página descreve o uso de widgets na interface clássica, que foi substituída no AEM 6.4.
>
>A Adobe recomenda que você aproveite a interface [moderna e habilitada para](/help/sites-developing/touch-ui-concepts.md) toque, com base na interface do usuário [](/help/sites-developing/touch-ui-concepts.md#coral-ui) Coral e na interface do usuário [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

A interface baseada na Web do Adobe Experience Manager usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG do conteúdo pelos autores diretamente na página da Web.

O Adobe Experience Manager (AEM) usa a biblioteca de widgets [ExtJS](https://www.sencha.com/) , que fornece os elementos altamente avançados da interface do usuário que funcionam em todos os navegadores mais importantes e permitem a criação de experiências de interface de usuário de nível desktop.

Esses widgets estão incluídos no AEM e, além de serem usados pelo próprio AEM, podem ser usados por qualquer site criado com o AEM.

Para obter uma referência completa de todos os widgets disponíveis no AEM, consulte a documentação [da API do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) widget ou a [lista de xtypes](/help/sites-developing/xtypes.md)existentes. Além disso, muitos exemplos que mostram como usar a estrutura ExtJS estão disponíveis no site [Sencha](https://www.sencha.com/products/extjs/examples/) , o proprietário da estrutura.

Esta página fornece algumas informações sobre como usar e estender widgets. Primeiro, descreve como [incluir o código do lado do cliente em uma página](#including-the-client-sided-code-in-a-page). Em seguida, ele descreve alguns componentes de amostra que foram criados para ilustrar algumas extensões e usos básicos. Esses componentes estão disponíveis no pacote **Usando widgets** ExtJS em Compartilhamento **de** pacotes.

O pacote inclui exemplos de:

* [Diálogos](#basic-dialogs) básicos criados com widgets predefinidos.
* [Diálogos](#dynamic-dialogs) dinâmicos criados com widgets predefinidos e lógica javascript personalizada.
* Diálogos com base em widgets [](#custom-widgets)personalizados.
* Um painel [de](#tree-overview) árvore exibindo uma árvore JCR abaixo de um determinado caminho.
* Um painel [de](#grid-overview) grade que exibe dados em um formato tabular.

>[!NOTE]
>
>A interface clássica do Adobe Experience Manager foi desenvolvida com base no [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusão do código do lado do cliente em uma página {#including-the-client-sided-code-in-a-page}

O javascript do lado do cliente e o código da folha de estilo devem ser colocados em uma biblioteca do cliente.

Para criar uma biblioteca de cliente:

1. Crie um nó abaixo `/apps/<project>` com as seguintes propriedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:PrimaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * category=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;
   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Abaixo, `clientlib` crie as pastas `css` e `js` pastas (nt:folder).

1. Abaixo, `clientlib` crie os arquivos `css.txt` e `js.txt` arquivos (nt:files). Esses arquivos .txt listam os arquivos que estão incluídos na biblioteca.

1. Editar `js.txt`: precisa começar com &#39; `#base=js`&#39; seguido da lista de arquivos que serão agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: precisa começar com &#39; `#base=css`&#39; seguido da lista de arquivos que serão agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=css
    components.css
   ```

1. Abaixo da `js` pasta, coloque os arquivos javascript que pertencem à biblioteca.

1. Abaixo da `css` pasta, coloque os `.css` arquivos e os recursos usados pelos arquivos css (por exemplo, `my_icon.png`).

>[!NOTE]
>
>A manipulação das folhas de estilos descritas anteriormente é opcional.

Para incluir a biblioteca do cliente no componente de página jsp:

* para incluir código javascript e folhas de estilo:
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
onde `<category-nameX>` é o nome da biblioteca do lado do cliente.

* para incluir somente código javascript:
   `<ui:includeClientLib js="<category-name>"/>`

Para obter mais detalhes, consulte a descrição da tag [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) .

Em alguns casos, uma biblioteca de cliente deve estar disponível somente no modo de autor e deve ser excluída no modo de publicação. Pode ser obtido da seguinte forma:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introdução às amostras {#getting-started-with-the-samples}

Para seguir os tutoriais desta página, instale o pacote chamado **Uso de widgets** ExtJS em uma instância do AEM local e crie uma página de amostra na qual os componentes serão incluídos. Para isso:

1. Em sua instância do AEM, baixe o pacote chamado **Usando widgets ExtJS (v01)** do Compartilhamento de pacotes e instale o pacote. Ele cria o projeto `extjstraining` abaixo `/apps` no repositório.
1. Inclua a biblioteca do cliente que contém os scripts (js) e a folha de estilo (css) na tag head da página geometrixx jsp, já que você incluirá os componentes de amostra em uma nova página da ramificação **Geometrixx** :
no **CRXDE Lite** , abra o arquivo `/apps/geometrixx/components/page/headlibs.jsp` e adicione a `cq.extjstraining` categoria à `<ui:includeClientLib>` tag existente da seguinte maneira:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Crie uma nova página na ramificação **Geometrixx** abaixo `/content/geometrixx/en/products` e chame-a **usando widgets** ExtJS.
1. Vá para o modo de design e adicione todos os componentes do grupo chamados **Usando widgets** ExtJS ao design do Geometrixx
1. Voltar no modo de edição: os componentes do grupo **Usando widgets** ExtJS estão disponíveis no Sidekick.

>[!NOTE]
>
>Os exemplos nesta página são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com o AEM, tendo sido substituído por We.Retail. Consulte o documento Implementação [de referência](/help/sites-developing/we-retail.md#we-retail-geometrixx) We.Retail para obter instruções sobre como baixar e instalar o Geometrixx.

### Diálogos básicos {#basic-dialogs}

Normalmente, as caixas de diálogo são usadas para editar conteúdo, mas também podem exibir informações. Uma maneira fácil de visualizar uma caixa de diálogo completa é acessar sua representação em formato json. Para isso, aponte o navegador para:

`https://localhost:4502/<path-to-dialog>.-1.json`

O primeiro componente do grupo **Usando widgets** ExtJS no Sidekick é chamado de **1. Conceitos básicos** da caixa de diálogo e inclui quatro diálogos básicos criados com widgets prontos e sem lógica javascript personalizada. As caixas de diálogo são armazenadas abaixo `/apps/extjstraining/components/dialogbasics`. Os diálogos básicos são:

* a caixa de diálogo Completo ( `full` nó): exibe uma janela com 3 guias, cada uma com 2 campos de texto.
* a caixa de diálogo Painel único ( `singlepanel` nó): exibe uma janela com 1 guia que tem 2 campos de texto.
* a caixa de diálogo Multi Panel (nó `multipanel` ): sua exibição é igual à caixa de diálogo Completo, mas é criada de forma diferente.
* a caixa de diálogo Design ( `design` nó): ela exibe uma janela com 2 guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto flexível. A segunda guia tem um conjunto de campos com 4 campos de texto e um conjunto de campos que pode ser recolhido com 2 campos de texto.

Inclua o **1. Componente Noções básicas** da caixa de diálogo na página de amostra:

1. Adicione o **1. Noções básicas** da caixa de diálogo para a página de amostra da guia **Uso de widgets** ExtJS no **Sidekick**.
1. O componente exibe um título, um texto e um link **PROPRIEDADES** : clique no link para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente no link para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemplo 1: Diálogo completo {#example-full-dialog}

A caixa de diálogo **Completo** exibe uma janela com três guias, cada uma com dois campos de texto. É a caixa de diálogo padrão do componente **Conceitos básicos** da caixa de diálogo. As suas características são:

* É definido por um nó: tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Exibe 3 guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/full`
* É renderizado no formato JSON solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

A caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Exemplo 2: Caixa de diálogo de painel único {#example-single-panel-dialog}

A caixa de diálogo Painel **** único exibe uma janela com uma guia que tem dois campos de texto. As suas características são:

* Exibe 1 guia (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* A guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Uma vantagem em relação à caixa de diálogo **** completa é a necessidade de menos configurações.
* Uso recomendado: para caixas de diálogo simples que exibem informações ou têm apenas alguns campos.

Para usar a caixa de diálogo Painel único:

1. Substitua a caixa de diálogo do componente Informações básicas **da caixa de diálogo pela caixa de diálogo Painel** **** único:
   1. No **CRXDE Lite**, exclua o nó: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Clique em **Salvar tudo** para salvar as alterações.
   1. Copie o nó: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Cole o nó copiado abaixo: `/apps/extjstraining/components/dialogbasics`
   1. Selecione o nó: `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`e renomeie-o `dialog`.
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemplo 3: Caixa de diálogo de vários painéis {#example-multi-panel-dialog}

A caixa de diálogo **Vários painéis** tem a mesma exibição da caixa de diálogo **Completa** , mas é criada de forma diferente. As suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Exibe 3 guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/multipanel`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Uma vantagem em relação ao diálogo **** completo é que ele tem uma estrutura simplificada.
* Uso recomendado: para caixas de diálogo de várias guias.

Para usar a caixa de diálogo Vários painéis:

1. Substitua a caixa de diálogo do componente **Conceitos básicos** da caixa de diálogo **Vários painéis** :
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemplo 4: Diálogo avançado {#example-rich-dialog}

A caixa de diálogo **Rico** exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto flexível. A segunda guia tem um conjunto de campos com quatro campos de texto e um conjunto de campos que pode ser recolhido com dois campos de texto. As suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 2 guias (tipo de nó = `cq:Panel`).
* A primeira guia tem um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com um ` [textfield](/help/sites-developing/xtypes.md#textfield)` e um ` [selection](/help/sites-developing/xtypes.md#selection)` widget com 3 opções e um widget que pode ser recolhido ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` com um ` [textarea](/help/sites-developing/xtypes.md#textarea)` widget.
* A segunda guia tem um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com 4 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets e um widget que pode ser recolhido `dialogfieldset` com 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets.
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/rich`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar a caixa de diálogo **Avançado** :

1. Substitua a caixa de diálogo do componente **Conceitos básicos** da caixa de diálogo **Avançado** :
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Diálogos dinâmicos {#dynamic-dialogs}

O segundo componente do grupo **Usando widgets** ExtJS no Sidekick é chamado de **2. Diálogos** dinâmicos e inclui três diálogos dinâmicos que são criados com widgets predefinidos e **com lógica** javascript personalizada. As caixas de diálogo são armazenadas abaixo `/apps/extjstraining/components/dynamicdialogs`. As caixas de diálogo dinâmicas são:

* a caixa de diálogo Alternar guias ( `switchtabs` nó): ela exibe uma janela com duas guias. A primeira guia tem uma seleção de rádio com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.
* o diálogo Arbitrário ( `arbitrary` nó): exibe uma janela com uma guia. A guia tem um campo para soltar ou fazer upload de um ativo e um campo que exibe algumas informações sobre a página que o contém e sobre o ativo, se houver referência.
* a caixa de diálogo Alternar campos ( `togglefield` nó): exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando estiver marcado, um conjunto de campos com dois campos de texto será exibido.

Para incluir o **2. Componente de caixas de diálogo** dinâmicas na página de amostra:

1. Adicione o **2. O componente Diálogos** dinâmicos para a página de amostra da guia **Usando widgets** ExtJS no **Sidekick**.
1. O componente exibe um título, um texto e um link **PROPRIEDADES** : clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemplo 1: Caixa de diálogo Alternar guias {#example-switch-tabs-dialog}

A caixa de diálogo **Alternar guias** exibe uma janela com duas guias. A primeira guia tem uma seleção de rádio com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 2 guias (tipo de nó = `cq:Panel`): 1 guia de seleção, a segunda guia depende da seleção na primeira guia (3 opções).
* Tem 3 guias opcionais (tipo de nó = `cq:Panel`), cada uma tem 2 campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Somente uma guia opcional é exibida por vez.
* É definido pelo `switchtabs` nó em:
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* O nó de diálogo tem um listener &quot; `beforeshow`&quot; que oculta todas as guias opcionais antes da exibição da caixa de diálogo:
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
   `dialog.items.get(0)` obtém o painel de guias que contém o painel de seleção e os três painéis opcionais.
* O `Ejst.x2` objeto é definido no `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.manageTabs()` método, como o valor de `index` é -1, todas as guias opcionais estão ocultas (i vai de 1 a 3).
* A guia de seleção tem dois ouvintes: um que mostra a guia selecionada quando a caixa de diálogo é carregada (&quot;evento `loadcontent`&quot;) e outro que mostra a guia selecionada quando a seleção é alterada (&quot;evento&quot; `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* No `Ejst.x2.showTab()` método:
   `field.findParentByType('tabpanel')` obtém o painel de guias que contém todas as guias ( `field` representa o widget de seleção)
   `field.getValue()` obtém o valor da seleção, por exemplo: tab2
   `Ejst.x2.manageTabs()` exibe a guia selecionada.
* Cada guia opcional tem um ouvinte que oculta a guia no evento &quot; `render`&quot;:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* No `Ejst.x2.hideTab()` método:
   `tabPanel` é o painel de guias que contém todas as guias
   `index` é o índice da guia opcional
   `tabPanel.hideTabStripItem(index)` oculta a guia

Ele é exibido da seguinte maneira:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemplo 2: Diálogo Arbitrário {#example-arbitrary-dialog}

Muitas vezes, uma caixa de diálogo exibe o conteúdo do componente subjacente. A caixa de diálogo descrita aqui, chamada de diálogo **Arbitrário** , extrai o conteúdo de um componente diferente.

A caixa de diálogo **Arbitrário** exibe uma janela com uma guia. A guia tem dois campos: um para soltar ou carregar um ativo e outro que exibe algumas informações sobre a página que o contém e sobre o ativo, se houver uma referência.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de tabulação (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) com 1 painel (tipo de nó = `cq:Panel`)
* O painel tem um widget smartfile (tipo de nó = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e um widget ownerdraw (tipo de nó = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* É definido pelo `arbitrary` nó em:
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* O widget ownerdraw tem um ouvinte &quot; `loadcontent`&quot; que mostra informações sobre a página que contém o componente e o ativo referenciado pelo widget smartfile quando o conteúdo é carregado:
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
   `field` é definido com o objeto ownerdraw
   `path` é definida com o caminho de conteúdo do componente (por exemplo: /content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* O `Ejst.x2` objeto é definido no `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.showInfo()` método:
   `pagePath` é o caminho da página que contém o componente
   `pageInfo` representa as propriedades da página no formato json
   `reference` é o caminho do ativo referenciado
   `metadata` representa os metadados do ativo em formato json
   `ownerdraw.getEl().update(html);` exibe o html criado na caixa de diálogo

Para usar a caixa de diálogo **Arbitrária** :

1. Substitua a caixa de diálogo do componente Diálogo **** dinâmico pela caixa de diálogo **Arbitrária** :
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Exemplo 3: Caixa de diálogo Alternar campos {#example-toggle-fields-dialog}

A caixa de diálogo **Alternar campos** exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando estiver marcado, um conjunto de campos com dois campos de texto será exibido.

As suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) com 1 painel (tipo de nó = `cq:Panel`).
* O painel tem um widget de seleção/caixa de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e um widget de conjunto de diálogo flexível (tipo de nó = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que está oculto por padrão, com 2 widgets de campo de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo `togglefields` nó em:
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

A lógica é implementada por meio de ouvintes de eventos e código javascript da seguinte maneira:

* a guia de seleção tem dois ouvintes: um que mostra o conjunto de diálogo quando o conteúdo é carregado (&quot;evento `loadcontent`&quot;) e outro que mostra o conjunto de diálogo quando a seleção é alterada (&quot;evento `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* O `Ejst.x2` objeto é definido no `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.toggleFieldSet()` método:
   `box` é o objeto de seleção
   `panel` é o painel que contém a seleção e os widgets dialogfieldset
   `fieldSet` é o objeto dialogfieldset
   `show` é o valor da seleção (true ou false) com base em &#39; `show`&#39;, o conjunto de diálogo é exibido ou não

Para usar a caixa de diálogo **Alternar campos** :

1. Substitua a caixa de diálogo do componente Caixa de diálogo **** dinâmica pela caixa de diálogo **Alternar campos** :
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Os widgets prontos fornecidos com o AEM devem abranger a maioria dos casos de uso. No entanto, às vezes pode ser necessário criar um widget personalizado para cobrir um requisito específico do projeto. É possível criar widgets personalizados estendendo os existentes. Para ajudá-lo a começar a usar essa personalização, o pacote **Usando widgets** ExtJS inclui três caixas de diálogo que usam três widgets personalizados diferentes:

* a caixa de diálogo Vários campos ( `multifield` nó) exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que tem dois campos: um menu suspenso com duas opções e um campo de texto. Como se baseia no widget `multifield` pronto para uso (que tem apenas um campo de texto), ele tem todos os recursos do `multifield` widget.
* a caixa de diálogo Navegação em árvore ( `treebrowse` nó) exibe uma janela com uma guia que contém um widget de navegação em caminho: quando você clica na seta, uma janela é aberta na qual você pode navegar por uma hierarquia e selecionar um item. O caminho do item é então adicionado ao campo de caminho e persiste quando a caixa de diálogo é fechada.
* uma caixa de diálogo ( `rteplugin` nó) baseada no Editor de Rich Text que adiciona um botão personalizado ao Editor de Rich Text para inserir algum texto personalizado ao texto principal. Ele consiste em um `richtext` widget (RTE) e de um recurso personalizado que é adicionado por meio do mecanismo de plug-in do RTE.

Os widgets personalizados e o plug-in são incluídos no componente chamado **3. Widgets** personalizados do pacote **Usando widgets** ExtJS. Para incluir esse componente na página de amostra:

1. Adicione o **3. Widgets** personalizados para a página de amostra da guia **Usando widgets** ExtJS no **Sidekick**.
1. O componente exibe um título, algum texto e, ao clicar no link **PROPRIEDADES** , as propriedades do parágrafo armazenadas no repositório. Clicar novamente oculta as propriedades.
O componente é exibido da seguinte maneira:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemplo 1: Widget de vários campos personalizados {#example-custom-multifield-widget}

A caixa de diálogo baseada no widget Multicampo **** personalizado exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que, ao contrário do widget padrão, tem dois campos: um menu suspenso com duas opções e um campo de texto.

A caixa de diálogo **personalizada com base no widget Multicampo** :

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um `multifield` widget (tipo de nó = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* O `multifield` widget tem um fieldconfig (tipo de nó = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) baseado no xtype personalizado &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; é uma opção de configuração do ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` objeto.
   * &#39; `optionsProvider`&#39; é uma configuração do `ejstcustom` widget. É definido com o `Ejst.x3.provideOptions` método definido em `exercises.js` :
      `/apps/extjstraining/clientlib/js/exercises.js`
e retorna 2 opções.
* É definido pelo `multifield` nó em:
   `/apps/extjstraining/components/customwidgets/multifield`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

O widget multicampo personalizado (xtype = `ejstcustom`):

* É um objeto javascript chamado `Ejst.CustomWidget`.
* Está definido no arquivo `CustomWidget.js` javascript em:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende o ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` widget.
* Tem 3 campos: `hiddenField` (Campo de texto), `allowField` (ComboBox) e `otherField` (Campo de texto)
* Substitui `CQ.Ext.Component#initComponent` para adicionar os 3 campos:
   * `allowField` é um objeto [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) do tipo &#39;select&#39;. optionsProvider é uma configuração do objeto Selection que é instanciada com a configuração optionsProvider do CustomWidget definido na caixa de diálogo
   * `otherField` é um objeto [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)
* Substitui os métodos `setValue`, `getValue` e `getRawValue` de [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) para definir e recuperar o valor de CustomWidget com o formato:
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`.
* Registra-se como &#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

A caixa de diálogo baseada no widget Multicampo **** personalizado é exibida da seguinte maneira:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemplo 2: Widget Navegador de árvore personalizado {#example-custom-treebrowse-widget}

A caixa de diálogo personalizada com base no widget **Treebrowse** exibe uma janela com uma guia contendo um widget de navegação de caminho personalizado: quando você clica na seta, uma janela é aberta na qual você pode navegar por uma hierarquia e selecionar um item. O caminho do item é então adicionado ao campo de caminho e persiste quando a caixa de diálogo é fechada.

A caixa de diálogo personalizada de navegação por árvore:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe 1 widget do painel de guias (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget personalizado (tipo de nó = `cq:Widget`, xtype = `ejstbrowse`)
* É definido pelo `treebrowse` nó em:
   `/apps/extjstraining/components/customwidgets/treebrowse`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

O widget personalizado de navegadores terrestres (xtype = `ejstbrowse`):

* É um objeto javascript chamado `Ejst.CustomWidget`.
* Está definido no arquivo `CustomBrowseField.js` javascript em:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Estende-se ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define uma janela de navegação chamada `browseWindow`.
* Substitui ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar a janela de navegação quando a seta é clicada.
* Define um objeto [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) :
   * Ele recebe seus dados ligando para o servlet registrado em `/bin/wcm/siteadmin/tree.json`.
   * Sua raiz é &quot; `apps/extjstraining`&quot;.
* Define um `window` objeto ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Baseado no painel predefinido.
   * Tem um botão **OK** que define o valor do caminho selecionado e oculta o painel.
* A janela é ancorada abaixo do campo **Caminho** .
* O caminho selecionado é transmitido do campo de navegação para a janela no `show` evento.
* Registra-se como &#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar a caixa de diálogo baseada no widget **Custom Treebrowse** :

1. Substitua a caixa de diálogo do componente Widgets **** personalizados pela caixa de diálogo Navegação em árvore **** personalizada:
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemplo 3: Plug-in de Editor de Rich Text (RTE) {#example-rich-text-editor-rte-plug-in}

A caixa de diálogo baseada no plug-in **** do Editor de Rich Text (RTE) é uma caixa de diálogo baseada no Editor de Rich Text que tem um botão personalizado para inserir algum texto personalizado entre colchetes. O texto personalizado pode ser analisado por alguma lógica do lado do servidor (não implementada neste exemplo), por exemplo, para adicionar algum texto definido no caminho especificado:

A caixa de diálogo baseada no plug-in **** do RTE:

* É definido pelo nó do plug-in em:
   `/apps/extjstraining/components/customwidgets/rteplugin`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* O `rtePlugins` nó tem um nó filho `inserttext` (tipo de nó = `nt:unstructured`) nomeado após o plug-in. Ela tem uma propriedade chamada `features`, que define quais dos recursos de plug-in estão disponíveis para o RTE.

O plug-in RTE:

* É um objeto javascript chamado `Ejst.InsertTextPlugin`.
* Está definido no arquivo `InsertTextPlugin.js` javascript em:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende o ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` objeto.
* Os seguintes métodos definem o ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` objeto e são substituídos no plug-in de implementação:
   * `getFeatures()` retorna uma matriz de todos os recursos disponibilizados pelo plug-in.
   * `initializeUI()` adiciona o novo botão à barra de ferramentas RTE.
   * `notifyPluginConfig()` exibe o título e o texto quando o botão é posicionado com o cursor do mouse.
   * `execute()` é chamado quando o botão é clicado e executa a ação do plug-in: exibe uma janela que é usada para definir o texto a ser incluído.
* `insertText()` insere um texto usando o objeto de caixa de diálogo correspondente `Ejst.InsertTextPlugin.Dialog` (consulte a seguir).
* `executeInsertText()` é chamado pelo `apply()` método da caixa de diálogo, que é acionado quando o botão **OK** é clicado.
* Registra-se como plug-in &#39; `inserttext`&#39;:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* o `Ejst.InsertTextPlugin.Dialog` objeto define a caixa de diálogo que é aberta quando o botão do plug-in é clicado. A caixa de diálogo consiste em um painel, um formulário, um campo de texto e dois botões (**OK** e **Cancelar**).

Para usar a caixa de diálogo baseada no plug-in **** do Editor de Rich Text (RTE):

1. Substitua a caixa de diálogo do componente Widgets **** personalizados pela caixa de diálogo baseada no plug-in **** do Editor de Rich Text (RTE):
siga as etapas descritas para o [Exemplo 2: Caixa de diálogo de painel único](#example-single-panel-dialog)
1. Edite o componente.
1. Clique no último ícone à direita (aquele com quatro setas). Digite um caminho e clique em **OK**:
O caminho é exibido entre parênteses ([ ]).
1. Clique em **OK** para fechar o Editor de Rich Text.

A caixa de diálogo baseada no plug-in **** do Editor de Rich Text (RTE) é exibida da seguinte maneira:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este exemplo mostra apenas como implementar a parte do lado do cliente da lógica: os espaços reservados (*[texto]*) devem ser analisados explicitamente no lado do servidor (por exemplo, no componente JSP).

### Visão geral da árvore {#tree-overview}

O ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` objeto predefinido fornece representação de IU estruturada em árvore de dados estruturados em árvore. O componente Visão geral da árvore incluído no pacote **Usando widgets** ExtJS mostra como usar o `TreePanel` objeto para exibir uma árvore JCR abaixo de um determinado caminho. A janela em si pode ser encaixada/desencaixada. Neste exemplo, a lógica da janela é incorporada no componente jsp entre as tags &lt;script>&lt;/script>.

Para incluir o componente Visão geral **da** árvore na página de amostra:

1. Adicione o **4. Componente Visão geral** da árvore para a página de amostra da guia **Uso de widgets** ExtJS no **Sidekick**.
1. O componente exibe:
   * um título, com algum texto
   * um link **PROPRIEDADES** : clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente para ocultar as propriedades.
   * uma janela flutuante com uma representação em árvore do repositório, que pode ser expandida.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

O componente Visão geral da árvore:

* Está definido em:
   `/apps/extjstraining/components/treeoverview`

* Sua caixa de diálogo permite definir o tamanho da janela e ancorar/desancorar a janela (veja os detalhes abaixo).

O componente jsp:

* Recupera a largura, a altura e as propriedades ancoradas do repositório.
* Exibe algum texto sobre o formato de dados de visão geral da árvore.
* Incorpora a lógica da janela no componente jsp entre tags javascript.
* Está definido em:
   `apps/extjstraining/components/treeoverview/content.jsp`

O código javascript incorporado no componente jsp:

* Define um `tree` objeto tentando recuperar uma janela de árvore da página.
* Se a janela que exibe a árvore não existir, `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) será criado:
   * `treePanel` contém os dados usados para criar a janela.
   * Os dados são recuperados chamando o servlet registrado em:
      `/bin/wcm/siteadmin/tree.json`
* O `beforeload` ouvinte garante que o nó clicado seja carregado.
* O `root` objeto define o caminho `apps/extjstraining` como a raiz da árvore.
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`) é definido com base no predefinido `treePanel`, e é exibido com:
   `tree.show();`
* Se a janela já existir, ela será exibida com base nas propriedades de largura, altura e ancoragem recuperadas do repositório.

A caixa de diálogo do componente:

* Exibe 1 guia com 2 campos para definir o tamanho (largura e altura) da janela de visão geral da árvore e 1 campo para ancorar/desancorar a janela
* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget sizefield (tipo de nó = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e um widget de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) com 2 opções (true/false)
* É definido pelo nó de diálogo em:
   `/apps/extjstraining/components/treeoverview/dialog`
* É renderizado no formato json solicitando:
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* É exibido da seguinte forma:

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Visão geral da grade {#grid-overview}

Um Painel de grade representa dados em um formato tabular de linhas e colunas. É composto pelo seguinte:

* Loja : o modelo que contém os registros de dados (linhas).
* Modelo de coluna: a composição da coluna.
* Exibir : encapsula a interface do usuário.
* Modelo de seleção: o comportamento da seleção.

O componente Visão geral da grade incluído no pacote **Uso de widgets** ExtJS mostra como exibir dados em um formato tabular:

* O exemplo 1 usa dados estáticos.
* O exemplo 2 usa dados recuperados do repositório.

Para incluir o componente Visão geral da grade à página de amostra:

1. Adicione o **5. O componente Visão geral** da grade para a página de amostra da guia **Uso de widgets** ExtJS no **Sidekick**.
1. O componente exibe:
   * um título com algum texto
   * um link **PROPRIEDADES** : clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente para ocultar as propriedades.
   * uma janela flutuante contendo dados em formato tabular.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemplo 1: Grade padrão {#example-default-grid}

Em sua versão predefinida, o componente Visão geral **da** grade exibe uma janela com dados estáticos em um formato tabular. Neste exemplo, a lógica é incorporada no componente jsp de duas maneiras:

* a lógica genérica é definida entre as tags &lt;script>&lt;/script>
* a lógica específica está disponível em um arquivo .js separado e está vinculada ao jsp. Essa configuração permite alternar facilmente entre as duas lógicas (estáticas/dinâmicas) ao comentar as tags &lt;script> desejadas.

O componente Visão geral da grade:

* Está definido em:
   `/apps/extjstraining/components/gridoverview`
* Sua caixa de diálogo permite definir o tamanho da janela e ancorar/desancorar a janela.

O componente jsp:

* Recupera a largura, a altura e as propriedades ancoradas do repositório.
* Exibe algum texto como introdução ao formato de dados de visão geral da grade.
* Refere o código javascript que define o objeto GridPanel:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
   `defaultgrid.js` define alguns dados estáticos como uma base para o objeto GridPanel.
* Incorpora código javascript entre tags javascript que definem o objeto Window que usa o objeto GridPanel.
* Está definido em:
   `apps/extjstraining/components/gridoverview/content.jsp`

O código javascript incorporado no componente jsp:

* Define o `grid` objeto tentando recuperar o componente de janela da página:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Se `grid` não existir, um objeto [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) será definido chamando o `getGridPanel()` método (consulte abaixo). Esse método é definido em `defaultgrid.js`.
* `grid` é um ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` objeto, com base no GridPanel predefinido, e é exibido: `grid.show();`
* Se `grid` já existir, ele será exibido com base nas propriedades de largura, altura e ancoragem recuperadas do repositório.

O arquivo javascript ( `defaultgrid.js`) referenciado no componente jsp define o `getGridPanel()` método chamado pelo script incorporado no JSP e retorna um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto, com base em dados estáticos. A lógica é a seguinte:

* `myData` é uma matriz de dados estáticos formatados como uma tabela de 5 colunas e 4 linhas.
* `store` é um `CQ.Ext.data.Store` objeto que consome `myData`.
* `store` é carregado na memória:
   `store.load();`
* `gridPanel` é um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto que consome `store`:
   * as larguras das colunas são sempre redistribuídas:
      `forceFit: true`
   * somente uma linha por vez pode ser selecionada:
      `singleSelect:true`

#### Exemplo 2: Grade de pesquisa de referência {#example-reference-search-grid}

Quando você instala o pacote, o componente `content.jsp` de Visão geral **da** grade exibe uma grade baseada em dados estáticos. É possível modificar o componente para exibir uma grade com as seguintes características:

* Tem três colunas.
* É baseado em dados recuperados do repositório chamando um servlet.
* As células da última coluna podem ser editadas. O valor é persistente em uma `test` propriedade abaixo do nó definido pelo caminho exibido na primeira coluna.

Conforme explicado na seção anterior, o objeto window obtém seu ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto chamando o `getGridPanel()` método definido no `defaultgrid.js` arquivo em `/apps/extjstraining/components/gridoverview/defaultgrid.js`. O **componente **Visão geral da grade **fornece uma implementação diferente para o `getGridPanel()` método, definido no `referencesearch.js` arquivo em `/apps/extjstraining/components/gridoverview/referencesearch.js`. Ao alternar o arquivo .js mencionado no componente jsp, a grade será baseada nos dados recuperados do repositório.

Alterne o arquivo .js mencionado no componente jsp:

1. No **CRXDE Lite**, no `content.jsp` arquivo do componente, comente a linha que inclui o `defaultgrid.js` arquivo, para que ele tenha a seguinte aparência:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Remova o comentário da linha que inclui o `referencesearch.js` arquivo, para que ele tenha a seguinte aparência:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salve as alterações.
1. Atualize a página de amostra.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

O código javascript referenciado no componente jsp ( `referencesearch.js`) define o `getGridPanel()` método chamado a partir do componente jsp e retorna um ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto, com base em dados recuperados dinamicamente do repositório. A lógica em `referencesearch.js` define alguns dados dinâmicos como uma base para o GridPanel:

* `reader` é um ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`objeto que lê a resposta do servlet no formato json para 3 colunas.
* `cm` é um ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` objeto para 3 colunas.
As células da coluna &quot;Testar&quot; podem ser editadas conforme são definidas com um editor:
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* as colunas são classificáveis:
   `cm.defaultSortable = true;`
* `store` é um ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` objeto:
   * obtém os dados chamando o servlet registrado em &quot; `/bin/querybuilder.json`&quot; com alguns parâmetros usados para filtrar a consulta
   * é baseado em `reader`, previamente definido
   * a tabela é classificada de acordo com a coluna &#39;**jcr:path**&#39; em ordem crescente
* `gridPanel` é um ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` objeto que pode ser editado:
   * é baseado no modelo predefinido `store` e na coluna `cm`
   * somente uma linha por vez pode ser selecionada:
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * o `afteredit` ouvinte garante que após a edição de uma célula na coluna &quot;**Testar**&quot;:
      * a propriedade &#39; `test`&#39; do nó no caminho definido pela coluna &quot;**jcr:path**&quot; é definida no repositório com o valor da célula
      * se o POST for bem-sucedido, o valor será adicionado ao `store` objeto; caso contrário, será rejeitado
