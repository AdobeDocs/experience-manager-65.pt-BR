---
title: Jornada do desenvolvedor AEM headless
description: Documentação de CMS do AEM sem periféricos. Comece aqui uma jornada guiada sobre os recursos headless avançados e flexíveis do AEM, suas capacidades e como usá-las em seu primeiro projeto.
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: 487136be68e04fd74affe43790587b37d4c3d3ef
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 69%

---

# Jornada do desenvolvedor AEM headless {#aem-headless-developer-journey}

Comece aqui para obter uma jornada guiada sobre os recursos headless avançados e flexíveis do AEM, suas capacidades e como usá-las em seu primeiro projeto de desenvolvimento headless. Esta jornada fornece toda a documentação do AEM Headless necessária para desenvolver seu primeiro aplicativo headless.

## Introdução {#introduction}

A implementação headless dispensa o gerenciamento de páginas e componentes tradicional utilizado em soluções de pilha completa e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em relação ao canal, assim como na entrega entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementação de experiências digitais.

Este guia aborda os tópicos de implementação mais headless no AEM para que, ao concluir, você:

* Tenha uma compreensão completa do que é entrega de conteúdo headless e seus benefícios.
* Entenda os recursos headless do AEM e como eles trabalham juntos para proporcionar uma experiência headless.
* Consiga dar os primeiros passos implementando seu primeiro projeto headless AEM.

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se quiser saber como a Adobe recomenda resolver casos de negócios headless com o AEM, inicie com as [Jornadas headless do AEM](/help/journey-headless/overview.md).

>[!TIP]
>
>Se preferir **aprenda fazendo** e têm conhecimento técnico, visitem os tutoriais AEM Headless, que são organizados por API e estrutura e estão disponíveis no [Seção Recursos adicionais](#additional-resources) no final deste documento.

## Público {#audience}

Essa jornada foi projetada para o perfil do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto AEM Headless da perspectiva do desenvolvedor. A jornada define perfis adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

A seguir estão os perfis que interagem nessa jornada.

| Perfil | Descrição | Função nesta jornada |
|---|---|---|
| Desenvolvedor (público-alvo) | Tem experiência no desenvolvimento de aplicativos headless que consomem conteúdo de diferentes fontes | Público-alvo desta jornada |
| Autor de conteúdo | Cria e gerencia conteúdo que é entregue de forma headless | Os Autores de conteúdo criam conteúdo que o desenvolvedor entrega de forma headless. |
| Administrador | Gerencia as definições básicas e a configuração do AEM | O desenvolvedor trabalha com o administrador para fazer as alterações de configuração necessárias para o desenvolvimento. |
| Arquiteto de conteúdo | Analisa os requisitos dos dados que devem ser entregues pelo método headless e define a estrutura desses dados | Os desenvolvedores trabalham com o arquiteto de conteúdo para entender a estrutura dos dados e os requisitos para fornecê-los de forma headless. |

As informações nesta jornada podem ser úteis para todos os perfis, mas algumas informações podem ser supérfluas para determinadas funções. Fique atento para [jornadas futuras que abordarão funções adicionais.](/help/journey-documentation/home.md#journeys)

## A jornada de desenvolvedores headless {#the-journey}

Muitos tópicos serão explorados nesta jornada. Os artigos a seguir fornecem conhecimento básico sobre headless no AEM e oferecem links para a documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo no headless no AEM, a Adobe recomenda que você comece do início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | Jornada do desenvolvedor AEM headless | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento headless CMS](learn-about.md) | Saiba mais sobre a Tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless](getting-started.md) | Saiba mais sobre os pré-requisitos AEM Headless |
| 3 | [Caminho para sua primeira experiência usando o AEM Headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM Headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. Em seguida, estabeleça essa estrutura no Adobe Experience Manager (AEM) usando modelos de fragmentos de conteúdo e fragmentos de conteúdo, para a reutilização em outros canais. |
| 5 | [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md) | Saiba como usar consultas do GraphQL para acessar o Conteúdo dos fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio de APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o Conteúdo dos fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu projeto AEM e prepará-lo para entrar em vigor com o SDK do AEM headless. |
| 8 | [Como executar o aplicativo headless](go-live.md) | Saiba como implantar o aplicativo em tempo real, colocar seu código local no Git e movê-lo para o Git do Cloud Manager para pipeline de CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPAs) com o AEM](create-spa.md) | Assim que você entender os recursos headless do AEM, explore como combinar delivery headful e headless e saiba como criar SPA editável usando a estrutura do Editor de AEM SPA. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar a jornada headless da Adobe. Recomendamos que você siga para a próxima parte da jornada e leia o artigo [Saiba mais sobre o desenvolvimento headless CMS.](learn-about.md)

### Escolha sua própria aventura {#choose-your-path}

No entanto, a Adobe quer que você tenha sucesso ao começar com seu projeto AEM Headless, independentemente do seu estilo de aprendizado. Portanto, considere essas duas opções.

* Se quiser **saber mais sobre conceitos headless e as tecnologias AEM headless**, continue sua jornada AEM headless, ao revisar, em seguida, o documento [Como modelar seu conteúdo como modelos de conteúdo AEM](model-your-content.md), por meio do qual você aprende a modelar sua estrutura de conteúdo no AEM.
* Se quiser **aprender na prática**, pule para o [Tutorial prático Introdução ao AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR), que o levará diretamente ao desenvolvimento AEM Headless, implementando um projeto simples para expor o conteúdo AEM headless.

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema empresarial fornecendo uma narrativa que o orienta por processos e recursos complexos e inter-relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade empresarial.

Como tal, as jornadas são projetadas para se manterem sozinhas. No entanto, vários deles podem estar relacionados entre si. Confira essas jornadas adicionais para obter mais informações sobre como os eficientes recursos do AEM funcionam juntos.

* [Tutoriais do AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - se você prefere aprender na prática e tem conhecimento técnico, utilize nossos tutoriais práticos organizados por API e estrutura, que exploram a criação e o uso de aplicativos incorporados no AEM Headless.
* [Jornada de tradução do AEM headless](/help/journey-headless/translation/overview.md) - essa jornada de documentação oferece uma ampla compreensão sobre a tecnologia headless, como o AEM fornece conteúdo headless e como você pode traduzi-lo.
* [Jornada de criação headless](/help/journey-headless/author/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e aprenda a modelar o conteúdo em seu primeiro projeto headless.
* [Jornada do arquiteto headless](/help/journey-headless/architect/overview.md) : comece aqui para obter uma introdução aos recursos headless avançados e flexíveis do Adobe Experience Manager e aprender como modelar o conteúdo para seu projeto.
* [Documentação técnica do AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) - Se você já tem uma sólida compreensão de AEM e tecnologias headless, você pode querer consultar diretamente nossos documentos técnicos aprofundados.

   * Um [Introdução ao AEM as a Headless CMS](/help/sites-developing/headless/introduction.md)

* A variável [Portal do desenvolvedor de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
