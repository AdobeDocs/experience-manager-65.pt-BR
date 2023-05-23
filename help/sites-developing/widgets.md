---
title: Uso e extensão de widgets (interface de usuário clássica)
description: A interface baseada na Web do Adobe Experience Manager usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG de conteúdo por autores diretamente na página da Web
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '4926'
ht-degree: 0%

---

# Uso e extensão de widgets (interface de usuário clássica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página descreve o uso de widgets na interface clássica do, que foi descontinuada no AEM 6.4.
>
>A Adobe recomenda usar o moderno, [interface habilitada para toque](/help/sites-developing/touch-ui-concepts.md) baseado em [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [Interface do Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

A interface baseada na Web do Adobe Experience Manager (AEM) usa o AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG de conteúdo por autores diretamente na página da Web.

O AEM usa o [ExtJS](https://www.sencha.com/) biblioteca de widgets, que fornece os elementos de interface de usuário altamente sofisticados que funcionam em todos os navegadores mais importantes e permitem a criação de experiências de interface de usuário de desktop.

Esses widgets estão incluídos no AEM e, além de serem usados pelo próprio AEM, podem ser usados por qualquer site criado com o uso do AEM.

Para obter uma referência completa de todos os widgets disponíveis no AEM, consulte [documentação da API do widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ou o [lista de xtypes existentes](/help/sites-developing/xtypes.md). Além disso, muitos exemplos mostrando como usar a estrutura ExtJS estão disponíveis no [Sencha](https://examples.sencha.com/extjs/7.6.0/) local, o proprietário da estrutura.

Esta página fornece alguns insights sobre como usar e estender widgets. Primeiro, descreve como [incluir código do lado do cliente em uma página](#including-the-client-sided-code-in-a-page). Em seguida, descreve alguns componentes de amostra que foram criados para ilustrar algum uso e extensão básicos. Esses componentes estão disponíveis no **Utilização de widgets ExtJS** pacote ativado **Compartilhamento de pacotes**.

O pacote inclui exemplos de:

* [Caixas de diálogo básicas](#basic-dialogs) criado com widgets prontos para uso.
* [Caixas de diálogo dinâmicas](#dynamic-dialogs) criado com widgets prontos para uso e lógica JavaScript personalizada.
* Caixas de diálogo baseadas em [widgets personalizados](#custom-widgets).
* A [painel em árvore](#tree-overview) exibindo uma árvore JCR abaixo de um determinado caminho.
* A [painel de grade](#grid-overview) exibição de dados em formato tabular.

>[!NOTE]
>
>A interface clássica do Adobe Experience Manager é criada em [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusão do código do lado do cliente em uma página {#including-the-client-sided-code-in-a-page}

O JavaScript do lado do cliente e o código da folha de estilos devem ser colocados em uma biblioteca do cliente.

Para criar uma biblioteca do cliente:

1. Criar um nó abaixo `/apps/<project>` com as seguintes propriedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:bloqueável]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Abaixo `clientlib` criar o `css` e `js` pastas (nt:folder).

1. Abaixo `clientlib` criar o `css.txt` e `js.txt` arquivos (nt:files). Esses arquivos .txt listam os arquivos incluídos na biblioteca.

1. Editar `js.txt`: deve começar com &#39; `#base=js`&quot; seguido pela lista dos arquivos que são agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: deve começar com &#39; `#base=css`&quot; seguido pela lista dos arquivos que são agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=css
    components.css
   ```

1. Abaixo do `js` , coloque os arquivos JavaScript que pertencem à biblioteca.

1. Abaixo do `css` pasta, coloque o `.css` e os recursos usados pelos arquivos css (por exemplo, `my_icon.png`).

>[!NOTE]
>
>O manuseio das folhas de estilos descritas anteriormente é opcional.

Para incluir a biblioteca do cliente no componente página jsp:

* para incluir código JavaScript e folhas de estilos:
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
em que 
`<category-nameX>` é o nome da biblioteca do lado do cliente.

* para incluir apenas o código JavaScript:
   `<ui:includeClientLib js="<category-name>"/>`

Para obter mais detalhes, consulte a descrição da [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) tag.

Às vezes, uma biblioteca do cliente deve estar disponível somente no modo de autor e deve ser excluída no modo de publicação. Isso pode ser feito da seguinte maneira:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introdução às amostras {#getting-started-with-the-samples}

Para seguir os tutoriais nesta página, instale o pacote **Utilização de widgets ExtJS** em uma instância de AEM local e crie uma página de exemplo na qual os componentes sejam incluídos. Para fazer isso, faça o seguinte:

1. Na instância do AEM, baixe o pacote chamado **Utilização de widgets ExtJS (v01)** em Compartilhamento de pacotes e instale o pacote. Ele cria o projeto `extjstraining` abaixo `/apps` no repositório.
1. Inclua a biblioteca do cliente que contém os scripts (js) e a folha de estilos (css) na tag head da jsp da página do Geometrixx. Você incluirá os componentes de amostra em uma nova página do **Geometrixx** ramificação: em **CRXDE Lite** abra o arquivo `/apps/geometrixx/components/page/headlibs.jsp` e adicione o `cq.extjstraining` categoria ao existente `<ui:includeClientLib>` da seguinte forma:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Crie uma página no **Geometrixx** ramificação abaixo `/content/geometrixx/en/products` e chame-o **Utilização de widgets ExtJS**.
1. Vá para o modo de design e adicione todos os componentes do grupo chamados **Utilização de widgets ExtJS** ao design do Geometrixx
1. Voltar para o modo de edição: os componentes do grupo **Utilização de widgets ExtJS** estão disponíveis no Sidekick.

>[!NOTE]
>
>Os exemplos desta página são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com AEM, tendo sido substituído pelo We.Retail. Consulte a [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

### Caixas de diálogo básicas {#basic-dialogs}

As caixas de diálogo normalmente são usadas para editar conteúdo, mas também podem exibir informações. Uma maneira fácil de visualizar uma caixa de diálogo completa é acessar sua representação no formato json. Para fazer isso, aponte seu navegador para:

`https://localhost:4502/<path-to-dialog>.-1.json`

O primeiro componente do **Utilização de widgets ExtJS** O grupo no Sidekick é chamado **1. Noções básicas da caixa de diálogo** O e o incluem quatro caixas de diálogo básicas que são criadas com widgets prontos para uso e sem lógica JavaScript personalizada. Os diálogos são armazenados abaixo `/apps/extjstraining/components/dialogbasics`. As caixas de diálogo básicas são:

* a caixa de diálogo Completa ( `full` node): exibe uma janela com três guias, cada uma com dois campos de texto.
* a caixa de diálogo Painel único ( `singlepanel` node): exibe uma janela com uma guia que tem dois campos de texto.
* a caixa de diálogo Vários painéis ( `multipanel` node): sua exibição é a mesma da caixa de diálogo Completa, mas é criada de forma diferente.
* a caixa de diálogo Design( `design` node): exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto recolhível. A segunda guia tem um campo definido com quatro campos de texto e um campo recolhível definido com dois campos de texto.

Inclua o **1. Noções básicas da caixa de diálogo** componente na página de exemplo:

1. Adicione o **1. Noções básicas da caixa de diálogo** componente para a página de exemplo da **Utilização de widgets ExtJS** na guia **Sidekick**.
1. O componente exibe um título, algum texto e um **PROPRIEDADES** link. Selecionar o link exibe as propriedades do parágrafo armazenadas no repositório. Selecione o link novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemplo 1: caixa de diálogo completa {#example-full-dialog}

A variável **Completo** exibe uma janela com três abas, cada uma com dois campos de texto. É a caixa de diálogo padrão do **Noções básicas da caixa de diálogo** componente. Suas características são:

* É definido por um nó: tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Exibe três guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/full`
* É renderizado no formato JSON, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

A caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Exemplo 2: caixa de diálogo Painel único {#example-single-panel-dialog}

A variável **Painel único** exibe uma janela com uma guia que tem dois campos de texto. Suas características são:

* Exibe uma guia (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* A guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Uma vantagem sobre a **Caixa de diálogo completa** é que menos configuração é necessária.
* Uso recomendado: para caixas de diálogo simples que exibem informações ou têm apenas alguns campos.

Para usar a caixa de diálogo Painel único:

1. Substituir a caixa de diálogo do **Noções básicas da caixa de diálogo** componente com o **Painel único** diálogo:
   1. Entrada **CRXDE Lite**, exclua o nó: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Clique em **Salvar tudo** para salvar as alterações.
   1. Copie o nó: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Cole o nó copiado abaixo: `/apps/extjstraining/components/dialogbasics`
   1. Selecione o nó: `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`e renomeá-la `dialog`.
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemplo 3: caixa de diálogo Vários painéis {#example-multi-panel-dialog}

A variável **Vários painéis** tem a mesma exibição que a caixa de diálogo **Completo** caixa de diálogo, mas é criada de forma diferente. Suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Exibe três guias (tipo de nó = `cq:Panel`).
* Cada guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/multipanel`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Uma vantagem sobre a **Caixa de diálogo completa** é que ele tem uma estrutura simplificada.
* Uso recomendado: para caixas de diálogo de várias guias.

Para usar a caixa de diálogo Vários painéis:

1. Substituir a caixa de diálogo do **Noções básicas da caixa de diálogo** componente com o **Vários painéis** caixa de diálogo: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemplo 4: caixa de diálogo rica {#example-rich-dialog}

A variável **Rico** exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto recolhível. A segunda guia tem um campo definido com quatro campos de texto e um campo recolhível definido com dois campos de texto. Suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe duas guias (tipo de nó = `cq:Panel`).
* A primeira guia tem um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com um ` [textfield](/help/sites-developing/xtypes.md#textfield)` e uma ` [selection](/help/sites-developing/xtypes.md#selection)` widget com três opções e um recolhível ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` com um ` [textarea](/help/sites-developing/xtypes.md#textarea)` widget.
* A segunda guia tem uma ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget com quatro ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets, e um `dialogfieldset` com dois ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets.
* É definido pelo nó:
   `/apps/extjstraining/components/dialogbasics/rich`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar o **Rico** diálogo:

1. Substituir a caixa de diálogo do **Noções básicas da caixa de diálogo** componente com o **Rico** caixa de diálogo: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Caixas de diálogo dinâmicas {#dynamic-dialogs}

O segundo componente do **Utilização de widgets ExtJS** O grupo no Sidekick é chamado **2. Caixas de diálogo dinâmicas** e inclui três caixas de diálogo dinâmicas que são criadas com widgets prontos para uso e **com lógica personalizada do JavaScript**. Os diálogos são armazenados abaixo `/apps/extjstraining/components/dynamicdialogs`. As caixas de diálogo dinâmicas são:

* a caixa de diálogo Alternar guias ( `switchtabs` node): exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.
* a caixa de diálogo Arbitrário ( `arbitrary` node): exibe uma janela com uma guia. A guia tem um campo para soltar ou fazer upload de um ativo e um campo que exibe algumas informações sobre a página que o contém e sobre o ativo, se houver uma referência a ele.
* a caixa de diálogo Alternar campos ( `togglefield` node): exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando marcada, um campo definido com dois campos de texto é exibido.

Para incluir a variável **2. Caixas de diálogo dinâmicas** componente na página de exemplo:

1. Adicione o **2. Caixas de diálogo dinâmicas** componente para a página de exemplo da **Utilização de widgets ExtJS** na guia **Sidekick**.
1. O componente exibe um título, algum texto e um **PROPRIEDADES** link. Selecionar o link exibe as propriedades do parágrafo armazenadas no repositório. Selecione o link novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemplo 1: Caixa de diálogo Alternar guias {#example-switch-tabs-dialog}

A variável **Alternar Guias** exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.

Suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe duas guias (tipo de nó = `cq:Panel`): uma guia de seleção, a segunda guia depende da seleção na primeira guia (três opções).
* Tem três guias opcionais (tipo de nó = `cq:Panel`), cada um tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Somente uma guia opcional é exibida por vez.
* É definido pelo `switchtabs` nó em:
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* O nó da caixa de diálogo tem um &quot; `beforeshow`&quot;ouvinte que oculta todas as guias opcionais antes que a caixa de diálogo seja exibida:
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` obtém o `tabpanel` que contém o painel de seleção e os três painéis opcionais.
* A variável `Ejst.x2` o objeto é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* No `Ejst.x2.manageTabs()` como o valor de `index` é -1, todas as guias opcionais ficam ocultas (vai de 1 a 3).
* A guia de seleção tem dois ouvintes: um que mostra a guia selecionada quando a caixa de diálogo é carregada (&quot; `loadcontent`&quot;) e uma que mostre a guia selecionada quando a seleção for alterada (&quot; `selectionchanged`&quot; evento):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Para o `Ejst.x2.showTab()` método,
   `field.findParentByType('tabpanel')` obtém o `tabpanel` que contém todas as guias ( `field` representa o widget de seleção)
   `field.getValue()` obtém o valor da seleção, por exemplo, tab2
   `Ejst.x2.manageTabs()` exibe a guia selecionada.
* Cada guia opcional tem um ouvinte que oculta a guia em &quot; `render`Evento &quot;:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Para o `Ejst.x2.hideTab()` método,
   `tabPanel` é o `tabpanel` que contém todas as guias
   `index` é o índice da guia opcional
   `tabPanel.hideTabStripItem(index)` oculta a guia

Ela é exibida da seguinte maneira:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemplo 2: caixa de diálogo arbitrária {#example-arbitrary-dialog}

Geralmente, uma caixa de diálogo exibe o conteúdo do componente subjacente. O diálogo descrito aqui, chamado **Arbitrário** , extrai o conteúdo de um componente diferente.

A variável **Arbitrário** exibe uma janela com uma guia. A guia tem dois campos: um para soltar ou fazer upload de um ativo e outro que exibe algumas informações sobre a página que o contém e sobre o ativo, se algum tiver sido referenciado.

Suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um `tabpanel` widget (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) com um painel (tipo de nó = `cq:Panel`)
* O painel tem um widget smartfile (tipo de nó = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e um widget ownerdraw (tipo de nó = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* É definido pelo `arbitrary` nó em:
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* A variável `ownerdraw` O widget tem um &quot; `loadcontent`&quot;que mostra informações sobre a página que contém o componente. Ou seja, o ativo referenciado pelo widget smartfile quando o conteúdo é carregado:
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` é definido com o `ownerdraw` objeto
   `path` é definido com o caminho do conteúdo do componente (por exemplo, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* A variável `Ejst.x2` o objeto é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Para o `Ejst.x2.showInfo()` método,
   `pagePath` é o caminho da página que contém o componente;
   `pageInfo` representa as propriedades da página no formato json;
   `reference` é o caminho do ativo referenciado;
   `metadata` representa os metadados do ativo no formato json;
   `ownerdraw.getEl().update(html);` exibe o html criado no diálogo

Para usar o **Arbitrário** diálogo:

1. Substituir a caixa de diálogo do **Caixa de diálogo dinâmica** componente com o **Arbitrário** caixa de diálogo: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Example 3: Toggle Fields Dialog {#example-toggle-fields-dialog}

A variável **Alternar campos** exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando marcada, um campo definido com dois campos de texto é exibido.

Suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um `tabpanel` widget (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) com um painel (tipo de nó = `cq:Panel`).
* O painel tem um widget seleção/caixa de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e um widget dialogfieldset recolhível (tipo de nó = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que fica oculto por padrão, com dois widgets de campo de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo `togglefields` nó em:
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* a guia de seleção tem dois ouvintes: um que mostra o dialogfieldset quando o conteúdo é carregado (&quot; `loadcontent`&quot; event) e um que mostre o dialogfieldset quando a seleção for alterada (&quot; `selectionchanged`&quot; evento):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* A variável `Ejst.x2` o objeto é definido na variável `exercises.js` arquivo em:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Para o `Ejst.x2.toggleFieldSet()` método,
   `box` é o objeto de seleção;
   `panel` é o painel que contém os widgets selection e dialogfieldset;
   `fieldSet` é o objeto dialogfieldset;
   `show` é o valor da seleção (verdadeiro ou falso); com base em &#39; `show`&#39; o dialogfieldset é exibido ou não

Para usar o **Alternar campos** , faça o seguinte:

1. Substituir a caixa de diálogo do **Caixa de diálogo dinâmica** componente com o **Alternar campos** caixa de diálogo: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Os widgets prontos para uso enviados com AEM devem abranger a maioria dos casos de uso. No entanto, às vezes pode ser necessário criar um widget personalizado para atender a um requisito específico do projeto. Widgets personalizados podem ser criados estendendo os existentes. Para ajudar você a começar com essa personalização, a variável **`Using ExtJS Widgets`** O pacote inclui três caixas de diálogo que usam três widgets personalizados diferentes:

* a caixa de diálogo Vários campos ( `multifield` ) exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que tem dois campos: um menu suspenso com duas opções e um campo de texto. Como se baseia nos recursos `multifield` (que tem apenas um campo de texto), ele tem todos os recursos do `multifield` widget.
* a caixa de diálogo Procurar na árvore ( `treebrowse` node) exibe uma janela com uma guia contendo um widget de navegação por caminho: quando você clica na seta, uma janela é aberta, na qual você pode navegar por uma hierarquia e selecionar um item. O caminho do item é adicionado ao campo de caminho e é mantido quando a caixa de diálogo é fechada.
* uma caixa de diálogo baseada em Plug-in do Editor de Rich Text ( `rteplugin` nó) que adiciona um botão personalizado ao Editor de Rich Text para inserir texto personalizado no texto principal. Consiste em uma `richtext` (RTE) e de um recurso personalizado adicionado por meio do mecanismo de plug-in RTE.

Os widgets personalizados e o plug-in são incluídos no componente chamado **3. Widgets personalizados** do **Utilização de widgets ExtJS** pacote. Para incluir esse componente na página de exemplo:

1. Adicione o **3. Widgets personalizados** componente para a página de exemplo da **Utilização de widgets ExtJS** na guia **Sidekick**.
1. O componente exibe um título, algum texto e, ao clicar no ícone **PROPRIEDADES** link, as propriedades do parágrafo armazenadas no repositório. Clicar novamente oculta as propriedades.
O componente é exibido da seguinte maneira:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemplo 1: Widget de vários campos personalizado {#example-custom-multifield-widget}

A variável **Vários campos personalizados** a caixa de diálogo baseada em widget exibe uma janela com uma guia. A guia tem um widget multicampo personalizado que, ao contrário do widget padrão que tem um campo, tem dois campos: um menu suspenso com duas opções e um campo de texto.

A variável **Vários campos personalizados** caixa de diálogo baseada em widget:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um `tabpanel` widget (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem uma `multifield` widget (tipo de nó = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* A variável `multifield` o widget tem um fieldconfig (tipo de nó = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) que é baseado no xtype personalizado &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; é uma opção de configuração de ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)` objeto.
   * &#39; `optionsProvider`&#39; é uma configuração de `ejstcustom` widget. É definido com a variável `Ejst.x3.provideOptions` método definido em `exercises.js` em:
      `/apps/extjstraining/clientlib/js/exercises.js`
e retorna duas opções.
* É definido pelo `multifield` nó em:
   `/apps/extjstraining/components/customwidgets/multifield`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

O personalizado `multifield` widget (xtype = `ejstcustom`):

* É um objeto JavaScript chamado `Ejst.CustomWidget`
* É definido na variável `CustomWidget.js` Arquivo JavaScript em:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende o ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` widget.
* Tem três campos: `hiddenField` (Textfield), `allowField` (ComboBox) e `otherField` (Campo de texto)
* Substituições `CQ.Ext.Component#initComponent` para adicionar os três campos:
   * `allowField` é um [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) objeto do tipo &#39;select&#39;. optionsProvider é uma configuração do objeto Selection que é instanciada com a configuração optionsProvider do CustomWidget definido na caixa de diálogo
   * `otherField` é um [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField) objeto
* Substitui os métodos `setValue`, `getValue`, e `getRawValue` de [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) para definir e recuperar o valor de CustomWidget com o formato:
   `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* Registra a si mesmo como &#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

****

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemplo 2: personalizado `Treebrowse` Widget {#example-custom-treebrowse-widget}

O personalizado **`Treebrowse`** a caixa de diálogo baseada em widget exibe uma janela com uma guia contendo um widget de navegação de caminho personalizado. Quando você seleciona a seta, é aberta uma janela na qual você pode procurar uma hierarquia e selecionar um item. O caminho do item é adicionado ao campo de caminho e é mantido quando a caixa de diálogo é fechada.

O personalizado `treebrowse` diálogo:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um `tabpanel` widget (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget personalizado (tipo de nó = `cq:Widget`, xtype = `ejstbrowse`)
* É definido pelo `treebrowse` nó em:
   `/apps/extjstraining/components/customwidgets/treebrowse`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

O widget personalizado de navegação na árvore (xtype = `ejstbrowse`):

* É um objeto JavaScript chamado `Ejst.CustomWidget`
* É definido na variável `CustomBrowseField.js` Arquivo JavaScript em:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Estende ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define uma janela de navegação chamada `browseWindow`.
* Substituições ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar a janela de navegação quando a seta é clicada.
* Define um [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) objeto:
   * Ele obtém seus dados chamando o servlet registrado em `/bin/wcm/siteadmin/tree.json`.
   * Sua raiz é &quot; `apps/extjstraining`&quot;.
* Define um `window` objeto ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Com base no painel predefinido.
   * Tem um **OK** botão que define o valor do caminho selecionado e oculta o painel.
* A janela está ancorada abaixo do **Caminho** campo.
* O caminho selecionado é passado do campo de procura para a janela em `show` evento.
* Registra a si mesmo como &#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar o **Treebrowse Personalizado** caixa de diálogo baseada em widget:

1. Substituir a caixa de diálogo do **Widgets personalizados** componente com o **Treebrowse Personalizado** caixa de diálogo: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemplo 3: Plug-in do Editor de Rich Text (RTE) {#example-rich-text-editor-rte-plug-in}

A variável **Plug-in do Editor de Rich Text (RTE)** caixa de diálogo baseada é uma caixa de diálogo baseada no Editor de Rich Text que tem um botão personalizado para inserir texto personalizado dentro de colchetes. O texto personalizado pode ser analisado por alguma lógica do lado do servidor (não implementada neste exemplo), por exemplo, para adicionar texto definido no caminho determinado:

A variável **Plug-in RTE** caixa de diálogo baseada em:

* É definido pelo nó replugin em:
   `/apps/extjstraining/components/customwidgets/rteplugin`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* A variável `rtePlugins` o nó tem um nó filho `inserttext` (tipo de nó = `nt:unstructured`) que tem o nome do plug-in. Ele tem uma propriedade chamada `features` que define quais dos recursos de plug-in estão disponíveis para o RTE.

O plug-in RTE:

* É um objeto JavaScript chamado `Ejst.InsertTextPlugin`
* É definido na variável `InsertTextPlugin.js` Arquivo JavaScript em:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende o ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` objeto.
* Os métodos a seguir definem o ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` e são substituídos no plug-in de implementação:
   * `getFeatures()` retorna uma matriz de todos os recursos que o plug-in disponibiliza.
   * `initializeUI()` adiciona o novo botão à barra de ferramentas do RTE.
   * `notifyPluginConfig()` exibe o título e o texto quando o botão é focalizado.
   * `execute()` é chamado quando o botão é clicado e executa a ação do plug-in: exibe uma janela usada para definir o texto a ser incluído.
* `insertText()` insere um texto usando o objeto de diálogo correspondente `Ejst.InsertTextPlugin.Dialog` (veja depois).
* `executeInsertText()` é chamado pelo `apply()` método da caixa de diálogo, que é acionado quando o **OK** é clicado.
* Registra a si mesmo como &#39; `inserttext`Plugin &#39;:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* o `Ejst.InsertTextPlugin.Dialog` O objeto define a caixa de diálogo que é aberta quando o botão de plug-in é clicado. O diálogo consiste em um painel, um formulário, um campo de texto e dois botões (**OK** e **Cancelar**).

Para usar o **Plug-in do Editor de Rich Text (RTE)** caixa de diálogo baseada em:

1. Substituir a caixa de diálogo do **Widgets personalizados** componente com o **Plug-in do Editor de Rich Text (RTE)** caixa de diálogo baseada em: siga as etapas descritas para o [Exemplo 2: caixa de diálogo Painel único](#example-single-panel-dialog)
1. Edite o componente.
1. Clique no último ícone à direita (aquele com quatro setas). Insira um caminho e clique em **OK**: O caminho é exibido entre colchetes ([ ]).
1. Clique em **OK** então você fecha o Editor de Rich Text.

A variável **Plug-in do Editor de Rich Text (RTE)** é exibida da seguinte maneira:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este exemplo mostra apenas como implementar a parte do lado do cliente da lógica: os espaços reservados (*[texto]*) devem ser analisadas explicitamente no lado do servidor (por exemplo, no componente JSP).

### Visão geral da árvore {#tree-overview}

O pacote pronto para uso ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` O objeto do fornece representação de dados estruturados em árvore na interface do usuário. O componente Visão geral da árvore incluído na **Utilização de widgets ExtJS** O pacote de mostra como usar o `TreePanel` para exibir uma árvore JCR abaixo de um determinado caminho. A janela em si pode ser encaixada/desencaixada. Neste exemplo, a lógica da janela é incorporada ao componente jsp entre &lt;script>&lt;/script> específicos.

Para incluir a variável **Visão geral da árvore** componente para a página de exemplo:

1. Adicione o **4. Visão geral da árvore** componente para a página de exemplo da **Utilização de widgets ExtJS** na guia **Sidekick**.
1. O componente exibe:
   * um título, com algum texto
   * a **PROPRIEDADES** link: clique em para exibir as propriedades do parágrafo armazenadas no repositório. Clique novamente para ocultar as propriedades.
   * uma janela flutuante com uma representação em árvore do repositório que pode ser expandida.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

O componente de Visão geral da árvore:

* É definido em:
   `/apps/extjstraining/components/treeoverview`

* A caixa de diálogo permite definir o tamanho da janela e encaixar ou desencaixar a janela (consulte os detalhes abaixo).

O componente jsp:

* Recupera a largura, a altura e as propriedades encaixadas do repositório.
* Exibe algum texto sobre o formato de dados da visão geral em árvore.
* Incorpora a lógica da janela na jsp do componente entre tags JavaScript.
* É definido em:
   `apps/extjstraining/components/treeoverview/content.jsp`

O código JavaScript incorporado no componente jsp:

* Define um `tree` tentando recuperar uma janela de árvore da página.
* Se a janela que exibe a árvore não existir, `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) é criada:
   * `treePanel` contém os dados usados para criar a janela.
   * Os dados são recuperados chamando o servlet registrado em:
      `/bin/wcm/siteadmin/tree.json`
* A variável `beforeload` o listener verifica se o nó selecionado está carregado.
* A variável `root` objeto define o caminho `apps/extjstraining` como a raiz da árvore.
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) é definido com base no padrão `treePanel`, e é exibido com:
   `tree.show();`
* Se a janela existir, ela será exibida com base na largura, altura e propriedades encaixadas recuperadas do repositório.

A caixa de diálogo do componente:

* Exibe uma guia com dois campos para definir o tamanho (largura e altura) da janela de visão geral da árvore e um campo para encaixar/desencaixar a janela
* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget sizefield (tipo de nó = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e um widget de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) com duas opções (true/false)
* É definido pelo nó da caixa de diálogo em:
   `/apps/extjstraining/components/treeoverview/dialog`
* É renderizado no formato json, solicitando:
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* É exibido da seguinte forma:

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Visão geral da grade {#grid-overview}

Um Painel de grade representa dados em um formato tabular de linhas e colunas. Ele é composto pelo seguinte:

* Armazenamento : o modelo que contém os registros de dados (linhas).
* Modelo da coluna : a composição da coluna.
* Exibição : encapsula a interface do usuário.
* Modelo de seleção : o comportamento da seleção.

O componente de Visão geral da grade incluído na **Utilização de widgets ExtJS** O pacote de mostra como exibir dados em formato tabular:

* O exemplo 1 usa dados estáticos.
* O exemplo 2 usa dados recuperados do repositório.

Para incluir o componente Visão geral da grade na página de exemplo:

1. Adicione o **5. Visão geral da grade** componente para a página de exemplo da **Utilização de widgets ExtJS** na guia **Sidekick**.
1. O componente exibe:
   * um título com algum texto
   * a **PROPRIEDADES** link: clique em para exibir as propriedades do parágrafo armazenadas no repositório. Clique novamente para ocultar as propriedades.
   * uma janela flutuante contendo dados em formato tabular.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemplo 1: Grade Padrão {#example-default-grid}

Em sua versão pronta para uso, a variável **Visão geral da grade** O componente exibe uma janela com dados estáticos em formato de tabela. Neste exemplo, a lógica é incorporada ao componente jsp de duas maneiras:

* a lógica genérica é definida entre &lt;script>&lt;/script> tags
* a lógica específica está disponível em um arquivo .js separado e está vinculada no jsp. This setup lets you switch between the two logic (static/dynamic) by commenting the desired &lt;script> tags.

O componente de Visão geral da grade:

* É definido em:
   `/apps/extjstraining/components/gridoverview`
* A caixa de diálogo permite definir o tamanho da janela e encaixar ou desencaixar a janela.

O componente jsp:

* Recupera a largura, a altura e as propriedades encaixadas do repositório.
* Exibe algum texto como introdução ao formato de dados da visão geral da grade.
* Faz referência ao código JavaScript que define o objeto GridPanel:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` define alguns dados estáticos como uma base para o objeto GridPanel.
* Incorpora o código JavaScript entre tags JavaScript que define o objeto Window consumindo o objeto GridPanel.
* É definido em:
   `apps/extjstraining/components/gridoverview/content.jsp`

O código JavaScript incorporado no componente jsp:

* Define o `grid` tentando recuperar o componente de janela da página:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Se `grid` não existir, uma [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) objeto ( `gridPanel`) é definido ao chamar o `getGridPanel()` (veja abaixo). Este método é definido em `defaultgrid.js`.
* `grid` é um ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` com base no GridPanel predefinido, e é exibido: `grid.show();`
* Se `grid` existir, será exibido com base na largura, altura e propriedades encaixadas recuperadas do repositório.

O arquivo JavaScript ( `defaultgrid.js`) referenciada no componente jsp define o `getGridPanel()` método chamado pelo script incorporado no JSP e retorna um ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto, com base em dados estáticos. A lógica é a seguinte:

* `myData` é uma matriz de dados estáticos formatados como uma tabela de cinco colunas e quatro linhas.
* `store` é um `CQ.Ext.data.Store` objeto que consome `myData`.
* `store` é carregado na memória:
   `store.load();`
* `gridPanel` é um ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto que consome `store`:
   * as larguras das colunas são sempre reproporcionadas:
      `forceFit: true`
   * somente uma linha por vez pode ser selecionada:
      `singleSelect:true`

#### Exemplo 2: Grade de Pesquisa de Referência {#example-reference-search-grid}

Ao instalar o pacote, a variável `content.jsp` do **Visão geral da grade** componente exibe uma grade que é baseada em dados estáticos. É possível modificar o componente para exibir uma grade com as seguintes características:

* Tem três colunas.
* É baseado em dados recuperados do repositório ao chamar um servlet.
* As células da última coluna podem ser editadas. O valor é mantido em um `test` abaixo do nó definido pelo caminho exibido na primeira coluna.

Como explicado na seção anterior, o objeto de janela recebe ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` ao chamar o `getGridPanel()` método definido na variável `defaultgrid.js` arquivo em `/apps/extjstraining/components/gridoverview/defaultgrid.js`. O componente **Visão geral da grade** fornece uma implementação diferente para o `getGridPanel()` , definido na `referencesearch.js` arquivo em `/apps/extjstraining/components/gridoverview/referencesearch.js`. Ao alternar o arquivo .js referenciado no componente jsp, a grade é baseada nos dados recuperados do repositório.

Troque o arquivo .js referenciado no componente jsp:

1. Entrada **CRXDE Lite**, no `content.jsp` do componente, comente a linha que inclui a variável `defaultgrid.js` para que tenha a seguinte aparência:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Remova o comentário da linha que inclui o `referencesearch.js` para que tenha a seguinte aparência:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salve as alterações.
1. Atualize a página de exemplo.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

O código JavaScript referenciado no componente jsp ( `referencesearch.js`) define o `getGridPanel()` chamado do componente jsp e retorna um ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objeto, com base nos dados recuperados dinamicamente do repositório. A lógica em `referencesearch.js` define alguns dados dinâmicos como uma base para o GridPanel:

* `reader` é um ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`objeto que lê a resposta do servlet no formato json para três colunas.
* `cm` é um ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` para três colunas.
As células da coluna &quot;Test&quot; podem ser editadas conforme são definidas com um editor:
   `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* as colunas são classificáveis:
   `cm.defaultSortable = true;`
* `store` é um ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` objeto:
   * ele obtém os dados chamando o servlet registrado em &quot; `/bin/querybuilder.json`&quot; com alguns parâmetros usados para filtrar a query
   * se baseia em `reader`, definido com antecedência
   * a tabela é classificada de acordo com a variável **jcr:path** Coluna &#39; em ordem crescente
* `gridPanel` é um ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` objeto que pode ser editado:
   * baseia-se na variável predefinida `store` e no modelo de coluna `cm`
   * somente uma linha por vez pode ser selecionada:
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * o `afteredit` o ouvinte garante que, após uma célula na variável &quot;**Teste** A coluna &quot; foi editada:
      * a propriedade &#39; `test`&#39; do nó no caminho definido pelo &quot;**jcr:path**&quot;A coluna é definida no repositório com o valor da célula
      * se o POST for bem-sucedido, o valor será adicionado à variável `store` objeto, caso contrário, será rejeitado
