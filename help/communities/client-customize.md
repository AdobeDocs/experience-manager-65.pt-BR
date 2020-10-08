---
title: Personalização do cliente
seo-title: Personalização do cliente
description: Personalizar comportamento ou aparência do lado do cliente no AEM Communities
seo-description: Personalizar comportamento ou aparência do lado do cliente no AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# Personalização do cliente  {#client-side-customization}

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Utilitário de personalização do servidor](server-customize.md)** |
|---|---|
|  | **[Auxiliares da proteção contra a fraude SCF](handlebars-helpers.md)** |

Para personalizar a aparência e/ou o comportamento de um componente AEM Communities no lado do cliente, há várias abordagens.

Duas abordagens principais são sobrepor ou estender um componente.

[A sobreposição](#overlays) de um componente altera o componente padrão e afeta todas as referências ao componente.

[Estender](#extensions) um componente, sendo nomeado unicamente, limita o escopo das alterações. O termo &quot;extensão&quot; é utilizado de forma permutável com &quot;substituição&quot;.

## Sobreposições {#overlays}

Sobrepor um componente é um método para fazer modificações em um componente padrão e afetar todas as instâncias que usam o padrão.

A sobreposição é realizada modificando uma cópia do componente padrão no diretório /**apps** , em vez de modificar o componente original no diretório /**libs** . O componente é construído com um caminho relativo idêntico, exceto que &quot;libs&quot; é substituído por &quot;apps&quot;.

O diretório /apps é o primeiro local pesquisado para resolver solicitações e, se não for encontrado, a versão padrão localizada no diretório /libs é usada.

O componente padrão no diretório /libs nunca deve ser modificado, pois os patches e atualizações futuros são gratuitos para alterar o diretório /libs de qualquer maneira necessária, mantendo as interfaces públicas.

Isso é diferente de [estender](#extensions) um componente padrão no qual o desejo é fazer modificações para um uso específico, criar um caminho exclusivo para o componente e depender da referência do componente padrão original no diretório /libs como o tipo de superrecurso.

Para obter um exemplo rápido de sobreposição do componente de comentários, tente o tutorial [Componente](overlay-comments.md)Sobrepor comentários.

## Extensões {#extensions}

A extensão (substituição) de um componente é um método de fazer modificações para um uso específico sem afetar todas as instâncias que usam o padrão. O componente estendido é nomeado exclusivamente na pasta /apps e faz referência ao componente padrão na pasta /libs, portanto, o design e o comportamento padrão de um componente não são modificados.

Isso é diferente da [sobreposição](#overlays) do componente padrão, no qual a natureza do Sling resolve referências relativas à pasta/aplicativos antes de pesquisar na pasta libs/, portanto, o design ou comportamento de um componente é modificado globalmente.

Para obter um exemplo rápido de como estender o componente de comentários, experimente o tutorial [](extend-comments.md)Extend Comments Component.

## Vínculo Javascript {#javascript-binding}

O script HBS do componente deve estar vinculado aos objetos, modelos e visualizações JavaScript, que implementam esse recurso.

O valor do `data-scf-component` atributo pode ser o padrão, como **`social/tally/components/hbs/rating`**, ou um componente estendido (personalizado) para funcionalidade personalizada, como **weretail/components/hbs/rating**.

Para vincular um componente, o script de componente inteiro deve estar incluído em um elemento &lt;div> com os seguintes atributos:

* `data-component-id`=&quot;{{id}}&quot;

   resolve para a propriedade id do contexto

* `data-scf-component`=&quot;*&lt;resourceType>*

Por exemplo, de `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## Propriedades Personalizadas {#custom-properties}

Ao estender ou sobrepor um componente, é possível adicionar propriedades a uma caixa de diálogo modificada.

Todas as propriedades definidas em um componente/recurso podem ser acessadas fazendo referência às chaves de propriedade no modelo handlebars:

`{{properties.<property_name>}}`

## CSS de capa {#skinning-css}

A personalização de componentes para corresponder ao tema geral do site pode ser alcançada pela &quot;capa&quot; - alteração de cores, fontes, imagens, botões, links, espaçamento e até mesmo posicionamento em certa medida.

A capa pode ser obtida substituindo seletivamente os estilos de estrutura ou escrevendo folhas de estilos totalmente novas. Os componentes SCF definem classes CSS namespacadas, modulares e semânticas que afetam os vários elementos que compõem um componente.

Para aplicar capa a um componente:

1. Identifique os elementos que deseja alterar (por exemplo - área do compositor, botões da barra de ferramentas, fonte da mensagem etc.).
1. Identifique a classe/regras CSS que afetam esses elementos.
1. Crie um arquivo de folha de estilos (.css).
1. Inclua a folha de estilo em uma pasta da biblioteca do cliente ([clientlibs](#clientlibs-for-scf)) para o seu site e verifique se ela foi incluída em seus modelos e páginas com [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. Redefina as classes e regras CSS identificadas (#2) na sua folha de estilos e adicione estilos.

Os estilos personalizados substituirão os estilos de estrutura padrão e o componente será renderizado com a nova capa.

>[!CAUTION]
>
>Qualquer nome de classe CSS com prefixo `scf-js` tem um uso específico no código javascript. Essas classes afetam o estado de um componente (por exemplo, alternar de oculto para visível) e não devem ser substituídas nem removidas.
>
>Embora as `scf-js` classes não afetem estilos, os nomes das classes podem ser usados em folhas de estilo com a ressalva de que, como controlam os estados dos elementos, podem haver efeitos colaterais.

## Extensão do Javascript {#extending-javascript}

Para estender uma implementação do Javascript de componentes, é necessário:

1. Crie um componente para seu aplicativo com um conjunto jcr:resourceSuperType definido com o valor de jcr:resourceType do componente estendido, por exemplo, social/forum/components/hbs/forum.
1. Examine o Javascript do componente SCF padrão para determinar que métodos devem ser registrados usando SCF.registerComponent().
1. Copie o Javascript ou o start do componente estendido do zero.
1. Estende o método.
1. Use SCF.registerComponent() para registrar todos os métodos com os padrões ou os objetos e visualizações personalizados.

### forum.js: Exemplo de extensão do fórum - HBS  {#forum-js-sample-extension-of-forum-hbs}

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

As tags de script nos scripts SCF não devem ser removidas ao substituir ou substituir componentes. As tags de script SCF criadas automaticamente para injetar JSON no HTML são identificadas com o atributo `data-scf-json=true`.

## Clientlibs para SCF {#clientlibs-for-scf}

O uso de bibliotecas [do lado do](../../help/sites-developing/clientlibs.md) cliente (clientlibs) fornece uma forma de organizar e otimizar o Javascript e o CSS usados para renderizar conteúdo no cliente.

As clientlibs para SCF seguem um padrão de nomenclatura muito específico para duas variantes, que variam apenas pela presença de &#39;autor&#39; no nome da categoria:

| Variante Clientlib | Padrão para a propriedade Categoria |
|--- |--- |
| clientlib completo | cq.social.hbs.&lt;nome do componente> |
| clientlib do autor | cq.social.author.hbs.&lt;nome do componente> |

### Complete Clientlibs {#complete-clientlibs}

Os clientlibs completos (não autores) incluem dependências e são convenientes para inclusão com ui:includeClientLib.

Essas versões são encontradas em:

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

Por exemplo:

* Nó de pasta do cliente: `/etc/clientlibs/social/hbs/forum`
* propriedade Categoria: `cq.social.hbs.forum`

O guia [Componentes da](components-guide.md) comunidade lista as clientlibs completas necessárias para cada componente do SCF.

[Clientlibs for Communities Os componentes](clientlibs.md) descrevem como adicionar clientlibs a uma página.

### Clientlibs do autor {#author-clientlibs}

As clientlibs da versão do autor são eliminadas até o Javascript mínimo necessário para implementar o componente.

Essas clientlibs nunca devem ser incluídas diretamente, mas estão disponíveis para incorporação em outras clientlibs, que são artesanais para um site.

Essas versões são encontradas na pasta libs SCF:

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

Por exemplo:

* Nó de pasta do cliente: `/libs/social/forum/hbs/forum/clientlibs`
* propriedade Categoria: `cq.social.author.hbs.forum`

Observação: enquanto os clientlibs do autor nunca incorporam outras bibliotecas, eles fazem lista de suas dependências. Quando incorporadas em outras bibliotecas, as dependências não são automaticamente extraídas e também devem ser incorporadas.

Os clientlibs do autor necessários podem ser identificados inserindo &quot;autor&quot; nos clientlibs listados para cada componente do SCF no guia [Componentes da](components-guide.md)comunidade.

### Considerações sobre o uso {#usage-considerations}

Cada site é diferente em como gerenciam bibliotecas de clientes. Vários fatores incluem:

* Velocidade geral: Talvez o desejo seja que o site responda, mas é aceitável que a primeira página seja um pouco lenta de carregamento. Se muitas das páginas usarem o mesmo Javascript, os vários Javascripts poderão ser incorporados em um clientlib e referenciados a partir da primeira página a ser carregada. O Javascript neste único download permanece em cache, minimizando a quantidade de dados para download para páginas subsequentes.
* Tempo curto para a primeira página: Talvez o desejo seja que a primeira página seja carregada rapidamente. Nesse caso, o Javascript está em vários arquivos pequenos para serem referenciados somente quando necessário.
* Um equilíbrio entre o carregamento da primeira página e os downloads subsequentes.

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Utilitário de personalização do servidor](server-customize.md)** |
|---|---|
|  | **[Auxiliares da proteção contra a fraude SCF](handlebars-helpers.md)** |

