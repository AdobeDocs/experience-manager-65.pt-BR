---
title: Auxiliares de Handlebars SCF
description: Métodos do Handlebars Helper para facilitar o trabalho com o SCF
topic-tags: developing
content-type: reference
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 2%

---

# Auxiliares de Handlebars SCF {#scf-handlebars-helpers}

| **[Feature Essentials](essentials.md)** | **[Personalização do lado do servidor ^](server-customize.md)** |
|---|---|
|   | **[Personalização no lado do cliente ^](client-customize.md)** |

Os Handlebars Helpers (helpers) são métodos chamados de scripts Handlebars para facilitar o trabalho com componentes SCF.

A implementação inclui uma definição do lado do cliente e do lado do servidor. Também é possível para os desenvolvedores criar auxiliares personalizados.

Os auxiliares SCF personalizados fornecidos com o AEM Communities são definidos na [biblioteca do cliente](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Instale o [pacote de recursos mais recente do Communities](deploy-communities.md#latestfeaturepack).

## Abreviar {#abbreviate}

Um auxiliar para retornar uma sequência de caracteres abreviada em conformidade com as propriedades maxWords e maxLength.

A cadeia de caracteres a ser abreviada é fornecida como contexto. Se nenhum contexto for fornecido, uma string vazia será retornada.

Primeiro, o contexto é reduzido para maxLength e, em seguida, o contexto é dividido em palavras e reduzido para maxWords.

Se safeString estiver definido como true, a cadeia de caracteres retornada será SafeString.

### Parâmetros {#parameters}

* **contexto**: String

  (Opcional) O padrão é a string vazia

* **maxLength**: Número

  (Opcional) Padrão é a duração do contexto.

* **maxWords**: Número

  (Opcional) Padrão é o número de palavras na string aparada.

* **safeString**: Booleano

  (Opcional) Retorna Handlebars.SafeString() se verdadeiro. O padrão é falso.

### Exemplos {#examples}

```
{{abbreviate subject maxWords=2}}

/*
If subject =
    "AEM Communities - Site Creation Wizard"

Then abbreviate would return
    "AEM Communities".
*/
```

```
{{{abbreviate message safeString=true maxLength=30}}}

/*
If message =
    "The goal of AEM Communities is to quickly create a community engagement site."

Then abbreviate would return
    "The goal of AEM Communities is"
*/
```

## Content-loadmore {#content-loadmore}

Um auxiliar para adicionar duas extensões em uma div, uma para o texto completo e outra para o menos texto, com a capacidade de alternar entre as duas visualizações.

### Parâmetros {#parameters-1}

* **contexto**: String

  (Opcional) O padrão é a cadeia de caracteres vazia.

* **numChars**: Número

  (Opcional) O número de caracteres a serem exibidos quando não estiver exibindo o texto completo. O padrão é 100.

* **moreText**: String

  (Opcional) O texto a ser exibido, indicando que há mais texto a ser exibido. O padrão é &quot;mais&quot;.

* **elipsesText**: String

  (Opcional) O texto a ser exibido indicando que há texto oculto. O padrão é &quot;...&quot;.

* **safeString**: Booleano

  (Opcional) Valor booleano que indica se Handlebars.SafeString() deve ser aplicado antes de retornar o resultado. O padrão é falso.

### Exemplo {#example}

```
{{content-loadmore  context numChars=32  moreText="go on"  ellipsesText="..." }}

/*
If context =
    "Here is the initial less content and this is more content."

Then content-loadmore would return
    "Here is the initial less content<span class="moreelipses">...</span> <span class="scf-morecontent"><span>and this is more content.</span>  <a href="" class="scf-morelink" evt="click=toggleContent">go on</a></span>"
*/
```

## DateUtil {#dateutil}

Um auxiliar para retornar uma string de data formatada.

### Parâmetros {#parameters-2}

* **contexto**: Número

  (Opcional) uma diferença de valor em milissegundos de 1º de janeiro de 1970 (época). O padrão é a data atual.

* **formato**: String

  (Opcional) O formato de data a ser aplicado. O padrão é &quot;`YYYY-MM-DDTHH:mm:ss.sssZ`&quot; e o resultado aparece como &quot;`2015-03-18T18:17:13-07:00`&quot;

### Exemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Igual a {#equals}

Um auxiliar para retornar o conteúdo dependendo de uma condição de igualdade.

### Parâmetros {#parameters-3}

* **lvalue**: String

  O valor à esquerda a ser comparado.

* **rvalue**: String

  O valor à direita a ser comparado.

### Exemplo {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
`{{else}}`
  <div>They are NOT equal!</div>
{{/equals}}
```

## If-wcm-mode {#if-wcm-mode}

Um auxiliar de bloco que testa o valor atual de [Modo WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) contra uma lista de modos separada por sequência.

### Parâmetros {#parameters-4}

* **contexto**: String

  (Opcional) A sequência de caracteres a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **modo**: String

  (Opcional) Uma lista separada por vírgulas de [Modos WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) para testar se definido.

### Exemplo {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{else}}
 ...
`{{/if-wcm-mode}}`
```

## i18n {#i-n}

Este auxiliar substitui o auxiliar Handlebars &#39;i18n&#39;.

Consulte também [Internacionalizando strings no código JavaScript](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parâmetros {#parameters-5}

* **contexto**: String

  (Opcional) A sequência de caracteres a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **padrão**: String

  (Opcional) A cadeia de caracteres padrão a ser traduzida. Obrigatório se nenhum contexto for fornecido.

* **comentário**: String

  (Opcional) Uma dica de tradução

### Exemplo {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Um auxiliar para incluir um componente como um recurso não existente em um modelo.

Esse método permite que o recurso seja personalizado programaticamente com mais facilidade do que é possível para um recurso adicionado como um nó JCR. Consulte [Adicionar ou incluir um componente das comunidades](scf.md#add-or-include-a-communities-component).

Apenas alguns componentes selecionados das Comunidades estão disponíveis para inclusão. <!-- OBSOLETE/OLD  NEED TO UPDATE FOR 6.5  For AEM 6.1, those that are includable are [comments](essentials-comments.md), [rating](rating-basics.md), [reviews](reviews-basics.md), and [voting](essentials-voting.md). -->

Este auxiliar, apropriado somente no lado do servidor, fornece funcionalidade semelhante a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-6}

* **contexto**: sequência ou objeto

  (Opcional, exceto se fornecer um caminho relativo)

  Uso `this` para transmitir o contexto atual.

  Uso `this.id` para obter o recurso em `id` para renderizar o resourceType solicitado.

* **resourceType**: String

  (Opcional) O tipo de recurso assume como padrão o tipo de recurso do contexto.

* **modelo**: String

  Caminho para o script do componente.

* **caminho**: String

  (Obrigatório) O caminho para o recurso. Se o caminho for relativo, um contexto deverá ser fornecido, caso contrário, a cadeia de caracteres vazia será retornada.

* **authoringDisabled**: Booleano

  (Opcional) O padrão é falso. Somente para uso interno.

### Exemplo {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Inclui um novo componente de comentários em `this.id` + /comentários.

## IncludeClientLib {#includeclientlib}

Um auxiliar que inclui uma biblioteca cliente AEM html, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo, js e css, essa tag deve ser usada várias vezes no script Handlebars.

Este auxiliar, apropriado somente no lado do servidor, fornece funcionalidade semelhante a [ui:includeClientLib](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-7}

* **categorias**: String

  (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Inclua todas as bibliotecas JavaScript e CSS para as categorias fornecidas. O nome do tema é extraído da solicitação.

* **tema**: String

  (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Inclua todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias fornecidas. O nome do tema é extraído da solicitação.

* **js**: String

  (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Inclui todas as bibliotecas JavaScript para as categorias fornecidas.

* **css**: String

  (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Inclui todas as bibliotecas CSS para as categorias fornecidas.

### Exemplos {#examples-2}

```
// all: js + theme (theme-js + css)
{{includeClientLib categories="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// only js libs
{{includeClientLib js="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/socialgraph.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// theme only (theme-js + css)
{{includeClientLib theme="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
    <script src="/etc/clientlibs/social/hbs/tally/voting.js" type="text/javascript"></script>
    <script src="/etc/clientlibs/social/hbs/comments.js" type="text/javascript"></script>

// css only
{{includeClientLib css="cq.social.hbs.comments, cq.social.hbs.voting"}}

// returns
    <link href="/etc/clientlibs/social/hbs/tally/voting.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/socialgraph.css" rel="stylesheet" type="text/css">
    <link href="/etc/clientlibs/social/hbs/comments.css" rel="stylesheet" type="text/css">
```

## Tempo bonito {#pretty-time}

Um auxiliar para exibir quanto tempo passou até um ponto de corte, após o qual um formato de data regular é exibido.

Por exemplo:

* 12 horas atrás
* 7 dias atrás

### Parâmetros {#parameters-8}

* **contexto**: Número

  Um horário no passado para comparar com &#39;agora&#39;. O tempo é expresso como um deslocamento de valor em milissegundos a partir de 1° de janeiro de 1970 (época).

* **daysCutoff**: Número

  O número de dias atrás antes de alternar para uma data real. O padrão é 60.

### Exemplo {#example-5}

```
{{pretty-time this.published daysCutoff=7}}

/*
Depending on how long in the past, may return

  "3 minutes ago"

  "3 hours ago"

  "3 days ago"
*/
```

## Xss-html {#xss-html}

Um auxiliar que codifica uma cadeia de caracteres de origem para o conteúdo do elemento de HTML para ajudar a proteger contra XSS.

OBSERVAÇÃO: este auxiliar não é um validador e não deve ser usado para gravar valores de atributo.

### Parâmetros {#parameters-9}

* **contexto**: objeto

  O HTML a ser codificado.

### Exemplo {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Um auxiliar que codifica uma cadeia de caracteres de origem para gravar em um valor de atributo HTML para ajudar a proteger contra XSS.

OBSERVAÇÃO: este auxiliar não é um validador e não deve ser usado para gravar atributos acionáveis (href, src, manipuladores de eventos).

### Parâmetros {#parameters-10}

* **contexto**: Objeto

  O HTML a ser codificado.

### Exemplo {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Um auxiliar que codifica uma cadeia de caracteres de origem para gravar no conteúdo de cadeia de caracteres JavaScript para ajudar a proteger contra XSS.

OBSERVAÇÃO: Este auxiliar não é um validador e não deve ser usado para gravação em JavaScript arbitrário.

### Parâmetros {#parameters-11}

* **contexto**: Objeto

  O HTML a ser codificado.

### Exemplo {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Um auxiliar que limpa um URL para gravar como um valor de atributo HTML href ou srce para ajudar a proteger contra XSS.

OBSERVAÇÃO: este auxiliar pode retornar uma cadeia de caracteres vazia.

### Parâmetros {#parameters-12}

* **contexto**: Objeto

  O URL para limpar.

### Exemplo {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Visão geral básica do Handlebars.js {#handlebars-js-basic-overview}

* Uma chamada de auxiliar do Handlebars é um identificador simples (o *name* do auxiliar), seguido por zero ou mais parâmetros separados por espaço.
* Os parâmetros podem ser um objeto String, número, booleano ou JSON simples e uma sequência opcional de pares de valores-chave (argumentos de hash) como os últimos parâmetros.
* As chaves nos argumentos de hash devem ser identificadores simples.
* Os valores em argumentos de hash são expressões Handlebars: identificadores simples, caminhos ou Strings.
* O contexto atual, `this`, está sempre disponível para os auxiliares do Handlebars.
* O contexto pode ser um objeto de dados String, number, boolean ou JSON.
* É possível passar um objeto aninhado no contexto atual como o contexto, como `this.url` ou `this.id` (consulte os exemplos a seguir de auxiliares simples e de bloco).

* Bloquear auxiliares são funções que podem ser chamadas de qualquer lugar no modelo. Eles podem chamar um bloco do modelo zero ou mais vezes com um contexto diferente a cada vez. Eles contêm um contexto entre `{{#*name*}}` e `{{/*name*}}`.

* Os Handlebars fornecem um parâmetro final para os auxiliares chamados de &quot;opções&quot;. O objeto especial &#39;options&#39; inclui

   * Dados particulares opcionais (options.data)
   * Propriedades de valor-chave opcionais da chamada (options.hash)
   * Capacidade de chamar a si mesmo (options.fn())
   * Capacidade de invocar o inverso de si mesmo (options.inverse())

* Recomenda-se que o conteúdo da Cadeia de HTML retornado de um auxiliar seja um SafeString.

### Um exemplo de um assistente simples da documentação do Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>`{{#posts}}`<li>{{{link_to "Post"}}}</li>`{{/posts}}`</ul>'

var template = Handlebars.compile(source);

template(context);
```

Renderizaria:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Publicar!&lt;/a>&lt;/li>
&lt;/ul>

### Um exemplo de um assistente de bloco da documentação do Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>`{{#people}}`<li>`{{#link}}``{{name}}``{{/link}}`</li>`{{/people}}`</ul>";

var template = Handlebars.compile(source);

template(data);
```

Renderizaria:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Auxiliares de SCF personalizados {#custom-scf-helpers}

Os auxiliares personalizados devem ser implementados no lado do servidor e no lado do cliente, especialmente ao transmitir dados. Para o SCF, a maioria dos modelos é compilada e renderizada no lado do servidor, pois o servidor gera o HTML para um determinado componente quando a página é solicitada.

### Auxiliares personalizados do lado do servidor {#server-side-custom-helpers}

Para implementar e registrar um auxiliar SCF personalizado no lado do servidor, basta implementar a interface Java™ [TemplateHelper](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), torne-o um [Serviço OSGi](../../help/sites-developing/the-basics.md#osgi) e instale-o como parte de um pacote OSGi.

Por exemplo:

### FooTextHelper.java {#footexthelper-java}

```java
/** Custom Handlebars Helper */

package com.my.helpers;

import java.io.IOException;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

import com.adobe.cq.social.handlebars.api.TemplateHelper;
import com.github.jknack.handlebars.Options;

@Service
@Component
public class FooTextHelper implements TemplateHelper<String>{

    @Override
    public CharSequence apply(String context, Options options) throws IOException {
        return "foo-" + context;
    }

    @Override
    public String getHelperName() {
        return "foo-text";
    }

    @Override
    public Class<String> getContextType() {
        return String.class;
    }
}
```

>[!NOTE]
>
>Um auxiliar criado para o lado do servidor também deve ser criado para o lado do cliente.
>
>O componente é renderizado novamente no lado do cliente para o usuário conectado e, se o auxiliar do lado do cliente não for encontrado, o componente desaparecerá.

### Auxiliares personalizados do lado do cliente {#client-side-custom-helpers}

Os auxiliares do lado do cliente são scripts Handlebars registrados chamando `Handlebars.registerHelper()`.
Por exemplo:

### custom-helpers.js {#custom-helpers-js}

```
function(Handlebars, SCF, $CQ) {

    Handlebars.registerHelper('foo-text', function(context, options) {
        if (!context) {
            return "";
        }
        return "foo-" + context;
    });

})(Handlebars, SCF, $CQ);
```

Os auxiliares personalizados do lado do cliente devem ser adicionados a uma biblioteca personalizada do cliente.
A clientlib deve:

* Incluir uma dependência em `cq.social.scf`.
* Carregar depois que o Handlebars for carregado.
* Ser [incluído](clientlibs.md).

Observação: os auxiliares do SCF estão definidos em `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[Feature Essentials](essentials.md)** | **[Personalização do lado do servidor ^](server-customize.md)** |
|---|---|
|   | **[Personalização no lado do cliente ^](client-customize.md)** |
