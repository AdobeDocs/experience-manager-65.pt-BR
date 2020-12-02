---
title: Aplicativos de página única
seo-title: Aplicativos de página única
description: Siga esta página para saber mais sobre aplicativos de página única, ou seja, você pode criar um aplicativo que tenha um desempenho idêntico a um aplicativo desktop ou móvel.
seo-description: Siga esta página para saber mais sobre aplicativos de página única, ou seja, você pode criar um aplicativo que tenha um desempenho idêntico a um aplicativo desktop ou móvel.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 0%

---


# Aplicativos de página única{#single-page-applications}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

[Aplicativos](https://en.wikipedia.org/wiki/Single-page_application)  de página única (SPA) alcançaram massa crítica, amplamente considerada o padrão mais eficaz para criar experiências ininterruptas com a tecnologia da Web. Seguindo um padrão SPA, você pode criar um aplicativo que tenha um desempenho idêntico a um desktop ou aplicativo móvel, mas alcance várias plataformas de dispositivos e fatores de forma, devido à sua fundação em padrões da Web abertos.

De modo geral, SPA parecem mais eficientes do que os sites baseados em páginas tradicionais porque eles normalmente carregam uma página HTML completa **apenas uma vez** (incluindo CSS, JS e conteúdo de fonte de suporte) e carregam somente o que é necessário sempre que uma mudança de estado ocorre no aplicativo. O que é necessário para essa mudança de estado pode variar com base no conjunto de tecnologias escolhidas, mas geralmente inclui um único fragmento HTML para substituir a &quot;visualização&quot; existente, e a execução de um bloco de código JS para conectar a nova visualização e executar qualquer renderização de modelo do lado do cliente que possa ser necessária. A velocidade dessa alteração de estado pode ser melhorada ainda mais, por meio do suporte a mecanismos de armazenamento de modelo em cache, ou até mesmo acesso offline ao conteúdo do modelo, se o Adobe PhoneGap for usado.

O AEM 6.1 é compatível com a criação e o gerenciamento de SPA por meio de AEM aplicativos. Este artigo fornecerá uma introdução aos conceitos por trás do SPA e como eles aproveitam [AngularJS](https://angularjs.org/) para trazer sua marca para a App Store e o Google Play.

## SPA em aplicativos AEM {#spa-in-aem-apps}

A estrutura de aplicativo de página única em AEM aplicativos permite o alto desempenho de um aplicativo AngularJS, ao mesmo tempo que permite que autores (ou outras pessoas não técnicas) criem e gerenciem o conteúdo do aplicativo por meio do ambiente editor otimizado para toque, arrastar e soltar, tradicionalmente reservado para o gerenciamento de sites. Já tem um site construído com AEM? Você descobrirá que reutilizar seu conteúdo, componentes, workflows, ativos e permissões é fácil com os aplicativos AEM.

## Módulo de aplicativo AngularJS {#angularjs-application-module}

Os aplicativos AEM lidam com grande parte da configuração AngularJS para você, incluindo a criação do módulo de nível superior do aplicativo. Por padrão, esse módulo é chamado de &#39;AEMAngularApp&#39; e o script responsável pela sua geração pode ser encontrado (e sobreposto) em /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp.

Parte da inicialização do aplicativo envolve especificar em quais módulos AngularJS o aplicativo depende. A lista de módulos usada pelo aplicativo é especificada por um script localizado em /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp, e pode ser sobreposta pelo componente de página do seu aplicativo para receber qualquer módulo AngularJS adicional que seu aplicativo exija. Por exemplo, compare o script acima com a implementação do Geometrixx (localizado em /apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp).

Para suportar a navegação entre os estados distintos no aplicativo, o script angular-app-module repete por todas as páginas descendentes da página do aplicativo de nível superior para gerar um conjunto de &quot;rotas&quot; e configura cada caminho no serviço $routeProvider da Angular. Para ver um exemplo de como isso ocorre na prática, consulte o script angular-app-module gerado pela amostra de aplicativo Geometrixx Outdoors: (o link requer uma instância local) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

Ao acessar o AEMAngularApp gerado, você encontrará uma série de rotas especificadas da seguinte maneira:

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

A amostra acima ilustra um exemplo de envio de um parâmetro como parte do caminho. Neste exemplo, estamos indicando que quando um caminho que atende ao padrão especificado (/content/phonegap/geometrixx-outdoors/en/home/products/:id) é solicitado, ele deve ser manipulado pelo modelo home/products.template.html e usar o controlador &#39;contentphonegapgeometrixoutorsenhomeproducts&#39;.

O modelo a ser carregado quando essa rota for solicitada é especificado pela propriedade templateUrl. Este modelo conterá o HTML de AEM componentes que foram incluídos na página, bem como quaisquer diretivas AngularJS necessárias para conectar o lado do cliente do aplicativo. Para ver um exemplo de uma diretiva AngularJS em um componente de Geometrixx, veja a linha 45 do template.jsp do carrossel deslizante (/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp).

## Controladores de página {#page-controllers}

Nas próprias palavras de Angular, &quot;um Controlador é uma função de construtor JavaScript usada para aumentar o Escopo Angular&quot;. ([source](https://docs.angularjs.org/guide/controller)) Cada página em um aplicativo AEM é automaticamente conectada a um controlador que pode ser aumentado por qualquer controlador que especifique um `frameworkType` de `angular`. Examine o componente ng-text como um exemplo (/libs/mobileapps/components/angle/ng-text), incluindo o nó cq:template, que garante que cada vez que esse componente for adicionado a uma página ela inclua essa propriedade importante.

Para obter um exemplo de controlador mais complexo, abra o script ng-template-page controller.jsp (localizado em /apps/geometrixx-outdoors-app/components/angle/ng-template-page). De particular interesse é o código javascript gerado quando executado, que renderiza da seguinte forma:

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

No exemplo acima, você observará que estamos pegando um parâmetro do serviço `$routeParams` e, em seguida, o inserindo na estrutura de diretório em que nossos dados JSON estão armazenados. Ao lidar com o sku `id` dessa maneira, podemos fornecer um único modelo de Produto que pode renderizar os dados do produto para milhares de produtos potencialmente distintos. Este é um modelo muito mais escalonável que requer uma rota individual para cada item em um (potencialmente) grande banco de dados de produtos.

Há também dois componentes em funcionamento aqui: ng-product aumenta o escopo com os dados extraídos da chamada `$http` acima. Também há uma ng-image nesta página que, por sua vez, também aumenta o escopo com o valor que recupera da resposta. Em virtude do serviço `$http` do Angular, cada componente aguardará pacientemente até que a solicitação seja concluída e a promessa criada seja cumprida.

## Próximas etapas {#the-next-steps}

Depois de saber mais sobre os aplicativos de página única, consulte [Desenvolvimento de aplicativos com o PhoneGap CLI](/help/mobile/phonegap-apps-pg-cli.md).
