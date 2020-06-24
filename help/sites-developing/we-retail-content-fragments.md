---
title: Experimentar fragmentos de conteúdo no We.Retail
seo-title: Experimentar fragmentos de conteúdo no We.Retail
description: 'null'
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 759d2dd8d12861757bf7f54b77d8d3ca170887fe
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 21%

---


# Experimentar fragmentos de conteúdo no We.Retail{#trying-out-content-fragments-in-we-retail}

Fragmentos de conteúdo permitem criar conteúdo neutro ao canal, juntamente com variações (possivelmente específicas ao canal). **We.Retail** (conforme disponível em uma instância predefinida do AEM) fornece o fragmento Surfing no **Ártico em Lofoten** como uma amostra básica. Isto ilustra que:

* Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são [criados e gerenciados como ativos independentes da página](/help/assets/content-fragments/content-fragments.md). Eles permitem criar um conteúdo neutro ao canal, juntamente com variações (possivelmente, específicas do canal).

   * Consulte [Onde localizar ativos de fragmento de conteúdo no We.Retail](#where-to-find-content-fragments-in-we-retail)

* You can then [use these fragments, and their variations, when authoring](/help/sites-authoring/content-fragments.md) your content pages.

   * Ver [onde os fragmentos de conteúdo são usados no We.Retail](#where-content-fragments-are-used-in-we-retail)

Para obter a documentação completa sobre como criar, gerenciar, usar e desenvolver fragmentos de conteúdo:

* Ver [Mais Informações](#further-information)

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)**são recursos diferentes no AEM:
>
>* **Fragmentos de conteúdo** são conteúdos editoriais, principalmente texto e imagens relacionadas. Eles são puro conteúdo, sem design e layout.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.

>
>
Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.

## Onde encontrar fragmentos de conteúdo no We.Retail {#where-to-find-content-fragments-in-we-retail}

Há vários fragmentos de conteúdo de amostra no We.Retail; navegue por **Assets**, **Files**, **We.Retail**, **English**, **Experiences**.

Estes incluem o Surfing **Ártico em Lofoten**, um fragmento junto com os ativos visuais relacionados:

* Navegue pelos **Assets**, **Files**, **We.Retail**, **English**, **Experiences******, Artic Surfing in Lofoten:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Você pode selecionar e editar o fragmento Surfing no **Ártico no Lofoten** :

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Aqui, você pode [editar e gerenciar](/help/assets/content-fragments/content-fragments.md) o fragmento usando as guias (painel do lado esquerdo):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[Variações](/help/assets/content-fragments/content-fragments-variations.md)**incluindo[marcação](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadados](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Onde os fragmentos de conteúdo são usados no We.Retail {#where-content-fragments-are-used-in-we-retail}

Para ilustrar a criação de [página com um fragmento](/help/sites-authoring/content-fragments.md) de conteúdo, há vários exemplos de páginas fornecidos em, por exemplo:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Por exemplo, o fragmento de conteúdo Navegação **Ártico no Lofoten** é referenciado na página Sites:

* Navegue pelos **Sites**, **We.Retail**, **Language Masters**, **Inglês**, **Experiência**. Em seguida, abra o **Ártico Surfing no Lofoten** para edição:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Informações adicionais {#further-information}

Para obter mais detalhes, consulte:

* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)

   * Saiba como criar, editar e gerenciar seus ativos de Fragmento de conteúdo.

* [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md)

   * Use seu Fragmento de conteúdo ao criar uma página.

* [Desenvolvimento do AEM - Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)

   * Uma visão geral dos componentes dos Fragmentos de conteúdo.

* [Desenvolvimento e extensão de fragmentos de conteúdo](/help/sites-developing/customizing-content-fragments.md)

   * Informações que ajudam a desenvolver e estender Fragmentos de conteúdo.

