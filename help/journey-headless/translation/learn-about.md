---
title: Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM
description: Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM tradução.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---

# Saiba mais sobre o conteúdo sem periféricos e como traduzi-lo em AEM {#learn-about}

Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM tradução.

## Objetivo {#objective}

Este documento ajuda você a entender a entrega de conteúdo sem periféricos, como o AEM é compatível e como esse conteúdo pode ser traduzido. Depois de ler, você deve:

* Entenda os conceitos básicos de entrega de conteúdo sem periféricos.
* Familiarize-se com o modo como o AEM suporta headless e tradução.

## Entrega de conteúdo em pilha completa {#full-stack}

Desde o aumento dos sistemas de gerenciamento de conteúdo (CMSs) fáceis de usar e em larga escala, as organizações os aproveitaram como um local central para gerenciar mensagens, identidade visual e comunicações. Usar o CMS como ponto central para administrar experiências melhorou a eficiência, eliminando a necessidade de duplicar tarefas em sistemas diferentes.

![O CMS clássico de pilha completa](/help/journey-headless/developer/assets/full-stack.png)

Em um CMS de pilha completa, toda a funcionalidade de manipulação de conteúdo está no CMS. Os recursos do sistema constituem componentes diferentes da pilha do CMS. A solução de pilha completa tem muitas vantagens.

* Há um sistema para manter.
* O conteúdo é gerenciado centralmente.
* Todos os serviços do sistema estão integrados.
* A criação de conteúdo é contínua.

Portanto, se um novo canal precisar ser adicionado ou se o suporte para novos tipos de experiências for necessário, um (ou mais) novo componente poderá ser inserido na pilha e só há um lugar para fazer alterações.

![Adicionar um novo canal à pilha](/help/journey-headless/developer/assets/adding-channel.png)

No entanto, a complexidade das dependências na pilha torna-se rapidamente aparente, pois outros itens na pilha precisam ser ajustados para acomodar as alterações.

## A Cabeça em Sem Cabeça {#the-head}

O cabeçalho de qualquer sistema é geralmente o renderizador de saída desse sistema, normalmente na forma de uma GUI ou outro resultado gráfico.

Quando falamos de um CMS sem interface, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, apenas entregando a variável **conteúdo** de forma padronizada, um CMS sem periféricos omita a renderização final de output, deixando o **apresentação** do conteúdo para o serviço de consumo.

![CMS sem periféricos](/help/journey-headless/developer/assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, uma loja da Web, experiências móveis, aplicativos da Web progressivos (PWA), etc., absorvem conteúdo do CMS sem periféricos e fornecem sua própria renderização. Eles cuidam de fornecer suas próprias cabeças para o seu conteúdo.

Omitir a cabeça simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Tradução do conteúdo sem cabeçalho no AEM {#translating-in-aem}

Além de oferecer ferramentas robustas para criar, gerenciar e fornecer páginas da Web tradicionais em pilha completa, o AEM também oferece a capacidade de criar seleções independentes de conteúdo e disponibilizá-las sem interrupções.

O poder do AEM permite que ele forneça conteúdo sem interface, em pilha completa ou em ambos os modelos ao mesmo tempo. Para o especialista em tradução, o mesmo conjunto de ferramentas de tradução pode ser aplicado a ambos os tipos de conteúdo, fornecendo uma abordagem unificada para a tradução do conteúdo.

Além disso, na jornada, você aprenderá os detalhes sobre como o AEM traduz o conteúdo, mas em um alto nível, o conceito é simples:

1. Defina uma conexão com um serviço de tradução configurando a estrutura de integração de tradução.
1. Defina qual conteúdo deve ser traduzido usando as regras de tradução.
1. Crie um projeto de tradução para colher o conteúdo, enviá-lo para o serviço de tradução e receber os resultados.
1. Revise e publique o conteúdo traduzido.

## O que vem a seguir {#what-is-next}

Obrigado por começar a sua jornada de tradução AEM sem cabeça! Agora que você leu este documento, deve:

* Entenda os conceitos básicos de entrega de conteúdo sem periféricos.
* Familiarize-se com o modo como o AEM suporta headless e tradução.

Aproveite esse conhecimento e prossiga com sua jornada de tradução sem periféricos de AEM ao próximo revisar o documento [Introdução a AEM tradução headless](getting-started.md) onde você terá uma visão geral de como o AEM gerencia o conteúdo sem periféricos e conhecerá suas ferramentas de tradução.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução sem periféricos revisando o documento [Comece com AEM tradução sem periféricos,](getting-started.md) a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada sem periféricos.

* [MSM e tradução](/help/sites-administering/msm-and-translation.md) - Os detalhes do AEM Multi-Site Manager e como ele funciona com suas ferramentas de tradução
