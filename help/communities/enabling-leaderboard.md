---
title: Recurso de quadro de líderes
seo-title: Leaderboard Feature
description: Adicionar um componente de Quadro de líderes a uma página
seo-description: Adding a Leaderboard component to a page
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 10%

---

# Recurso de quadro de líderes {#leaderboard-feature}

## Introdução {#introduction}

O `Leaderboard` fornece a capacidade de obter uma noção de como os membros estão interagindo dentro da comunidade por meio da classificação de membros de acordo com os pontos obtidos (pontuação básica) ou seu conhecimento (pontuação avançada).

Antes de incluir o componente de quadro de liderança em uma página, é necessário configurar [Pontuação e emblemas de comunidades](/help/communities/implementing-scoring.md).

Esta seção da documentação descreve:

* Adicionar a `Leaderboard` para um [site da comunidade](/help/communities/overview.md#community-sites).
* Configurações para o `Leaderboard` componente.

### Adicionar um Quadro de líderes a uma página {#adding-a-leaderboard-to-a-page}

Para adicionar uma `Leaderboard` para uma página no modo autor, localize o componente

* `Communities / Leaderboard`

e arraste-a para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![quadro de líderes](assets/leaderboard.png)

### Configuração do Quadro de Liderança {#configuring-leaderboard}

Selecione o `Leaderboard` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![configure-lead board](assets/configure-leaderboard.png)

#### Guia Configurações {#settings-tab}

Em **[!UICONTROL Configurações]** , especifique quais informações relacionadas ao membro são exibidas :

* **Nome para exibição**

   Um nome descritivo a ser exibido para o quadro, refletindo as regras selecionadas para a exibição de emblemas e pontuações.
O padrão é `Leaderboard`, se nada tiver sido inserido.

* **Insígnia**

   Se marcada, uma coluna para ícones de selo é incluída no quadro de líderes.
O padrão está desmarcado.

* **Nome da insígnia**

   Se marcada, uma coluna para o nome do símbolo é incluída no quadro de líderes.
O padrão está desmarcado.

* **Usar Avatar**

   Se marcada, a imagem de avatar do membro é incluída no quadro de líderes, ao lado de seu link de nome para seu perfil de membro.
O padrão está desmarcado.

#### Guia Regras {#rules-tab}

Em **Regras** guia, o site da comunidade e suas regras de pontuação e marcação

* **Local da regra**

   (Obrigatório) Local onde a regra de Pontuação / Aviso é configurada.

* **Regra de pontuação**

   (Obrigatório) Regra específica que gera as pontuações a serem exibidas.

* **Regra para insígnias**

   (Obrigatório) Regra específica que gera o símbolo a ser exibido.

* **Limite de exibição**

   Número de membros a serem exibidos por página.O padrão é 10.

### Exemplo: Quadro de líderes dos participantes {#example-participants-leaderboard}

Este relatório do painel de líderes resulta da aplicação de regras básicas de pontuação.

Configuração do componente do Quadro de líderes:

* Guia Configurações :

   * Nome para exibição = `Participation Board`
   * `checked`:

      * Insígnia
      * Nome da insígnia
      * Usar Avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regra para insígnias = `/libs/settings/community/badging/rules//reference-badging`
   * Limite de exibição = `10`

![painel de líderes dos participantes](assets/participants-leaderboard.png)

### Exemplo: Quadro de líderes de especialistas {#example-experts-leaderboard}

Esse relatório de painel resulta da aplicação de regras de pontuação avançadas.

Configuração do componente do Quadro de líderes:

* Guia Configurações :

   * Nome para exibição = `Expertise Board`
   * `checked`:

      * Insígnia
      * Usar Avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regra para insígnias = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite de exibição = `10`

![conselho de administração de peritos](assets/experts-leaderboard.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Princípios básicos do painel de líderes](/help/communities/leaderboard.md) página para desenvolvedores.

As instruções para a criação de regras são fornecidas no [Pontuação e emblemas de comunidades](/help/communities/implementing-scoring.md) página para administradores.
