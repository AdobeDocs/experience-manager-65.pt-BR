---
title: Introdução ao SPA no AEM - Angular
seo-title: Getting Started with SPAs in AEM - Angular
description: Este artigo apresenta um exemplo de aplicativo SPA, explica como ele é montado e permite que você entre em funcionamento com seu próprio SPA rapidamente usando a estrutura do Angular.
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the Angular framework.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 6%

---

# Introdução ao SPA no AEM - Angular{#getting-started-with-spas-in-aem-angular}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar com facilidade o conteúdo no AEM para um site criado usando estruturas SPA.

O recurso de criação de SPA oferece uma solução abrangente para oferecer suporte à SPA no AEM. Este artigo apresenta um aplicativo de SPA simplificado na estrutura do Angular, explica como ele é montado, permitindo que você entre em funcionamento com seu próprio SPA rapidamente.

>[!NOTE]
>
>Este artigo é baseado na estrutura do Angular. Para o documento correspondente para o Quadro React, consulte [Introdução ao SPA no AEM - React](/help/sites-developing/spa-getting-started-react.md).

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

Este documento abordará a estrutura de um SPA simplificado e ilustrará como ele funciona, para que você possa aplicar essa compreensão ao seu próprio SPA.

## Dependências, configuração e criação {#dependencies-configuration-and-building}

Além da dependência esperada do Angular, o SPA de amostra pode aproveitar bibliotecas adicionais para tornar a criação do SPA mais eficiente.

### Dependências {#dependencies}

O `package.json` O arquivo define os requisitos do pacote de SPA geral. As dependências mínimas de AEM necessárias estão listadas aqui.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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

Na verdade, criar as alavancas do aplicativo [Webpack](https://webpack.js.org/) para transpilação, além do gerador aem-clientlib para criação automática de biblioteca do cliente. Portanto, o comando build será semelhante a:

`"build": "ng build --build-optimizer=false && clientlib",`

Depois de criado, o pacote pode ser carregado em uma instância de AEM.

### Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou Angular e utiliza o SDK do SPA.

## Estrutura do aplicativo {#application-structure}

Incluir as dependências e criar seu aplicativo conforme descrito anteriormente o colocará em funcionamento um pacote de SPA que você pode fazer upload para sua instância de AEM.

A próxima seção deste documento abordará a estrutura de um SPA no AEM, os arquivos importantes que orientam o aplicativo e como eles trabalham juntos.

Um componente de imagem simplificado é usado como exemplo, mas todos os componentes do aplicativo são baseados no mesmo conceito.

### app.module.ts {#app-module-ts}

O ponto de entrada no SPA é o `app.module.ts` arquivo mostrado aqui simplificado para se concentrar no conteúdo importante.

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

O `app.module.ts` O arquivo é o ponto inicial do aplicativo e contém a configuração inicial do projeto e os `AppComponent` para inicializar o aplicativo.

#### Instalação estática {#static-instantiation}

Quando o componente é instanciado estaticamente usando o modelo de componente, o valor deve ser passado do modelo para as propriedades do componente. Os valores do modelo são passados como atributos para disponibilização posterior como propriedades do componente.

### app.component.ts {#app-component-ts}

Uma vez `app.module.ts` bootstraps `AppComponent`, ele pode inicializar o aplicativo, que é mostrado aqui em uma versão simplificada para se concentrar no conteúdo importante.

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

Ao processar a página, `app.component.ts` chamadas `main-content.component.ts` listado aqui em uma versão simplificada.

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

O `MainComponent` assimila a representação JSON do modelo de página e processa o conteúdo para envolver/decorar cada elemento da página. Mais detalhes sobre o `Page` pode ser encontrado no documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

O `Page` é composto de componentes. Com o JSON assimilado, a variável `Page` pode processar esses componentes, como `image.component.ts` como mostrado aqui.

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

A ideia central de SPA no AEM é mapear componentes SPA para AEM componentes e atualizar o componente quando o conteúdo for modificado (e vice-versa). Consulte o documento [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md) para um resumo deste modelo de comunicação.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

O `MapTo` O método mapeia o componente de SPA para o componente de AEM. Ele suporta o uso de uma única string ou de uma matriz de strings.

`ImageEditConfig` é um objeto de configuração que contribui para habilitar os recursos de criação de um componente, fornecendo os metadados necessários para que o editor gere espaços reservados

Se não houver conteúdo, os rótulos serão fornecidos como espaços reservados para representar o conteúdo vazio.

#### Propriedades transmitidas dinamicamente {#dynamically-passed-properties}

Os dados provenientes do modelo são transmitidos dinamicamente como propriedades do componente.

### image.component.html {#image-component-html}

Finalmente, a imagem pode ser renderizada em `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Compartilhamento de informações entre componentes do SPA {#sharing-information-between-spa-components}

É necessário que os componentes em um aplicativo de página única compartilhem informações regularmente. Há várias maneiras recomendadas de fazer isso, listadas a seguir em uma ordem crescente de complexidade.

* **Opção 1:** Centralize a lógica e a transmissão para os componentes necessários, por exemplo, usando uma classe util como uma solução pura orientada a objetos.
* **Opção 2:** Compartilhe estados do componente usando uma biblioteca de estado, como NgRx.
* **Opção 3:** Aproveite a hierarquia de objetos personalizando e estendendo o componente do contêiner.

## Próximas etapas {#next-steps}

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte [Introdução ao Editor de SPA de AEM - Tutorial de eventos WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=pt-BR).

Para obter mais informações sobre como se organizar para desenvolver SPA para AEM, consulte o artigo [Desenvolvimento de SPA para AEM](/help/sites-developing/spa-architecture.md).

Para obter mais detalhes sobre o modelo dinâmico para o mapeamento de componentes e como ele funciona no SPA em AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desejar implementar o SPA no AEM para uma estrutura diferente de React ou Angular ou simplesmente quiser aprofundar como o SDK SPA para AEM funciona, consulte o [SPA Blueprint](/help/sites-developing/spa-blueprint.md) artigo 10. o
