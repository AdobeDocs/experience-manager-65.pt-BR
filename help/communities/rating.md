---
title: Uso de classificações
description: Saiba como adicionar um componente de Classificação a uma página que permite que os membros da comunidade conectados expressem suas opiniões por meio de conteúdo de classificação.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# Uso de classificações {#using-ratings}

A variável `Rating` O componente é usado de forma independente ou com outros recursos do Communities. Este componente permite que membros da comunidade conectados expressem suas opiniões por meio de conteúdo de classificação.

## Adicionar uma classificação a uma página {#adding-a-rating-to-a-page}

Para adicionar um `Rating` para uma página no modo de autor, localize o componente `Communities / Rating` e arraste-o para o local em uma página, como uma posição relativa ao recurso para que os membros avaliem.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](rating-basics.md#essentials-for-client-side) são incluídos, é assim que a variável `Rating` é exibido.

![avaliação](assets/rating.png)

## Configuração da classificação {#configuring-rating}

Selecione o colocado `Rating` para que você possa acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

No **[!UICONTROL Textos e rótulos]** especifique o identificador interno para a Classificação.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nome Tally]**
(*Obrigatório*) Um nome simples para o `Rating` que identifica exclusivamente esta instância. Deve ser um nome de nó válido para o repositório.

## Experiência de visitante do site {#site-visitor-experience}

### Membros {#members}

Só é permitida uma classificação por membro. O membro pode alterar a sua classificação a qualquer momento.

### Anônimo {#anonymous}

Não há suporte para postagem anônima de uma classificação. Os visitantes do site devem se registrar (tornar-se membros) e fazer logon para participar.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos de classificação](rating-basics.md) página para desenvolvedores.
