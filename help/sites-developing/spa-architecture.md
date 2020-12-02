---
title: Desenvolver SPA para AEM
seo-title: Desenvolver SPA para AEM
description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM, além de fornecer uma visão geral da arquitetura do AEM em relação à SPA para ter em mente ao implantar um SPA desenvolvido no AEM.
seo-description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM, além de fornecer uma visão geral da arquitetura do AEM em relação à SPA para ter em mente ao implantar um SPA desenvolvido no AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 0%

---


# Desenvolver SPA para AEM{#developing-spas-for-aem}

Aplicativos de página única (SPA) podem oferta experiências interessantes para usuários de sites. Os desenvolvedores querem ser capazes de criar sites usando estruturas SPA e os autores querem editar o conteúdo no AEM para um site criado usando essas estruturas.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM e fornece uma visão geral da arquitetura do AEM em relação à implantação do SPA no AEM.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Princípios de desenvolvimento SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única em AEM pressupõe que o desenvolvedor front-end observe as práticas recomendadas padrão ao criar um SPA. Se você seguir essas práticas recomendadas gerais e alguns princípios específicos para AEM como desenvolvedor front-end, seu SPA funcionará com [AEM e seus recursos de criação de conteúdo](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidade](/help/sites-developing/spa-architecture.md#portability)  -** Como em qualquer componente, os componentes devem ser construídos para serem o mais portáteis possível. O SPA deve ser construído com componentes portáveis e reutilizáveis.
* **[Estrutura](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  do site do AEM - o desenvolvedor do front-end cria componentes e é proprietário de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  dinâmica: todas as renderizações devem ser dinâmicas.
* **[Roteamento](#dynamic-routing)  dinâmico -** O SPA é responsável pelo roteamento e AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Se você tiver esses princípios em mente ao desenvolver seu SPA, ele será o mais flexível e a prova futura possível, além de permitir a funcionalidade de criação AEM suportada.

Se você não precisar suportar os recursos de criação AEM, talvez precise considerar um [SPA modelo de design](/help/sites-developing/spa-architecture.md#spa-design-models) diferente.

### Portabilidade {#portability}

Como ao desenvolver qualquer componente, seus componentes devem ser projetados de modo a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou a reusabilidade dos componentes devem ser evitados para garantir a compatibilidade, flexibilidade e manutenção futura.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### Estrutura do site das unidades AEM {#aem-drives-site-structure}

O desenvolvedor front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor front-end tem controle total da estrutura interna dos componentes. [No entanto, AEM sempre possui a estrutura do site.](/help/sites-developing/spa-overview.md)

Isso significa que o desenvolvedor front-end pode adicionar conteúdo ao cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não está no controle total de como os componentes são aninhados, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão na qual AEM busca e renderiza todos os filhos da estrutura de conteúdo. [](/help/sites-developing/spa-architecture.md#portability)

Qualquer renderização explícita que aponte para um conteúdo específico é considerada uma renderização estática e, embora seja suportada, não será compatível com AEM recursos de criação de conteúdo. Isso também vai contra o princípio de [portability](/help/sites-developing/spa-architecture.md#portability).

### Roteamento dinâmico {#dynamic-routing}

Assim como na renderização, todos os roteamentos também devem ser dinâmicos. No AEM, [o SPA deve ser o proprietário do roteamento](/help/sites-developing/spa-routing.md) e AEM o escuta e busca conteúdo com base nele.

Qualquer roteamento estático funciona de acordo com o princípio [de portabilidade](/help/sites-developing/spa-architecture.md#portability) e limita o autor ao não ser compatível com os recursos de criação de conteúdo da AEM. Por exemplo, com roteamento estático, se o autor do conteúdo quiser alterar uma rota ou uma página, ele ou ela precisará solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM{#aem-project-archetype}

Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SPA SDK.

## Modelos de design SPA {#spa-design-models}

Se os princípios [de desenvolvimento de SPA em AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) forem seguidos, seu SPA funcionará com todos os recursos de criação AEM conteúdo suportados. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

No entanto, podem existir casos em que tal não seja inteiramente necessário. A tabela a seguir apresenta uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>AEM é usado como um CMS sem cabeçalho sem usar <a href="/help/sites-developing/spa-reference-materials.md">SPA estrutura SDK do Editor.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem aproveitar AEM experiência de criação de conteúdo.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor do conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, permitindo apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo são restritos a um conjunto limitado de experiências de criação de conteúdo AEM.</p> <p>O código pode não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto aproveita totalmente o SDK do Editor de SPA e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada à AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor do conteúdo pode editar o aplicativo usando AEM experiência de criação de conteúdo.<br /> </p> <p>O SPA é compatível com o editor de modelo.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam suportados em AEM, somente ao implementar o terceiro (e, portanto, seguir os [SPA princípios de desenvolvimento recomendados em AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) os autores de conteúdo poderão interagir e editar o conteúdo do SPA na AEM, conforme estiverem acostumados.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migração de SPA existentes para AEM {#migrating-existing-spas-to-aem}

Geralmente, se seu SPA seguir os [SPA Princípios de desenvolvimento para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), então seu SPA funcionará em AEM e poderá ser editado usando o Editor de SPA de AEM.

Siga estas etapas para preparar seu SPA existente para trabalhar com AEM.

1. **Torne seus componentes JS modulares.**

   Torne-os capazes de serem renderizados em qualquer ordem, posição e tamanho.
1. **Use os container fornecidos pelo SDK para colocar seus componentes na tela.**

   AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente AEM para cada componente JS.**

   Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores front-end {#instructions-for-front-end-developers}

A principal tarefa para que um desenvolvedor de front-end crie um SPA para AEM é concordar com os componentes e seus modelos JSON.

A seguir está um resumo das etapas que um desenvolvedor front-end precisa seguir ao desenvolver um SPA para AEM.

1. **Concordar em componentes e em seus modelos JSON**

   Desenvolvedores front-end e desenvolvedores de AEM back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individual entre SPA componentes e os componentes back-end.

   AEM componentes ainda são necessários principalmente para fornecer caixas de diálogo de edição e exportar o modelo do componente.

1. **Em Reagir componentes, acesse o modelo via`this.props.cqModel`**

   Depois que os componentes forem aceitos e o modelo JSON estiver implementado, o desenvolvedor front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON via `this.props.cqModel`.

1. **Implementar o  `render()` método do componente**

   O desenvolvedor de front-end implementa o método `render()` conforme ele/ela julgar adequado e pode usar os campos da propriedade `cqModel`. Isso gera os fragmentos DOM e HTML que serão inseridos na página. Essa é a maneira padrão de criar um aplicativo no React.

1. **Mapeie o componente para o tipo de recurso AEM via`MapTo()`**

   O mapeamento armazena classes de componentes e é usado internamente pelo componente `Container` fornecido para recuperar e instanciar dinamicamente componentes com base no tipo de recurso fornecido.

   Isso serve como a &quot;colagem&quot; entre front-end e back-end para que o editor saiba a quais componentes os componentes reagem correspondem.

   Os `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Defina o parâmetro do componente  `EditConfig` como`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado desde que ainda não seja renderizado ou não tenha conteúdo para renderizar.

1. **Estender a  `Container` classe fornecida para páginas e container**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação aos componentes internos funcione como esperado.

1. **Implemente uma solução de roteamento que use a  `History` API HTML5.**

   Quando `ModelRouter` estiver ativado, chamar as funções `pushState` e `replaceState` acionará uma solicitação para `PageModelManager` buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não suporta o uso de URLs personalizados ou aliases.

   O `ModelRouter` pode ser desativado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como seus componentes React e Angular não precisam de nada que seja Adobe ou AEM específico.

* Tudo o que está dentro do componente JavaScript é AEM-agnóstico.
* O que, no entanto, é específico para AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

O auxiliar `MapTo` é a &quot;cola&quot; que permite que os componentes de back-end e de front-end sejam combinados:

* Ele informa ao container JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo será exibida ao autor ao editar o componente.

Para obter mais informações sobre como usar `MapTo` e criar SPA para AEM em geral, consulte o guia Introdução para sua estrutura selecionada.

* [Introdução ao SPA no AEM - Reagir](/help/sites-developing/spa-getting-started-react.md)
* [Introdução ao SPA no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitetura AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral de AEM incluindo ambientes de desenvolvimento, criação e publicação não é alterada ao usar SPA. No entanto, é útil entender como o desenvolvimento SPA se encaixa nessa arquitetura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Criar Ambiente**

   É aqui que a origem do aplicativo SPA e a fonte do componente são desconectadas.

   * O gerador clientlib do NPM cria uma biblioteca de clientes a partir do projeto SPA.
   * Essa biblioteca será tirada pelo Maven e implantada pelo plug-in Maven Build juntamente com o componente para o autor do AEM.

* **AEM Author**

   O conteúdo é criado no autor AEM, incluindo a criação de SPA.

   Quando um SPA é editado usando o Editor SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O Javascript do aplicativo SPA é carregado.
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo os atributos `cq-data`.
   1. Esses atributos `cq-data` permitem que o editor carregue informações adicionais da página para que ele saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

   É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos SPA aplicativos, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher / CDN**

   O dispatcher serve como a camada de cache de AEM para visitantes no site.

   * As solicitações são processadas de forma semelhante à forma como estão no autor de AEM, no entanto, não há solicitação de informações da página, pois isso só é necessário para o editor.
   * Javascript, CSS, JSON e HTML são armazenados em cache, otimizando a página para delivery rápido.

>[!NOTE]
>
>Dentro AEM não há necessidade de executar os mecanismos de criação do Javascript ou executar o próprio Javascript. AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

Para obter uma visão geral de como um SPA simples no AEM está estruturado e como ele funciona, consulte o guia de introdução para [React](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obter um guia passo a passo para a criação de seu próprio SPA, consulte [Introdução ao Editor de SPA AEM - Tutorial de Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obter mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do SPA em AEM, consulte o artigo [Dynamic Model to Component Mapping for SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar SPA no AEM para uma estrutura diferente de React ou Angular ou simplesmente quiser aprofundar-se em como o SDK SPA para AEM funciona, consulte o artigo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
