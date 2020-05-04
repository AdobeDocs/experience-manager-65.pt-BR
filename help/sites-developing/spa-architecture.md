---
title: Desenvolver SPAs para o AEM
seo-title: Desenvolver SPAs para o AEM
description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor front-end para desenvolver um SPA para o AEM, além de fornecer uma visão geral da arquitetura do AEM em relação aos SPAs para ter em mente ao implantar um SPA desenvolvido no AEM.
seo-description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor front-end para desenvolver um SPA para o AEM, além de fornecer uma visão geral da arquitetura do AEM em relação aos SPAs para ter em mente ao implantar um SPA desenvolvido no AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# Desenvolver SPAs para o AEM{#developing-spas-for-aem}

Os aplicativos de página única (SPAs) podem oferta experiências interessantes para os usuários do site. Os desenvolvedores desejam criar sites usando estruturas SPA e os autores desejam editar o conteúdo no AEM sem problemas para um site criado usando essas estruturas.

Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor front-end para desenvolver um SPA para o AEM e fornece uma visão geral da arquitetura do AEM em relação à implantação de SPAs no AEM.

>[!NOTE]
>
>O Editor SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em estrutura SPA (por exemplo, Reagir ou Angular).

## Princípios de desenvolvimento do SPA para o AEM {#spa-development-principles-for-aem}

Desenvolver aplicativos de página única no AEM pressupõe que o desenvolvedor front-end observe as práticas recomendadas padrão ao criar um SPA. Se você seguir essas práticas recomendadas gerais e alguns princípios específicos do AEM como desenvolvedor de front-end, seu SPA estará funcionando com o [AEM e seus recursos](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)de criação de conteúdo.

* **[Portabilidade](/help/sites-developing/spa-architecture.md#portability)**- Assim como com qualquer componente, os componentes devem ser criados para serem o mais portáteis possível. O SPA deve ser construído com componentes portáveis e reutilizáveis.
* **[Estrutura](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**do site de drives do AEM - o desenvolvedor front-end cria componentes e é proprietário de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização](/help/sites-developing/spa-architecture.md#dynamic-rendering)**dinâmica: todas as renderizações devem ser dinâmicas.
* **[Roteamento](#dynamic-routing)dinâmico -**o SPA é responsável pelo roteamento e o AEM o escuta e faz buscas com base nele. Qualquer roteamento também deve ser dinâmico.

Se você tiver esses princípios em mente ao desenvolver seu SPA, ele será o mais flexível e a prova futura possível, além de ativar todas as funcionalidades de criação do AEM suportadas.

Se você não precisar suportar os recursos de criação do AEM, pode ser necessário considerar um modelo [de design](/help/sites-developing/spa-architecture.md#spa-design-models)SPA diferente.

### Portabilidade {#portability}

Como ao desenvolver qualquer componente, seus componentes devem ser projetados de modo a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou a reusabilidade dos componentes devem ser evitados para garantir a compatibilidade, flexibilidade e manutenção futura.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### Estrutura do site das unidades AEM {#aem-drives-site-structure}

O desenvolvedor front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor front-end tem controle total da estrutura interna dos componentes. [No entanto, o AEM sempre possui a estrutura do site.](/help/sites-developing/spa-overview.md)

Isso significa que o desenvolvedor front-end pode adicionar conteúdo ao cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não está no controle total de como os componentes são aninhados, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão na qual o AEM busca e renderiza todos os filhos da estrutura de conteúdo. [](/help/sites-developing/spa-architecture.md#portability)

Qualquer renderização explícita que aponte para um conteúdo específico é considerada uma renderização estática e, embora compatível, não será compatível com os recursos de criação de conteúdo do AEM. Isto também vai contra o princípio da [portabilidade](/help/sites-developing/spa-architecture.md#portability).

### Roteamento dinâmico {#dynamic-routing}

Assim como na renderização, todos os roteamentos também devem ser dinâmicos. No AEM, [o SPA deve ser o proprietário do roteamento](/help/sites-developing/spa-routing.md) e o AEM o escuta e busca conteúdo com base nele.

Qualquer roteamento estático funciona de acordo com o [princípio de portabilidade](/help/sites-developing/spa-architecture.md#portability) e limita o autor ao não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com roteamento estático, se o autor do conteúdo quiser alterar uma rota ou uma página, ele ou ela precisará solicitar que o desenvolvedor de front-end faça isso.

## AEM Project Archetype {#aem-project-archetype}

Qualquer projeto do AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SDK do SPA.

## Modelos de design do SPA {#spa-design-models}

Se os [princípios de desenvolvimento de SPAs no AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) forem seguidos, seu SPA funcionará com todos os recursos de criação de conteúdo do AEM suportados. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

No entanto, podem existir casos em que tal não seja inteiramente necessário. A tabela a seguir apresenta uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>O AEM é usado como um CMS sem cabeçalho sem usar a estrutura SDK do Editor <a href="/help/sites-developing/spa-reference-materials.md">SPA.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem aproveitar a experiência de criação de conteúdo do AEM.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor front-end usa a estrutura SDK do Editor SPA, mas abre apenas algumas áreas para o autor do conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, permitindo apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo estão restritos a um conjunto limitado de experiências de criação de conteúdo do AEM.</p> <p>O código pode não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelo, portanto, o desenvolvedor front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto aproveita totalmente o SDK do Editor SPA e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada ao AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor do conteúdo pode editar o aplicativo usando a experiência de criação de conteúdo do AEM.<br /> </p> <p>O SPA é compatível com o editor de modelos.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando o AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam compatíveis com o AEM, somente ao implementar o terceiro (e, portanto, seguir os princípios de desenvolvimento de [SPA recomendados no AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) os autores de conteúdo poderão interagir e editar o conteúdo do SPA no AEM, conforme estiverem acostumados.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migração de SPAs existentes para o AEM {#migrating-existing-spas-to-aem}

Geralmente, se seu SPA seguir os princípios de desenvolvimento do [SPA para o AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), seu SPA funcionará no AEM e poderá ser editado usando o editor SPA do AEM.

Siga estas etapas para preparar seu SPA existente para trabalhar com o AEM.

1. **Torne seus componentes JS modulares.**

   Torne-os capazes de serem renderizados em qualquer ordem, posição e tamanho.
1. **Use os container fornecidos pelo SDK para colocar seus componentes na tela.**

   O AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente AEM para cada componente JS.**

   Os componentes do AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores front-end {#instructions-for-front-end-developers}

A principal tarefa para ativar um desenvolvedor front-end para criar um SPA para o AEM é concordar com os componentes e seus modelos JSON.

A seguir está um resumo das etapas que um desenvolvedor front-end precisa seguir ao desenvolver um SPA para o AEM.

1. **Concordar em componentes e em seus modelos JSON**

   Os desenvolvedores front-end e os desenvolvedores de AEM back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individual entre os componentes de SPA e os componentes de back-end.

   Os componentes do AEM ainda são necessários principalmente para fornecer caixas de diálogo de edição e exportar o modelo do componente.

1. **Em Reagir componentes, acesse o modelo via`this.props.cqModel`**

   Depois que os componentes forem aceitos e o modelo JSON estiver implementado, o desenvolvedor de front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON via `this.props.cqModel`.

1. **Implementar o`render()`método do componente**

   O desenvolvedor de front-end implementa o `render()` método conforme ele/ela o considerar adequado e pode usar os campos da `cqModel` propriedade. Isso gera os fragmentos DOM e HTML que serão inseridos na página. Essa é a maneira padrão de criar um aplicativo no React.

1. **Mapeie o componente para o tipo de recurso AEM por meio de`MapTo()`**

   O mapeamento armazena classes de componentes e é usado internamente pelo componente fornecido `Container` para recuperar e instanciar dinamicamente componentes com base no tipo de recurso fornecido.

   Isso serve como a &quot;colagem&quot; entre front-end e back-end para que o editor saiba a quais componentes os componentes reagem correspondem.

   Os `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Defina o parâmetro do componente`EditConfig`como`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado desde que ainda não seja renderizado ou não tenha conteúdo para renderizar.

1. **Estender a`Container`classe fornecida para páginas e container**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação aos componentes internos funcione como esperado.

1. **Implemente uma solução de roteamento que use a API HTML5`History`.**

   Quando o `ModelRouter` estiver ativado, chamar as funções `pushState` e `replaceState` disparará uma solicitação para o `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do suporte `ModelRouter` apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não suporta o uso de URLs personalizados ou aliases.

   O `ModelRouter` pode ser desabilitado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como seus componentes React e Angular não precisam de nada específico da Adobe ou do AEM.

* Tudo o que está dentro do componente JavaScript é agnóstico de AEM.
* O que é específico para o AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

O `MapTo` auxiliar é a &quot;cola&quot; que permite que os componentes de back-end e de front-end sejam combinados:

* Ele informa ao container JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor SPA saiba qual caixa de diálogo será exibida ao autor ao editar o componente.

Para obter mais informações sobre como usar `MapTo` e criar SPAs para o AEM em geral, consulte o guia Introdução para sua estrutura selecionada.

* [Introdução aos SPAs no AEM - Reagir](/help/sites-developing/spa-getting-started-react.md)
* [Introdução aos SPAs no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitetura e SPAs do AEM {#aem-architecture-and-spas}

A arquitetura geral do AEM, incluindo ambientes de desenvolvimento, criação e publicação, não é alterada ao usar SPAs. No entanto, é útil entender como o desenvolvimento do SPA se encaixa nessa arquitetura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Criar Ambiente**

   É aqui que a fonte da fonte do aplicativo SPA e da fonte do componente é retirada.

   * O gerador clientlib do NPM cria uma biblioteca de clientes a partir do projeto do SPA.
   * Essa biblioteca será tirada pelo Maven e implantada pelo plug-in Maven Build juntamente com o componente para o autor do AEM.

* **AEM Author**

   O conteúdo é criado no autor do AEM, incluindo a criação de SPAs.

   Quando um SPA é editado usando o Editor SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O Javascript do aplicativo SPA é carregado.
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página incluindo os `cq-data` atributos.
   1. Esses `cq-data` atributos permitem que o editor carregue informações adicionais da página para que ele saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

   É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos de aplicativos SPA, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher / CDN**

   O dispatcher serve como a camada de cache do AEM para visitantes no site.

   * As solicitações são processadas de forma semelhante à forma como estão no autor de AEM, no entanto, não há solicitação de informações da página, pois isso só é necessário para o editor.
   * Javascript, CSS, JSON e HTML são armazenados em cache, otimizando a página para delivery rápido.

>[!NOTE]
>
>Dentro do AEM não há necessidade de executar os mecanismos de criação do Javascript ou executar o próprio Javascript. O AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

Para obter uma visão geral de como um SPA simples no AEM está estruturado e como ele funciona, consulte o guia de introdução para [React](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte o Tutorial [Introdução ao editor SPA AEM - Eventos WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Para obter mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona em SPAs no AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPAs](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar SPAs no AEM para uma estrutura diferente de React ou Angular ou simplesmente desejar aprofundar o modo como o SDK do SPA para AEM funciona, consulte o artigo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
