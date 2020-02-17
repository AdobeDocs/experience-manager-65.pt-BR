---
title: Bibliotecas de tags
seo-title: Bibliotecas de tags
description: As bibliotecas de tags Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP de seus modelos e componentes
seo-description: As bibliotecas de tags Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP de seus modelos e componentes
uuid: e622d47b-cfb3-4b4a-b8e3-e1adee294219
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 6678e3c3-fb0f-4300-8838-38f23f14db07
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Bibliotecas de tags{#tag-libraries}

As bibliotecas de tags Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP dos seus modelos e componentes.

## Biblioteca de tags Granite {#granite-tag-library}

A biblioteca de tags Granite contém funções úteis.

Ao desenvolver o script jsp de um componente de interface do usuário Granite, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

O global também declara a biblioteca [](/help/sites-developing/taglib.md#sling-tag-library)Sling.

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

A `<ui:includeClientLib>` tag Inclui uma biblioteca de cliente html do AEM, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno da interface de ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)` serviço.

Ele tem os seguintes atributos:

**categorias** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias especificadas. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias especificadas. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript para as categorias especificadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas de CSS para as categorias especificadas.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temed** - deve ser incluído um sinalizador que indica apenas bibliotecas temáticas ou não. Se omitidos, ambos os conjuntos serão incluídos. Aplica-se somente às inclusões de JS ou CSS puras (não para categorias ou inclusão de temas).

A `<ui:includeClientLib>` tag pode ser usada como segue em um jsp:

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

## Biblioteca de tags do CQ {#cq-tag-library}

A biblioteca de tags do CQ contém funções úteis.

Para usar a Biblioteca de tags do CQ em seu script, o script deve começar com o seguinte código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando o `/libs/foundation/global.jsp` arquivo é incluído no script, a tag é declarada automaticamente.

Ao desenvolver o script jsp de um componente AEM, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Ele declara os sling, CQ e jstl taglibs e expõe os objetos de script usados regularmente definidos pela [ tag `<cq:defineObjects />`](#amp-lt-cq-defineobjects) . Isso reduz e simplifica o código jsp do seu componente.

### <cq:text> {#cq-text}

A `<cq:text>` tag é uma tag de conveniência que gera o texto do componente em um JSP.

Ele tem os seguintes atributos opcionais:

**propriedade** - Nome da propriedade a ser usada. O nome é relativo ao recurso atual.

**value** - Valor a ser usado para saída. Se esse atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**oldValue** - Valor a ser usado para saída diff. Se esse atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**escapeXml** - Define se os caracteres &lt;, >, &amp;, &#39; e &quot; na sequência resultante devem ser convertidos para seus códigos de entidade de caractere correspondentes. O valor padrão é falso. Observe que o escape é aplicado após a formatação opcional.

**format** - opcional java.text.Format a ser usado para a formatação do texto.

**noDiff** - suprime o cálculo de uma saída diff, mesmo se uma informação diff estiver presente.

**tagClass** - o nome da classe CSS de um elemento que rodeia uma saída não vazia. Se estiver vazio, nenhum elemento será adicionado.

**tagName** - o nome do elemento que delimitará uma saída não vazia. O padrão é DIV.

**espaço reservado** - Valor padrão para usar para texto nulo ou vazio no modo de edição, ou seja, o espaço reservado. Observe que a verificação padrão é executada após a formatação opcional e a fuga, isto é, ela é gravada como está na saída. O padrão é:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**default** - Valor padrão a ser usado para texto nulo ou vazio. Observe que a verificação padrão é realizada após a formatação opcional e a saída, isto é, é gravada como está na saída.

Alguns exemplos de como a `<cq:text>` tag pode ser usada em um JSP:

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

### <cq:setContentBundle> {#cq-setcontentbundle}

A `<cq:setContentBundle>` tag cria um contexto de localização do i18n e o armazena na variável de `javax.servlet.jsp.jstl.fmt.localizationContext` configuração.

Ele tem os seguintes atributos:

**idioma** - o idioma da localidade para a qual recuperar o conjunto de recursos.

**source** - a fonte de onde a localidade deve ser retirada. Pode ser definido como um dos seguintes valores:

* **static** - a localidade é retirada do `language` atributo, se disponível, caso contrário, da localidade padrão do servidor.

* **page** - a localidade é retirada do idioma da página ou do recurso atual, se disponível, caso contrário, do `language` atributo, se disponível, caso contrário, da localidade padrão do servidor.

* **request** - a localidade é retirada da localidade da solicitação ( `request.getLocale()`).

* **auto** - a localidade é retirada do `language` atributo, se disponível, caso contrário, do idioma da página ou recurso atual, se disponível, caso contrário, da solicitação.

Se o `source` atributo não estiver definido:

* Se o `language` atributo estiver definido, o `source` atributo assumirá &quot; `static`.

* Se o `language` atributo não estiver definido, o `source` atributo assumirá `auto`.

O &quot;pacote de conteúdo&quot; pode ser usado simplesmente por `<fmt:message>` tags JSTL padrão. A consulta das mensagens por chaves é dupla:

1. Primeiro, as propriedades do JCR do recurso subjacente que está sendo renderizado no momento são pesquisadas por traduções. Isso permite que você defina uma caixa de diálogo de componente simples para editar esses valores.
1. Se o nó não contiver uma propriedade chamada exatamente como a chave, o fallback será carregar um conjunto de recursos da solicitação de sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). O idioma ou a localidade desse pacote é definida pelos atributos de idioma e origem da `<cq:setContentBundle>` tag .

A `<cq:setContentBundle>` tag pode ser usada da seguinte forma em um jsp.

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

### <cq:include> {#cq-include}

A `<cq:include>` tag inclui um recurso na página atual.

Ele tem os seguintes atributos:

**descarga**

* Um booliano que define se a saída deve ser despachada antes de incluir a meta.

**path**

* O caminho para o objeto de recurso a ser incluído no processamento da solicitação atual. Se esse caminho for relativo, ele será anexado ao caminho do recurso atual cujo script está incluindo o recurso fornecido. É necessário especificar path e resourceType ou script.

**resourceType**

* O tipo de recurso do recurso a ser incluído. Se o tipo de recurso estiver definido, o caminho deve ser o caminho exato para um objeto de recurso: nesse caso, não há suporte para a adição de parâmetros, seletores e extensões ao caminho.
* Se o recurso a ser incluído for especificado com o atributo path que não pode ser resolvido como um recurso, a tag poderá criar um objeto de recurso sintético fora do caminho e desse tipo de recurso.
* É necessário especificar path e resourceType ou script.

**script**

* O script jsp a ser incluído. É necessário especificar path e resourceType ou script.

**ignoreComponentHierarchy**

* Um booliano que controla se a hierarquia do componente deve ser ignorada para a resolução do script. Se verdadeiro, somente os caminhos de pesquisa serão respeitados.

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

Você deve usar `<%@ include file="myScript.jsp" %>` ou `<cq:include script="myScript.jsp" %>` incluir um script?

* A `<%@ include file="myScript.jsp" %>` diretiva informa o compilador JSP para incluir um arquivo completo no arquivo atual. É como se o conteúdo do arquivo incluído fosse colado diretamente no arquivo original.
* Com a `<cq:include script="myScript.jsp">` tag , o arquivo é incluído no tempo de execução.

Você deveria usar `<cq:include>` ou `<sling:include>`?

* Ao desenvolver componentes do AEM, a Adobe recomenda que você use `<cq:include>`.
* `<cq:include>` permite que você inclua diretamente os arquivos de script pelo seu nome ao usar o atributo de script. Isso leva em conta a herança do tipo de componente e recurso, e geralmente é mais simples do que a estrita adesão à resolução do script do Sling usando seletores e extensões.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` foi substituída desde o AEM 5.6. Em vez disso, [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) deve ser utilizado.

A `<cq:includeClientLib>` tag Inclui uma biblioteca de cliente html do AEM, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno da interface de `com.day.cq.widget.HtmlLibraryManager` serviço.

Ele tem os seguintes atributos:

**categorias** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias especificadas. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias especificadas. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript para as categorias especificadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css** - uma lista de categorias de lib de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas de CSS para as categorias especificadas.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temed** - deve ser incluído um sinalizador que indica apenas bibliotecas temáticas ou não. Se omitidos, ambos os conjuntos serão incluídos. Aplica-se somente às inclusões de JS ou CSS puras (não para categorias ou inclusão de temas).

A `<cq:includeClientLib>` tag pode ser usada como segue em um jsp:

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

### <cq:defineObjects> {#cq-defineobjects}

A `<cq:defineObjects>` tag expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor. Ele também expõe os objetos definidos pela [ tag `<sling:defineObjects>`](#amp-lt-sling-defineobjects) .

**componentContext**

* o objeto de contexto do componente atual da solicitação (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* o objeto do componente AEM atual do recurso atual (com.day.cq.wcm.api.components.Component interface).

**currentDesign**

* o objeto de design atual da página atual (com.day.cq.wcm.api.designer.Design interface).

**currentPage**

* o objeto de página WCM AEM atual (com.day.cq.wcm.api.Page interface).

**currentStyle**

* o objeto de estilo atual da célula atual (com.day.cq.wcm.api.designer.Style interface).

**designer**

* o objeto do designer usado para acessar informações de design (com.day.cq.wcm.api.designer.interface do Designer).

**editContext**

* o objeto de contexto de edição do componente AEM (com.day.cq.wcm.api.components.EditContext interface).

**pageManager**

* o objeto do gerenciador de páginas para operações em nível de página (com.day.cq.wcm.api.interface do PageManager).

**pageProperties**

* o objeto de propriedades da página atual (org.apache.sling.api.resource.ValueMap).

**propriedades**

* o objeto de propriedades do recurso atual (org.apache.sling.api.resource.ValueMap).

**resourceDesign**

* o objeto de design da página de recursos (com.day.cq.wcm.api.designer.Design interface).

**resourcePage**

* o objeto da página de recursos (com.day.cq.wcm.api.Page interface).
* Ele tem os seguintes atributos:

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
>Quando o `/libs/foundation/global.jsp` arquivo é incluído no script, a `<cq:defineObjects />` tag é incluída automaticamente.

### <cq:requestURL> {#cq-requesturl}

A `<cq:requestURL>` tag grava o URL da solicitação atual no JspWriter. As duas tags [ `<cq:addParam>`](#amp-lt-cq-addparam) e [ `<cq:removeParam>`](#amp-lt-cq-removeparam) e podem ser usadas dentro do corpo dessa tag para modificar o URL da solicitação atual antes de ser gravado.

Permite criar links para a página atual com parâmetros variáveis. Por exemplo, permite transformar a solicitação:

`mypage.html?mode=view&query=something` em `mypage.html?query=something`.

O uso de `addParam` ou `removeParam` apenas altera a ocorrência de determinado parâmetro, todos os outros parâmetros não são afetados.

`<cq:requestURL>` não tem nenhum atributo.

Exemplos:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

A `<cq:addParam>` tag adiciona um parâmetro de solicitação com o nome e o valor fornecidos à [ `<cq:requestURL>`](#amp-lt-cq-requesturl) tag de inclusão.

Ele tem os seguintes atributos:

**name**

* nome do parâmetro a ser adicionado

**valor**

* valor do parâmetro a ser adicionado

**Exemplo:**

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:removeParam> {#cq-removeparam}

A `<cq:removeParam>` tag remove um parâmetro de solicitação com o nome e o valor fornecidos da [`<cq:requestURL>`](#amp-lt-cq-requesturl) tag de inclusão. Se nenhum valor for fornecido, todos os parâmetros com o nome especificado serão removidos.

Ele tem os seguintes atributos:

**name**

* nome do parâmetro a ser removido

Exemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Biblioteca de tags Sling {#sling-tag-library}

A biblioteca de tags Sling contém funções Sling úteis.

Ao usar a Biblioteca de tags do Sling em seu script, o script deve começar com o seguinte código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando o `/libs/foundation/global.jsp` arquivo é incluído no script, o sling taglib é declarado automaticamente.

### <sling:include> {#sling-include}

A `<sling:include>` tag inclui um recurso na página atual.

Ele tem os seguintes atributos:

**descarga**

* Um booliano que define se a saída deve ser despachada antes de incluir a meta.

**recurso**

* O objeto de recurso a ser incluído no processamento da solicitação atual. É necessário especificar o recurso ou o caminho. Se ambos forem especificados, o recurso terá precedência.

**path**

* O caminho para o objeto de recurso a ser incluído no processamento da solicitação atual. Se esse caminho for relativo, ele será anexado ao caminho do recurso atual cujo script está incluindo o recurso fornecido. É necessário especificar o recurso ou o caminho. Se ambos forem especificados, o recurso terá precedência.

**resourceType**

* O tipo de recurso do recurso a ser incluído. Se o tipo de recurso estiver definido, o caminho deve ser o caminho exato para um objeto de recurso: nesse caso, não há suporte para a adição de parâmetros, seletores e extensões ao caminho.
* Se o recurso a ser incluído for especificado com o atributo path que não pode ser resolvido como um recurso, a tag poderá criar um objeto de recurso sintético fora do caminho e desse tipo de recurso.

**replaceSelectors**

* Ao despachar, os seletores são substituídos pelo valor desse atributo.

**addSelectors**

* Ao despachar, o valor desse atributo é adicionado aos seletores.

**replaceSuffix**

* Ao despachar, o sufixo é substituído pelo valor desse atributo.

>[!NOTE]
>
>A resolução do recurso e do script incluídos com a `<sling:include>` tag é a mesma que para uma resolução normal de URL de sling. Por padrão, os seletores, a extensão etc. da solicitação atual também são usados para o script incluído. Eles podem ser modificados pelos atributos da tag: por exemplo, `replaceSelectors="foo.bar"` permite que você substitua os seletores.

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

### <sling:defineObjects> {#sling-defineobjects}

A `<sling:defineObjects>` tag expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor:

**slingRequest**

* O objeto SlingHttpServletRequest, que fornece acesso às informações do cabeçalho da solicitação HTTP - estende o HttpServletRequest padrão - e fornece acesso a itens específicos do Sling, como recursos, informações de caminho, seletor etc.

**slingResponse**

* Objeto SlingHttpServletResponse, fornecendo acesso para a resposta HTTP criada pelo servidor. Atualmente, é o mesmo que HttpServletResponse, a partir do qual é estendida.**solicitação**
* O objeto de solicitação JSP padrão que é um HttpServletRequest puro.**response**
* O objeto de resposta JSP padrão que é um HttpServletResponse puro.

**resourceResolver**

* O objeto ResourceResolver atual. É igual a slingRequest.getResourceResolver()

.**sling**

* Um objeto SlingScriptHelper, que contém métodos de conveniência para scripts, principalmente sling.include(&#39;/some/other/resource&#39;) para incluir as respostas de outros recursos dentro dessa resposta (por exemplo, incorporação de snippets html de cabeçalho) e sling.getService(foo.bar.Service.class) para recuperar os serviços OSGi disponíveis no Sling (notação de classe dependendo da linguagem de script).

**recurso**

* o objeto de Recurso atual a ser tratado, dependendo do URL da solicitação. É o mesmo que slingRequest.getResource().

**currentNode**

* Se o recurso atual apontar para um nó JCR (que normalmente é o caso no Sling), isso fornece acesso direto ao objeto Node. Caso contrário, esse objeto não será definido.

**registro**

* Fornece um Logger SLF4J para registro no sistema de log Sling a partir de scripts, por exemplo. log.info(&quot;Executando meu script&quot;).

* Ele tem os seguintes atributos:

**requestName**

**responseName**

**nodeName**

resourceResolverName do **logName**

**slingName**

**Exemplo:**

```xml
<%@page session="false" %><%
%><%@page import="com.day.cq.wcm.foundation.forms.ValidationHelper"%><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/>
```

## Biblioteca de tags JSTL {#jstl-tag-library}

A Biblioteca [de tags do](https://www.oracle.com/technetwork/java/index-jsp-135995.html) JavaServer Pages Standard contém várias tags úteis e padrão. Os taglibs de núcleo, formatação e funções são definidos pelo `/libs/foundation/global.jsp` como mostrado no trecho a seguir.

### Extração de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Depois de importar o `/libs/foundation/global.jsp` arquivo como descrito anteriormente, você pode usar os prefixos `c`, `fmt` e `fn` para acessar esses taglibs. A documentação oficial do JSTL está disponível no Tutorial [do Java EE 5 - Biblioteca](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html)de tags do JavaServer Pages Standard.
