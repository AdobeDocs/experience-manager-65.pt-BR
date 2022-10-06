---
title: Aplicativos de página única
seo-title: Single Page Applications
description: Siga esta página para saber mais sobre aplicativos de página única, ou seja, você pode criar um aplicativo com desempenho idêntico em um desktop ou aplicativo móvel.
seo-description: Follow this page to learn about single page applications, that is, you can create an application that performs identically to a desktop or mobile application.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---

# Aplicativos de página única{#single-page-applications}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

[Aplicativos de página única](https://en.wikipedia.org/wiki/Single-page_application) (SPA) atingiram massa crítica, amplamente considerada como o padrão mais eficaz para construir experiências sem interrupções com a tecnologia da Web. Seguindo um padrão de SPA, você pode criar um aplicativo com desempenho idêntico a um aplicativo móvel ou de desktop, mas atinge uma variedade de plataformas de dispositivos e fatores de forma devido à sua base em padrões da Web abertos.

De modo geral, SPA parecem ser mais eficientes do que os sites baseados em páginas tradicionais, pois eles normalmente carregam uma HTML page completa **somente uma vez** (incluindo CSS, JS e conteúdo de fonte de suporte) e, em seguida, carregar somente o que é necessário sempre que uma alteração de estado ocorrer no aplicativo. O que é necessário para essa mudança de estado pode variar com base no conjunto de tecnologias escolhidas, mas geralmente inclui um único fragmento de HTML para substituir a &quot;visualização&quot; existente e a execução de um bloco de código JS para articular a nova exibição e executar qualquer renderização de modelo do lado do cliente que seja necessária. A velocidade dessa alteração de estado pode ser aprimorada ainda mais, por meio do suporte a mecanismos de armazenamento de modelo ou até mesmo do acesso offline ao conteúdo do modelo, se o Adobe PhoneGap for usado.

O AEM 6.1 é compatível com a criação e o gerenciamento de SPA por meio de AEM aplicativos. Este artigo fornecerá uma introdução aos conceitos subjacentes ao SPA e como eles se aproveitam [AngularJS](https://angularjs.org/) para trazer sua marca para a App Store e a Google Play.

## SPA em aplicativos AEM {#spa-in-aem-apps}

A estrutura Aplicativo de página única em AEM aplicativos permite o alto desempenho de um aplicativo AngularJS, enquanto capacita autores (ou outra equipe não técnica) a criar e gerenciar o conteúdo do aplicativo por meio do ambiente otimizado para toque, do editor de arrastar e soltar, que tradicionalmente tem sido reservado para gerenciar sites. Já tem um site criado com AEM? Você descobrirá que reutilizar o conteúdo, os componentes, os fluxos de trabalho, os ativos e as permissões é fácil com os aplicativos AEM.

## Módulo de aplicativo AngularJS {#angularjs-application-module}

AEM aplicativos lida com grande parte da configuração AngularJS para você, incluindo a montagem do módulo de nível superior do seu aplicativo. Por padrão, esse módulo é chamado de &#39;AEMAngularApp&#39; e o script responsável pela sua geração pode ser encontrado (e sobreposto) em /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte da inicialização do aplicativo envolve especificar em quais módulos AngularJS o aplicativo depende. A lista de módulos usados pelo seu aplicativo é especificada por um script localizado em /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, e pode ser sobreposta pelo componente de página do seu próprio aplicativo para receber qualquer módulo AngularJS adicional exigido pelo seu aplicativo. Como exemplo, compare o script acima com a implementação do Geometrixx (localizada em /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para oferecer suporte à navegação entre os estados distintos no aplicativo, o script do módulo angular-app itera por todas as páginas descendentes da página do aplicativo de nível superior para gerar um conjunto de &quot;rotas&quot; e configura cada caminho no serviço Angular $routeProvider. Para obter um exemplo de como isso se parece na prática, consulte o script angular-app-module gerado pelo exemplo de aplicativo Geometrixx Outdoors: (o link requer uma instância local) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Ao fazer logon no AEMAngularApp gerado, você encontrará uma série de rotas especificadas da seguinte maneira:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

A amostra acima ilustra um exemplo de transmissão de um parâmetro como parte do caminho. Neste exemplo, estamos indicando que quando um caminho que atende ao padrão especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id) é solicitado, ele deve ser manipulado pelo modelo home/products.template.html e usar o controlador &#39;contentphonegapgeometrixoutorsenhomeproducts&#39;.

O modelo a ser carregado quando essa rota for solicitada é especificado pela propriedade templateUrl . Esse template conterá o HTML de AEM componentes que foram incluídos na página, bem como quaisquer diretivas AngularJS necessárias para a fiação do lado do cliente do aplicativo. Para obter um exemplo de uma diretiva AngularJS em um componente do Geometrixx, consulte a linha 45 do script swipe-carousel&#39;s template.jsp (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controladores de página {#page-controllers}

Em palavras do Angular, &quot;um Controlador é uma função do construtor JavaScript usada para aumentar o Escopo do Angular&quot;. ([source](https://docs.angularjs.org/guide/controller)) Cada página em um aplicativo AEM é automaticamente conectada a um controlador que pode ser aumentado por qualquer controlador que especifique um `frameworkType` de `angular`. Consulte o componente ng-text como um exemplo (/libs/mobileapps/components/angular/ng-text), incluindo o nó cq:template que garante que cada vez que esse componente for adicionado a uma página, ele inclua essa propriedade importante.

Para um exemplo de controlador mais complexo, abra o script ng-template-page controller.jsp (localizado em /apps/geometrixx-outdoors-app/components/angular/ng-template-page). Particularmente interessante é o código javascript gerado quando executado, que renderiza da seguinte maneira:

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

No exemplo acima, você observará que estamos tomando um parâmetro da variável `$routeParams` e massacrá-lo na estrutura do diretório em que nossos dados JSON são armazenados. Ao lidar com o sku `id` dessa forma, podemos fornecer um único modelo de Produto que possa renderizar os dados do produto para milhares de produtos distintos. Este é um modelo muito mais escalável que requer uma rota individual para cada item em um banco de dados de produtos (potencialmente) massivo.

Há também dois componentes em funcionamento aqui: ng-product amplia o escopo com os dados que extrai do acima `$http` chame. Também há uma ng-image nesta página que, por sua vez, também aumenta o escopo com o valor que ela recupera da resposta. Em virtude do Angular `$http` , cada componente aguardará com paciência até que a solicitação seja concluída e a promessa criada seja cumprida.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre os Aplicativos de página única, consulte [Desenvolvimento de aplicativos com CLI PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
