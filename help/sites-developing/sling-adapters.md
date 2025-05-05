---
title: Uso de adaptadores Sling
description: O Sling oferece um padrão de adaptador para traduzir convenientemente objetos que implementam a interface adaptável
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 6465e2c4-28e5-4fc8-8cca-7b632f10ba5a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 4%

---

# Uso de adaptadores Sling{#using-sling-adapters}

O [Sling](https://sling.apache.org) oferece um [Padrão de adaptador](https://sling.apache.org/documentation/the-sling-engine/adapters.html) para traduzir convenientemente objetos que implementam a interface [Adaptável](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29). Esta interface fornece um método [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) genérico que traduz o objeto para o tipo de classe que está sendo passado como argumento.

Por exemplo, para traduzir um objeto Resource para o objeto Node correspondente, você pode simplesmente fazer:

```java
Node node = resource.adaptTo(Node.class);
```

## Casos de uso {#use-cases}

Existem os seguintes casos de uso:

* Obter objetos específicos de implementação.

  Por exemplo, uma implementação baseada em JCR da interface genérica [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) fornece acesso ao JCR subjacente [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Criação de atalhos de objetos que exigem que objetos de contexto interno sejam passados.

  Por exemplo, o [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) baseado em JCR contém uma referência ao [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) da solicitação, que por sua vez é necessária para muitos objetos que funcionarão com base nessa sessão de solicitação, como o [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html) ou [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html).

* Atalho para serviços.

  Um caso raro - `sling.getService()` também é simples.

### Valor de retorno nulo {#null-return-value}

`adaptTo()` retorna nulo.

Há várias razões para isso, incluindo:

* a implementação não dá suporte ao tipo de destino
* uma fábrica de adaptadores que lida com esse caso não está ativa (por exemplo, devido a referências de serviço ausentes)
* falha na condição interna
* serviço não disponível

É importante que você lide com o caso nulo normalmente. Para renderizações jsp, pode ser aceitável que o jsp falhe se isso resultar em um conteúdo vazio.

### Armazenamento em cache {#caching}

Para melhorar o desempenho, as implementações estão livres para armazenar em cache o objeto retornado de uma chamada `obj.adaptTo()`. Se o `obj` for o mesmo, o objeto retornado será o mesmo.

Este cache é executado para todos os casos baseados em `AdapterFactory`.

No entanto, não há uma regra geral: o objeto pode ser uma nova instância ou uma existente. Isso significa que você não pode confiar em nenhum dos comportamentos. Portanto, é importante, especialmente dentro de `AdapterFactory`, que os objetos sejam reutilizáveis nesse cenário.

### Como funciona {#how-it-works}

Há várias maneiras de implementar o `Adaptable.adaptTo()`:

* Pelo próprio objeto; implementando o próprio método e mapeando para determinados objetos.
* Por um [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que pode mapear objetos arbitrários.

  Os objetos ainda devem implementar a interface `Adaptable` e devem estender [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (que passa a chamada `adaptTo` para um gerenciador de adaptador central).

  Isso permite ganchos no mecanismo `adaptTo` para classes existentes, como `Resource`.

* Uma combinação de ambos.

Para o primeiro caso, os documentos Java™ podem indicar o que `adaptTo-targets` é possível. No entanto, para subclasses específicas, como o Recurso baseado em JCR, geralmente isso não é possível. No último caso, as implementações de `AdapterFactory` normalmente fazem parte das classes privadas de um pacote e, portanto, não são expostas em uma API cliente, nem listadas em documentos Java™. Teoricamente, seria possível acessar todas as implementações de `AdapterFactory` do tempo de execução do serviço [OSGi](/help/sites-deploying/configuring-osgi.md) e examinar suas configurações (fontes e destinos) &quot;adaptáveis&quot;, mas não mapeá-las entre si. No final, isso depende da lógica interna, que deve ser documentada. Daí esta referência.

## Referência {#reference}

### Sling {#sling}

[**Recurso**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Se este for um recurso baseado em nó JCR ou uma propriedade JCR que faz referência a um nó.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propriedade</a></td>
   <td>Se este for um recurso baseado em propriedades JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Item</a></td>
   <td>Se este for um recurso baseado em JCR (nó ou propriedade)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Mapa</a></td>
   <td>Retorna um mapa das propriedades, se este for um recurso baseado em nó JCR (ou outros recursos que suportam mapas de valores)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Retorna um mapa conveniente de propriedades se este for um recurso baseado em nó JCR (ou outro recurso que suporte mapas de valor). Também pode ser obtido (de forma mais simples) usando <br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> (processa maiúsculas e minúsculas e assim por diante)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensão de <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite que a hierarquia de recursos seja considerada ao procurar propriedades</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModisibleValueMap</a></td>
   <td>Uma extensão do <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que permite modificar propriedades nesse nó</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Retorna o conteúdo binário de um recurso de arquivo (se este for um recurso baseado em nó JCR e o tipo de nó for <code>nt:file</code> ou <code>nt:resource</code>; se este for um recurso de pacote; conteúdo de arquivo, se este for um recurso do sistema de arquivos) ou os dados de um recurso de propriedade JCR binário</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Retorna um URL para o recurso (URL do repositório deste nó se este for um recurso baseado em nó JCR; URL do pacote jar se este for um recurso do pacote; URL do arquivo se este for um recurso do sistema de arquivos)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">Arquivo</a></td>
   <td>Se este for um recurso do sistema de arquivos</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Se esse recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com o sling</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>Se esse recurso for um script (por exemplo, arquivo jsp) para o qual um mecanismo de script está registrado com o sling ou se for um recurso de servlet.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Cadeia de caracteres</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Longo</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Duplo</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendário</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">Cadeia de caracteres[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Booleano[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Longo[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendário[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Valor[]</a></td>
   <td>Retorna os valores se este for um recurso baseado em propriedades JCR (e o valor se ajustar).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Se este for um recurso baseado em nó JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Se este for um recurso baseado em nó JCR e o nó for um <code>cq:Page</code> (ou <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Se este for um recurso de nó <code>cq:Component</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Design.html">Design</a></td>
   <td>Se este for um nó de design (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html">Modelo</a></td>
   <td>Se este for um recurso de nó <code>cq:Template</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Blueprint</a></td>
   <td>Se este for um recurso de nó <code>cq:Template</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Asset.html">Ativo</a></td>
   <td>Se este for um recurso do nó dam:Asset</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/Rendition.html">Representação</a></td>
   <td>Se for uma representação dam:Asset (nt:file na pasta de representação de um dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/Tag.html">Tag</a></td>
   <td>Se este for um recurso de nó <code>cq:Tag</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Baseado na sessão JCR, se este for um recurso baseado em JCR e o usuário tiver permissões para acessar o UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a></td>
   <td>A Autorizável é a interface básica comum para usuários e grupos</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a></td>
   <td>O usuário é um Authorizable especial que pode ser autenticado e representado</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/SimpleSearch.html">PesquisaSimples</a></td>
   <td>Pesquisa abaixo o recurso (ou use setSearchIn()) se este for um recurso baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Status do fluxo de trabalho para determinada página/nó de carga do fluxo de trabalho</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html">StatusReplicação</a></td>
   <td>Status de replicação para o recurso fornecido ou seu subnó jcr:content (marcado primeiro)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Retorna um recurso de conector adaptado para determinados tipos, se este for um recurso baseado em nó JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">Configuração</a></td>
   <td>Se este for um recurso de nó <code>cq:ContentSyncConfig</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Se isso estiver abaixo de um recurso de nó <code>cq:ContentSyncConfig</code></td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/ResourceResolver.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>A sessão JCR da solicitação, se for um resolvedor de recursos baseado em JCR (padrão)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>Com base na sessão JCR, se este for um resolvedor de recursos baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>Com base na sessão JCR, se este for um resolvedor de recursos baseado em JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>O UserManager fornece acesso e meios para manter objetos autorizáveis, ou seja, usuários e grupos. O UserManager está associado a uma sessão específica
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizável</a> </td>
   <td>O usuário atual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuário</a><br /> </td>
   <td>O usuário atual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar URLs absolutas, mesmo sem o objeto de solicitação<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) adapta-se a:

Ainda sem destinos, mas implementa Adaptable e pode ser usado como origem em um AdapterFactory personalizado.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ManipuladordeConteúdo</a><br /> (XML)</td>
   <td>Se esta for uma resposta de reescrita do sling</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Página](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)** adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><br /> </td>
   <td>Recurso da página</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Recurso rotulado (== este)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó da página</td>
  </tr>
  <tr>
   <td>..</td>
   <td>Tudo ao qual o recurso da página pode ser adaptado</td>
  </tr>
 </tbody>
</table>

**[O componente](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/components/Component.html)** se adapta a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do componente. |
|---|---|
| [RecursoRotulado](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso rotulado (== este). |
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do componente. |
| .. | Tudo ao qual o recurso do componente pode ser adaptado. |

**[Modelo](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Template.html)** adapta-se a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso do modelo</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/LabeledResource.html">RecursoRotulado</a></td>
   <td>Recurso rotulado (== este)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nó</a></td>
   <td>Nó deste modelo</td>
  </tr>
  <tr>
   <td>..</td>
   <td>Tudo ao qual o recurso do modelo pode ser adaptado.</td>
  </tr>
 </tbody>
</table>

#### Segurança {#security}

**Autorizável**, **Usuário e &#x200B;** Grupo** adaptam-se a:

| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Retorna o nó inicial do usuário/grupo. |
|---|---|
| [StatusDaReplicação](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/replication/ReplicationStatus.html) | Retorna o status de replicação do nó inicial do usuário/grupo. |

#### DAM {#dam}

**O ativo** se adapta a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso do ativo. |
|---|---|
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó do ativo. |
| .. | Tudo ao qual o recurso do ativo pode ser adaptado. |

#### Marcação com tags {#tagging}

**A marca** se adapta a:

| [Recurso](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso da tag. |
|---|---|
| [Nó](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nó da tag. |
| .. | Tudo ao qual o recurso da tag pode ser adaptado. |

#### Outro {#other}

Além disso, o Sling/JCR/OCM também fornece um ` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)` para objetos OCM personalizados ([Mapeamento de conteúdo de objeto](https://jackrabbit.apache.org/jcr/object-content-mapping.html)).
