---
title: Uso de classificações
seo-title: Uso de classificações
description: Adicionar um componente de Classificação a uma página
seo-description: Adicionar um componente de Classificação a uma página
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Uso de classificações {#using-ratings}

O `Rating` componente é usado separadamente ou em conjunto com outros recursos das Comunidades. Este componente permite que membros da comunidade com logon expressem suas opiniões por meio da classificação do conteúdo.

## Adding a Rating to a Page {#adding-a-rating-to-a-page}

Para adicionar um `Rating` componente a uma página no modo de autor, localize o componente `Communities / Rating` e arraste-o para o lugar em uma página, como uma posição relativa ao recurso para os membros classificarem.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](rating-basics.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Rating` componente será exibido.

![chlimage_1-493](assets/chlimage_1-493.png)

## Configuração da classificação {#configuring-rating}

Selecione o componente inserido a ser acessado e selecione o `Rating` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-494](assets/chlimage_1-494.png)

Na guia **[!UICONTROL Textos e etiquetas]** , especifique o identificador interno para a Classificação.

![chlimage_1-495](assets/chlimage_1-495.png)

**[!UICONTROL Nome]** Tally (*Obrigatório*) Um nome simples para o `Rating`que identifica exclusivamente esta instância. Deve ser um nome de nó válido para o repositório.

## Experiência com o Visitante do site {#site-visitor-experience}

### Membros {#members}

Somente uma classificação por membro é permitida. O membro pode alterar a sua notação a qualquer momento.

### Anônimo {#anonymous}

Não há suporte para a publicação anônima de uma classificação. Os visitantes do site devem se registrar (tornar-se um membro) e fazer logon para participar.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Rating Essentials](rating-basics.md) para desenvolvedores.
