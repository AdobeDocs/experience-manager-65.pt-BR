---
title: jornada do desenvolvedor sem periféricos do AEM
description: AEM Documentação CMS sem cabeçalho. Comece aqui para obter uma jornada guiada com os recursos avançados e flexíveis do AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento.
source-git-commit: 919cef01470dd930884e97b15f2d40a38872c0d0
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 2%

---

# jornada do desenvolvedor sem periféricos do AEM {#aem-headless-developer-journey}

Comece aqui para obter uma jornada guiada por meio dos recursos avançados e flexíveis sem interface de AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento sem periféricos. Esta jornada fornece toda a Documentação sem cabeçalho AEM necessária para desenvolver seu primeiro aplicativo sem periféricos.

## Introdução {#introduction}

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa, e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em canais e em sua entrega entre canais. É um padrão de desenvolvimento moderno e dinâmico para a implementação de experiências digitais.

Este guia aborda os tópicos de implementação sem cabeçalho no AEM para que, ao concluir, você:

* Ter uma compreensão completa do que é entrega de conteúdo sem periféricos e de seus benefícios.
* Entenda AEM recursos sem periféricos e como eles trabalham juntos para proporcionar uma experiência sem periféricos.
* Tenha a capacidade de realizar as primeiras etapas de implementação do seu primeiro projeto sem periféricos AEM.

## jornadas de documentação de AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados ao fornecer uma narrativa que ajude o leitor, que pode ser novo a AEM, compreender e resolver um problema de negócios do início ao fim, assumindo o mínimo de tópico ou conhecimento AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa Adobe, experiência comprovada de implementação de consultores de Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como resolver casos de negócios sem periféricos com o AEM, [AEM Jornadas headless](/help/journey-headless/home.md) são onde começar.

>[!TIP]
>
> Se preferir **aprenda fazendo** e são tecnicamente inclinados, visite os tutoriais sem cabeçalho do AEM, que são organizados pela API e pela estrutura e estão disponíveis no [Seção Recursos adicionais](#additional-resources) no final deste documento.

## Público {#audience}

Essa jornada foi projetada para o persona do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto sem cabeçalho AEM da perspectiva do desenvolvedor. A jornada define personas adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

A seguir estão as personas que interagem nessa jornada.

| Persona | Descrição | Função nesta Jornada |
|---|---|---|
| Desenvolvedor (público-alvo) | Tem experiência no desenvolvimento de aplicativos sem periféricos que consomem conteúdo de diferentes fontes | Público-alvo desta jornada |
| Autor do conteúdo | Cria e gerencia conteúdo entregue sem interface | Os autores de conteúdo criam conteúdo que o desenvolvedor oferece sem cabeçalho. |
| Administrador | Gerencia a configuração básica e a configuração do AEM | O desenvolvedor trabalha com o administrador para fazer as alterações de configuração necessárias para o desenvolvimento. |
| Arquitetura de conteúdo | Analisa os requisitos dos dados que devem ser entregues sem periféricos e define a estrutura desses dados | Os desenvolvedores trabalham com o arquiteto de conteúdo para entender a estrutura dos dados e os requisitos para fornecê-los sem interrupções. |

As informações nesta jornada podem, é claro, ser úteis para todas as pessoas, mas algumas informações podem ser supérfluas para determinadas funções. Fique ligado para [jornadas futuras que abordarão funções adicionais.](/help/journey-documentation/home.md#journeys)

## A Jornada de desenvolvedores headless {#the-journey}

Você explorará muitos tópicos nesta jornada. Os artigos a seguir fornecem um conhecimento fundamental da AEM sem cabeça e vinculam-se à documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo em AEM sem periféricos, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada do desenvolvedor sem periféricos do AEM | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento sem cabeçalho CMS](learn-about.md) | Saiba mais sobre a tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless](getting-started.md) | Saiba mais sobre AEM pré-requisitos headless |
| 3 | [Caminho para sua primeira experiência usando AEM headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. Em seguida, perceba essa estrutura do Adobe Experience Manager (AEM) usando Modelos de fragmentos de conteúdo e Fragmentos de conteúdo, para reutilização em canais. |
| 5 | [Como acessar seu conteúdo por meio AEM APIs de entrega](access-your-content.md) | Saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio de APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu AEM Project e prepará-lo para entrar em vigor com o AEM Headless SDK. |
| 8 | [Como executar o aplicativo sem periféricos](go-live.md) | Saiba como implantar o aplicativo ao vivo, obter seu código local no Git e movê-lo para o pipeline de Git do Cloud Manager para CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPA) com AEM](create-spa.md) | Assim que você entender AEM recursos headless, explore como combinar delivery headful e headless e saiba como criar SPA editáveis usando AEM estrutura SPA Editor. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar sua jornada sem cabeça do Adobe. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Saiba mais sobre o CMS Headless Development (Desenvolvimento sem periféricos CMS).](learn-about.md)

### Escolha Sua Própria Aventura {#choose-your-path}

No entanto, o Adobe quer que você tenha sucesso à medida que inicia seu projeto sem cabeçalho AEM, independentemente do seu estilo de aprendizagem. Por isso, por favor, considere estas duas opções.

* Se preferir continuar a **saiba mais sobre conceitos sem periféricos e AEM tecnologias sem periféricos**, você deve continuar sua jornada sem periféricos AEM conforme recomendado ao revisar o documento em seguida [Como modelar seu conteúdo como modelos de conteúdo AEM](model-your-content.md) onde você aprende a modelar sua estrutura de conteúdo no AEM.
* Se preferir **aprenda fazendo**, você pode pular para o [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) onde você vai participar diretamente AEM desenvolvimento sem cabeçalho implementando um projeto simples para expor AEM conteúdo sem cabeçalho.

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema comercial fornecendo uma narrativa que o orienta por processos e recursos complexos e inter-relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade de negócios.

Como tais jornadas são projetadas para se sustentarem sozinhas. No entanto, alguns deles podem estar relacionados entre si. Confira estas jornadas adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [Tutoriais AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Se você preferir aprender fazendo e for tecnicamente inclinado, utilize nossos tutoriais práticos organizados por API e framework, que exploram a criação e o uso de aplicativos criados AEM Headless.
* [jornada de tradução sem cabeçalho AEM](/help/journey-headless/translation/overview.md) - Essa jornada de documentação oferece uma ampla compreensão da tecnologia sem interface, como a AEM fornece conteúdo sem interface e como você pode traduzi-la.
* [Jornada de criação sem cabeçalho](/help/journey-headless/author/overview.md) - Comece aqui para obter uma jornada guiada por meio dos recursos avançados e flexíveis sem interface de AEM, seus recursos e como modelar seu conteúdo em seu primeiro projeto sem interface.
* [Jornada de arquitetura headless](/help/journey-headless/architect/overview.md) - Comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como modelar o conteúdo para seu projeto.
* [Documentação técnica AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) - Se você já tiver um conhecimento profundo das tecnologias AEM e sem interface, poderá consultar diretamente nossos documentos técnicos aprofundados.
