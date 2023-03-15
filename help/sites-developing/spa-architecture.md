---
title: Desenvolvimento de SPAs para o AEM
seo-title: Developing SPAs for AEM
description: Este artigo apresenta questões importantes a serem consideradas ao engajar um desenvolvedor de front-end para desenvolver uma SPA para AEM, além de fornecer uma visão geral da arquitetura de AEM em relação à SPA para manter em mente ao implantar uma SPA desenvolvida em AEM.
seo-description: This article presents important questions to consider when engaging a front-end developer to develop a SPA for AEM as well as gives an overview of the architecture of AEM with respect to SPAs to keep in mind when deploying a developed SPA on AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 8%

---

# Desenvolvimento de SPAs para o AEM{#developing-spas-for-aem}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas de SPA, e os autores desejam editar o conteúdo de um site criado usando essas estruturas diretamente no AEM.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver uma SPA para AEM e fornece uma visão geral da arquitetura de AEM em relação à implantação de SPA no AEM.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Princípios de desenvolvimento SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Se, como desenvolvedor front-end, você seguir essas práticas recomendadas gerais, bem como alguns princípios específicos de AEM, seu SPA funcionará com [AEM e seus recursos de criação de conteúdo](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidade](/help/sites-developing/spa-architecture.md#portability) -** Assim como em qualquer componente, os componentes devem ser construídos para serem tão portáteis quanto possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **[AEM controla a estrutura do site](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - O desenvolvedor de front-end cria componentes e tem a propriedade de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização dinâmica](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - Todas as renderizações devem ser dinâmicas.
* **[Roteamento dinâmico](#dynamic-routing) -** O SPA é responsável pelo roteamento e AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Caso tenha esses princípios em mente ao desenvolver seu SPA, ele será o mais flexível e uma prova futura possível, além de ativar todas as funcionalidades de criação AEM compatíveis.

Se você não precisar oferecer suporte aos recursos de criação de AEM, talvez seja necessário considerar um [Modelo de design SPA](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilidade {#portability}

Assim como ao desenvolver qualquer componente, seus componentes devem ser projetados de forma a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou a reutilização dos componentes devem ser evitados para garantir a compatibilidade, flexibilidade e sustentabilidade a partir de agora.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### AEM unidades Estrutura do Site {#aem-drives-site-structure}

O desenvolvedor front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor front-end tem controle total da estrutura interna dos componentes. [No entanto, AEM sempre possui a estrutura do site.](/help/sites-developing/spa-overview.md)

Isso significa que o desenvolvedor de front-end pode adicionar conteúdo de cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não tem controle total sobre como os componentes são aninhados, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão em que o AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada renderização estática e, embora seja suportada, não será compatível com AEM recursos de criação de conteúdo. Isto também contraria o princípio da [portabilidade](/help/sites-developing/spa-architecture.md#portability).

### Roteamento dinâmico {#dynamic-routing}

Assim como com a renderização, todo o roteamento também deve ser dinâmico. Em AEM, [o SPA deve sempre ser o proprietário do roteamento](/help/sites-developing/spa-routing.md) e AEM escuta e busca conteúdo com base nela.

Qualquer roteamento estático funciona em relação à variável [princípio da portabilidade](/help/sites-developing/spa-architecture.md#portability) e limita o autor ao não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com roteamento estático, se o autor de conteúdo quiser alterar uma rota ou alterar uma página, ele precisará solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou Angular e utiliza o SDK do SPA.

## Modelos de design de SPA {#spa-design-models}

Se a variável [princípios do desenvolvimento da SPA em AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) forem seguidas, sua SPA funcionará com todos os recursos de criação de conteúdo AEM compatíveis.

No entanto, pode haver casos em que tal não seja totalmente necessário. A tabela a seguir apresenta uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>AEM é usado como um CMS sem periféricos sem usar o <a href="/help/sites-developing/spa-reference-materials.md">SPA estrutura do SDK do Editor.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem aproveitar AEM experiência de criação de conteúdo.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor de front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor de conteúdo.</td>
   <td>O desenvolvedor mantém o controle sobre o aplicativo, permitindo apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo são restritos a um conjunto limitado de AEM experiência de criação de conteúdo.</p> <p>O código pode não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto aproveita totalmente o SDK do Editor de SPA e os componentes de primeiro plano são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada à AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor de conteúdo pode editar o aplicativo usando AEM experiência de criação de conteúdo.<br /> </p> <p>O SPA é compatível com o editor de modelo.</p> </td>
   <td><p>O desenvolvedor não está no controle da estrutura do aplicativo e da parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando o AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam compatíveis com o AEM, apenas com a implementação do terceiro (e, portanto, seguindo o [SPA princípios de desenvolvimento em AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) os autores de conteúdo poderão interagir e editar o conteúdo da SPA no AEM como estão acostumados.

## Migrando SPA existentes para AEM {#migrating-existing-spas-to-aem}

Geralmente, se o SPA seguir a variável [Princípios de desenvolvimento SPA para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), seu SPA funcionará no AEM e poderá ser editado usando o Editor de SPA AEM.

Siga estas etapas para preparar seu SPA existente para trabalhar com o AEM.

1. **Torne seus componentes JS modulares.**

   Torne-os capazes de ser renderizados em qualquer ordem, posição e tamanho.
1. **Use os contêineres fornecidos pelo SDK para colocar seus componentes na tela.**

   AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente de AEM para cada componente JS.**

   Os componentes de AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores front-end {#instructions-for-front-end-developers}

A principal tarefa para habilitar um desenvolvedor de front-end para criar um SPA para AEM é concordar com os componentes e seus modelos JSON.

Veja a seguir um esboço das etapas que um desenvolvedor de front-end precisa seguir ao desenvolver um SPA para AEM.

1. **Concordar em componentes e em seu modelo JSON**

   Os desenvolvedores front-end e os desenvolvedores de AEM back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individual entre SPA componentes e os componentes back-end.

   AEM componentes ainda são necessários, principalmente para fornecer caixas de diálogo de edição e exportar o modelo de componentes.

1. **Nos componentes React , acesse o modelo por meio de`this.props.cqModel`**

   Depois que os componentes forem aceitos e o modelo JSON estiver em vigor, o desenvolvedor front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON por meio de `this.props.cqModel`.

1. **Implementar `render()` método**

   O desenvolvedor de front-end implementa o `render()` como entender e usar os campos do `cqModel` propriedade. Isso gera os fragmentos DOM e HTML que serão inseridos na página. Esta é a maneira padrão de criar um aplicativo no React.

1. **Mapeie o componente para o tipo de recurso AEM por meio de`MapTo()`**

   O mapeamento armazena classes de componentes e é usado internamente pelo `Container` componente para recuperar e instanciar dinamicamente componentes com base no tipo de recurso especificado.

   Isso serve como a &quot;cola&quot; entre front-end e back-end para que o editor saiba a quais componentes os componentes de reação correspondem.

   O `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Defina o `EditConfig` como parâmetro para`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado, desde que o ainda não seja renderizado ou não tenha conteúdo para renderização.

1. **Estender o `Container` classe para páginas e contêineres**

   Os sistemas de páginas e parágrafo devem estender essa classe para que a delegação para componentes internos funcione conforme esperado.

1. **Implemente uma solução de roteamento que use o HTML5 `History` API.**

   Quando a variável `ModelRouter` está ativado, chamando a função `pushState` e `replaceState` As funções do acionarão uma solicitação para `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontem para o caminho de recurso real dos pontos de entrada do Modelo do Sling. Não é compatível com o uso de URLs personalizados ou aliases.

   O `ModelRouter` pode ser desativado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como seus componentes React e Angular não precisam de nada que seja específico de Adobe ou AEM.

* Tudo o que está dentro do componente JavaScript é independente de AEM.
* No entanto, o que é específico para AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo .

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

O `MapTo` O auxiliar é a &quot;cola&quot; que permite que os componentes de back-end e de front-end sejam combinados:

* Informa ao contêiner JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo HTML data ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo exibir ao autor ao editar o componente.

Para obter mais informações sobre como usar `MapTo` e criando SPA para AEM em geral, consulte o guia de Introdução para sua estrutura escolhida.

* [Introdução ao SPA no AEM - React](/help/sites-developing/spa-getting-started-react.md)
* [Introdução ao SPA no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitetura AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral de AEM incluindo ambientes de desenvolvimento, criação e publicação não é alterada ao usar SPA. No entanto, é útil entender como o desenvolvimento SPA se encaixa nessa arquitetura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Ambiente de compilação**

   É aqui que a origem do aplicativo SPA e a origem do componente são verificadas.

   * O gerador clientlib do NPM cria uma biblioteca do cliente do projeto do SPA.
   * Essa biblioteca será obtida pelo Maven e implantada pelo plug-in Maven Build, juntamente com o componente para o autor do AEM.

* **Autor do AEM**

   O conteúdo é criado no autor do AEM, incluindo a criação de SPA.

   Quando um SPA é editado usando o Editor de SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O Javascript do aplicativo SPA é carregado.
   1. Quando o aplicativo de SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo o `cq-data` atributos.
   1. Essa `cq-data` os atributos do permitem que o editor carregue informações adicionais da página para que saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

   É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos SPA aplicativo, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher / CDN**

   O dispatcher serve como a camada de cache de AEM para os visitantes do site.

   * As solicitações são processadas de forma semelhante à forma como estão no Autor do AEM, no entanto, não há solicitação das informações da página, pois isso só é necessário para o editor.
   * Javascript, CSS, JSON e HTML são armazenados em cache, otimizando a página para entrega rápida.

>[!NOTE]
>
>No AEM, não há necessidade de executar mecanismos de criação do Javascript ou executar o próprio Javascript. AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

Para obter uma visão geral de como um SPA simples no AEM está estruturado e como funciona, consulte o guia de introdução para ambos [Reagir](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte [Introdução ao Editor de SPA de AEM - Tutorial de eventos WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=pt-BR).

Para obter mais detalhes sobre o modelo dinâmico para o mapeamento de componentes e como ele funciona no SPA em AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desejar implementar o SPA no AEM para uma estrutura diferente de React ou Angular ou simplesmente quiser aprofundar como o SDK SPA para AEM funciona, consulte o [SPA Blueprint](/help/sites-developing/spa-blueprint.md) artigo 10. o
