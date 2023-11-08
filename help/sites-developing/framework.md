---
title: Estrutura de marcação do AEM
description: Marcar conteúdo e usar a infraestrutura de Marcação AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---


# Estrutura de marcação do AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por um namespace e uma taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte o documento [Uso de tags](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte o documento [Administração de tags](/help/sites-administering/tags.md) para obter a perspectiva de um administrador sobre a criação e o gerenciamento de tags e a quais tags de conteúdo foram aplicadas.

Este artigo se concentra na estrutura subjacente que oferece suporte à marcação no AEM e em como usá-lo como desenvolvedor.

## Introdução {#introduction}

Para marcar conteúdo e usar a infraestrutura de marcação AEM:

* A tag deve existir como um nó do tipo `[cq:Tag](#tags-cq-tag-node-type)` no [nó raiz de taxonomia.](#taxonomy-root-node)

* O do nó de conteúdo marcado `NodeType` deve incluir o [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* A variável [`TagID`](#tagid) é adicionado ao do nó de conteúdo [`cq:tags`](#tagged-content-cq-tags-property) propriedade e é resolvido para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`.

## Tags : cq:Tag Node Type  {#tags-cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag`.

Uma tag pode ser uma palavra simples (por exemplo, `sky`) ou representam uma taxonomia hierárquica (por exemplo, `fruit/apple`, ou seja, os genéricos `fruit` e, mais especificamente, `apple`).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário, em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`n
* O nome do nó é um componente do [TagID](#tagid).
* A variável [TagID](#tagid) sempre inclui um [namespace.](#tag-namespace)
* A variável `jcr:title` (o título a ser exibido na interface do usuário) é opcional.
* A variável `jcr:description` é opcional.
* Ao conter nós filhos, a tag do é chamada de [tag container.](#container-tags)
* A tag é armazenada no repositório abaixo de um caminho base chamado de [nó raiz de taxonomia.](#taxonomy-root-node)

Como as tags são simplesmente nós JCR, os nomes dos nós devem obedecer à [Convenção de nomenclatura JCR.](naming-conventions.md)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a TagID é uma TagID abreviada que começa com o namespace ou pode ser uma TagID absoluta que começa com o [nó raiz de taxonomia.](#taxonomy-root-node)

Quando o conteúdo for marcado, se ainda não existir, a variável `[cq:tags](#tagged-content-cq-tags-property)` é adicionada ao nó de conteúdo e a TagID é adicionada à propriedade `String` valor da matriz.

A TagID consiste em um [namespace](#tag-namespace) seguido pela TagID local. [Tags de contêiner](#container-tags) ter subtags que representam uma ordem hierárquica na taxonomia. Subtags podem ser usadas para fazer referência a tags como qualquer TagID local. Por exemplo, marcar conteúdo com `fruit` é permitido, mesmo se for uma tag container com subtags, como `fruit/apple` e `fruit/banana`.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia não deve ser um nó do tipo `cq:Tag`.

No AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais típico é um namespace por site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Ativos, Comunidades). Mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo de [nó raiz de taxonomia](#taxonomy-root-node). Um namespace é um nó do tipo `cq:Tag` cujo pai não é um `cq:Tag` tipo de nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é TagID `default` com o título `Standard Tags`, ou seja, `/content/cq:tags/default`.

### Tags de contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós secundários, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, tags container (ou supertags) em uma taxonomia servem como subsoma de todas as subtags. Por exemplo, conteúdo marcado com `fruit/apple` é considerado marcado com `fruit` também. Ou seja, pesquisar conteúdo marcado com `fruit` também localizaria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a TagID contiver dois pontos (`:`), os dois pontos separam o namespace da tag ou subtaxonomia, que é separada por barras (`/`). Se TagID não tiver dois pontos, o namespace padrão será considerado.

O local padrão e único das tags é abaixo de `/content/cq:tags`.

Marca que faz referência a caminhos ou caminhos não existentes que não apontam para um `cq:Tag` são considerados inválidos e são ignorados.

A tabela a seguir mostra algumas amostras de TagIDs, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

| TagID | Namespace | ID local | Tags de contêiner | Tag de folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`, `apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | Nenhum | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | Nenhum | Nenhum | Nenhum, o namespace | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional ( `jcr:title`), é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte os seguintes documentos:

* [Tags em diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages), que descreve o uso das APIs
* [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), que descreve o uso do console de marcação

### Controle de acesso {#access-control}

As tags existem como nós no repositório, na variável [nó raiz de taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controla a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo que o `tag-administrators` acesso de gravação de grupo/função a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Esse grupo vem com AEM pronto para uso.
* Permitir que usuários/autores leiam todos os namespaces que devem ser legíveis para eles (principalmente todos).
* Permitir que usuários/autores gravem acesso aos namespaces em que as tags devem ser definidas livremente por usuários/autores (adicione um nó sob `/content/cq:tags/some_namespace`)

## Conteúdo Marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) devem incluir a `cq:Taggable` mixin ou o `cq:OwnerTaggable` mixin.

A variável `cq:OwnerTaggable` mixin, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó. A variável `cq:OwnerTaggable` O mixin não é exigido pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar tags somente no nó de nível superior de um item de conteúdo agregado (ou em sua `jcr:content` nó). Os exemplos incluem:
>
>* Páginas (`cq:Page`) em que o `jcr:content`o nó é do tipo `cq:PageContent` que inclui a `cq:Taggable` mixin
>* Ativos ( `cq:Asset`) em que o `jcr:content/metadata` o nó sempre tem o `cq:Taggable` mixin
>

### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação do JCR [aqui](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

A variável `cq:tags` propriedade é um `String` Matriz usada para armazenar uma ou mais TagIDs quando elas são aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com o `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Para usar a funcionalidade de marcação AEM, os aplicativos desenvolvidos de forma personalizada não devem definir propriedades de tag diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o [console de marcação](/help/sites-administering/tags.md):

* Quando uma tag A é movida ou mesclada na tag B em `/content/cq:tags`:

   * A tag A não é excluída e obtém um `cq:movedTo` propriedade.
   * A tag B é criada (se houver uma movimentação) e obtém um `cq:backlinks` propriedade.

* `cq:movedTo` aponta para a tag B.

   * Essa propriedade significa que a tag A foi movida ou mesclada na tag B. Mover a tag B atualiza essa propriedade de acordo. A tag A fica oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo da tag remove tags como a tag A assim que os nós de conteúdo não apontam mais para elas.

   * Um valor especial para o `cq:movedTo` propriedade é `nirvana`. Ele é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma `cq:movedTo` que deve ser mantido.

  >[!NOTE]
  >
  >A variável `cq:movedTo` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
  >
  >1. Tag for usada no conteúdo (significando que tem uma referência) ou
  >1. A tag tem filhos que já foram movidos.

* `cq:backlinks` mantém as referências na outra direção. Ou seja, ela mantém uma lista de todas as tags que foram movidas ou mescladas com a tag B. Isso é necessário principalmente para manter `cq:movedTo` propriedades atualizadas quando a tag B é movida/mesclada/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

  >[!NOTE]
  >
  >A variável `cq:backlinks` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
  >
  >1. A tag é usada no conteúdo (o que significa que tem uma referência) OU
  >1. A tag tem filhos que já foram movidos.

* Ler um `cq:tags` A propriedade de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag é retornada.

   1. Se a tag tiver uma `cq:movedTo` for definida, a ID da tag referenciada será seguida.

      * Esta etapa é repetida desde que a tag seguida tenha uma `cq:movedTo` propriedade.

   1. Se a tag seguida não tiver um `cq:movedTo` propriedade, a tag será lida.

* Para publicar a alteração quando uma tag tiver sido movida ou mesclada, a variável `cq:Tag` e todos os seus backlinks devem ser replicados. Isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores no da página `cq:tags` propriedade limpa automaticamente as referências antigas. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.

>[!NOTE]
>
>O movimento de tags é diferente da migração de tags.

## Migração de tags {#tags-migration}

A partir do Adobe Experience Manager 6.4, as tags são armazenadas no `/content/cq:tags` Considerando que as versões anteriores armazenavam tags em `/etc/tags`.

Sempre que atualizar um sistema AEM de uma versão anterior à 6.4, as tags devem ser migradas para `/content/cq:tags`. Consulte [Reestruturação do repositório comum no AEM 6.5](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags) para obter mais informações.
