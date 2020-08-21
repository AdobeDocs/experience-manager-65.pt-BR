---
title: Uso da votação
seo-title: Uso da votação
description: Adicionar o componente de Votação a uma página
seo-description: Adicionar o componente de Votação a uma página
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 4%

---


# Uso da votação {#using-voting}

O `Voting` componente é uma ferramenta útil que permite que os membros da comunidade classifiquem um conteúdo específico, como uma resposta em um componente QnA. Com o `Voting` componente, os membros selecionam setas para cima ou para baixo para indicar sua opinião.

## Adicionar votação a uma página {#adding-voting-to-a-page}

Para adicionar um `Voting` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / Voting` e arrastá-lo para o local em uma página, como uma posição relativa ao recurso no qual os usuários votarão.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](essentials-voting.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Voting` componente será exibido.

![componente de votação](assets/voting-component.png)

## Configuração da votação {#configuring-voting}

Selecione o componente inserido a ser acessado e selecione o `Voting` `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Na guia **[!UICONTROL Textos e etiquetas]** , especifique as propriedades usadas para registrar votos.

![etiqueta de voto](assets/voting-label.png)

* **[!UICONTROL Rótulo de resposta positiva]**

   (*Obrigatório*) O nome da propriedade interna para uma resposta positiva.

* **[!UICONTROL Etiqueta de resposta negativa]**

   (*Obrigatório*) O nome da propriedade interna para uma resposta negativa.

* **[!UICONTROL Nome Tally]**

   (*Obrigatório*) O nome de propriedade interno e identificável para esta instância de um componente de votação.

## Experiência com o Visitante do site {#site-visitor-experience}

### Membros {#members}

Os deputados só podem votar uma vez, mas podem alterar a sua votação em qualquer altura.

### Anônimo {#anonymous}

Voto anônimo não é apoiado. Os visitantes do site devem se registrar (tornar-se membros) e fazer logon para participar da votação uma vez.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Noting Essentials](essentials-voting.md) para desenvolvedores.
