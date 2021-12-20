---
title: Estrutura de marcação de AEM
seo-title: AEM Tagging Framework
description: Adicionar tags ao conteúdo e aproveitar a infraestrutura de marcação de AEM
seo-description: Tag content and leverage the AEM Tagging infrastructure
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
feature: Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
source-git-commit: 4db9279f2d15f2e08939ba453ae8ddbbc3c3d69f
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 0%

---

# Estrutura de marcação de AEM {#aem-tagging-framework}

Para marcar o conteúdo e aproveitar a infraestrutura de marcação de AEM :

* A tag deve existir como um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)` nos termos do [nó raiz da taxonomia](#taxonomy-root-node)

* O NodeType do nó de conteúdo marcado deve incluir a variável [ `cq:Taggable`](#taggable-content-cq-taggable-mixin) mistura
* O [TagID](#tagid) é adicionado ao nó de conteúdo [ `cq:tags`](#tagged-content-cq-tags-property) e resolve para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tags : cq:Tag Node Type  {#tags-cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

Uma tag pode ser uma palavra simples (por exemplo, céu) ou representar uma taxonomia hierárquica (por exemplo, frutas/maçã, ou seja, tanto o fruto genérico como a maçã mais específica).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem meta informações opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido em interfaces do usuário, em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* o tipo de nó é `cq:Tag`
* o nome do nó é um componente do ` [TagID](#tagid)`
* o ` [TagID](#tagid)` sempre inclui uma [namespace](#tag-namespace)

* opcional `jcr:title` propriedade (o Título a ser exibido na interface do usuário)

* opcional `jcr:description` propriedade

* quando contém nós filho, é referido como um [tag container](#container-tags)
* é armazenado no repositório abaixo de um caminho base chamado [nó raiz da taxonomia](#taxonomy-root-node)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a TagID é uma TagID abreviada que começa com o namespace ou pode ser uma TagID absoluta que começa no [nó raiz da taxonomia](#taxonomy-root-node).

Quando o conteúdo é marcado, se ainda não existir, a variável ` [cq:tags](#tagged-content-cq-tags-property)` é adicionada ao nó content e a TagID é adicionada ao valor da matriz String da propriedade.

A TagID consiste em um [namespace](#tag-namespace) seguido pela TagID local. [Tags do contêiner](#container-tags) têm subtags que representam uma ordem hierárquica na taxonomia. As subtags podem ser usadas para referenciar tags da mesma maneira que qualquer TagID local. Por exemplo, é permitido marcar o conteúdo com &quot;fruta&quot;, mesmo que seja uma tag container com subtags, como &quot;fruta/maçã&quot; e &quot;frutas/banana&quot;.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia deve *not* ser um nó do tipo `  cq   :Tag`.

Em AEM, o caminho base é `/content/  cq   :tags` e o nó raiz é do tipo `  cq   :Folder`.

### Namespace de tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais comum é ter um namespace por site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Ativos, Comunidades), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore da taxonomia, que é o nó imediatamente abaixo do [nó raiz da taxonomia](#taxonomy-root-node). Um namespace é um nó do tipo `cq:Tag` cujo pai não é um `cq:Tag`tipo de nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é TagID `default` (O título é `Standard Tags),`que `/content/cq:tags/default.`

### Tags do contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` contendo qualquer número e tipo de nós filhos, o que possibilita aprimorar o modelo de tags com metadados personalizados.

Além disso, tags de contêiner (ou supertags) em uma taxonomia servem como subsoma de todas as subtags: por exemplo, o conteúdo marcado com frutos/maçã também é considerado marcado com frutos, ou seja, a pesquisa de conteúdo marcado apenas com frutos também encontraria o conteúdo marcado com frutas/maçã.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos &quot;:&quot;, o dois pontos separará o namespace da tag ou da subtaxonomia, que são separadas por barras normais &quot;/&quot;. Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das tags está abaixo de /content/cq:tags.

A tag que faz referência a caminhos ou caminhos não existentes que não apontam para um nó cq:Tag é considerada inválida e é ignorada.

A tabela a seguir mostra algumas TagIDs de exemplo, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório:

A tabela a seguir mostra algumas TagIDs de exemplo, seus elementos e como a TagID é resolvida para um caminho absoluto no repositório :

<table>
 <tbody>
  <tr>
   <td><strong>TagID<br /> </strong></td>
   <td><strong>Namespace</strong></td>
   <td><strong>ID local</strong></td>
   <td><strong>Tags do contêiner</strong></td>
   <td><strong>Tag Folha</strong></td>
   <td><strong>Repositório<br /> Caminho absoluto da tag</strong></td>
  </tr>
  <tr>
   <td>dam:frut/apple/braeburn</td>
   <td>barragem</td>
   <td>fruta/maçã/queimadura</td>
   <td>fruta, maçã</td>
   <td>queimadura</td>
   <td>/content/cq:tags/dam/setor de frutas/apple/braeburn</td>
  </tr>
  <tr>
   <td>cor/vermelho</td>
   <td>default</td>
   <td>cor/vermelho</td>
   <td>cor</td>
   <td>vermelho</td>
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
   <td>dam:</td>
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

Quando a tag inclui a string de título opcional ( `jcr:title`) é possível localizar o título para exibição ao adicionar a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte

* [Tags em diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages) - que descreve o uso das APIs
* [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages) - que descreve o uso do console Marcação

### Controle de acesso {#access-control}

As tags existem como nós no repositório no [nó raiz da taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a conteúdo específico.

Uma prática típica inclui:

* Permitir o `tag-administrators` acesso de gravação de grupo/função para todos os namespaces (adicionar/modificar em `/content/cq:tags`). Este grupo vem com AEM pronto para uso.

* Permitir que usuários/autores leiam o acesso a todos os namespaces que devem ser legíveis a eles (em sua maioria, todos).
* Permitir que usuários/autores gravem acesso aos namespaces, onde as tags devem ser livremente definidas pelos usuários/autores (add_node em `/content/cq:tags/some_namespace`)

## Conteúdo marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem tags a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve incluir o `cq:Taggable` mistura ou o `cq:OwnerTaggable` mistura.

O `cq:OwnerTaggable` mixin, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó . O `cq:OwnerTaggable` a mixin não é exigida pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar tags somente no nó de nível superior de um item de conteúdo agregado (ou em seu nó jcr:content). Os exemplos incluem:
>
>* páginas ( `cq:Page`) em que `jcr:content`o nó é do tipo `cq:PageContent` que inclui `cq:Taggable` mistura.
>
>* ativos ( `cq:Asset`) em que `jcr:content/metadata` o nó sempre tem o `cq:Taggable` mistura.

>


### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação JCR. [here](https://jackrabbit.apache.org/node-type-notation.html).

As definições essenciais para os Tipos de nó incluídos no AEM são as seguintes:

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

O `cq:tags` é uma matriz String usada para armazenar uma ou mais TagIDs quando aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó que é definido com a variável `[cq:Taggable](#taggable-content-cq-taggable-mixin)` mistura.

>[!NOTE]
>
>Para aproveitar AEM funcionalidade de marcação, os aplicativos desenvolvidos e personalizados não devem definir outras propriedades de tag além de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o [Console de marcação](/help/sites-administering/tags.md):

* Quando uma tag A é movida ou unida na tag B em `/content/cq:tags`:

   * A tag A não é excluída e obtém um `cq:movedTo` propriedade.
   * a tag B é criada (no caso de uma movimentação) e obtém um `cq:backlinks` propriedade.

* `cq:movedTo` aponta para a tag B. Essa propriedade significa que a tag A foi movida ou mesclada na tag B. Mover a tag B atualizará essa propriedade de acordo. A tag A fica oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo de tag remove tags como a tag A, uma vez que mais nós de conteúdo apontam para elas.
Um valor especial para a variável `cq:movedTo` a propriedade é `nirvana`: ela é aplicada quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma `cq:movedTo` isso tem de ser mantido.

   >[!NOTE]
   >
   >O `cq:movedTo` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   > 1. A tag é usada no conteúdo (o que significa que tem uma referência) OU
   > 1. A tag tem filhos que já foram movidos.


* `cq:backlinks` mantém as referências na outra direção, ou seja, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B. Isso é necessário principalmente para manter `cq:movedTo`propriedades atualizadas quando a tag B for movida/mesclada/excluída também ou quando a tag B for ativada, nesse caso todas as tags de backlinks também deverão ser ativadas.

   >[!NOTE]
   >
   >O `cq:backlinks` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   >
   > 1. A tag é usada no conteúdo (o que significa que tem uma referência) OU >
   > 1. A tag tem filhos que já foram movidos.


* Ler um `cq:tags` a propriedade de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag é retornada.
   1. Se a tag tiver uma `cq:movedTo` do conjunto de propriedades, a ID da tag referenciada é seguida.
Essa etapa é repetida, desde que a tag seguida tenha uma `cq:movedTo` propriedade.

   1. Se a tag seguida não tiver uma `cq:movedTo` , a tag será lida.

* Para publicar a alteração quando uma tag tiver sido movida ou mesclada, a variável `cq:Tag` nó e todos os seus backlinks devem ser replicados: isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores no `cq:tags` limpa automaticamente as referências &quot;antigas&quot;. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.

>[!NOTE]
>
>O movimento das tags é diferente da migração das tags.

## Migração de tags {#tags-migration}

As tags do Experience Manager 6.4 em diante são armazenadas sob `/content/cq:tags`, que anteriormente estavam armazenadas em `/etc/tags`. No entanto, em cenários em que o Adobe Experience Manager foi atualizado da versão anterior, as tags ainda estão presentes no local antigo `/etc/tags`. Em sistemas atualizados, as tags do precisam ser migradas em `/content/cq:tags`.

>[!NOTE]
>
>Na página Propriedades da página de tags , é recomendável usar a ID da tag (`geometrixx-outdoors:activity/biking`) em vez de codificar o caminho base da tag (por exemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para listar tags, `com.day.cq.tagging.servlets.TagListServlet` pode ser usada.

>[!NOTE]
>
>É recomendável usar a API do gerenciador de tags como recurso.

### Se a instância atualizada do AEM for compatível com a API do TagManager {#upgraded-instance-support-tagmanager-api}

1. No início do componente, a API do TagManager detecta se é uma instância de AEM atualizada. No sistema atualizado, as tags são armazenadas em `/etc/tags`.

1. A API do TagManager é executada no modo de compatibilidade anterior, o que significa que a API usa `/etc/tags` como o caminho base. Caso contrário, ele usará uma nova localização `/content/cq:tags`.

1. Atualize o local das tags.

1. Depois de migrar as tags para o novo local, execute o seguinte script:

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

O script busca todas as tags que têm `/etc/tags` no valor de `cq:movedTo/cq:backLinks` propriedade. Em seguida, ele repete por meio do conjunto de resultados buscados e resolve a variável `cq:movedTo` e `cq:backlinks` valores de propriedade para `/content/cq:tags` caminhos (no caso em que `/etc/tags` é detectado no valor).

### Se a instância de AEM atualizada for executada na interface clássica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>A interface clássica não é compatível com tempo de inatividade zero e não é compatível com o novo caminho de base de tags. Se você quiser usar a interface clássica do que `/etc/tags` precisa ser criada, seguido de `cq-tagging` reinicialização do componente.

No caso de instâncias de AEM atualizadas compatíveis com a API do TagManager e em execução na interface clássica:

1. Uma vez, referências ao caminho base da tag antiga `/etc/tags` são substituídos por tagId ou nova localização de tag `/content/cq:tags`, você pode migrar tags para o novo local `/content/cq:tags` no CRX, seguido pela reinicialização do componente.

1. Depois de migrar as tags para o novo local, execute o script acima mencionado.
