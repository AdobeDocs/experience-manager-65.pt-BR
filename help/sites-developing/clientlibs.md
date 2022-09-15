---
title: Uso de bibliotecas do cliente
seo-title: Using Client-Side Libraries
description: O AEM fornece Pastas de biblioteca do lado do cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente
seo-description: AEM provides Client-side Library Folders, which allow you to store your client-side code in the repository, organize it into categories, and define when and how each category of code is to be served to the client
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 684474d764ac2a2c187827382e0180e6c0d5259b
workflow-type: tm+mt
source-wordcount: '2861'
ht-degree: 2%

---

# Uso de bibliotecas do cliente{#using-client-side-libraries}

Sites modernos dependem muito de processamento no lado do cliente impulsionado por códigos complexos de JavaScript e CSS. Organizar e otimizar a veiculação desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, AEM fornece **Pastas de bibliotecas do lado do cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente. O sistema de biblioteca do lado do cliente cuida da produção dos links corretos na página da Web final para carregar o código correto.

## Como as bibliotecas do lado do cliente funcionam no AEM {#how-client-side-libraries-work-in-aem}

A maneira padrão de incluir uma biblioteca do lado do cliente (ou seja, um arquivo JS ou CSS) no HTML de uma página é simplesmente incluir um `<script>` ou `<link>` no JSP dessa página, contendo o caminho para o arquivo em questão. Por exemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Embora essa abordagem funcione em AEM, pode levar a problemas quando as páginas e seus componentes constituintes se tornam complexos. Nesses casos, há o perigo de várias cópias da mesma biblioteca JS serem incluídas na saída final do HTML. Para evitar isso e permitir a organização lógica de bibliotecas do lado do cliente AEM usuários **pastas de bibliotecas do lado do cliente**.

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. É definição em [Notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Por padrão, `cq:ClientLibraryFolder` os nós podem ser colocados em qualquer lugar dentro do `/apps`, `/libs` e `/etc` subárvores do repositório (esses padrões e outras configurações podem ser controladas pelo **Gerenciador de biblioteca de HTML do Adobe Granite** painel do [Console do sistema](https://localhost:4502/system/console/configMgr)).

Cada `cq:ClientLibraryFolder` O é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades da variável `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `categories`: Identifica as categorias em que o conjunto de arquivos JS e/ou CSS dentro dessa `cq:ClientLibraryFolder` outono. O `categories` , com vários valores, permite que uma pasta de biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais essa pasta da biblioteca depende. Por exemplo, considerando dois `cq:ClientLibraryFolder` nodes `F` e `G`, se um arquivo em `F` requer outro arquivo em `G` para funcionar adequadamente, pelo menos um dos `categories` de `G` deve estar entre as `dependencies` de `F`.

* `embed`: Usado para incorporar o código de outras bibliotecas. Se o nó F incorporar os nós G e H, o HTML resultante será uma concentração de conteúdo dos nós G e H.
* `allowProxy`: Se uma biblioteca do cliente estiver localizada em `/apps`, essa propriedade permite acesso a ela por meio do servlet proxy. Consulte [Localizando uma pasta da biblioteca do cliente e usando o servlet de bibliotecas do cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.

## Referência a bibliotecas do lado do cliente {#referencing-client-side-libraries}

Como o HTL é a tecnologia preferida para desenvolver sites de AEM, o HTL deve ser usado para incluir bibliotecas do lado do cliente no AEM. No entanto, também é possível fazer isso usando o JSP.

### Uso de HTL {#using-htl}

No HTL, as bibliotecas do cliente são carregadas por meio de um modelo auxiliar fornecido pelo AEM, que pode ser acessado por meio de [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Três modelos estão disponíveis nesse arquivo, que pode ser chamado por meio de [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Carrega apenas os arquivos CSS das bibliotecas de clientes referenciadas.
* **js** - Carrega somente os arquivos JavaScript das bibliotecas de clientes referenciadas.
* **all** - Carrega todos os arquivos das bibliotecas de clientes referenciadas (CSS e JavaScript).

Cada modelo auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de cadeias de caracteres ou uma cadeia contendo uma lista de valores separados por vírgula.

Para obter mais detalhes e exemplos de uso, consulte o documento [Introdução à Linguagem de modelo do HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Uso de JSP {#using-jsp}

Adicione um `ui:includeClientLib` adicione um link às bibliotecas do cliente na página HTML gerada. Para fazer referência às bibliotecas, use o valor da variável `categories` da `ui:includeClientLib` nó .

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por exemplo, a variável `/etc/clientlibs/foundation/jquery` o nó é do tipo `cq:ClientLibraryFolder` com uma propriedade categories de valor `cq.jquery`. O código a seguir em um arquivo JSP faz referência às bibliotecas:

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
>`<cq:includeClientLib>`, que anteriormente era comumente usada para incluir bibliotecas de clientes, foi descontinuada desde o AEM 5.6. [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) deve ser usada como detalhado acima.

## Criação de pastas da biblioteca do cliente {#creating-client-library-folders}

Crie um `cq:ClientLibraryFolder` para definir bibliotecas JavaScript e Folha de estilos em cascata e disponibilizá-las para HTML pages. Use o `categories` propriedade do nó para identificar as categorias da biblioteca à qual pertence.

O nó contém um ou mais arquivos de origem que, em tempo de execução, são mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a variável `.js` ou `.css` extensão do nome do arquivo. Por exemplo, o nó da biblioteca chamado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca de clientes contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS a serem mesclados.
* Recursos que oferecem suporte a estilos CSS, como arquivos de imagem.

   **Observação:** Você pode usar subpastas para organizar arquivos de origem.
* One `js.txt` arquivo e/ou um `css.txt` arquivo que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados.

![clientlibarch](assets/clientlibarch.png)

Para obter informações sobre os requisitos específicos das bibliotecas de clientes para widgets, consulte [Uso e extensão de widgets](/help/sites-developing/widgets.md).

O cliente Web deve ter permissões para acessar o `cq:ClientLibraryFolder` nó . Também é possível expor bibliotecas de áreas seguras do repositório (consulte Incorporação de código a partir de outras bibliotecas, abaixo).

### Substituição de bibliotecas em /lib {#overriding-libraries-in-lib}

Pastas da biblioteca de clientes localizadas abaixo `/apps` tem prioridade sobre as pastas com mesmo nome que estão localizadas de forma semelhante no `/libs`. Por exemplo, `/apps/cq/ui/widgets` tem precedência sobre `/libs/cq/ui/widgets`. Quando essas bibliotecas pertencem à mesma categoria, a biblioteca abaixo `/apps` é usada.

### Localizando uma pasta da biblioteca do cliente e usando o servlet de bibliotecas do cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Em versões anteriores, as pastas da biblioteca do cliente estavam localizadas abaixo `/etc/clientlibs` no repositório. Isso ainda é suportado, no entanto, é recomendável que as bibliotecas de clientes agora estejam localizadas em `/apps`. Isso é para localizar as bibliotecas de clientes perto dos outros scripts, que geralmente são encontrados abaixo `/apps` e `/libs`.

>[!NOTE]
>
>Os recursos estáticos abaixo da pasta da biblioteca do cliente devem estar em uma pasta chamada *recursos*. Se você não tiver os recursos estáticos, como imagens, na pasta *recursos*, ele não pode ser referenciado em uma instância de publicação. Veja um exemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para isolar melhor o código do conteúdo e da configuração, é recomendável localizar as bibliotecas de clientes em `/apps` e expô-las via `/etc.clientlibs` aproveitando a `allowProxy` propriedade.

Para as bibliotecas de clientes em `/apps` para ser acessível, um servidor proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido via `/etc.clientlibs/` se a variável `allowProxy` está definida como `true`.

Um recurso estático só pode ser acessado por meio do proxy, se ele residir abaixo de um recurso abaixo da pasta da biblioteca do cliente.

Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

Em seguida, defina a variável `allowProxy` propriedade em `foo` para verdadeiro.

* Você pode solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Você pode fazer referência à imagem por meio de `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Ao usar bibliotecas de cliente proxy, a configuração do Dispatcher de AEM pode exigir uma atualização para garantir que os URIs com as clientlibs de extensão sejam permitidos.

>[!CAUTION]
>
>O Adobe recomenda localizar as bibliotecas de clientes em `/apps` e disponibilizá-los usando o servlet proxy. No entanto, lembre-se de que as práticas recomendadas ainda exigem que os sites públicos nunca incluam nada que seja distribuído diretamente sobre um `/apps` ou `/libs` caminho.

### Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

1. Abra o CRXDE Lite em um navegador da Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selecione a pasta onde deseja localizar a pasta da biblioteca do cliente e clique em **Criar > Criar nó**.
1. Insira um nome para o arquivo da biblioteca e, na lista Tipo, selecione `cq:ClientLibraryFolder`. Clique em **OK** e, em seguida, clique em **Salvar tudo**.
1. Para especificar a categoria ou categorias à qual a biblioteca pertence, selecione o `cq:ClientLibraryFolder` , adicione a seguinte propriedade e clique em **Salvar tudo**:

   * Nome: categorias
   * Tipo: String
   * Valor: O nome da categoria
   * Várias: Selecionar

1. Adicione arquivos de origem à pasta da biblioteca de qualquer maneira. Por exemplo, use um cliente WebDav para copiar arquivos ou crie um arquivo e crie o conteúdo manualmente.

   **Observação:** Você pode organizar os arquivos de origem em subpastas, se desejar.

1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:

   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma Folha de estilos em cascata.

1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:

   `#base=*[root]*`

   Substituir * `[root]`* com o caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta do arquivo TXT:

   `#base=.`

   O código a seguir define a raiz como a pasta nomeada móvel abaixo da função `cq:ClientLibraryFolder` nó:

   `#base=mobile`

1. Nas linhas abaixo `#base=[root]`, digite os caminhos dos arquivos de origem em relação à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. No JSP, a variável `ui:includeClientLib` A tag que faz referência à pasta da biblioteca do cliente faz com que o código do HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categories do nó cq:ClientLibraryFolder da qual a pasta de biblioteca atual depende.

Por exemplo, o / `etc/clientlibs/myclientlibs/publicmain` tem uma dependência do `cq.jquery` biblioteca. O JSP que faz referência à biblioteca principal do cliente gera HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Como Incorporar Código A Partir De Outras Bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar o código de uma biblioteca do cliente em outra biblioteca do cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso a bibliotecas que são armazenadas em áreas seguras do repositório.

#### Pastas da biblioteca de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados a aplicativos em sua pasta de aplicativos abaixo `/apps`. Também é uma prática recomendada negar o acesso dos visitantes do site à variável `/app` pasta. Para atender às duas práticas recomendadas, crie uma pasta de biblioteca de clientes abaixo `/apps`e torná-lo acessível por meio do servlet proxy, conforme descrito em [Localizando uma pasta da biblioteca do cliente e usando o servlet de bibliotecas do cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

Use a propriedade categories para identificar a pasta da biblioteca de clientes a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade à incorporação `cq:ClientLibraryFolder` , usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** String[]
* **Valor:** O valor da propriedade categories da variável `cq:ClientLibraryFolder` nó a ser incorporado.

#### Usando a Incorporação para Minimizar Solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para uma página típica pela sua instância de publicação inclui um número relativamente grande de `<script>` , especialmente se seu site estiver usando informações de contexto do cliente para análise ou direcionamento. Por exemplo, em um projeto não otimizado, você pode encontrar a seguinte série de `<script>` na HTML de de uma página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário em em um único arquivo para que o número de solicitações de frente e verso no carregamento da página seja reduzido. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca do cliente específica do aplicativo usando a propriedade embed do `cq:ClientLibraryFolder` nó .

As seguintes categorias da biblioteca de clientes são incluídas no AEM. Você deve incorporar somente aqueles necessários para o funcionamento de seu site específico. No entanto, **você deve manter a ordem listada aqui**:

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

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos que são relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível publicamente `/etc/client/libraries/myclientlibs/publicmain` incorpora o `/apps/myapp/clientlib` biblioteca do cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

O `main.css` O arquivo contém o seguinte estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS que `publicmain` O nó gerado contém o seguinte estilo, usando o URL da imagem original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Usar uma biblioteca para grupos móveis específicos {#using-a-library-for-specific-mobile-groups}

Use o `channels` de uma pasta da biblioteca do cliente para identificar o grupo móvel que usa a biblioteca. O `channels` é útil quando bibliotecas da mesma categoria são projetadas para diferentes recursos do dispositivo.

Para associar uma pasta da biblioteca do cliente a um grupo de dispositivos, adicione uma propriedade a `cq:ClientLibraryFolder` nó com os seguintes atributos:

* **Nome:** canais
* **Tipo:** String[]
* **Valores:** O nome do grupo móvel. Para excluir a pasta da biblioteca de um grupo, coloque o nome com um ponto de exclamação (&quot;!&quot;).

Por exemplo, a tabela a seguir lista o valor da variável `channels` para cada pasta da biblioteca do cliente do `cq.widgets` categoria:

| Pasta da biblioteca do cliente | Valor da propriedade channels |
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

AEM permite pré-processadores e entregas conectáveis com suporte para [Compressor YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e [Compilador de Fechamento do Google (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores são configuráveis com opções
* Os processadores podem ser usados para minificação, mas também para casos não minificados
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, o AEM usa o Compactador YUI. Consulte a [Documentação do YUI Compressor GitHub](https://github.com/yui/yuicompressor/issues) para obter uma lista de problemas conhecidos. Alternar para o compressor GCC para clientlibs específicas pode resolver alguns problemas observados ao usar YUI.

>[!CAUTION]
>
>Não coloque uma biblioteca minificada em uma biblioteca do cliente. Em vez disso, forneça a biblioteca bruta e, se a minificação for necessária, use as opções dos pré-processadores.

### Uso {#usage}

Você pode optar por configurar a configuração de pré-processadores por biblioteca do cliente ou todo o sistema.

* Adicionar as propriedades de vários valores `cssProcessor` e `jsProcessor` no nó clientlibrary

* Ou defina a configuração padrão do sistema por meio do **Gerenciador da biblioteca HTML** Configuração do OSGi

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

#### Compactador YUI para Minificação de CSS e GCC para JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Tipo para pré-processar e, em seguida, GCC para minificar e ofuscar {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Para obter mais detalhes sobre as opções do GCC, consulte o [Documentação do GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Definir Minificador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como minificador padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Vá para o Apache Felix Config Manager em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Encontre e edite o **Gerenciador de biblioteca de HTML do Adobe Granite**.
1. Ative o **Minimizar** (se ainda não estiver habilitado).
1. Defina o valor **Configurações padrão do processador JS** para `min:gcc`.

   As opções podem ser passadas se separadas por um ponto e vírgula, por exemplo `min:gcc;obfuscate=true`.

1. Clique em **Salvar** para salvar as alterações.

## Ferramentas de depuração {#debugging-tools}

O AEM fornece várias ferramentas para depurar e testar as pastas da biblioteca do cliente.

### Consulte Arquivos incorporados {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas estejam produzindo os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe a variável `debugClientLibs=true` para o URL da página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo do anterior [Como Incorporar Código A Partir De Outras Bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) seção , a variável `/etc/client/libraries/myclientlibs/publicmain` a pasta da biblioteca do cliente incorpora o `/apps/myapp/clientlib` pasta da biblioteca do cliente. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Abrir o `publicmain.css` O arquivo revela o seguinte código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:

   `?debugClientLibs=true`
1. Quando a página for carregada, visualize a fonte da página.
1. Clique no link fornecido como href para o elemento do link para abrir o arquivo e exibir o código-fonte.

### Bibliotecas de clientes do Discover {#discover-client-libraries}

O `/libs/cq/granite/components/dumplibs/dumplibs` O componente gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O `/libs/granite/ui/content/dumplibs` tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O `dumplibs` componente inclui um seletor de teste que exibe o código-fonte gerado para `ui:includeClientLib` tags. A página inclui código para diferentes combinações de js, css e atributos temáticos.

1. Use um dos métodos a seguir para abrir a página Saída de teste:

   * No `dumplibs.html` clique no link na página **Clique aqui para testar a saída** texto.

   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   A página padrão mostra a saída de tags sem valor para o atributo de categorias.

1. Para ver a saída de uma categoria, digite o valor da biblioteca do cliente `categories` propriedade e clique em **Enviar Consulta**.

## Configuração do tratamento de biblioteca para desenvolvimento e produção {#configuring-library-handling-for-development-and-production}

Os processos do serviço Gerenciador de biblioteca do HTML `cq:ClientLibraryFolder` e gera as bibliotecas no tempo de execução. O tipo de ambiente, desenvolvimento ou produção determina como você deve configurar o serviço:

* Aumente a segurança: Desativar depuração
* Melhore o desempenho: Remova o espaço em branco e compacte as bibliotecas.
* Melhore a legibilidade: Inclua o espaço em branco e não compacte.

Para obter informações sobre como configurar o serviço, consulte [Gerenciador da biblioteca do HTML AEM](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
