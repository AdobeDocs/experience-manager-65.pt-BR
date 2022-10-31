---
title: jornada do desenvolvedor sem periféricos do AEM
description: AEM Documentação CMS sem cabeçalho. Comece aqui para obter uma jornada guiada com os recursos avançados e flexíveis do AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento.
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 26%

---

# jornada do desenvolvedor sem periféricos do AEM {#aem-headless-developer-journey}

Comece aqui para obter uma jornada guiada por meio dos recursos avançados e flexíveis sem interface de AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento sem periféricos. Esta jornada fornece toda a Documentação sem cabeçalho AEM necessária para desenvolver seu primeiro aplicativo sem periféricos.

## Introdução {#introduction}

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa, e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em canais e em sua entrega entre canais. É um padrão de desenvolvimento moderno e dinâmico para a implementação de experiências digitais.

Este guia aborda os tópicos de implementação sem cabeçalho no AEM para que, ao concluir, você:

* Ter uma compreensão completa do que é entrega de conteúdo sem periféricos e de seus benefícios.
* Entenda AEM recursos sem periféricos e como eles trabalham juntos para proporcionar uma experiência sem periféricos.
* Tenha a capacidade de realizar as primeiras etapas de implementação do seu primeiro projeto sem periféricos AEM.

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como resolver casos de negócios sem periféricos com o AEM, [AEM Jornadas headless](/help/journey-headless/home.md) são onde começar.

>[!TIP]
>
>Se preferir **aprenda fazendo** e são tecnicamente inclinados, visite os tutoriais sem cabeçalho do AEM, que são organizados pela API e pela estrutura e estão disponíveis no [Seção Recursos adicionais](#additional-resources) no final deste documento.

## Público {#audience}

Essa jornada foi projetada para o persona do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto sem cabeçalho AEM da perspectiva do desenvolvedor. A jornada define personas adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

A seguir estão os perfis que interagem nessa jornada.

| Perfil | Descrição | Função nesta Jornada |
|---|---|---|
| Desenvolvedor (público-alvo) | Tem experiência no desenvolvimento de aplicativos sem periféricos que consomem conteúdo de diferentes fontes | Público-alvo desta jornada |
| Autor de conteúdo | Cria e gerencia conteúdo entregue sem interface | Os autores de conteúdo criam conteúdo que o desenvolvedor oferece sem cabeçalho. |
| Administrador | Gerencia as definições básicas e a configuração do AEM | O desenvolvedor trabalha com o administrador para fazer as alterações de configuração necessárias para o desenvolvimento. |
| Arquiteto de conteúdo | Analisa os requisitos dos dados que devem ser entregues sem periféricos e define a estrutura desses dados | Os desenvolvedores trabalham com o arquiteto de conteúdo para entender a estrutura dos dados e os requisitos para fornecê-los sem interrupções. |

As informações nesta jornada podem ser úteis para todos os perfis, mas algumas informações podem ser supérfluas para determinadas funções. Fique atento para [jornadas futuras que abordarão funções adicionais.](/help/journey-documentation/home.md#journeys)

## A Jornada de desenvolvedores headless {#the-journey}

Muitos tópicos serão explorados nesta jornada. Os artigos a seguir fornecem um conhecimento fundamental da AEM sem cabeça e vinculam-se à documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo em AEM sem periféricos, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada do desenvolvedor sem periféricos do AEM | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento headless CMS](learn-about.md) | Saiba mais sobre a tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless](getting-started.md) | Saiba mais sobre AEM pré-requisitos headless |
| 3 | [Caminho para sua primeira experiência usando o AEM Headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. Em seguida, perceba essa estrutura do Adobe Experience Manager (AEM) usando Modelos de fragmentos de conteúdo e Fragmentos de conteúdo, para reutilização em canais. |
| 5 | [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md) | Saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio de APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu AEM Project e prepará-lo para entrar em vigor com o AEM Headless SDK. |
| 8 | [Como executar o aplicativo headless](go-live.md) | Saiba como implantar o aplicativo ao vivo, obter seu código local no Git e movê-lo para o pipeline de Git do Cloud Manager para CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPA) com AEM](create-spa.md) | Assim que você entender AEM recursos headless, explore como combinar delivery headful e headless e saiba como criar SPA editáveis usando AEM estrutura SPA Editor. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar sua jornada sem cabeça do Adobe. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Saiba mais sobre o CMS Headless Development (Desenvolvimento sem periféricos CMS).](learn-about.md)

### Escolha Sua Própria Aventura {#choose-your-path}

No entanto, o Adobe quer que você tenha sucesso à medida que inicia seu projeto sem cabeçalho AEM, independentemente do seu estilo de aprendizagem. Por isso, por favor, considere estas duas opções.

* Se preferir continuar a **saiba mais sobre conceitos sem periféricos e AEM tecnologias sem periféricos**, você deve continuar sua jornada sem periféricos AEM conforme recomendado ao revisar o documento em seguida [Como modelar seu conteúdo como modelos de conteúdo AEM](model-your-content.md) onde você aprende a modelar sua estrutura de conteúdo no AEM.
* Se preferir **aprenda fazendo**, você pode pular para o [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR) onde você vai participar diretamente AEM desenvolvimento sem cabeçalho implementando um projeto simples para expor AEM conteúdo sem cabeçalho.

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema comercial fornecendo uma narrativa que o orienta por processos e recursos complexos e inter-relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade de negócios.

Como tais jornadas são projetadas para se sustentarem sozinhas. No entanto, alguns deles podem estar relacionados entre si. Confira estas jornadas adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [Tutoriais do AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - se você prefere aprender na prática e tem conhecimento técnico, utilize nossos tutoriais práticos organizados por API e estrutura, que exploram a criação e o uso de aplicativos incorporados no AEM Headless.
* [jornada de tradução sem cabeçalho AEM](/help/journey-headless/translation/overview.md) - Essa jornada de documentação oferece uma ampla compreensão da tecnologia sem interface, como a AEM fornece conteúdo sem interface e como você pode traduzi-la.
* [Jornada de criação headless](/help/journey-headless/author/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e aprenda a modelar o conteúdo em seu primeiro projeto headless.
* [Jornada de arquitetura headless](/help/journey-headless/architect/overview.md) - Comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como modelar o conteúdo para seu projeto.
* [Documentação técnica do AEM ](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) - se você já tiver uma sólida compreensão das tecnologias headless e do AEM, poderá consultar diretamente os nossos documentos técnicos detalhados.
