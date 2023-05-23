---
title: Uso do gráfico social
seo-title: Using Social Graph
description: Adicionar um componente seguinte a uma página
seo-description: Adding a Following component to a page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Uso do gráfico social {#using-social-graph}

## Introdução {#introduction}

A capacidade de um membro da comunidade de seguir [atividades](activities.md) e ser seguida é estabelecida por meio de dois componentes: `Follow` e `Following`.

A variável `Follow` o componente deve ser associado a outro recurso, e essa associação já foi estabelecida para membros e recursos da comunidade.

A variável `Following` o componente simplesmente lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social dos relacionamentos entre membros é incluído no perfil do usuário estabelecido para um [site da comunidade](overview.md#communitiessites).

## Adicionar seguidores a uma página {#adding-following-to-a-page}

Se desejar adicionar um `Following` para uma página no modo de autor, localize o componente `Communities / Following` e arraste-o para o local em uma página onde o gráfico social deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-socialgraph.md#essentials-for-client-side) são incluídos, é assim que a variável `Following` componente aparecerá:

![seguindo](assets/following.png)

## Configurar o seguinte {#configuring-following}

No momento, é necessário definir a propriedade para determinar se o componente exibe a variável `follows` ou a `following` relação.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do gráfico social](essentials-socialgraph.md) página para desenvolvedores.
