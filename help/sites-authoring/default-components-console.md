---
title: Console de componentes
seo-title: Console de componentes
description: 'null'
seo-description: 'null'
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# Console de componentes{#components-console}

O console Componentes permite navegar em todos os componentes definidos para a sua instância e exibir as principais informações de cada componente. 

It can be accessed from **Tools ->** **General ->** **Components**. No console, as visualizações de cartão e de lista estão disponíveis. Como não há uma estrutura de árvore para componentes, a visualização de coluna não está disponível.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>O console Componentes mostra todos os componentes do sistema. O [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) mostra componentes que estão disponíveis para autores e oculta todos os grupos de componentes que começam com um ponto final ( `.`).

## Pesquisar {#searching}

Com o ícone **Apenas conteúdo** (na parte superior esquerda), você pode abrir o painel **Pesquisar** para pesquisar e/ou filtrar os componentes: 

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Detalhes do componente {#component-details}

Para exibir detalhes sobre um componente específico, toque/clique no recurso desejado. As três guias fornecem:

* **Propriedades**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   Na guia Propriedades, é possível:

   * Veja as propriedades gerais do componente.
   * Visualizar como o [ícone ou a abreviação foi definida](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) para o componente.

      * Clicar na origem do ícone levará você até esse componente.
   * Visualizar o **Tipo de recurso** e o **Supertipo do recurso** (se definido) para o componente.

      * Clicar no Supertipo do recurso levará você até esse componente.
   >[!NOTE]
   >
   >Because `/apps` is not editable at runtime, the Components Console is read-only.

* **Políticas**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **Uso em tempo real**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >Devido à natureza das informações coletadas para esta exibição, ela pode levar algum tempo para ser agrupada/exibida. 

* **Documentação**

   Se o desenvolvedor tiver fornecido a [documentação referente ao componente](/help/sites-developing/developing-components.md#documenting-your-component), ela aparecerá na guia **Documentação**. Se não houver documentação disponível, a guia **Documentação** não será exibida.

   ![chlimage_1-171](assets/chlimage_1-171.png)

