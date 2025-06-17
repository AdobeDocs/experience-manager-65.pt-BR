---
title: Implementação de um componente de reação para SPA
description: Este artigo apresenta um exemplo de como adaptar um componente React simples e existente para trabalhar com o Editor de SPA do Adobe Experience Manager (AEM).
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 9%

---


# Implementação de um componente de reação para SPA{#implementing-a-react-component-for-spa}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no Adobe Experience Manager (AEM) para um site criado com o uso de estruturas SPA.

O recurso de criação de SPA oferece uma solução abrangente para suporte a SPAs no AEM. Este artigo apresenta um exemplo de como adaptar um componente React simples e existente para funcionar com o Editor SPA do AEM.

{{ue-over-spa}}

## Introdução {#introduction}

Graças ao contrato simples e leve exigido pela AEM e estabelecido entre o SPA e o Editor SPA, pegar um aplicativo JavaScript existente e adaptá-lo para uso com um SPA no AEM é uma questão simples.

Este artigo ilustra o exemplo do componente de tempo no We.Retail Journal de amostra SPA.

Familiarize-se com a [estrutura de um aplicativo SPA para AEM](/help/sites-developing/spa-getting-started-react.md) antes de ler este artigo.

>[!CAUTION]
>Este documento usa o [aplicativo We.Retail Journal](https://github.com/adobe/aem-sample-we-retail-journal) somente para fins de demonstração. Não o use para nenhum trabalho de projeto.
>
>Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/overview), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## O componente de Tempo {#the-weather-component}

O componente de meteorologia é encontrado no canto superior esquerdo do aplicativo We.Retail Journal. Ele exibe o tempo atual de um local definido, extraindo dados meteorológicos dinamicamente.

### Usar o widget de clima {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Ao criar conteúdo do SPA no Editor de SPA, o componente meteorológico aparece como qualquer outro componente do AEM, completo com uma barra de ferramentas e editável.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

A cidade pode ser atualizada em uma caixa de diálogo, como qualquer outro componente do AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

A alteração é persistente e o componente se atualiza automaticamente com os novos dados meteorológicos.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implementação do componente de tempo {#weather-component-implementation}

O componente meteorológico é baseado em um componente do React disponível publicamente, chamado [React Open Weather](https://www.npmjs.com/package/react-open-weather). Ele foi adaptado para funcionar como um componente no aplicativo We.Retail Journal de SPA de amostra.

A seguir estão trechos da documentação do NPM sobre o uso do componente de tempo aberto do React.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Examinando o código do componente de clima personalizado ( `Weather.js`) no aplicativo We.Retail Journal:

* **Linha 16**: o widget do React Open Weather foi carregado conforme necessário.
* **Linha 46**: a função `MapTo` relaciona este componente React a um componente AEM correspondente para que ele possa ser editado no Editor SPA.

* **Linhas 22-29**: A `EditConfig` está definida, verificando se a cidade foi preenchida e definindo o valor se estiver vazia.

* **Linhas 31-44**: o componente Tempo estende a classe `Component` e fornece os dados necessários conforme definido na documentação de uso do NPM para o componente Tempo Aberto no React e renderiza o componente.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Embora um componente de back-end já deva existir, o desenvolvedor de front-end pode usar o componente de Tempo aberto do React no SPA do We.Retail Journal com pouca codificação.

## Próxima etapa {#next-step}

Para obter mais informações sobre como desenvolver SPAs para AEM, consulte o artigo [Desenvolvimento de SPAs para AEM](/help/sites-developing/spa-architecture.md).
