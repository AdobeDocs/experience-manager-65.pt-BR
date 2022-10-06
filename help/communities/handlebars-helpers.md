---
title: Auxiliares do Handlebars do SCF
seo-title: SCF Handlebars Helpers
description: Manipuladores Métodos de ajuda para facilitar o trabalho com o SCF
seo-description: Handlebars Helper methods to facilitate work with SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
exl-id: bfb95cae-4b0f-4521-a113-042dc4005a63
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 2%

---

# Auxiliares do Handlebars do SCF {#scf-handlebars-helpers}

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do servidor](server-customize.md)** |
|---|---|
|  | **[Personalização do lado do cliente](client-customize.md)** |

Os Handlebars Helpers (helpers) são métodos que podem ser chamados a partir de scripts Handlebars para facilitar o trabalho com componentes SCF.

A implementação inclui uma definição do lado do cliente e do lado do servidor. Também é possível para os desenvolvedores criarem ajuda personalizada.

Os auxiliar SCF personalizados fornecidos com o AEM Communities são definidos na variável [biblioteca cliente](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Certifique-se de instalar o [Pacote de recursos mais recente das Comunidades](deploy-communities.md#latestfeaturepack).

## Abreviar {#abbreviate}

Um auxiliar para retornar uma string abreviada que esteja em conformidade com as propriedades maxWords e maxLength.

A string a ser abreviada é fornecida como o contexto. Se nenhum contexto for fornecido, uma string vazia será retornada.

Primeiro, o contexto é reduzido a maxLength e, em seguida, o contexto é dividido em palavras e reduzido a maxWords.

Se safeString estiver definido como true, a string retornada será uma SafeString.

### Parâmetros {#parameters}

* **contexto**: String

   (Opcional) O padrão é a string vazia

* **maxLength**: Número

   (Opcional) O padrão é o comprimento do contexto.

* **maxWords**: Número

   (Opcional) Padrão é o número de palavras na string aparada.

* **safeString**: Booleano

   (Opcional) Retorna um Handlebars.SafeString() se verdadeiro. O padrão é false.

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

Um auxiliar para adicionar duas extensões em um div, uma para o texto completo e outra para o texto menor, com a capacidade de alternar entre as duas visualizações.

### Parâmetros {#parameters-1}

* **contexto**: String

   (Opcional) O padrão é a string vazia.

* **numChars**: Número

   (Opcional) O número de caracteres a serem exibidos ao não exibir texto completo. O padrão é 100.

* **moreText**: String

   (Opcional) O texto a ser exibido, indicando que há mais texto para exibir. O padrão é &quot;mais&quot;.

* **elipsesText**: String

   (Opcional) O texto a ser exibido, indicando que há texto oculto. O padrão é &quot;...&quot;.

* **safeString**: Booleano

   (Opcional) Valor booleano indicando se deve ou não aplicar Handlebars.SafeString() antes de retornar o resultado. O padrão é false.

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

   (Opcional) um deslocamento de valor de milissegundo de 1º de janeiro de 1970 (época). O padrão é a data atual.

* **format**: String

   (Opcional) O formato de data a ser aplicado. O padrão é &quot;AAAA-MM-DDTHH:mm:s.sssZ&quot; e o resultado aparece como &quot;2015-03-18T18:17:13-07:00&quot;

### Exemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Igual {#equals}

Um auxiliar para retornar conteúdo dependendo de uma condição de igualdade.

### Parâmetros {#parameters-3}

* **valor**: String

   O valor à esquerda a ser comparado.

* **rvalue**: String

   O valor à direita para comparar.

### Exemplo {#example-1}

```
{{#equals  value "some-value"}}
  <div>They are EQUAL!</div>
{{else}}
  <div>They are NOT equal!</div>
{{/equals}}
```

## Modo If-wcm {#if-wcm-mode}

Um auxiliar de bloco que testa o valor atual de [Modo WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) em relação a uma lista de modos separada por sequência.

### Parâmetros {#parameters-4}

* **contexto**: String

   (Opcional) A string a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **modo**: String

   (Opcional) Uma lista separada por vírgulas de [Modos WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) para testar se definido.

### Exemplo {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Esse auxiliar substitui o Auxiliar Handlebars &#39;i18n&#39;.

Consulte também [Internacionalização de strings no código JavaScript](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code).

### Parâmetros {#parameters-5}

* **contexto**: String

   (Opcional) A string a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **default**: String

   (Opcional) A string padrão para traduzir. Obrigatório se nenhum contexto tiver sido fornecido.

* **comentário**: String

   (Opcional) Uma dica de tradução

### Exemplo {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Um auxiliar para incluir um componente como um recurso não existente em um modelo.

Isso permite que o recurso seja programaticamente personalizado mais facilmente do que é possível para um recurso adicionado como um nó JCR. Consulte [Adicionar ou incluir um componente Comunidades](scf.md#add-or-include-a-communities-component).

Somente alguns componentes selecionados das Comunidades podem ser incluídos. Para AEM 6.1, os que podem ser incluídos são [comentários](essentials-comments.md), [classificação](rating-basics.md), [revisões](reviews-basics.md)e [votação](essentials-voting.md).

Esse auxiliar, apropriado somente no lado do servidor, fornece funcionalidade semelhante a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-6}

* **contexto**: String ou objeto

   (Opcional, a menos que forneça um caminho relativo)

   Use `this` para transmitir o contexto atual.

   Use `this.id` para obter o recurso em `id` para renderizar o resourceType solicitado.

* **resourceType**: String

   (Opcional) o tipo de recurso assumirá como padrão o tipo de recurso do contexto.

* **modelo**: String

   Caminho para o script do componente.

* **caminho**: String

   (Obrigatório) O caminho para o recurso. Se o caminho for relativo, um contexto deve ser fornecido, caso contrário, a string vazia é retornada.

* **authoringDisabled**: Booleano

   (Opcional) O padrão é falso. Apenas para uso interno.

### Exemplo {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Isso incluirá um novo componente de comentários em `this.id` + /comentários.

## IncludeClientLib {#includeclientlib}

Um auxiliar que inclui uma biblioteca cliente html AEM, que pode ser uma biblioteca js, css ou tema. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no script Handlebars.

Esse auxiliar, apropriado somente no lado do servidor, fornece funcionalidade semelhante a [ui:includeClientLib](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-7}

* **categorias**: String

   (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias fornecidas. O nome do tema é extraído da solicitação.

* **tema**: String

   (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (tanto CSS quanto JS) para as categorias fornecidas. O nome do tema é extraído da solicitação.

* **js**: String

   (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso incluirá todas as bibliotecas JavaScript para as categorias fornecidas.

* **css**: String

   (Opcional) Uma lista de categorias de bibliotecas de clientes separadas por vírgulas. Isso incluirá todas as bibliotecas CSS para as categorias fornecidas.

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

## Bastante tempo {#pretty-time}

Um auxiliar para exibir quanto tempo passou até um ponto de interrupção, após o qual um formato de data regular é exibido.

Por exemplo:

* Há 12 horas
* há 7 dias

### Parâmetros {#parameters-8}

* **contexto**: Número

   Um tempo no passado para comparar com &quot;agora&quot;. O tempo é expresso como um deslocamento de valor de milissegundo a partir de 1º de janeiro de 1970 (época).

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

Um auxiliar que codifica uma cadeia de caracteres de origem para o conteúdo do elemento HTML para ajudar a proteger contra XSS.

OBSERVAÇÃO: isso não é um validador e não deve ser usado para gravar valores de atributos.

### Parâmetros {#parameters-9}

* **contexto**: objeto

   A HTML para codificar.

### Exemplo {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Um auxiliar que codifica uma cadeia de caracteres de origem para gravar em um valor de atributo HTML para ajudar a proteger contra XSS.

OBSERVAÇÃO: isso não é um validador e não deve ser usado para gravar atributos acionáveis (href, src, manipuladores de eventos).

### Parâmetros {#parameters-10}

* **contexto**: Objeto

   A HTML para codificar.

### Exemplo {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Um auxiliar que codifica uma cadeia de caracteres de origem para gravação no conteúdo da sequência de caracteres do JavaScript para ajudar a proteger contra XSS.

OBSERVAÇÃO: isso não é um validador e não deve ser usado para gravar em JavaScript arbitrário.

### Parâmetros {#parameters-11}

* **contexto**: Objeto

   A HTML para codificar.

### Exemplo {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Um auxiliar que limpa um URL para escrever como HTML href ou valor de atributo de força para ajudar a proteger contra XSS.

OBSERVAÇÃO: isso pode retornar uma string vazia

### Parâmetros {#parameters-12}

* **contexto**: Objeto

   O URL para limpar.

### Exemplo {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Visão geral do Handlebars.js {#handlebars-js-basic-overview}

* Uma chamada de ajuda Handlebars é um identificador simples (a variável *name* do auxiliar), seguido por zero ou mais parâmetros separados por espaço.
* Os parâmetros podem ser um simples objeto String, number, boolean ou JSON, bem como uma sequência opcional de pares de valores chave (argumentos de hash) como o(s) último(s) parâmetro(s).
* As chaves nos argumentos de hash devem ser identificadores simples.
* Os valores em argumentos de hash são expressões Handlebars: identificadores simples, caminhos ou strings.
* O contexto atual, `this`, está sempre disponível para os Handlebars helpers.
* O contexto pode ser uma string, um número, um booleano ou um objeto de dados JSON.
* É possível transmitir um objeto aninhado no contexto atual como o contexto, como `this.url` ou `this.id` (ver exemplos de ajuda simples e de bloqueio).

* Bloquear auxiliar são funções que podem ser chamadas de qualquer lugar no modelo. Eles podem invocar um bloco do modelo zero ou mais vezes com um contexto diferente a cada vez. Eles contêm um contexto entre {{#*name*}} and {{/*name*}}.

* O Handlebars fornece um parâmetro final a ajudantes chamados de &quot;opções&quot;. O objeto especial &quot;opções&quot; inclui

   * Dados privados opcionais (options.data)
   * Propriedades opcionais do valor-chave da chamada (options.hash)
   * Capacidade de invocar a si mesmo (options.fn())
   * Capacidade de invocar o inverso de si mesmo (options.inverse())

* Recomenda-se que o conteúdo HTML String retornado de um auxiliar seja um SafeString.

### Um exemplo de um auxiliar simples da documentação do Handlebars.js: {#an-example-of-a-simple-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link_to', function(title, options) {
    return new Handlebars.SafeString('<a href="/posts' + this.url + '">' + title + "!</a>");
});

var context = {posts: [
    {url: "/hello-world",
      body: "Hello World!"}
  ] };

// when link_to is called, posts is the current context
var source = '<ul>{{#posts}}<li>{{{link_to "Post"}}}</li>{{/posts}}</ul>'

var template = Handlebars.compile(source);

template(context);
```

Renderizaria:

&lt;ul>
&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Post!&lt;/a>&lt;/li>
&lt;/ul>

### Um exemplo de um bloco helper da documentação do Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

```
Handlebars.registerHelper('link', function(options) {
    return new Handlebars.SafeString('<a href="/people/' + this.id + '">' + options.fn(this) + '</a>');
});

var data = { "people": [
  { "name": "Alan", "id": 1 },
  { "name": "Yehuda", "id": 2 }
]};

// when link is called, people is the current context
var source = "<ul>{{#people}}<li>{{#link}}{{name}}{{/link}}</li>{{/people}}</ul>";

var template = Handlebars.compile(source);

template(data);
```

Renderizaria:
&lt;ul>
&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>
&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>
&lt;/ul>

## Ajuda personalizada do SCF {#custom-scf-helpers}

Os auxiliares personalizados devem ser implementados no lado do servidor e no lado do cliente, especialmente ao transmitir dados. Para SCF, a maioria dos modelos é compilada e renderizada no lado do servidor à medida que o servidor gera o HTML para um determinado componente quando a página é solicitada.

### Ajudantes personalizados do lado do servidor {#server-side-custom-helpers}

Para implementar e registrar um auxiliar SCF personalizado no lado do servidor, basta implementar a interface Java [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html), torne-o um [Serviço OSGi](../../help/sites-developing/the-basics.md#osgi) e instale-o como parte de um pacote OSGi.

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
>O componente é renderizado novamente no lado do cliente para o usuário conectado e, se o auxiliar do lado do cliente não for encontrado, o componente desaparece.

### Auxiliares personalizados do lado do cliente {#client-side-custom-helpers}

Os auxiliar do lado do cliente são scripts Handlebars registrados ao invocar `Handlebars.registerHelper()`.
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

Os auxiliar personalizados do lado do cliente devem ser adicionados a uma biblioteca personalizada do cliente.
A clientlib deve:

* Incluir uma dependência em `cq.social.scf`.
* Carregar depois que o Handlebars tiver sido carregado.
* Be [included](clientlibs.md).

Observação: os assistentes do CCAH são definidos em `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[Fundamentos dos recursos ⇐](essentials.md)** | **[Personalização do lado do servidor](server-customize.md)** |
|---|---|
|  | **[Personalização do lado do cliente](client-customize.md)** |
