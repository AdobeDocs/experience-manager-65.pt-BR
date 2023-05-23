---
title: Criação de tags em um aplicativo AEM
seo-title: Building Tagging into an AEM Application
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---

# Criação de tags em um aplicativo AEM{#building-tagging-into-an-aem-application}

Para trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado, esta página descreve o uso da variável

* [API de marcação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](/help/sites-developing/framework.md)

Para obter informações relacionadas à marcação, consulte:

* [Administração de tags](/help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags e sobre quais tags de conteúdo foram aplicadas.
* [Uso de tags](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A execução do [estrutura de marcação](/help/sites-developing/framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. O TagManager garante que as tags sejam inseridas como valores na variável `cq:tags` As propriedades de matriz de sequência de caracteres não são duplicadas. Elas removem as TagIDs que apontam para tags não existentes e atualizam as TagIDs para tags movidas ou mescladas. O TagManager usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão na [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) pacote:

* JcrTagManagerFactory - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite a resolução e a criação de tags por caminhos e nomes.
* `Tag` - define o objeto de tag.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância do TagManager, você precisa ter um JCR `Session` e para chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, também é possível adaptar a uma `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

A `Tag` pode ser recuperado por meio da variável `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` no JCR `Nodes`, você pode usar o do Sling diretamente `adaptTo` se você tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma tag só possa ser convertida *a partir de *um recurso (não um nó), uma tag pode ser convertida *em *um nó e um recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptando-se diretamente do `Node` para `Tag` não é possível, porque `Node` não implementa o Sling `Adaptable.adaptTo(Class)` método.

### Obter e definir tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Pesquisando tags {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>O válido `RangeIterator` usar é:
>
>`com.day.cq.commons.RangeIterator`

### Exclusão de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação ( `Replicator`) com tags, pois as tags são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Marcação no lado do cliente {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` é um widget de formulário para inserção de tags. Ele tem um menu pop-up para seleção entre tags existentes, inclui preenchimento automático e muitos outros recursos. Seu xtype é `tags`.

## O coletor de lixo da tag {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não usadas. Tags ocultas e não usadas são as tags abaixo `/content/cq:tags` que tenham um `cq:movedTo` e não são usados em um nó de conteúdo - têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, o `cq:tags` ) não precisa ser atualizada como parte da operação de mover ou mesclar. As referências no `cq:tags` são atualizados automaticamente quando a variável `cq:tags` A propriedade do é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Pesquisa de tags e listagem de tags {#tag-search-and-tag-listing}

A pesquisa de tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por TagID pesquisa as tags que têm a propriedade `cq:movedTo` Defina como TagID e siga as etapas de `cq:movedTo` TagIDs.

* A pesquisa por título de tag pesquisa somente as tags que não têm um `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Conforme descrito na documentação para administração de tags, na seção [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), uma tag `title`podem ser definidos em diferentes idiomas. Em seguida, uma propriedade que diferencia idiomas é adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` pela tradução francesa. `<locale>` deve ser uma sequência de caracteres de localidade ISO em minúsculas e usar &quot;_&quot; em vez de &quot;-&quot;, por exemplo: `de_ch`.

Quando a variável **Animais** é adicionada à guia **Produtos** página, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó /content/geometrixx/en/products/jcr:content. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor localizou `title`Métodos relacionados ao:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Localidade)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Local)
   * getTitlePath(Localidade)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, localidade)
   * createTagByTitle(String tagTitlePath, localidade)
   * resolveByTitle(String tagTitlePath, localidade)

No AEM, o idioma pode ser obtido no idioma da página ou no idioma do usuário:

* para recuperar o idioma da página em uma JSP:

   * `currentPage.getLanguage(false)`

* para recuperar o idioma do usuário em uma JSP:

   * `slingRequest.getLocale()`

`currentPage` e `slingRequest` estão disponíveis em um JSP por meio do [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) tag.

Para marcação, a localização depende do contexto como tag `titles`pode ser exibido no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (finlandês) à **Editar tag** diálogo:

1. Entrada **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.

1. Adicionar `fi_fi` - que representa a localidade finlandesa - e salve as alterações.

O novo idioma (finlandês) agora está disponível na caixa de diálogo de tag das propriedades da página e no **Editar tag** caixa de diálogo ao editar uma tag no **Marcação** console.

>[!NOTE]
>
>O novo idioma precisa ser um dos idiomas reconhecidos pelo AEM, ou seja, precisa estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.
