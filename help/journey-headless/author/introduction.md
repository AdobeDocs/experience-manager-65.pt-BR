---
title: jornada do autor de conteúdo sem cabeçalho do AEM
description: Uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager e como criar conteúdo para o seu projeto.
index: true
hide: false
hidefromtoc: false
source-git-commit: 867b0a5a4c660a069e54094ed003cd93289048c7
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Criação para headless com AEM - uma introdução {#author-headless-introduction}

Nesta parte do [jornada do autor de conteúdo sem cabeçalho do AEM](overview.md), você pode aprender os conceitos e a terminologia (básica) necessários para entender a criação de conteúdo para entrega de conteúdo sem periféricos com o Adobe Experience Manager (AEM).

## Objetivo {#objective}

* **Público**: Iniciante
* **Objetivo**: Apresente os conceitos e a terminologia relevantes para a criação sem cabeçalho.

## Sistema de gerenciamento de conteúdo (CMS) {#content-management-system}

O que é um sistema de gerenciamento de conteúdo?

Um Sistema de Gerenciamento de Conteúdo (CMS) é exatamente o que diz ser - um sistema de computador usado para gerenciar conteúdo. Isso é um pouco geral, portanto, para ser mais preciso, ele é (normalmente) usado para gerenciar conteúdo que você deseja disponibilizar em seu(s) site(s).

## CMS sem periféricos {#headless-cms}

Headless é um termo usado para descrever sistemas que efetivamente desconectam o conteúdo da maneira de exibir esse conteúdo na Web.

Tradicionalmente, você gerenciava seu conteúdo em um CMS e o mesmo CMS seria responsável pela renderização desse conteúdo em suas páginas da Web.

Agora, sem periféricos significa que o conjunto de conteúdo pode ser gerenciado no CMS e, em seguida, acessado por um ou mais aplicativos (independentes).

Isso significa que seu conteúdo pode ser entregue a qualquer dispositivo, em uma grande variedade de formatos. Isso torna todo o processo muito mais flexível e também significa que você não precisa se preocupar com layout e formatação.

>[!NOTE]
>
>Se quiser saber mais sobre os detalhes técnicos do CMS sem periféricos, leia mais em Saiba mais sobre o desenvolvimento sem periféricos do CMS.

## Adobe Experience Manager {#aem-cms}

Então, o que é AEM?

Em primeiro lugar, AEM é um sistema de gerenciamento de conteúdo com uma grande variedade de recursos que também podem ser personalizados para atender às suas necessidades.

Isso significa que ele pode ser usado como um:

* CMS sem periféricos
   * Para ser headless, seu conteúdo pode ser criado como **Fragmentos de conteúdo**.
Esses são itens autônomos de conteúdo que podem ser acessados diretamente por uma variedade de aplicativos, pois têm uma estrutura predefinida, com base em **Modelos de fragmentos do conteúdo**.
Isso significa que o conteúdo pode atingir uma grande variedade de dispositivos, em uma grande variedade de formatos e com uma ampla seleção de funcionalidade.
(E como um whammy duplo, esses fragmentos também podem ser usados na construção de páginas AEM da Web, se desejar).

* CMS &quot;tradicional&quot;
   * O conteúdo é criado para páginas da Web, usando uma variedade de componentes que definem como o conteúdo será renderizado em seu site. Mesmo aqui AEM é extremamente flexível, pois a equipe de projeto pode desenvolver componentes personalizados.

## Modelagem de conteúdo {#content-modeling}

Portanto, a modelagem de conteúdo (também conhecida como modelagem de dados) é outro termo técnico - por que ela deve interessá-lo como autor?

Para que os aplicativos sem periféricos possam acessar seu conteúdo e fazer algo com ele, seu conteúdo precisa realmente ter uma estrutura predefinida. Seria possível ter seu conteúdo como de forma livre, mas isso faria vida *very* complicado para os aplicativos.

Basicamente, o processo de definição da estrutura para que o seu conteúdo adira ao envolve o design de um modelo, chamado de modelagem de dados.

Para AEM a função de Arquiteto de conteúdo (geralmente uma pessoa diferente), executará a modelagem de dados para projetar uma variedade de **Modelos de fragmentos do conteúdo** - que você usa como base para o seu conteúdo usando **Fragmentos de conteúdo**.

>[!NOTE]
>
>Se quiser saber mais sobre a modelagem de dados, leia mais na Jornada AEM Headless Content Architect .

## O que vem a seguir {#whats-next}

Agora que você aprendeu os conceitos e a terminologia, o próximo passo é [Saiba mais sobre as noções básicas da criação de Fragmentos de conteúdo](basics.md). Isso introduzirá a manipulação básica de AEM, além de como criar Fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* jornada do desenvolvedor sem periféricos do AEM
   * [Saiba mais sobre o desenvolvimento sem periféricos do CMS](/help/journey-headless/developer/learn-about.md)

* [jornada do AEM Headless Content Architect](/help/journey-headless/architect/overview.md)

* [jornada de tradução de conteúdo sem cabeçalho do AEM](/help/journey-headless/translation/overview.md)
