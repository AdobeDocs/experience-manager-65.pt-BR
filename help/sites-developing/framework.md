---
title: Estrutura de marcação AEM
seo-title: Estrutura de marcação AEM
description: Adicione tags ao conteúdo e aproveite a infraestrutura de Marcação de AEM
seo-description: Adicione tags ao conteúdo e aproveite a infraestrutura de Marcação de AEM
uuid: f80a2cb1-359f-41dd-a70b-626d92cc3d4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f69db472-9f5c-4c0d-9292-2920ef69feeb
docset: aem65
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 0%

---


# Estrutura de marcação AEM {#aem-tagging-framework}

Para marcar o conteúdo e aproveitar a infraestrutura de Marcação de AEM:

* A tag deve existir como um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)` no nó raiz de [taxonomia](#taxonomy-root-node)

* O NodeType do nó de conteúdo marcado deve incluir a combinação [ `cq:Taggable`](#taggable-content-cq-taggable-mixin)
* O [TagID](#tagid) é adicionado à propriedade [ `cq:tags`](#tagged-content-cq-tags-property) do nó de conteúdo e resolve-se para um nó do tipo ` [cq:Tag](#tags-cq-tag-node-type)`

## Tags: cq:Tipo de nó de tag {#tags-cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

Uma marca pode ser uma palavra simples (por exemplo, o céu) ou representar uma taxonomia hierárquica (por exemplo, fruta/maçã, ou seja, tanto o fruto genérico como a maçã mais específica).

As tags são identificadas por uma TagID exclusiva.

Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário em vez da TagID, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* o tipo de nó é `cq:Tag`
* o nome do nó é um componente de ` [TagID](#tagid)`
* o ` [TagID](#tagid)` sempre inclui uma [namespace](#tag-namespace)

* propriedade opcional `jcr:title` (o Título a ser exibido na interface do usuário)

* propriedade opcional `jcr:description`

* ao conter nós filho, é chamado de [tag de container](#container-tags)
* é armazenado no repositório abaixo de um caminho base chamado [nó raiz de taxonomia](#taxonomy-root-node)

### TagID {#tagid}

Uma TagID identifica um caminho que é resolvido para um nó de tag no repositório.

Geralmente, a TagID é uma TagID abreviada que começa com a namespace ou pode ser uma TagID absoluta que começa no nó raiz de [taxonomia](#taxonomy-root-node).

Quando o conteúdo é marcado, se ainda não existir, a propriedade ` [cq:tags](#tagged-content-cq-tags-property)` é adicionada ao nó de conteúdo e a TagID é adicionada ao valor da matriz String da propriedade.

A TagID consiste em uma [namespace](#tag-namespace) seguida pela TagID local. [Container ](#container-tags) tagshave subtags que representam uma ordem hierárquica na taxonomia. As subtags podem ser usadas para referenciar tags como qualquer TagID local. Por exemplo, é permitida a marcação do conteúdo com &quot;fruta&quot;, mesmo que se trate de uma etiqueta de container com sub-marcas, como &quot;fruta/maçã&quot; e &quot;fruta/banana&quot;.

### Nó raiz de taxonomia {#taxonomy-root-node}

O nó raiz de taxonomia é o caminho base para todas as tags no repositório. O nó raiz de taxonomia deve *e não* ser um nó do tipo `  cq   :Tag`.

No AEM, o caminho base é `/content/  cq   :tags` e o nó raiz é do tipo `  cq   :Folder`.

### Namespace de tags {#tag-namespace}

Namespaces permitem agrupar itens. O caso de uso mais comum é ter uma namespace por site (web)site (por exemplo, público, interno e portal) ou por aplicativo maior (por exemplo, WCM, Ativos, Comunidades), mas as namespaces podem ser usadas para várias outras necessidades. As namespaces são usadas na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de determinada namespace) que se aplica ao conteúdo atual.

A namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo do [nó raiz de taxonomia](#taxonomy-root-node). Uma namespace é um nó do tipo `cq:Tag` cujo pai não é um tipo de nó `cq:Tag`.

Todas as tags têm uma namespace. Se nenhuma namespace for especificada, a tag será atribuída à namespace padrão, que é TagID `default` (o Título é `Standard Tags),`que é `/content/cq:tags/default.`

### Tags de container {#container-tags}

Uma tag de container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós secundários, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, as tags de container (ou super tags) em uma taxonomia servem como subsoma de todas as subtags: por exemplo, considera-se que o conteúdo marcado com frutas/maçãs também é marcado com frutos, ou seja, procurar por conteúdo marcado apenas com frutos também encontraria o conteúdo marcado com frutas/maçã.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos &quot;:&quot;, o dois pontos separará a namespace da tag ou subtaxonomia, que são então separados por barras normais &quot;/&quot;. Se a ID da tag não tiver dois pontos, a namespace padrão será implícita.

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
   <td><strong>Tags de container</strong></td>
   <td><strong>Marca Folha</strong></td>
   <td><strong>Repositório<br /> Caminho absoluto da tag</strong></td>
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
   <td>(nenhum, a namespace)</td>
   <td>/content/cq:tags/dam</td>
  </tr>
  <tr>
   <td>/content/cq:tags/categoria/car</td>
   <td>categoria</td>
   <td>carro</td>
   <td>carro</td>
   <td>carro</td>
   <td>/content/cq:tags/categoria/car</td>
  </tr>
 </tbody>
</table>

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional ( `jcr:title`), é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte

* [Tags em diferentes idiomas](/help/sites-developing/building.md#tags-in-different-languages)  - que descreve o uso das APIs
* [Gerenciamento de tags em diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages)  - que descreve o uso do console Marcação

### Controle de acesso {#access-control}

As tags existem como nós no repositório sob o nó raiz de [taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em uma determinada namespace pode ser alcançado ao configurar ACLs apropriadas no repositório.

Além disso, negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo o acesso de gravação de `tag-administrators` grupo/função a todas as namespaces (adicione/modifique em `/content/cq:tags`). Este grupo vem com AEM prontos.

* Permitir que usuários/autores leiam acesso a todas as namespaces que deveriam ser legíveis para eles (na maioria das vezes, todas).
* Permitir que usuários/autores gravem acesso às namespaces nas quais as tags devem ser definidas livremente pelos usuários/autores (add_node em `/content/cq:tags/some_namespace`)

## Conteúdo marcável: cq:Mistura marcável {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve incluir a combinação `cq:Taggable` ou `cq:OwnerTaggable`.

A combinação `cq:OwnerTaggable`, que herda de `cq:Taggable`, serve para indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do nó `cq:PageContent`. A combinação `cq:OwnerTaggable` não é exigida pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar somente tags no nó de nível superior de um item de conteúdo agregado (ou em seu nó jcr:content). Os exemplos incluem:
>
>* páginas ( `cq:Page`) onde o nó `jcr:content`é do tipo `cq:PageContent` que inclui a combinação `cq:Taggable`.
   >
   >
* ativos ( `cq:Asset`) em que o nó `jcr:content/metadata` sempre tem a combinação `cq:Taggable`.

>



### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação JCR [here](https://jackrabbit.apache.org/node-type-notation.html).

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

A propriedade `cq:tags` é uma matriz String usada para armazenar uma ou mais TagIDs quando são aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com a combinação `[cq:Taggable](#taggable-content-cq-taggable-mixin)`.

>[!NOTE]
>
>Para aproveitar AEM funcionalidade de marcação, os aplicativos desenvolvidos personalizados não devem definir propriedades de tags diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

A seguir está uma descrição dos efeitos no repositório ao mover ou unir tags usando o [console de marcação](/help/sites-administering/tags.md):

* Quando uma tag A é movida ou unida na tag B sob `/content/cq:tags`:

   * a tag A não é excluída e obtém uma propriedade `cq:movedTo`.
   * a tag B é criada (no caso de uma movimentação) e obtém uma propriedade `cq:backlinks`.

* `cq:movedTo` aponta para a tag B. Essa propriedade significa que a tag A foi movida ou mesclada para a tag B. Mover a tag B atualizará essa propriedade de acordo. A tag A fica então oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A. O coletor de lixo de tags remove tags como a tag A, uma vez que nenhum nó de conteúdo aponta para elas.
Um valor especial para a propriedade `cq:movedTo` é `nirvana`: ela é aplicada quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com `cq:movedTo` que devem ser mantidas.

   >[!NOTE]
   >
   >A propriedade `cq:movedTo` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência) OU
   > 1. A tag tem filhos que já foram movidos.


* `cq:backlinks` mantém as referências na outra direção, isto é, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B. Isso é necessário principalmente para manter  `cq:movedTo`as propriedades atualizadas quando a tag B também é movida/unida/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

   >[!NOTE]
   >
   >A propriedade `cq:backlinks` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
   >
   > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência) OU    >
   > 1. A tag tem filhos que já foram movidos.


* A leitura de uma propriedade `cq:tags` de um nó de conteúdo envolve a seguinte resolução:

   1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag será retornada.
   1. Se a tag tiver uma propriedade `cq:movedTo` definida, a ID da tag referenciada será seguida.
Essa etapa é repetida, contanto que a tag seguida tenha uma propriedade `cq:movedTo`.

   1. Se a tag seguida não tiver uma propriedade `cq:movedTo`, a tag será lida.

* Para publicar a alteração quando uma tag tiver sido movida ou unida, o nó `cq:Tag` e todos os seus backlinks devem ser replicados: isso é feito automaticamente quando a tag é ativada no console de administração de tags.

* Atualizações posteriores para a propriedade `cq:tags` da página limpam automaticamente as referências &quot;antigas&quot;. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo assim a ID da tag de destino.

>[!NOTE]
>
>O movimento das tags é diferente da migração das tags.

## Migração de tags {#tags-migration}

As tags a partir de Experience Manager 6.4 são armazenadas em `/content/cq:tags`, que foram armazenadas anteriormente em `/etc/tags`. No entanto, em cenários em que o Adobe Experience Manager foi atualizado da versão anterior, as tags ainda estão presentes no local antigo `/etc/tags`. Em sistemas atualizados, as tags precisam ser migradas em `/content/cq:tags`.

>[!NOTE]
>
>Na página Propriedades da página de tags, recomenda-se usar a ID da tag (`geometrixx-outdoors:activity/biking`) em vez de codificar o caminho da base da tag (por exemplo, `/etc/tags/geometrixx-outdoors/activity/biking`).
>
>Para lista de tags, `com.day.cq.tagging.servlets.TagListServlet` pode ser usado.

>[!NOTE]
>
>Recomenda-se usar a API do gerenciador de tags como recurso.

### Se a instância AEM atualizada suportar TagManager API {#upgraded-instance-support-tagmanager-api}

1. No start do componente, a API do TagManager detecta se é uma instância AEM atualizada. No sistema atualizado, as tags são armazenadas em `/etc/tags`.

1. A API do TagManager é executada no modo de compatibilidade com versões anteriores, o que significa que a API usa `/etc/tags` como caminho base. Caso contrário, ele usa a nova localização `/content/cq:tags`.

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

O script obtém todas as tags que têm `/etc/tags` no valor da propriedade `cq:movedTo/cq:backLinks`. Em seguida, ele repete pelo conjunto de resultados obtidos e resolve os valores das propriedades `cq:movedTo` e `cq:backlinks` para os caminhos `/content/cq:tags` (no caso em que `/etc/tags` é detectado no valor).

### Se a instância AEM atualizada for executada na interface clássica {#upgraded-instance-runs-classic-ui}

>[!NOTE]
>
>A interface clássica não é compatível com zero tempo de inatividade e não oferece suporte para o novo caminho de base de tags. Se você deseja usar a interface clássica que `/etc/tags` precisa ser criada, seguido por `cq-tagging` reinicialização do componente.

No caso de instâncias de AEM atualizadas suportadas pela API do TagManager e executadas na interface clássica:

1. Depois que as referências ao caminho base da tag antiga `/etc/tags` forem substituídas usando o tagId ou o novo local da tag `/content/cq:tags`, você poderá migrar as tags para o novo local `/content/cq:tags` no CRX, seguido da reinicialização do componente.

1. Depois de migrar as tags para o novo local, execute o script mencionado acima.
