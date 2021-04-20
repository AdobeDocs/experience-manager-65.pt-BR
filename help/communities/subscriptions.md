---
title: Assinaturas das Comunidades
seo-title: Assinaturas das Comunidades
description: Os membros da comunidade interagem com outros membros por email
seo-description: Os membros da comunidade interagem com outros membros por email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 2%

---


# Assinaturas das Comunidades {#communities-subscriptions}

## Visão geral {#overview}

A partir de Comunidades [FP1](deploy-communities.md#latestfeaturepack), os membros da comunidade podem interagir com a comunidade por meio de email usando um recurso chamado de assinaturas.

As assinaturas são semelhantes a [notificações](notifications.md), pois os membros podem se inscrever ao seguir artigos de blog, tópicos do fórum ou perguntas de QnA.

O que distingue as assinaturas das notificações é:

* Os membros não podem subscrever-se depois de outros membros.
* A única ação que os membros devem tomar é selecionar `Email Subscriptions` ao seguir.
* Quando a resposta por e-mail é configurada, os membros podem efetivamente postar conteúdo simplesmente respondendo ao e-mail recebido.

### Requisitos {#requirements}

**Configurar Email**

O email deve ser configurado para que as assinaturas sejam funcionais e os membros respondam por email.

Para obter instruções sobre como configurar o email, consulte [Configuração do email](email.md).

**Ativar assinaturas e seguir**

Os componentes devem ser configurados para ativar as assinaturas *e* a seguir. Os recursos que permitem assinaturas são [blog](blog-feature.md), [forum](forum.md) e [QnA](working-with-qna.md).

## Assinaturas de {#subscriptions-from-following} a seguir

![subscription-following](assets/subscription-following.png)

O botão **Follow** fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Sempre que o botão **Follow** é selecionado, é possível ativar ou desativar uma seleção.

Se qualquer método do seguinte for selecionado, o texto do botão será alterado para **Seguindo**. Para maior comodidade, é possível selecionar `Unfollow All` para desligar todos os métodos.

O botão **Follow** incluirá a opção `Email Subscriptions` somente quando um fórum, QnA ou blog estiver configurado para ativar assinaturas de email. Esse botão aparecerá:

* Na página de recurso principal do fórum habilitado, QnA ou blog Enviará um email para todas as atividades sob esse recurso.

* Para uma entrada específica, como um tópico de fórum, pergunta de QnA ou artigo de blog Enviará um email quando houver atividade para essa entrada específica.

## Responder por e-mail {#reply-by-email}

Quando o email for [configurado para responder por email](email.md#configure-polling-importer), o membro que se inscreveu receberá um email com o conteúdo postado e um link para o conteúdo online.

Se responderem ao email, o conteúdo inserido na resposta será exibido como conteúdo online.

![email-reply](assets/email-reply.png)

O tempo que leva para uma resposta ser postada é controlado pelo [intervalo de atualização do importador de pesquisa](email.md#configure-polling-importer).

![QA](assets/qa.png)

