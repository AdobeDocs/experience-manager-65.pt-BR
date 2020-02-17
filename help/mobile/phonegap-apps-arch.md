---
title: Anatomia de um aplicativo
seo-title: Anatomia de um aplicativo
description: Esta página fornece uma descrição dos componentes de página que você cria para seu aplicativo com base no componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite em um servidor local).
seo-description: Esta página fornece uma descrição dos componentes de página que você cria para seu aplicativo com base no componente /libs/mobileapps/components/angular/ng-page (CRXDE Lite em um servidor local).
uuid: 4c1a74c1-85af-4a79-b723-e9fbfc661d35
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 55667e62-a61b-4794-b292-8d54929c41ac
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Anatomia de um aplicativo{#the-anatomy-of-an-app}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

## Modelos de página para aplicativos móveis {#page-templates-for-mobile-apps}

Os componentes de página criados para seu aplicativo são baseados no componente /libs/mobileapps/components/angular/ng-page ([aberto no CRXDE Lite em um servidor](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)local). Este componente contém os seguintes scripts JSP que seu componente herda ou substitui:

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

Determina o nome do aplicativo usando a `applicationName` propriedade e o expõe via pageContext.

Inclui head.jsp e body.jsp.

### head.jsp {#head-jsp}

Grava o `<head>` elemento da página do aplicativo.

Se desejar substituir a propriedade viewport meta do aplicativo, este é o arquivo que você sobrescreve.

Seguindo as práticas recomendadas, o aplicativo inclui a parte css das bibliotecas do cliente no cabeçalho, enquanto o JS está incluído no elemento &lt; `body>` de fechamento.

### body.jsp {#body-jsp}

O corpo de uma página Angular é renderizado de forma diferente dependendo se wcmMode for detectado (!= WCMMode.DISABLED) para determinar se a página está aberta para criação ou como uma página publicada.

**Modo de autor**

No modo de autor, cada página individual é renderizada separadamente. O Angular não lida com o roteamento entre páginas, nem com uma exibição ng usada para carregar um modelo parcial que contém os componentes da página. Em vez disso, o conteúdo do modelo de página (template.jsp) é incluído no lado do servidor por meio da `cq:include` tag .

Essa estratégia habilita os recursos do autor (como adicionar e editar componentes no sistema de parágrafo, Sidekick, modo de design etc.) para funcionar sem modificação. As páginas que dependem da renderização no cliente, como as dos aplicativos, não funcionam bem no modo de autor de AEM.

Observe que a inclusão template.jsp está encapsulada em um `div` elemento que contém a `ng-controller` diretiva. Essa estrutura permite a vinculação do conteúdo do DOM ao controlador. Portanto, embora as páginas que se renderizam no lado do cliente falhem, os componentes individuais que funcionam bem (consulte a seção Componentes abaixo).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Modo de publicação**

No modo de publicação (como quando o aplicativo é exportado usando a Sincronização de conteúdo), todas as páginas se tornam um aplicativo de página única (SPA). (Para saber mais sobre SPAs, use o tutorial Angular, especificamente [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07).)

Há apenas uma página HTML em um SPA (uma página que contém o `<html>` elemento). Esta página é conhecida como &quot;modelo de layout&quot;. Na terminologia angular, é &quot;...um modelo comum para todas as exibições em nosso aplicativo.&quot; Considere esta página como a &quot;página de aplicativos de nível superior&quot;. Por convenção, a página do aplicativo de nível superior é o `cq:Page` nó do aplicativo mais próximo da raiz (e não é um redirecionamento).

Como o URI real do aplicativo não é alterado no modo de publicação, as referências a ativos externos desta página devem usar caminhos relativos. Portanto, é fornecido um componente de imagem especial que leva essa página de nível superior em conta ao renderizar imagens para exportação.

Como um SPA, esta página de modelo de layout simplesmente gera um elemento div com uma diretiva de exibição ng.

```xml
 <div ng-view ng-class="transition"></div>
```

O serviço de rota angular usa esse elemento para exibir o conteúdo de cada página no aplicativo, incluindo o conteúdo criável da página atual (contido em template.jsp).

O arquivo body.jsp inclui header.jsp e footer.jsp que estão vazios. Se desejar fornecer conteúdo estático em cada página, você pode substituir esses scripts no aplicativo.

Por fim, clientlibs javascript são incluídos na parte inferior do elemento &lt;body>, incluindo dois arquivos JS especiais que são gerados no servidor: *&lt;page name>*.angle-app-module.js e *&lt;page name>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

Esse script define o módulo Angular do aplicativo. A saída desse script está vinculada à marcação gerada pelo restante do componente do modelo pelo `html` elemento em ng-page.jsp, que contém o seguinte atributo:

```xml
ng-app="<c:out value='${applicationName}'/>"
```

Este atributo indica ao Angular que o conteúdo deste elemento DOM deve ser vinculado ao seguinte módulo. Este módulo vincula as exibições (no AEM, seriam recursos cq:Page) com controladores correspondentes.

Este módulo também define um controlador de nível superior chamado `AppController` , que expõe a `wcmMode` variável ao escopo, e configura o URI do qual buscar cargas de atualização de Sincronização de conteúdo.

Por fim, este módulo repete cada página descendente (incluindo ele mesmo) e renderiza o conteúdo do enquadramento da rota de cada página (através do seletor e extensão do route-fragment.js) angular, incluindo-o como uma entrada de configuração para o $routeProvider da Angular. Em outras palavras, o $routeProvider informa ao aplicativo qual conteúdo renderizar quando um determinado caminho é solicitado.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

Esse script gera um fragmento JavaScript que deve assumir o seguinte formato:

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

Este código indica para $routeProvider (definido em angular-app-module.js.jsp) que &#39;/&lt;caminho>&#39; deve ser manipulado pelo recurso em `templateUrl`e conectado por `controller` (o que chegaremos em seguida).

Se necessário, é possível substituir esse script para manipular caminhos mais complexos, incluindo aqueles com variáveis. Um exemplo disso pode ser visto no script /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp instalado com o AEM:

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

Em angular, os controladores conectam variáveis no $scope, expondo-as à exibição. O script angular-app-controllers.js.jsp segue o padrão ilustrado pelo angular-app-module.js.jsp, pois ele é repetido em cada página descendente (incluindo ele mesmo) e gera o fragmento do controlador definido por cada página (via controller.js.jsp). O módulo definido é chamado `cqAppControllers` e deve ser listado como uma dependência do módulo de aplicativo de nível superior para que os controladores de página fiquem disponíveis.

### controller.js.jsp {#controller-js-jsp}

O script controller.js.jsp gera o fragmento do controlador para cada página. Esse fragmento do controlador assume o seguinte formato:

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

Observe que a `data` variável recebe a promessa retornada pelo `$http.get` método Angular. Cada componente incluído nesta página pode, se desejado, disponibilizar algum conteúdo .json (por meio de seu script angular.json.jsp) e agir sobre o conteúdo dessa solicitação quando for resolvido. A solicitação é muito rápida em dispositivos móveis porque simplesmente acessa o sistema de arquivos.

Para que um componente faça parte do controlador dessa forma, ele deve estender o componente /libs/mobileapps/components/angular/ng-componente e incluir a `frameworkType: angular` propriedade.

### template.jsp {#template-jsp}

Introduzido pela primeira vez na seção body.jsp, template.jsp simplesmente contém os parsys da página. No modo de publicação, esse conteúdo é referenciado diretamente (em &lt;page-path>.template.html) e carregado no SPA por meio do templateUrl configurado no $routeProvider.

O parsys neste script pode ser configurado para aceitar qualquer tipo de componente. No entanto, é necessário ter cuidado ao lidar com componentes criados para um site tradicional (em vez de um SPA). Por exemplo, o componente de imagem da base funciona corretamente somente na página do aplicativo de nível superior, pois não foi projetado para fazer referência a ativos que estão dentro de um aplicativo.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

Esse script simplesmente gera as dependências angulares do módulo de aplicativo Angular de nível superior. É referenciado pelo angular-app-module.js.jsp.

### header.jsp {#header-jsp}

Um script para colocar o conteúdo estático na parte superior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da exibição.

### footer.jsp {#footer-jsp}

Um script para colocar o conteúdo estático na parte inferior do aplicativo. Esse conteúdo é incluído pela página de nível superior, fora do escopo da exibição.

### js_clientlibs.jsp {#js-clientlibs-jsp}

Substitua esse script para incluir seus clientlibs JavaScript.

### css_clientlibs.jsp {#css-clientlibs-jsp}

Substitua esse script para incluir seus clientlibs CSS.

## Componentes do aplicativo {#app-components}

Os componentes do aplicativo devem funcionar não apenas em uma instância do AEM (publicar ou criar), mas também quando o conteúdo do aplicativo for exportado para o sistema de arquivos por meio da Sincronização de conteúdo. Por conseguinte, o componente deve incluir as seguintes características:

* Todos os ativos, modelos e scripts em um aplicativo PhoneGap devem ser referenciados relativamente.
* A manipulação de links difere se a instância do AEM estiver operando no modo de autor ou publicação.

### Ativos relativos {#relative-assets}

O URI de qualquer ativo específico em um aplicativo PhoneGap é diferente não apenas por plataforma, mas é único em cada instalação do aplicativo. Por exemplo, observe o seguinte URI de um aplicativo em execução no Simulador do iOS:

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

Observe o GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39; no caminho.

Como desenvolvedor do PhoneGap, o conteúdo com o qual você está preocupado está localizado abaixo do diretório www. Para acessar os ativos do aplicativo, use caminhos relativos.

Para compor o problema, seu aplicativo PhoneGap usa o padrão de aplicativo de página única (SPA) para que o URI base (exceto o hash) nunca seja alterado. Portanto, cada ativo, modelo ou script que você referenciar **deve ser relativo à sua página de nível superior. **A página de nível superior inicializa o roteamento Angular e os controladores em virtude de `*<name>*.angular-app-module.js` e `*<name>*.angular-app-controllers.js`. Esta página deve ser a página mais próxima da raiz do repositório que *não *estende um sling:redirect.

Vários métodos auxiliares estão disponíveis para lidar com caminhos relativos:

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

Para ver exemplos de seu uso, abra a fonte mobileapps localizada em /libs/mobileapps/components/angle.

### Links {#links}

Os links devem usar a `ng-click="go('/path')"` função para suportar todos os modos WCM. Essa função depende do valor de uma variável de escopo para determinar corretamente a ação do link:

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

Quando `$scope.wcmMode == true` lidamos com cada evento de navegação da maneira habitual, de modo que o resultado seja uma alteração no caminho e/ou na parte da página do URL.

Como alternativa, se `$scope.wcmMode == false`, cada evento de navegação resulta em uma alteração na parte hash do URL que é resolvida internamente pelo módulo ngRoute do Angular.

### Detalhes do script do componente {#component-script-details}

![chlimage_1-144](assets/chlimage_1-144.png)

#### ng-component.jsp {#ng-component-jsp}

Esse script exibe o conteúdo do componente ou um espaço reservado adequado quando o modo Editar é detectado.

#### template.jsp {#template-jsp-1}

O script template.jsp renderiza a marcação do componente. Se o componente em questão for conduzido por dados JSON extraídos do AEM (como &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text/template.jsp), esse script será responsável por conectar a marcação com dados expostos pelo escopo do controlador da página.

No entanto, os requisitos de desempenho às vezes determinam que nenhum modelo do lado do cliente (conhecido como vínculo de dados) seja executado. Nesse caso, basta renderizar a marcação do componente no lado do servidor e ela é incluída no conteúdo do modelo da página.

#### head.jsp {#overhead-jsp}

Em componentes movidos por dados JSON (como &quot;ng-text&quot;: /libs/mobileapps/components/angle/ng-text), o arquivo head.jsp pode ser usado para remover todo o código Java de template.jsp. Em seguida, ele é referenciado a partir de template.jsp e quaisquer variáveis que ele expõe na solicitação estão disponíveis para uso. Essa estratégia incentiva a separação da lógica da apresentação e limita a quantidade de código que deve ser copiada e colada quando um novo componente é derivado de um existente.

#### controller.js.jsp {#controller-js-jsp-1}

Conforme descrito em Modelos de página AEM, cada componente pode produzir um fragmento JavaScript para consumir o conteúdo JSON exposto pela `data` promessa. De acordo com as convenções angulares, um controlador só deve ser usado para atribuir variáveis ao escopo.

#### angle.json.jsp {#angular-json-jsp}

Esse script é incluído como um fragmento no arquivo &#39;&lt;page-name>.angular.json&#39; que é exportado para cada página que estende ng-page. Neste arquivo, o desenvolvedor do componente pode expor qualquer estrutura JSON necessária para o componente. No exemplo &#39;ng-text&#39;, essa estrutura simplesmente inclui o conteúdo de texto do componente, e um sinalizador que indica se o componente inclui ou não Rich Text.

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

## Conteúdo do download dos ativos CLI {#contents-of-the-cli-assets-download}

Baixe ativos CLI do console Aplicativos para otimizá-los para uma plataforma específica e crie o aplicativo usando a API CLI (Command Line Integration, integração de linha de comando) do PhoneGap. O conteúdo do arquivo ZIP salvo no sistema de arquivos local tem a seguinte estrutura:

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

Este é um diretório oculto que você pode não ver dependendo das configurações atuais do SO. Você deve configurar o SO para que esse diretório fique visível se planeja modificar os ganchos do aplicativo que ele contém.

#### .cordova/hooks/ {#cordova-hooks}

Este diretório contém os ganchos [CLI](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). As pastas no diretório hooks contêm scripts node.js que são executados em pontos exatos durante a compilação.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

O diretório after-platform_add contém o `copy_AMS_Conifg.js` arquivo. Esse script copia um arquivo de configuração para suportar a coleção de análises do Adobe Mobile Services.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

O diretório after-prepare contém o `copy_resource_files.js` arquivo. Esse script copia várias imagens de ícone e tela de apresentação em locais específicos da plataforma.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

O diretório before_platform_add contém o `install_plugins.js` arquivo. Esse script é repetido por meio de uma lista de identificadores de plug-ins do Cordova, instalando aqueles que ele detecta ainda não estão disponíveis.

Essa estratégia não exige que você agrupe e instale os plug-ins no AEM sempre que o `content-package:install` comando Maven for executado. A estratégia alternativa de verificar os arquivos no seu sistema SCM requer agrupamento repetitivo e atividades de instalação.

#### .cordova/ganchos/Outros ganchos {#cordova-hooks-other-hooks}

Inclua outros ganchos, conforme necessário. Os seguintes ganchos estão disponíveis (conforme fornecido pelo aplicativo Phonegap exemplo hello world):

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

#### platforms/ {#platforms}

Esse diretório fica vazio até que você execute o `phonegap run <platform>` comando no projeto. Atualmente, `<platform>` pode ser `ios` ou `android`.

Depois de criar o aplicativo para uma plataforma específica, o diretório correspondente é criado e ele contém o código do aplicativo específico da plataforma.

#### plugins/ {#plugins}

O diretório de plug-ins é preenchido por cada plug-in listado no `.cordova/hooks/before_platform_add/install_plugins.js` arquivo depois que você executa o `phonegap run <platform>` comando. O diretório está inicialmente vazio.

#### www/ {#www}

O diretório www contém todo o conteúdo da Web (arquivos HTML, JS e CSS) que implementa a aparência e o comportamento do aplicativo. Exceto pelas exceções descritas abaixo, este conteúdo é originário do AEM e é exportado para sua forma estática via Sincronização de conteúdo.

#### www/config.xml {#www-config-xml}

A documentação [do](https://docs.phonegap.com) PhoneGap se refere a esse arquivo como um &quot;arquivo de configuração global&quot;. O config.xml contém várias propriedades do aplicativo, como o nome do aplicativo, as &quot;preferências&quot; do aplicativo (por exemplo, se uma visualização da Web do iOS permite sobreposição) e as dependências do plug-in que são consumidas *somente* pela compilação do PhoneGap.

O arquivo config.xml é um arquivo estático no AEM e é exportado no estado em que está por meio da Sincronização de conteúdo.

#### www/index.html {#www-index-html}

O arquivo index.html redireciona para a página inicial do aplicativo.

O arquivo config.xml contém o `content` elemento:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

Na documentação [](https://docs.phonegap.com)do PhoneGap, esse elemento é descrito como &quot;O elemento &lt;content> opcional define a página inicial do aplicativo no diretório de ativos da Web de nível superior. O valor padrão é index.html, que normalmente aparece no diretório www de nível superior de um projeto.&quot;

A compilação do PhoneGap falhará se um arquivo index.html não estiver presente. Portanto, este arquivo é incluído.

#### www/res {#www-res}

O diretório res contém ícones e imagens de tela de apresentação. O `copy_resource_files.js` script copia os arquivos para seus locais específicos da plataforma durante a fase de `after_prepare` criação.

#### www/etc {#www-etc}

Por convenção, no AEM, o nó /etc contém conteúdo clientlib estático. O diretório etc contém as bibliotecas Topcoat, AngularJS e Geometrixx ng-clientlibsall.

#### www/apps {#www-apps}

O diretório apps contém o código relacionado à página inicial. A característica única da página inicial de um aplicativo AEM é que ele inicializa o aplicativo sem interação do usuário. O conteúdo clientlib (CSS e JS) do aplicativo é, portanto, mínimo para maximizar o desempenho.

#### www/content {#www-content}

O diretório de conteúdo contém o restante do conteúdo da Web do aplicativo. O conteúdo pode incluir, entre outros, os seguintes arquivos:

* Conteúdo da página HTML, que é criado diretamente no AEM
* Ativos de imagem associados aos componentes do AEM
* Conteúdo JavaScript gerado por scripts do lado do servidor
* Arquivos JSON que descrevem o conteúdo da página ou do componente

#### www/package.json {#www-package-json}

O arquivo package.json é um arquivo manifest que lista os arquivos que um download **completo** de Sincronização de conteúdo inclui. Esse arquivo também contém o carimbo de data e hora no qual a carga da Sincronização de conteúdo foi gerada ( `lastModified`). Essa propriedade é usada ao solicitar atualizações parciais do aplicativo do AEM.

#### www/package-update.json {#www-package-update-json}

Se esta carga for um download do aplicativo inteiro, este manifesto contém a lista exata de arquivos como `package.json`.

No entanto, se essa carga for uma atualização parcial, `package-update.json` conterá apenas os arquivos incluídos nessa carga específica.

### Próximas etapas {#the-next-steps}

Depois de saber mais sobre a Anatomia de um aplicativo, consulte Aplicativos [de página](/help/mobile/phonegap-single-page-applications.md)única.
