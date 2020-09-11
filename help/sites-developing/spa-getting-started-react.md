---
title: Introdução aos SPAs no AEM - Reagir
seo-title: Introdução aos SPAs no AEM - Reagir
description: Este artigo apresenta um aplicativo SPA de amostra, explica como ele é colocado junto e permite que você entre em operação com seu próprio SPA rapidamente usando a estrutura React.
seo-description: Este artigo apresenta um aplicativo SPA de amostra, explica como ele é colocado junto e permite que você entre em operação com seu próprio SPA rapidamente usando a estrutura React.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 1%

---


# Introdução aos SPAs no AEM - Reagir{#getting-started-with-spas-in-aem-react}

Os aplicativos de página única (SPAs) podem oferta experiências interessantes para os usuários do site. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferta uma solução abrangente para suportar SPAs dentro do AEM. Este artigo apresenta um aplicativo SPA simplificado na estrutura React, explica como ele é montado, permitindo que você se familiarize com seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia - se no quadro React. Para o documento correspondente da estrutura Angular, consulte [Introdução às ZPEs em AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>O Editor SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em estrutura SPA (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de um SPA simples e o mínimo que você precisa saber para executar o seu.

Para obter mais detalhes sobre como os SPAs funcionam em AEM, consulte os seguintes documentos:

* [Introdução ao SPA e Walkthrough](/help/sites-developing/spa-walkthrough.md)
* [Introdução à criação do SPA](/help/sites-developing/spa-overview.md)
* [Blueprint do SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo em um SPA, o conteúdo deve ser armazenado em AEM e exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento percorrerá a estrutura de um SPA simplificado criado usando a estrutura React e ilustrará como ele funciona para que você possa aplicar esse entendimento ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do React, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O `package.json` arquivo define os requisitos do pacote SPA geral. As dependências mínimas de AEM para um SPA em funcionamento estão listadas aqui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Como este exemplo é baseado na estrutura React, existem duas dependências React-specific que são obrigatórias no `package.json` arquivo:

```
react
 react-dom
```

O recurso `aem-clientlib-generator` é utilizado para tornar a criação de bibliotecas de clientes automática como parte do processo de criação.

`"aem-clientlib-generator": "^1.4.1",`

Mais detalhes sobre o assunto podem ser encontrados [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>A versão mínima do `aem-clientlib-generator` necessário é 1.4.1.

O `aem-clientlib-generator` é configurado no `clientlib.config.js` arquivo da seguinte maneira.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Criando {#building}

Na verdade, a criação do aplicativo aproveita o [Webpack](https://webpack.js.org/) para transpilação, além do gerador aem-clientlib para a criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "webpack && clientlib --verbose"`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SDK do SPA.

## Estrutura do aplicativo {#application-structure}

A inclusão das dependências e a criação do aplicativo conforme descrito anteriormente o deixarão com um pacote SPA em funcionamento que você pode carregar para a instância AEM.

A próxima seção deste documento o orientará sobre como um SPA em AEM é estruturado, os arquivos importantes que acionam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### index.js {#index-js}

O ponto de entrada no SPA é, claro, o `index.js` arquivo mostrado aqui simplificado para focar no conteúdo importante.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

A função principal do é `index.js` alavancar a `ReactDOM.render` função para determinar onde o DOM deve injetar o aplicativo.

Este é um uso padrão desta função, não exclusivo para este aplicativo de exemplo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente (por exemplo, JSX), o valor deve ser passado do modelo para as propriedades do componente.

### App.js {#app-js}

Ao renderizar o aplicativo, `index.js` as chamadas `App.js`, que são mostradas aqui em uma versão simplificada para focar no conteúdo importante.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` serve principalmente para envolver os componentes raiz que compõem o aplicativo. O ponto de entrada de qualquer aplicativo é a página.

### Page.js {#page-js}

Ao renderizar a página, `App.js` as chamadas `Page.js` listadas aqui em uma versão simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

Neste exemplo, a `AppPage` classe se estende `Page`, que contém os métodos de conteúdo interno que podem ser usados.

O `Page` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Para obter mais detalhes sobre o `Page` documento, consulte [SPA Blueprint (Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)do SPA do adaptador SPA).

### Image.js {#image-js}

Com a página renderizada, os componentes, como `Image.js` mostrado aqui, podem ser renderizados.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

A ideia central dos SPAs no AEM é mapear componentes do SPA para AEM componentes e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte Visão geral [do editor](/help/sites-developing/spa-overview.md) SPA do documento para obter um resumo desse modelo de comunicação.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

O `MapTo` método mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para ativar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades aprovadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

## Exportar conteúdo editável {#exporting-editable-content}

Você pode exportar um componente e mantê-lo editável.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

A `MapTo` função retorna um resultado `Component` que é o resultado de uma composição que estende o conteúdo fornecido `PageClass` com os nomes e atributos da classe que habilitam a criação. Esse componente pode ser exportado para ser instanciado posteriormente na marcação do aplicativo.

Quando exportado usando as funções `MapTo` ou `withModel` , o `Page` componente é encapsulado com um `ModelProvider` componente que fornece aos componentes padrão acesso à versão mais recente do modelo de página ou a um local preciso nesse modelo de página.

Para obter mais informações, consulte o documento [](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743)SPA Blueprint.

>[!NOTE]
>
>Por padrão, você recebe o modelo inteiro do componente ao usar a `withModel` função.

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É necessário que os componentes de um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir, para aumentar a ordem de complexidade.

* **Opção 1:** Centralize a lógica e transmita para os componentes necessários, por exemplo, usando Reagir contexto.
* **Opção 2:** Compartilhe estados de componentes usando uma biblioteca de estados como Redux.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de container.

## Próximas etapas {#next-steps}

Para obter um guia passo a passo para a criação de seu próprio SPA, consulte o [Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)Introdução ao Editor SPA AEM - Eventos WKND.

Para obter mais informações sobre como se organizar para desenvolver SPAs para AEM consulte o artigo [Desenvolvimento de SPAs para AEM](/help/sites-developing/spa-architecture.md).

Para obter mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona em SPAs no AEM, consulte o artigo Modelo [dinâmico para mapeamento de componentes para SPAs](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar SPAs em AEM para uma estrutura diferente de React ou Angular ou simplesmente desejar aprofundar-se sobre como o SDK do SPA para AEM funciona, consulte o artigo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
