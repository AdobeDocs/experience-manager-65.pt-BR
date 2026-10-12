---
title: Usando a votação
description: Saiba como adicionar o componente de Votação a uma página que permite que os membros da comunidade conectados avaliem um conteúdo específico, como uma resposta.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%
---
# Usando a votação {#using-voting}

O componente `Voting` é uma ferramenta útil que permite aos membros da comunidade classificar um conteúdo específico, como uma resposta dentro de um componente QnA. Com o componente `Voting`, os membros selecionam setas para cima ou para baixo para indicar sua opinião.

## Adicionando votação a uma página {#adding-voting-to-a-page}

Para adicionar um componente `Voting` a uma página no modo Autor, use o navegador de componentes. Localize `Communities / Voting` e arraste-o para o local em uma página, como uma posição relativa ao recurso para que os usuários possam votar.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](essentials-voting.md#essentials-for-client-side) são incluídas, é assim que o componente `Voting` aparece.

![componente de votação](assets/voting-component.png)

## Configurando a votação {#configuring-voting}

Selecione o componente `Voting` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **[!UICONTROL Textos e rótulos]**, especifique as propriedades usadas para registrar votos.

![rótulo de votação](assets/voting-label.png)

* **[!UICONTROL Rótulo de Resposta Positiva]**

  (*Obrigatório*) O nome da propriedade interna para uma resposta positiva.

* **[!UICONTROL Rótulo de resposta negativo]**

  (*Obrigatório*) O nome da propriedade interna para uma resposta negativa.

* **[!UICONTROL Nome da Tally]**

  (*Obrigatório*) O nome de propriedade interno e identificável para esta instância de um componente de votação.

## Experiência de visitante do site {#site-visitor-experience}

### Membros {#members}

Os deputados só podem votar uma vez, mas podem alterar o seu voto a qualquer momento.

### Anônimo {#anonymous}

O voto anônimo não é suportado. Os visitantes do site devem se registrar (se tornar um membro) e fazer logon para participar da votação uma vez.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página do [Voting Essentials](essentials-voting.md) para desenvolvedores.
