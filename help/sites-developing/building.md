---
title: Criação de tags em um aplicativo AEM
seo-title: Criação de tags em um aplicativo AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
seo-description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 1493b301ecf4c25f785495e11ead352de600ddb7
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Criação de tags em um aplicativo AEM{#building-tagging-into-an-aem-application}

Para a finalidade de trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado, esta página descreve o uso da variável

* [API de marcação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](/help/sites-developing/framework.md)

Para obter informações relacionadas à marcação, consulte :

* [Administração de tags](/help/sites-administering/tags.md) para obter informações sobre como criar e gerenciar tags, bem como sobre quais tags de conteúdo foram aplicadas.
* [Usar tags](/help/sites-authoring/tags.md) para obter informações sobre como marcar conteúdo.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A implementação da estrutura [de](/help/sites-developing/framework.md) marcação no AEM permite o gerenciamento de tags e do conteúdo de tags usando a API JCR. O TagManager garante que as tags inseridas como valores na propriedade da matriz de `cq:tags` string não sejam duplicadas, ele remove TagIDs apontando para tags não existentes e atualiza TagIDs para tags movidas ou unidas. O TagManager usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no pacote [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory - retorna uma implementação baseada em JCR de uma `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar tags por caminhos e nomes.
* `Tag` - define o objeto de tag.

### Obtendo um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância do TagManager, é necessário ter um JCR `Session` e chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, você também pode se adaptar a um `TagManager` dos `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Como recuperar um objeto de tag {#retrieving-a-tag-object}

Uma tag `Tag` pode ser recuperada pelo `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` para JCR `Nodes`, você pode usar diretamente o `adaptTo` mecanismo do Sling se tiver o recurso (por exemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Enquanto uma tag só pode ser convertida *de *um recurso (não um nó), uma tag pode ser convertida *para *tanto um nó quanto um recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Não é possível adaptar diretamente de `Node` para, porque `Tag` não implementa o `Node` `Adaptable.adaptTo(Class)` método Sling.

### Obtendo e configurando tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Pesquisando por tags {#searching-for-tags}

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
>O uso válido `RangeIterator` é:
>
>`com.day.cq.commons.RangeIterator`

### Excluindo tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação ( `Replicator`) com tags, pois elas são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Marcação no lado do cliente {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` é um widget de formulário para inserir tags. Ele tem um menu pop-up para seleção de tags existentes, inclui o preenchimento automático e muitos outros recursos. Seu xtype é `tags`.

## O Coletor de Lixo da Etiqueta {#the-tag-garbage-collector}

O coletor de lixo de tags é um serviço em segundo plano que limpa as tags que estão ocultas e não são usadas. As tags ocultas e não usadas são tags abaixo `/content/cq:tags` que têm uma `cq:movedTo` propriedade e não são usadas em um nó de conteúdo - elas têm uma contagem zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, a `cq:tags` propriedade) não precisa ser atualizado como parte da operação de movimentação ou mesclagem. As referências na `cq:tags` propriedade são automaticamente atualizadas quando a `cq:tags` propriedade é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Pesquisa de tags e Lista de tags {#tag-search-and-tag-listing}

A pesquisa por tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por TagID pesquisa as tags que têm a propriedade `cq:movedTo` definida como TagID e segue pelas `cq:movedTo` TagIDs.

* A pesquisa por Título da tag pesquisa somente as tags que não possuem uma `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Conforme descrito na documentação para administração de tags, na seção [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), uma tag `title`pode ser definida em idiomas diferentes. Uma propriedade sensível ao idioma é então adicionada ao nó da tag. Esta propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma sequência de caracteres de localidade ISO em minúsculas e usar &quot;_&quot; em vez de &quot;-&quot;, por exemplo: `de_ch`.

Quando a tag **Animais** é adicionada à página **Produtos** , o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó /content/geometrixx/en/products/jcr:content. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor tem métodos localizados `title`relacionados:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitle()
   * getTitle(localidade local)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, localidade local)
   * createTagByTitle(String tagTitlePath, localidade local)
   * resolveByTitle(String tagTitlePath, localidade local)

No AEM, o idioma pode ser obtido do idioma da página ou do idioma do usuário:

* para recuperar o idioma da página em um JSP:

   * `currentPage.getLanguage(false)`

* para recuperar o idioma do usuário em um JSP:

   * `slingRequest.getLocale()`

`currentPage` e `slingRequest` estão disponíveis em um JSP por meio da tag [&lt;cq:definedObjects>](/help/sites-developing/taglib.md) .

Para marcação, a localização depende do contexto, já que a tag `titles`pode ser exibida no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (finlandês) à caixa de diálogo Editar **** tag:

1. No **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.

1. Adicione `fi_fi` - que representa a localidade finlandesa - e salve as alterações.

O novo idioma (finlandês) agora está disponível na caixa de diálogo de tags das propriedades da página e na caixa de diálogo **Editar tag** ao editar uma tag no console **Marcação** .

>[!NOTE]
>
>O novo idioma precisa ser um dos idiomas reconhecidos pelo AEM, ou seja, precisa estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.

