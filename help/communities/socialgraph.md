---
title: Uso do gráfico social
seo-title: Uso do gráfico social
description: Adicionar um componente a seguir a uma página
seo-description: Adicionar um componente a seguir a uma página
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Usando o Gráfico Social {#using-social-graph}

## Introdução {#introduction}

A capacidade de um membro da comunidade seguir [atividade](activities.md), assim como a de ser seguido, é estabelecida por meio de dois componentes: `Follow` e `Following`.

O componente `Follow` deve estar associado a outro recurso, e essa associação já está estabelecida para membros e recursos da comunidade.

O componente `Following` simplesmente lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social das relações entre membros é incluído no perfil de usuário estabelecido para um [site da comunidade](overview.md#communitiessites).

## Adicionar a seguinte a uma página {#adding-following-to-a-page}

Se desejar adicionar um componente `Following` a uma página no modo de autor, localize o componente `Communities / Following` e arraste-o para o lugar em uma página onde o gráfico social deve aparecer.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](essentials-socialgraph.md#essentials-for-client-side) forem incluídas, o componente `Following` aparecerá desta forma:

![following](assets/following.png)

## Configurando {#configuring-following}

Atualmente, é necessário definir a propriedade para determinar se o componente exibe a relação `follows` ou `following`.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Social Graph Essentials](essentials-socialgraph.md) para desenvolvedores.
