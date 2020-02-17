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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso da votação {#using-voting}

O `Voting` componente é uma ferramenta útil que permite que os membros da comunidade classifiquem um conteúdo específico, como uma resposta em um componente QnA. Com o `Voting` componente, os membros selecionam setas para cima ou para baixo para indicar sua opinião.

## Adicionar votação a uma página {#adding-voting-to-a-page}

Para adicionar um `Voting` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / Voting` e arrastá-lo para o local em uma página, como uma posição relativa ao recurso no qual os usuários votarão.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](essentials-voting.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Voting` componente será exibido.

![chlimage_1-307](assets/chlimage_1-307.png)

## Configuração da votação {#configuring-voting}

Selecione o componente inserido a ser acessado e selecione o `Voting` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-308](assets/chlimage_1-308.png)

Na guia **[!UICONTROL Textos e etiquetas]** , especifique as propriedades usadas para registrar votos.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL Rótulo]** de resposta positiva (*obrigatório*) O nome da propriedade interna para uma resposta positiva.

* **[!UICONTROL Rótulo]** de resposta negativa (*obrigatório*) O nome da propriedade interna para uma resposta negativa.

* **[!UICONTROL Nome]** de contagem (*obrigatório*) O nome de propriedade interno e identificável para esta instância de um componente de votação.

## Experiência do visitante do site {#site-visitor-experience}

### Membros {#members}

Os deputados só podem votar uma vez, mas podem alterar a sua votação em qualquer altura.

### Anônimo {#anonymous}

Voto anônimo não é apoiado. Os visitantes do site devem se registrar (tornar-se um membro) e fazer logon para participar da votação uma vez.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Noting Essentials](essentials-voting.md) para desenvolvedores.
