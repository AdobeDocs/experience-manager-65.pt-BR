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
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 1%

---


# Bibliotecas de tags{#tag-libraries}

As bibliotecas de tags Granite, CQ e Sling fornecem acesso a funções específicas para uso no script JSP dos seus modelos e componentes.

## Biblioteca de tags do Granite {#granite-tag-library}

A biblioteca de tags Granite contém funções úteis.

Ao desenvolver o script jsp de um componente de interface do usuário Granite, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/granite/ui/global.jsp"%>
```

O global também declara a [biblioteca Sling](/help/sites-developing/taglib.md#sling-tag-library).

```xml
<%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling" %>
```

### <ui:includeClientLib> {#ui-includeclientlib}

A tag `<ui:includeClientLib>` Inclui uma biblioteca de cliente html AEM, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno da interface de serviço ` [com.adobe.granite.ui.clientlibs.HtmlLibraryManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/ui/clientlibs/HtmlLibraryManager.html)`.

Ele tem os seguintes atributos:

**categorias**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias em questão. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeIncludes`

**tema**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias em questão. O nome do tema é extraído da solicitação.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeThemeInclude`

**js** - Uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas do Javascript para as categorias em questão.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeJsInclude`

**css**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas de CSS para as categorias em questão.

Equivalente a: `com.adobe.granite.ui.clientlibs.HtmlLibraryManager#writeCssInclude`

**temed** - Deve ser incluído um sinalizador que indique apenas bibliotecas temáticas ou não. Se omitidos, ambos os conjuntos serão incluídos. Aplica-se somente às inclusões de JS ou CSS puras (não para categorias ou inclusão de temas).

A tag `<ui:includeClientLib>` pode ser usada como segue em um jsp:

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

Para usar a Biblioteca de tags do CQ em seu script, o script deve ser start com o seguinte código:

```xml
<%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
```

>[!NOTE]
>
>Quando o arquivo `/libs/foundation/global.jsp` for incluído no script, a tag será declarada automaticamente.

Ao desenvolver o script jsp de um componente AEM, é recomendável incluir o seguinte código na parte superior do script:

```xml
<%@include file="/libs/foundation/global.jsp"%>
```

Ele declara os sling, CQ e jstl taglibs e expõe os objetos de script usados regularmente definidos pela tag [ `<cq:defineObjects />`](#amp-lt-cq-defineobjects). Isso reduz e simplifica o código jsp do seu componente.

### <cq:text> {#cq-text}

A tag `<cq:text>` é uma tag de conveniência que gera o texto do componente em um JSP.

Ele tem os seguintes atributos opcionais:

**propriedade**  - Nome da propriedade a ser usada. O nome é relativo ao recurso atual.

**value** - Valor a ser usado para saída. Se esse atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**oldValue**  - Valor a ser usado para saída diff. Se esse atributo estiver presente, ele substituirá o uso do atributo de propriedade.

**escapeXml** - Define se os caracteres  &lt;>, &amp;, &#39; e &quot; na sequência resultante devem ser convertidos para seus códigos de entidade de caractere correspondentes. O valor padrão é falso. Observe que o escape é aplicado após a formatação opcional.

**format**  - opcional java.text.Format para usar na formatação do texto.

**noDiff** - Suprime o cálculo de uma saída diff, mesmo se uma informação diff estiver presente.

**tagClass**  - o nome da classe CSS de um elemento que rodeia uma saída não vazia. Se estiver vazio, nenhum elemento será adicionado.

**tagName** - O nome do elemento que rodeará uma saída não vazia. O padrão é DIV.

**espaço reservado**  - Valor padrão a ser usado para texto nulo ou vazio no modo de edição, ou seja, o espaço reservado. Observe que a verificação padrão é executada após a formatação opcional e a fuga, isto é, ela é gravada como está na saída. O padrão é:

`<div><span class="cq-text-placeholder">&para;</span></div>`

**padrão**  - Valor padrão a ser usado para texto nulo ou vazio. Observe que a verificação padrão é executada após a formatação opcional e a saída, isto é, ela é gravada como está na saída.

Alguns exemplos de como a tag `<cq:text>` pode ser usada em um JSP:

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

A tag `<cq:setContentBundle>` cria um contexto de localização i18n e o armazena na variável de configuração `javax.servlet.jsp.jstl.fmt.localizationContext`.

Ele tem os seguintes atributos:

**idioma**  - o idioma da localidade para a qual recuperar o conjunto de recursos.

**fonte**  - a fonte de onde a localidade deve ser retirada. Ele pode ser definido como um dos seguintes valores:

* **static**  - a localidade é retirada do  `language` atributo, se disponível, caso contrário, da localidade padrão do servidor.

* **página**  - a localidade é retirada do idioma da página ou do recurso atual, se disponível, caso contrário, do  `language` atributo, se disponível, caso contrário, da localidade padrão do servidor.

* **solicitação**  - a localidade é retirada da localidade da solicitação (  `request.getLocale()`).

* **auto** - a localidade é retirada do  `language` atributo, se disponível, caso contrário, do idioma da página ou recurso atual, se disponível, caso contrário, da solicitação.

Se o atributo `source` não estiver definido:

* Se o atributo `language` estiver definido, o padrão do atributo `source` será &quot;`static`.

* Se o atributo `language` não estiver definido, o padrão do atributo `source` será `auto`.

O &quot;pacote de conteúdo&quot; pode ser usado simplesmente pelas tags padrão JSTL `<fmt:message>`. A consulta das mensagens por chaves é dupla:

1. Primeiro, as propriedades do JCR do recurso subjacente que está sendo renderizado no momento são pesquisadas por traduções. Isso permite que você defina uma caixa de diálogo de componente simples para editar esses valores.
1. Se o nó não contiver uma propriedade chamada exatamente como a chave, o fallback será carregar um conjunto de recursos da solicitação sling ( `SlingHttpServletRequest.getResourceBundle(Locale)`). O idioma ou a localidade desse pacote é definida pelos atributos de idioma e origem da tag `<cq:setContentBundle>`.

A tag `<cq:setContentBundle>` pode ser usada da seguinte forma em um jsp.

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

A tag `<cq:include>` inclui um recurso na página atual.

Ele tem os seguintes atributos:

**descarga**

* Um booliano que define se deve liberar a saída antes de incluir o público alvo.

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

Você deve usar `<%@ include file="myScript.jsp" %>` ou `<cq:include script="myScript.jsp" %>` para incluir um script?

* A diretiva `<%@ include file="myScript.jsp" %>` informa o compilador JSP para incluir um arquivo completo no arquivo atual. É como se o conteúdo do arquivo incluído fosse colado diretamente no arquivo original.
* Com a tag `<cq:include script="myScript.jsp">`, o arquivo é incluído no tempo de execução.

Você deve usar `<cq:include>` ou `<sling:include>`?

* Ao desenvolver componentes AEM, o Adobe recomenda usar `<cq:include>`.
* `<cq:include>` permite que você inclua diretamente os arquivos de script pelo seu nome ao usar o atributo de script. Isso leva em conta a herança do tipo de componente e recurso, e geralmente é mais simples do que a estrita adesão à resolução do script do Sling usando seletores e extensões.

### <cq:includeClientLib> {#cq-includeclientlib}

>[!CAUTION]
>
>`<cq:includeClientLib>` está obsoleto desde AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#ui-includeclientlib) deve ser usada em vez disso.

A tag `<cq:includeClientLib>` Inclui uma biblioteca de cliente html AEM, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no jsp. Esta tag é um invólucro de conveniência em torno da interface de serviço `com.day.cq.widget.HtmlLibraryManager`.

Ele tem os seguintes atributos:

**categorias**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias em questão. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeIncludes`

**tema**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias em questão. O nome do tema é extraído da solicitação.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#`writeThemeInclude

**js** - Uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas do Javascript para as categorias em questão.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeJsInclude`

**css**  - uma lista de categorias de biblioteca de cliente separadas por vírgulas. Isso incluirá todas as bibliotecas de CSS para as categorias em questão.

Equivalente a: `com.day.cq.widget.HtmlLibraryManager#writeCssInclude`

**temed** - Deve ser incluído um sinalizador que indique apenas bibliotecas temáticas ou não. Se omitidos, ambos os conjuntos serão incluídos. Aplica-se somente às inclusões de JS ou CSS puras (não para categorias ou inclusão de temas).

A tag `<cq:includeClientLib>` pode ser usada como segue em um jsp:

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

A tag `<cq:defineObjects>` expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor. Ele também expõe os objetos definidos pela tag [ `<sling:defineObjects>`](#amp-lt-sling-defineobjects).

**componentContext**

* o objeto de contexto do componente atual da solicitação (com.day.cq.wcm.api.components.ComponentContext interface).

**componente**

* o objeto AEM componente atual do recurso atual (com.day.cq.wcm.api.components.Component interface).

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
>Quando o arquivo `/libs/foundation/global.jsp` for incluído no script, a tag `<cq:defineObjects />` será incluída automaticamente.

### <cq:requestURL> {#cq-requesturl}

A tag `<cq:requestURL>` grava o URL da solicitação atual no JspWriter. As duas tags [ `<cq:addParam>`](#amp-lt-cq-addparam) e [ `<cq:removeParam>`](#amp-lt-cq-removeparam) e podem ser usadas dentro do corpo dessa tag para modificar o URL da solicitação atual antes de ser gravado.

Permite criar links para a página atual com parâmetros variáveis. Por exemplo, permite transformar a solicitação:

`mypage.html?mode=view&query=something` em `mypage.html?query=something`.

O uso de `addParam` ou `removeParam` somente altera a ocorrência do parâmetro especificado, todos os outros parâmetros não são afetados.

`<cq:requestURL>` não tem nenhum atributo.

Exemplos:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

```xml
<a title="filter results" href="<cq:requestURL><cq:addParam name="language" value="${bucket.value}"/></cq:requestURL>">${label} (${bucket.count})</a>
```

### <cq:addParam> {#cq-addparam}

A tag `<cq:addParam>` adiciona um parâmetro de solicitação com o nome e o valor fornecidos à tag [ `<cq:requestURL>`](#amp-lt-cq-requesturl) anexada.

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

A tag `<cq:removeParam>` remove um parâmetro de solicitação com o nome e o valor fornecidos da tag [ `<cq:requestURL>`](#amp-lt-cq-requesturl) anexada. Se nenhum valor for fornecido, todos os parâmetros com o nome especificado serão removidos.

Ele tem os seguintes atributos:

**name**

* nome do parâmetro a ser removido

Exemplo:

```xml
<a href="<cq:requestURL><cq:removeParam name="language"/></cq:requestURL>">remove filter</a>
```

## Biblioteca de tags Sling {#sling-tag-library}

A biblioteca de tags Sling contém funções Sling úteis.

Quando você usa a Biblioteca de tags Sling em seu script, o script deve ser start com o seguinte código:

```xml
<%@ taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %>
```

>[!NOTE]
>
>Quando o arquivo `/libs/foundation/global.jsp` for incluído no script, a sling taglib será declarada automaticamente.

### <sling:include> {#sling-include}

A tag `<sling:include>` inclui um recurso na página atual.

Ele tem os seguintes atributos:

**descarga**

* Um booliano que define se deve liberar a saída antes de incluir o público alvo.

**recurso**

* O objeto de recurso a ser incluído no processamento da solicitação atual. É necessário especificar o recurso ou o caminho. Se ambos forem especificados, o recurso terá precedência.

**caminho**

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
>A resolução do recurso e do script incluídos com a tag `<sling:include>` é a mesma que para uma resolução normal de URL de sling. Por padrão, os seletores, a extensão etc. da solicitação atual também são usados para o script incluído. Eles podem ser modificados pelos atributos da tag: por exemplo, `replaceSelectors="foo.bar"` permite que você substitua os seletores.

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

A tag `<sling:defineObjects>` expõe os seguintes objetos de script, usados regularmente, que podem ser referenciados pelo desenvolvedor:

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

A [Biblioteca de tags do JavaServer Pages Standard](https://www.oracle.com/technetwork/java/index-jsp-135995.html) contém muitas tags úteis e padrão. Os taglibs principal, de formatação e de funções são definidos pelo `/libs/foundation/global.jsp`, conforme mostrado no trecho a seguir.

### Extração de /libs/foundation/global.jsp {#extract-of-libs-foundation-global-jsp}

```xml
<%@taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
<%@taglib prefix="fmt" uri="https://java.sun.com/jsp/jstl/fmt" %>
<%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions" %>
```

Depois de importar o arquivo `/libs/foundation/global.jsp` conforme descrito anteriormente, você pode usar os prefixos `c`, `fmt` e `fn` para acessar esses taglibs. A documentação oficial do JSTL está disponível em [O tutorial do Java EE 5 - Biblioteca de tags do JavaServer Pages Standard](https://docs.oracle.com/javaee/5/tutorial/doc/bnakc.html).
