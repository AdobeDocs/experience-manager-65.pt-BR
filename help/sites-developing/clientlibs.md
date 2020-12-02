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
source-git-commit: 5d33b48000cf607eb77c626ec539280cadab378e
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---


# Usando bibliotecas do lado do cliente{#using-client-side-libraries}

Sites modernos dependem muito do processamento no cliente, conduzido por códigos complexos de JavaScript e CSS. Organizar e otimizar a entrega desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, AEM fornece **Pastas de biblioteca do lado do cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos em sua página final para carregar o código correto.

## Como as bibliotecas do lado do cliente funcionam em AEM {#how-client-side-libraries-work-in-aem}

A maneira padrão de incluir uma biblioteca do lado do cliente (ou seja, um arquivo JS ou CSS) no HTML de uma página é simplesmente incluir uma tag `<script>` ou `<link>` no JSP dessa página, contendo o caminho para o arquivo em questão. Por exemplo,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

Embora essa abordagem funcione em AEM, pode causar problemas quando as páginas e seus componentes se tornam complexos. Nesses casos, há o perigo de várias cópias da mesma biblioteca JS poderem ser incluídas na saída HTML final. Para evitar isso e permitir a organização lógica de bibliotecas do lado do cliente, AEM usa **pastas de biblioteca do lado do cliente**.

Uma pasta de biblioteca do lado do cliente é um nó de repositório do tipo `cq:ClientLibraryFolder`. É a definição em [Notação CND](https://jackrabbit.apache.org/node-type-notation.html) é

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

Por padrão, os nós `cq:ClientLibraryFolder` podem ser colocados em qualquer lugar dentro das subárvores `/apps`, `/libs` e `/etc` do repositório (esses padrões e outras configurações podem ser controladas pelo painel **Adobe Granite HTML Library Manager** do [Console do Sistema](https://localhost:4502/system/console/configMgr)).

Cada `cq:ClientLibraryFolder` é preenchido com um conjunto de arquivos JS e/ou CSS, juntamente com alguns arquivos de suporte (veja abaixo). As propriedades de `cq:ClientLibraryFolder` são configuradas da seguinte maneira:

* `categories`: Identifica as categorias nas quais o conjunto de arquivos JS e/ou CSS nesse  `cq:ClientLibraryFolder` outono. A propriedade `categories`, que tem vários valores, permite que uma pasta de biblioteca faça parte de mais de uma categoria (veja abaixo como isso pode ser útil).

* `dependencies`: Esta é uma lista de outras categorias da biblioteca do cliente das quais esta pasta da biblioteca depende. Por exemplo, dados dois nós `cq:ClientLibraryFolder` `F` e `G`, se um arquivo em `F` exigir outro arquivo em `G` para funcionar corretamente, pelo menos um dos `categories` de `G` deve estar entre `dependencies` de `F`.

* `embed`: Usado para incorporar código de outras bibliotecas. Se o nó F incorporar os nós G e H, o HTML resultante será uma concentração de conteúdo dos nós G e H.
* `allowProxy`: Se uma biblioteca do cliente estiver localizada em  `/apps`, essa propriedade permitirá o acesso a ela por meio do servlet proxy. Consulte [Localizando uma pasta de biblioteca de cliente e Usando o Servlet de bibliotecas de cliente proxy](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) abaixo.

## Referência a bibliotecas do lado do cliente {#referencing-client-side-libraries}

Como o HTL é a tecnologia preferida para desenvolver sites AEM, o HTL deve ser usado para incluir bibliotecas do lado do cliente no AEM. No entanto, também é possível fazê-lo usando a JSP.

### Usando HTL {#using-htl}

Em HTL, as bibliotecas do cliente são carregadas por meio de um modelo auxiliar fornecido pela AEM, que pode ser acessado por meio de [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). Três modelos estão disponíveis neste arquivo, que pode ser chamado por meio de [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - Carrega somente os arquivos CSS das bibliotecas clientes referenciadas.
* **js** - carrega somente os arquivos JavaScript das bibliotecas de clientes referenciadas.
* **all** - Carrega todos os arquivos das bibliotecas de cliente referenciadas (CSS e JavaScript).

Cada modelo auxiliar espera uma opção `categories` para fazer referência às bibliotecas de clientes desejadas. Essa opção pode ser uma matriz de valores de string ou uma string contendo uma lista de valores separados por vírgula.

Para obter mais detalhes e exemplos de uso, consulte o documento [Introdução à Linguagem de Modelo HTML](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### Usando JSP {#using-jsp}

Adicione uma tag `ui:includeClientLib` ao código JSP para adicionar um link às bibliotecas do cliente na página HTML gerada. Para referenciar as bibliotecas, use o valor da propriedade `categories` do nó `ui:includeClientLib`.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

Por exemplo, o nó `/etc/clientlibs/foundation/jquery` é do tipo `cq:ClientLibraryFolder` com uma propriedade categoria do valor `cq.jquery`. O código a seguir em um arquivo JSP faz referência às bibliotecas:

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
>`<cq:includeClientLib>`, que no passado costumava ser usada para incluir bibliotecas de clientes, foi substituída desde AEM 5.6.  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) em vez disso, conforme detalhado acima.

## Criando Pastas da Biblioteca de Clientes {#creating-client-library-folders}

Crie um nó `cq:ClientLibraryFolder` para definir bibliotecas JavaScript e Folha de estilos em cascata e disponibilizá-las para páginas HTML. Use a propriedade `categories` do nó para identificar as categorias de biblioteca às quais ele pertence.

O nó contém um ou mais arquivos de origem que, em tempo de execução, são mesclados em um único arquivo JS e/ou CSS. O nome do arquivo gerado é o nome do nó com a extensão `.js` ou `.css` do nome do arquivo. Por exemplo, o nó de biblioteca chamado `cq.jquery` resulta no arquivo gerado chamado `cq.jquery.js` ou `cq.jquery.css`.

As pastas da biblioteca do cliente contêm os seguintes itens:

* Os arquivos de origem JS e/ou CSS a serem mesclados.
* Recursos que suportam estilos CSS, como arquivos de imagem.

   **Observação:** você pode usar subpastas para organizar arquivos de origem.
* Um arquivo `js.txt` e/ou um arquivo `css.txt` que identifica os arquivos de origem a serem mesclados nos arquivos JS e/ou CSS gerados.

![clientlibarch](assets/clientlibarch.png)

Para obter informações sobre os requisitos específicos das bibliotecas clientes para widgets, consulte [Uso e extensão de widgets](/help/sites-developing/widgets.md).

O cliente Web deve ter permissões para acessar o nó `cq:ClientLibraryFolder`. Você também pode expor bibliotecas de áreas protegidas do repositório (consulte Incorporação de código a partir de outras bibliotecas, abaixo).

### Substituição de bibliotecas em /lib {#overriding-libraries-in-lib}

As pastas da biblioteca do cliente localizadas abaixo de `/apps` têm prioridade sobre as pastas com o mesmo nome que estão localizadas de maneira semelhante em `/libs`. Por exemplo, `/apps/cq/ui/widgets` tem prioridade sobre `/libs/cq/ui/widgets`. Quando essas bibliotecas pertencem à mesma categoria, a biblioteca abaixo de `/apps` é usada.

### Localizando uma pasta de biblioteca de cliente e usando o servlet de bibliotecas de cliente proxy {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

Em versões anteriores, as pastas da biblioteca do cliente estavam localizadas abaixo de `/etc/clientlibs` no repositório. Isso ainda é suportado, mas é recomendável que as bibliotecas do cliente agora estejam localizadas em `/apps`. Isso serve para localizar as bibliotecas do cliente perto dos outros scripts, que geralmente são encontrados abaixo de `/apps` e `/libs`.

>[!NOTE]
>
>Os recursos estáticos abaixo da pasta da biblioteca do cliente devem estar em uma pasta chamada *resources*. Se você não tiver os recursos estáticos, como imagens, na pasta *resources*, ele não poderá ser referenciado em uma instância de publicação. Veja um exemplo: https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>Para isolar melhor o código do conteúdo e da configuração, é recomendável localizar as bibliotecas do cliente em `/apps` e expô-las via `/etc.clientlibs` aproveitando a propriedade `allowProxy`.

Para que as bibliotecas do cliente em `/apps` sejam acessíveis, um servidor proxy é usado. As ACLs ainda são aplicadas na pasta da biblioteca do cliente, mas o servlet permite que o conteúdo seja lido por `/etc.clientlibs/` se a propriedade `allowProxy` estiver definida como `true`.

Um recurso estático só pode ser acessado por meio do proxy, se ele residir abaixo de um recurso abaixo da pasta da biblioteca do cliente.

Como exemplo:

* Você tem uma clientlib em `/apps/myproject/clientlibs/foo`
* Você tem uma imagem estática em `/apps/myprojects/clientlibs/foo/resources/icon.png`

Em seguida, defina a propriedade `allowProxy` em `foo` como true.

* Você pode solicitar `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Você pode fazer referência à imagem por meio de `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>Ao usar bibliotecas de clientes proxy, a configuração do Dispatcher AEM pode exigir uma atualização para garantir que os URIs com as clientlibs de extensão sejam permitidos.

>[!CAUTION]
>
>O Adobe recomenda localizar as bibliotecas do cliente em `/apps` e disponibilizá-las usando o servlet proxy. No entanto, lembre-se de que as práticas recomendadas ainda exigem que os sites públicos nunca incluam nada que seja enviado diretamente sobre um caminho `/apps` ou `/libs`.

### Criar uma pasta da biblioteca do cliente {#create-a-client-library-folder}

1. Abra o CRXDE Lite em um navegador da Web ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Selecione a pasta na qual deseja localizar a pasta da biblioteca do cliente e clique em **Criar > Criar nó**.
1. Digite um nome para o arquivo de biblioteca e, na lista Tipo, selecione `cq:ClientLibraryFolder`. Clique em **OK** e, em seguida, clique em **Salvar tudo**.
1. Para especificar a categoria ou as categorias às quais a biblioteca pertence, selecione o nó `cq:ClientLibraryFolder`, adicione a seguinte propriedade e clique em **Salvar tudo**:

   * Nome: categorias
   * Tipo: String
   * Valor: O nome da categoria
   * Vários: Selecionar

1. Adicione os arquivos de origem à pasta da biblioteca por qualquer meio. Por exemplo, use um cliente WebDav para copiar arquivos ou crie um arquivo e crie o conteúdo manualmente.

   **Observação:** você pode organizar arquivos de origem em subpastas, se desejar.

1. Selecione a pasta da biblioteca do cliente e clique em **Criar > Criar arquivo**.
1. Na caixa Nome do arquivo, digite um dos seguintes nomes de arquivo e clique em OK:

   * **`js.txt`:** Use esse nome de arquivo para gerar um arquivo JavaScript.
   * **`css.txt`:** Use esse nome de arquivo para gerar uma folha de estilos em cascata.

1. Abra o arquivo e digite o seguinte texto para identificar a raiz do caminho dos arquivos de origem:

   `#base=*[root]*`

   Substitua * `[root]`* pelo caminho para a pasta que contém os arquivos de origem, em relação ao arquivo TXT. Por exemplo, use o seguinte texto quando os arquivos de origem estiverem na mesma pasta que o arquivo TXT:

   `#base=.`

   O código a seguir define a raiz como a pasta chamada mobile abaixo do nó `cq:ClientLibraryFolder`:

   `#base=mobile`

1. Nas linhas abaixo de `#base=[root]`, digite os caminhos dos arquivos de origem relativos à raiz. Coloque cada nome de arquivo em uma linha separada.
1. Clique em **Salvar tudo**.

### Vincular a dependências {#linking-to-dependencies}

Quando o código na pasta da biblioteca do cliente fizer referência a outras bibliotecas, identifique as outras bibliotecas como dependências. No JSP, a tag `ui:includeClientLib` que faz referência à pasta da biblioteca do cliente faz com que o código HTML inclua um link para o arquivo da biblioteca gerado, bem como as dependências.

As dependências devem ser outras `cq:ClientLibraryFolder`. Para identificar dependências, adicione uma propriedade ao nó `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** dependências
* **Tipo:** String[]
* **Valores:** O valor da propriedade categoria do nó cq:ClientLibraryFolder do qual a pasta da biblioteca atual depende.

Por exemplo, / `etc/clientlibs/myclientlibs/publicmain` tem uma dependência na biblioteca `cq.jquery`. O JSP que faz referência à biblioteca principal do cliente gera HTML que inclui o seguinte código:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporando código de outras bibliotecas {#embedding-code-from-other-libraries}

Você pode incorporar código de uma biblioteca de cliente em outra biblioteca de cliente. No tempo de execução, os arquivos JS e CSS gerados da biblioteca de incorporação incluem o código da biblioteca incorporada.

A incorporação do código é útil para fornecer acesso às bibliotecas que são armazenadas em áreas protegidas do repositório.

#### Pastas da biblioteca de clientes específicas do aplicativo {#app-specific-client-library-folders}

É uma prática recomendada manter todos os arquivos relacionados ao aplicativo em sua pasta de aplicativos abaixo de `/app`. Também é uma prática recomendada negar o acesso de visitantes do site à pasta `/app`. Para satisfazer ambas as práticas recomendadas, crie uma pasta de biblioteca de cliente abaixo da pasta `/etc` que incorpora a biblioteca de cliente que está abaixo de `/app`.

Use a propriedade categoria para identificar a pasta da biblioteca do cliente a ser incorporada. Para incorporar a biblioteca, adicione uma propriedade ao nó de incorporação `cq:ClientLibraryFolder`, usando os seguintes atributos de propriedade:

* **Nome:** embed
* **Tipo:** String[]
* **Valor:** O valor da propriedade categoria do  `cq:ClientLibraryFolder` nó a ser incorporado.

#### Usando a incorporação para minimizar solicitações {#using-embedding-to-minimize-requests}

Em alguns casos, você pode descobrir que o HTML final gerado para a página típica pela sua instância de publicação inclui um número relativamente grande de elementos `<script>`, especialmente se o site estiver usando informações de contexto do cliente para análise ou direcionamento. Por exemplo, em um projeto não otimizado, você pode encontrar a seguinte série de elementos `<script>` no HTML de uma página:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

Nesses casos, pode ser útil combinar todo o código da biblioteca do cliente necessário em um único arquivo para que o número de solicitações de ida e volta no carregamento da página seja reduzido. Para fazer isso, você pode `embed` as bibliotecas necessárias na biblioteca de cliente específica do aplicativo usando a propriedade embed do nó `cq:ClientLibraryFolder`.

As seguintes categorias da biblioteca de cliente são incluídas com AEM. Você deve incorporar somente aqueles que são necessários para o funcionamento de seu site específico. Entretanto, **você deve manter a ordem listada aqui**:

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

Quando você incorpora arquivos CSS, o código CSS gerado usa caminhos para recursos relativos à biblioteca de incorporação. Por exemplo, a biblioteca acessível ao público `/etc/client/libraries/myclientlibs/publicmain` incorpora a biblioteca `/apps/myapp/clientlib` do cliente:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

O arquivo `main.css` contém o seguinte estilo:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

O arquivo CSS gerado pelo nó `publicmain` contém o seguinte estilo, usando o URL da imagem original:

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### Usando uma biblioteca para grupos móveis específicos {#using-a-library-for-specific-mobile-groups}

Use a propriedade `channels` de uma pasta da biblioteca do cliente para identificar o grupo móvel que usa a biblioteca. A propriedade `channels` é útil quando bibliotecas da mesma categoria são projetadas para diferentes recursos do dispositivo.

Para associar uma pasta da biblioteca do cliente a um grupo de dispositivos, adicione uma propriedade ao nó `cq:ClientLibraryFolder` com os seguintes atributos:

* **Nome:** canais
* **Tipo:** String[]
* **Valores:** O nome do grupo móvel. Para excluir a pasta da biblioteca de um grupo, prefixe o nome com um ponto de exclamação (&quot;!&quot;).

Por exemplo, a tabela a seguir lista o valor da propriedade `channels` para cada pasta da biblioteca do cliente da categoria `cq.widgets`:

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

AEM permite pré-processadores e entregas conectáveis com suporte para [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) para CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) para JavaScript com YUI definido como AEM pré-processador padrão.

Os pré-processadores conectáveis permitem uma utilização flexível, incluindo:

* Definindo ScriptProcessors que podem processar fontes de script
* Os processadores podem ser configurados com opções
* Os processadores podem ser usados para a miniificação, mas também para casos não-reduzidos
* A clientlib pode definir qual processador usar

>[!NOTE]
>
>Por padrão, AEM usa o Compressor YUI. Consulte a documentação do [YUI Compressor GitHub](https://github.com/yui/yuicompressor/issues) para obter uma lista de problemas conhecidos. Mudar para o compressor GCC para clientlibs específicos pode resolver alguns problemas observados ao utilizar IU.

>[!CAUTION]
>
>Não coloque uma biblioteca minimizada em uma biblioteca cliente. Em vez disso, forneça a biblioteca bruta e, se for necessário a miniificação, use as opções dos pré-processadores.

### Uso {#usage}

Você pode optar por configurar a configuração dos pré-processadores por biblioteca do cliente ou por todo o sistema.

* Adicione as propriedades multivalue `cssProcessor` e `jsProcessor` no nó clientlibrary

* Ou defina a configuração padrão do sistema por meio da configuração **HTML Library Manager** OSGi

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

#### Opções adicionais de GCC {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Para obter mais detalhes sobre as opções de GCC, consulte a [documentação da GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

### Definir Miniador Padrão do Sistema {#set-system-default-minifier}

A IU é definida como a miniatura padrão no AEM. Para alterar para GCC, siga estas etapas.

1. Vá para o Apache Felix Config Manager em [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. Localize e edite o **Gerenciador de biblioteca HTML Granite do Adobe**.
1. Ative a opção **Minify** (se ainda não estiver ativada).
1. Defina o valor **Configurações padrão do processador JS** como `min:gcc`.

   As opções podem ser passadas se separadas por um ponto-e-vírgula, por exemplo `min:gcc;obfuscate=true`.

1. Clique em **Salvar** para salvar as alterações.

## Ferramentas de depuração {#debugging-tools}

AEM fornece várias ferramentas para depurar e testar pastas da biblioteca do cliente.

### Consulte Arquivos incorporados {#see-embedded-files}

Para rastrear a origem do código incorporado ou garantir que as bibliotecas de clientes incorporadas produzam os resultados esperados, você pode ver os nomes dos arquivos que estão sendo incorporados no tempo de execução. Para ver os nomes dos arquivos, anexe o parâmetro `debugClientLibs=true` ao URL da sua página da Web. A biblioteca gerada contém `@import` instruções em vez do código incorporado.

No exemplo na seção anterior [Incorporando código de outras bibliotecas](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries), a pasta da biblioteca de cliente `/etc/client/libraries/myclientlibs/publicmain` incorpora a pasta da biblioteca de cliente `/apps/myapp/clientlib`. Anexar o parâmetro à página da Web produz o seguinte link no código-fonte da página da Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

A abertura do arquivo `publicmain.css` revela o seguinte código:

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Na caixa de endereço do navegador da Web, anexe o seguinte texto ao URL do seu HTML:

   `?debugClientLibs=true`
1. Quando a página for carregada, visualização a fonte da página.
1. Clique no link fornecido como href para o elemento de link para abrir o arquivo e visualização o código fonte.

### Bibliotecas do Discover Client {#discover-client-libraries}

O componente `/libs/cq/granite/components/dumplibs/dumplibs` gera uma página de informações sobre todas as pastas da biblioteca do cliente no sistema. O nó `/libs/granite/ui/content/dumplibs` tem o componente como um tipo de recurso. Para abrir a página, use o seguinte URL (alterando o host e a porta, conforme necessário):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

As informações incluem o caminho e o tipo da biblioteca (CSS ou JS) e os valores dos atributos da biblioteca, como categorias e dependências. As tabelas subsequentes na página mostram as bibliotecas em cada categoria e canal.

### Consulte Saída gerada {#see-generated-output}

O componente `dumplibs` inclui um seletor de teste que exibe o código-fonte gerado para as tags `ui:includeClientLib`. A página inclui código para diferentes combinações de atributos js, css e temáticos.

1. Use um dos seguintes métodos para abrir a página Saída de teste:

   * Na página `dumplibs.html`, clique no link no texto **Clique aqui para obter o teste de saída**.

   * Abra o seguinte URL no navegador da Web (use um host e uma porta diferentes, conforme necessário):

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   A página padrão mostra a saída de tags sem valor para o atributo categoria.

1. Para ver a saída de uma categoria, digite o valor da propriedade `categories` da biblioteca do cliente e clique em **Enviar Query**.

## Configurando o Manuseio de Biblioteca para Desenvolvimento e Produção {#configuring-library-handling-for-development-and-production}

O serviço Gerenciador de biblioteca HTML processa `cq:ClientLibraryFolder` tags e gera as bibliotecas em tempo de execução. O tipo de ambiente, desenvolvimento ou produção determina como você deve configurar o serviço:

* Aumente a segurança: Desativar depuração
* Melhore o desempenho: Remova o espaço em branco e compacte as bibliotecas.
* Melhore a legibilidade: Inclua espaços em branco e não compacte.

Para obter informações sobre como configurar o serviço, consulte [AEM Gerenciador de biblioteca HTML](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
