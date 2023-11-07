---
title: Desenvolvimento do SPA para Adobe Experience Manager
description: Este artigo apresenta questões importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para Adobe Experience Manager (AEM AEM SPA SPA AEM) e fornece uma visão geral da arquitetura do em relação ao para ter em mente ao implantar um desenvolvido no.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 6%

---

# Desenvolvimento de SPAs para o AEM{#developing-spas-for-aem}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas SPA, e os autores desejam editar o conteúdo no Adobe Experience Manager (AEM) para um site criado com essas estruturas.

Este artigo apresenta perguntas importantes a serem consideradas ao envolver um desenvolvedor de front-end para desenvolver um SPA para AEM e fornece uma visão geral da arquitetura do AEM em relação à implantação do no SPA AEM.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização no lado do cliente baseada na estrutura SPA (por exemplo, React ou Angular).

## Princípios de desenvolvimento do SPA para AEM {#spa-development-principles-for-aem}

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Se, como desenvolvedor de front-end, você seguir essas práticas recomendadas gerais e alguns princípios específicos do AEM, seu SPA estará funcional com [AEM e seus recursos de criação de conteúdo](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilidade](/help/sites-developing/spa-architecture.md#portability) -** Assim como com qualquer componente, os componentes devem ser criados para serem o mais portáteis possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **[AEM controla a estrutura do site](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** - O desenvolvedor de front-end cria componentes e tem a propriedade de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **[Renderização dinâmica](/help/sites-developing/spa-architecture.md#dynamic-rendering)** - Todas as renderizações devem ser dinâmicas.
* **[Roteamento Dinâmico](#dynamic-routing) -** O SPA é responsável pelo roteamento e o AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Se você considerar esses princípios ao desenvolver seu SPA, ele será o mais flexível e inovador possível e, ao mesmo tempo, ativará todas as funcionalidades de criação compatíveis com AEM.

Se não precisar de suporte para recursos de criação de AEM, talvez seja necessário considerar um [Modelo de design SPA](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilidade {#portability}

Assim como no desenvolvimento de qualquer componente, seus componentes devem ser projetados de forma a maximizar sua portabilidade. Quaisquer padrões que funcionem contra a portabilidade ou reutilização dos componentes devem ser evitados para garantir a compatibilidade, a flexibilidade e a manutenção no futuro.

O SPA resultante deve ser construído com componentes altamente portáteis e reutilizáveis.

### AEM direciona a estrutura do site {#aem-drives-site-structure}

O desenvolvedor de front-end deve se considerar responsável pela criação de uma biblioteca de componentes SPA usados para criar o aplicativo. O desenvolvedor de front-end tem controle total da estrutura interna dos componentes. [No entanto, o AEM, em todos os momentos, é o dono da estrutura do site.](/help/sites-developing/spa-overview.md)

Isso significa que o desenvolvedor de front-end pode adicionar conteúdo do cliente antes ou depois do ponto de entrada dos componentes e também pode fazer chamadas de terceiros dentro do componente. No entanto, o desenvolvedor de front-end não tem controle total sobre como os componentes se aninham, por exemplo.

### Renderização dinâmica {#dynamic-rendering}

O SPA deve depender apenas da renderização dinâmica do conteúdo. Essa é a expectativa padrão em que o AEM busca e renderiza todos os filhos da estrutura de conteúdo.

Qualquer renderização explícita que aponte para um conteúdo específico é considerada renderização estática e, embora suportada, não será compatível com os recursos de criação de conteúdo AEM. Isto é igualmente contrário ao princípio da [portabilidade](/help/sites-developing/spa-architecture.md#portability).

### Roteamento Dinâmico {#dynamic-routing}

Assim como na renderização, todo o roteamento também deve ser dinâmico. No AEM, [o SPA sempre deve ser o proprietário do roteamento](/help/sites-developing/spa-routing.md) e o AEM escuta e busca conteúdo com base nela.

Qualquer roteamento estático funciona contra o [princípio da portabilidade](/help/sites-developing/spa-architecture.md#portability) e limita o autor por não ser compatível com os recursos de criação de conteúdo do AEM. Por exemplo, com o roteamento estático, se o autor de conteúdo quiser alterar uma rota ou alterar uma página, ele terá que solicitar que o desenvolvedor de front-end faça isso.

## Arquétipo de projeto do AEM {#aem-project-archetype}

Qualquer projeto do AEM deve utilizar o [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que aceita projetos SPA que usam o React ou o Angular e utiliza o SDK de SPA.

## Modelos de design SPA {#spa-design-models}

Se a variável [princípios do desenvolvimento do AEM no SPA](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) forem seguidos, o SPA funcionará com todos os recursos de criação de conteúdo AEM compatíveis.

Pode haver casos em que isso não seja totalmente necessário. A tabela a seguir fornece uma visão geral dos vários modelos de design, suas vantagens e suas desvantagens.

<table>
 <tbody>
  <tr>
   <th><strong>Modelo de design<br /> </strong></th>
   <th><strong>Vantagens</strong></th>
   <th><strong>Desvantagens</strong></th>
  </tr>
  <tr>
   <td>O AEM é usado como um CMS headless sem usar o <a href="/help/sites-developing/spa-reference-materials.md">Estrutura do SDK do editor de SPA.</a></td>
   <td>O desenvolvedor front-end tem controle total sobre o aplicativo.</td>
   <td><p>Os autores de conteúdo não podem usar a experiência de criação de conteúdo AEM.</p> <p>O código não é portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O desenvolvedor de front-end usa a estrutura do SDK do Editor de SPA, mas abre apenas algumas áreas para o autor de conteúdo.</td>
   <td>O desenvolvedor mantém controle sobre o aplicativo, habilitando apenas a criação em áreas restritas do aplicativo.</td>
   <td><p>Os autores de conteúdo estão restritos a um conjunto limitado de experiências de criação de conteúdo no AEM.</p> <p>O código corre o risco de não ser portátil nem reutilizável se contiver referências estáticas ou roteamento.</p> <p>Não permite o uso do editor de modelos, portanto, o desenvolvedor de front-end deve manter modelos editáveis por meio do JCR.</p> </td>
  </tr>
  <tr>
   <td>O projeto usa totalmente o SDK do Editor de SPA, e os componentes de front-end são desenvolvidos como uma biblioteca e a estrutura de conteúdo do aplicativo é delegada ao AEM.</td>
   <td><p>O aplicativo é reutilizável e portátil.</p> <p>O autor de conteúdo pode editar o aplicativo usando a experiência de criação de conteúdo AEM.<br /> </p> <p>O SPA é compatível com o editor de modelos.</p> </td>
   <td><p>O desenvolvedor não controla a estrutura do aplicativo e a parte do conteúdo delegada ao AEM.</p> <p>O desenvolvedor ainda pode reservar áreas do aplicativo para o conteúdo que não deve ser criado usando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Embora todos os modelos sejam suportados no AEM, somente implementando o terceiro (e, portanto, seguindo o recomendado) [Princípios de desenvolvimento do SPA no AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)SPA ) os autores de conteúdo poderão interagir com o AEM e editá-lo conforme estão acostumados.

## Migração do AEM existente para o SPA {#migrating-existing-spas-to-aem}

Geralmente, se o seu SPA seguir o [Princípios de desenvolvimento do SPA para AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), em seguida, seu SPA funcionará no AEM e será editável usando o editor de AEM do SPA.

Siga estas etapas para preparar seu SPA existente para trabalhar com AEM.

1. **Torne seus componentes JS modulares.**

   Torne-os capazes de ser renderizados em qualquer ordem, posição e tamanho.
1. **Use os contêineres fornecidos pelo SDK do Adobe para colocar seus componentes na tela.**

   O AEM fornece um componente de sistema de página e parágrafo para você usar.
1. **Crie um componente AEM para cada componente JS.**

   Os componentes AEM definem a caixa de diálogo e a saída JSON.

## Instruções para desenvolvedores de front-end {#instructions-for-front-end-developers}

A principal tarefa de envolver um desenvolvedor de front-end para criar um SPA para AEM é chegar a um acordo sobre os componentes e seus modelos JSON.

Veja a seguir um resumo das etapas que um desenvolvedor de front-end precisa seguir ao desenvolver um SPA para AEM.

1. **Concordar sobre os componentes e seu modelo JSON**

   Desenvolvedores de front-end e desenvolvedores de AEM de back-end precisam concordar sobre quais componentes são necessários e um modelo para que haja uma correspondência individualizada entre os componentes de SPA e os componentes de back-end.

   Os componentes do AEM ainda são necessários, principalmente para fornecer caixas de diálogo de edição e exportar o modelo de componentes.

1. **Nos componentes do React, acesse o modelo via`this.props.cqModel`**

   Quando os componentes forem acordados e o modelo JSON estiver em vigor, o desenvolvedor de front-end poderá desenvolver o SPA e simplesmente acessar o modelo JSON por meio de `this.props.cqModel`.

1. **Implementar do componente `render()` método**

   O desenvolvedor de front-end implementa o `render()` como bem entenderem e podem usar os campos de `cqModel` propriedade. Isso gera o DOM e os fragmentos de HTML inseridos na página. Essa é a maneira padrão de criar um aplicativo no React.

1. **Mapear o componente para o tipo de recurso AEM via`MapTo()`**

   O mapeamento armazena classes de componente e é usado internamente pelo `Container` componente para recuperar e instanciar dinamicamente os componentes com base no tipo de recurso especificado.

   Isso serve como &quot;cola&quot; entre o front-end e o back-end, para que o editor saiba a quais componentes os componentes de reação correspondem.

   A variável `Page` e `ResponsiveGrid` são bons exemplos de classes que estendem a base `Container`.

1. **Definir o `EditConfig` como parâmetro para`MapTo()`**

   Esse parâmetro é necessário para informar ao editor como o componente deve ser nomeado, desde que ainda não tenha sido renderizado ou não tenha conteúdo para renderizar.

1. **Estender o fornecido `Container` classe para páginas e contêineres**

   Os sistemas de páginas e parágrafos devem estender essa classe para que a delegação para componentes internos funcione conforme esperado.

1. **Implementar uma solução de roteamento que use o HTML `History` API.**

   Quando a variável `ModelRouter` está ativado, chamando o `pushState` e `replaceState` acionar uma solicitação para o `PageModelManager` para buscar um fragmento ausente do modelo.

   A versão atual do `ModelRouter` O suporta apenas o uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

   A variável `ModelRouter` O pode ser desativado ou configurado para ignorar uma lista de expressões regulares.

## AEM-Agnóstico {#aem-agnostic}

Esses blocos de código ilustram como os componentes do React e do Angular não precisam de nada que seja específico do Adobe ou do AEM.

* Tudo o que está dentro do componente JavaScript é independente de AEM.
* No entanto, o que é específico do AEM é que o componente JS deve ser mapeado para um componente AEM com o auxiliar MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

A variável `MapTo` helper é a &quot;cola&quot; que permite que os componentes de back-end e front-end sejam combinados:

* Informa ao contêiner JS (ou sistema de parágrafo JS) qual componente JS é responsável pela renderização de cada um dos componentes presentes no JSON.
* Ele adiciona um atributo de dados HTML ao HTML que o componente JS renderiza, para que o Editor de SPA saiba qual caixa de diálogo exibir para o autor ao editar o componente.

Para obter mais informações sobre o uso de `MapTo` e a criação do AEM para SPA em geral, consulte o guia de Introdução para a estrutura escolhida.

* [SPA Introdução ao AEM - React](/help/sites-developing/spa-getting-started-react.md)
* [Introdução ao SPA no AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Arquitetura do AEM e SPA {#aem-architecture-and-spas}

A arquitetura geral do AEM, incluindo ambientes de desenvolvimento, criação e publicação, não é alterada ao usar o SPA. No entanto, é útil compreender como o desenvolvimento do SPA se encaixa nessa arquitetura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Ambiente de compilação**

  É aqui que a origem do aplicativo SPA e a origem do componente são verificadas.

   * O gerador de clientlib do NPM cria uma biblioteca do cliente a partir do projeto SPA.
   * Essa biblioteca é retirada pelo Maven e implantada pelo plug-in Maven Build, juntamente com o componente, no autor do AEM.

* **Autor do AEM**

  O conteúdo é criado sobre o autor de AEM, incluindo a criação de SPA.

  Quando um SPA é editado usando o Editor de SPA no ambiente de criação:

   1. O SPA solicita o HTML externo.
   1. O CSS é carregado.
   1. O JavaScript do aplicativo SPA é carregado.
   1. Quando o aplicativo SPA é executado, o JSON é solicitado, permitindo que o aplicativo crie o DOM da página, incluindo o `cq-data` atributos.
   1. Este `cq-data` Os atributos permitem que o editor carregue informações adicionais da página para que saiba quais configurações de edição estão disponíveis para os componentes.

* **AEM Publish**

  É aqui que o conteúdo criado e as bibliotecas compiladas, incluindo artefatos de aplicativos SPA, clientlibs e componentes, são publicados para consumo público.

* **Dispatcher/CDN**

  O Dispatcher serve como a camada de armazenamento em cache do AEM para os visitantes do site.

   * As solicitações são processadas de forma semelhante à do autor AEM. No entanto, não há solicitação de informações da página, pois elas são necessárias somente para o editor.
   * JavaScript, CSS, JSON e HTML são armazenados em cache, otimizando a página para entrega rápida.

>[!NOTE]
>
>Dentro do AEM, não há necessidade de executar mecanismos de criação JavaScript ou executar o próprio JavaScript. O AEM hospeda somente os artefatos compilados do aplicativo SPA.

## Próximas etapas {#next-steps}

Para obter uma visão geral de como um SPA simples no AEM está estruturado e como ele funciona, consulte o guia de introdução para ambos [React](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Para obter um guia passo a passo sobre como criar seu próprio SPA, consulte o [Introdução ao editor SPA AEM - Tutorial de eventos do WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=pt-BR).

SPA Para mais detalhes sobre o modelo dinâmico para mapeamento de componentes e como ele funciona dentro do AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se você quiser implementar o SPA no AEM para uma estrutura diferente do React ou do Angular SPA AEM ou simplesmente quiser se aprofundar em como funciona o SDK do para o, consulte o [Blueprint SPA](/help/sites-developing/spa-blueprint.md) artigo.
