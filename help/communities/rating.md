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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 1%
---
# Uso de classificações {#using-ratings}

O componente `Rating` é usado de forma independente ou com outros recursos das Comunidades. Este componente permite que membros da comunidade conectados expressem suas opiniões por meio de conteúdo de classificação.

## Adicionar uma classificação a uma página {#adding-a-rating-to-a-page}

Para adicionar um componente `Rating` a uma página no modo de autor, localize o componente `Communities / Rating` e arraste-o para o local em uma página, como uma posição relativa ao recurso para que os membros avaliem.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](rating-basics.md#essentials-for-client-side) são incluídas, é assim que o componente `Rating` aparece.

![classificação](assets/rating.png)

## Configuração da classificação {#configuring-rating}

Selecione o componente `Rating` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

Na guia **[!UICONTROL Textos e rótulos]**, especifique o identificador interno da classificação.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nome Tally]**
(*Obrigatório*) Um nome simples para `Rating` que identifica exclusivamente esta instância. Deve ser um nome de nó válido para o repositório.

## Experiência de visitante do site {#site-visitor-experience}

### Membros {#members}

Só é permitida uma classificação por membro. O membro pode alterar a sua classificação a qualquer momento.

### Anônimo {#anonymous}

Não há suporte para postagem anônima de uma classificação. Os visitantes do site devem se registrar (tornar-se membros) e fazer logon para participar.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Rating Essentials](rating-basics.md) para desenvolvedores.
