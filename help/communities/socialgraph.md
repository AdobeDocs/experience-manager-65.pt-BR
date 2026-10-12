---
title: Uso do gráfico social
description: Saiba como adicionar um componente Seguinte a uma página que permite que membros da comunidade conectados sigam atividades ou sejam seguidos.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
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
source-wordcount: '199'
ht-degree: 1%
---
# Uso do gráfico social {#using-social-graph}

## Introdução {#introduction}

A capacidade de um membro da comunidade seguir [atividades](activities.md) e ser seguido é estabelecida por dois componentes: `Follow` e `Following`.

O componente `Follow` deve ser associado a outro recurso, e essa associação já foi estabelecida para membros e recursos da comunidade.

O componente `Following` simplesmente lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social das relações entre membros está incluído no perfil de usuário estabelecido para um [site de comunidade](overview.md#communitiessites).

## Adicionar seguidores a uma página {#adding-following-to-a-page}

Se quiser adicionar um componente `Following` a uma página no modo de criação, localize o componente `Communities / Following` e arraste-o para o local em uma página onde o gráfico social deverá aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](essentials-socialgraph.md#essentials-for-client-side) são incluídas, é assim que o componente `Following` aparece:

![seguintes](assets/following.png)

## Configurar o seguinte {#configuring-following}

Atualmente, é necessário definir a propriedade para determinar se o componente exibe a relação `follows` ou a relação `following`.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página do [Social Graph Essentials](essentials-socialgraph.md) para desenvolvedores.
