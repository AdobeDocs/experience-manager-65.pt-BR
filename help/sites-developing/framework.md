---
title: Estrutura de marcação do AEM
seo-title: Estrutura de marcação do AEM
description: Adicione tags ao conteúdo e aproveite a infraestrutura de AEM Tagging
seo-description: Adicione tags ao conteúdo e aproveite a infraestrutura de AEM Tagging
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Estrutura de marcação do AEM{#aem-tagging-framework}

Para marcar o conteúdo e aproveitar a infraestrutura de marcação do AEM:

* A tag deve existir como um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)` no nó raiz [da taxonomia](#taxonomy-root-node)

* O NodeType do nó de conteúdo marcado deve incluir a [ combinação `cq:Taggable`](#taggable-content-cq-taggable-mixin)
* A [TagID](#tagid) é adicionada à [ propriedade do nó de conteúdo `cq:tags`](#tagged-content-cq-tags-property) e resolve para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tags: cq:Tipo de nó de tag {#tags-cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

Uma marca pode ser uma palavra simples (por exemplo, o céu) ou representar uma taxonomia hierárquica (por exemplo, fruta/maçã, ou seja, tanto o fruto genérico como a maçã mais específica).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* o tipo de nó é `cq:Tag`
* o nome do nó é um componente do ` [TagID](#tagid)`
* o ` [TagID](#tagid)` sempre inclui um [namespace](#tag-namespace)

* propriedade opcional `jcr:title` (o Título a ser exibido na interface do usuário)

* propriedade opcional `jcr:description`

* ao conter nós filhos, é chamada de tag [container](#container-tags)
* é armazenado no repositório abaixo de um caminho base chamado nó raiz de [taxonomia](#taxonomy-root-node)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a TagID é uma TagID abreviada que começa com o namespace ou pode ser uma TagID absoluta que começa no nó [raiz da](#taxonomy-root-node)taxonomia.

Quando o conteúdo é marcado, se ainda não existir, a ` [cq:tags](#tagged-content-cq-tags-property)` propriedade é adicionada ao nó de conteúdo e a TagID é adicionada ao valor da matriz String da propriedade.

A TagID consiste em um [namespace](#tag-namespace) seguido pela TagID local. [As tags](#container-tags) do contêiner têm subtags que representam uma ordem hierárquica na taxonomia. As subtags podem ser usadas para referenciar tags como qualquer TagID local. Por exemplo, é permitida a marcação do conteúdo com &quot;fruta&quot;, mesmo que se trate de uma marca de embalagem com sub-marcas, como &quot;fruta/maçã&quot; e &quot;fruta/banana&quot;.

### Nó raiz de taxonomia {#taxonomy-root-node}

O nó raiz de taxonomia é o caminho base para todas as tags no repositório. O nó raiz de taxonomia *não* deve ser do tipo `  cq   :Tag`.

No AEM, o caminho base é `/content/  cq   :tags` e o nó raiz é do tipo `  cq   :Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar coisas. O caso de uso mais comum é ter um namespace por (web)site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Ativos, Comunidades), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo do nó [raiz de](#taxonomy-root-node)taxonomia. Um namespace é um nó do tipo `cq:Tag` cujo pai não é um tipo de `cq:Tag`nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é TagID `default` (Título `Standard Tags),`que é `/content/cq:tags/default.`

### Tags do contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós filhos, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, as tags de contêiner (ou super tags) em uma taxonomia servem como subsoma de todas as subtags: por exemplo, considera-se que o conteúdo marcado com frutas/maçãs também é marcado com frutos, ou seja, procurar por conteúdo marcado apenas com frutos também encontraria o conteúdo marcado com frutas/maçã.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos &quot;:&quot;, os dois pontos separarão o namespace da tag ou subtaxonomia, que são separados por barras normais &quot;/&quot;. Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das tags está abaixo das tags /content/cq:.

A tag que faz referência a caminhos ou caminhos não existentes que não apontam para um nó cq:Tag é considerada inválida e é ignorada.

A tabela a seguir mostra algumas TagIDs de amostra, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:


A tabela a seguir mostra algumas TagIDs de amostra, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:
A tabela a seguir mostra algumas TagIDs de amostra, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

<table>
 <tbody>
  <tr>
   <td><strong>TagID<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Tags do contêiner</strong></td>
   <td><strong>Marca Folha</strong></td>
   <td><strong>Caminho absoluto da tag do repositório<br /></strong></td>
  </tr>
  <tr>
   <td>represa:fruta/maçã/queimadura</td>
   <td>barragem</td>
   <td>fruta/maçã/queimadura</td>
   <td>fruta, maçã</td>
   <td>braquia</td>
   <td>/content/cq:tags/dam/frus/apple/braeburn</td>
  </tr>
  <tr>
   <td>cor/vermelho</td>
   <td>default</td>
   <td>cor/vermelho</td>
   <td>cor</td>
   <td>red</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>céu</td>
   <td>default</td>
   <td>céu</td>
   <td>(nenhum)</td>
   <td>céu</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>barragem:</td>
   <td>barragem</td>
   <td>(nenhum)</td>
   <td>(nenhum)</td>
   <td>(nenhum, o namespace)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/category/car</td>
   <td>categoria</td>
   <td>carro</td>
   <td>carro</td>
   <td>carro</td>
   <td>/content/cq:tags/category/car</td>
  </tr>
 </tbody>
</table>

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional ( `jcr:title`), é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte

* [Tags em diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages) - que descreve o uso das APIs
* [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) - que descreve o uso do console Marcação

### Controle de acesso {#access-control}

As tags existem como nós no repositório no nó [raiz de](#taxonomy-root-node)taxonomia. Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido ao configurar ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo o acesso de gravação de `tag-administrators` grupo/função a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Este grupo vem com o AEM pronto para usar.

* Permitir que os usuários/autores leiam o acesso a todos os namespaces que devem ser legíveis para eles (na maioria das vezes, todos).
* Permitir que usuários/autores gravem acesso aos namespaces nos quais as tags devem ser definidas livremente pelos usuários/autores (add_node em `/content/cq:tags/some_namespace`)

## Conteúdo marcável: cq:Mistura marcável {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve incluir a `cq:Taggable` mistura ou a `cq:OwnerTaggable` mistura.

A `cq:OwnerTaggable` mistura, que herda de `cq:Taggable`, serve para indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó. A `cq:OwnerTaggable` mistura não é exigida pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar somente tags no nó de nível superior de um item de conteúdo agregado (ou em seu nó jcr:content). Os exemplos incluem:
>
>* páginas ( `cq:Page`) em que o `jcr:content`nó é do tipo `cq:PageContent` que inclui a `cq:Taggable` mistura.
   >
   >
* ativos ( `cq:Asset`) em que o `jcr:content/metadata` nó sempre tem a `cq:Taggable` combinação.
>



### Nó de notação de tipo (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação JCR [aqui](https://jackrabbit.apache.org/node-type-notation.html).

As definições essenciais para os tipos de nó incluídos no AEM são as seguintes:

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

## Conteúdo marcado: cq:tags Property {#tagged-content-cq-tags-property}

A `cq:tags` propriedade é uma matriz String usada para armazenar uma ou mais TagIDs quando aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó que é definido com a ` [cq:Taggable](#taggable-content-cq-taggable-mixin)` mistura.

>[!NOTE]
>
>Para aproveitar a funcionalidade de marcação AEM, os aplicativos desenvolvidos personalizados não devem definir outras propriedades de tags além `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

A seguir está uma descrição dos efeitos no repositório ao mover ou unir tags usando o console [](/help/sites-administering/tags.md)Marcação:

* Quando uma tag A é movida ou unida na tag B em `/content/cq:tags`:

   * a tag A não é excluída e obtém uma `cq:movedTo` propriedade.
   * a tag B é criada (no caso de uma movimentação) e obtém uma `cq:backlinks` propriedade.

* `cq:movedTo` aponta para a tag B.
Essa propriedade significa que a tag A foi movida ou mesclada para a tag B. Mover a tag B atualizará essa propriedade de acordo. A tag A fica então oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo de tags remove tags como a tag A, uma vez que nenhum nó de conteúdo aponta para elas.
Um valor especial para a `cq:movedTo` propriedade é `nirvana`: ela é aplicada quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma tag `cq:movedTo` que deve ser mantida.

   >[!NOTE]
   >
   >A `cq:movedTo` propriedade só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   > 1. A tag é usada no conteúdo (ou seja, tem uma referência) OU
   > 1. A tag tem filhos que já foram movidos.


* `cq:backlinks` mantém as referências na outra direção, isto é, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B. Isso é necessário principalmente para manter `cq:movedTo`as propriedades atualizadas quando a tag B também é movida/unida/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

   >[!NOTE]
   >
   >A `cq:backlinks` propriedade só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   > 1. A tag é usada no conteúdo (ou seja, tem uma referência) OU
   > 1. A tag tem filhos que já foram movidos.


* Ler uma `cq:tags` propriedade de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag será retornada.
   1. Se a tag tiver uma `cq:movedTo` propriedade definida, a ID da tag referenciada será seguida.
Essa etapa é repetida desde que a tag seguida tenha uma `cq:movedTo` propriedade.

   1. Se a tag seguida não tiver uma `cq:movedTo` propriedade, ela será lida.

* Para publicar a alteração quando uma tag tiver sido movida ou unida, o `cq:Tag` nó e todos os seus backlinks devem ser replicados: isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores à propriedade da página `cq:tags` limpam automaticamente as referências &quot;antigas&quot;. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo assim a ID da tag de destino.
