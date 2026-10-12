---
title: Saiba mais sobre como usar referências em Fragmentos de conteúdo
description: Saiba mais sobre como usar referências em Fragmentos de conteúdo para conteúdo, outros fragmentos e outros ativos (mídia). Apresente a necessidade e a mecânica de fragmentos aninhados para a criação de CMS headless.
exl-id: d54a0a40-a8af-456a-9bf5-219d84540c97
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer, User, Leader
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 85%
---
# Saiba mais sobre como usar referências em Fragmentos de conteúdo {#author-headless-references}

## A história até agora {#story-so-far}

No início da [Jornada do autor de conteúdo headless do AEM](overview.md), a [Introdução](introduction.md) abordou os conceitos básicos e a terminologia relevante para a criação de conteúdo headless.

Você aprendeu os fundamentos da criação de CMS headless, com uma introdução à autoria com AEMaaCS e, em particular, à autoria de Fragmentos de conteúdo.

Este artigo se baseia nesses itens para que você entenda como usar referências para criar seu próprio conteúdo para seu projeto headless do AEM.

## Objetivo {#objective}

* **Público-alvo**: avançado
* **Objetivo**: introduzir o uso de referências para a Criação de CMS headless. Que tipos de referências estão disponíveis e quais são seus objetivos:

  * Referências do conteúdo
  * Referências de ativo/mídia
  * Referências de fragmento
  * Referências ad hoc de dentro de um bloco de texto

## O que são referências {#what-are-references}

As referências são simplesmente um mecanismo para conectar seus recursos, seja outro conteúdo, ativos (como em imagens) ou outros fragmentos. Embora muito parecidas, há algumas diferenças.

Algumas referências têm tipos de dados dedicados (por exemplo, Referências de conteúdo e Referências de fragmento), enquanto outras são simplesmente adicionadas como referência em um bloco de texto (referências de ativos e referências ad hoc).

![Fragmentos de conteúdo: referências](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Referências de conteúdo {#content-references}

As Referências de conteúdo fazem exatamente isso - elas permitem fazer referência a qualquer outro conteúdo. Isso abre um navegador que permite selecionar o item de conteúdo.

## Referências de ativo/mídia {#assets-media-references}

Os ativos (por exemplo, imagens ou mídia) podem ser referenciados em um bloco de texto usando a opção **Inserir ativo**. Isso abre um navegador que permite selecionar o ativo.

![Fragmentos de conteúdo: inserir ativo](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Referências de fragmento {#fragment-references}

Novamente, as Referências de fragmento fazem exatamente isso - elas permitem fazer referência a outro fragmento. Por ser relevante, precisa de um pouco mais de explicação.

Por exemplo, você pode ter os seguintes modelos de fragmento de conteúdo definidos:

* Cidade
* Empresa
* Pessoa
* Prêmios

Parece bastante simples, mas uma Empresa tem um CEO e Funcionários... e todas essas são pessoas, cada uma definida como uma Pessoa.

E uma pessoa pode ter um prêmio (ou talvez dois).

* Minha empresa - Empresa
  * CEO - Pessoa
  * Funcionário(s) - Pessoa
    * Prêmios pessoais - Prêmio

E isso é só para começar. Dependendo da complexidade, um prêmio pode ser específico da empresa ou uma empresa pode ter seu escritório principal em uma cidade específica.

A representação dessas inter-relações pode ser alcançada com as Referências de fragmento, já que são entendidas por você (o autor) e pelos aplicativos headless.

Como autor, você não é responsável por definir esses relacionamentos (isso é feito pelo Arquiteto de conteúdo ao criar o Modelo de fragmento de conteúdo), mas precisa saber como reconhecer e editar as referências.

### Como criar fragmentos aninhados {#author-nested-fragment}

A criação de referências de fragmento é bastante direta (embora o campo geralmente não seja rotulado como **Referência de fragmento**). Você pode digitar a referência diretamente ou (mais provavelmente) selecionar o ícone de pasta para abrir um navegador que permita navegar e selecionar o fragmento necessário.

![Fragmentos de conteúdo: referências](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

A definição do Modelo de fragmento de conteúdo controla:

* se você pode optar por adicionar várias referências
* os tipos de modelo de Fragmentos de conteúdo que você pode selecionar; o Modelo de fragmento de conteúdo define os modelos de fragmento permitidos para a referência, de modo que o AEM apresenta apenas fragmentos com base nesses modelos.

### Como navegar pelos fragmentos aninhados {#navigate-nested-fragment}

Com a utilização da guia **Árvore da estrutura** do Editor de fragmento de conteúdo, é possível navegar pelos fragmentos referenciados pelo fragmento e, em seguida, por meio de quaisquer referências que eles possam conter. Selecionar uma referência abre esse fragmento para edição.

>[!NOTE]
>
>Com a utilização da navegação estrutural no painel principal, é possível navegar de volta ao ponto inicial.

![Árvore de estrutura do fragmento de conteúdo](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Referências ad hoc {#adhoc-references}

Referências ad hoc podem ser adicionadas como um link simples dentro de um bloco de texto:

![Fragmentos de conteúdo: referências ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## O que vem a seguir {#whats-next}

Agora que você aprendeu sobre referências e estrutura nos Fragmentos de conteúdo, a próxima etapa é [Saber mais sobre metadados e marcação](metadata-tagging.md). Isso apresentará e discutirá como você pode definir metadados e tags para os Fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* [Trabalho com Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)

  * [Gerenciamento dos Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-managing.md)

    * [Aplique a configuração à sua pasta de ativos](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

    * [Criação de um Fragmento de conteúdo](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

  * [Variações: criação de Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-variations.md)

  * [Modelos de fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-models.md)

    * [Modelos de fragmento de conteúdo - Tipos de dados](/help/assets/content-fragments/content-fragments-models.md#data-types)

    * [Modelos de fragmento de conteúdo: propriedades](/help/assets/content-fragments/content-fragments-models.md#properties)

* Guias de introdução
  * [Criação de um guia de início rápido do Assets Folder Headless](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Jornada do arquiteto de conteúdo do AEM Headless](/help/journey-headless/architect/overview.md)

* [Jornada de tradução headless do AEM](/help/journey-headless/translation/overview.md)
