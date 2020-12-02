---
title: Internacionalização de strings de interface
seo-title: Internacionalização de strings de interface
description: APIs Java e JavaScript permitem internacionalizar strings
seo-description: APIs Java e JavaScript permitem internacionalizar strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---


# Internacionalizando strings de interface {#internationalizing-ui-strings}

As APIs Java e Javascript permitem que você internacionalize strings nos seguintes tipos de recursos:

* Arquivos de código-fonte Java.
* Scripts JSP.
* Javascript em bibliotecas do lado do cliente ou na fonte da página.
* Valores de propriedade do nó JCR usados em caixas de diálogo e propriedades de configuração do componente.

Para obter uma visão geral do processo de internacionalização e localização, consulte [Internacionalizando componentes](/help/sites-developing/i18n.md).

## Internacionalização de strings no código Java e JSP {#internationalizing-strings-in-java-and-jsp-code}

O pacote Java `com.day.cq.i18n` permite que você exiba strings localizadas na interface do usuário. A classe `I18n` fornece o método `get` que recupera strings localizadas do dicionário AEM. O único parâmetro obrigatório do método `get` é o literal de string no idioma inglês. Inglês é o idioma padrão para a interface do usuário. O exemplo a seguir localiza a palavra `Search`:

`i18n.get("Search");`

A identificação da string no idioma inglês difere das estruturas de internacionalização típicas, onde uma ID identifica uma string e é usada para referenciar a string no tempo de execução. O uso do literal de string em inglês oferece os seguintes benefícios:

* O código é fácil de entender.
* A string no idioma padrão está sempre disponível.

### Determinando o Idioma do Usuário {#determining-the-user-s-language}

Há duas maneiras de determinar o idioma preferido pelo usuário:

* Para usuários autenticados, determine o idioma a partir das preferências na conta de usuário.
* A localidade da página solicitada.

A propriedade language da conta do usuário é o método preferencial, pois é mais confiável. No entanto, o usuário deve estar conectado para usar esse método.

#### Criação do objeto Java I18n {#creating-the-i-n-java-object}

A classe I18n fornece dois construtores. Como determinar o idioma preferencial do usuário determina o construtor a ser usado.

Para apresentar a string no idioma especificado na conta de usuário, use o seguinte construtor (após importar `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

O construtor usa `SlingHTTPRequest` para recuperar a configuração de idioma do usuário.

Para usar a localidade da página para determinar o idioma, primeiro é necessário obter o ResourceBundle para o idioma da página solicitada:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internacionalizando uma string {#internationalizing-a-string}

Use o método `get` do objeto `I18n` para internacionalizar uma string. O único parâmetro obrigatório do método `get` é a string a ser internacionalizada. A string corresponde a uma string em um dicionário do Tradutor. O método get procura a string no dicionário e retorna a tradução para o idioma atual.

O primeiro argumento do método `get` deve estar em conformidade com as seguintes regras:

* O valor deve ser um literal de string. Uma variável do tipo `String` não é aceitável.
* O literal de string deve ser expresso em uma única linha.
* A string faz distinção entre maiúsculas e minúsculas.

```xml
i18n.get("Enter a search keyword");
```

#### Usando dicas de tradução {#using-translation-hints}

Especifique a [dica de conversão](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) da cadeia de caracteres internacionalizada para distinguir entre cadeias de duplicados no dicionário. Use o segundo parâmetro opcional do método `get` para fornecer a dica de conversão. A dica de conversão deve corresponder exatamente à propriedade Comentário do item no dicionário.

Por exemplo, o dicionário contém a string `Request` duas vezes: uma vez como verbo e uma vez como substantivo. O código a seguir inclui a dica de conversão como um argumento no método `get`:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Incluindo variáveis em frases localizadas {#including-variables-in-localized-sentences}

Inclua variáveis na string localizada para criar significado contextual em uma sentença. Por exemplo, depois de fazer logon em um aplicativo da Web, o home page exibe a mensagem &quot;Bem-vindo ao administrador. Você tem duas mensagens na sua caixa de entrada.&quot; O contexto da página determina o nome do usuário e o número de mensagens.

[No dicionário](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), as variáveis são representadas em strings como índices entre colchetes. Especifique os valores das variáveis como argumentos do método `get`. Os argumentos são colocados após a dica de tradução, e os índices correspondem à ordem dos argumentos:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

A string internacionalizada e a dica de tradução devem corresponder exatamente à string e ao comentário no dicionário. Você pode omitir a dica de localização fornecendo um valor `null` como segundo argumento.

#### Usando o Método Static Get {#using-the-static-get-method}

A classe `I18N` define um método estático `get` que é útil quando você precisa localizar um pequeno número de strings. Além dos parâmetros do método `get` de um objeto, o método estático exige o objeto `SlingHttpRequest` ou `ResourceBundle` que você está usando, de acordo com a forma como está determinando o idioma preferencial do usuário:

* Use a preferência de idioma do usuário: Forneça SlingHttpRequest como o primeiro parâmetro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Use o idioma da página: Forneça o ResourceBundle como o primeiro parâmetro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internacionalizando strings no código JavaScript {#internationalizing-strings-in-javascript-code}

A API do Javascript permite que você localize sequências de caracteres no cliente. Assim como com os códigos [Java e JSP](#internationalizing-strings-in-java-and-jsp-code), a API do Javascript permite identificar strings para localizar, fornecer dicas de localização e incluir variáveis nas strings localizadas.

A `granite.utils` [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md) fornece a API do Javascript. Para usar a API, inclua esta pasta da biblioteca de cliente na sua página. As funções de localização usam a namespace `Granite.I18n`.

Antes de apresentar strings localizadas, é necessário definir a localidade usando a função `Granite.I18n.setLocale`. A função requer o código de idioma da localidade como um argumento:

```
Granite.I18n.setLocale("fr");
```

Para apresentar uma string localizada, use a função `Granite.I18n.get`:

```
Granite.I18n.get("string to localize");
```

O exemplo a seguir internacionaliza a string &quot;Bem-vindo de volta&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Os parâmetros de função são diferentes do método Java I18n.get:

* O primeiro parâmetro é o literal de string a ser localizado.
* O segundo parâmetro é uma matriz de valores a serem injetados no literal de string.
* O terceiro parâmetro é a dica de localização.

O exemplo a seguir usa o Javascript para localizar o &quot;Welcome back Administrator&quot;. Você tem duas mensagens na sua caixa de entrada.&quot; frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internacionalizando strings de nós JCR {#internationalizing-strings-from-jcr-nodes}

As sequências de caracteres da interface geralmente têm por base as propriedades de nós do JCR. Por exemplo, a propriedade `jcr:title` de uma página geralmente é usada como o conteúdo do elemento `h1` no código da página. A classe `I18n` fornece o método `getVar` para localizar essas strings.

O script JSP de exemplo a seguir recupera a propriedade `jcr:title` do repositório e exibe a string localizada na página:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Especificação de dicas de tradução para nós JCR {#specifying-translation-hints-for-jcr-nodes}

Semelhante às dicas de tradução [na API Java](#using-translation-hints), você pode fornecer dicas de tradução para distinguir as sequências de duplicados no dicionário. Forneça a dica de conversão como uma propriedade do nó que contém a propriedade internacionalizada. O nome da propriedade de dica é composto do nome do nome da propriedade internacionalizada com o sufixo `_commentI18n`:

`${prop}_commentI18n`

Por exemplo, um nó `cq:page` inclui a propriedade jcr:title que está sendo localizada. A dica é fornecida como o valor da propriedade chamada jcr:title_commentI18n.

### Teste da cobertura de internacionalização {#testing-internationalization-coverage}

Teste se você internacionalizou todas as strings na sua interface do usuário. Para ver quais strings são cobertas, defina o idioma do usuário como zz_ZZ e abra a interface no navegador da Web. As strings internacionalizadas são exibidas com uma tradução de stub no seguinte formato:

`USR_*Default-String*_尠`

A imagem a seguir mostra a tradução de stub para o home page AEM:

![chlimage_1](assets/chlimage_1a.jpeg)

Para definir o idioma para o usuário, configure a propriedade de idioma do nó de preferências para a conta do usuário.

O nó de preferências de um usuário tem um caminho como este:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)

