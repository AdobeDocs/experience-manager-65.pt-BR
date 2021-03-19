---
title: Experimentação de fragmentos de conteúdo no We.Retail
seo-title: Experimentação de fragmentos de conteúdo no We.Retail
description: Experimentação de fragmentos de conteúdo no We.Retail
seo-description: 'null'
uuid: 66daddfe-8e98-47b6-8499-db055887ac17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: d1326737-f378-46d0-9916-61ead4d31639
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 21%

---


# Tentando fragmentos de conteúdo no We.Retail{#trying-out-content-fragments-in-we-retail}

Os Fragmentos de conteúdo permitem criar conteúdo neutro ao canal, juntamente com variações (possivelmente específicas do canal). **We.Retail**  (conforme disponível em uma instância predefinida do AEM) fornece o fragmento Navegação no  **Ártico em** Lofotenas como uma amostra básica. Isto ilustra que:

* Os fragmentos de conteúdo do Adobe Experience Manager (AEM) são [criados e gerenciados como ativos independentes da página](/help/assets/content-fragments/content-fragments.md). Eles permitem criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). 

   * Consulte [Onde encontrar ativos de Fragmento de conteúdo no We.Retail](#where-to-find-content-fragments-in-we-retail)

* Em seguida, você pode [usar esses fragmentos e suas variações, ao criar](/help/sites-authoring/content-fragments.md) suas páginas de conteúdo.

   * Consulte [Onde fragmentos de conteúdo são usados no We.Retail](#where-content-fragments-are-used-in-we-retail)

Para obter a documentação completa sobre como criar, gerenciar, usar e desenvolver fragmentos de conteúdo:

* Consulte [Mais Informações](#further-information)

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-authoring/experience-fragments.md)** são recursos diferentes no AEM:
>
>* **Fragmentos de conteúdo** são conteúdos editoriais, principalmente texto e imagens relacionadas. Eles são puro conteúdo, sem design e layout.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.

>
>
Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.

## Onde encontrar fragmentos de conteúdo no We.Retail {#where-to-find-content-fragments-in-we-retail}

Há vários fragmentos de conteúdo de exemplo no We.Retail; navegue por **Assets**, **Arquivos**, **We.Retail**, **Inglês**, **Experiências**.

Isso inclui **Navegação Árctica no Lofoten**, um fragmento junto com os ativos visuais relacionados:

* Navegue pelo **Assets**, **Arquivos**, **We.Retail**, **Inglês**, **Experiências**, **Navegação Ártica no Lofoten**:

   * [http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten](http://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten)

![cf-44](assets/cf-44.png)

Você pode selecionar e editar o fragmento **Navegação Ártica no Lofoten**:

* [http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten](http://localhost:4502/editor.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten/arctic-surfing-in-lofoten)

Aqui você pode [editar e gerenciar](/help/assets/content-fragments/content-fragments.md) seu fragmento usando as guias (painel lateral esquerdo):

<!--![](do-not-localize/cf-45-aa.png) ![](do-not-localize/cf-45-a.png) ASSET does not exist-->

* **[](/help/assets/content-fragments/content-fragments-variations.md)** Variações, incluindo  [Marcação](/help/assets/content-fragments/content-fragments-markdown.md)
* **[Conteúdo associado](/help/assets/content-fragments/content-fragments-assoc-content.md)**
* **[Metadados](/help/assets/content-fragments/content-fragments-metadata.md)**

![cf-46](assets/cf-46.png)

## Onde os fragmentos de conteúdo são usados no We.Retail {#where-content-fragments-are-used-in-we-retail}

Para ilustrar [criação de página com um fragmento de conteúdo](/help/sites-authoring/content-fragments.md), há vários exemplos de páginas fornecidos em, por exemplo:

* [http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience](http://localhost:4502/sites.html/content/we-retail/language-masters/en/experience)

Por exemplo, o fragmento de conteúdo **Navegação no Ártico no Lofoten** é referenciado na página Sites :

* Navegue pelos **Sites**, **We.Retail**, **Mestres de Idioma**, **Inglês**, **Experiência**. Em seguida, abra **Navegação Ártica no Lofoten** para edição:

   * [http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html)

![cf-53](assets/cf-53.png)

## Informações adicionais {#further-information}

Para obter mais detalhes, consulte:

* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)

   * Saiba como criar, editar e gerenciar os ativos do Fragmento de conteúdo.

* [Criação de página com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md)

   * Use o Fragmento do conteúdo ao criar uma página.

* [Desenvolvimento de AEM - Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)

   * Uma visão geral dos componentes dos Fragmentos de conteúdo.

* [Desenvolvimento e extensão de fragmentos de conteúdo](/help/sites-developing/customizing-content-fragments.md)

   * Informações para ajudá-lo a desenvolver e estender Fragmentos de conteúdo.

