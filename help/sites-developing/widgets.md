---
title: Uso e extensão de widgets (interface de usuário clássica)
description: A interface baseada na Web do Adobe Experience Manager usa AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG de conteúdo por autores diretamente na página da Web
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# Uso e extensão de widgets (interface de usuário clássica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Esta página descreve o uso de widgets na interface clássica do, que foi descontinuada no AEM 6.4.
>
>A Adobe recomenda usar a [interface do usuário habilitada para toque](/help/sites-developing/touch-ui-concepts.md) moderna, baseada na [interface do usuário do Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e na [interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

A interface baseada na Web do Adobe Experience Manager (AEM) usa o AJAX e outras tecnologias modernas de navegador para permitir a edição e a formatação WYSIWYG de conteúdo por autores diretamente na página da Web.

O AEM usa a biblioteca de widgets [ExtJS](https://www.sencha.com/), que fornece os elementos de interface de usuário altamente aprimorados que funcionam em todos os navegadores mais importantes e permitem a criação de experiências de interface de usuário de desktop.

Esses widgets estão incluídos no AEM e, além de serem usados pelo próprio AEM, podem ser usados por qualquer site criado com o uso do AEM.

Para obter uma referência completa de todos os widgets disponíveis no AEM, consulte a [documentação da API de widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ou a [lista de xtypes](/help/sites-developing/xtypes.md) existentes. Além disso, muitos exemplos mostrando como usar a estrutura ExtJS estão disponíveis no site [Sencha](https://examples.sencha.com/extjs/7.6.0/), o proprietário da estrutura.

Esta página fornece alguns insights sobre como usar e estender widgets. Primeiro, descreve como [incluir código do lado do cliente em uma página](#including-the-client-sided-code-in-a-page). Em seguida, descreve alguns componentes de amostra que foram criados para ilustrar algum uso e extensão básicos. Esses componentes estão disponíveis no **pacote Usando ExtJS Widgets** no **Compartilhamento de Pacotes**.

O pacote inclui exemplos de:

* [Caixas de diálogo básicas](#basic-dialogs) criadas com widgets prontos para uso.
* [Caixas de diálogo dinâmicas](#dynamic-dialogs) criadas com widgets prontos para uso e lógica personalizada do JavaScript.
* Caixas de diálogo baseadas em [widgets personalizados](#custom-widgets).
* Um [painel de árvore](#tree-overview) exibindo uma árvore JCR abaixo de um determinado caminho.
* Um [painel de grade](#grid-overview) exibindo dados em formato tabular.

>[!NOTE]
>
>A interface clássica do Adobe Experience Manager foi criada em [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusão do código do lado do cliente em uma página {#including-the-client-sided-code-in-a-page}

O JavaScript do lado do cliente e o código da folha de estilos devem ser colocados em uma biblioteca do cliente.

Para criar uma biblioteca do cliente:

1. Crie um nó abaixo de `/apps/<project>` com as seguintes propriedades:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;nome-da-categoria>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. Abaixo de `clientlib`, crie as pastas `css` e `js` (nt:folder).

1. Abaixo de `clientlib`, crie os arquivos `css.txt` e `js.txt` (nt:files). Esses arquivos .txt listam os arquivos incluídos na biblioteca.

1. Editar `js.txt`: deve começar com &#39; `#base=js`&#39; seguido da lista dos arquivos que são agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Editar `css.txt`: deve começar com &#39; `#base=css`&#39; seguido da lista dos arquivos que são agregados pelo serviço de biblioteca do cliente CQ, por exemplo:

   ```
   #base=css
    components.css
   ```

1. Abaixo da pasta `js`, coloque os arquivos JavaScript que pertencem à biblioteca.

1. Abaixo da pasta `css`, coloque os arquivos `.css` e os recursos usados pelos arquivos css (por exemplo, `my_icon.png`).

>[!NOTE]
>
>O manuseio das folhas de estilos descritas anteriormente é opcional.

Para incluir a biblioteca do cliente no componente página jsp:

* para incluir código JavaScript e folhas de estilos:
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
onde `<category-nameX>` é o nome da biblioteca do lado do cliente.

* para incluir apenas o código JavaScript:
  `<ui:includeClientLib js="<category-name>"/>`

Para obter mais detalhes, consulte a descrição do [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) tag.&lt;/ui:includeClientLib>

Às vezes, uma biblioteca do cliente só deve estar disponível no modo autor e deve ser excluída publicar modo. Ele pode ser alcançado da seguinte maneira:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Introdução com as amostras {#getting-started-with-the-samples}

Para seguir os tutoriais nesta página, instale o pacote **Usando Widgets ExtJS** em uma instância do AEM local e crie uma página de exemplo na qual os componentes estejam incluídos. Para fazer isso, faça o seguinte:

1. Na instância do AEM, baixe o pacote chamado **Usando ExtJS Widgets (v01)** do Compartilhamento de Pacotes e instale o pacote. Ele cria o projeto `extjstraining` abaixo de `/apps` no repositório.
1. Inclua a biblioteca do cliente que contém os scripts (js) e a folha de estilos (css) na tag head da jsp da página do Geometrixx. Você incluirá os componentes de exemplo em uma nova página da ramificação **Geometrixx**:
em **CRXDE Lite**, abra o arquivo `/apps/geometrixx/components/page/headlibs.jsp` e adicione a categoria `cq.extjstraining` à marca `<ui:includeClientLib>` existente da seguinte maneira:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Crie uma página na ramificação **Geometrixx** abaixo de `/content/geometrixx/en/products` e chame-a de **Usando Dispositivos ExtJS**.
1. Vá para o modo de design e adicione todos os componentes do grupo chamado **Usando Dispositivos ExtJS** ao design do Geometrixx
1. Volte para o modo de edição: os componentes do grupo **Uso de widgets ExtJS** estão disponíveis no Sidekick.

>[!NOTE]
>
>Os exemplos desta página são baseados no conteúdo de amostra do Geometrixx, que não é mais enviado com AEM, tendo sido substituído pelo We.Retail. Consulte a [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) para saber como baixar e instalar o Geometrixx.

### Caixas de diálogo básicas {#basic-dialogs}

As caixas de diálogo normalmente são usadas para editar conteúdo, mas também podem exibir informações. Uma maneira fácil de visualizar uma caixa de diálogo completa é acessar sua representação no formato json. Para fazer isso, aponte seu navegador para:

`https://localhost:4502/<path-to-dialog>.-1.json`

O primeiro componente do grupo **Usando Dispositivos ExtJS** no Sidekick é chamado **1. Noções básicas da caixa de diálogo** e inclui quatro caixas de diálogo básicas que são criadas com widgets prontos para uso e sem lógica personalizada do JavaScript. As caixas de diálogo estão armazenadas abaixo de `/apps/extjstraining/components/dialogbasics`. As caixas de diálogo básicas são:

* a caixa de diálogo completa ( nó `full`): ela exibe uma janela com três guias, cada uma com dois campos de texto.
* a caixa de diálogo Painel Único (nó `singlepanel`): ela exibe uma janela com uma guia que tem dois campos de texto.
* a caixa de diálogo Vários Painéis (nó `multipanel`): sua exibição é igual à caixa de diálogo Completa, mas é criada de forma diferente.
* a caixa de diálogo Design( nó `design`): ela exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto recolhível. A segunda guia tem um campo definido com quatro campos de texto e um campo recolhível definido com dois campos de texto.

Inclua o **1. Componente** de Noções básicas da caixa de diálogo na página de exemplo:

1. Adicione o **1. Componente** de Noções básicas da caixa de diálogo para a página de exemplo de **Uso de widgets ExtJS** na **Sidekick**.
1. O componente exibe um título, algum texto e um link **PROPRIEDADES**. Selecionar o link exibe as propriedades do parágrafo armazenadas no repositório. Selecione o link novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemplo 1: caixa de diálogo completa {#example-full-dialog}

A caixa de diálogo **Cheia** exibe uma janela com três guias, cada uma com dois campos de texto. É a caixa de diálogo padrão do componente **Noções básicas da caixa de diálogo**. Suas características são:

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

A caixa de diálogo **Painel Único** exibe uma janela com uma guia que tem dois campos de texto. Suas características são:

* Exibe uma guia (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* A guia tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* É definido pelo nó:
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Uma vantagem sobre a **Caixa de Diálogo Completa** é que é necessária menos configuração.
* Uso recomendado: para caixas de diálogo simples que exibem informações ou têm apenas alguns campos.

Para usar a caixa de diálogo Painel único:

1. Substitua a caixa de diálogo do componente **Noções básicas da caixa de diálogo** pela caixa de diálogo **Painel Único**:
   1. Em **CRXDE Lite**, exclua o nó: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Clique em **Salvar tudo** para salvar as alterações.
   1. Copiar o nó: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Cole o nó copiado abaixo: `/apps/extjstraining/components/dialogbasics`
   1. Selecione o nó: `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`e renomeie-o `dialog`.
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemplo 3: caixa de diálogo Vários painéis {#example-multi-panel-dialog}

A caixa de diálogo **Vários Painéis** tem a mesma exibição da caixa de diálogo **Completa**, mas é criada de forma diferente. Suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Exibe três guias (nó tipo = `cq:Panel`).
* Cada guia tem dois campos de texto (nó tipo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó:
  `/apps/extjstraining/components/dialogbasics/multipanel`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Uma vantagem sobre a **Caixa de Diálogo Completa** é que ela tem uma estrutura simplificada.
* Uso recomendado: para caixas de diálogo de várias guias.

Para usar a caixa de diálogo Vários painéis:

1. Substitua a caixa de diálogo do componente **Noções básicas da caixa de diálogo** pela caixa de diálogo **Vários painéis**:
siga as etapas descritas para o [Exemplo 2: Caixa de Diálogo de Painel Único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemplo 4: caixa de diálogo rica {#example-rich-dialog}

A caixa de diálogo **Rich** exibe uma janela com duas guias. A primeira guia tem um campo de texto, um menu suspenso e uma área de texto recolhível. A segunda guia tem um campo definido com quatro campos de texto e um campo recolhível definido com dois campos de texto. Suas características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe duas guias (tipo de nó = `cq:Panel`).
* A primeira guia tem um widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` com um ` [textfield](/help/sites-developing/xtypes.md#textfield)` e um widget ` [selection](/help/sites-developing/xtypes.md#selection)` com três opções, e um ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` recolhível com um widget ` [textarea](/help/sites-developing/xtypes.md#textarea)`.
* A segunda guia tem um widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` com quatro widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)`, e um `dialogfieldset` recolhível com dois widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)`.
* É definido pelo nó:
  `/apps/extjstraining/components/dialogbasics/rich`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Para usar a caixa de diálogo **Rich**:

1. Substitua a caixa de diálogo do componente **Noções básicas da caixa de diálogo** pela caixa de diálogo **Rich**:
siga as etapas descritas para o [Exemplo 2: Caixa de Diálogo de Painel Único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Caixas de diálogo dinâmicas {#dynamic-dialogs}

O segundo componente do grupo **Usando Dispositivos ExtJS** no Sidekick é chamado **2. Caixas de Diálogo Dinâmicas** e inclui três caixas de diálogo dinâmicas que são criadas com widgets prontos para uso e **com lógica personalizada de JavaScript**. As caixas de diálogo estão armazenadas abaixo de `/apps/extjstraining/components/dynamicdialogs`. As caixas de diálogo dinâmicas são:

* a caixa de diálogo Alternar guias (nó `switchtabs`): ela exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.
* a caixa de diálogo Arbitrária (nó `arbitrary`): exibe uma janela com uma guia. A guia tem um campo para soltar ou fazer upload de um ativo e um campo que exibe algumas informações sobre a página que o contém e sobre o ativo, se houver uma referência a ele.
* a caixa de diálogo Alternar campos (nó `togglefield`): ela exibe uma janela com uma guia. A guia tem uma caixa de seleção: quando marcada, um campo definido com dois campos de texto é exibido.

Para incluir o **2. Componente de Caixas de Diálogo Dinâmicas** na página de exemplo:

1. Adicione o **2. Caixas de diálogo dinâmicas** para a página de exemplo do **Usando Dispositivos ExtJS** guia no **Sidekick**.
1. O componente exibe um título, algum texto e um link **PROPRIEDADES**. Selecionar o link exibe as propriedades do parágrafo armazenadas no repositório. Selecione o link novamente para ocultar as propriedades.

O componente é exibido da seguinte maneira:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemplo 1: Caixa de diálogo Alternar guias {#example-switch-tabs-dialog}

A caixa de diálogo **Alternar Guias** exibe uma janela com duas guias. A primeira guia tem uma seleção de opção com três opções: quando uma opção é selecionada, uma guia relacionada à opção é exibida. A segunda guia tem dois campos de texto.

Suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe duas guias (tipo de nó = `cq:Panel`): uma guia de seleção, a segunda guia depende da seleção na primeira guia (três opções).
* Tem três guias opcionais (tipo de nó = `cq:Panel`), cada uma tem dois campos de texto (tipo de nó = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Somente uma guia opcional é exibida por vez.
* É definido pelo nó `switchtabs` em:
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* O nó da caixa de diálogo tem um ouvinte &quot; `beforeshow`&quot; que oculta todas as guias opcionais antes da exibição da caixa de diálogo:
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` obtém a `tabpanel` que contém o painel de seleção e os três painéis opcionais.
* O objeto `Ejst.x2` está definido no arquivo `exercises.js` em:
  `/apps/extjstraining/clientlib/js/exercises.js`
* No método `Ejst.x2.manageTabs()`, como o valor de `index` é -1, todas as guias opcionais ficam ocultas (ele vai de 1 a 3).
* A guia de seleção tem dois ouvintes: um que mostra a guia selecionada quando a caixa de diálogo é carregada (evento &quot;`loadcontent`&quot;) e outro que mostra a guia selecionada quando a seleção é alterada (evento &quot;`selectionchanged`&quot;):
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Para o método `Ejst.x2.showTab()`,
  `field.findParentByType('tabpanel')` obtém a `tabpanel` que contém todas as guias ( `field` representa o widget de seleção)
  `field.getValue()` obtém o valor da seleção, por exemplo, tab2
  `Ejst.x2.manageTabs()` exibe a guia selecionada.
* Cada guia opcional tem um ouvinte que oculta a guia no evento &quot; `render`&quot;:
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Para o método `Ejst.x2.hideTab()`,
  `tabPanel` é a `tabpanel` que contém todas as guias
  `index` é o índice da guia opcional
  `tabPanel.hideTabStripItem(index)` o oculta o guia

Ela é exibida da seguinte maneira:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemplo 2: caixa de diálogo arbitrária {#example-arbitrary-dialog}

Geralmente, uma caixa de diálogo exibe o conteúdo do componente subjacente. A caixa de diálogo descrita aqui, chamada caixa de diálogo **Arbitrária**, extrai o conteúdo de um componente diferente.

A caixa de diálogo **Arbitrária** exibe uma janela com uma guia. A guia tem dois campos: um para soltar ou fazer upload de um ativo e outro que exibe algumas informações sobre a página que o contém e sobre o ativo, se algum tiver sido referenciado.

Suas principais características são:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um widget `tabpanel` (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) com um painel (tipo de nó = `cq:Panel`)
* O painel tem um widget smartfile (tipo de nó = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e um widget ownerdraw (tipo de nó = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* É definido pelo nó `arbitrary` em:
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* O widget `ownerdraw` tem um ouvinte &quot; `loadcontent`&quot; que mostra informações sobre a página que contém o componente. Ou seja, o ativo referenciado pelo widget smartfile quando o conteúdo é carregado:
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` está definido com o objeto `ownerdraw`
  `path` está definido com o caminho de conteúdo do componente (por exemplo, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* O objeto `Ejst.x2` está definido no arquivo `exercises.js` em:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Para o método `Ejst.x2.showInfo()`,
  `pagePath` é o caminho da página que contém o componente;
  `pageInfo` representa as propriedades da página em formato json;
  `reference` é o caminho do ativo referenciado;
  `metadata` representa os metadados do ativo em formato json;
  `ownerdraw.getEl().update(html);` exibe o html criado no diálogo

Para usar a caixa de diálogo **Arbitrária**:

1. Substituir caixa de diálogo do **componente diálogo** dinâmico com a **caixa de diálogo Arbitrária** :
seguir as etapas descritas para o [exemplo 2: caixa de diálogo de painel único](#example-single-panel-dialog)
1. Editar o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Exemplo 3: caixa de diálogo Alternar campos {#example-toggle-fields-dialog}

A caixa de diálogo **Alternar Campos** exibe uma janela com uma guia. O guia tem uma caixa de seleção: quando é marcado, um campo definido com dois campos de texto é exibido.

Suas principais características são:

* É definido por uma nó (nó tipo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um `tabpanel` widget (nó tipo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) com um painel (nó tipo = `cq:Panel`).
* O painel possui um widget de seleção/caixa de seleção (nó tipo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e um widget dialogfieldset dobrável (nó tipo = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) que é oculto por padrão, com dois widgets de campo de texto (nó tipo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* É definido pelo nó `togglefields` em:
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

A lógica é implementada por meio de ouvintes de eventos e do código JavaScript, da seguinte maneira:

* a guia seleção tem dois ouvintes: um que mostra o dialogfieldset quando o conteúdo é carregado (evento &quot;`loadcontent`&quot;) e outro que mostra o dialogfieldset quando a seleção é alterada (evento &quot;`selectionchanged`&quot;):
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* O objeto `Ejst.x2` está definido no arquivo `exercises.js` em:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Para o método `Ejst.x2.toggleFieldSet()`,
  `box` é o objeto de seleção;
  `panel` é o painel que contém os widgets selection e dialogfieldset;
  `fieldSet` é o objeto dialogfieldset;
  `show` é o valor da seleção (verdadeiro ou falso);
baseado em &#39; `show`&#39;, o dialogfieldset é exibido ou não

Para usar a caixa de diálogo **Alternar Campos**, faça o seguinte:

1. Substitua a caixa de diálogo do componente **Caixa de Diálogo Dinâmica** pela caixa de diálogo **Alternar Campos**:
siga as etapas descritas para o [Exemplo 2: Caixa de Diálogo de Painel Único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personalizados {#custom-widgets}

Os widgets prontos para uso enviados com AEM devem abranger a maioria dos casos de uso. No entanto, às vezes pode ser necessário criar um widget personalizado para atender a um requisito específico do projeto. Widgets personalizados podem ser criados estendendo os existentes. Para ajudar você a começar com essa personalização, o pacote **`Using ExtJS Widgets`** inclui três caixas de diálogo que usam três widgets personalizados diferentes:

* a caixa de diálogo Vários Campos (nó `multifield`) exibe uma janela com uma guia. A guia tem um widget de vários campos personalizado que tem dois campos: um menu suspenso com duas opções e um campo de texto. Como se baseia no widget `multifield` pronto para uso (que tem apenas um campo de texto), ele tem todos os recursos do widget `multifield`.
* a caixa de diálogo Procurar árvore (nó `treebrowse`) exibe uma janela com uma guia contendo um widget de procura de caminho: quando você clica na seta, uma janela é aberta, na qual você pode procurar uma hierarquia e selecionar um item. O caminho do item é adicionado ao campo de caminho e é mantido quando a caixa de diálogo é fechada.
* uma caixa de diálogo baseada em Plug-in do Editor de Rich Text (nó `rteplugin`) que adiciona um botão personalizado ao Editor de Rich Text para inserir texto personalizado no texto principal. Ele consiste em um widget (RTE) do `richtext` e em um recurso personalizado que é adicionado por meio do mecanismo de plug-in RTE.

Os widgets personalizados e o plug-in são incluídos no componente chamado **3. Widgets personalizados** do **pacote Usar widgets** ExtJS. Para incluir esse componente na página de amostra:

1. Adicione o **3. Componente de Widgets personalizados** para o página de amostra dos **Widgets** ExtJS guia no **Sidekick**.
1. O componente exibe um título, um texto e, ao clicar na **link PROPRIEDADES** , as propriedades do parágrafo armazenadas no repositório. Clicar novamente oculta as propriedades.
O componente é exibido da seguinte maneira:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemplo 1: Widget de vários campos personalizado {#example-custom-multifield-widget}

A caixa de diálogo **Multicampo Personalizado** baseada em widget exibe uma janela com uma guia. A guia tem um widget multicampo personalizado que, ao contrário do widget padrão que tem um campo, tem dois campos: um menu suspenso com duas opções e um campo de texto.

A caixa de diálogo baseada no widget **Multicampo Personalizado**:

* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um widget `tabpanel` (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget `multifield` (tipo de nó = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* O widget `multifield` tem um fieldconfig (tipo de nó = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) que é baseado no xtype personalizado &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; é uma opção de configuração do objeto ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)`.
   * &#39; `optionsProvider`&#39; é uma configuração do widget `ejstcustom`. Está definido com o método `Ejst.x3.provideOptions`, que está definido em `exercises.js` às:
     `/apps/extjstraining/clientlib/js/exercises.js`
e retorna duas opções.
* É definido pelo nó `multifield` em:
  `/apps/extjstraining/components/customwidgets/multifield`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

O widget personalizado `multifield` (xtype = `ejstcustom`):

* É um objeto JavaScript chamado `Ejst.CustomWidget`
* Está definido no arquivo JavaScript `CustomWidget.js` em:
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende o widget ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)`.
* Tem três campos: `hiddenField` (Textfield), `allowField` (ComboBox) e `otherField` (Textfield)
* Substitui `CQ.Ext.Component#initComponent` para adicionar os três campos:
   * `allowField` é um objeto [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) do tipo &#39;select&#39;. optionsProvider é uma configuração do objeto Selection que é instanciada com a configuração optionsProvider do CustomWidget definido na caixa de diálogo
   * `otherField` é um objeto [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)
* Substitui os métodos `setValue`e `getValue``getRawValue` o [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) para definir e recuperar o valor de CustomWidget com o formato:
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* Registra-se como &#39; `ejstcustom`&#39; xtype:
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

A caixa de diálogo **Multicampo Personalizado** baseada em widget é exibida da seguinte forma:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemplo 2: Dispositivo personalizado `Treebrowse` {#example-custom-treebrowse-widget}

A caixa de diálogo com base em widgets personalizados **`Treebrowse`** exibe uma janela com uma guia contendo um widget de navegação por caminho personalizado. Quando você seleciona a seta, abre-se uma janela na qual você pode navegar em uma hierarquia e selecionar um item. O caminho do item é então adicionado ao campo de caminho e é persistente quando a caixa de diálogo é fechada.

A caixa de diálogo personalizada `treebrowse` :

* É definido por uma nó (nó tipo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Exibe um widget `tabpanel` (tipo de nó = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contendo um painel (tipo de nó = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget personalizado (tipo de nó = `cq:Widget`, xtype = `ejstbrowse`)
* É definido pelo nó `treebrowse` em:
  `/apps/extjstraining/components/customwidgets/treebrowse`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

Widget de navegação de árvore personalizado (xtype = `ejstbrowse`):

* É um objeto JavaScript chamado `Ejst.CustomWidget`
* Está definido no arquivo JavaScript `CustomBrowseField.js` em:
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Estende ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Define uma janela de navegação chamada `browseWindow`.
* Substitui ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` para mostrar a janela de navegação quando a seta é clicada.
* Define um objeto [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel):
   * Ele obtém seus dados chamando o servlet registrado em `/bin/wcm/siteadmin/tree.json`.
   * Sua raiz é &quot; `apps/extjstraining`&quot;.
* Define um objeto `window` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Com base no painel predefinido.
   * Tem um botão **OK** que define o valor do caminho selecionado e oculta o painel.
* A janela está ancorada abaixo do campo **Caminho**.
* O caminho selecionado é passado do campo de procura para a janela no evento `show`.
* Registra-se como &#39; `ejstbrowse`&#39; xtype:
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Para usar a caixa de diálogo **Procurar Árvore Personalizada** baseada em widget:

1. Substitua a caixa de diálogo do componente **Widgets personalizados** pela caixa de diálogo **Treebrowse personalizado**:
siga as etapas descritas para o [Exemplo 2: Caixa de Diálogo de Painel Único](#example-single-panel-dialog)
1. Edite o componente: a caixa de diálogo é exibida da seguinte maneira:

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemplo 3: plug-in de editor de rich text (RTE) {#example-rich-text-editor-rte-plug-in}

A **caixa de diálogo com base na editor editor Rich Text (RTE) é uma caixa de diálogo baseada em** Editor Rich Text que possui uma botão personalizada para inserir algum texto personalizado dentro de colchetes. O texto personalizado pode ser analisado por alguma lógica lado do servidor (não implementada neste exemplo), por exemplo, para adicionar algum texto que seja definido em um determinado caminho:

A **caixa de diálogo baseada no plug-in** RTE:

* É definido pelo nó replugin em:
  `/apps/extjstraining/components/customwidgets/rteplugin`
* É renderizado no formato json, solicitando:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* O nó `rtePlugins` tem um nó filho `inserttext` (tipo de nó = `nt:unstructured`) que é nomeado após o plug-in. Ele tem uma propriedade chamada `features` que define quais dos recursos de plug-in estão disponíveis para o RTE.

O plug-in RTE:

* É um objeto JavaScript chamado `Ejst.InsertTextPlugin`
* Está definido no arquivo JavaScript `InsertTextPlugin.js` em:
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende o objeto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`.
* Os métodos a seguir definem o objeto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` e são substituídos no plug-in de implementação:
   * `getFeatures()` retorna uma matriz de todos os recursos que o plug-in disponibiliza.
   * `initializeUI()` adiciona o novo botão à barra de ferramentas do RTE.
   * `notifyPluginConfig()` exibe o título e o texto quando o botão é focalizado.
   * `execute()` é chamado quando o botão é clicado e executa a ação do plug-in: exibe uma janela que é usada para definir o texto a ser incluído.
* `insertText()` insere um texto usando o objeto de diálogo correspondente `Ejst.InsertTextPlugin.Dialog` (veja depois).
* `executeInsertText()` é chamado pelo método `apply()` da caixa de diálogo, que é acionado ao clicar no botão **OK**.
* Registra-se como &#39; `inserttext`&#39; plug-in:
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* o objeto `Ejst.InsertTextPlugin.Dialog` define a caixa de diálogo que é aberta quando o botão de plug-in é clicado. A caixa de diálogo consiste em um painel, um formulário, um campo de texto e dois botões (**OK** e **Cancelar**).

Para usar a caixa de diálogo baseada no **Plug-in do Editor de Rich Text (RTE)**:

1. Substitua a caixa de diálogo do componente **Widgets personalizados** pela caixa de diálogo baseada no **Plug-in do Editor de Rich Text (RTE)**:
siga as etapas descritas para o [Exemplo 2: Caixa de Diálogo de Painel Único](#example-single-panel-dialog)
1. Edite o componente.
1. Clique no último ícone à direita (aquele com quatro setas). Insira um caminho e clique em **OK**:
O caminho é exibido entre colchetes ([ ]).
1. Clique em **OK** para fechar o Editor de Rich Text.

A **caixa de diálogo com base em plug-in** da editor Rich Text (RTE) é exibida da seguinte maneira:

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Este exemplo mostra apenas como implementar a parte da lógica do lado do cliente: os espaços reservados (*[texto]*) devem ser analisados explicitamente no lado do servidor (por exemplo, no componente JSP).

### Visão geral da árvore {#tree-overview}

O objeto ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` pronto para uso fornece representação da interface estruturada em árvore de dados estruturados em árvore. O componente Visão geral da árvore incluído no **pacote Usar widgets** ExtJS mostra como usar o `TreePanel` objeto para exibir uma árvore JCR abaixo de um determinado caminho. A janela em si pode ser ancorada/não ancorada. Neste exemplo, a lógica de janela está incorporada no jsp de componentes entre &lt;script> tags.

Para incluir o **componente Visão geral** da árvore ao página de amostra:

1. Adicione o **4. Componente de Visão geral** da árvore para o página de amostra usando widgets **** ExtJS guia no **Sidekick**.
1. O componente é exibido:
   * um título, com algum texto
   * um link **PROPERTIES**: clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente para ocultar as propriedades.
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

* Define um objeto `tree` tentando recuperar uma janela de árvore da página.
* Se a janela que exibe a árvore não existir, `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) será criado:
   * `treePanel` contém os dados usados para criar a janela.
   * Os dados são recuperados chamando o servlet registrado em:
     `/bin/wcm/siteadmin/tree.json`
* O ouvinte `beforeload` verifica se o nó selecionado está carregado.
* O objeto `root` define o caminho `apps/extjstraining` como a raiz da árvore.
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) está definido com base no `treePanel` predefinido e é exibido com:
  `tree.show();`
* Se a janela existir, ela será exibida com base na largura, altura e propriedades encaixadas recuperadas do repositório.

A caixa de diálogo do componente:

* Exibe uma guia com dois campos para definir o tamanho (largura e altura) da janela de visão geral da árvore e um campo para encaixar/desencaixar a janela
* É definido por um nó (tipo de nó = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* O painel tem um widget sizefield (tipo de nó = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e um widget de seleção (tipo de nó = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`) com duas opções (true/false)
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

O componente de Visão geral de grade incluído no pacote **Using ExtJS Widgets** mostra como exibir dados em formato tabular:

* O exemplo 1 usa dados estáticos.
* O exemplo 2 usa dados recuperados do repositório.

Para incluir o componente Visão geral da grade na página de exemplo:

1. Adicione o **5. Visão geral de grade** para a página de exemplo de **Usando widgets ExtJS** na **Sidekick**.
1. O componente exibe:
   * um título com algum texto
   * um link **PROPERTIES**: clique em para exibir as propriedades do parágrafo armazenado no repositório. Clique novamente para ocultar as propriedades.
   * uma janela flutuante contendo dados em formato tabular.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemplo 1: Grade Padrão {#example-default-grid}

Na versão inicial, o **componente Visão geral** de grade exibe uma janela com dados estáticos em um formato tabular. Neste exemplo, a lógica é incorporada no jsp do componente de duas maneiras:

* a lógica genérica é definida entre &lt;script> tags
* a lógica específica está disponível em um arquivo .js separado e está vinculada no jsp. Essa configuração permite alternar entre as duas lógicas (estática/dinâmica) ao comentar as &lt;script> tags desejadas.

O componente de Visão geral da grade:

* É definido em:
  `/apps/extjstraining/components/gridoverview`
* A caixa de diálogo permite definir o tamanho da janela e ancorar ou cancelar a âncora da janela.

O jsp do componente:

* Recupera a largura, a altura e as propriedades ancoradas do repositório.
* Exibe texto como introdução ao formato de dados de visão geral da grade.
* Faz referência ao código JavaScript que define o objeto GridPanel:
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` define alguns dados estáticos como base para o objeto GridPanel.
* Incorpora o código JavaScript entre tags JavaScript que define o objeto Window consumindo o objeto GridPanel.
* É definido em:
  `apps/extjstraining/components/gridoverview/content.jsp`

O código JavaScript incorporado no componente jsp:

* Define o objeto `grid` tentando recuperar o componente de janela da página:
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Se `grid` não existir, um objeto [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) será definido ao chamar o método `getGridPanel()` (veja abaixo). Este método é definido em `defaultgrid.js`.
* `grid` é um objeto ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`, com base no GridPanel predefinido, e é exibido: `grid.show();`
* Se `grid` existir, ele será exibido com base na largura, altura e propriedades encaixadas recuperadas do repositório.

O arquivo JavaScript ( `defaultgrid.js`) referenciado no componente jsp define o método `getGridPanel()` que é chamado pelo script incorporado no JSP e retorna um objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, com base em dados estáticos. A lógica é a seguinte:

* `myData` é uma matriz de dados estáticos formatados como uma tabela de cinco colunas e quatro linhas.
* `store` é um objeto `CQ.Ext.data.Store` que consome `myData`.
* `store` está carregado na memória:
  `store.load();`
* `gridPanel` é um objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` que consome `store`:
   * as larguras das colunas são sempre reproporcionadas:
     `forceFit: true`
   * somente uma linha por vez pode ser selecionada:
     `singleSelect:true`

#### Exemplo 2: Grade de Pesquisa de Referência {#example-reference-search-grid}

Quando você instala o pacote, a `content.jsp` do componente **Visão Geral da Grade** exibe uma grade que é baseada em dados estáticos. É possível modificar o componente para exibir uma grade com as seguintes características:

* Tem três colunas.
* É baseado em dados recuperados do repositório ao chamar um servlet.
* As células da última coluna podem ser editadas. O valor é mantido em uma propriedade `test` abaixo do nó definido pelo caminho exibido na primeira coluna.

Como explicado na seção anterior, o objeto da janela obtém seu objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` chamando o método `getGridPanel()` definido no arquivo `defaultgrid.js` em `/apps/extjstraining/components/gridoverview/defaultgrid.js`. O componente **Visão geral da grade **fornece uma implementação diferente para o método `getGridPanel()`, definido no arquivo `referencesearch.js` em `/apps/extjstraining/components/gridoverview/referencesearch.js`. Ao alternar o arquivo .js referenciado no componente jsp, a grade é baseada nos dados recuperados do repositório.

Troque o arquivo .js referenciado no componente jsp:

1. Em **CRXDE Lite**, no arquivo `content.jsp` do componente, comente a linha que inclui o arquivo `defaultgrid.js` para que ele tenha a seguinte aparência:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Remova o comentário da linha que inclui o arquivo `referencesearch.js` para que ele tenha a seguinte aparência:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salve as alterações.
1. Atualize a página de exemplo.

O componente é exibido da seguinte maneira:

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

O código JavaScript referenciado no componente jsp ( `referencesearch.js`) define o método `getGridPanel()` chamado do componente jsp e retorna um objeto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, com base nos dados recuperados dinamicamente do repositório. A lógica em `referencesearch.js` define alguns dados dinâmicos como base para o GridPanel:

* `reader` é um objeto ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` que lê a resposta do servlet no formato json para três colunas.
* `cm` é um objeto ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` para três colunas.
As células da coluna &quot;Test&quot; podem ser editadas conforme são definidas com um editor:
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* as colunas são classificáveis:
  `cm.defaultSortable = true;`
* `store` é um objeto ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)`:
   * ele obtém seus dados chamando o servlet registrado em &quot;`/bin/querybuilder.json`&quot; com alguns parâmetros usados para filtrar a consulta
   * é baseado em `reader`, definido anteriormente
   * a tabela é classificada de acordo com a coluna &#39;**jcr:path**&#39; em ordem crescente
* `gridPanel` é um objeto ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` que pode ser editado:
   * baseia-se no `store` predefinido e no modelo de coluna `cm`
   * somente uma linha por vez pode ser selecionada:
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * o ouvinte `afteredit` verifica se, após uma célula na coluna &quot;**Test**&quot;, ela foi editada:
      * a propriedade &#39; `test`&#39; do nó no caminho definido pela coluna &quot;**jcr:path**&quot; está definida no repositório com o valor da célula
      * se o POST for bem-sucedido, o valor será adicionado ao objeto `store`; caso contrário, será rejeitado
