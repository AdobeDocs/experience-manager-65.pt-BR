---
title: Usar votação
seo-title: Using Voting
description: Adicionar o componente de Votação a uma página
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 5%

---

# Usar votação {#using-voting}

O `Voting` é uma ferramenta útil que permite aos membros da comunidade classificar um conteúdo específico, como uma resposta em um componente de QnA. Com o `Voting` , os membros selecionam setas para cima ou para baixo para indicar sua opinião.

## Adicionar votação a uma página {#adding-voting-to-a-page}

Para adicionar uma `Voting` para uma página no modo autor, use o navegador de componentes para localizar `Communities / Voting` e arraste-a para o local em uma página, como uma posição relativa ao recurso no qual os usuários devem votar.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-voting.md#essentials-for-client-side) são incluídos, é assim que a variável `Voting` será exibido.

![componente de votação](assets/voting-component.png)

## Configuração da votação {#configuring-voting}

Selecione o `Voting` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Em **[!UICONTROL Textos e rótulos]** , especifique as propriedades usadas para registrar votos.

![rótulo de voto](assets/voting-label.png)

* **[!UICONTROL Rótulo de resposta positiva]**

   (*Obrigatório*) O nome da propriedade interna para uma resposta positiva.

* **[!UICONTROL Etiqueta de resposta negativa]**

   (*Obrigatório*) O nome da propriedade interna para uma resposta negativa.

* **[!UICONTROL Nome Tally]**

   (*Obrigatório*) O nome de propriedade interno e identificável para esta instância de um componente de votação.

## Experiência de visitante do site {#site-visitor-experience}

### Membros {#members}

Os deputados só podem votar uma vez, mas podem alterar a sua votação em qualquer altura.

### Anônimo {#anonymous}

A votação anônima não é apoiada. Os visitantes do site devem se registrar (se tornar um membro) e fazer logon para participar da votação uma vez.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos da votação](essentials-voting.md) página para desenvolvedores.
