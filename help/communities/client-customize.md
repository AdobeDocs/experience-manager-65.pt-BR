---
title: Personalização do lado do cliente
seo-title: Client-side Customization
description: Personalização de comportamento ou aparência no lado do cliente no AEM Communities
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Personalização do lado do cliente  {#client-side-customization}

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do servidor](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers †](handlebars-helpers.md)** |

Para personalizar a aparência e/ou o comportamento de um componente do AEM Communities no lado do cliente, há várias abordagens.

Duas abordagens principais são sobrepor ou estender um componente.

[Sobreposição](#overlays) um componente altera o componente padrão e afeta todas as referências ao componente.

[Extensão](#extensions) um componente, sendo nomeado exclusivamente, limita o escopo das alterações. O termo &quot;estender&quot; é utilizado alternadamente com &quot;sobrepor&quot;.

## Sobreposições {#overlays}

Sobrescrever um componente é um método para fazer modificações em um componente padrão e afetar todas as instâncias que usam o padrão.

A sobreposição é realizada modificando uma cópia do componente padrão no /**aplicativos** , em vez de modificar o componente original no /**libs** diretório. O componente é construído com um caminho relativo idêntico, exceto que &#39;libs&#39; é substituído por &#39;apps&#39;.

O diretório /apps é o primeiro local pesquisado para resolver solicitações e, se não for encontrado, a versão padrão localizada no diretório /libs será usada.

O componente padrão no diretório /libs nunca deve ser modificado, pois os patches e atualizações futuros são livres para alterar o diretório /libs de qualquer maneira necessária, mantendo as interfaces públicas.

Isso é diferente de [extensão](#extensions) um componente padrão no qual o desejo é fazer modificações para um uso específico, criando um caminho exclusivo para o componente e confiando em fazer referência ao componente padrão original no diretório /libs como o tipo de superrecurso.

Para obter um exemplo rápido de sobreposição do componente de comentários, tente a variável [Tutorial do componente Comentários da sobreposição](overlay-comments.md).

## Extensões  {#extensions}

Estender (substituir) um componente é um método para fazer modificações para um uso específico sem afetar todas as instâncias que usam o padrão. O componente estendido é nomeado exclusivamente na pasta /apps e faz referência ao componente padrão na pasta /libs, portanto, o design e o comportamento padrão de um componente não são modificados.

Isso é diferente de [sobreposição](#overlays) o componente padrão, no qual a natureza do Sling resolve referências relativas para os aplicativos/pastas antes de pesquisar nas libs/pasta, portanto, o design ou comportamento de um componente é modificado globalmente.

Para obter um exemplo rápido de como estender o componente comentários, tente o [Tutorial do componente Estender comentários](extend-comments.md).

## Vínculo Javascript {#javascript-binding}

O script HBS do componente deve ser vinculado aos objetos, modelos e visualizações do JavaScript que implementam esse recurso.

O valor da variável `data-scf-component` pode ser o padrão, como **`social/tally/components/hbs/rating`** ou um componente estendido (personalizado) para funcionalidade personalizada, como **rede/componentes/hbs/classificação**.

Para vincular um componente, o script de componente inteiro deve ser incluído em um &lt;div> elemento com os seguintes atributos:

* `data-component-id`=&quot;{{id}}&quot;

   resolve para a propriedade id do contexto

* `data-scf-component`=&quot;*&lt;resourcetype>*

Por exemplo, de `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriedades Personalizadas {#custom-properties}

Ao estender ou sobrepor um componente, é possível adicionar propriedades a uma caixa de diálogo modificada.

Todas as propriedades definidas em um componente/recurso podem ser acessadas referenciando as chaves da propriedade no modelo de handlebars:

`{{properties.<property_name>}}`

## CSS de capa {#skinning-css}

A personalização de componentes para corresponder ao tema geral do site pode ser alcançada com a definição de &quot;esfolamento&quot; - alteração de cores, fontes, imagens, botões, links, espaçamento e até mesmo posicionamento.

A capa pode ser alcançada substituindo seletivamente os estilos de estrutura ou escrevendo folhas de estilos inteiramente novas. Os componentes do SCF definem classes CSS namespacadas, modulares e semânticas que afetam os vários elementos que compõem um componente.

Para captar um componente:

1. Identifique os elementos que deseja alterar (por exemplo, área do compositor, botões da barra de ferramentas, fonte da mensagem etc.).
1. Identifique a classe/regras de CSS que afetam esses elementos.
1. Crie um arquivo de folha de estilos (.css).
1. Inclua a folha de estilos em uma pasta da biblioteca do cliente ([clientlibs](#clientlibs-for-scf)) para seu site e verifique se ele foi incluído nos modelos e páginas com [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redefina as classes e regras de CSS identificadas (#2) na sua folha de estilos e adicione estilos.

Os estilos personalizados agora substituirão os estilos de estrutura padrão e o componente será renderizado com a nova capa.

>[!CAUTION]
>
>Qualquer nome de classe CSS prefixado com `scf-js` O tem um uso específico no código javascript. Essas classes afetam o estado de um componente (por exemplo, alternar de oculto para visível) e não devem ser substituídas nem removidas.
>
>Enquanto a variável `scf-js` classes não afetam os estilos, os nomes de classe podem ser usados em folhas de estilos com a advertência de que, como controlam os estados dos elementos, pode haver efeitos colaterais.

## Extensão Do Javascript {#extending-javascript}

Para estender uma implementação de componentes do Javascript, é necessário:

1. Crie um componente para seu aplicativo com um jcr:resourceSuperType definido com o valor do jcr:resourceType do componente estendido, por exemplo, social/forum/components/hbs/forum.
1. Examine o Javascript do componente SCF padrão para determinar quais métodos precisam ser registrados usando SCF.registerComponent().
1. Copie o Javascript do componente estendido ou inicie do zero.
1. Estenda o método .
1. Use SCF.registerComponent() para registrar todos os métodos com os padrões ou com os objetos e visualizações personalizados.

### forum.js: Exemplo de extensão do Fórum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

As tags de script são uma parte inerente da estrutura do lado do cliente. Elas são a cola que ajuda a vincular a marcação gerada no lado do servidor aos modelos e visualizações no lado do cliente.

As tags de script em scripts SCF não devem ser removidas ao substituir ou substituir componentes. As tags de script SCF criadas automaticamente para injetar JSON no HTML são identificadas com o atributo `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

O uso de [bibliotecas do lado do cliente](../../help/sites-developing/clientlibs.md) (clientlibs), fornece um meio de organizar e otimizar o Javascript e o CSS usado para renderizar o conteúdo no cliente.

As clientlibs para SCF seguem um padrão de nomenclatura muito específico para duas variantes, que variam somente pela presença de &quot;autor&quot; no nome da categoria:

| Variante Clientlib | Padrão para a propriedade Categorias |
|--- |--- |
| clientlib completo | cq.social.hbs.&lt;component name> |
| clientlib do autor | cq.social.author.hbs.&lt;component name> |

### Clientlibs completos {#complete-clientlibs}

As clientlibs completas (não autoras) incluem dependências e são convenientes para inclusão com ui:includeClientLib.

Essas versões são encontradas em:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por exemplo:

* Nó da pasta do cliente: `/etc/clientlibs/social/hbs/forum`
* Propriedade Categorias: `cq.social.hbs.forum`

O [Guia de componentes da comunidade](components-guide.md) lista as clientlibs completas necessárias para cada componente do SCF.

[Clientlibs para componentes do Communities](clientlibs.md) descreve como adicionar clientlibs a uma página.

### Clientlibs de Autor {#author-clientlibs}

As clientlibs de versão do autor são removidas para o Javascript mínimo necessário para implementar o componente.

Essas clientlibs nunca devem ser incluídas diretamente, mas estão disponíveis para incorporação em outras clientlibs, que são artesanais para um site.

Essas versões são encontradas na pasta libs do SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por exemplo:

* Nó da pasta do cliente: `/libs/social/forum/hbs/forum/clientlibs`
* Propriedade Categorias: `cq.social.author.hbs.forum`

Observação: embora as clientlibs do autor nunca incorporem outras bibliotecas, elas listam suas dependências. Quando incorporadas em outras bibliotecas, as dependências não são automaticamente extraídas e também devem ser incorporadas.

As clientlibs do autor necessárias podem ser identificadas ao inserir &quot;autor&quot; nas clientlibs listadas para cada componente do SCF no [Guia de componentes da comunidade](components-guide.md).

### Considerações sobre o uso {#usage-considerations}

Cada site é diferente em como eles gerenciam bibliotecas de clientes. Vários fatores incluem:

* Velocidade geral: Talvez o desejo seja que o site seja responsivo, mas é aceitável que a primeira página seja um pouco lenta de carregamento. Se muitas páginas usarem o mesmo Javascript, os vários Javascripts poderão ser incorporados em uma clientlib e referenciados a partir da primeira página a ser carregada. O Javascript neste único download permanece em cache, minimizando a quantidade de dados para download nas páginas subsequentes.
* Hora abreviada para a primeira página: Talvez o desejo seja que a primeira página carregue rapidamente. Nesse caso, o Javascript está em vários arquivos pequenos para serem referenciados somente quando necessário.
* Um equilíbrio entre o primeiro carregamento de página e os downloads subsequentes.

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do servidor](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers †](handlebars-helpers.md)** |
