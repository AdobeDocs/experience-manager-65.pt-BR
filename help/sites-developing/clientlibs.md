---
title: Usando bibliotecas do lado do cliente
seo-title: Usando bibliotecas do lado do cliente
description: AEM fornece as Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente
seo-description: AEM fornece as Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: f0dc620926a3ba2558313153f7a0fd3f8cd3c712
workflow-type: tm+mt
source-wordcount: '2740'
ht-degree: 0%

---


# Usando bibliotecas do lado do cliente{#using-client-side-libraries}

Sites modernos dependem muito do processamento no cliente, conduzido por códigos complexos de JavaScript e CSS. Organizar e otimizar a entrega desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, o AEM fornece pastas **de biblioteca do lado do** cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos em sua página final para carregar o código correto.

## Como as bibliotecas do lado do cliente funcionam em AEM {#how-client-side-libraries-work-in-aem}

A maneira padrão de incluir uma biblioteca do lado do cliente (ou seja, um arquivo JS ou CSS) no HTML de uma página é simplesmente incluir uma `<script>` ou `<link>` tag no JSP para essa página, contendo o caminho para o arquivo em questão. Por exemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Embora essa abordagem funcione em AEM, pode causar problemas quando as páginas e seus componentes se tornam complexos. Nesses casos, há o perigo de várias cópias da mesma biblioteca JS poderem ser incluídas na saída HTML final. Para evitar isso e permitir a organização lógica de bibliotecas do lado do cliente, AEM usa pastas **de biblioteca do lado do** cliente.

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. A definição na notação [](https://jackrabbit.apache.org/node-type-notation.html) CND é

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Por padrão, `cq:ClientLibraryFolder` os nós podem ser colocados em qualquer lugar dentro das `/apps`subárvores `/libs` e `/etc` do repositório (esses padrões e outras configurações podem ser controladas pelo painel **Adobe Granite HTML Library Manager** do Console [do](https://localhost:4502/system/console/configMgr)sistema).

Cada um `cq:ClientLibraryFolder` é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades do `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `categories`: Identifica as categorias nas quais o conjunto de arquivos JS e/ou CSS nesse `cq:ClientLibraryFolder` intervalo. A `categories` propriedade, sendo de vários valores, permite que uma pasta da biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais esta pasta da biblioteca depende. Por exemplo, dados dois `cq:ClientLibraryFolder` nós `F` e `G`, se um arquivo em `F` requer outro arquivo `G` para funcionar corretamente, então pelo menos um dos `categories` nós `G` deve estar entre os `dependencies` de `F`.

* `embed`: Usado para incorporar código de outras bibliotecas. Se o nó F incorporar os nós G e H, o HTML resultante será uma concentração de conteúdo dos nós G e H.
* `allowProxy`: Se uma biblioteca do cliente estiver localizada em `/apps`, essa propriedade permitirá o acesso a ela por meio do servlet proxy. Consulte [Localizando uma pasta da biblioteca do cliente e Usando o Servlet](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) de bibliotecas do cliente proxy abaixo.

## Referência a bibliotecas do lado do cliente {#referencing-client-side-libraries}

Como o HTL é a tecnologia preferida para desenvolver sites AEM, o HTL deve ser usado para incluir bibliotecas do lado do cliente no AEM. No entanto, também é possível fazê-lo usando a JSP.

### Uso de HTL {#using-htl}

Em HTL, as bibliotecas do cliente são carregadas por meio de um modelo auxiliar fornecido pela AEM, que pode ser acessado por meio [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Três modelos estão disponíveis neste arquivo, que pode ser chamado por meio [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)de:

* **css** - carrega somente os arquivos CSS das bibliotecas de clientes referenciadas.
* **js** - carrega somente os arquivos JavaScript das bibliotecas de clientes referenciadas.
* **all** - Carrega todos os arquivos das bibliotecas de cliente referenciadas (CSS e JavaScript).

Cada modelo de ajuda espera uma `categories` opção para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de string ou uma string contendo uma lista de valores separados por vírgula.

Para obter mais detalhes e exemplos de uso, consulte a [Introdução do documento à Linguagem](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries)de modelo HTML.

### Uso do JSP {#using-jsp}

Adicione uma `ui:includeClientLib` tag ao código JSP para adicionar um link às bibliotecas do cliente na página HTML gerada. Para fazer referência às bibliotecas, use o valor da `categories` propriedade do `ui:includeClientLib` nó.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por exemplo, o `/etc/clientlibs/foundation/jquery` nó é do tipo `cq:ClientLibraryFolder` com uma propriedade de valor do categoria `cq.jquery`. O código a seguir em um arquivo JSP faz referência às bibliotecas:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

A página HTML gerada contém o seguinte código:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Para obter informações completas, incluindo atributos para filtrar JS, CSS ou bibliotecas de temas, consulte [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, que no passado costumava ser usada para incluir bibliotecas de clientes, foi substituída desde AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) em vez disso, conforme detalhado acima.

## Criando Pastas de Biblioteca de Clientes {#creating-client-library-folders}

Crie um `cq:ClientLibraryFolder` nó para definir bibliotecas JavaScript e Folha de estilos em cascata e disponibilizá-las para páginas HTML. Use a `categories` propriedade do nó para identificar as categorias de biblioteca às quais ele pertence.

O nó contém um ou mais arquivos de origem que, em tempo de execução, são mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a extensão do nome do arquivo `.js` ou `.css` . Por exemplo, o nó da biblioteca nomeado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca do cliente contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS a serem mesclados.
* Recursos que suportam estilos CSS, como arquivos de imagem.

   **Observação:** Você pode usar subpastas para organizar arquivos de origem.
* Um `js.txt` arquivo e/ou um `css.txt` arquivo que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados.

![clientlibarch](assets/clientlibarch.png)

Para obter informações sobre os requisitos específicos das bibliotecas clientes para widgets, consulte [Uso e extensão de widgets](/help/sites-developing/widgets.md).

O cliente Web deve ter permissões para acessar o `cq:ClientLibraryFolder` nó. Você também pode expor bibliotecas de áreas protegidas do repositório (consulte Incorporação de código a partir de outras bibliotecas, abaixo).

### Substituição de bibliotecas em /lib {#overriding-libraries-in-lib}

As pastas da biblioteca do cliente localizadas abaixo `/apps` têm prioridade sobre as pastas com o mesmo nome que estão localizadas da mesma forma em `/libs`. Por exemplo, `/apps/cq/ui/widgets` tem precedência sobre `/libs/cq/ui/widgets`. Quando essas bibliotecas pertencem à mesma categoria, a biblioteca abaixo `/apps` é usada.

### Localizando uma pasta da biblioteca do cliente e usando o servlet de bibliotecas do cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Em versões anteriores, as pastas da biblioteca do cliente estavam localizadas abaixo `/etc/clientlibs` no repositório. Isso ainda é suportado, mas é recomendável que as bibliotecas do cliente agora estejam localizadas em `/apps`. Isso serve para localizar as bibliotecas do cliente perto dos outros scripts, que geralmente são encontrados abaixo `/apps` e `/libs`.

>[!NOTE]
>
>Os recursos estáticos abaixo da pasta da biblioteca do cliente devem estar em uma pasta chamada *resources*. Se você não tiver os recursos estáticos, como imagens, nos *recursos* da pasta, eles não poderão ser referenciados em uma instância de publicação. Veja um exemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para isolar melhor o código do conteúdo e da configuração, é recomendável localizar as bibliotecas do cliente em `/apps` e expô-las por meio `/etc.clientlibs` da utilização da `allowProxy` propriedade.

Para que as bibliotecas do cliente possam `/apps` ser acessadas, um servidor proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a `allowProxy` propriedade estiver definida como `true`.

Um recurso estático só pode ser acessado por meio do proxy, se ele residir abaixo de um recurso abaixo da pasta da biblioteca do cliente.

Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

Em seguida, você define a `allowProxy` propriedade como true `foo` .

* Você pode solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Você pode fazer referência à imagem via `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Ao usar bibliotecas de clientes proxy, a configuração do Dispatcher AEM pode exigir uma atualização para garantir que os URIs com as clientlibs de extensão sejam permitidos.

>[!CAUTION]
>
>A Adobe recomenda localizar as bibliotecas do cliente em `/apps` e disponibilizá-las usando o servlet proxy. No entanto, lembre-se de que as práticas recomendadas ainda exigem que os sites públicos nunca incluam nada que seja servido diretamente sobre um `/apps` caminho ou `/libs` caminho.

### Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

1. Abra o CRXDE Lite em um navegador da Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selecione a pasta na qual deseja localizar a pasta da biblioteca do cliente e clique em **Criar > Criar nó**.
1. Digite um nome para o arquivo da biblioteca e, na opção lista Tipo, selecione `cq:ClientLibraryFolder`. Clique em **OK** e em **Salvar tudo**.
1. Para especificar a categoria ou as categorias às quais a biblioteca pertence, selecione o `cq:ClientLibraryFolder` nó, adicione a seguinte propriedade e clique em **Salvar tudo**:

   * Nome: categorias
   * Tipo: String
   * Valor: O nome da categoria
   * Vários: Selecionar

1. Adicione os arquivos de origem à pasta da biblioteca por qualquer meio. Por exemplo, use um cliente WebDav para copiar arquivos ou crie um arquivo e crie o conteúdo manualmente.

   **Observação:** Se desejar, você pode organizar os arquivos de origem em subpastas.

1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:

   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma folha de estilos em cascata.

1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:

   `#base=*[root]*`

   Substitua * `[root]`* pelo caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta que o arquivo TXT:

   `#base=.`

   O código a seguir define a raiz como a pasta chamada mobile abaixo do `cq:ClientLibraryFolder` nó:

   `#base=mobile`

1. Nas linhas abaixo `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. No JSP, a `ui:includeClientLib` tag que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao seu `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categoria do nó cq:ClientLibraryFolder do qual a pasta da biblioteca atual depende.

Por exemplo, o / `etc/clientlibs/myclientlibs/publicmain` tem uma dependência na `cq.jquery` biblioteca. O JSP que faz referência à biblioteca principal do cliente gera HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporação de código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar código de uma biblioteca de cliente em outra biblioteca de cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso às bibliotecas que são armazenadas em áreas protegidas do repositório.

#### Pastas da biblioteca de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados ao aplicativo em sua pasta de aplicativos abaixo `/app`. Também é uma prática recomendada negar o acesso de visitantes do site à `/app` pasta. Para satisfazer ambas as práticas recomendadas, crie uma pasta da biblioteca do cliente abaixo da `/etc` pasta que incorpora a biblioteca do cliente abaixo `/app`.

Use a propriedade categoria para identificar a pasta da biblioteca do cliente a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade ao `cq:ClientLibraryFolder` nó de incorporação, usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** String[]
* **Valor:** O valor da propriedade categoria do `cq:ClientLibraryFolder` nó a ser incorporado.

<!-- #### Using Embedding to Minimize Requests {#using-embedding-to-minimize-requests}

In some cases you may find that the final HTML generated for typical page by your publish instance includes a relatively large number of `<script>` elements, particularly if your site is using client context information for analaytics or targeting. For example, in a non-optimized project you might find the following series of `<script>` elements in the HTML for a page:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/underscore.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

In such cases, it can be useful to combine all the required client library code in to a single file so that the number of back and forth requests on page load is reduced. To do this you can `embed` the required libraries into you app-specific client library using the embed property of the `cq:ClientLibraryFolder` node.

The following client library categories are incuded with AEM. You should embed only those that are required for he functioning of your particular site. However, **you should maintain the order listed here**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

EDITOR NOTE: removed as requested on CQDOC-16765

-->

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível ao público `/etc/client/libraries/myclientlibs/publicmain` incorpora a biblioteca do `/apps/myapp/clientlib` cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

O `main.css` arquivo contém o seguinte estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS gerado pelo `publicmain` nó contém o seguinte estilo, usando o URL da imagem original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Uso de uma biblioteca para grupos móveis específicos {#using-a-library-for-specific-mobile-groups}

Use a `channels` propriedade de uma pasta da biblioteca do cliente para identificar o grupo móvel que usa a biblioteca. A `channels` propriedade é útil quando bibliotecas da mesma categoria são projetadas para diferentes recursos do dispositivo.

Para associar uma pasta da biblioteca do cliente a um grupo de dispositivos, adicione uma propriedade ao seu `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** canais
* **Tipo:** String[]
* **Valores:** O nome do grupo móvel. Para excluir a pasta da biblioteca de um grupo, prefixe o nome com um ponto de exclamação (&quot;!&quot;).

Por exemplo, a tabela a seguir lista o valor da `channels` propriedade para cada pasta da biblioteca do cliente da `cq.widgets` categoria:

| Pasta da biblioteca do cliente | Valor da propriedade canais |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[sem valor]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## Uso de pré-processadores {#using-preprocessors}

AEM permite pré-processadores e entregas conectáveis com suporte para o [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e o [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores podem ser configurados com opções
* Os processadores podem ser usados para a miniificação, mas também para casos não-reduzidos
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, AEM usa o Compressor YUI. Consulte a documentação [do](https://github.com/yui/yuicompressor/issues) YUI Compressor GitHub para obter uma lista de problemas conhecidos. Mudar para o compressor GCC para clientlibs específicos pode resolver alguns problemas observados ao utilizar IU.

>[!CAUTION]
>
>Não coloque uma biblioteca minimizada em uma biblioteca cliente. Em vez disso, forneça a biblioteca bruta e, se for necessário a miniificação, use as opções dos pré-processadores.

### Uso {#usage}

Você pode optar por configurar a configuração dos pré-processadores por biblioteca do cliente ou por todo o sistema.

* Adicionar as propriedades multivalue `cssProcessor` e `jsProcessor` no nó clientlibrary

* Ou defina a configuração padrão do sistema por meio da configuração OSGi do Gerenciador **de biblioteca** HTML

Uma configuração de pré-processador no nó clientlib tem prioridade sobre a configuração OSGI.

### Formato e exemplos {#format-and-examples}

#### Formato {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### Compressor YUI para Minificação CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Digitar para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Opções adicionais do GCC {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obter mais detalhes sobre as opções de GCC, consulte a documentação [do](https://developers.google.com/closure/compiler/docs/compilation_levels)GCC.

### Definir Miniador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como a miniatura padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Vá para o Apache Felix Config Manager em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localize e edite o Gerenciador **de biblioteca HTML** Granite.
1. Ative a **opção Minifique** (se ainda não estiver ativada).
1. Defina o valor Configurações padrão do processador **JS** como `min:gcc`.

   As opções podem ser passadas se separadas por um ponto-e-vírgula, por exemplo `min:gcc;obfuscate=true`.

1. Click **Save** to save the changes.

## Ferramentas de depuração {#debugging-tools}

AEM fornece várias ferramentas para depurar e testar pastas da biblioteca do cliente.

### Consulte Arquivos incorporados {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas produzam os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe o `debugClientLibs=true` parâmetro ao URL da sua página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo na seção anterior [Incorporar código de outras bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) , a pasta da biblioteca do `/etc/client/libraries/myclientlibs/publicmain` cliente incorpora a pasta da biblioteca do `/apps/myapp/clientlib` cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

A abertura do `publicmain.css` arquivo revela o seguinte código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:

   `?debugClientLibs=true`
1. Quando a página for carregada, visualização a fonte da página.
1. Clique no link fornecido como href para o elemento de link para abrir o arquivo e visualização o código fonte.

### Bibliotecas do Discover Client {#discover-client-libraries}

O `/libs/cq/granite/components/dumplibs/dumplibs` componente gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O `/libs/granite/ui/content/dumplibs` nó tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O `dumplibs` componente inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` as tags. A página inclui código para diferentes combinações de atributos js, css e temáticos.

1. Use um dos seguintes métodos para abrir a página Saída de teste:

   * Na `dumplibs.html` página, clique no link no texto **Clique aqui para teste** de saída.

   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   A página padrão mostra a saída de tags sem valor para o atributo categoria.

1. Para ver a saída de uma categoria, digite o valor da propriedade da biblioteca do cliente `categories` e clique em **Enviar Query**.

## Configuração do manuseio de biblioteca para desenvolvimento e produção {#configuring-library-handling-for-development-and-production}

O serviço Gerenciador de biblioteca HTML processa `cq:ClientLibraryFolder` tags e gera as bibliotecas em tempo de execução. O tipo de ambiente, desenvolvimento ou produção determina como você deve configurar o serviço:

* Aumente a segurança: Desativar depuração
* Melhore o desempenho: Remova o espaço em branco e compacte as bibliotecas.
* Melhore a legibilidade: Inclua espaços em branco e não compacte.

Para obter informações sobre como configurar o serviço, consulte [AEM Gerenciador](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)de biblioteca HTML.
