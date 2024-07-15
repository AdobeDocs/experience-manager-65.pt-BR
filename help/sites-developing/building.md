---
title: Criação de tags em um aplicativo AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Developing,Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Criação de tags em um aplicativo AEM{#building-tagging-into-an-aem-application}

Para trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado, esta página descreve o uso da variável

* [API de marcação](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

Que interage com o

* [Estrutura de marcação](/help/sites-developing/framework.md)

Para obter informações relacionadas à marcação, consulte:

* [Administrando Tags](/help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags e às quais as tags de conteúdo foram aplicadas.
* [Usando Marcas](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A implementação da [estrutura de marcação](/help/sites-developing/framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. O TagManager garante que as marcas inseridas como valores na propriedade de matriz da cadeia de caracteres `cq:tags` não sejam duplicadas, ele remove TagIDs que apontam para marcas não existentes e atualiza TagIDs para marcas movidas ou mescladas. O TagManager usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no pacote [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* JcrTagManagerFactory - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar marcas por caminhos e nomes.
* `Tag` - define o objeto de marca.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância do TagManager, você deve ter um JCR `Session` e chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, você também pode adaptar a um `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

Um `Tag` pode ser recuperado por meio de `TagManager`, resolvendo uma marca existente ou criando uma:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` para JCR `Nodes`, você pode usar diretamente o mecanismo `adaptTo` do Sling se tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

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
>Adaptar diretamente de `Node` a `Tag` não é possível, porque `Node` não implementa o método Sling `Adaptable.adaptTo(Class)`.

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
>O `RangeIterator` válido a ser usado é:
>
>`com.day.cq.commons.RangeIterator`

### Exclusão de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação ( `Replicator`) com marcas porque as marcas são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Marcação no lado do cliente {#tagging-on-the-client-side}

O widget de formulário `CQ.tagging.TagInputField` serve para inserir marcas. Ele tem um menu pop-up para seleção entre tags existentes, inclui preenchimento automático e muitos outros recursos. Seu xtype é `tags`.

## O coletor de lixo da tag {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não usadas. Marcas ocultas e não usadas são marcas abaixo de `/content/cq:tags` que têm uma propriedade `cq:movedTo` e não são usadas em um nó de conteúdo - elas têm uma contagem igual a zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, a propriedade `cq:tags`) não precisa ser atualizado como parte da operação de movimentação ou mesclagem. As referências na propriedade `cq:tags` são atualizadas automaticamente quando a propriedade `cq:tags` é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Você pode configurá-lo em:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Pesquisa de tags e listagem de tags {#tag-search-and-tag-listing}

A pesquisa de tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por TagID pesquisa as tags que têm a propriedade `cq:movedTo` definida como TagID e segue pelas TagIDs `cq:movedTo`.

* A pesquisa por Título de marca somente pesquisa as marcas que não têm a propriedade `cq:movedTo`.

## Tags em diferentes idiomas {#tags-in-different-languages}

Conforme descrito na documentação para administração de tags, na seção [Gerenciamento de Tags em Diferentes Idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), uma tag `title` pode ser definida em diferentes idiomas. Em seguida, uma propriedade que diferencia idiomas é adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` para a tradução em francês. O `<locale>` deve ser uma cadeia de caracteres de localidade ISO em minúsculas e usar &quot;_&quot; em vez de &quot;-&quot;, por exemplo: `de_ch`.

Quando a marca **Animais** é adicionada à página **Produtos**, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó /content/geometrixx/en/products/jcr:content. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor localizou métodos relacionados a `title`:

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Localidade)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Local)
   * getTitlePath(Localidade)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, localidade)
   * createTagByTitle(String tagTitlePath, localidade)
   * resolveByTitle(String tagTitlePath, localidade)

No AEM, o idioma pode ser obtido no idioma da página ou no idioma do usuário:

* para recuperar o idioma da página em uma JSP:

   * `currentPage.getLanguage(false)`

* para recuperar o idioma do usuário em uma JSP:

   * `slingRequest.getLocale()`

O `currentPage` e o `slingRequest` estão disponíveis em um JSP por meio da marca [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Para marcação, a localização depende do contexto, pois a marca `titles` pode ser exibida no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um idioma (finlandês) à caixa de diálogo **Editar tag**:

1. No **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.

1. Adicione `fi_fi` - que representa a localidade finlandesa - e salve as alterações.

O novo idioma (finlandês) agora está disponível na caixa de diálogo de marca das propriedades da página e na caixa de diálogo **Editar marca** ao editar uma marca no console **Marcação**.

>[!NOTE]
>
>A nova língua deve ser uma das línguas reconhecidas pelo AEM. Ou seja, ele deve estar disponível como um nó abaixo de `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>A instalação de conteúdo pronto para uso relacionado à marcação por meio de um pacote de atualização oficial (incluindo Service Packs, Service Packs de Segurança, Extended Feature Packs, Cumulative Feature Packs, patches e outros) redefine a propriedade de idiomas do nó `/content/cq:tags` para o padrão. Portanto, é necessário adicioná-lo das propriedades antes da instalação.
