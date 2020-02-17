---
title: Uso de adaptadores Sling
seo-title: Uso de adaptadores Sling
description: O Sling oferece um padrão de adaptador para converter convenientemente objetos que implementam a interface adaptável
seo-description: O Sling oferece um padrão de adaptador para converter convenientemente objetos que implementam a interface adaptável
uuid: 07f66a33-072d-49e1-8e67-8b80a6a9072a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: c081b242-67e4-4820-9bd3-7e4495df459e
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Uso de adaptadores Sling{#using-sling-adapters}

[O Sling](https://sling.apache.org) oferece um padrão [de](https://sling.apache.org/site/adapters.html) adaptador para converter convenientemente objetos que implementam a interface [adaptável](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) . Essa interface fornece um método genérico [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) que traduzirá o objeto para o tipo de classe que está sendo passado como argumento.

Por exemplo, para traduzir um objeto de Recurso para o objeto Nó correspondente, basta fazer o seguinte:

```java
Node node = resource.adaptTo(Node.class);
```

## Use Cases {#use-cases}

Há os seguintes casos de uso:

* Obtenha objetos específicos da implementação.

   Por exemplo, uma implementação baseada em JCR da interface genérica fornece acesso ao JCR subjacente [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) [`Node`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).&quot;

* Criação de atalhos de objetos que exigem a transmissão de objetos de contexto internos.

   Por exemplo, o JCR [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) contém uma referência ao [`JCR Session`](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html)da solicitação, que por sua vez é necessária para muitos objetos que funcionarão com base na sessão da solicitação, como o [`PageManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) ou [`UserManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html).

* Atalho para serviços.

   Um caso raro - `sling.getService()` também é simples.

### Valor de retorno nulo {#null-return-value}

`adaptTo()` pode retornar nulo.

Há várias razões para isso, incluindo:

* a implementação não suporta o tipo de alvo
* um adaptador de fábrica que manuseia este caso não está ativo (por exemplo, devido a referências de serviço ausentes)
* falha na condição interna
* serviço não está disponível

É importante que você manipule a caixa nula com cuidado. Para renderizações jsp, pode ser aceitável que o jsp falhe se isso resultar em um conteúdo vazio.

### Cache {#caching}

Para melhorar o desempenho, as implementações podem armazenar em cache o objeto retornado de uma `obj.adaptTo()` chamada. Se o objeto `obj` for o mesmo, o objeto retornado será o mesmo.

Esse cache é executado para todos os casos `AdapterFactory` baseados.

No entanto, não há regra geral - o objeto pode ser uma nova instância ou uma existente. Isso significa que você não pode confiar em nenhum dos comportamentos. Assim, é importante, principalmente dentro `AdapterFactory`, que os objetos sejam reutilizáveis nesse cenário.

### Como funciona {#how-it-works}

Há várias maneiras de `Adaptable.adaptTo()` implementar:

* Pelo próprio objeto; implementação do próprio método e mapeamento para certos objetos.
* Por um [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html)&quot;, que pode mapear objetos arbitrários.

   Os objetos ainda devem implementar a `Adaptable` interface e ser estendidos [`SlingAdaptable`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (o que passa a `adaptTo` chamada para um gerenciador central do adaptador).

   Isso permite que os ganchos entrem no `adaptTo` mecanismo para classes existentes, como `Resource`.

* Uma combinação de ambos.

No primeiro caso, os javadocs podem dizer o que `adaptTo-targets` é possível. No entanto, para subclasses específicas, como o recurso baseado no JCR, isso geralmente não é possível. No último caso, as implementações de `AdapterFactory` são normalmente parte das classes privadas de um pacote e, portanto, não são expostas em uma API de cliente, nem listadas em javadocs. Teoricamente, seria possível acessar todas as `AdapterFactory` implementações a partir do tempo de execução do serviço [OSGi](/help/sites-deploying/configuring-osgi.md) e observar suas configurações &quot;adaptáveis&quot; (fontes e destinos), mas não mapeá-las umas às outras. Afinal, isso depende da lógica interna, que deve ser documentada. Daí essa referência.

## Referência {#reference}

### Sling {#sling}

[**O recurso **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html)se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Se for um recurso baseado em nó JCR ou uma propriedade JCR que faça referência a um nó.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propriedade</a></td>
   <td>Se este for um recurso baseado em propriedade JCR.</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td>
   <td>Se for um recurso baseado em JCR (nó ou propriedade).</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api//java/util/Map.html">Mapa</a></td>
   <td>Retorna um mapa das propriedades, se este for um recurso baseado em nós JCR (ou outros mapas de valor de suporte de recursos).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Retorna um mapa conveniente das propriedades, se for um recurso baseado em nós JCR (ou outros mapas de valor de suporte de recursos). Também pode ser obtido (mais simples) usando<br /> <code><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceUtil.html#getvaluemap%28org.apache.sling.api.resource.resource%29">ResourceUtil.getValueMap(Resource)</a></code> (manipula letras maiúsculas e minúsculas, etc.).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensão do <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite que a hierarquia de recursos seja considerada ao procurar propriedades.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/PersistableValueMap.html">PersistableValueMap</a></td>
   <td>Se este for um recurso baseado em nó JCR e o usuário tiver permissões para modificar as propriedades nesse nó.<br /> Observação: vários mapas persistentes não compartilham seus valores.</td>
  </tr>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Retorna o conteúdo binário de um "arquivo"<code>nt:resource</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>AuthorizableResourceProvider</code><code>org.apache.sling.jackrabbit.usermanager</code><code>/system/userManager</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Page</code><code>cq:PseudoPage</code></td></tr><tr><td></td><td><code>cq:Component</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td><code>cq:Template</code></td></tr><tr><td></td><td><code>cq:Page</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:Tag</code></td></tr><tr><td></td><td><code>cq:Preferences</code></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr><tr><td></td><td><code>cq:ContentSyncConfig</code></td></tr></tbody></table>

[**O ResourceResolver **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/ResourceResolver.html)adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Sessão</a></td>
   <td>A sessão JCR da solicitação, se for um resolvedor de recursos baseado em JCR (padrão).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Com base na sessão JCR, se for um resolvedor de recursos baseado em JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Com base na sessão JCR, se for um resolvedor de recursos baseado em JCR.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Com base na sessão JCR, se este for um resolvedor de recursos baseado em JCR e se o usuário tiver permissões para acessar o UserManager.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a> </td>
   <td>O usuário atual.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a><br /> </td>
   <td>O usuário atual.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/privileges/PrivilegeManager.html">PrivilegeManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/Preferences.html">Preferências</a></td>
   <td>Preferências do usuário atual (com base na sessão JCR se for um resolvedor de recursos baseado em JCR).</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/preferences/PreferencesService.html">PreferencesService</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/auth/pin/PinManager.html">PinManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar URLs absolutos, mesmo sem o objeto de solicitação.<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletRequest.html)adapta-se a:

Nenhum destino ainda, mas implementa Adaptável e pode ser usado como fonte em um AdapterFactory personalizado.

[**SlingHttpServletResponse **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/SlingHttpServletResponse.html)adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://java.sun.com/j2se/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br /> (XML)</td>
   <td>Se isso for uma resposta de um sling rewriter.</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

[**A página **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><br /> </td>
   <td>Recurso da página.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabelResource</a></td>
   <td>Recurso rotulado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó da página.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tudo ao qual o recurso da página pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

[**O componente **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/components/Component.html)adapta-se a:

| [Recurso](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do componente. |
|---|---|
| [LabelResource](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso rotulado (== this). |
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do componente. |
| ... | Tudo ao qual o recurso do componente pode ser adaptado. |

[**O modelo **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Template.html)adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /></a></td>
   <td>Recurso do modelo.</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/LabeledResource.html">LabelResource</a></td>
   <td>Recurso rotulado (== this).</td>
  </tr>
  <tr>
   <td><a href="https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó deste modelo.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Tudo ao qual o recurso do modelo pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

#### Segurança {#security}

[**Autorizável **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Authorizable.html),[**Usuário**](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/User.html) e [**Grupo **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/security/Group.html)se adaptam a:

| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Retorna o nó inicial do usuário/grupo. |
|---|---|
| [ReplicationStatus](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/ReplicationStatus.html) | Retorna o status de replicação do nó inicial do usuário/grupo. |

#### DAM {#dam}

[**O ativo **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/Asset.html)se adapta a:

| [Recurso](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do ativo. |
|---|---|
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do ativo. |
| ... | Tudo ao qual o recurso do ativo pode ser adaptado. |

#### Marcação com tags {#tagging}

[**A tag **](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/Tag.html)se adapta a:

| [Recurso](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso da tag . |
|---|---|
| [Nó](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó da tag . |
| ... | Tudo ao qual o recurso da tag pode ser adaptado. |

#### Outro {#other}

Além disso, Sling / JCR / COM também fornece um ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` para objetos MAC personalizados ([Object Content Mapping](https://jackrabbit.apache.org/object-content-mapping.html)).
