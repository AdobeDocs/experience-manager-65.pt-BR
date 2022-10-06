---
title: jornada de tradução sem cabeçalho AEM
description: Comece aqui para obter uma jornada guiada por meio da tradução do conteúdo sem periféricos usando AEM ferramentas de tradução avançadas.
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 45%

---

# jornada de tradução sem cabeçalho AEM {#aem-headless-translation-journey}

Comece aqui para obter uma jornada guiada por meio da tradução do conteúdo sem periféricos usando AEM ferramentas de tradução avançadas.

## Introdução {#introduction}

A implementação sem periféricos está se tornando cada vez mais importante para fornecer experiências ao seu público-alvo, onde quer que sejam e independentemente do canal, da região ou da localidade.

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa, e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em canais e em sua entrega entre canais. Ao usar AEM ferramentas de tradução avançadas, esses fragmentos reutilizáveis podem ser facilmente traduzidos e entregues ao seu público-alvo, onde quer que seja.

Este guia o conduz pelos tópicos mais importantes de tradução sem cabeçalho, de modo que, ao concluir, você:

* Ter uma visão geral do que é a entrega de conteúdo sem periféricos.
* Ter uma compreensão básica AEM recursos sem periféricos.
* Entenda AEM recursos de tradução e como eles estão relacionados ao conteúdo sem periféricos.
* Tenha a capacidade de começar a traduzir seu próprio conteúdo sem periféricos.

O objetivo é fornecer uma ampla compreensão da tecnologia sem interface, como a AEM serve conteúdo sem interface e como você pode traduzi-la. Se você não está familiarizado com nenhum desses tópicos, este é o seu lugar ideal para começar.

Se você já está familiarizado com AEM, sem cabeça e tradução, você pode já ter o conhecimento fundamental dessa jornada. Considere consultar nossa documentação técnica vinculada ao [seção recursos adicionais abaixo.](#additional-resources)

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como resolver casos de negócios sem periféricos com o AEM, [AEM Jornadas headless](/help/journey-headless/home.md) são onde começar.

## Público {#audience}

Essa jornada foi criada para o perfil de um especialista em tradução, geralmente chamado de Gerente de projetos de tradução. Essa jornada apresenta os requisitos, as etapas e a abordagem para traduzir o conteúdo sem periféricos em AEM. A jornada pode definir perfis adicionais com os quais o especialista em tradução deve interagir, mas o ponto de vista da jornada é o do especialista em tradução.

Essa jornada supõe que o leitor tenha experiência de tradução de conteúdo em um grande sistema CMS, mas não assume conhecimento de tecnologia ou AEM sem periféricos.

A seguir estão os perfis que interagem nessa jornada.

| Perfil | Descrição | Função na jornada |
|---|---|---|
| Especialista em tradução | Define qual conteúdo deve ser traduzido e gerencia esses fluxos de trabalho | Público-alvo desta jornada |
| Autor de conteúdo | Cria e gerencia conteúdo entregue sem cabeçalho | Os autores de conteúdo criam o conteúdo que o especialista em tradução deve traduzir. |
| Administrador | Gerencia as definições básicas e a configuração do AEM | O especialista em tradução trabalha com o administrador para fazer as alterações de configuração necessárias para a tradução, como a instalação de um conector de tradução. |
| Arquiteto de conteúdo | Analisa os requisitos dos dados que devem ser entregues sem periféricos e define a estrutura desses dados | Os especialistas em tradução trabalham com o arquiteto de conteúdo para definir a organização do conteúdo, para que ele possa ser facilmente traduzido. |

As informações nesta jornada podem ser úteis para todos os perfis, mas algumas informações podem ser supérfluas para determinadas funções. Fique atento para [jornadas futuras que abordarão funções adicionais.](/help/journey-documentation/home.md#journeys)

## A Jornada de tradução sem cabeçalho {#the-journey}

Muitos tópicos serão explorados nesta jornada. Os artigos a seguir fornecem conhecimento fundamental da tradução do conteúdo sem interface no AEM e vinculam a documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo em uma tradução sem cabeçalho no AEM, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada de tradução sem cabeçalho AEM | Este documento |
| 1 | [Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM](learn-about.md) | Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM tradução. |
| 2 | [Introdução à tradução do AEM headless](getting-started.md) | Saiba como organizar o conteúdo sem periféricos e como funcionam AEM ferramentas de tradução. |
| 3 | [Configurar o conector de tradução](configure-connector.md) | Saiba como conectar o AEM a um serviço de tradução. |
| 4 | [Configurar regras de tradução](translation-rules.md) | Saiba como definir regras de tradução para identificar o conteúdo a ser traduzido. |
| 5 | [Traduzir conteúdo](translate-content.md) | Use o conector e as regras de tradução para traduzir o conteúdo sem cabeçalho. |
| 6 | [Publicar conteúdo traduzido](publish-content.md) | Saiba como publicar seu conteúdo traduzido e atualizar a tradução quando o conteúdo subjacente for atualizado. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar a jornada de tradução sem cabeçalho do Adobe. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM](learn-about.md)

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema comercial fornecendo uma narrativa que o orienta por processos e recursos complexos e inter-relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade de negócios.

Como tais jornadas são projetadas para se sustentarem sozinhas. No entanto, alguns deles podem estar relacionados entre si. Confira estas jornadas adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [Jornada de criação headless](/help/journey-headless/author/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e aprenda a modelar o conteúdo em seu primeiro projeto headless.
* [Jornada de arquitetura headless](/help/journey-headless/architect/overview.md) - Comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como modelar o conteúdo para seu projeto.
* [Jornada de desenvolvedores headless do AEM](/help/journey-headless/developer/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e como aproveitá-las em seu primeiro projeto.
* [Documentação técnica do AEM ](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) - se você já tiver uma sólida compreensão das tecnologias headless e do AEM, poderá consultar diretamente os nossos documentos técnicos detalhados.
* [Tutoriais do AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - se você prefere aprender na prática e tem conhecimento técnico, utilize nossos tutoriais práticos organizados por API e estrutura, que exploram a criação e o uso de aplicativos incorporados no AEM Headless.
