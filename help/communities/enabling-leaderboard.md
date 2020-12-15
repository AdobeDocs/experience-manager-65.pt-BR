---
title: Recurso de quadro de líderes
seo-title: Recurso de quadro de líderes
description: Adicionar um componente de Quadro de líderes a uma página
seo-description: Adicionar um componente de Quadro de líderes a uma página
uuid: c4633919-75d3-4bc7-830c-ef9c28cc1cba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9045ce2e-a06d-4da5-9b83-56dd823007bb
docset: aem65
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 9%

---


# Recurso do Quadro de líderes {#leaderboard-feature}

## Introdução {#introduction}

O componente `Leaderboard` fornece a capacidade de obter uma noção de como os membros estão interagindo dentro da comunidade classificando os membros de acordo com os pontos ganhos (pontuação básica) ou sua experiência (pontuação avançada).

Antes de incluir o componente de quadro de líderes em uma página, é necessário configurar [Pontuação e emblemas das comunidades](/help/communities/implementing-scoring.md).

Esta seção da documentação descreve:

* Adicionando o componente `Leaderboard` a um [site da comunidade](/help/communities/overview.md#community-sites).
* Configurações do componente `Leaderboard`.

### Adicionar um Quadro de líderes a uma Página {#adding-a-leaderboard-to-a-page}

Para adicionar um componente `Leaderboard` a uma página no modo de autor, localize o componente

* `Communities / Leaderboard`

e arraste-o para o lugar em uma página.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando colocado pela primeira vez em uma página de um site da comunidade, é assim que o componente aparece:

![quadro](assets/leaderboard.png)

### Configurando o Quadro de líderes {#configuring-leaderboard}

Selecione o componente `Leaderboard` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![configure-líder](assets/configure-leaderboard.png)

#### Guia Configurações {#settings-tab}

Na guia **[!UICONTROL Settings]**, especifique as informações relacionadas ao membro que serão exibidas:

* **Nome para exibição**

   Um nome descritivo a ser exibido para o quadro, refletindo as regras selecionadas para exibição de símbolos e pontuações.
O padrão é `Leaderboard`, se nada for inserido.

* **Insígnia**

   Se marcada, uma coluna para ícones de crachá é incluída no quadro de líderes.
O padrão está desmarcado.

* **Nome da insígnia**

   Se marcada, uma coluna para o nome do crachá é incluída no quadro de líderes.
O padrão está desmarcado.

* **Usar avatar**

   Se marcada, a imagem de avatar do membro é incluída no quadro de líderes, ao lado do link de nome para o perfil do membro.
O padrão está desmarcado.

#### Guia Regras {#rules-tab}

Na guia **Regras**, o site da comunidade e suas regras de pontuação e marcação

* **Local da regra**

   (Obrigatório) Local onde a regra de Pontuação/Classificação está configurada.

* **Regra de pontuação**

   (Obrigatório) Regra específica que gera as pontuações a serem exibidas.

* **Regra para insígnias**

   (Obrigatório) Regra específica que gera o crachá a ser exibido.

* **Limite de exibição**

   Número de membros a serem exibidos por página. O padrão é 10.

### Exemplo: Painel de líderes dos participantes {#example-participants-leaderboard}

Este quadro de líderes informa os resultados da aplicação de regras básicas de pontuação.

Configuração do componente de quadro de líderes:

* Guia Configurações:

   * Nome para exibição = `Participation Board`
   * `checked`:

      * Insígnia
      * Nome da insígnia
      * Usar avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/forums-scoring`
   * Regra para insígnias = `/libs/settings/community/badging/rules//reference-badging`
   * Limite de exibição = `10`

![quadro de líderes de participantes](assets/participants-leaderboard.png)

### Exemplo: Painel de líderes de especialistas {#example-experts-leaderboard}

Esse relatório de quadro de líderes resulta da aplicação de regras de pontuação avançadas.

Configuração do componente de quadro de líderes:

* Guia Configurações:

   * Nome para exibição = `Expertise Board`
   * `checked`:

      * Insígnia
      * Usar avatar

* Guia Regras:

   * Local da regra = `/content/sites/<site name>/jcr:content`
   * Regra de pontuação = `/libs/settings/community/scoring/rules/adv-forums-scoring`
   * Regra para insígnias = `/libs/settings/community/badging/rules/adv-forums-badging`
   * Limite de exibição = `10`

![comitê de peritos](assets/experts-leaderboard.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Principais componentes do Quadro de líderes](/help/communities/leaderboard.md) para desenvolvedores.

As instruções para a criação de regras são fornecidas na página [Pontuação de comunidades e emblemas](/help/communities/implementing-scoring.md) para administradores.
