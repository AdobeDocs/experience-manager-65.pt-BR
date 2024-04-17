---
title: SPA Introdução ao AEM - React
description: Este artigo apresenta uma amostra de aplicativo SPA, explica como ele é montado e permite que você comece a usar seu próprio SPA rapidamente usando a estrutura do React.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 552649e7-6054-4ae8-b570-5ba7230e6f19
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 4%

---

# SPA Introdução ao AEM - React{#getting-started-with-spas-in-aem-react}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação do SPA oferece uma solução abrangente para oferecer suporte ao SPA no AEM. Este artigo apresenta um aplicativo simplificado para SPA na estrutura do React, explica como ele é montado, permitindo que você comece a usar seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia-se no quadro do React. Para o documento correspondente para a estrutura do Angular, consulte [Introdução ao SPA no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização no lado do cliente baseada na estrutura SPA (por exemplo, React ou Angular).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de um SPA simples e o mínimo que você precisa saber para que o seu funcione.

Para obter mais detalhes sobre como o SPA funciona no AEM, consulte os seguintes documentos:

* [Introdução e passo a passo do SPA](/help/sites-developing/spa-walkthrough.md)
* [Introdução à criação do SPA](/help/sites-developing/spa-overview.md)
* [Blueprint do SPA](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo dentro de um SPA, o conteúdo deve ser armazenado no AEM e ser exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento abordará a estrutura de um SPA simplificado criado usando a estrutura do React e ilustrará como ele funciona para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do React, o SPA de amostra pode usar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

A variável `package.json` define os requisitos do pacote SPA geral. As dependências mínimas do AEM para um SPA em funcionamento estão listadas aqui.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Como este exemplo se baseia na estrutura do React, há duas dependências específicas do React que são obrigatórias na variável `package.json` arquivo:

```
react
 react-dom
```

A variável `aem-clientlib-generator` O é usado para tornar a criação de bibliotecas de clientes automática como parte do processo de criação.

`"aem-clientlib-generator": "^1.4.1",`

Mais detalhes podem ser encontrados [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>A versão mínima do `aem-clientlib-generator` necessário é o 1.4.1.

A variável `aem-clientlib-generator` está configurado no `clientlib.config.js` arquivo como segue.

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

### Compilação {#building}

Criar realmente os usos do aplicativo [Webpack](https://webpack.js.org/) para tradução, além do aem-clientlib-generator para criação automática da biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "webpack && clientlib --verbose"`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente deixará você com um pacote de SPA que funciona e que você pode carregar para sua instância do AEM.

A próxima seção deste documento abordará como um SPA no AEM é estruturado, os arquivos importantes que orientam o aplicativo e como eles funcionam juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo se baseiam no mesmo conceito.

### index.js {#index-js}

O ponto de entrada no SPA é o `index.js` O arquivo mostrado aqui foi simplificado para se concentrar no conteúdo importante.

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

A principal função do `index.js` é usar o `ReactDOM.render` para determinar onde inserir o aplicativo no DOM.

Este é um uso padrão dessa função, não exclusivo deste aplicativo de exemplo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o template do componente (por exemplo, JSX), o valor deve ser passado do modelo para as propriedades do componente.

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

`App.js` O serve principalmente para envolver os componentes raiz que compõem o aplicativo. O ponto de entrada de qualquer aplicativo é a página.

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

Neste exemplo, a variável `AppPage` class extends `Page`, que contém os métodos de conteúdo interno que podem ser usados.

A variável `Page` A assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` pode ser encontrado no documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Com a página renderizada, os componentes como `Image.js` conforme mostrado aqui pode ser renderizado.

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

A ideia central do AEM é a ideia de mapear componentes do SPA AEM para componentes do SPA e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md) para obter um resumo deste modelo de comunicação.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

A variável `MapTo` O método mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades passadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

## Exportar conteúdo editável {#exporting-editable-content}

É possível exportar um componente e mantê-lo editável.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

A variável `MapTo` função retorna um valor `Component` que é o resultado de uma composição que estende o `PageClass` com os nomes e atributos de classe que permitem a criação. Esse componente pode ser exportado para ser instanciado posteriormente na marcação do aplicativo.

Quando exportado usando o `MapTo` ou `withModel` funções, a variável `Page` componente, é envolvido com um `ModelProvider` componente que fornece aos componentes padrão acesso à versão mais recente do modelo de página ou a um local preciso nesse modelo de página.

Para obter mais informações, consulte a [Documento do blueprint do SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Por padrão, você recebe o modelo inteiro do componente ao usar o `withModel` função.

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É regularmente necessário que os componentes de um aplicativo de página única compartilhem informações. Há várias maneiras recomendadas de fazer isso, listadas a seguir em uma ordem crescente de complexidade.

* **Opção 1:** Centralize a lógica e a transmissão para os componentes necessários, por exemplo, usando o Contexto do React.
* **Opção 2:** Compartilhe estados do componente usando uma biblioteca de estado, como Redux.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente de contêiner.

## Próximas etapas {#next-steps}

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte o [Introdução ao editor SPA AEM - Tutorial de eventos do WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html?lang=pt-BR).

Para obter mais informações sobre como se organizar para desenvolver SPA para AEM, consulte o artigo [Desenvolvimento de AEM para SPA](/help/sites-developing/spa-architecture.md).

SPA Para mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar o SPA no AEM para uma estrutura diferente do React ou do Angular SPA AEM ou simplesmente quiser se aprofundar em como funciona o SDK do para o, consulte o [Blueprint SPA](/help/sites-developing/spa-blueprint.md) artigo.
