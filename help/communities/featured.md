---
title: Recurso de conteúdo em destaque
seo-title: Featured Content Feature
description: O recurso Conteúdo em destaque permite que visitantes do site que fizeram logon destaque o conteúdo
seo-description: The Featured Content feature lets signed-in site visitors highlight content
uuid: 7a2ff570-01bb-46fb-8d66-3b47e2efa72e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ee39435d-80f5-4758-ae01-1ea0d221b00b
exl-id: 76b76e0e-531b-4f80-be70-68532ef81a7f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 5%

---

# Recurso de conteúdo em destaque {#featured-content-feature}

## Introdução {#introduction}

O recurso de conteúdo em destaque fornece uma área para visitantes do site que fizeram logon (membros da comunidade) no ambiente de publicação para destacar o conteúdo para:

* [Blogs](blog-feature.md)
* [Calendários](calendar.md)
* [Fóruns](forum.md)
* [Ideias](ideation-feature.md)
* [Perguntas e respostas](working-with-qna.md)

Quando o conteúdo for sinalizado como em destaque, ele será listado dentro desse componente, que pode ser colocado em landing pages ou áreas específicas que facilmente chamam a atenção dos membros da comunidade.

A capacidade de incluir conteúdo pode ser permitida ou não permitida por componente.

Esta seção da documentação descreve:

* Adicionar conteúdo em destaque a um site da comunidade.
* Configurações para o `Featured Content` componente.

## Adicionar conteúdo em destaque a uma página {#adding-featured-content-to-a-page}

Para adicionar uma `Featured Content` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Featured Content`

e arraste-o para o lugar em uma página onde o conteúdo em destaque deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-featured.md#essentials-for-client-side) são incluídos, é assim que a variável `Featured Content` componente será exibido:

![featuredcontent](assets/featuredcontent.png)

## Configuração do conteúdo em destaque {#configuring-featured-content}

Selecione o `Featured Content` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Guia Configurações {#settings-tab}

Em **[!UICONTROL Configurações]** , identifique o conteúdo a ser exibido:

* **[!UICONTROL Nome para exibição]**

   O título da lista de conteúdos em destaque. Por exemplo `Featured Questions` ou `Featured Ideas`. O padrão é `Featured Content` se deixado em branco.

* **[!UICONTROL Local do conteúdo em destaque]**

   *(Obrigatório)* Navegue até a página que contém o conteúdo que pode ser um recurso (os componentes dessa página devem ser configurados para Permitir conteúdo em destaque). Por exemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite de exibição]**

   O número máximo de conteúdos em destaque a serem exibidos. O padrão é 5.

## Experiência de visitante do site {#site-visitor-experience}

A capacidade de marcar o conteúdo como um conteúdo em destaque requer privilégios de moderador.

Quando um moderador exibe o conteúdo publicado, ele tem acesso aos sinalizadores de moderação no contexto, que incluem o novo `Feature` sinalizador.

![experiência de visitante do site](assets/site-visitor-experience.png)

Depois de sinalizado como recurso, o sinalizador de moderação torna-se `Unfeature`.

A página que contém o `Featured Content` , agora incluirá essa publicação.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` é um link para a publicação real.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Conteúdo em destaque](essentials-featured.md) página para desenvolvedores.

Para marcar o conteúdo como em destaque, consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).
