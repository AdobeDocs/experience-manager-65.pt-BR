---
title: Recurso de conteúdo em destaque
seo-title: Featured Content Feature
description: O recurso Conteúdo em destaque permite que os visitantes do site conectados destaquem o conteúdo
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

O recurso de conteúdo em destaque fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente de publicação para destacar conteúdo para:

* [Blogs](blog-feature.md)
* [Calendários](calendar.md)
* [Fóruns](forum.md)
* [Ideias](ideation-feature.md)
* [QnA](working-with-qna.md)

Quando o conteúdo for sinalizado como em destaque, ele será listado neste componente, que pode ser colocado em páginas de aterrissagem específicas ou áreas que chamam facilmente a atenção dos membros da comunidade.

A capacidade de apresentar conteúdo pode ser permitida ou não por componente.

Esta seção da documentação descreve:

* Adicionando conteúdo em destaque a um site da comunidade.
* Definições de configuração para o `Featured Content` componente.

## Adicionar conteúdo em destaque a uma página {#adding-featured-content-to-a-page}

Para adicionar um `Featured Content` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Featured Content`

e arraste-o para o local em uma página onde o conteúdo em destaque deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](essentials-featured.md#essentials-for-client-side) são incluídos, é assim que a variável `Featured Content` componente aparecerá:

![featuredcontent](assets/featuredcontent.png)

## Configuração de conteúdo em destaque {#configuring-featured-content}

Selecione o colocado `Featured Content` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![featuredcontent1](assets/featuredcontent1.png)

### Guia Configurações {#settings-tab}

No **[!UICONTROL Configurações]** identifique o conteúdo que será exibido:

* **[!UICONTROL Nome de exibição]**

   O título da lista de conteúdo em destaque. Por exemplo `Featured Questions` ou `Featured Ideas`. O padrão é `Featured Content` se deixado em branco.

* **[!UICONTROL Local do conteúdo em destaque]**

   *(Obrigatório)* Navegue até a página que contém o conteúdo que pode ser o recurso (os componentes dessa página devem ser configurados para Permitir conteúdo em destaque). Por exemplo, `/content/sites/engage/en/forum`.

* **[!UICONTROL Limite de exibição]**

   O número máximo de conteúdos em destaque a serem exibidos. O padrão é 5.

## Experiência de visitante do site {#site-visitor-experience}

A capacidade de sinalizar conteúdo como conteúdo em destaque requer privilégios de moderador.

Quando um moderador visualiza o conteúdo publicado, ele tem acesso aos sinalizadores de moderação do contexto, que incluem o novo `Feature` sinalizador.

![site-visitor-experience](assets/site-visitor-experience.png)

Depois de sinalizado como recurso, o sinalizador de moderação se torna `Unfeature`.

A página que contém a variável `Featured Content` componente, agora incluirá esta publicação.

![site-visitor-experience1](assets/site-visitor-experience1.png)

`Read More` é um link para a publicação real.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Conteúdo incluso](essentials-featured.md) página para desenvolvedores.

Para sinalizar conteúdo como em destaque, consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).
