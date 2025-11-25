---
title: Console de componentes
description: O console Componentes permite navegar em todos os componentes definidos para a instância e visualizar as principais informações de cada componente.
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 43%

---

# Console de componentes{#components-console}

O console Componentes permite navegar em todos os componentes definidos para a instância e visualizar as principais informações de cada componente.

Ele pode ser acessado em **Ferramentas >** **Geral >** **Componentes**. No console, as visualizações em Cartão e Lista estão disponíveis. Como não há estrutura em árvore para componentes, a exibição em coluna não está disponível.

![captura de tela_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>O console Componentes mostra todos os componentes do sistema. O [Navegador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser) mostra componentes que estão disponíveis para autores e oculta todos os grupos de componentes que começam com um ponto final ( `.`).

## Pesquisar {#searching}

Com o ícone **Apenas conteúdo** (na parte superior esquerda), você pode abrir o painel **Pesquisar** para pesquisar e/ou filtrar os componentes: 

![captura de tela_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Detalhes do componente {#component-details}

Para exibir detalhes sobre um componente específico, clique no recurso desejado. Três guias fornecem:

* **Propriedades**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  Na guia Propriedades, é possível:

   * Veja as propriedades gerais do componente.
   * Visualizar como o [ícone ou abreviação foi definido](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) para o componente.

      * Clicar na origem do ícone levará você ao componente.

   * Exiba o **Tipo de Recurso** e o **Supertipo de Recurso** (se definido) do componente.

      * Clicar no Supertipo de recurso levará você a esse componente.

  >[!NOTE]
  >
  >Como `/apps` não pode ser editado no tempo de execução, o console Componentes fica somente leitura.

* **Políticas**

  ![Políticas](assets/chlimage_1-169.png)

* **Uso em tempo real**

  ![Uso em tempo real](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >Devido à natureza das informações coletadas para esta exibição, ela pode levar algum tempo para ser agrupada/exibida. 

* **Documentação**

  Se o desenvolvedor tiver fornecido a [documentação referente ao componente](/help/sites-developing/developing-components.md#documenting-your-component), ela aparecerá na guia **Documentação**. Se não houver documentação disponível, a guia **Documentação** não será exibida.

  ![Documentação](assets/chlimage_1-171.png)
