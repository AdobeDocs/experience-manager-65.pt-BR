---
title: Recurso de conteúdo em destaque
description: O recurso Conteúdo em destaque permite que os visitantes do site conectados destaquem o conteúdo
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# Recurso de conteúdo em destaque {#featured-content-feature}

## Introdução {#introduction}

O recurso de conteúdo em destaque fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente de publicação para destacar conteúdo para:

* [Blogs](blog-feature.md)
* [Calendários](calendar.md)
* [Fóruns](forum.md)
* [Ideias](ideation-feature.md)
* [QnA](working-with-qna.md)

Depois que o conteúdo é sinalizado como em destaque, ele é listado neste componente, que pode ser colocado em páginas de aterrissagem específicas ou áreas que chamam facilmente a atenção dos membros da comunidade.

A capacidade de apresentar conteúdo pode ser permitida ou não por componente.

Esta seção da documentação descreve:

* Adicionando conteúdo em destaque a um site da comunidade.
* Definições de configuração para o `Featured Content` componente.

## Adicionar conteúdo em destaque a uma página {#adding-featured-content-to-a-page}

Para adicionar um `Featured Content` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Featured Content`

E arraste-o para o local em uma página onde o conteúdo em destaque deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-featured.md#essentials-for-client-side) são incluídos, é assim que a variável `Featured Content` é exibido:

![featuredcontent](assets/featuredcontent.png)

## Configuração de conteúdo em destaque {#configuring-featured-content}

Selecione o colocado `Featured Content` para que você possa acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Guia Configurações {#settings-tab}

No **[!UICONTROL Configurações]** identifique o conteúdo que será exibido:

* **[!UICONTROL Nome de exibição]**

  O título da lista de conteúdo em destaque. Por exemplo, `Featured Questions` ou `Featured Ideas`. O padrão é `Featured Content` se deixado em branco.

* **[!UICONTROL Local do conteúdo em destaque]**

  *(Obrigatório)* Navegue até a página que contém o conteúdo que pode ser apresentado (os componentes dessa página devem ser configurados para Permitir conteúdo em destaque). Por exemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite de exibição]**

  O número máximo de conteúdos em destaque a serem exibidos. O padrão é 5.

## Experiência de visitante do site {#site-visitor-experience}

A capacidade de sinalizar conteúdo como conteúdo em destaque requer privilégios de moderador.

Quando um moderador visualiza o conteúdo publicado, ele tem acesso aos sinalizadores de moderação do contexto, que incluem o novo `Feature` sinalizador.

![site-visitor-experience](assets/site-visitor-experience.png)

Depois de sinalizado como um recurso, o sinalizador de moderação se torna `Unfeature`.

A página que contém a variável `Featured Content` componente, agora inclui esta publicação.

![site-visitor-experience1](assets/site-visitor-experience1.png)

A variável `Read More` links para a publicação real.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Conteúdo incluso](essentials-featured.md) página para desenvolvedores.

Para sinalizar conteúdo como em destaque, consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).
