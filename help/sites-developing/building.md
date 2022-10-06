---
title: Criação de tags em um aplicativo AEM
seo-title: Building Tagging into an AEM Application
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado
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

Para a finalidade de trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado, esta página descreve o uso da variável

* [API de marcação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](/help/sites-developing/framework.md)

Para obter informações relacionadas à marcação, consulte :

* [Administração de tags](/help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags, bem como sobre quais tags de conteúdo foram aplicadas.
* [Uso de tags](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A aplicação do [estrutura de marcação](/help/sites-developing/framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR . O TagManager garante que as tags sejam inseridas como valores na variável `cq:tags` a propriedade da matriz da sequência de caracteres não está duplicada, ela remove TagIDs apontando para tags não existentes e atualiza TagIDs para tags movidas ou mescladas. O TagManager usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) pacote:

* JcrTagManagerFactory - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar tags por caminhos e nomes.
* `Tag` - define o objeto da tag.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância do TagManager, você precisa ter um JCR `Session` e para chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto típico do Sling, você também pode se adaptar a um `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

A `Tag` podem ser recuperadas por meio do `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` no JCR `Nodes`, você pode usar diretamente o Sling `adaptTo` mecanismo se você tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma tag possa ser convertida apenas *de *um recurso (não um nó), uma tag pode ser convertida *para *tanto um nó quanto um recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptação direta de `Node` para `Tag` não é possível, porque `Node` não implementa o Sling `Adaptable.adaptTo(Class)` método .

### Obter e definir tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Pesquisar por tags {#searching-for-tags}

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
>O `RangeIterator` para usar é:
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

`CQ.tagging.TagInputField` é um widget de formulário para inserir tags. Ele tem um menu pop-up para selecionar entre tags existentes, inclui o preenchimento automático e muitos outros recursos. Seu xtype é `tags`.

## O Coletor de lixo de tags {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não utilizadas. Tags ocultas e não usadas são tags abaixo `/content/cq:tags` que tenham uma `cq:movedTo` e não são usados em um nó de conteúdo - eles têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, o `cq:tags` ) não precisa ser atualizada como parte da operação de movimentação ou mesclagem. As referências no `cq:tags` são atualizadas automaticamente quando a variável `cq:tags` for atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Pesquisa de tags e Lista de tags {#tag-search-and-tag-listing}

A pesquisa por tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por TagID pesquisa as tags que têm a propriedade `cq:movedTo` definido como TagID e segue por meio do `cq:movedTo` TagIDs.

* A pesquisa por Título da tag pesquisa somente as tags que não têm uma `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Conforme descrito na documentação para administração de tags, na seção [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), uma tag `title`pode ser definido em idiomas diferentes. Uma propriedade sensível ao idioma é então adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma sequência de caracteres de localidade ISO em letras minúsculas e usar &quot;_&quot; em vez de &quot;-&quot;, por exemplo: `de_ch`.

Quando a variável **Animais** é adicionada à variável **Produtos** página, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó /content/geometrixx/en/products/jcr:content. A tradução é referenciada a partir do nó da tag .

A API do lado do servidor foi localizada `title`-métodos relacionados:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedtitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

No AEM, o idioma pode ser obtido no idioma da página ou no idioma do usuário:

* para recuperar o idioma da página em um JSP:

   * `currentPage.getLanguage(false)`

* para recuperar o idioma do usuário em um JSP:

   * `slingRequest.getLocale()`

`currentPage` e `slingRequest` estão disponíveis em um JSP por meio do [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) .

Para marcação, a localização depende do contexto como tag `titles`pode ser exibido no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (finlandês) ao **Editar tag** caixa de diálogo:

1. Em **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.

1. Adicionar `fi_fi` - que representa a localidade finlandesa - e salve as alterações.

O novo idioma (finlandês) agora está disponível na caixa de diálogo de tags das propriedades da página e no **Editar tag** ao editar uma tag no **Marcação** console.

>[!NOTE]
>
>O novo idioma precisa ser um dos idiomas reconhecidos AEM, ou seja, precisa estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.
