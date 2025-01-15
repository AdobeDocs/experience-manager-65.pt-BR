---
title: Aplicativos de página única
description: Siga esta página para saber mais sobre aplicativos de página única, ou seja, você pode criar um aplicativo que tenha o mesmo desempenho de um aplicativo móvel ou desktop.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Aplicativos de página única{#single-page-applications}

{{ue-over-mobile}}

[Aplicativos de Página Única](https://en.wikipedia.org/wiki/Single-page_application) (SPA) atingiram massa crítica, amplamente considerada como o padrão mais eficaz para a criação de experiências perfeitas com a tecnologia da Web. Seguindo um padrão SPA, você pode criar um aplicativo que tenha o mesmo desempenho de um aplicativo móvel ou desktop, mas que alcance uma variedade de plataformas de dispositivos e fatores de forma devido à sua base em padrões abertos da Web.

De modo geral, o SPA parece ter mais desempenho do que os sites tradicionais baseados em página, pois eles normalmente carregam uma página de HTML completa **apenas uma vez** (incluindo CSS, JS e conteúdo de fonte de suporte) e, em seguida, carregam apenas exatamente o que é necessário sempre que ocorre uma alteração de estado no aplicativo. O que é necessário para essa mudança de estado pode variar com base no conjunto de tecnologias escolhidas, mas normalmente inclui um único fragmento de HTML para substituir a &quot;visualização&quot; existente, e a execução de um bloco de código JS para conectar a nova visualização e executar qualquer renderização de modelo do lado do cliente que seja necessária. A velocidade dessa alteração de estado pode ser melhorada ainda mais com o suporte a mecanismos de cache de modelos ou até mesmo acesso offline ao conteúdo do modelo, se o Adobe PhoneGap for usado.

O AEM 6.1 é compatível com a criação e o gerenciamento do SPA por meio de aplicativos AEM. Este artigo fornece uma introdução aos conceitos por trás do SPA e como ele usa o [AngularJS](https://angularjs.org/) para trazer sua marca para a App Store e para o Google Play.

## SPA em aplicativos AEM {#spa-in-aem-apps}

A estrutura de aplicativo de página única em aplicativos AEM permite o alto desempenho de um aplicativo AngularJS, enquanto permite que os autores (ou outra equipe não técnica) criem e gerenciem o conteúdo do aplicativo por meio do ambiente do editor de arrastar e soltar otimizado para toque, que tradicionalmente era reservado para o gerenciamento de sites. Já possui um site construído com AEM? Você acha que reutilizar conteúdo, componentes, fluxos de trabalho, ativos e permissões é fácil com aplicativos AEM.

## Módulo do aplicativo AngularJS {#angularjs-application-module}

Os aplicativos AEM lidam com grande parte da configuração AngularJS para você, incluindo a montagem do módulo de nível superior do seu aplicativo. Por padrão, esse módulo é chamado de &quot;AEMAngularApp&quot; e o script responsável por sua geração pode ser encontrado (e sobreposto) em /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte da inicialização do aplicativo envolve especificar de quais módulos AngularJS o aplicativo depende. A lista de módulos usados pelo seu aplicativo é especificada por um script localizado em /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, e pode ser sobreposta pelo componente da página dos seus próprios aplicativos para receber qualquer módulo AngularJS adicional exigido pelo seu aplicativo. Como exemplo, compare o script acima com a implementação do Geometrixx (localizada em /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para oferecer suporte à navegação entre os estados distintos no aplicativo, o script angular-app-module itera por todas as páginas descendentes da página do aplicativo de nível superior para gerar um conjunto de &quot;rotas&quot; e configura cada caminho no serviço $routeProvider do Angular. Para obter um exemplo de como isso é exibido na prática, verifique o script angular-app-module gerado pela amostra de aplicativo Geometrixx Outdoors: (o link requer uma instância local) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Ao acessar o AEMAngularApp gerado, você encontrará uma série de rotas especificadas da seguinte maneira:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

A amostra acima ilustra, em particular, um exemplo de passagem de um parâmetro como parte do caminho. Neste exemplo, está indicando que, quando um caminho que atende ao padrão especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id) for solicitado, ele deverá ser manipulado pelo modelo home/products.template.html e usar a controladora &quot;contentphonegapgeometrixxoutdoors&quot;.

O modelo a ser carregado quando esta rota for solicitada é especificado pela propriedade templateUrl. Este modelo contém o HTML dos componentes AEM que foram incluídos na página e quaisquer diretivas AngularJS necessárias para conectar o lado do cliente do aplicativo. Para obter um exemplo de uma diretiva AngularJS em um componente do Geometrixx, verifique a linha 45 do template.jsp do carrossel de deslizamento (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controladores de página {#page-controllers}

Nas próprias palavras do Angular, &quot;um Controlador é uma função do construtor JavaScript usada para aumentar o Escopo do Angular&quot;. ([origem](https://docs.angularjs.org/guide/controller)) Cada página em um aplicativo AEM é conectada automaticamente a um controlador que pode ser aumentado por qualquer controlador que especifique um `frameworkType` de `angular`. Observe o componente de ng-text como um exemplo (/libs/mobileapps/components/angular/ng-text), incluindo o nó cq:template, que garante que cada vez que esse componente for adicionado a uma página, ele inclua essa propriedade importante.

Para um exemplo de controlador mais complexo, abra o script ng-template-page controller.jsp (em /apps/geometrixx-outdoors-app/components/angular/ng-template-page). De particular interesse é o código JavaScript gerado ao ser executado, que é renderizado da seguinte maneira:

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

No exemplo acima, o parâmetro do serviço `$routeParams` é coletado e, em seguida, massageado na estrutura de diretório em que os dados JSON são armazenados. Ao lidar com o SKU `id` dessa maneira, você pode fornecer um único modelo de produto que pode renderizar os dados do produto para potencialmente milhares de produtos distintos. Este é um modelo muito mais escalável que requer uma rota individual para cada item em um banco de dados de produtos (potencialmente) massivo.

Também há dois componentes em funcionamento aqui: ng-product aumenta o escopo com os dados que extrai da chamada `$http` acima. Também há uma ng-image nessa página que, por sua vez, também aumenta o escopo com o valor que ele recupera da resposta. Devido ao serviço `$http` do Angular, cada componente aguarda pacientemente até que a solicitação seja concluída e a promessa criada seja cumprida.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre os Aplicativos de Página Única, consulte [Desenvolvendo Aplicativos com a CLI do PhoneGap](/help/mobile/phonegap-apps-pg-cli.md).
