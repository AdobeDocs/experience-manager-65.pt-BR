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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
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
