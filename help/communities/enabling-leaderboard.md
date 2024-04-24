---
title: Recurso de quadro de classificação
description: Saiba como o componente de Quadro de classificação permite ver como os membros interagem na comunidade, classificando os membros com base em pontos ganhos e experiência.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 8b4d56d9-ba73-4eda-9773-3daaa9237abe
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 2%

---

# Recurso de quadro de classificação {#leaderboard-feature}

## Introdução {#introduction}

A variável `Leaderboard` o componente ajuda você a ter uma ideia de como os membros estão interagindo na comunidade, classificando-os de acordo com os pontos ganhos (pontuação básica) ou sua experiência (pontuação avançada).

Antes de incluir o componente de quadro de classificação em uma página, é necessário configurar [Pontuação e medalhas das comunidades](/help/communities/implementing-scoring.md).

Esta seção da documentação descreve:

* Adicionar o `Leaderboard` componente a um [site da comunidade](/help/communities/overview.md#community-sites).
* Definições de configuração para o `Leaderboard` componente.

### Adicionar um quadro de classificação a uma página {#adding-a-leaderboard-to-a-page}

Para adicionar um `Leaderboard` para uma página no modo de autor, localize o componente

* `Communities / Leaderboard`

E arraste-o para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![placar de líderes](assets/leaderboard.png)

### Configurar quadro de classificação {#configuring-leaderboard}

Selecione o colocado `Leaderboard` para que você possa acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![configure-leaderboard](assets/configure-leaderboard.png)

#### Guia Configurações {#settings-tab}

No **[!UICONTROL Configurações]** especifique quais informações relacionadas ao membro são exibidas:

* **Nome de exibição**

  Um nome descritivo a ser exibido para o quadro, refletindo as regras selecionadas para exibir selos e pontuações.
O padrão é `Leaderboard` se nada for inserido.

* **Medalha**

  Se marcada, uma coluna para ícones de selo é incluída no quadro de classificação.
O padrão está desmarcado.

* **Nome da insígnia**

  Se marcada, uma coluna para o nome do selo é incluída no quadro de classificação.
O padrão está desmarcado.

* **Usar Avatar**

  Se marcada, a imagem do avatar do membro é incluída no quadro de classificação, ao lado do link de nome para o perfil do membro.
O padrão está desmarcado.

#### Guia Regras {#rules-tab}

No **Regras** , o site da comunidade e suas regras de pontuação e criação de símbolos

* **Local da regra**

  (Obrigatório) Local onde a regra de Pontuação/Inscrição está configurada.

* **Regra de pontuação**

  (Obrigatório) Regra específica que gera as pontuações a serem exibidas.

* **Regra de insígnia**

  (Obrigatório) Regra específica que gera o símbolo a ser exibido.

* **Limite de exibição**

  Número de membros a serem exibidos por página. O padrão é 10.

### Exemplo: Quadro de classificação de participantes {#example-participants-leaderboard}

Esse quadro de classificação relata os resultados da aplicação das regras básicas de pontuação.

Configuração do componente de quadro de classificação:

* Guia Configurações:

   * Nome de exibição = `Participation Board`
   * `checked`:

      * Insígnia
      * Nome da insígnia
      * Usar Avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regra de insígnia = `/libs/settings/community/badging/rules//reference-badging`
   * Limite de exibição = `10`

![participantes-quadro de classificação](assets/participants-leaderboard.png)

### Exemplo: Quadro de classificação de especialistas {#example-experts-leaderboard}

Este quadro de classificação relata os resultados da aplicação de regras de pontuação avançadas.

Configuração do componente de quadro de classificação:

* Guia Configurações:

   * Nome de exibição = `Expertise Board`
   * `checked`:

      * Insígnia
      * Usar Avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regra de insígnia = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite de exibição = `10`

![especialistas-quadro de classificação](assets/experts-leaderboard.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do Placar de líderes](/help/communities/leaderboard.md) página para desenvolvedores.

As instruções para criar regras são fornecidas no [Pontuação e medalhas das comunidades](/help/communities/implementing-scoring.md) página para administradores.
