---
title: jornada de tradução sem cabeçalho AEM
description: Comece aqui para obter uma jornada guiada por meio da tradução do conteúdo sem periféricos usando AEM ferramentas de tradução avançadas.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 2%

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

## jornadas de documentação de AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/home.md) une vários tópicos e recursos diferentes e talvez complicados ao fornecer uma narrativa que ajude o leitor, que pode ser novo a AEM, compreender e resolver um problema de negócios do início ao fim, assumindo o mínimo de tópico ou conhecimento AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa Adobe, experiência comprovada de implementação de consultores de Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como resolver casos de negócios sem periféricos com o AEM, [AEM Jornadas headless](/help/journey-headless/home.md) são onde começar.

## Público {#audience}

Essa jornada foi projetada para o perfil especialista em tradução, geralmente chamado de Gerenciador de projetos de tradução ou TPM. Essa jornada apresenta os requisitos, as etapas e a abordagem para traduzir o conteúdo sem periféricos em AEM. A jornada pode definir personas adicionais com as quais o especialista de tradução deve interagir, mas o ponto de vista da jornada é o do especialista de tradução.

Essa jornada supõe que o leitor tenha experiência de tradução de conteúdo em um grande sistema CMS, mas não assume conhecimento de tecnologia ou AEM sem periféricos.

A seguir estão as personas que interagem nessa jornada.

| Persona | Descrição | Função no Jornada |
|---|---|---|
| Especialista em tradução | Define qual conteúdo deve ser traduzido e gerencia esses workflows | Público-alvo desta jornada |
| Autor do conteúdo | Cria e gerencia conteúdo entregue sem cabeçalho | Os Autores de conteúdo criam conteúdo que o especialista de tradução deve traduzir. |
| Administrador | Gerencia a configuração básica e a configuração do AEM | O especialista em tradução trabalha com o administrador para fazer as alterações de configuração necessárias para a tradução, como instalar um conector de tradução. |
| Arquitetura de conteúdo | Analisa os requisitos dos dados que devem ser entregues sem periféricos e define a estrutura desses dados | Especialistas em tradução trabalham com o arquiteto de conteúdo para definir a organização do conteúdo, para que ele possa ser facilmente traduzido. |

As informações nesta jornada podem, é claro, ser úteis para todas as pessoas, mas algumas informações podem ser supérfluas para determinadas funções. Fique ligado para [jornadas futuras que abordarão funções adicionais.](/help/journey-documentation/home.md#journeys)

## A Jornada de tradução sem cabeçalho {#the-journey}

Você explorará muitos tópicos nesta jornada. Os artigos a seguir fornecem conhecimento fundamental da tradução do conteúdo sem interface no AEM e vinculam a documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo em uma tradução sem cabeçalho no AEM, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada de tradução sem cabeçalho AEM | Este documento |
| 1 | [Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM](learn-about.md) | Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM tradução. |
| 2 | [Introdução a AEM tradução headless](getting-started.md) | Saiba como organizar o conteúdo sem periféricos e como funcionam AEM ferramentas de tradução. |
| 3 | [Configurar o conector de tradução](configure-connector.md) | Saiba como conectar AEM a um serviço de tradução. |
| 4 | [Configurar regras de tradução](translation-rules.md) | Saiba como definir regras de tradução para identificar o conteúdo para tradução. |
| 5 | [Traduzir conteúdo](translate-content.md) | Use o conector e as regras de tradução para traduzir o conteúdo sem cabeçalho. |
| 6 | [Publicar conteúdo traduzido](publish-content.md) | Saiba como publicar seu conteúdo traduzido e atualizar a tradução quando o conteúdo subjacente for atualizado. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar a jornada de tradução sem cabeçalho do Adobe. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM](learn-about.md)

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema comercial fornecendo uma narrativa que o orienta por processos e recursos complexos e inter-relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade de negócios.

Como tais jornadas são projetadas para se sustentarem sozinhas. No entanto, alguns deles podem estar relacionados entre si. Confira estas jornadas adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [Jornada de criação sem cabeçalho](/help/journey-headless/author/overview.md) - Comece aqui para obter uma jornada guiada por meio dos recursos avançados e flexíveis sem interface de AEM, seus recursos e como modelar seu conteúdo em seu primeiro projeto sem interface.
* [Jornada de arquitetura headless](/help/journey-headless/architect/overview.md) - Comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como modelar o conteúdo para seu projeto.
* [jornada do desenvolvedor sem periféricos do AEM](/help/journey-headless/developer/overview.md) - Comece aqui para obter uma jornada guiada com os recursos avançados e flexíveis do AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento.
* [Documentação técnica AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR) - Se você já tiver um conhecimento profundo das tecnologias AEM e sem interface, poderá consultar diretamente nossos documentos técnicos aprofundados.
* [Tutoriais AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Se você preferir aprender fazendo e for tecnicamente inclinado, utilize nossos tutoriais práticos organizados por API e framework, que exploram a criação e o uso de aplicativos criados AEM Headless.
