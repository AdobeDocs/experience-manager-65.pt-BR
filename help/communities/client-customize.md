---
title: Personalização do lado do cliente
description: Personalização do comportamento ou aparência do lado do cliente no AEM Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Personalização do lado do cliente  {#client-side-customization}

| **[⇐ Feature Essentials](essentials.md)** | **[Personalização no lado do servidor ^](server-customize.md)** |
|---|---|
|   | **[Helpers do Handlebars do SCF ^](handlebars-helpers.md)** |

Há várias abordagens para personalizar a aparência e/ou o comportamento de um componente do AEM Communities no lado do cliente.

Duas abordagens principais são a sobreposição ou a extensão de um componente.

[Sobreposição](#overlays) um componente altera o componente padrão e afeta todas as referências ao componente.

[A extensão](#extensions) de um componente, com nome exclusivo, limita o escopo das alterações. O termo &quot;estender&quot; é usado alternadamente com &quot;substituir&quot;.

## Sobreposições {#overlays}

Sobrepor um componente é um método para fazer modificações em um componente padrão e afetar todas as instâncias que usam o padrão.

A sobreposição é realizada modificando uma cópia do componente padrão no diretório /**apps**, em vez de modificar o componente original no diretório /**libs**. O componente é construído com um caminho relativo idêntico, exceto que &quot;libs&quot; é substituído por &quot;apps&quot;.

O diretório /apps é o primeiro local pesquisado para resolver solicitações e, se não for encontrado, a versão padrão no diretório/libs será usada.

O componente padrão no diretório /libs nunca deve ser modificado, pois os patches e upgrades futuros podem alterar o diretório /libs de qualquer maneira necessária enquanto mantêm as interfaces públicas.

Isso é diferente de [estender](#extensions) um componente padrão em que o desejo é fazer modificações para um uso específico, criando um caminho exclusivo para o componente e confiando na referência ao componente padrão original no diretório /libs como o tipo de super recurso.

Para obter um exemplo rápido de sobreposição do componente de comentários, tente o [tutorial do Componente de Sobreposição de Comentários](overlay-comments.md).

## Extensões  {#extensions}

Estender (substituir) um componente é um método de fazer modificações para um uso específico sem afetar todas as instâncias que usam o padrão. O componente estendido é nomeado exclusivamente na pasta /apps e faz referência ao componente padrão na pasta /libs, portanto, o design e o comportamento padrão de um componente não são modificados.

Isso é diferente de [sobrepor](#overlays) o componente padrão, onde a natureza do Sling resolve referências relativas à pasta apps/ antes de pesquisar na pasta libs/, portanto, o design ou comportamento de um componente é modificado globalmente.

Para obter um exemplo rápido de extensão do componente de comentários, tente o [tutorial Estender componente de comentários](extend-comments.md).

## Vínculo do JavaScript {#javascript-binding}

O script HBS do componente deve ser vinculado aos objetos, modelos e visualizações do JavaScript que implementam esse recurso.

O valor do atributo `data-scf-component` pode ser o padrão, como **`social/tally/components/hbs/rating`**, ou um componente estendido (personalizado) para funcionalidade personalizada, como **weretail/components/hbs/rating**.

Para vincular um componente, todo o script do componente deve ser delimitado em um elemento &lt;div> com os seguintes atributos:

* `data-component-id`=&quot;`{{id}}`&quot;

  resolve para a propriedade id do contexto

* `data-scf-component`=&quot;*&lt;resourceType>*

Por exemplo, de `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriedades personalizadas {#custom-properties}

Ao estender ou sobrepor um componente, é possível adicionar propriedades a uma caixa de diálogo modificada.

Todas as propriedades definidas em um componente/recurso podem ser acessadas fazendo referência às chaves de propriedade no modelo handlebars:

`{{properties.<property_name>}}`

## Aplicação de capa a CSS {#skinning-css}

A personalização de componentes para corresponder ao tema geral do site pode ser realizada alterando cores, fontes, imagens, botões, links, espaçamento e até mesmo o posicionamento em uma determinada extensão.

A atribuição de capa pode ser obtida substituindo seletivamente os estilos da estrutura ou escrevendo folhas de estilos totalmente novas. Os componentes SCF definem classes CSS namespace, modulares e semânticas que afetam os vários elementos que compõem um componente.

Para aplicar capa a um componente:

1. Identifique os elementos que deseja alterar (por exemplo, área do compositor, botões da barra de ferramentas, fonte da mensagem e assim por diante).
1. Identifique a classe/regras CSS que afetam esses elementos.
1. Crie um arquivo de folha de estilos (.css).
1. Inclua a folha de estilos em uma pasta da biblioteca do cliente ([clientlibs](#clientlibs-for-scf)) para o seu site e verifique se ela está incluída em seus modelos e páginas com [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redefina as classes e regras CSS identificadas (#2) na folha de estilos e adicione estilos.

Os estilos personalizados agora substituirão os estilos de estrutura padrão, e o componente será renderizado com a nova capa.

>[!CAUTION]
>
>Qualquer nome de classe CSS que tenha o prefixo `scf-js` tem um uso específico no código JavaScript. Essas classes afetam o estado de um componente (por exemplo, alternar de oculto para visível) e não devem ser substituídas nem removidas.
>
>Embora as classes `scf-js` não afetem estilos, os nomes de classe podem ser usados em folhas de estilos com o aviso de que, como elas controlam os estados dos elementos, pode haver efeitos colaterais.

## Extensão do JavaScript {#extending-javascript}

Para estender uma implementação do JavaScript de componentes, é necessário:

1. Crie um componente para seu aplicativo com um jcr:resourceSuperType definido com o valor do jcr:resourceType do componente estendido, por exemplo, social/forum/components/hbs/forum.
1. Examine o JavaScript do componente SCF padrão para determinar quais métodos precisam ser registrados usando SCF.registerComponent().
1. Copie o JavaScript do componente estendido ou inicie do zero.
1. Estenda o método.
1. Use SCF.registerComponent() para registrar todos os métodos com os padrões ou com os objetos e exibições personalizados.

### forum.js: Exemplo de extensão do Forum - HBS  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## Tags de script {#script-tags}

As tags de script são uma parte inerente da estrutura do lado do cliente. Eles são a cola que ajuda a vincular a marcação gerada no lado do servidor aos modelos e visualizações no lado do cliente.

As tags de script nos scripts SCF não devem ser removidas ao sobrepor ou substituir componentes. As tags de script SCF criadas automaticamente para inserção de JSON no HTML são identificadas com o atributo `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

O uso de [bibliotecas do lado do cliente](../../help/sites-developing/clientlibs.md) (clientlibs) fornece um meio de organizar e otimizar a JavaScript e o CSS usados para renderizar conteúdo no cliente.

As clientlibs do SCF seguem um padrão de nomenclatura muito específico para duas variantes, que variam somente pela presença de &quot;autor&quot; no nome da categoria:

| Variante do Clientlib | Padrão da propriedade Categorias |
|--- |--- |
| clientlib completo | cq.social.hbs.&lt;nome do componente> |
| author clientlib | cq.social.author.hbs.&lt;nome do componente> |

### Clientlibs completos {#complete-clientlibs}

As bibliotecas de clientes completas (não de autor) incluem dependências e são convenientes para inclusão com ui:includeClientLib.

Essas versões são encontradas em:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por exemplo:

* Nó da pasta do cliente: `/etc/clientlibs/social/hbs/forum`
* Propriedade de categorias: `cq.social.hbs.forum`

O [guia de Componentes da Comunidade](components-guide.md) lista as clientlibs completas necessárias para cada componente do SCF.

[Clientlibs para componentes das comunidades](clientlibs.md) descreve como adicionar clientlibs a uma página.

### Clientlibs do autor {#author-clientlibs}

As clientlibs da versão do autor são reduzidas ao JavaScript mínimo necessário para implementar o componente.

Essas clientlibs nunca devem ser incluídas diretamente, mas em vez disso estão disponíveis para serem incorporadas a outras clientlibs, que são criadas manualmente para um site.

Essas versões são encontradas na pasta SCF libs:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por exemplo:

* Nó da pasta do cliente: `/libs/social/forum/hbs/forum/clientlibs`
* Propriedade de categorias: `cq.social.author.hbs.forum`

Observação: embora as clientlibs do autor nunca incorporem outras bibliotecas, elas listam suas dependências. Quando incorporadas em outras bibliotecas, as dependências não são automaticamente extraídas e também devem ser incorporadas.

As clientlibs do autor necessárias podem ser identificadas inserindo-se &quot;author&quot; nas clientlibs listadas para cada componente do SCF no [guia de Componentes da Comunidade](components-guide.md).

### Considerações sobre uso {#usage-considerations}

Cada site é diferente na forma como eles gerenciam as bibliotecas de clientes. Vários fatores incluem:

* Velocidade geral: talvez o desejo seja que o site seja responsivo, mas é aceitável que a primeira página seja um pouco lenta de carregar. Se muitas das páginas usarem a mesma JavaScript, as várias JavaScript poderão ser incorporadas a uma clientlib e referenciadas a partir da primeira página a ser carregada. A JavaScript nesse download único permanece em cache, minimizando a quantidade de dados para baixar para páginas subsequentes.
* Breve tempo para a primeira página: talvez o desejo seja que a primeira página seja carregada rapidamente. Nesse caso, o JavaScript está em vários arquivos pequenos para serem referenciados somente onde necessário.
* Um equilíbrio entre o primeiro carregamento da página e os downloads subsequentes.

| **[⇐ Feature Essentials](essentials.md)** | **[Personalização no lado do servidor ^](server-customize.md)** |
|---|---|
|   | **[Helpers do Handlebars do SCF ^](handlebars-helpers.md)** |
