---
title: Bibliotecas de tags
description: As bibliotecas de tags do Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP de seus modelos e componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 50e608d5-951f-4a3f-bed4-9e92ff5d7bd4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2460'
ht-degree: 0%

---

# Bibliotecas de tags{#tag-libraries}

As bibliotecas de tags do Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP de seus modelos e componentes.

## Biblioteca de tags do Granite {#granite-tag-library}

A biblioteca de tags do Granite contém funções úteis.

Ao desenvolver o script jsp de um componente da interface do Granite, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

O global também declara que a [Biblioteca Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### &lt;ui:includeClientLib> {#ui-includeclientlib}

A variável `<ui:includeClientLib>` tag Inclui uma biblioteca cliente AEM html, que pode ser uma js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo, js e css, essa tag deve ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno do ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` interface de serviço.

Ela tem os seguintes atributos:

**categorias** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas JavaScript e CSS para as categorias fornecidas. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias fornecidas. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas JavaScript para as categorias fornecidas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas CSS para as categorias fornecidas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temático** - Um sinalizador que indica que apenas bibliotecas com ou sem temas devem ser incluídas. Se omitido, ambos os conjuntos serão incluídos. Aplica-se somente a inclusões puras de JS ou CSS (não para inclusões de categorias ou temas).

A variável `<ui:includeClientLib>` tag pode ser usada da seguinte maneira em um jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<ui:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<ui:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<ui:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<ui:includeClientLib css="cq.collab.calendar, cq.security" />
```

## Biblioteca de tags CQ {#cq-tag-library}

A biblioteca de tags do CQ contém funções úteis.

Para usar a Biblioteca de tags do CQ no script, ele deve começar com o seguinte código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando a variável `/libs/foundation/global.jsp` for incluído no script, a taglib será declarada automaticamente.

Ao desenvolver o script jsp de um componente AEM, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Ele declara as taglibs sling, CQ e jstl e expõe os objetos de script usados regularmente definidos pelo [`<cq:defineObjects />`](#amp-lt-cq-defineobjects) tag. Isso reduz e simplifica o código jsp do seu componente.

### &lt;cq:text> {#cq-text}

A variável `<cq:text>` tag é uma tag de conveniência que gera texto de componente em um JSP.

Ele tem os seguintes atributos opcionais:

**propriedade** - Nome da propriedade a ser usada. O nome é relativo ao recurso atual.

**value** - Valor a ser usado para saída. Se este atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**oldValue** - Valor a ser usado para saída diff. Se este atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**escapeXml** - Define se os caracteres &lt;, >, &amp;, &#39; e &quot; na cadeia de caracteres resultante devem ser convertidos em seus códigos de entidade de caractere correspondentes. O valor padrão é falso. O escape é aplicado após a formatação opcional.

**formato** - Opcional java.text.Format para formatar o texto.

**noDiff** - Suprime o cálculo de uma saída de diferenças, mesmo se uma informação de diferenças estiver presente.

**tagClass** - Nome da classe CSS de um elemento que envolverá uma saída não vazia. Se estiver vazio, nenhum elemento será adicionado.

**tagName** - Nome do elemento que envolverá uma saída não vazia. O padrão é DIV.

**espaço reservado** - Valor padrão a ser usado para texto nulo ou vazio no modo de edição, ou seja, o espaço reservado. A verificação padrão é executada após a formatação e o escape opcionais, ou seja, ela é gravada como está na saída. O padrão é:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**padrão** - Valor padrão a ser usado para texto nulo ou vazio. A verificação padrão é executada após a formatação opcional e o escape, ou seja, ela é gravada como está na saída.

Alguns exemplos mostram como o `<cq:text>` A tag pode ser usada em uma JSP:

```xml
<cq:text property="jcr:title" tagName="h2"/>
<cq:text property="jcr:description" tagName="p"/>

<cq:text value="<%= listItem.getTitle() %>" tagName="h4" placeholder="" />
<cq:text value="<%= listItem.getDescription() %>" tagName="p" placeholder=""/>

<cq:text property="jcr:title" value="<%= title %>" tagName="h3"/><%
    } else if (type.equals("link")) {
        %><cq:text property="jcr:title" value="<%= "\u00bb " + title %>" tagName="p" tagClass="link"/><%
    } else if (type.equals("extralarge")) {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h1"/><%
    } else {
        %><cq:text property="jcr:title" value="<%= title %>" tagName="h2"/><%

<cq:text property="jcr:description" placeholder="" tagName="small"/>

<cq:text property="tableData"
               escapeXml="false"
               placeholder="<img src=\"/libs/cq/ui/resources/0.gif\" class=\"cq-table-placeholder\" alt=\"\">"
    />

<cq:text property="text"/>

<cq:text property="image/jcr:description" placeholder="" tagName="small"/>
<cq:text property="text" tagClass="text"/>
```

### &lt;cq:setContentBundle> {#cq-setcontentbundle}

A variável `<cq:setContentBundle>` A tag cria um contexto de localização i18n e o armazena na tag `javax.servlet.jsp.jstl.fmt.localizationContext` variável de configuração.

Ela tem os seguintes atributos:

**idioma** - O idioma do local para o qual recuperar o pacote de recursos.

**origem** - A fonte de onde o local deve ser obtido. Ele pode ser definido como um dos seguintes valores:

* **estático** - a localidade é retirada do `language` atributo, se disponível, caso contrário, no local padrão do servidor.

* **página** - o local é obtido do idioma da página atual ou do recurso, se disponível, caso contrário, do `language` atributo, se disponível, caso contrário, no local padrão do servidor.

* **solicitação** - a localidade é retirada da localidade da solicitação ( `request.getLocale()`).

* **automático** - a localidade é retirada do `language` atributo, se disponível; caso contrário, do idioma da página atual ou do recurso, se disponível, caso contrário, da solicitação.

Se a variável `source` o atributo não está definido:

* Se a variável `language` for definido, a variável `source` o padrão do atributo é &quot; `static`.

* Se a variável `language` atributo não estiver definido, a variável `source` o padrão do atributo é `auto`.

O &quot;pacote de conteúdo&quot; pode ser usado pelo JSTL padrão `<fmt:message>` específicos. A pesquisa de mensagens por chaves é dupla:

1. Primeiro, as propriedades JCR do recurso subjacente renderizado são pesquisadas para traduções. Isso permite que você defina uma caixa de diálogo de componente simples para editar esses valores.
1. Se o nó não contiver uma propriedade chamada exatamente como a chave, o fallback será para carregar um conjunto de recursos da solicitação do sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). O idioma ou localidade desse pacote é definido pelo idioma e pelos atributos de origem do `<cq:setContentBundle>` tag.

A variável `<cq:setContentBundle>` tag pode ser usada da seguinte maneira em uma jsp.

Para páginas que definem seu idioma:

```xml
... %><cq:setContentBundle source="page"/><%  %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

Para páginas personalizadas do usuário:

```xml
... %><cq:setContentBundle scope="request"/><% %>
<div class="error"><fmt:message key="Hello"/>
</div> ...
```

### &lt;cq:include> {#cq-include}

A variável `<cq:include>` A tag inclui um recurso na página atual.

Ela tem os seguintes atributos:

**liberar**

* Um booleano que define se a saída deve ser liberada antes da inclusão do destino.

**caminho**

* O caminho para o objeto de recurso a ser incluído no processamento da solicitação atual. Se esse caminho for relativo, ele será anexado ao caminho do recurso atual cujo script está incluindo o recurso determinado. Path e resourceType ou script devem ser especificados.

**resourceType**

* O tipo de recurso do recurso a ser incluído. Se o tipo de recurso for definido, o caminho deverá ser o caminho exato para um objeto de recurso. Nesse caso, não há suporte para a adição de parâmetros, seletores e extensões ao caminho.
* Se o recurso a ser incluído for especificado com o atributo path que não pode ser resolvido para um recurso, a tag poderá criar um objeto de recurso sintético fora do caminho e desse tipo de recurso.
* Path e resourceType ou script devem ser especificados.

**script**

* O script jsp a ser incluído. Path e resourceType ou script devem ser especificados.

**ignoreComponentHierarchy**

* Um booleano que controla se a hierarquia de componentes deve ser ignorada para a resolução do script. Se true, somente os caminhos de pesquisa serão respeitados.

**Exemplo:**

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><div class="center">
    <cq:include path="trail" resourceType="foundation/components/breadcrumb" />
    <cq:include path="title" resourceType="foundation/components/title" />
    <cq:include script="redirect.jsp"/>
    <cq:include path="par" resourceType="foundation/components/parsys" />
</div>
```

Você deve usar `<%@ include file="myScript.jsp" %>` ou `<cq:include script="myScript.jsp" %>` para incluir um script?

* A variável `<%@ include file="myScript.jsp" %>` A diretiva informa o compilador JSP a incluir um arquivo completo no arquivo atual. É como se o conteúdo do arquivo incluído fosse colado diretamente no arquivo original.
* Com o `<cq:include script="myScript.jsp">` , o arquivo será incluído no tempo de execução.

Você deve usar `<cq:include>` ou `<sling:include>`?

* Ao desenvolver componentes para AEM, a Adobe recomenda o uso de `<cq:include>`.
* `<cq:include>` permite incluir arquivos de script diretamente pelo nome ao usar o atributo de script. Isso leva em conta a herança de componentes e tipos de recursos e geralmente é mais simples do que a adesão estrita à resolução de script do Sling usando seletores e extensões.

### &lt;cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` Obsoleto desde o AEM 5.6. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) deve ser usado em vez disso.

A variável `<cq:includeClientLib>` tag Inclui uma biblioteca cliente AEM html, que pode ser uma js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo, js e css, essa tag deve ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno do `com.day.cq.widget.HtmlLibraryManager` interface de serviço.

Ela tem os seguintes atributos:

**categorias** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas JavaScript e CSS para as categorias fornecidas. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias fornecidas. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas JavaScript para as categorias fornecidas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso inclui todas as bibliotecas CSS para as categorias fornecidas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temático** - Um sinalizador que indica que apenas bibliotecas com ou sem temas devem ser incluídas. Se omitido, ambos os conjuntos serão incluídos. Aplica-se somente a inclusões puras de JS ou CSS (não para inclusões de categorias ou temas).

A variável `<cq:includeClientLib>` tag pode ser usada da seguinte maneira em um jsp:

```xml
<%-- all: js + theme (theme-js + css) --%>
<cq:includeClientLib categories="cq.wcm.edit" />

<%-- only js libs --%>
<cq:includeClientLib js="cq.collab.calendar, cq.security" />

<%-- theme only (theme-js + css) --%>
<cq:includeClientLib theme="cq.collab.calendar, cq.security" />

<%-- css only --%>
<cq:includeClientLib css="cq.collab.calendar, cq.security" />
```

### &lt;cq:defineObjects> {#cq-defineobjects}

A variável `<cq:defineObjects>` A tag do expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor. Também expõe os objetos definidos pelo [`<sling:defineObjects>`](#amp-lt-sling-defineobjects) tag.

**componentContext**

* o objeto de contexto do componente atual da solicitação (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* o objeto do componente AEM atual do recurso atual (com.day.cq.wcm.api.components.Component interface).

**currentDesign**

* o objeto de design atual da página atual (interface com.day.cq.wcm.api.designer.Design).

**currentPage**

* o objeto da página WCM do AEM atual (com.day.cq.wcm.api.Page interface).

**currentStyle**

* o objeto de estilo atual da célula atual (interface com.day.cq.wcm.api.designer.Style).

**designer**

* o objeto de designer usado para acessar informações de design (interface com.day.cq.wcm.api.designer.Designer).

**editContext**

* o objeto de contexto de edição do componente AEM (com.day.cq.wcm.api.components.EditContext interface).

**pageManager**

* o objeto do gerenciador de páginas para operações no nível da página (com.day.cq.wcm.api.PageManager interface).

**pageProperties**

* o objeto de propriedades da página atual (org.apache.sling.api.resource.ValueMap).

**propriedades**

* o objeto de propriedades do recurso atual (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* o objeto de design da página de recursos (interface com.day.cq.wcm.api.designer.Design).

**resourcePage**

* o objeto da página de recursos (com.day.cq.wcm.api.Page interface).
* Ela tem os seguintes atributos:

**requestName**

* herdado do sling

**responseName**

* herdado do sling

**resourceName**

* herdado do sling

**nodeName**

* herdado do sling

**logName**

* herdado do sling

**resourceResolverName**

* herdado do sling

**slingName**

* herdado do sling

**componentContextName**

* específico do wcm

**editContextName**

* específico do wcm

**propertiesName**

* específico do wcm

**pageManagerName**

* específico do wcm

**currentPageName**

* específico do wcm

**resourcePageName**

* específico do wcm

**pagePropertiesName**

* específico do wcm

**componentName**

* específico do wcm

**designerName**

* específico do wcm

**currentDesignName**

* específico do wcm

**resourceDesignName**

* específico do wcm

**currentStyleName**

* específico do wcm

**Exemplo**

```xml
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%@ page import="com.day.cq.wcm.api.WCMMode" %><%
%><%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
%><cq:defineObjects/>
```

>[!NOTE]
>
>Quando a variável `/libs/foundation/global.jsp` arquivo estiver incluído no script, a variável `<cq:defineObjects />` é incluída automaticamente.

### &lt;cq:requestURL> {#cq-requesturl}

A variável `<cq:requestURL>` A tag grava o URL da solicitação atual no JspWriter. As duas tags [`<cq:addParam>`](#amp-lt-cq-addparam) e [`<cq:removeParam>`](#amp-lt-cq-removeparam) e podem ser usados no corpo dessa tag para modificar o URL de solicitação atual antes que ele seja gravado.

Ela permite criar links para a página atual com parâmetros variáveis. Por exemplo, ela permite transformar a solicitação:

`mypage.html?mode=view&query=something` em `mypage.html?query=something`.

A utilização de `addParam` ou `removeParam` altera apenas a ocorrência do parâmetro fornecido, todos os outros parâmetros não são afetados.

`<cq:requestURL>` não tem nenhum atributo.

Exemplos:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:addParam> {#cq-addparam}

A variável `<cq:addParam>` adiciona um parâmetro de solicitação com o nome e valor fornecidos ao delimitador [`<cq:requestURL>`](#amp-lt-cq-requesturl) tag.

Ela tem os seguintes atributos:

**name**

* nome do parâmetro a ser adicionado

**valor**

* valor do parâmetro a ser adicionado

**Exemplo:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### &lt;cq:removeParam> {#cq-removeparam}

A variável `<cq:removeParam>` A tag remove um parâmetro de solicitação com o nome e o valor fornecidos do delimitador [`<cq:requestURL>`](#amp-lt-cq-requesturl) tag. Se nenhum valor for fornecido, todos os parâmetros com o nome fornecido serão removidos.

Ela tem os seguintes atributos:

**name**

* nome do parâmetro a ser removido

Exemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Biblioteca de tags Sling {#sling-tag-library}

A biblioteca de tags Sling contém funções Sling úteis.

Ao usar a Biblioteca de tags do Sling no script, ele deve começar com o seguinte código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando a variável `/libs/foundation/global.jsp` for incluído no script, o sling taglib será declarado automaticamente.

### &lt;sling:include> {#sling-include}

A variável `<sling:include>` A tag inclui um recurso na página atual.

Ela tem os seguintes atributos:

**liberar**

* Um booleano que define se a saída deve ser liberada antes da inclusão do destino.

**resource**

* O objeto de recurso a ser incluído no processamento da solicitação atual. O recurso ou o caminho deve ser especificado. Se ambos forem especificados, o recurso terá prioridade.

**caminho**

* O caminho para o objeto de recurso a ser incluído no processamento da solicitação atual. Se esse caminho for relativo, ele será anexado ao caminho do recurso atual cujo script está incluindo o recurso determinado. O recurso ou o caminho deve ser especificado. Se ambos forem especificados, o recurso terá prioridade.

**resourceType**

* O tipo de recurso do recurso a ser incluído. Se o tipo de recurso for definido, o caminho deverá ser o caminho exato para um objeto de recurso. Nesse caso, não há suporte para a adição de parâmetros, seletores e extensões ao caminho.
* Se o recurso a ser incluído for especificado com o atributo path que não pode ser resolvido para um recurso, a tag poderá criar um objeto de recurso sintético fora do caminho e desse tipo de recurso.

**replaceSelectors**

* Ao despachar, os seletores são substituídos pelo valor desse atributo.

**addSelectors**

* Ao despachar, o valor desse atributo é adicionado aos seletores.

**replaceSuffix**

* Ao despachar, o sufixo é substituído pelo valor desse atributo.

>[!NOTE]
>
>A resolução do recurso e o script incluídos com o `<sling:include>` A tag é igual à resolução normal de um URL do sling. Por padrão, os seletores, a extensão e assim por diante da solicitação atual também são usados para o script incluído. Eles podem ser modificados por meio dos atributos de tag: por exemplo, `replaceSelectors="foo.bar"` permite substituir os seletores.

Exemplos:

```xml
<div class="item"><sling:include path="<%= pathtoinclude %>"/></div>
```

```xml
<sling:include resource="<%= par %>"/>
```

```xml
<sling:include addSelectors="spool"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include resource="<%= par %>" resourceType="<%= newType %>"/>
```

```xml
<sling:include replaceSelectors="content" />
```

### &lt;sling:defineObjects> {#sling-defineobjects}

A variável `<sling:defineObjects>` A tag do expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor:

**slingRequest**

* O objeto SlingHttpServletRequest, que fornece acesso às informações do cabeçalho da solicitação HTTP, estende o HttpServletRequest padrão e fornece acesso a itens específicos do Sling, como recurso, informações de caminho e seletor.

**slingResponse**

* Objeto SlingHttpServletResponse, que fornece acesso à resposta HTTP criada pelo servidor. É o mesmo que HttpServletResponse do qual se estende.**solicitação**
* O objeto de solicitação JSP padrão que é um HttpServletRequest puro.**resposta**
* O objeto de resposta JSP padrão que é um HttpServletResponse puro.

**resourceResolver**

* O objeto ResourceResolver atual. É o mesmo que slingRequest.getResourceResolver()

.**sling**

* Um objeto SlingScriptHelper, que contém métodos de conveniência para scripts, principalmente sling.include(&#39;/some/other/resource&#39;) para incluir as respostas de outros recursos dentro dessa resposta (por exemplo, incorporação de trechos de cabeçalho html) e sling.getService(foo.bar.Service.class) para recuperar serviços OSGi disponíveis em Sling (notação de classe dependendo da linguagem de script).

**resource**

* o objeto de Recurso atual a ser manipulado, dependendo do URL da solicitação. É o mesmo que slingRequest.getResource().

**currentNode**

* Se o recurso atual apontar para um nó JCR (que normalmente é o caso no Sling), isso dará acesso direto ao objeto Node. Caso contrário, esse objeto não será definido.

**log**

* Fornece um Logger SLF4J para fazer logon no sistema de log Sling a partir de scripts, por exemplo, log.info(&quot;Executando meu script&quot;).

* Ela tem os seguintes atributos:

**requestName**

**responseName**

**nodeName**

l **ogName resourceResolverName**

**slingName**

**Exemplo:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Biblioteca de tags JSTL {#jstl-tag-library}

A variável [Biblioteca de tags padrão de páginas JavaServer](https://www.oracle.com/java/technologies/java-server-tag-library.html) O contém muitas tags úteis e padrão. As taglibs principal, de formatação e de funções são definidas pelo `/libs/foundation/global.jsp` conforme mostrado no trecho a seguir.

### Extrato de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Após a importação do `/libs/foundation/global.jsp` conforme descrito anteriormente, você pode usar o `c`, `fmt` e `fn` prefixos para acessar essas bibliotecas de tags. A documentação oficial do JSTL está disponível em [Tutorial do Java™ EE 5 - Biblioteca de tags padrão de páginas JavaServer](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
