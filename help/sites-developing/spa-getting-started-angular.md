---
title: Introdução ao SPA no AEM - Angular
seo-title: Introdução ao SPA no AEM - Angular
description: Este artigo apresenta uma amostra SPA aplicativo, explica como ele é montado e permite que você entre em operação com sua própria SPA rapidamente usando a estrutura Angular.
seo-description: Este artigo apresenta uma amostra SPA aplicativo, explica como ele é montado e permite que você entre em operação com sua própria SPA rapidamente usando a estrutura Angular.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 1%

---


# Introdução ao SPA no AEM - Angular{#getting-started-with-spas-in-aem-angular}

Aplicativos de página única (SPA) podem oferta experiências interessantes para usuários de sites. Os desenvolvedores querem ser capazes de criar sites usando estruturas SPA e os autores querem editar o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação de SPA oferta uma solução abrangente para suportar SPA dentro do AEM. Este artigo apresenta uma aplicação SPA simplificada na estrutura Angular, explica como ela é montada, permitindo que você se familiarize com sua própria SPA rapidamente.

>[!NOTE]
>
>Este artigo baseia-se na estrutura Angular. Para obter o documento correspondente para a estrutura React, consulte [Introdução ao SPA em AEM - React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Este artigo resume o funcionamento básico de uma SPA simples e o mínimo que você precisa saber para executar a sua.

Para obter mais detalhes sobre como SPA trabalhar em AEM, consulte os seguintes documentos:

* [Introdução SPA e Walkthrough](/help/sites-developing/spa-walkthrough.md)
* [Introdução à criação de SPA](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Para ser capaz de criar conteúdo dentro de um SPA, o conteúdo deve ser armazenado em AEM e exposto pelo modelo de conteúdo.
>
>Um SPA desenvolvido fora do AEM não será autorável se não respeitar o contrato do modelo de conteúdo.

Este documento irá percorrer a estrutura de um SPA simplificado e ilustrará como ele funciona para que você possa aplicar este entendimento ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência Angular esperada, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O arquivo `package.json` define os requisitos do pacote SPA geral. As dependências de AEM mínimas obrigatórias estão listadas aqui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

O `aem-clientlib-generator` é aproveitado para tornar a criação de bibliotecas de clientes automática como parte do processo de compilação.

`"aem-clientlib-generator": "^1.4.1",`

Para obter mais detalhes sobre ele, acesse [no GitHub aqui](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>A versão mínima de `aem-clientlib-generator` necessária é 1.4.1.

O `aem-clientlib-generator` está configurado no arquivo `clientlib.config.js` da seguinte forma.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Depois de criado, o pacote pode ser carregado para uma instância AEM.

### Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SPA SDK.

## Estrutura do aplicativo {#application-structure}

A inclusão das dependências e a criação do aplicativo conforme descrito anteriormente o deixarão com um pacote SPA que pode ser carregado para a instância AEM.

A próxima seção deste documento o orientará sobre como um SPA em AEM é estruturado, os arquivos importantes que acionam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### app.module.ts {#app-module-ts}

O ponto de entrada no SPA é o arquivo `app.module.ts` mostrado aqui simplificado para focar no conteúdo importante.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

O arquivo `app.module.ts` é o ponto de partida do aplicativo e contém a configuração inicial do projeto e usa `AppComponent` para inicializar o aplicativo.

#### Instanciação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente, o valor deve ser passado do modelo para as propriedades do componente. Os valores do modelo são passados como atributos para ficarem disponíveis posteriormente como propriedades do componente.

### app.component.ts {#app-component-ts}

Depois de `app.module.ts` inicializar `AppComponent`, é possível inicializar o aplicativo, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

Ao processar a página, `app.component.ts` chama `main-content.component.ts` listadas aqui em uma versão simplificada.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

O `MainComponent` ingere a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` podem ser encontrados no documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

O `Page` é composto de componentes. Com o JSON assimilado, o `Page` pode processar esses componentes, como `image.component.ts`, conforme mostrado aqui.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

A ideia central do SPA em AEM é mapear componentes SPA para AEM componentes e atualizar o componente quando o conteúdo é modificado (e vice-versa). Consulte o documento [SPA Visão geral do editor](/help/sites-developing/spa-overview.md) para obter um resumo deste modelo de comunicação.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

O método `MapTo` mapeia o componente SPA para o componente AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para ativar os recursos de criação de um componente, fornecendo os metadados necessários para o editor gerar espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades aprovadas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

### image.component.html {#image-component-html}

Finalmente, a imagem pode ser renderizada em `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Compartilhando informações entre SPA componentes {#sharing-information-between-spa-components}

É necessário que os componentes de um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir, para aumentar a ordem de complexidade.

* **Opção 1:** Centralize a lógica e a transmissão para os componentes necessários, por exemplo, usando uma classe util como uma solução pura orientada a objetos.
* **Opção 2:** Compartilhe estados de componentes usando uma biblioteca de estado como NgRx.
* **Opção 3:** aproveite a hierarquia de objetos personalizando e estendendo o componente de container.

## Próximas etapas {#next-steps}

Para obter um guia passo a passo para a criação de seu próprio SPA, consulte [Introdução ao Editor de SPA AEM - Tutorial de Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obter mais informações sobre como se organizar para desenvolver SPA para AEM, consulte o artigo [Desenvolvimento de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obter mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA em AEM, consulte o artigo [Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar SPA no AEM para uma estrutura diferente de React ou Angular ou simplesmente quiser aprofundar-se em como o SDK SPA para AEM funciona, consulte o artigo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
