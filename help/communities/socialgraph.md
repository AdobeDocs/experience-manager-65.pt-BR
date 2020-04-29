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
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Uso do gráfico social {#using-social-graph}

## Introdução {#introduction}

A capacidade de um membro da comunidade seguir as [atividades](activities.md) e ser seguido é estabelecida por meio de dois componentes: `Follow` e `Following`.

O `Follow` componente deve ser associado a outro recurso, e essa associação já está estabelecida para membros e recursos da comunidade.

O `Following` componente simplesmente lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social das relações entre os membros é incluído no perfil do usuário estabelecido para um site [da](overview.md#communitiessites)comunidade.

## Adicionar o seguinte a uma página {#adding-following-to-a-page}

Se desejar adicionar um `Following` componente a uma página no modo de autor, localize o componente `Communities / Following` e arraste-o para o lugar em uma página onde o gráfico social deve aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](essentials-socialgraph.md#essentials-for-client-side) necessárias forem incluídas, o `Following` componente aparecerá desta forma:

![chlimage_1-447](assets/chlimage_1-447.png)

## Configuração a seguir {#configuring-following}

Atualmente, é necessário definir a propriedade para determinar se o componente exibe a `follows` relação ou a `following` relação.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página Essenciais [do gráfico](essentials-socialgraph.md) social para desenvolvedores.
