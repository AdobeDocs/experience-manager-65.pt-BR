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
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 0%

---

# Estrutura de marcação do AEM {#aem-tagging-framework}

Para marcar conteúdo e usar a infraestrutura de marcação AEM:

* A tag deve existir como um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)` no [nó raiz de taxonomia](#taxonomy-root-node)

* O NodeType do nó de conteúdo marcado deve incluir o [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin
* A variável [TagID](#tagid) é adicionado ao do nó de conteúdo [`cq:tags`](#tagged-content-cq-tags-property) propriedade e é resolvido para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tags : cq:Tag Node Type  {#tags-cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

Uma tag pode ser uma palavra simples (por exemplo, céu) ou representar uma taxonomia hierárquica (por exemplo, fruta/maçã, o que significa tanto a fruta genérica quanto a maçã mais específica).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário, em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* o tipo de nó é `cq:Tag`
* o nome do nó é um componente da ` [TagID](#tagid)`
* o ` [TagID](#tagid)` sempre inclui um [namespace](#tag-namespace)

* opcional `jcr:title` (o Título a ser exibido na interface do usuário)

* opcional `jcr:description` propriedade

* ao conter nós filhos, é chamado de [tag container](#container-tags)
* é armazenado no repositório abaixo de um caminho base chamado de [nó raiz de taxonomia](#taxonomy-root-node)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a TagID é uma TagID abreviada que começa com o namespace ou pode ser uma TagID absoluta que começa com o [nó raiz de taxonomia](#taxonomy-root-node).

Quando o conteúdo for marcado, se ainda não existir, a variável ` [cq:tags](#tagged-content-cq-tags-property)` A propriedade é adicionada ao nó de conteúdo e o TagID é adicionado ao valor da matriz String da propriedade.

A TagID consiste em um [namespace](#tag-namespace) seguido pela TagID local. [Tags de contêiner](#container-tags) ter subtags que representam uma ordem hierárquica na taxonomia. Subtags podem ser usadas para fazer referência a tags como qualquer TagID local. Por exemplo, marcar o conteúdo com &quot;fruta&quot; é permitido, mesmo se for uma tag container com subtags, como &quot;fruta/maçã&quot; e &quot;fruta/banana&quot;.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia deve *não* ser um nó do tipo `  cq   :Tag`.

No AEM, o caminho base é `/content/  cq   :tags` e o nó raiz é do tipo `  cq   :Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais comum é ter um namespace por (site) site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Ativos, Comunidades), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo de [nó raiz de taxonomia](#taxonomy-root-node). Um namespace é um nó do tipo `cq:Tag` cujo pai não é um `cq:Tag`tipo de nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é TagID `default` (O título é `Standard Tags),`que é `/content/cq:tags/default.`

### Tags de contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós secundários, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, as tags container (ou supertags) em uma taxonomia servem como a soma de todas as subtags. Por exemplo, o conteúdo marcado com fruta/maçã também é considerado marcado com fruta. Ou seja, a pesquisa de conteúdo marcado com fruta também localizaria o conteúdo marcado com fruta/maçã.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos &quot;:&quot;, os dois pontos separam o namespace da tag ou subtaxonomia, que são então separadas por barras normais &quot;/&quot;. Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das tags é abaixo de /content/cq:tags.

A marca que faz referência a caminhos ou caminhos não existentes que não apontam para um nó cq:Tag é considerada inválida e é ignorada.

A tabela a seguir mostra algumas amostras de TagIDs, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

A tabela a seguir mostra algumas amostras de TagIDs, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

<table>
 <tbody>
  <tr>
   <td><strong>TagID<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Tags de contêiner</strong></td>
   <td><strong>Tag de folha</strong></td>
   <td><strong>Repositório<br /> Caminho absoluto da tag</strong></td>
  </tr>
  <tr>
   <td>represa:fruta/maçã/queimadura</td>
   <td>dam</td>
   <td>fruta/maçã/queimadura</td>
   <td>fruta, maçã</td>
   <td>braeburn</td>
   <td>/content/cq:tags/dam/fruit/apple/braeburn</td>
  </tr>
  <tr>
   <td>color/red</td>
   <td>default</td>
   <td>color/red</td>
   <td>cor</td>
   <td>vermelho</td>
   <td>/content/cq:tags/default/color/red</td>
  </tr>
  <tr>
   <td>céu</td>
   <td>default</td>
   <td>céu</td>
   <td>(nenhuma)</td>
   <td>céu</td>
   <td>/content/cq:tags/default/sky</td>
  </tr>
  <tr>
   <td>dam:</td>
   <td>dam</td>
   <td>(nenhuma)</td>
   <td>(nenhuma)</td>
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

Quando a tag inclui a string de título opcional ( `jcr:title`) é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte

* [Tags em diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages) - que descreve o uso das APIs
* [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) - que descreve o uso do console de marcação

### Controle de acesso {#access-control}

As tags existem como nós no repositório, na variável [nó raiz de taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controla a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo que o `tag-administrators` acesso de gravação de grupo/função a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Esse grupo vem com AEM pronto para uso.

* Permitir que usuários/autores leiam todos os namespaces que devem ser legíveis para eles (principalmente todos).
* Permitir que usuários/autores gravem acesso aos namespaces em que as tags devem ser definidas livremente por usuários/autores (add_node em `/content/cq:tags/some_namespace`)

## Conteúdo Marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) devem incluir a `cq:Taggable` mixin ou o `cq:OwnerTaggable` mixin.

A variável `cq:OwnerTaggable` mixin, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó. A variável `cq:OwnerTaggable` O mixin não é exigido pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar tags somente no nó de nível superior de um item de conteúdo agregado (ou em seu nó jcr:content). Os exemplos incluem:
>
>* páginas ( `cq:Page`) em que o `jcr:content`o nó é do tipo `cq:PageContent` que inclui a `cq:Taggable` mixin.
>
>* ativos ( `cq:Asset`) em que o `jcr:content/metadata` o nó sempre tem o `cq:Taggable` mixin.
>

### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação do JCR [aqui](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

A variável `cq:tags` A propriedade é uma matriz de cadeia de caracteres usada para armazenar uma ou mais TagIDs quando são aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com o `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin.

>[!NOTE]
>
>Para usar a funcionalidade de marcação AEM, os aplicativos desenvolvidos de forma personalizada não devem definir propriedades de tag diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o [Console de marcação](/help/sites-administering/tags.md):

* Quando uma tag A é movida ou mesclada na tag B em `/content/cq:tags`:

   * A tag A não é excluída e obtém um `cq:movedTo` propriedade.
   * A tag B é criada (se houver uma movimentação) e obtém um `cq:backlinks` propriedade.

* `cq:movedTo` aponta para a tag B. Essa propriedade significa que a tag A foi movida ou mesclada na tag B. Mover a tag B atualiza essa propriedade de acordo. A tag A fica oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo da tag remove tags como a tag A assim que os nós de conteúdo não apontam mais para elas.
Um valor especial para o `cq:movedTo` propriedade é `nirvana`: é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma `cq:movedTo` que deve ser mantido.

  >[!NOTE]
  >
  >A variável `cq:movedTo` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
  >
  >1. A tag é usada no conteúdo (o que significa que tem uma referência) OU
  >1. A tag tem filhos que já foram movidos.

* `cq:backlinks` mantém as referências na outra direção. Ou seja, ela mantém uma lista de todas as tags que foram movidas ou mescladas com a tag B. Isso é necessário principalmente para manter `cq:movedTo`propriedades atualizadas quando a tag B é movida/mesclada/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

  >[!NOTE]
  >
  >A variável `cq:backlinks` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
  >
  >1. A tag é usada no conteúdo (o que significa que tem uma referência) OU
  >1. A tag tem filhos que já foram movidos.

* Ler um `cq:tags` propriedade de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag é retornada.
   1. Se a tag tiver uma `cq:movedTo` for definida, a ID da tag referenciada será seguida.
Esta etapa é repetida desde que a tag seguida tenha uma `cq:movedTo` propriedade.

   1. Se a tag seguida não tiver um `cq:movedTo` propriedade, a tag será lida.

* Para publicar a alteração quando uma tag tiver sido movida ou mesclada, a variável `cq:Tag` o nó e todos os seus backlinks devem ser replicados: isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores no da página `cq:tags` automaticamente as referências &quot;antigas&quot;. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.

>[!NOTE]
>
>O movimento de tags é diferente da migração de tags.

## Migração de tags {#tags-migration}

As tags do Experience Manager 6.4 em diante são armazenadas em `/content/cq:tags`, que foram armazenados anteriormente no `/etc/tags`. No entanto, em cenários em que o Adobe Experience Manager foi atualizado da versão anterior, as tags ainda estão presentes no local antigo `/etc/tags`. Em sistemas atualizados, as tags devem ser migradas em `/content/cq:tags`.

>[!NOTE]
>
>Na página Propriedades da página de tags, é recomendável usar a ID da tag (`geometrixx-outdoors:activity/biking`) em vez de codificar o caminho base da tag (por exemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para listar tags, `com.day.cq.tagging.servlets.TagListServlet` pode ser usado.

>[!NOTE]
>
>É recomendável usar a API do gerenciador de tags como recurso.

### Se a instância do AEM atualizada suportar a API do TagManager {#upgraded-instance-support-tagmanager-api}

1. No início do componente, a API do TagManager detecta se é uma instância de AEM atualizada. No sistema atualizado, as tags são armazenadas em `/etc/tags`.

1. A API do TagManager é executada no modo de compatibilidade com versões anteriores, o que significa que a API usa `/etc/tags` como o caminho base. Caso contrário, ele usará um novo local `/content/cq:tags`.

1. Atualize o local das tags.

1. Depois de migrar as tags para o novo local, execute o script a seguir:

```java
import org.apache.sling.api.resource.*
import javax.jcr.*

ResourceResolverFactory resourceResolverFactory = osgi.getService(ResourceResolverFactory.class);
ResourceResolver resolver = resourceResolverFactory.getAdministrativeResourceResolver(null);
Session session = resolver.adaptTo(Session.class);

def queryManager = session.workspace.queryManager;
def statement = "/jcr:root/content/cq:tags//element(*, cq:Tag)[jcr:contains(@cq:movedTo,\'/etc/tags\') or jcr:contains(@cq:backlinks,\'/etc/tags\')]";
def query = queryManager.createQuery(statement, "xpath");

println "query = ${query.statement}\n";

def tags = query.execute().getNodes();


tags.each { node ->
  def tagPath = node.path;
  println "tag = ${tagPath}";

  if(node.hasProperty("cq:movedTo") && node.getProperty("cq:movedTo").getValue().toString().startsWith("/etc/tags"))
    {
     def movedTo = node.getProperty("cq:movedTo").getValue().toString();

     println "cq:movedTo = ${movedTo} \n";

     movedTo = movedTo.replace("/etc/tags","/content/cq:tags");
     node.setProperty("cq:movedTo",movedTo);
     } else if(node.hasProperty("cq:backlinks")){

     String[] backLinks = node.getProperty("cq:backlinks").getValues();
     int count = 0;

     backLinks.each { value ->
             if(value.startsWith("/etc/tags")){
                     println "cq:backlinks = ${value}\n";
                     backLinks[count] = value.replace("/etc/tags","/content/cq:tags");
    }
             count++;
     }

    node.setProperty("cq:backlinks",backLinks);
  }
}
session.save();

println "---------------------------------Success-------------------------------------"
```

O script busca todas as tags que têm `/etc/tags` no valor de `cq:movedTo/cq:backLinks` propriedade. Em seguida, ele repete o conjunto de resultados obtido e resolve o `cq:movedTo` e `cq:backlinks` valores de propriedade para `/content/cq:tags` caminhos (no caso em que `/etc/tags` é detectado no valor ).

### Se a instância do AEM atualizada for executada na interface clássica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>A interface clássica não é compatível com tempo de inatividade zero e não é compatível com o novo caminho de base de tags. Se quiser usar a interface clássica, `/etc/tags` deve ser criado seguido por `cq-tagging` reinicialização do componente.

Se houver instâncias de AEM atualizadas com suporte pela API TagManager e em execução na interface clássica:

1. Uma vez faz referência ao antigo caminho de base da tag `/etc/tags` são substituídos por tagId ou novo local da tag `/content/cq:tags`, é possível migrar tags para o novo local `/content/cq:tags` no CRX seguido pela reinicialização do componente.

1. Depois de migrar as tags para o novo local, execute o script mencionado acima.
