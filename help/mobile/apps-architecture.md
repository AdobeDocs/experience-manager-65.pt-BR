---
title: Modelos de página para aplicativos móveis
seo-title: Page Templates for Mobile Apps
description: Siga esta página para saber mais sobre templates de página. Os componentes de página criados para seu aplicativo são baseados no componente /libs/mobileapps/components/angular/ng-page.
seo-description: Follow this page to learn more about page templates. Page components that you create for your app are based on the /libs/mobileapps/components/angular/ng-page component.
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 0%

---

# Modelos de página para aplicativos móveis {#page-templates-for-mobile-apps}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

## Modelos de página para aplicativos móveis {#page-templates-for-mobile-apps-1}

Os componentes de página criados para seu aplicativo são baseados no componente /libs/mobileapps/components/angular/ng-page ([abrir no CRXDE Lite em um servidor local](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). Esse componente contém os seguintes scripts JSP que seu componente herda ou substitui:

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

Determina o nome do aplicativo usando o `applicationName` e a expõe por meio do pageContext.

Inclui head.jsp e body.jsp.

### head.jsp {#head-jsp}

Grava o `<head>` elemento da página do aplicativo.

Se você quiser substituir a propriedade meta viewport do aplicativo, esse será o arquivo que você substituirá.

Seguindo as práticas recomendadas, o aplicativo inclui a parte css das bibliotecas de clientes no cabeçalho, enquanto o JS é incluído no fechamento &lt; `body>` elemento.

### body.jsp {#body-jsp}

O corpo de uma página do Angular é renderizado de forma diferente dependendo se wcmMode é detectado (!= WCMMode.DISABLED) para determinar se a página está aberta para criação ou como uma página publicada.

**Modo de Autor**

No modo autor, cada página individual é renderizada separadamente. O Angular não lida com o roteamento entre páginas, nem é uma ng-view usada para carregar um modelo parcial que contém os componentes da página. Em vez disso, o conteúdo do modelo de página (template.jsp) é incluído no lado do servidor por meio do `cq:include` .

Essa estratégia habilita os recursos do autor (como adicionar e editar componentes no sistema de parágrafo, Sidekick, modo de design etc.) para funcionar sem modificação. As páginas que dependem da renderização do lado do cliente, como aquelas para aplicativos, não funcionam bem AEM modo de criação.

Observe que a inclusão de template.jsp está encapsulada em um `div` elemento que contém o `ng-controller` diretiva. Essa estrutura permite a vinculação do conteúdo DOM à controladora. Portanto, embora as páginas que se renderizam no lado do cliente falhem, os componentes individuais que o fazem funcionam bem (consulte a seção Componentes abaixo).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo de publicação**

No modo de publicação (como quando o aplicativo é exportado usando a Sincronização de conteúdo), todas as páginas se tornam um aplicativo de página única (SPA). (Para saber mais sobre SPA, use o tutorial do Angular, especificamente [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Há apenas uma HTML page em um SPA (uma página que contém a variável `<html>` elemento). Essa página é conhecida como &quot;modelo de layout&quot;. Na terminologia do Angular, é &quot;...um modelo comum para todas as exibições em nosso aplicativo.&quot; Considere esta página como a &quot;página do aplicativo de nível superior&quot;. Por convenção, a página do aplicativo de nível superior é a `cq:Page` nó do aplicativo mais próximo da raiz (e que não é um redirecionamento).

Como o URI real do aplicativo não muda no modo de publicação, as referências a ativos externos desta página devem usar caminhos relativos. Portanto, é fornecido um componente de imagem especial que considera essa página de nível superior ao renderizar imagens para exportação.

Como SPA, essa página de modelo de layout simplesmente gera um elemento div com uma diretiva ng-view.

```xml
 <div ng-view ng-class="transition"></div>
```

O serviço de rota do Angular usa esse elemento para exibir o conteúdo de cada página no aplicativo, incluindo o conteúdo autorável da página atual (contido em template.jsp).

O arquivo body.jsp inclui header.jsp e footer.jsp que estão vazios. Se quiser fornecer conteúdo estático em cada página, é possível substituir esses scripts no aplicativo.

Por fim, as clientlibs do javascript são incluídas na parte inferior da variável &lt;body> elemento incluindo dois arquivos JS especiais gerados no servidor: *&lt;page name=&quot;&quot;>*.angular-app-module.js e *&lt;page name=&quot;&quot;>*.angular-app-controladores.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Esse script define o módulo Angular do aplicativo. A saída desse script é vinculada à marcação gerada pelo restante do componente do modelo por meio da variável `html` em ng-page.jsp, que contém o seguinte atributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Esse atributo indica ao Angular que o conteúdo desse elemento DOM deve ser vinculado ao seguinte módulo. Esse módulo vincula as exibições (em AEM seriam recursos cq:Page) aos controladores correspondentes.

Esse módulo também define um controlador de nível superior chamado `AppController` que expõe a variável `wcmMode` para o escopo e configura o URI do qual buscar cargas de atualização da Sincronização de conteúdo.

Por fim, esse módulo faz uma iteração em cada página descendente (incluindo ele mesmo) e renderiza o conteúdo da divisão da rota de cada página (por meio do seletor e extensão angular-route-fragment.js), incluindo-a como uma entrada de configuração para o Angular \$routeProvider. Em outras palavras, o \$routeProvider informa ao aplicativo qual conteúdo renderizar quando um determinado caminho é solicitado.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Esse script gera um fragmento JavaScript que deve assumir o seguinte formulário:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica para $routeProvider (definido em angular-app-module.js.jsp) que &#39;/&lt;path>&#39; deve ser tratado pelo recurso em `templateUrl`e conectado por `controller` (o que chegaremos a seguir).

Se necessário, é possível substituir esse script para lidar com caminhos mais complexos, incluindo aqueles com variáveis. Um exemplo disso pode ser visto no script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp instalado com o AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

No Angular, controladores conectam variáveis no escopo \$s, expondo-as à visualização. O script angular-app-controllers.js.jsp segue o padrão ilustrado por angular-app-module.js.jsp , na medida em que ele repete cada página descendente (incluindo ele mesmo) e gera o fragmento do controlador que cada página define (via controller.js.jsp). O módulo que ele define é chamado de `cqAppControllers` e devem ser listados como uma dependência do módulo de aplicativo de nível superior para que os controladores de página sejam disponibilizados.

### controller.js.jsp {#controller-js-jsp}

O script controller.js.jsp gera o fragmento do controlador para cada página. Esse fragmento de controlador tem o seguinte formato:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Observe que a variável `data` for atribuída à promessa retornada pelo Angular `$http.get` método . Cada componente incluído nesta página pode, se desejado, disponibilizar algum conteúdo .json (por meio de seu script angular.json.jsp) e agir sobre o conteúdo dessa solicitação quando for resolvida. A solicitação é muito rápida em dispositivos móveis porque simplesmente acessa o sistema de arquivos.

Para que um componente faça parte do controlador dessa forma, ele deve estender o componente /libs/mobileapps/components/angular/ng-component e incluir o `frameworkType: angular` propriedade.

### template.jsp {#template-jsp}

Primeiro introduzido na seção body.jsp, template.jsp simplesmente contém o parsys da página. No modo de publicação, esse conteúdo é referenciado diretamente (em &lt;page-path>.template.html) e carregada no SPA por meio do templateUrl configurado no \$routeProvider.

Os parsys neste script podem ser configurados para aceitar qualquer tipo de componente. No entanto, deve-se ter cuidado ao lidar com componentes que são criados para um site tradicional (em vez de um SPA). Por exemplo, o componente de imagem de base funciona corretamente apenas na página do aplicativo de nível superior, pois não foi projetado para fazer referência a ativos que estão dentro de um aplicativo.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Esse script simplesmente gera as dependências do Angular do módulo de aplicativo Angular de nível superior. É referenciado por angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Um script para colocar conteúdo estático na parte superior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da ng-view.

### footer.jsp {#footer-jsp}

Um script para colocar conteúdo estático na parte inferior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da ng-view.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Substitua esse script para incluir suas clientlibs do JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Substitua esse script para incluir suas clientlibs de CSS.

## Componentes do aplicativo {#app-components}

Os componentes do aplicativo devem funcionar não apenas em uma instância do AEM (publicar ou criar), mas também quando o conteúdo do aplicativo for exportado para o sistema de arquivos por meio da Sincronização de conteúdo. Por conseguinte, o componente deve incluir as seguintes características:

* Todos os ativos, modelos e scripts em um aplicativo PhoneGap devem ser referenciados relativamente.
* A manipulação de links difere se a instância de AEM estiver operando no modo de criação ou publicação.

### Ativos relativos {#relative-assets}

O URI de qualquer ativo específico em um aplicativo PhoneGap é diferente não apenas por plataforma, mas é único em cada instalação do aplicativo. Por exemplo, observe o seguinte URI de um aplicativo em execução no Simulador de iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe o GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; no caminho.

Como desenvolvedor do PhoneGap, o conteúdo com o qual você está preocupado está localizado abaixo do diretório www. Para acessar os ativos do aplicativo, use caminhos relativos.

Para compor o problema, o aplicativo PhoneGap usa o padrão de aplicativo de página única (SPA) para que o URI base (excluindo o hash) nunca mude. Portanto, cada ativo, modelo ou script que você referencia **deve ser relativa à página de nível superior.** A página de nível superior inicializa o roteamento e os controladores do Angular em virtude do `*<name>*.angular-app-module.js` e `*<name>*.angular-app-controllers.js`. Esta página deve ser a página mais próxima da raiz do repositório que *não estende um sling:redirect.

Vários métodos de ajuda estão disponíveis para lidar com caminhos relativos:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver exemplos de seu uso, abra a fonte mobileapps localizada em /libs/mobileapps/components/angular.

### Links {#links}

Os links devem usar o `ng-click="go('/path')"` para suportar todos os modos WCM. Essa função depende do valor de uma variável de escopo para determinar corretamente a ação do link:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

When `$scope.wcmMode == true` lidamos com cada evento de navegação da maneira usual, de modo que o resultado seja uma alteração no caminho e/ou parte da página do URL.

Como alternativa, se `$scope.wcmMode == false`, cada evento de navegação resulta em uma alteração na parte de hash do URL que é resolvida internamente pelo módulo Angular ngRoute.

### Detalhes do script de componente {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

Esse script exibe o conteúdo do componente ou um espaço reservado adequado quando o modo Editar é detectado.

#### template.jsp {#template-jsp-1}

O script template.jsp renderiza a marcação do componente. Se o componente em questão for conduzido por dados JSON extraídos de AEM (como &#39;ng-text&#39;): /libs/mobileapps/components/angular/ng-text/template.jsp), esse script será responsável pela fiação da marcação com dados expostos pelo escopo do controlador da página.

No entanto, os requisitos de desempenho às vezes determinam que nenhum modelo do lado do cliente (também conhecido como vínculo de dados) seja executado. Nesse caso, basta renderizar a marcação do componente no lado do servidor e ela é incluída no conteúdo do modelo da página.

#### overhead.jsp {#overhead-jsp}

Em componentes movidos por dados JSON (como &#39;ng-text&#39;): /libs/mobileapps/components/angular/ng-text), overhead.jsp pode ser usado para remover todo o código Java de template.jsp. Ela é referenciada a partir de template.jsp e quaisquer variáveis que ela exponha na solicitação estão disponíveis para uso. Essa estratégia incentiva a separação da lógica da apresentação e limita a quantidade de código que deve ser copiado e colado quando um novo componente é derivado de um existente.

#### controller.js.jsp {#controller-js-jsp-1}

Conforme descrito em AEM Modelos de página, cada componente pode produzir um fragmento JavaScript para consumir o conteúdo JSON exposto pela variável `data` promessa. Seguindo as convenções de Angular, um controlador só deve ser usado para atribuir variáveis ao escopo.

#### angular.json.jsp {#angular-json-jsp}

Este script é incluído como um fragmento no &#39;&lt;page-name>Arquivo .angular.json que é exportado para cada página que estende ng-page. Nesse arquivo, o desenvolvedor do componente pode expor qualquer estrutura JSON necessária para o componente. No exemplo &quot;ng-text&quot;, essa estrutura simplesmente inclui o conteúdo de texto do componente e um sinalizador que indica se o componente inclui ou não rich text.

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

## Conteúdo do download dos ativos da CLI {#contents-of-the-cli-assets-download}

Baixe ativos da CLI no console Aplicativos para otimizá-los para uma plataforma específica e, em seguida, crie o aplicativo usando a API da CLI (Command Line Integration, integração de linha de comando) do PhoneGap. O conteúdo do arquivo ZIP salvo no sistema de arquivos local tem a seguinte estrutura:

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

Esse é um diretório oculto que você pode não ver, dependendo das configurações atuais do sistema operacional. Você deve configurar o sistema operacional para que esse diretório fique visível se planeja modificar os ganchos do aplicativo que ele contém.

#### .cordova/hooks/ {#cordova-hooks}

Esse diretório contém o [Ganchos da CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). As pastas no diretório hooks contêm scripts node.js que são executados em pontos exatos durante a criação.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

O diretório after-platform_add contém a variável `copy_AMS_Conifg.js` arquivo. Este script copia um arquivo de configuração para suportar a coleção da análise do Adobe Mobile Services.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

O diretório depois da preparação contém a variável `copy_resource_files.js` arquivo. Esse script copia várias imagens de ícone e tela inicial em locais específicos da plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

O diretório before_platform_add contém a variável `install_plugins.js` arquivo. Esse script é repetido por meio de uma lista de identificadores de plug-ins Cordova, instalando aqueles que ele detecta ainda não estão disponíveis.

Essa estratégia não requer o empacotamento e a instalação de plug-ins para AEM sempre que o Maven `content-package:install` é executado. A estratégia alternativa de verificar os arquivos no sistema SCM requer o agrupamento repetitivo e a instalação de atividades.

#### .cordova/hooks/Other Hooks {#cordova-hooks-other-hooks}

Inclua outros ganchos, conforme necessário. Os seguintes ganchos estão disponíveis (conforme fornecido pelo aplicativo Phonegap sample hello world):

* after_build
* before_build
* after_compilation
* before_compilation
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

Esse diretório fica vazio até que você execute o `phonegap run <platform>` no projeto. Atualmente, `<platform>` pode ser `ios` ou `android`.

Depois de criar o aplicativo para uma plataforma específica, o diretório correspondente é criado e contém o código de aplicativo específico da plataforma.

#### plugins/ {#plugins}

O diretório de plug-ins é preenchido por cada plug-in listado no `.cordova/hooks/before_platform_add/install_plugins.js` após executar o `phonegap run <platform>` comando. Inicialmente, o diretório está vazio.

#### www/ {#www}

O diretório www contém todo o conteúdo da Web (HTML, JS e arquivos CSS) que implementa a aparência e o comportamento do aplicativo. Exceto pelas exceções descritas abaixo, esse conteúdo é originário de AEM e exportado para seu formulário estático por meio da Sincronização de conteúdo.

#### www/config.xml {#www-config-xml}

O [Documentação do PhoneGap](https://docs.phonegap.com) refere-se a esse arquivo como um &quot;arquivo de configuração global&quot;. O config.xml contém muitas propriedades de aplicativo, como o nome do aplicativo, as &quot;preferências&quot; do aplicativo (por exemplo, se uma visualização da Web do iOS permite ou não a rolagem) e as dependências de plug-in que são *only* consumida pela build do PhoneGap.

O arquivo config.xml é um arquivo estático no AEM e é exportado como está por meio da Sincronização de conteúdo.

#### www/index.html {#www-index-html}

O arquivo index.html redireciona para a página inicial do aplicativo.

O arquivo config.xml contém a variável `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

Em [a documentação do PhoneGap](https://docs.phonegap.com), este elemento é descrito como &quot;O elemento opcional &lt;content> O elemento define a página inicial do aplicativo no diretório de ativos da Web de nível superior. O valor padrão é index.html, que normalmente aparece no diretório www de nível superior de um projeto.&quot;

A build do PhoneGap falhará se um arquivo index.html não estiver presente. Portanto, esse arquivo é incluído.

#### www/res {#www-res}

O diretório res contém imagens e ícones de tela inicial. O `copy_resource_files.js` O script copia os arquivos para seus locais específicos da plataforma durante a `after_prepare` fase de criação.

#### www/etc {#www-etc}

Por convenção, AEM nó /etc contém conteúdo clientlib estático. O diretório etc contém as bibliotecas Topcoat, AngularJS e Geometrixx-clientlibsall.

#### www/apps {#www-apps}

O diretório de aplicativos contém o código relacionado à página inicial. A característica única da página inicial de um aplicativo AEM é que ele inicializa o aplicativo sem interação do usuário. Portanto, o conteúdo clientlib (CSS e JS) do aplicativo é mínimo para maximizar o desempenho.

#### www/content {#www-content}

O diretório de conteúdo contém o restante do conteúdo da Web do aplicativo. O conteúdo pode incluir, entre outros, os seguintes arquivos:

* Conteúdo de HTML page, criado diretamente em AEM
* Ativos de imagem associados aos componentes de AEM
* Conteúdo JavaScript gerado por scripts do lado do servidor
* Arquivos JSON que descrevem o conteúdo da página ou do componente

#### www/package.json {#www-package-json}

O arquivo package.json é um arquivo manifest que lista os arquivos que uma **full** O download da Sincronização de conteúdo inclui. Esse arquivo também contém o carimbo de data e hora em que a carga da Sincronização de conteúdo foi gerada (`lastModified`). Essa propriedade é usada ao solicitar atualizações parciais do aplicativo do AEM.

#### www/package-update.json {#www-package-update-json}

Se esta carga for um download de todo o aplicativo, este manifesto contém a listagem exata de arquivos como `package.json`.

No entanto, se essa carga for uma atualização parcial, `package-update.json` contém apenas os arquivos incluídos nesta carga específica.
