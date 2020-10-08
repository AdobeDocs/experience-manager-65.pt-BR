---
title: Auxiliares de barras de mão SCF
seo-title: Auxiliares de barras de mão SCF
description: Métodos de ajuda para handbars para facilitar o trabalho com SCF
seo-description: Métodos de ajuda para handbars para facilitar o trabalho com SCF
uuid: 9c514199-871e-4b68-8147-2052d2eeda15
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8b6c1697-d693-41f4-8337-f41658465107
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# Auxiliares de barras de mão SCF {#scf-handlebars-helpers}

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Utilitário de personalização do servidor](server-customize.md)** |
|---|---|
|  | **[Localização da personalização do cliente](client-customize.md)** |

Os Handlebars Helpers (helpers) são métodos chamáveis dos scripts Handlebars para facilitar o trabalho com componentes SCF.

A implementação inclui uma definição do lado do cliente e do lado do servidor. Também é possível para os desenvolvedores criar auxiliares personalizados.

Os auxiliares SCF personalizados fornecidos com a AEM Communities são definidos na biblioteca do [cliente](../../help/sites-developing/clientlibs.md):

* `/etc/clientlibs/social/commons/scf/helpers.js`

>[!NOTE]
>
>Instale o pacote de recursos [mais recente das Comunidades](deploy-communities.md#latestfeaturepack).

## Abreviar {#abbreviate}

Um auxiliar para retornar uma string abreviada em conformidade com as propriedades maxWords e maxLength.

A string a ser abreviada é fornecida como o contexto. Se nenhum contexto for fornecido, uma string vazia será retornada.

Primeiro, o contexto é aparado para maxLength e, em seguida, o contexto é fatiado em palavras e reduzido para maxWords.

Se safeString estiver definido como true, a string retornada será SafeString.

### Parâmetros {#parameters}

* **contexto**: String

   (Opcional) O padrão é a string vazia

* **maxLength**: Número

   (Opcional) O padrão é o comprimento do contexto.

* **maxWords**: Número

   (Opcional) Padrão é o número de palavras na string aparada.

* **safeString**: Booleano

   (Opcional) Retorna um Handlebars.SafeString() se verdadeiro. O padrão é falso.

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

Um auxiliar para adicionar duas extensões sob uma div, uma para o texto completo e outra para o texto menor, com a capacidade de alternar entre as duas visualizações.

### Parâmetros {#parameters-1}

* **contexto**: String

   (Opcional) O padrão é a string vazia.

* **numChars**: Número

   (Opcional) O número de caracteres a serem exibidos ao não exibir o texto completo. O padrão é 100.

* **moreText**: String

   (Opcional) O texto a ser exibido indica que há mais texto para exibir. O padrão é &quot;mais&quot;.

* **elipsesText**: String

   (Opcional) O texto a ser exibido indicando que há texto oculto. O padrão é &quot;...&quot;.

* **safeString**: Booleano

   (Opcional) Valor booliano que indica se deve ou não aplicar Handlebars.SafeString() antes de retornar o resultado. O padrão é falso.

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

   (Opcional) um deslocamento de valor de milissegundo a partir de 1º de janeiro de 1970 (época). O padrão é a data atual.

* **formato**: String

   (Opcional) O formato de data a ser aplicado. O padrão é &quot;AAAA-MM-DDTHH:mm:ss.sssZ&quot; e o resultado aparece como &quot;2015-03-18T18:17:13-07:00&quot;

### Exemplos {#examples-1}

```
{{dateUtil this.memberSince format="dd MMM yyyy, hh:mm"}}

// returns "18 Mar 2015, 18:17"
```

```
{{dateUtil this.birthday format="MM-DD-YYYY"}}

// returns "03-18-2015"
```

## Equals {#equals}

Um auxiliar para retornar conteúdo dependendo de uma condição de igualdade.

### Parâmetros {#parameters-3}

* **lvalue**: String

   O valor à esquerda para comparar.

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

Um auxiliar de bloco que testa o valor atual do modo [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM em relação a uma lista de modos separada por sequências de caracteres.

### Parâmetros {#parameters-4}

* **contexto**: String

   (Opcional) A string a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **modo**: String

   (Opcional) Uma lista separada por vírgulas dos modos [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM para testar se estão definidos.

### Exemplo {#example-2}

```xml
{{#if-wcm-mode mode="DESIGN, EDIT"}}
 ...
{{else}}
 ...
{{/if-wcm-mode}}
```

## i18n {#i-n}

Este auxiliar substitui o Auxiliar Handlebars &#39;i18n&#39;.

Consulte também [Internacionalização de strings no código](../../help/sites-developing/i18n-dev.md#internationalizing-strings-in-javascript-code)JavaScript.

### Parâmetros {#parameters-5}

* **contexto**: String

   (Opcional) A string a ser traduzida. Obrigatório se nenhum padrão for fornecido.

* **padrão**: String

   (Opcional) A string padrão a ser traduzida. Obrigatório se nenhum contexto tiver sido fornecido.

* **comentário**: String

   (Opcional) Uma dica de tradução

### Exemplo {#example-3}

```
{{i18n "hello"}}
{{i18n "hello" comment="greeting" default="bonjour"}}
```

## Incluir {#include}

Um auxiliar para incluir um componente como um recurso não existente em um modelo.

Isso permite que o recurso seja programaticamente personalizado mais facilmente do que é possível para um recurso adicionado como um nó JCR. Consulte [Adicionar ou incluir um componente](scf.md#add-or-include-a-communities-component)de Comunidades.

Somente alguns componentes selecionados de Comunidades podem ser incluídos. No AEM 6.1, os que podem ser incluídos são [comentários](essentials-comments.md), [classificações](rating-basics.md), [revisões](reviews-basics.md)e [votação](essentials-voting.md).

Esse auxiliar, apropriado apenas no lado do servidor, fornece funcionalidade semelhante a [cq:include](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-6}

* **contexto**: String ou objeto

   (Opcional, a menos que forneça um caminho relativo)

   Use `this` para passar o contexto atual.

   Use `this.id` para obter o recurso em `id` para renderizar o resourceType solicitado.

* **resourceType**: String

   (Opcional) o tipo de recurso assumirá como padrão o tipo de recurso do contexto.

* **modelo**: String

   Caminho para o script de componente.

* **caminho**: String

   (Obrigatório) O caminho para o recurso. Se o caminho for relativo, um contexto deverá ser fornecido, caso contrário, a string vazia será retornada.

* **authoringDisabled**: Booleano

   (Opcional) O padrão é falso. Apenas para uso interno.

### Exemplo {#example-4}

```
{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}
```

Isso incluirá um novo componente de comentários em `this.id` + /comments.

## IncludeClientLib {#includeclientlib}

Um auxiliar que inclui uma biblioteca de cliente html AEM, que pode ser um js, um css ou uma biblioteca de temas. Para várias inclusões de tipos diferentes, por exemplo js e css, essa tag precisa ser usada várias vezes no script Handlebars.

Esse auxiliar, apropriado apenas no lado do servidor, fornece funcionalidade semelhante à [ui:includeClientLib](../../help/sites-developing/taglib.md) para scripts JSP.

### Parâmetros {#parameters-7}

* **categorias**: String

   (Opcional) Uma lista de categorias de link do cliente separadas por vírgulas. Isso incluirá todas as bibliotecas Javascript e CSS para as categorias em questão. O nome do tema é extraído da solicitação.

* **tema**: String

   (Opcional) Uma lista de categorias de link do cliente separadas por vírgulas. Isso incluirá todas as bibliotecas relacionadas ao tema (CSS e JS) para as categorias em questão. O nome do tema é extraído da solicitação.

* **js**: String

   (Opcional) Uma lista de categorias de link do cliente separadas por vírgulas. Isso incluirá todas as bibliotecas do Javascript para as categorias em questão.

* **css**: String

   (Opcional) Uma lista de categorias de link do cliente separadas por vírgulas. Isso incluirá todas as bibliotecas de CSS para as categorias em questão.

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

## Muito tempo {#pretty-time}

Um auxiliar para exibir quanto tempo passou até um ponto de interrupção, após o qual um formato de data regular é exibido.

Por exemplo:

* 12 horas atrás
* 7 dias atrás

### Parâmetros {#parameters-8}

* **contexto**: Número

   Um tempo no passado para comparar com &quot;agora&quot;. O tempo é expresso como um deslocamento de milissegundo a partir de 1º de janeiro de 1970 (época).

* **daysCutoff**: Número

   O número de dias antes de alternar para uma data real. O padrão é 60.

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

Um auxiliar que codifica uma string de origem para conteúdo de elemento HTML para ajudar a proteger contra XSS.

NOTA: isso não é um validador e não deve ser usado para gravar valores de atributos.

### Parâmetros {#parameters-9}

* **contexto**: objeto

   O HTML a ser codificado.

### Exemplo {#example-6}

```
<p>{{xss-html forum-ugc}}</p>
```

## Xss-htmlAttr {#xss-htmlattr}

Um auxiliar que codifica uma string de origem para gravar em um valor de atributo HTML para ajudar a proteger contra XSS.

NOTA: isso não é um validador e não deve ser usado para gravar atributos acionáveis (href, src, manipuladores de eventos).

### Parâmetros {#parameters-10}

* **contexto**: Objeto

   O HTML a ser codificado.

### Exemplo {#example-7}

```
<div id={{xss-htmlAttr id}} />
```

## Xss-jsString {#xss-jsstring}

Um auxiliar que codifica uma string de origem para gravação no conteúdo da string JavaScript para ajudar a proteger contra XSS.

NOTA: isso não é um validador e não deve ser usado para gravar em JavaScript arbitrário.

### Parâmetros {#parameters-11}

* **contexto**: Objeto

   O HTML a ser codificado.

### Exemplo {#example-8}

```
var input = {{xss-jsString topic-title}}
```

## Xss-validHref {#xss-validhref}

Um auxiliar que apaga um URL para escrever como um valor HTML href ou atributo srce para ajudar a proteger contra XSS.

NOTA: isso pode retornar uma string vazia

### Parâmetros {#parameters-12}

* **contexto**: Objeto

   O URL para limpar.

### Exemplo {#example-9}

```
<a href="{{xss-validHref url}}">my link</a>
```

## Visão geral básica do Handlebars.js {#handlebars-js-basic-overview}

Uma rápida visão geral das funções de ajuda da documentação [](https://handlebarsjs.com/expressions.html)do Handlebars.js:

* Uma chamada de ajuda Handlebars é um identificador simples (o *nome* do auxiliar), seguido por zero ou mais parâmetros separados por espaço.
* Os parâmetros podem ser um simples objeto String, number, boolean ou JSON, bem como uma sequência opcional de pares de chave-valor (argumentos hash) como o(s) último(s) parâmetro(s).
* As chaves nos argumentos hash devem ser identificadores simples.
* Os valores nos argumentos hash são expressões Handlebars: identificadores simples, caminhos ou strings.
* O contexto atual, `this`, está sempre disponível para os ajudantes do Handlebars.
* O contexto pode ser uma String, um número, um booleano ou um objeto de dados JSON.
* É possível passar um objeto aninhado dentro do contexto atual como o contexto, como `this.url` ou `this.id` (consulte os exemplos a seguir de ajuda simples e de bloqueio).

* Os auxiliares de bloco são funções que podem ser chamadas de qualquer lugar no modelo. Eles podem invocar um bloco do modelo zero ou mais vezes com um contexto diferente a cada vez. Elas contêm um contexto entre {{#*name*}} e {{/*name*}}.

* O Handlebars fornece um parâmetro final para os auxiliares chamados de &quot;opções&quot;. As &quot;opções&quot; do objeto especial incluem

   * Dados privados opcionais (options.data)
   * Propriedades opcionais do valor da chave da chamada (options.hash)
   * Capacidade de invocar a si mesmo (options.fn())
   * Capacidade de invocar o inverso de si mesmo (options.inverse())

* Recomenda-se que o conteúdo da string HTML retornado de um auxiliar seja uma SafeString.

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

&lt;ul>&lt;li>&lt;a href=&quot;/posts/hello-world&quot;>Postar!&lt;/a>&lt;/li>&lt;/ul>

### Um exemplo de um auxiliar de bloco da documentação do Handlebars.js: {#an-example-of-a-block-helper-from-handlebars-js-documentation}

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
&lt;ul>&lt;li>&lt;a href=&quot;/people/1&quot;>Alan&lt;/a>&lt;/li>&lt;li>&lt;a href=&quot;/people/2&quot;>Yehuda&lt;/a>&lt;/li>&lt;/ul>

## Auxiliares SCF personalizados {#custom-scf-helpers}

Os auxiliares personalizados devem ser implementados no lado do servidor e no lado do cliente, especialmente ao transmitir dados. Para SCF, a maioria dos modelos são compilados e renderizados no lado do servidor, já que o servidor gera o HTML para um determinado componente quando a página é solicitada.

### Auxiliares personalizados do servidor {#server-side-custom-helpers}

Para implementar e registrar um auxiliar SCF personalizado no lado do servidor, basta implementar o [TemplateHelper](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/handlebars/api/TemplateHelper.html)da interface Java, torná-lo um serviço [](../../help/sites-developing/the-basics.md#osgi) OSGi e instalá-lo como parte de um pacote OSGi.

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

### Ajuda personalizada do lado do cliente {#client-side-custom-helpers}

Os auxiliares do cliente são scripts Handlebars registrados chamando `Handlebars.registerHelper()`.
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

Os auxiliares personalizados do cliente devem ser adicionados a uma biblioteca personalizada do cliente.
A clientlib deve:

* Incluir uma dependência em `cq.social.scf`.
* Carregar após o carregamento dos Handlebars.
* Seja [incluído](clientlibs.md).

Observação: os auxiliares do quadro SEPA estão definidos em `/etc/clientlibs/social/commons/scf/helpers.js`.

| **[⇐ Fundamentos de recursos](essentials.md)** | **[Utilitário de personalização do servidor](server-customize.md)** |
|---|---|
|  | **[Localização da personalização do cliente](client-customize.md)** |

