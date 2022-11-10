---
title: Introdução ao SPA no AEM - React
seo-title: Getting Started with SPAs in AEM - React
description: Este artigo apresenta um exemplo de aplicativo SPA, explica como ele é montado e permite que você entre em funcionamento com seu próprio SPA rapidamente usando a estrutura React.
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the React framework.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 3%

---

# Introdução ao SPA no AEM - React{#getting-started-with-spas-in-aem-react}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar com facilidade o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação de SPA oferece uma solução abrangente para oferecer suporte à SPA no AEM. Este artigo apresenta um aplicativo de SPA simplificado no React Framework, explica como ele é montado, permitindo que você entre em funcionamento com seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia - se no Quadro React. Para o documento correspondente para a estrutura do Angular, consulte [Introdução ao SPA no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de um SPA simples e o mínimo que você precisa saber para executar o seu.

Para obter mais detalhes sobre como SPA trabalhar no AEM, consulte os seguintes documentos:

* [Introdução e passo a passo do SPA](/help/sites-developing/spa-walkthrough.md)
* [Introdução à criação de SPA](/help/sites-developing/spa-overview.md)
* [Blueprint do SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para poder criar conteúdo em um SPA, o conteúdo deve ser armazenado no AEM e ser exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento abordará a estrutura de um SPA simplificado criado usando a estrutura React e ilustrará como funciona, para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do React, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O `package.json` O arquivo define os requisitos do pacote de SPA geral. As dependências mínimas de AEM para um SPA funcional estão listadas aqui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Como este exemplo se baseia no React framework, há duas dependências específicas do React que são obrigatórias no `package.json` arquivo:

```
react
 react-dom
```

O `aem-clientlib-generator` O é aproveitado para tornar a criação de bibliotecas de clientes automática como parte do processo de criação.

`"aem-clientlib-generator": "^1.4.1",`

Mais detalhes podem ser encontrados [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>A versão mínima do `aem-clientlib-generator` obrigatório é 1.4.1.

O `aem-clientlib-generator` é configurado no `clientlib.config.js` como mostrado a seguir.

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

Na verdade, criar as alavancas do aplicativo [Webpack](https://webpack.js.org/) para transpilação, além do gerador aem-clientlib para criação automática de biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "webpack && clientlib --verbose"`

Depois de criado, o pacote pode ser carregado em uma instância de AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto AEM deve aproveitar [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que suporta projetos SPA usando o React ou Angular e aproveita o SDK SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente o colocará em funcionamento um pacote de SPA que você pode fazer upload para sua instância de AEM.

A próxima seção deste documento abordará a estrutura de um SPA no AEM, os arquivos importantes que orientam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### index.js {#index-js}

O ponto de entrada no SPA é, obviamente, o `index.js` arquivo mostrado aqui simplificado para se concentrar no conteúdo importante.

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

A função principal de `index.js` é aproveitar o `ReactDOM.render` para determinar onde no DOM deve injetar o aplicativo.

Esse é um uso padrão dessa função, não exclusiva a este aplicativo de exemplo.

#### Instalação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente (por exemplo, JSX), o valor deve ser passado do modelo para as propriedades do componente.

### App.js {#app-js}

Ao renderizar o aplicativo, `index.js` chamadas `App.js`, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

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

Ao renderizar a página, `App.js` chamadas `Page.js` listado aqui em uma versão simplificada.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

Neste exemplo, a variável `AppPage` classe estende `Page`, que contém os métodos de conteúdo interno que podem ser usados.

O `Page` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` pode ser encontrado no documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Com a página renderizada, os componentes como `Image.js` como mostrado aqui, pode ser renderizado.

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

A ideia central de SPA no AEM é mapear componentes SPA para AEM componentes e atualizar o componente quando o conteúdo for modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md) para um resumo deste modelo de comunicação.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

O `MapTo` O método mapeia o componente de SPA para o componente de AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para que o editor gere espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades transmitidas dinamicamente {#dynamically-passed-properties}

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

O `MapTo` a função retorna um `Component` que é o resultado de uma composição que estende o `PageClass` com os nomes de classe e atributos que permitem a criação. Esse componente pode ser exportado para o posteriormente ser instanciado na marcação do aplicativo.

Quando exportado usando o `MapTo` ou `withModel` , a `Page` componente, está envolvido com um `ModelProvider` componente que fornece aos componentes padrão acesso à versão mais recente do modelo de página ou a um local preciso nesse modelo de página.

Para obter mais informações, consulte [SPA documento Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Por padrão, você recebe o modelo inteiro do componente ao usar o `withModel` .

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É necessário que os componentes em um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir em uma ordem crescente de complexidade.

* **Opção 1:** Centralize a lógica e transmita para os componentes necessários, por exemplo, usando o Contexto de Reação.
* **Opção 2:** Compartilhe estados dos componentes usando uma biblioteca de estado, como Redux.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente do contêiner.

## Próximas etapas {#next-steps}

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte [Introdução ao Editor de SPA de AEM - Tutorial de eventos WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=pt-BR).

Para obter mais informações sobre como se organizar para desenvolver SPA para AEM, consulte o artigo [Desenvolvimento de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obter mais detalhes sobre o modelo dinâmico para o mapeamento de componentes e como ele funciona no SPA em AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desejar implementar o SPA no AEM para uma estrutura diferente de React ou Angular ou simplesmente quiser aprofundar como o SDK SPA para AEM funciona, consulte o [SPA Blueprint](/help/sites-developing/spa-blueprint.md) artigo 10. o
