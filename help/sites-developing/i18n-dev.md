---
title: Internacionalizando strings de interface do usuário
seo-title: Internationalizing UI Strings
description: As APIs Java e Javascript permitem internacionalizar strings
seo-description: Java and Javascript APIs enable you to internationalize strings
uuid: 1cfa409f-9b1e-466f-8b03-5628db42bc57
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 9da8823c-13a4-4244-bfab-a910a4fd44e7
exl-id: bc5b1cb7-a011-42fe-8759-3c7ee3068aad
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 0%

---

# Internacionalizando strings de interface do usuário {#internationalizing-ui-strings}

As APIs Java e Javascript permitem internacionalizar strings nos seguintes tipos de recursos:

* Arquivos de código-fonte Java.
* Scripts JSP.
* Javascript em bibliotecas do lado do cliente ou na origem da página.
* Valores de propriedade do nó JCR usados em caixas de diálogo e propriedades de configuração do componente.

Para obter uma visão geral do processo de internacionalização e localização, consulte [Internacionalizar componentes](/help/sites-developing/i18n.md).

## Internacionalizando strings em código Java e JSP {#internationalizing-strings-in-java-and-jsp-code}

A variável `com.day.cq.i18n` O pacote Java permite exibir strings localizadas na interface do usuário. A variável `I18n` A classe fornece a `get` método que recupera strings localizadas do dicionário AEM. O único parâmetro obrigatório do `get` method é a cadeia de caracteres literal no idioma inglês. O inglês é o idioma padrão da interface do usuário do. O exemplo a seguir localiza a palavra `Search`:

`i18n.get("Search");`

A identificação da sequência de caracteres no idioma inglês difere das estruturas de internacionalização típicas, onde um ID identifica uma sequência de caracteres e é usado para fazer referência à sequência de caracteres no tempo de execução. Usar o literal de string em inglês oferece os seguintes benefícios:

* O código é fácil de entender.
* A cadeia de caracteres no idioma padrão está sempre disponível.

### Determinar o idioma do usuário {#determining-the-user-s-language}

Há duas maneiras de determinar o idioma preferido pelo usuário:

* Para usuários autenticados, determine o idioma nas preferências da conta do usuário.
* A localidade da página solicitada.

A propriedade language da conta do usuário é o método preferido porque é mais confiável. No entanto, o usuário deve estar conectado para usar esse método.

#### Criação do objeto Java I18n {#creating-the-i-n-java-object}

A classe I18n fornece dois construtores. A maneira como você determina a linguagem preferencial do usuário determina o construtor a ser usado.

Para apresentar a cadeia de caracteres no idioma especificado na conta do usuário, use o seguinte construtor (após a importação `com.day.cq.i18n.I18n)`:

```java
I18n i18n = new I18n(slingRequest);
```

O construtor usa o `SlingHTTPRequest` para recuperar a configuração de idioma do usuário.

Para usar o locale da página para determinar o idioma, primeiro é necessário obter o ResourceBundle para o idioma da página solicitada:

```java
Locale pageLang = currentPage.getLanguage(false);
ResourceBundle resourceBundle = slingRequest.getResourceBundle(pageLang);
I18n i18n = new I18n(resourceBundle);
```

#### Internacionalizando uma string {#internationalizing-a-string}

Use o `get` método do `I18n` para internacionalizar uma string. O único parâmetro obrigatório do `get` é a sequência de caracteres a ser internacionalizada. A string corresponde a uma string em um dicionário do Translator. O método get pesquisa a string no dicionário e retorna a tradução para o idioma atual.

O primeiro argumento do `get` deve estar em conformidade com as seguintes regras:

* O valor deve ser um literal de cadeia de caracteres. Uma variável do tipo `String` não é aceitável.
* O literal da cadeia de caracteres deve ser expresso em uma única linha.
* A cadeia de caracteres diferencia maiúsculas de minúsculas.

```xml
i18n.get("Enter a search keyword");
```

#### Uso de dicas de tradução {#using-translation-hints}

Especifique a [dica de tradução](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings) da string internacionalizada para distinguir entre strings duplicadas no dicionário. Use o segundo parâmetro opcional do `get` para fornecer a dica de tradução. A dica de tradução deve corresponder exatamente à propriedade Comentário do item no dicionário.

Por exemplo, o dicionário contém a string `Request` duas vezes: uma como verbo e outra como substantivo. O código a seguir inclui a dica de tradução como argumento na variável `get` método:

```java
i18n.get("Request","A noun, as in a request for a web page");
```

#### Inclusão de variáveis em frases localizadas {#including-variables-in-localized-sentences}

Inclua variáveis na string localizada para criar significado contextual em uma frase. Por exemplo, depois de fazer logon em um aplicativo web, a página inicial exibe a mensagem &quot;Bem-vindo de volta, Administrador. Você tem duas mensagens na sua caixa de entrada.&quot; O contexto da página determina o nome de usuário e o número de mensagens.

[No dicionário](/help/sites-developing/i18n-translator.md#adding-changing-and-removing-strings), as variáveis são representadas em strings como índices entre colchetes. Especifique os valores das variáveis como argumentos da variável `get` método. Os argumentos são colocados após a dica de tradução e os índices correspondem à ordem dos argumentos:

```xml
i18n.get("Welcome back {0}. You have {1} messages.", "user name, number of messages", user.getDisplayName(), numItems);
```

A string internacionalizada e a dica de tradução devem corresponder exatamente à string e ao comentário no dicionário. Você pode omitir a dica de localização fornecendo um `null` como o segundo argumento.

#### Uso do Método Get Estático {#using-the-static-get-method}

A variável `I18N` define um parâmetro estático `get` que é útil quando você precisa localizar um pequeno número de strings. Além dos parâmetros de um objeto `get` , o método estático exige o `SlingHttpRequest` ou o `ResourceBundle` que você está usando, de acordo com a forma como está determinando o idioma preferido do usuário:

* Usar a preferência de idioma do usuário: forneça o SlingHttpRequest como o primeiro parâmetro.

   `I18n.get(slingHttpRequest, "Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`
* Usar a linguagem da página: forneça o ResourceBundle como o primeiro parâmetro.

   `I18n.get(resourceBundle,"Welcome back {}. You have {} messages.", "user name, number of messages", user.getDisplayName(), numItems);`

### Internacionalizando strings no código Javascript {#internationalizing-strings-in-javascript-code}

A API do Javascript permite localizar strings no cliente. Assim como com [Java e JSP](#internationalizing-strings-in-java-and-jsp-code) , a API JavaScript permite identificar strings para localização, fornecer dicas de localização e incluir variáveis nas strings localizadas.

A variável `granite.utils` [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md) O fornece a API do Javascript. Para usar a API, inclua essa pasta da biblioteca do cliente na sua página. As funções de localização usam o `Granite.I18n` namespace.

Antes de apresentar strings localizadas, é necessário definir o local usando o `Granite.I18n.setLocale` função. A função requer o código de idioma do local como argumento:

```
Granite.I18n.setLocale("fr");
```

Para apresentar uma string localizada, use o `Granite.I18n.get` função:

```
Granite.I18n.get("string to localize");
```

O exemplo a seguir internacionaliza a string &quot;Bem-vindo de volta&quot;:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("string to localize", [variables], "localization hint");
```

Os parâmetros da função são diferentes do método Java I18n.get:

* O primeiro parâmetro é o literal da string a ser localizado.
* O segundo parâmetro é uma matriz de valores a serem inseridos no literal da string.
* O terceiro parâmetro é a dica de localização.

O exemplo a seguir usa o Javascript para localizar o Administrador de &quot;Boas-vindas de volta&quot;. Você tem duas mensagens na sua caixa de entrada.&quot; frase:

```
Granite.I18n.setLocale("fr");
Granite.I18n.get("Welcome back {0}. You have {1} new messages in your inbox.", [username, numMsg], "user name, number of messages");
```

### Internacionalizando strings de nós JCR {#internationalizing-strings-from-jcr-nodes}

As cadeias de caracteres da interface do usuário geralmente se baseiam nas propriedades do nó JCR. Por exemplo, a variável `jcr:title` propriedade de uma página é normalmente usada como o conteúdo da variável `h1` elemento no código da página. A variável `I18n` A classe fornece a `getVar` método para localizar essas cadeias de caracteres.

O exemplo de script JSP a seguir recupera o `jcr:title` do repositório e exibe a cadeia de caracteres localizada na página:

```java
<% title = properties.get("jcr:title", String.class);%>
<h1><%=i18n.getVar(title) %></h1>
```

#### Especificando dicas de tradução para nós JCR {#specifying-translation-hints-for-jcr-nodes}

Semelhante [dicas de tradução na API Java](#using-translation-hints), você pode fornecer dicas de tradução para distinguir cadeias de caracteres duplicadas no dicionário. Forneça a dica de tradução como uma propriedade do nó que contém a propriedade internacionalizada. O nome da propriedade de dica é composto do nome da propriedade internacionalizada com a variável `_commentI18n` sufixo:

`${prop}_commentI18n`

Por exemplo, uma variável `cq:page` O nó inclui a propriedade jcr:title que está sendo localizada. A dica é fornecida como o valor da propriedade chamada jcr:title_commentI18n.

### Testar cobertura de internacionalização {#testing-internationalization-coverage}

Teste se você internacionalizou todas as strings na interface do usuário. Para ver quais cadeias de caracteres são cobertas, defina o idioma do usuário como zz_ZZ e abra a interface do usuário no navegador da Web. As strings internacionalizadas são exibidas com uma tradução de stub no seguinte formato:

`USR_*Default-String*_尠`

A imagem a seguir mostra a tradução de stub para a página inicial do AEM:

![chlimage_1](assets/chlimage_1a.jpeg)

Para definir o idioma do usuário, configure a propriedade language do nó de preferências para a conta do usuário.

O nó de preferências de um usuário tem um caminho como este:

`/home/users/<letter>/<hash>/preferences`

![chlimage_1-1](assets/chlimage_1-1a.jpeg)
