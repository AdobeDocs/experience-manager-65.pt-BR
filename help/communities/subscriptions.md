---
title: Assinaturas das Comunidades
seo-title: Communities Subscriptions
description: Os membros da comunidade interagem com outros membros por email
seo-description: Community members interact with other members through email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Assinaturas das Comunidades {#communities-subscriptions}

## Visão geral {#overview}

Comunidades [FP1](deploy-communities.md#latestfeaturepack), os membros da comunidade podem interagir com a comunidade por email usando um recurso chamado de assinaturas.

As assinaturas são semelhantes a [notificações](notifications.md) como membros podem se inscrever ao seguir artigos de blog, tópicos do fórum ou perguntas de QnA.

O que distingue as assinaturas das notificações é:

* Os membros não podem subscrever-se depois de outros membros.
* A única ação que os membros devem tomar é selecionar `Email Subscriptions` ao seguir.
* Quando a resposta por e-mail é configurada, os membros podem efetivamente postar conteúdo simplesmente respondendo ao e-mail recebido.

### Requisitos {#requirements}

**Configurar Email**

O email deve ser configurado para que as assinaturas sejam funcionais e os membros respondam por email.

Para obter instruções sobre como configurar o email, consulte [Configuração de email](email.md).

**Ativar assinaturas e seguir**

Os componentes devem ser configurados para habilitar assinaturas *e* seguinte. Os recursos que permitem assinaturas são [blog](blog-feature.md), [fórum](forum.md) e [QnA](working-with-qna.md).

## Assinaturas do seguinte {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

O **Seguir** fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Sempre que a variável **Seguir** for selecionado, é possível ativar ou desativar uma seleção.

Se qualquer método de seguir for selecionado, o texto do botão será alterado para **Seguindo**. Para maior comodidade, é possível selecionar `Unfollow All` para desativar todos os métodos.

O **Seguir** incluirá o botão `Email Subscriptions` somente quando um fórum, QnA ou blog é configurado para ativar assinaturas de email. Esse botão aparecerá:

* Na página de recurso principal do fórum habilitado, QnA ou blog Enviará um email para todas as atividades sob esse recurso.

* Para uma entrada específica, como um tópico de fórum, pergunta de QnA ou artigo de blog Enviará um email quando houver atividade para essa entrada específica.

## Responder por email {#reply-by-email}

Quando o email é [configurado para responder por email](email.md#configure-polling-importer), o membro que se inscreveu receberá um email com o conteúdo publicado e um link para o conteúdo online.

Se responderem ao email, o conteúdo inserido na resposta será exibido como conteúdo online.

![email-reply](assets/email-reply.png)

O tempo necessário para uma resposta ser postada é controlado pela variável [intervalo de atualização do importador de pesquisa](email.md#configure-polling-importer).

![QA](assets/qa.png)
