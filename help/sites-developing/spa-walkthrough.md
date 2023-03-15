---
title: Introdução e passo a passo do SPA
description: Este artigo apresenta os conceitos de um SPA e aborda o uso de um SPA básico para criação, mostrando como ele está relacionado ao editor de SPA integrado do AEM.
topic-tags: spa
content-type: reference
exl-id: 95990112-2afc-420a-a7c7-9613f40d4c4a
source-git-commit: 0e8ad326e883f73e795929ce7d5d36f1bcdc5347
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 73%

---


# Introdução e passo a passo do SPA {#spa-introduction-and-walkthrough}

Aplicativos de página única (SPAs) podem oferecer experiências interessantes para usuários de sites. Os desenvolvedores desejam criar sites usando estruturas de SPA, e os autores desejam editar o conteúdo de um site criado usando essas estruturas diretamente no AEM.

O editor de SPA oferece uma solução abrangente para permitir o uso de SPAs no AEM. Este artigo aborda o uso de um SPA básico para criação e mostra como ele se relaciona ao editor de SPA integrado do AEM.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

### Objetivo do artigo {#article-objective}

Este artigo apresenta os conceitos básicos sobre SPAs antes de conduzir o leitor por um passo a passo do editor de SPA, usando um SPA simples para demonstrar a edição básica de conteúdo. Em seguida, ele se aprofunda na construção da página e em como o SPA se relaciona e interage com o editor de SPA do AEM.

A meta desta introdução e passo a passo é demonstrar a um desenvolvedor do AEM por que SPAs são relevantes, como eles geralmente funcionam, como um SPA é manipulado pelo editor de SPA do AEM e como ele é diferente de um aplicativo padrão do AEM.

## Requisitos {#requirements}

O passo a passo é baseado na funcionalidade padrão do AEM e no aplicativo de exemplo Projeto SPA WKND. Para acompanhar esse passo a passo, você deve ter o seguinte disponível.

* [AEM versão 6.5.4 ou mais recente](/help/release-notes/release-notes.md)
   * Você deve ter direitos de administrador no sistema.
* [O aplicativo de exemplo Projeto SPA WKND está disponível no GitHub](https://github.com/adobe/aem-guides-wknd-spa)
   * Baixe o [última versão do aplicativo React.](https://github.com/adobe/aem-guides-wknd-spa/releases) Ele será nomeado como semelhante a `wknd-spa-react.all.classic-X.Y.Z-SNAPSHOT.zip`.
   * Baixe o [imagens de amostra mais recentes](https://github.com/adobe/aem-guides-wknd-spa/releases) para o aplicativo. Ele será nomeado como semelhante a `wknd-spa-sample-images-X.Y.Z.zip`.
   * [Usar gerenciador de pacotes](/help/sites-administering/package-manager.md) para instalar os pacotes como você faria com qualquer outro pacote no AEM.
   * O aplicativo não precisa ser instalado usando o Maven para fins deste passo a passo.

>[!CAUTION]
>
>Este documento usa o [Aplicativo de projeto Spa WKND](https://github.com/adobe/aem-guides-wknd-spa) apenas para fins de demonstração. Ele não deve ser utilizado ao trabalhar em projetos.
>
>Qualquer projeto AEM deve aproveitar [Arquétipo de projeto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) que suporta projetos SPA usando o React ou Angular e aproveita o SDK SPA.

### O que é um SPA? {#what-is-a-spa}

Um aplicativo de página única (SPA) é diferente de uma página convencional, no sentido de que ele é renderizado no lado do cliente e orientado principalmente por Javascript, dependendo das chamadas do Ajax para carregar dados e atualizar dinamicamente a página. A maior parte ou todo o conteúdo é recuperado uma vez em um único carregamento de página, com os recursos adicionais sendo carregados de forma assíncrona conforme necessário, com base na interação do usuário com a página.

Isso reduz a necessidade de atualizações de página e apresenta uma experiência ao usuário que é contínua, rápida e se parece mais com uma experiência de aplicativo nativo.

O editor de SPA do AEM permite que desenvolvedores de front-end criem SPAs que possam ser integrados a um site do AEM, possibilitando que os autores de conteúdo editem o conteúdo do SPA tão facilmente quanto qualquer outro conteúdo do AEM.

### Por que um SPA? {#why-a-spa}

Devido a ser mais rápido, fluido e semelhante a um aplicativo nativo, um SPA apresenta uma experiência muito atrativa não apenas para o visitante da página da web, mas também para profissionais de marketing e desenvolvedores, devido à natureza do funcionamento dos SPAs.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visitantes**

* Os visitantes desejam experiências nativas quando interagem com o conteúdo.
* Dados claros informam que quanto mais rapidamente uma página é exibida, maior é a possibilidade de uma conversão.

**Profissionais de marketing**

* Os profissionais de marketing desejam oferecer experiências nativas e relevantes para atrair visitantes a se envolverem totalmente com o conteúdo.
* A personalização pode tornar essas experiências ainda mais atrativas.

**Desenvolvedores**

* Os desenvolvedores desejam uma separação clara entre o conteúdo e a apresentação.
* Uma boa separação torna o sistema mais extensível, além de permitir o desenvolvimento independente do front-end.

### Como funciona um SPA? {#how-does-a-spa-work}

A ideia principal por trás de um SPA é que as chamadas e a dependência em um servidor sejam reduzidas para minimizar os atrasos causados pelas chamadas do servidor, de modo que o SPA se aproxime da capacidade de resposta de um aplicativo nativo.

Em uma página da web tradicional e sequencial, somente os dados necessários para a página imediata são carregados. Isso significa que quando o visitante se move para outra página, o servidor é chamado para os recursos adicionais. As chamadas adicionais podem ser necessárias, pois o visitante interage com elementos na página. Essas várias chamadas podem criar uma sensação de defasagem ou atraso na página, pois ela precisa acompanhar as solicitações do visitante.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Para uma experiência mais fluida, que se aproxima do que um visitante espera de aplicativos móveis e nativos, um SPA carrega todos os dados necessários para o visitante na primeira carga. Embora possa ser um pouco mais demorado no início, isso elimina a necessidade de chamadas de servidor adicionais.

Ao renderizar no lado do cliente, o elemento da página reage mais rapidamente e as interações com a página pelo visitante são imediatas. Qualquer dado adicional que possa ser necessário é chamado de forma assíncrona para maximizar a velocidade da página.

>[!NOTE]
>
>Para obter detalhes técnicos sobre como SPA trabalhar no AEM, consulte o artigo [Introdução ao SPA no AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Para uma análise mais detalhada do design, arquitetura e fluxo de trabalho técnico do Editor de SPA, consulte o artigo [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md).

## Experiência de edição de conteúdo com SPA {#content-editing-experience-with-spa}

Quando uma SPA é criada para aproveitar o Editor de SPA de AEM, o autor de conteúdo não percebe diferença ao editar e criar conteúdo. A funcionalidade comum do AEM pode ser utilizada e nenhuma alteração no fluxo de trabalho do autor é necessária.

1. Edite o aplicativo Projeto SPA WKND no AEM.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Etapa 1](assets/spa-walkthrough-step-1.png)

1. Selecione um componente de cabeçalho e observe que uma barra de ferramentas aparece como para qualquer outro componente. Selecione **Editar**.

   ![Etapa 2](assets/spa-walkthrough-step-2.png)

1. Edite o conteúdo normalmente no AEM e observe que as alterações são mantidas.

   ![Etapa 3](assets/spa-walkthrough-step-3.png)

   >[!NOTE]
   >
   >Consulte a [Visão geral do editor de SPA](spa-overview.md#requirements-limitations) para obter mais informações sobre o editor de texto em vigor e o SPA.

1. Use o Navegador de ativos para arrastar e soltar uma nova imagem em um componente de imagem.

   ![Etapa 4](assets/spa-walkthrough-step-4.png)

1. A alteração é mantida.

   ![Etapa 5](assets/spa-walkthrough-step-5.png)

Outras operações de criação são permitidas, como arrastar e soltar componentes adicionais na página, reorganizar componentes e modificar o layout, assim como acontece em qualquer outro aplicativo do que não seja um SPA.

>[!NOTE]
>
>O editor de SPA não modifica o DOM do aplicativo. O próprio SPA é responsável pelo DOM.
>
>Para ver como isso funciona, prossiga para a próxima seção deste artigo: [SPAs e o editor de SPA do AEM](#spa-apps-and-the-aem-spa-editor).

## SPAs e o editor de SPA do AEM {#spa-apps-and-the-aem-spa-editor}

Usar o comportamento de um SPA para o usuário final e, em seguida, inspecionar a página de SPA ajuda a entender melhor como um aplicativo SAP funciona com o Editor de SPA em AEM.

### Usando um SPA {#using-an-spa-application}

1. Carregue o aplicativo Projeto SPA WKND no servidor de publicação ou usando a opção **Exibir como publicado**, no menu **Informações da página** do editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Etapa 1](assets/spa-walkthrough-step-1-1.png)

   Observe a estrutura das páginas, incluindo a navegação para páginas filhas, widget de clima e artigos.

1. Navegue até uma página secundária usando o menu e veja que a página é carregada imediatamente sem a necessidade de uma atualização.

   ![Etapa 2](assets/spa-walkthrough-step-1-2.png)

1. Abra as ferramentas do desenvolvedor incorporadas ao seu navegador e monitore a atividade da rede à medida que navega pelas páginas secundárias.

   ![Etapa 3](assets/spa-walkthrough-step-1-3.png)

   Há muito pouco tráfego ao mudar de uma página para outra no aplicativo. A página não é recarregada e somente as novas imagens são solicitadas.

   O SPA gerencia o conteúdo e o roteamento totalmente no lado do cliente.

Mas se a página não é recarregada ao navegar pelas páginas secundárias, como ela é carregada?

A próxima seção, [Carregamento de um aplicativo SPA,](#loading-an-spa-application) aprofunda-se nos mecanismos de carregamento de SPA e como o conteúdo pode ser carregado de forma síncrona e assíncrona.

### Carregar um SPA {#loading-an-spa-application}

1. Se ainda não o tiver carregado, carregue o aplicativo Projeto SPA WKND no servidor de publicação ou usando a opção **Exibir como publicado**, no menu **Informações da página** do editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Etapa 1](assets/spa-walkthrough-step-1-1.png)

1. Use a ferramenta incorporada do seu navegador para visualizar a fonte da página.
1. Observe que o conteúdo da fonte é extremamente limitado.

   * A página não possui conteúdo em seu corpo. Ele é composto principalmente de folhas de estilo e uma chamada para vários scripts, como `clientlib-react.min.js`.
   * Esses scripts são os principais acionadores desse aplicativo e são responsáveis por renderizar todo o conteúdo.

1. Use as ferramentas internas do seu navegador para inspecionar a página. Veja o conteúdo do DOM totalmente carregado.

   ![Etapa 4](assets/spa-walkthrough-step-1-4.png)

1. Alterne para **Rede** das ferramentas do desenvolvedor e recarregue a página.

   Ignorando solicitações de imagem, observe que os recursos primários carregados para a página são a própria página, o CSS, o React Javascript, suas dependências, bem como os dados JSON da página.

   ![Etapa 5](assets/spa-walkthrough-step-1-5.png)

1. Carregue o `react.model.json` em uma nova guia.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![Etapa 6](assets/spa-walkthrough-step-1-6.png)

   O editor de SPA do AEM aproveita os [serviços de conteúdo do AEM](/help/assets/content-fragments/content-fragments.md) para fornecer todo o conteúdo da página como um modelo JSON.

   Ao implementar interfaces específicas, os modelos do Sling fornecem as informações necessárias para o SPA. A entrega dos dados JSON é delegada de cima para baixo a cada componente (da página, ao parágrafo, ao componente etc.).

   Cada componente escolhe o que expõe e como é renderizado (no lado do servidor com HTL ou no lado do cliente com o React). Este artigo se concentra na renderização do lado do cliente com o React.

1. O modelo também pode agrupar as páginas para que elas sejam carregadas de forma síncrona, reduzindo o número de recarregamentos de página necessários.

   No exemplo do aplicativo Projeto SPA WKND, as páginas `home`, `page-1`, `page-2` e `page-3` são carregadas de forma síncrona, já que os visitantes normalmente visitam todas essas páginas.

   Esse comportamento não é obrigatório e é totalmente configurável.

   ![Etapa 7](assets/spa-walkthrough-step-1-7.png)

1. Para exibir essa diferença de comportamento, recarregue a página e limpe a atividade de rede das ferramentas do desenvolvedor. Navegue para `page-1` no menu da página e veja que a única atividade de rede é uma solicitação de imagem da `page-1`. A `page-1` em si não precisa ser carregada.

   ![Etapa 8](assets/spa-walkthrough-step-1-8.png)

### Interação com o editor de SPA {#interaction-with-the-spa-editor}

Usando o aplicativo de exemplo Projeto SPA WKND, fica claro como o aplicativo se comporta e como ele é carregado quando publicado, aproveitando os serviços de conteúdo para a entrega de conteúdo JSON, bem como o carregamento assíncrono de recursos.

Além disso, para o autor de conteúdo, a criação de conteúdo no editor de SPA é realizada sem interrupções no AEM.

Na seção a seguir, exploraremos o contrato que permite que o editor de SPA relacione componentes dentro do SPA aos componentes do AEM, o que garante essa experiência de edição contínua.

1. Carregue o aplicativo Projeto SPA WKND no editor e alterne para o modo de **Visualização**.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Usando as ferramentas de desenvolvedor incorporadas do seu navegador, inspecione o conteúdo da página. Usando a ferramenta de seleção, selecione um componente editável na página e visualize os detalhes do elemento.

   Observe que o componente tem um novo atributo de dados `data-cq-data-path`.

   ![Etapa 2](assets/spa-walkthrough-step-2-2.png)

   Por exemplo

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Esse caminho permite a recuperação e a associação do objeto de configuração de contexto de edição de cada componente.

   Esse é o único atributo de marcação necessário para que o editor reconheça esse componente como editável no SPA. Com base nesse atributo, o editor de SPA determinará qual configuração editável está associada ao componente, para que os elementos (quadro, barra de ferramentas etc.) corretos sejam carregados.

   Alguns nomes de classe específicos também são adicionados para marcar espaços reservados e para a funcionalidade de arrastar e soltar ativos.

   >[!NOTE]
   >
   >Essa é uma alteração no comportamento de páginas renderizadas do lado do servidor no AEM, onde há uma `cq` elemento inserido para cada componente editável.
   >
   >
   >Essa abordagem no SPA remove a necessidade de inserir elementos personalizados, confiando apenas em um atributo de dados adicional, tornando a marcação mais simples para o desenvolvedor principal.

## Próximas etapas {#next-steps}

Agora que você entende a experiência de edição de SPA no AEM e como um SPA se relaciona ao editor de SPA, aprofunde-se ainda mais para entender como um SPA é criado.

* [Introdução ao SPA no AEM](/help/sites-developing/spa-getting-started-react.md) mostra como um SPA básico é criado para funcionar com o Editor de SPA no AEM
* A [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md) aborda em detalhes o modelo de comunicação do AEM e do SPA.
* O artigo [Desenvolvimento de SPAs para o AEM](/help/sites-developing/spa-architecture.md) descreve como envolver desenvolvedores de front-end no desenvolvimento de um SPA para o AEM e como os SPAs interagem com a arquitetura do AEM.
