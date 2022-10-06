---
title: Jornada do arquiteto de conteúdo do AEM Headless
description: Uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como modelar o conteúdo para seu projeto.
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# Modelagem de conteúdo para headless com o AEM - uma introdução {#architect-headless-introduction}

Nesta parte do [jornada do AEM Headless Content Architect](overview.md), você pode aprender os conceitos e a terminologia (básica) necessários para entender a modelagem de conteúdo para entrega de conteúdo sem periféricos com o Adobe Experience Manager (AEM).

Este documento ajuda você a entender a entrega sem periféricos, como o AEM suporta periféricos e como o conteúdo é modelado para ficar sem periféricos. Depois de ler esse documento, você deverá:

* Entenda os conceitos básicos de entrega de conteúdo sem periféricos.
* Familiarize-se com o modo como o AEM suporta modelagem sem periféricos e de conteúdo.

## Objetivo {#objective}

* **Público**: Iniciante
* **Objetivo**: Apresente os conceitos e a terminologia relevantes para a Modelagem de conteúdo sem cabeçalho.

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

No entanto, a complexidade das dependências na pilha rapidamente se torna aparente, pois outros itens na pilha precisam ser ajustados para acomodar as alterações.

## A Cabeça em Sem Cabeça {#the-head}

O cabeçalho de qualquer sistema é geralmente o renderizador de saída desse sistema, normalmente na forma de uma GUI ou outro resultado gráfico.

Quando falamos de um CMS sem interface, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, apenas entregando a variável **conteúdo** de forma padronizada, um CMS sem periféricos omita a renderização final de output, deixando o **apresentação** do conteúdo para o serviço de consumo.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, um webshop, experiências móveis, aplicativos web progressivos (PWA), etc., absorvem conteúdo do CMS sem cabeçalho e fornecem sua própria renderização. Eles cuidam de fornecer suas próprias cabeças para o seu conteúdo.

Omitir a cabeça simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Modelagem de conteúdo {#content-modeling}

A modelagem de conteúdo (também conhecida como modelagem de dados) é sua especialidade, portanto, o que precisa ser considerado ao modelar para imutável?

Para que os aplicativos sem periféricos possam acessar seu conteúdo e fazer algo com ele, o conteúdo precisa realmente ter uma estrutura predefinida. Seria possível ter seu conteúdo como de forma livre, mas isso faria vida *very* complicado para os aplicativos.

Para AEM você, como um Arquiteto de conteúdo, executará a modelagem de conteúdo para projetar uma variedade de **Modelos de fragmentos do conteúdo**. Eles definem a estrutura usada quando os autores de conteúdo criam a variável **Fragmentos de conteúdo** que contêm o conteúdo.

### Acesso ao conteúdo {#access-content}

Isso é mais um detalhe de desenvolvimento - mas pode lhe interessar, apenas para concluir a história.

Depois de criar os Modelos de fragmento de conteúdo, e seus autores os usaram para gerar o conteúdo, os aplicativos sem cabeçalho precisarão acessar esse conteúdo.

A Adobe Experience Manager (AEM) pode acessar seletivamente seus Fragmentos de conteúdo usando a API GraphQL AEM, para retornar somente o conteúdo necessário. Usando a API, um desenvolvedor pode formular consultas que selecionam conteúdo específico. Esse processo de seleção é baseado em *your* Modelos de fragmentos do conteúdo.

Isso significa que seu projeto pode realizar a entrega sem interface de conteúdo estruturado para uso em seus aplicativos.

## O que vem a seguir {#whats-next}

Agora que você aprendeu os conceitos e a terminologia, o próximo passo é [Saiba mais sobre as noções básicas de modelagem com Modelos de fragmentos de conteúdo](basics.md).

## Recursos adicionais {#additional-resources}

* jornada do desenvolvedor sem periféricos do AEM
   * [Saiba mais sobre o desenvolvimento sem periféricos do CMS](/help/journey-headless/developer/learn-about.md)
   * [Saiba como modelar seu conteúdo](/help/journey-headless/developer/model-your-content.md)
