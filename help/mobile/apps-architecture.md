---
title: Modelos de página para aplicativos móveis
description: Siga esta página para saber mais sobre modelos de página. Os componentes de página criados para seu aplicativo são baseados no componente /libs/mobileapps/components/angular/ng-page.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2587'
ht-degree: 0%

---

# Modelos de página para aplicativos móveis {#page-templates-for-mobile-apps}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

## Modelos de página para aplicativos móveis {#page-templates-for-mobile-apps-1}

Os componentes de página criados para seu aplicativo são baseados no componente /libs/mobileapps/components/angular/ng-page ([abrir no CRXDE Lite em um servidor local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Este componente contém os seguintes scripts JSP que seu componente herda ou substitui:

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

Determina o nome do aplicativo usando a propriedade `applicationName` e o expõe por meio do pageContext.

Inclui head.jsp e body.jsp.

### head.jsp {#head-jsp}

Grava o elemento `<head>` da página do aplicativo.

Se você quiser substituir a metapropriedade viewport do aplicativo, esse será o arquivo que você substituirá.

Seguindo as práticas recomendadas, o aplicativo inclui a parte css das bibliotecas do cliente no cabeçalho, enquanto o JS é incluído no elemento &lt; `body>` de fechamento.

### body.jsp {#body-jsp}

O corpo de uma página de Angular é renderizado de forma diferente dependendo de o wcmMode ser detectado (!= WCMMode.DISABLED) para determinar se a página está aberta para criação ou como uma página publicada.

**Modo de Autor**

No modo de criação, cada página individual é renderizada separadamente. O Angular não lida com o roteamento entre páginas, nem uma ng-view é usada para carregar um modelo parcial que contém os componentes da página. Em vez disso, o conteúdo do modelo de página (template.jsp) é incluído no lado do servidor por meio da tag `cq:include`.

Essa estratégia permite que os recursos do autor (como adicionar e editar componentes no sistema de parágrafo, Sidekick, modo de design e assim por diante) funcionem sem modificação. As páginas que dependem da renderização do lado do cliente, como aquelas para aplicativos, não têm bom desempenho no modo de autor AEM.

A inclusão template.jsp é encapsulada em um elemento `div` que contém a diretiva `ng-controller`. Essa estrutura permite a vinculação do conteúdo DOM com o controlador. Portanto, embora as páginas que se renderizam no lado do cliente falhem, os componentes individuais que o fazem funcionam bem (consulte a seção Componentes abaixo).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo Publish**

No modo de publicação (como quando o aplicativo é exportado usando a Sincronização de conteúdo), todas as páginas se tornam um aplicativo de página única (SPA). (Para saber mais sobre o SPA, use o tutorial do Angular, especificamente [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Há apenas uma página de HTML em um SPA (uma página que contém o elemento `<html>`). Essa página é conhecida como &quot;modelo de layout&quot;. Na terminologia do Angular, é &quot;...um modelo comum a todas as exibições no nosso aplicativo&quot;. Considere essa página como a &quot;página do aplicativo de nível superior&quot;. Por convenção, a página do aplicativo de nível superior é o nó `cq:Page` do seu aplicativo que está mais próximo da raiz (e não é um redirecionamento).

Como o URI real do seu aplicativo não é alterado no modo de publicação, as referências a ativos externos desta página devem usar caminhos relativos. Portanto, é fornecido um componente de imagem especial que considera essa página de nível superior ao renderizar imagens para exportação.

Como um SPA, essa página de modelo de layout simplesmente gera um elemento div com uma diretiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

O serviço de rota de Angular usa esse elemento para exibir o conteúdo de cada página no aplicativo, incluindo o conteúdo autorável da página atual (contido em template.jsp).

O arquivo body.jsp inclui header.jsp e footer.jsp que estão vazios. Se você quiser fornecer conteúdo estático em cada página, é possível substituir esses scripts no aplicativo.

Finalmente, clientlibs de javascript são incluídas na parte inferior do elemento &lt;body>, incluindo dois arquivos JS especiais gerados no servidor: *&lt;page name>*.angular-app-module.js e *&lt;page name>*.angular-app-controllers.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Este script define o módulo Angular do aplicativo. A saída desse script está vinculada à marcação que o restante do componente do modelo gera por meio do elemento `html` em ng-page.jsp, que contém o seguinte atributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Esse atributo indica ao Angular que o conteúdo desse elemento DOM deve ser vinculado ao seguinte módulo. Esse módulo vincula as visualizações (no AEM, seriam cq:Page resources) com os controladores correspondentes.

Esse módulo também define um controlador de nível superior chamado `AppController` que expõe a variável `wcmMode` ao escopo e configura o URI do qual buscar cargas de atualização da Sincronização de Conteúdo.

Por fim, esse módulo itera por cada página descendente (incluindo ele mesmo) e renderiza o conteúdo do fragmento de rota de cada página (por meio do seletor e extensão angular-route-fragment.js), incluindo-o como uma entrada de configuração para o \$routeProvider do Angular. Em outras palavras, o \$routeProvider informa ao aplicativo qual conteúdo deve ser renderizado quando determinado caminho for solicitado.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Esse script gera um fragmento do JavaScript que deve ter o seguinte formato:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica para $routeProvider (definido em angular-app-module.js.jsp) que &#39;/&lt;path>&#39; deve ser manipulado pelo recurso em `templateUrl`, e ligado por `controller` (que chegaremos em seguida).

Se necessário, é possível substituir esse script para manipular caminhos mais complexos, incluindo aqueles com variáveis. Um exemplo disso pode ser visto no script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp que está instalado com AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

No Angular, os Controladores conectam variáveis no \$scope, expondo-as à visualização. O script angular-app-controllers.js.jsp segue o padrão ilustrado por angular-app-module.js.jsp na medida em que repete cada página descendente (incluindo ela mesma) e gera o fragmento do controlador definido por cada página (via controller.js.jsp). O módulo que ele define é chamado de `cqAppControllers` e deve ser listado como uma dependência do módulo de aplicativo de nível superior para que os controladores de página sejam disponibilizados.

### controller.js.jsp {#controller-js-jsp}

O script controller.js.jsp gera o fragmento de controlador para cada página. Esse fragmento de controlador assume o seguinte formato:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

A variável `data` é atribuída à promessa retornada pelo método `$http.get` do Angular. Cada componente incluído nesta página pode, se desejado, disponibilizar conteúdo .json (por meio do script angular.json.jsp) e agir de acordo com o conteúdo dessa solicitação quando ela for resolvida. A solicitação é muito rápida em dispositivos móveis porque simplesmente acessa o sistema de arquivos.

Para que um componente faça parte do controlador dessa maneira, ele deve estender o componente /libs/mobileapps/components/angular/ng-component e incluir a propriedade `frameworkType: angular`.

### template.jsp {#template-jsp}

Introduzido pela primeira vez na seção body.jsp, o template.jsp simplesmente contém o parsys da página. No modo de publicação, esse conteúdo é referenciado diretamente (em &lt;page-path>.template.html) e carregado no SPA por meio do templateUrl configurado no \$routeProvider.

O parsys neste script pode ser configurado para aceitar qualquer tipo de componente. No entanto, é necessário ter cuidado ao lidar com componentes criados para um site tradicional (em vez de um SPA). Por exemplo, o componente de imagem de base funciona corretamente somente na página do aplicativo de nível superior, pois não foi projetado para fazer referência a ativos que estão dentro de um aplicativo.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Esse script simplesmente gera as dependências do Angular do módulo do aplicativo Angular de nível superior. É referenciado por angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Um script para colocar conteúdo estático na parte superior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da ng-view.

### footer.jsp {#footer-jsp}

Um script para colocar conteúdo estático na parte inferior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Substitua esse script para incluir as bibliotecas de clientes do JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Substitua esse script para incluir suas bibliotecas de clientes CSS.

## Componentes do aplicativo {#app-components}

Os componentes do aplicativo devem funcionar não apenas em uma instância AEM (publicação ou autor), mas também quando o conteúdo do aplicativo for exportado para o sistema de arquivos por meio da Sincronização de conteúdo. O componente deve, portanto, incluir as seguintes características:

* Todos os ativos, modelos e scripts em um aplicativo PhoneGap devem ser referenciados relativamente.
* O manuseio de links é diferente se a instância do AEM estiver operando no modo de autor ou publicação.

### Assets relativo {#relative-assets}

O URI de qualquer ativo específico em um aplicativo PhoneGap difere não apenas em uma base por plataforma, mas é exclusivo em cada instalação do aplicativo. Por exemplo, observe o seguinte URI de um aplicativo em execução no iOS Simulator:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe o GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; no caminho.

Como desenvolvedor do PhoneGap, o conteúdo com o qual você está preocupado está localizado abaixo do diretório www. Para acessar os ativos do aplicativo, use caminhos relativos.

Para compor o problema, seu aplicativo PhoneGap usa o padrão de aplicativo de página única (SPA), para que o URI base (excluindo o hash) nunca seja alterado. Portanto, cada ativo, modelo ou script que você menciona **deve ser relativo à sua página de nível superior.** A página de nível superior inicializa o roteamento e os controladores do Angular em virtude de `*<name>*.angular-app-module.js` e `*<name>*.angular-app-controllers.js`. Essa página deve ser a mais próxima da raiz do repositório que *não *estende um sling:redirect.

Vários métodos auxiliares estão disponíveis para lidar com caminhos relativos:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver exemplos de uso, abra a origem mobileapps localizada em /libs/mobileapps/components/angular.

### Links {#links}

Os links devem usar a função `ng-click="go('/path')"` para dar suporte a todos os modos WCM. Essa função depende do valor de uma variável de escopo para determinar corretamente a ação do link:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Quando `$scope.wcmMode == true` lidamos com cada evento de navegação da maneira usual, de forma que o resultado seja uma alteração no caminho e/ou parte da página da URL.

Como alternativa, se `$scope.wcmMode == false`, cada evento de navegação resulta em uma alteração na parte de hash da URL que é resolvida internamente pelo módulo ngRoute do Angular.

### Detalhes do script de componente {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

Este script exibe o conteúdo do componente ou um espaço reservado adequado quando o modo Editar é detectado.

#### template.jsp {#template-jsp-1}

O script template.jsp renderiza a marcação do componente. Se o componente em questão for orientado por dados JSON extraídos do AEM (como &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text/template.jsp), esse script será responsável por conectar a marcação com dados expostos pelo escopo do controlador da página.

No entanto, os requisitos de desempenho às vezes exigem que nenhum modelo do lado do cliente (também conhecido como vinculação de dados) seja executado. Nesse caso, basta renderizar a marcação do componente no lado do servidor e ela será incluída no conteúdo do modelo de página.

#### overhead.jsp {#overhead-jsp}

Em componentes orientados por dados JSON (como &quot;ng-text&quot;: /libs/mobileapps/components/angular/ng-text), overhead.jsp pode ser usado para remover todo o código Java de template.jsp. Ele é referenciado a partir do template.jsp e todas as variáveis que ele expõe na solicitação estão disponíveis para uso. Essa estratégia incentiva a separação da lógica da apresentação e limita a quantidade de código que deve ser copiada e colada quando um novo componente é derivado de um existente.

#### controller.js.jsp {#controller-js-jsp-1}

Conforme descrito em Modelos de página AEM, cada componente pode produzir um fragmento do JavaScript para consumir o conteúdo JSON exposto pela promessa `data`. Seguindo as convenções de Angular, um controlador só deve ser usado para atribuir variáveis ao escopo.

#### angular.json.jsp {#angular-json-jsp}

Esse script é incluído como um fragmento no arquivo &#39;&lt;page-name>.angular.json&#39; de toda a página que é exportado para cada página que estende ng-page. Nesse arquivo, o desenvolvedor do componente pode expor qualquer estrutura JSON exigida pelo componente. No exemplo de &quot;ng-text&quot;, essa estrutura simplesmente inclui o conteúdo do texto do componente e um sinalizador que indica se o componente inclui ou não rich text.

O componente de produto do aplicativo Geometrixx outdoors é um exemplo mais complexo (/apps/geometrixx-outdoors-app/components/angular/ng-product):

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## Conteúdo de download da CLI Assets {#contents-of-the-cli-assets-download}

Baixe ativos de CLI no console Aplicativos para otimizá-los para uma plataforma específica e, em seguida, crie o aplicativo usando a API de integração de linha de comando (CLI) do PhoneGap. O conteúdo do arquivo ZIP que você salva no sistema de arquivos local tem a seguinte estrutura:

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

Este é um diretório oculto que talvez você não veja, dependendo das configurações atuais do sistema operacional. Você deve configurar o sistema operacional para que esse diretório fique visível se quiser modificar os ganchos de aplicativo que ele contém.

#### .cordova/ganchos/ {#cordova-hooks}

Este diretório contém os [ganchos de CLI](https://cordova.apache.org/docs/en/10.x/guide/appdev/hooks/). As pastas no diretório de ganchos contêm scripts node.js que são executados em pontos exatos durante a criação.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

O diretório after-platform_add contém o arquivo `copy_AMS_Conifg.js`. Este script copia um arquivo de configuração para suportar a coleção de análises do Adobe Mobile Services.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

O diretório após a preparação contém o arquivo `copy_resource_files.js`. Esse script copia vários ícones e imagens da tela de abertura em locais específicos da plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

O diretório before_platform_add contém o arquivo `install_plugins.js`. Esse script repete por meio de uma lista de identificadores de plug-in Cordova, instalando aqueles que ele detecta que ainda não estão disponíveis.

Essa estratégia não requer o agrupamento e a instalação dos plug-ins no AEM toda vez que o comando Maven `content-package:install` for executado. A estratégia alternativa de verificar os arquivos no sistema SCM requer o agrupamento repetitivo e a instalação de atividades.

#### .cordova/ganchos/Outros ganchos {#cordova-hooks-other-hooks}

Inclua outros ganchos conforme necessário. Os seguintes ganchos estão disponíveis (conforme fornecido pelo aplicativo Hello world de amostra do Phonegap):

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

#### plataformas/ {#platforms}

Este diretório ficará vazio até que você execute o comando `phonegap run <platform>` no projeto. Atualmente, `<platform>` pode ser `ios` ou `android`.

Depois de criar o aplicativo para uma plataforma específica, o diretório correspondente é criado e contém o código do aplicativo específico da plataforma.

#### plugins/ {#plugins}

O diretório de plug-ins é preenchido por cada plug-in listado no arquivo `.cordova/hooks/before_platform_add/install_plugins.js` depois que você executa o comando `phonegap run <platform>`. O diretório está inicialmente vazio.

#### www/ {#www}

O diretório www contém todo o conteúdo da Web (arquivos HTML, JS e CSS) que implementa a aparência e o comportamento do aplicativo. Exceto pelas exceções descritas abaixo, esse conteúdo é originário do AEM e é exportado para sua forma estática por meio da Sincronização de conteúdo.

#### www/config.xml {#www-config-xml}

A documentação do PhoneGap (`https://docs.phonegap.com`) se refere a esse arquivo como um &#39;arquivo de configuração global&#39;. O config.xml contém muitas propriedades de aplicativo, como o nome do aplicativo, as &quot;preferências&quot; do aplicativo (por exemplo, se um webview do iOS permite ou não a sobrerolagem) e as dependências de plug-in que são *somente* consumidas pela build do PhoneGap.

O arquivo config.xml é um arquivo estático no AEM e é exportado como está pela Sincronização de conteúdo.

#### www/index.html {#www-index-html}

O arquivo index.html redireciona para a página inicial do aplicativo.

O arquivo config.xml contém o elemento `content`:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

Na documentação do PhoneGap (`https://docs.phonegap.com`), esse elemento é descrito como &quot;O elemento opcional &lt;content> define a página inicial do aplicativo no diretório de ativos da Web de nível superior. O valor padrão é index.html, que normalmente aparece em um diretório www de nível superior do projeto.&quot;

A build do PhoneGap falhará se um arquivo index.html não estiver presente. Portanto, esse arquivo está incluído.

#### www/res {#www-res}

O diretório res contém imagens e ícones da tela inicial. O script `copy_resource_files.js` copia os arquivos para seus locais específicos de plataforma durante a fase de compilação `after_prepare`.

#### www/etc {#www-etc}

Por convenção, no AEM, o nó /etc contém conteúdo clientlib estático. O diretório etc contém as bibliotecas Topcoat, AngularJS e Geometrixx-clientlibsall.

#### www/apps {#www-apps}

O diretório apps contém o código relacionado à página inicial. A característica única da página inicial de um aplicativo AEM é que ele inicializa o aplicativo sem nenhuma interação com o usuário. O conteúdo clientlib (CSS e JS) do aplicativo é, portanto, mínimo para maximizar o desempenho.

#### www/content {#www-content}

O diretório de conteúdo contém o restante do conteúdo da Web do aplicativo. O conteúdo pode incluir, mas não está limitado aos seguintes arquivos:

* conteúdo da página HTML, que é criado diretamente no AEM
* Ativos de imagem associados aos componentes do AEM
* Conteúdo do JavaScript gerado por scripts do lado do servidor
* Arquivos JSON que descrevem o conteúdo da página ou do componente

#### www/package.json {#www-package-json}

O arquivo package.json é um arquivo de manifesto que lista os arquivos incluídos por um download da Sincronização de Conteúdo **completo**. Esse arquivo também contém o carimbo de data e hora em que a carga da sincronização de conteúdo foi gerada (`lastModified`). Essa propriedade é usada ao solicitar atualizações parciais do aplicativo do AEM.

#### www/package-update.json {#www-package-update-json}

Se esta carga for um download do aplicativo inteiro, este manifesto conterá a listagem exata dos arquivos como `package.json`.

No entanto, se essa carga for uma atualização parcial, `package-update.json` conterá apenas os arquivos incluídos nessa carga específica.
