---
title: Saiba mais sobre o conteúdo headless e como traduzi-lo no AEM
description: Aprenda conceitos headless, como eles são mapeados no AEM e a teoria de tradução do AEM.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 100%

---

# Saiba mais sobre o conteúdo headless e como traduzi-lo no AEM {#learn-about}

Aprenda conceitos headless, como eles são mapeados no AEM e a teoria de tradução do AEM.

## Objetivo {#objective}

Este documento ajuda você a entender a entrega de conteúdo headless, como o AEM é compatível com a tecnologia headless e como esse conteúdo pode ser traduzido. Depois de ler esse documento, você deverá:

* Entender os conceitos básicos de entrega de conteúdo headless.
* Estar familiarizado com como o AEM dá suporte a headless e tradução.

## Entregar conteúdo em pilha completa {#full-stack}

Desde o aumento dos sistemas de gerenciamento de conteúdo (CMSs) fáceis de usar e em larga escala, as organizações os estão aproveitando como um local central para gerenciar mensagens, identidade visual e comunicações. Usar o CMS como ponto central para administrar experiências melhorou a eficiência, eliminando a necessidade de duplicar tarefas em sistemas diferentes.

![O CMS clássico de pilha completa](/help/journey-headless/developer/assets/full-stack.png)

Em um CMS de pilha completa, toda a funcionalidade de manipulação de conteúdo está no CMS. Os recursos do sistema constituem componentes diferentes da pilha do CMS. A solução de pilha completa tem muitas vantagens.

* Há um sistema para manter.
* O conteúdo é gerenciado centralmente.
* Todos os serviços do sistema estão integrados.
* A criação de conteúdo é contínua.

Portanto, se um novo canal precisar ser adicionado ou for necessário oferecer suporte a novos tipos de experiências, um novo componente (ou mais) pode ser inserido na pilha e as alterações podem ser feitas em um único local.

![Adicionar um novo canal à pilha](/help/journey-headless/developer/assets/adding-channel.png)

No entanto, a complexidade das dependências na pilha torna-se rapidamente aparente, pois outros itens na pilha precisam ser ajustados para acomodar as alterações.

## A interface no headless {#the-head}

A interface de qualquer sistema é geralmente o renderizador de saída, normalmente na forma de uma GUI ou outra saída gráfica.

Quando falamos de um CMS headless, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, apenas entregando o **conteúdo** de forma padronizada, um CMS headless omite a renderização final de saída, deixando a **apresentação** do conteúdo para o serviço de consumo.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, uma loja virtual, experiências móveis, aplicativos Web progressivos (PWAs) etc., absorvem conteúdo do CMS headless e fornecem sua própria renderização. Eles fornecem suas próprias interfaces para o conteúdo.

Omitir a interface simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Tradução de conteúdo headless no AEM {#translating-in-aem}

Além de oferecer ferramentas robustas para criar, gerenciar e fornecer páginas da Web tradicionais em pilha completa, o AEM também oferece a capacidade de criar seleções independentes de conteúdo e disponibilizá-las de forma headless.

O poder do AEM permite que ele forneça conteúdo headless, em pilha completa ou em ambos os modelos ao mesmo tempo. Para o especialista em tradução, o mesmo conjunto de ferramentas de tradução pode ser aplicado a ambos os tipos de conteúdo, fornecendo uma abordagem unificada para a tradução do conteúdo.

Além disso, na jornada, você conhecerá os detalhes sobre como o AEM traduz o conteúdo, mas em alto nível. O conceito é simples:

1. Definir uma conexão com um serviço de tradução, configurando a estrutura de integração de tradução.
1. Definir qual conteúdo deve ser traduzido usando as regras de tradução.
1. Criar um projeto de tradução para coletar o conteúdo, enviá-lo para o serviço de tradução e receber os resultados.
1. Revisar e publicar o conteúdo traduzido.

## O que vem a seguir {#what-is-next}

Agradecemos por você ter iniciado a jornada de tradução headless do AEM. Agora que leu este documento, você deve:

* Entender os conceitos básicos de entrega de conteúdo headless.
* Estar familiarizado com como o AEM dá suporte a headless e tradução.

Desenvolver esse conhecimento e continuar sua jornada de tradução headless do AEM revisando o documento [Introdução à tradução headless do AEM](getting-started.md), por meio da qual você terá uma visão geral de como o AEM gerencia conteúdo e conhecerá suas ferramentas de tradução.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de tradução headless revisando o documento [Introdução à tradução headless do AEM](getting-started.md), veja a seguir alguns recursos opcionais adicionais que fazem uma análise mais profunda de alguns conceitos mencionados neste documento, mas não são necessários para continuar na jornada headless.

* [MSM e tradução](/help/sites-administering/msm-and-translation.md) - os detalhes do Gerenciamento de vários sites do AEM e como ele trabalha com ferramentas de tradução
