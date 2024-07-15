---
title: Estrutura de marcação do AEM
description: Marcar conteúdo e usar a infraestrutura de Marcação AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Developing,Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 0%

---


# Estrutura de marcação do AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por um namespace e uma taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte o documento [Usando Tags](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte o documento [Administração de tags](/help/sites-administering/tags.md) para obter a perspectiva de um administrador sobre como criar e gerenciar tags e para quais tags de conteúdo foram aplicadas.

Este artigo se concentra na estrutura subjacente que oferece suporte à marcação no AEM e em como usá-lo como desenvolvedor.

## Introdução {#introduction}

Para marcar conteúdo e usar a infraestrutura de marcação AEM:

* A marca deve existir como um nó do tipo `[cq:Tag](#tags-cq-tag-node-type)` no nó raiz de [taxonomia.](#taxonomy-root-node)

* O nó de conteúdo marcado `NodeType` deve incluir o mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* O [`TagID`](#tagid) é adicionado à propriedade [`cq:tags`](#tagged-content-cq-tags-property) do nó de conteúdo e é resolvido para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`.

## Tags : cq:Tag Node Type  {#tags-cq-tag-node-type}

A declaração de uma marca é capturada no repositório em um nó do tipo `cq:Tag`.

Uma marca pode ser uma palavra simples (por exemplo, `sky`) ou representar uma taxonomia hierárquica (por exemplo, `fruit/apple`, significando tanto o `fruit` genérico quanto o `apple` mais específico).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário, em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`n
* O nome do nó é um componente de [TagID](#tagid).
* A [TagID](#tagid) sempre inclui um [namespace.](#tag-namespace)
* A propriedade `jcr:title` (o título a ser exibido na interface do usuário) é opcional.
* A propriedade `jcr:description` é opcional.
* Ao conter nós filhos, a marca é chamada de [marca de contêiner.](#container-tags)
* A marca é armazenada no repositório abaixo de um caminho base chamado nó raiz de taxonomia [.](#taxonomy-root-node)

Como as marcas são simplesmente nós JCR, os nomes dos nós devem obedecer à [convenção de nomenclatura JCR.](naming-conventions.md)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a TagID é uma TagID abreviada que começa com o namespace ou pode ser uma TagID absoluta que começa no [nó raiz de taxonomia.](#taxonomy-root-node)

Quando o conteúdo é marcado, se ainda não existir, a propriedade `[cq:tags](#tagged-content-cq-tags-property)` é adicionada ao nó de conteúdo e o TagID é adicionado ao valor da matriz `String` da propriedade.

A TagID consiste em um [namespace](#tag-namespace) seguido pela TagID local. [Marcas de contêiner](#container-tags) têm submarcas que representam uma ordem hierárquica na taxonomia. Subtags podem ser usadas para fazer referência a tags como qualquer TagID local. Por exemplo, a marcação de conteúdo com `fruit` é permitida, mesmo que seja uma marca de contêiner com submarcas, como `fruit/apple` e `fruit/banana`.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia não deve ser um nó do tipo `cq:Tag`.

No AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais típico é um namespace por site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Assets, Communities). Mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da marca é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo do [nó raiz de taxonomia](#taxonomy-root-node). Um namespace é um nó do tipo `cq:Tag` cujo pai não é um tipo de nó `cq:Tag`.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a marca será atribuída ao namespace padrão, que é TagID `default` com o título `Standard Tags`, ou seja, `/content/cq:tags/default`.

### Tags de contêiner {#container-tags}

Uma marca de contêiner é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós filhos, o que permite aprimorar o modelo de marca com metadados personalizados.

Além disso, tags container (ou supertags) em uma taxonomia servem como subsoma de todas as subtags. Por exemplo, o conteúdo marcado com `fruit/apple` também é considerado marcado com `fruit`. Ou seja, pesquisar conteúdo marcado com `fruit` também localizaria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a TagID contiver dois pontos (`:`), os dois pontos separarão o namespace da marca ou subtaxonomia, que é separada ainda mais com barras (`/`). Se TagID não tiver dois pontos, o namespace padrão será considerado.

O local padrão e único das marcas está abaixo de `/content/cq:tags`.

A marca que faz referência a caminhos ou caminhos não existentes que não apontam para um nó `cq:Tag` é considerada inválida e é ignorada.

A tabela a seguir mostra algumas amostras de TagIDs, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

| TagID | Namespace | ID local | Tags de contêiner | Tag de folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Nenhum | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Nenhum | Nenhum | Nenhum, o namespace | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a marca inclui a cadeia de caracteres de título opcional ( `jcr:title`), é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte os seguintes documentos:

* [Marcas em Diferentes Idiomas](/help/sites-developing/building.md#tags-in-different-languages), que descreve o uso das APIs
* [Gerenciamento de Marcas em Diferentes Idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), que descreve o uso do console de marcação

### Controle de acesso {#access-control}

As marcas existem como nós no repositório no [nó raiz de taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controla a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo acesso de gravação de grupo/função `tag-administrators` a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Esse grupo vem com AEM pronto para uso.
* Permitir que usuários/autores leiam todos os namespaces que devem ser legíveis para eles (principalmente todos).
* Permitir que usuários/autores gravem acesso aos namespaces em que as marcas devem ser definidas livremente por usuários/autores (adicione um nó sob `/content/cq:tags/some_namespace`)

## Conteúdo Marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve incluir o mixin `cq:Taggable` ou `cq:OwnerTaggable`.

O mixin `cq:OwnerTaggable`, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do nó `cq:PageContent`. O mixin `cq:OwnerTaggable` não é exigido pela estrutura de marcação.

>[!NOTE]
>
>É recomendável habilitar tags somente no nó de nível superior de um item de conteúdo agregado (ou em seu nó `jcr:content`). Os exemplos incluem:
>
>* Páginas (`cq:Page`) onde o nó `jcr:content` é do tipo `cq:PageContent` que inclui o mixin `cq:Taggable`
>* Assets ( `cq:Asset`) onde o nó `jcr:content/metadata` sempre tem o mixin `cq:Taggable`
>

### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação JCR [aqui](https://jackrabbit.apache.org/jcr/node-type-notation.html).

As definições essenciais para os Tipos de nós incluídos no AEM são as seguintes:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## Conteúdo marcado: cq:tags Propriedade {#tagged-content-cq-tags-property}

A propriedade `cq:tags` é uma matriz `String` usada para armazenar uma ou mais TagIDs quando elas são aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com o mixin `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Para usar a funcionalidade de marcação AEM, os aplicativos personalizados desenvolvidos não devem definir propriedades de marca diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Esta é uma descrição dos efeitos no repositório ao mover ou mesclar marcas usando o [console de marcação](/help/sites-administering/tags.md):

* Quando uma tag A é movida ou mesclada na tag B em `/content/cq:tags`:

   * A tag A não é excluída e obtém uma propriedade `cq:movedTo`.
   * A marca B é criada (se houver uma movimentação) e obtém uma propriedade `cq:backlinks`.

* `cq:movedTo` pontos para a marca B.

   * Essa propriedade significa que a tag A foi movida ou mesclada na tag B. Mover a tag B atualiza essa propriedade de acordo. A tag A fica oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo da tag remove tags como a tag A assim que os nós de conteúdo não apontam mais para elas.

   * Um valor especial para a propriedade `cq:movedTo` é `nirvana`. Ele é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com um `cq:movedTo` que deve ser mantido.

  >[!NOTE]
  >
  >A propriedade `cq:movedTo` só será adicionada à marca movida ou mesclada se qualquer uma destas condições for atendida:
  >
  >1. Tag for usada no conteúdo (significando que tem uma referência) ou
  >1. A tag tem filhos que já foram movidos.

* `cq:backlinks` mantém as referências na outra direção. Ou seja, ela mantém uma lista de todas as tags que foram movidas ou mescladas com a tag B. Isso é necessário principalmente para manter as propriedades `cq:movedTo` atualizadas quando a tag B também é movida/mesclada/excluída ou quando a tag B é ativada, caso em que todas as tags de backlinks também devem ser ativadas.

  >[!NOTE]
  >
  >A propriedade `cq:backlinks` só será adicionada à marca movida ou mesclada se qualquer uma destas condições for atendida:
  >
  >1. A tag é usada no conteúdo (o que significa que tem uma referência) OU
  >1. A tag tem filhos que já foram movidos.

* A leitura de uma propriedade `cq:tags` de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag será retornada.

   1. Se a marca tiver um conjunto de propriedades `cq:movedTo`, a ID de marca referenciada será seguida.

      * Esta etapa será repetida desde que a marca seguida tenha uma propriedade `cq:movedTo`.

   1. Se a marca seguida não tiver uma propriedade `cq:movedTo`, a marca será lida.

* Para publicar a alteração quando uma marca for movida ou mesclada, o nó `cq:Tag` e todos os seus backlinks deverão ser replicados. Isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores na propriedade `cq:tags` da página limpam automaticamente as referências antigas. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.

>[!NOTE]
>
>O movimento de tags é diferente da migração de tags.

## Migração de tags {#tags-migration}

A partir do Adobe Experience Manager 6.4, as tags são armazenadas em `/content/cq:tags`, enquanto as versões anteriores armazenavam tags em `/etc/tags`.

Sempre que atualizar um sistema AEM de uma versão anterior à 6.4, as tags devem ser migradas para o `/content/cq:tags`. Consulte [Reestruturação do repositório comum no AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) para obter mais informações.
