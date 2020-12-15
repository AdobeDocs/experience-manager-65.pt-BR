---
title: Recurso de conteúdo em destaque
seo-title: Recurso de conteúdo em destaque
description: O recurso Conteúdo em destaque permite que visitantes do site com logon destacem conteúdo
seo-description: O recurso Conteúdo em destaque permite que visitantes do site com logon destacem conteúdo
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
translation-type: tm+mt
source-git-commit: a8b1ad0fcd2ca9c7fe3117dd8bd161da82d13e8a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---


# Recurso de conteúdo em destaque {#featured-content-feature}

## Introdução {#introduction}

O recurso de conteúdo em destaque fornece uma área para visitantes de site conectados (membros da comunidade) no ambiente de publicação para destacar o conteúdo de:

* [Blogs](blog-feature.md)
* [Calendários](calendar.md)
* [Fóruns](forum.md)
* [Ideias](ideation-feature.md)
* [Perguntas e respostas](working-with-qna.md)

Quando o conteúdo for sinalizado como em destaque, ele será listado dentro deste componente, que pode ser colocado em landings page específicas ou áreas que facilmente chamam a atenção dos membros da comunidade.

A capacidade de incluir conteúdo pode ser permitida ou não permitida por componente.

Esta seção da documentação descreve:

* Adicionar conteúdo em destaque a um site da comunidade.
* Configurações do componente `Featured Content`.

## Adicionar conteúdo em destaque a uma página {#adding-featured-content-to-a-page}

Para adicionar um componente `Featured Content` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Featured Content`

e arraste-o para o lugar em uma página onde o conteúdo em destaque deve aparecer.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](essentials-featured.md#essentials-for-client-side) forem incluídas, o componente `Featured Content` aparecerá desta forma:

![featuredcontent](assets/featuredcontent.png)

## Configuração do conteúdo em destaque {#configuring-featured-content}

Selecione o componente `Featured Content` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Guia Configurações {#settings-tab}

Na guia **[!UICONTROL Settings]**, identifique o conteúdo a ser exibido:

* **[!UICONTROL Nome para exibição]**

   O título para a lista do conteúdo em destaque. Por exemplo `Featured Questions` ou `Featured Ideas`. O padrão é `Featured Content` se deixado em branco.

* **[!UICONTROL Local do conteúdo em destaque]**

   *(Obrigatório)* Navegue até a página que contém o conteúdo que pode ser um recurso (os componentes dessa página devem ser configurados para Permitir conteúdo em destaque). Por exemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite de exibição]**

   O número máximo de conteúdos em destaque a serem exibidos. O padrão é 5.

## Experiência de Visitante do site {#site-visitor-experience}

A capacidade de sinalizar o conteúdo como conteúdo em destaque requer privilégios de moderador.

Quando um moderador visualização postou conteúdo, ele tem acesso aos sinalizadores de moderação no contexto, que inclui o novo sinalizador `Feature`.

![experiência com o visitante do site](assets/site-visitor-experience.png)

Depois de sinalizado como recurso, o sinalizador de moderação se torna `Unfeature`.

A página que contém o componente `Featured Content` agora incluirá essa publicação.

![site-visitante-experience1](assets/site-visitor-experience1.png)

`Read More` é um link para a publicação real.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Conteúdo em destaque](essentials-featured.md) para desenvolvedores.

Para marcar o conteúdo como em destaque, consulte [Moderando conteúdo gerado pelo usuário](moderate-ugc.md).
