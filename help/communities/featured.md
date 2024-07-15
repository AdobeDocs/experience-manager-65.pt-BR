---
title: Recurso de conteúdo em destaque
description: O recurso Conteúdo em destaque permite que os visitantes do site conectados destaquem o conteúdo
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

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
* Definições de configuração para o componente `Featured Content`.

## Adicionar conteúdo em destaque a uma página {#adding-featured-content-to-a-page}

Para adicionar um componente `Featured Content` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Featured Content`

E arraste-o para o local em uma página onde o conteúdo em destaque deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](essentials-featured.md#essentials-for-client-side) são incluídas, é assim que o componente `Featured Content` aparece:

![conteúdo do recurso](assets/featuredcontent.png)

## Configuração de conteúdo em destaque {#configuring-featured-content}

Selecione o componente `Featured Content` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

![conteúdo_do_recurso1](assets/featuredcontent1.png)

### Guia Configurações {#settings-tab}

Na guia **[!UICONTROL Configurações]**, identifique o conteúdo a ser apresentado:

* **[!UICONTROL Nome de exibição]**

  O título da lista de conteúdo em destaque. Por exemplo, `Featured Questions` ou `Featured Ideas`. O padrão é `Featured Content` se deixado em branco.

* **[!UICONTROL Local do Conteúdo em Destaque]**

  *(Obrigatório)* Navegue até a página que contém o conteúdo que pode ser apresentado (os componentes dessa página devem ser configurados para Permitir Conteúdo em Destaque). Por exemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite de exibição]**

  O número máximo de conteúdos em destaque a serem exibidos. O padrão é 5.

## Experiência de visitante do site {#site-visitor-experience}

A capacidade de sinalizar conteúdo como conteúdo em destaque requer privilégios de moderador.

Quando um moderador exibe o conteúdo postado, ele tem acesso aos sinalizadores de moderação no contexto, que incluem o novo sinalizador `Feature`.

![experiência-visitante-site](assets/site-visitor-experience.png)

Depois de sinalizado como recurso, o sinalizador de moderação torna-se `Unfeature`.

A página contendo o componente `Featured Content`, agora inclui esta publicação.

![experiência-visitante-site1](assets/site-visitor-experience1.png)

O `Read More` está vinculado à postagem real.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Conteúdo em destaque](essentials-featured.md) para desenvolvedores.

Para sinalizar conteúdo como em destaque, consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).
