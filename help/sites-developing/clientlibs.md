---
title: Uso de bibliotecas do cliente
seo-title: Using Client-Side Libraries
description: O AEM fornece Pastas de bibliotecas do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 7ceee6819618d785f04029b9ac1c6f763995b3ac
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 2%

---

# Uso de bibliotecas do cliente{#using-client-side-libraries}

Sites modernos dependem muito do processamento do lado do cliente orientado por códigos JavaScript e CSS complexos. Organizar e otimizar a veiculação desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, o AEM fornece **Pastas de biblioteca do lado cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos na página da Web final para carregar o código correto.

## Como as bibliotecas do lado do cliente funcionam no AEM {#how-client-side-libraries-work-in-aem}

A maneira padrão de incluir uma biblioteca do lado do cliente (ou seja, um arquivo JS ou CSS) no HTML de uma página é simplesmente incluir uma `<script>` ou `<link>` no JSP dessa página, contendo o caminho para o arquivo em questão. Por exemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Embora essa abordagem funcione no AEM, ela pode levar a problemas quando as páginas e seus componentes se tornam complexos. Nesses casos, há o perigo de que várias cópias da mesma biblioteca JS possam ser incluídas na saída de HTML final. Para evitar isso e permitir a organização lógica de bibliotecas do lado do cliente, o AEM usa **pastas de biblioteca do lado do cliente**.

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. Sua definição está em [Notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Por padrão, `cq:ClientLibraryFolder` nós podem ser colocados em qualquer lugar dentro do `/apps`, `/libs` e `/etc` subárvores do repositório (esses padrões e outras configurações podem ser controlados por meio da **Gerenciador de biblioteca de HTML do Adobe Granite** painel da [Console do sistema](https://localhost:4502/system/console/configMgr)).

Each `cq:ClientLibraryFolder` O é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades da variável `cq:ClientLibraryFolder` são configurados da seguinte maneira:

* `categories`: identifica as categorias nas quais o conjunto de arquivos JS e/ou CSS dentro desse `cq:ClientLibraryFolder` outono. A variável `categories` por ter vários valores, permite que uma pasta da biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

* `dependencies`: esta é uma lista de outras categorias de bibliotecas de clientes das quais essa pasta de biblioteca depende. Por exemplo, dados dois `cq:ClientLibraryFolder` nós `F` e `G`, se um arquivo em `F` requer outro arquivo em `G` para funcionar corretamente, pelo menos um dos `categories` de `G` deve estar entre os `dependencies` de `F`.

* `embed`: usado para incorporar o código de outras bibliotecas do. Se o nó F incorporar os nós G e H, o HTML resultante será uma concentração de conteúdo dos nós G e H.
* `allowProxy`: se uma biblioteca do cliente estiver localizada em `/apps`, essa propriedade permite acesso a ela por meio do servlet proxy. Consulte [Localizar uma pasta de bibliotecas de clientes e usar o servlet de bibliotecas de clientes proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.

## Referência a bibliotecas do lado do cliente {#referencing-client-side-libraries}

Como HTL é a tecnologia preferida para o desenvolvimento de sites AEM, o HTL deve ser usado para incluir bibliotecas do lado do cliente no AEM. No entanto, também é possível fazer isso usando o JSP.

### Uso do HTL {#using-htl}

No HTL, as bibliotecas do cliente são carregadas por meio de um modelo auxiliar fornecido pelo AEM, que pode ser acessado por meio de [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Três modelos estão disponíveis nesse arquivo, que pode ser chamado por meio de [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - carrega somente os arquivos CSS das bibliotecas de clientes referenciadas.
* **js** - carrega somente os arquivos JavaScript das bibliotecas de clientes referenciadas.
* **all** - carrega todos os arquivos das bibliotecas de clientes referenciadas (CSS e JavaScript).

Cada modelo auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de cadeias de caracteres ou uma cadeia contendo uma lista de valores separados por vírgula.

Para obter mais detalhes e exemplos de uso, consulte o documento [Introdução à Linguagem de modelo do HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Usando JSP {#using-jsp}

Adicionar um `ui:includeClientLib` para adicionar um link para as bibliotecas de clientes na página de HTML gerada. Para fazer referência às bibliotecas, use o valor do `categories` propriedade do `ui:includeClientLib` nó.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por exemplo, a variável `/etc/clientlibs/foundation/jquery` o nó é do tipo `cq:ClientLibraryFolder` com uma propriedade de categorias de valor `cq.jquery`. O código a seguir em um arquivo JSP faz referência às bibliotecas:

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

A página de HTML gerada contém o seguinte código:

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

Para obter informações completas, incluindo atributos para filtrar JS, CSS ou bibliotecas de temas, consulte [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`, que no passado era comumente usado para incluir bibliotecas de clientes, foi descontinuada desde o AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) deve ser usado em vez dos detalhados acima.

## Criação de pastas de bibliotecas de clientes {#creating-client-library-folders}

Criar um `cq:ClientLibraryFolder` nó para definir bibliotecas JavaScript e Folha de Estilos em Cascata e disponibilizá-las para páginas HTML. Use o `categories` propriedade do nó para identificar as categorias de biblioteca às quais ele pertence.

O nó contém um ou mais arquivos de origem que, no tempo de execução, são mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a variável `.js` ou `.css` extensão do nome do arquivo. Por exemplo, o nó de biblioteca chamado `cq.jquery` resultados no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca do cliente contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS que serão mesclados.
* Recursos que oferecem suporte a estilos CSS, como arquivos de imagem.

   **Nota:** Você pode usar subpastas para organizar arquivos de origem.
* Um `js.txt` arquivo e/ou um `css.txt` arquivo que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados.

![clientlibarch](assets/clientlibarch.png)

Para obter informações sobre os requisitos específicos das bibliotecas de clientes para widgets, consulte [Uso e extensão de widgets](/help/sites-developing/widgets.md).

O cliente Web deve ter permissões para acessar o `cq:ClientLibraryFolder` nó. Você também pode expor bibliotecas de áreas seguras do repositório (consulte Incorporação de código de outras bibliotecas, abaixo).

### Substituição de bibliotecas em /lib {#overriding-libraries-in-lib}

Pastas da biblioteca do cliente localizadas abaixo `/apps` têm precedência sobre pastas com o mesmo nome que estejam localizadas de forma semelhante em `/libs`. Por exemplo, `/apps/cq/ui/widgets` tem precedência sobre `/libs/cq/ui/widgets`. Quando essas bibliotecas pertencem à mesma categoria, a biblioteca abaixo `/apps` é usada.

### Localizar uma pasta de bibliotecas de clientes e usar o servlet de bibliotecas de clientes proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Em versões anteriores, as pastas da biblioteca do cliente estavam localizadas abaixo `/etc/clientlibs` no repositório. Isso ainda é suportado, no entanto, é recomendável que as bibliotecas de clientes agora estejam localizadas em `/apps`. Isso é para localizar as bibliotecas de clientes próximas aos outros scripts, que geralmente são encontrados abaixo `/apps` e `/libs`.

>[!NOTE]
>
>Os recursos estáticos abaixo da pasta da biblioteca do cliente devem estar em uma pasta chamada *recursos*. Se você não tiver os recursos estáticos, como imagens, na pasta *recursos*, ele não pode ser referenciado em uma instância de publicação. Veja um exemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para isolar melhor o código do conteúdo e da configuração, é recomendável localizar as bibliotecas de clientes em `/apps` e expô-los via `/etc.clientlibs` aproveitando o `allowProxy` propriedade.

Para que as bibliotecas de clientes em `/apps` para ser acessível, um servlet proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a variável `allowProxy` propriedade está definida como `true`.

Um recurso estático só pode ser acessado por meio do proxy se estiver abaixo de um recurso abaixo da pasta da biblioteca do cliente.

Como exemplo:

* Você tem uma clientlib no `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática no `/apps/myprojects/clientlibs/foo/resources/icon.png`

Em seguida, defina o `allowProxy` propriedade em `foo` para verdadeiro.

* Em seguida, você pode solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Você pode fazer referência à imagem por meio de `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Ao usar bibliotecas de clientes com proxy, a configuração do AEM Dispatcher pode exigir uma atualização para garantir que os URIs com a extensão clientlibs sejam permitidos.

>[!CAUTION]
>
>O Adobe recomenda localizar bibliotecas de clientes em `/apps` e disponibilizá-los usando o servlet proxy. No entanto, lembre-se de que as práticas recomendadas ainda exigem que os sites públicos nunca incluam nada que seja distribuído diretamente por um `/apps` ou `/libs` caminho.

### Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

1. Abra o CRXDE Lite em um navegador da Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selecione a pasta onde deseja localizar a pasta da biblioteca do cliente e clique em **Criar > Criar nó**.
1. Insira um nome para o arquivo de biblioteca e, na lista Tipo, selecione `cq:ClientLibraryFolder`. Clique em **OK** e clique em **Salvar tudo**.
1. Para especificar a categoria ou categorias às quais a biblioteca pertence, selecione a `cq:ClientLibraryFolder` , adicione a seguinte propriedade e clique em **Salvar tudo**:

   * Nome: categorias
   * Tipo: String
   * Valor: o nome da categoria
   * Múltiplo: Selecionar

1. Adicione arquivos de origem à pasta da biblioteca por qualquer meio. Por exemplo, use um cliente WebDAV para copiar arquivos ou crie um arquivo e crie o conteúdo manualmente.

   **Nota:** Você pode organizar os arquivos de origem em subpastas, se desejar.

1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:

   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma Folha de Estilos em Cascata.

1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:

   `#base=*[root]*`

   Substituir * `[root]`* com o caminho para a pasta que contém os arquivos de origem, relativo ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de código-fonte estiverem na mesma pasta que o arquivo TXT:

   `#base=.`

   O código a seguir define a raiz como a pasta chamada mobile abaixo de `cq:ClientLibraryFolder` nó:

   `#base=mobile`

1. Nas linhas abaixo `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

### Vinculação a Dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. No JSP, a variável `ui:includeClientLib` A tag que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo de biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade à `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categories do nó cq:ClientLibraryFolder do qual a pasta da biblioteca atual depende.

Por exemplo, o / `etc/clientlibs/myclientlibs/publicmain` tem uma dependência no `cq.jquery` biblioteca. O JSP que faz referência à biblioteca cliente principal gera um HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Como incorporar código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar o código de uma biblioteca do cliente a outra biblioteca do cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso às bibliotecas armazenadas em áreas seguras do repositório.

#### Pastas de bibliotecas de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados ao aplicativo na pasta do aplicativo abaixo `/apps`. Também é uma prática recomendada negar acesso aos visitantes do site à `/apps` pasta. Para atender às duas práticas recomendadas, crie uma pasta de biblioteca do cliente abaixo `/apps`e torná-lo acessível por meio do servlet proxy, conforme descrito em [Localizar uma pasta de bibliotecas de clientes e usar o servlet de bibliotecas de clientes proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Use a propriedade categories para identificar a pasta da biblioteca do cliente a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade à incorporação `cq:ClientLibraryFolder` usando os seguintes atributos de propriedade:

* **Nome:** incorporar
* **Tipo:** String[]
* **Valor:** O valor da propriedade categories do `cq:ClientLibraryFolder` nó a ser incorporado.

#### Utilização de incorporação para minimizar solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para a página típica pela instância de publicação inclui um número relativamente grande de `<script>` elementos, principalmente se o site estiver usando informações de contexto do cliente para análise ou direcionamento. Por exemplo, em um projeto não otimizado, você pode encontrar a seguinte série de `<script>` elementos no HTML para uma página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário no em um único arquivo para reduzir o número de solicitações de ida e volta no carregamento da página. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca do cliente específica do aplicativo usando a propriedade embed do `cq:ClientLibraryFolder` nó.

As seguintes categorias de bibliotecas de clientes estão incluídas no AEM. Você deve incorporar apenas aqueles que são necessários para o funcionamento do seu site específico. No entanto, **você deve manter a ordem listada aqui**:

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

#### Caminhos em arquivos CSS {#paths-in-css-files}

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível publicamente `/etc/client/libraries/myclientlibs/publicmain` incorpora o `/apps/myapp/clientlib` biblioteca do cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

A variável `main.css` O arquivo contém o seguinte estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS que o `publicmain` O nó gerado contém o seguinte estilo, usando o URL da imagem original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Uso de uma biblioteca para grupos móveis específicos {#using-a-library-for-specific-mobile-groups}

Use o `channels` propriedade de uma pasta da biblioteca do cliente para identificar o grupo móvel que usa a biblioteca. A variável `channels` A propriedade é útil quando bibliotecas da mesma categoria são projetadas para diferentes recursos do dispositivo.

Para associar uma pasta da biblioteca do cliente a um grupo de dispositivos, adicione uma propriedade à `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** canais
* **Tipo:** String[]
* **Valores:** O nome do grupo móvel. Para excluir a pasta da biblioteca de um grupo, adicione um ponto de exclamação (&quot;!&quot;) ao nome.

Por exemplo, a tabela a seguir lista o valor de `channels` para cada pasta da biblioteca do cliente do `cq.widgets` categoria:

| Pasta da biblioteca do cliente | Valor da propriedade de canais |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## Uso de pré-processadores {#using-preprocessors}

O AEM permite pré-processadores conectáveis e é fornecido com suporte para [Compactador YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e [Compilador de Fechamento do Google (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como pré-processador padrão do AEM.

Os pré-processadores conectáveis permitem um uso flexível, incluindo:

* Definição de ScriptProcessors que podem processar origens de script
* Os processadores são configuráveis com opções
* Os processadores podem ser usados para minificação, mas também para casos não minificados
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, o AEM usa o Compactador YUI. Consulte a [Documentação do GitHub do Compactador YUI](https://github.com/yui/yuicompressor/issues) para obter uma lista de problemas conhecidos. Alternar para o compactador GCC para clientlibs específicas pode resolver alguns problemas observados ao usar a interface do usuário do.

>[!CAUTION]
>
>Não coloque uma biblioteca minificada em uma biblioteca do cliente. Em vez disso, forneça a biblioteca bruta e, se a minificação for necessária, use as opções dos pré-processadores.

### Uso {#usage}

Você pode optar por definir a configuração de pré-processadores por biblioteca do cliente ou em todo o sistema.

* Adicionar as propriedades multivalor `cssProcessor` e `jsProcessor` no nó clientlibrary

* Ou defina a configuração padrão do sistema por meio do **Gerenciador de biblioteca HTML** Configuração OSGi

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

#### Compactador YUI para Minificação CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Digitar script para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### Opções adicionais de GCC {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obter mais detalhes sobre as opções do GCC, consulte a [Documentação do GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Definir Minificador Padrão do Sistema {#set-system-default-minifier}

A interface do usuário é definida como o minificador padrão no AEM. Para alterar isso para GCC, siga estas etapas.

1. Acesse o Apache Felix Config Manager em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localize e edite o **Gerenciador de biblioteca de HTML do Adobe Granite**.
1. Ativar o **Minify** (se ainda não estiver ativada).
1. Definir o valor **Configurações padrão do processador JS** para `min:gcc`.

   As opções podem ser passadas se separadas por ponto e vírgula, por exemplo. `min:gcc;obfuscate=true`.

1. Clique em **Salvar** para salvar as alterações.

## Ferramentas de depuração {#debugging-tools}

O AEM fornece várias ferramentas para depurar e testar pastas da biblioteca do cliente.

### Consulte Arquivos incorporados {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas estejam produzindo os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe o `debugClientLibs=true` para o URL da sua página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo no anterior [Como incorporar código de outras bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) seção, a variável `/etc/client/libraries/myclientlibs/publicmain` a pasta da biblioteca do cliente incorpora o `/apps/myapp/clientlib` pasta da biblioteca do cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abrir o `publicmain.css` revela o seguinte código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do HTML:

   `?debugClientLibs=true`
1. Quando a página for carregada, exiba a origem da página.
1. Clique no link fornecido como href para o elemento do link para abrir o arquivo e exibir o código-fonte.

### Descubra bibliotecas de clientes {#discover-client-libraries}

A variável `/libs/cq/granite/components/dumplibs/dumplibs` O componente gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. A variável `/libs/granite/ui/content/dumplibs` possui o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS), bem como os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

A variável `dumplibs` componente inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` específicos. A página inclui código para diferentes combinações de js, css e atributos temáticos.

1. Use um dos métodos a seguir para abrir a página Saída do teste:

   * No `dumplibs.html` clique no link na **Clique aqui para testar a saída** texto.

   * Abra o seguinte URL no navegador da Web (use um host e porta diferentes, conforme necessário):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   A página padrão mostra saída para tags sem valor para o atributo categories.

1. Para ver a saída de uma categoria, digite o valor da variável do `categories` e clique em **Enviar consulta**.

## Configuração da manipulação de bibliotecas para desenvolvimento e produção {#configuring-library-handling-for-development-and-production}

Os processos do serviço Gerenciador de biblioteca de HTML `cq:ClientLibraryFolder` e gera as bibliotecas no tempo de execução. O tipo de ambiente, desenvolvimento ou produção determina como você deve configurar o serviço:

* Aumentar segurança: Desativar depuração
* Melhorar o desempenho: remova espaços em branco e compacte bibliotecas.
* Melhorar a legibilidade: inclua espaços em branco e não compacte.

Para obter informações sobre como configurar o serviço, consulte [Gerenciador de biblioteca de HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
