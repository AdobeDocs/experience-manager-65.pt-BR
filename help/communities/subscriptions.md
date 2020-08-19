---
title: Subscrições de comunidades
seo-title: Subscrições de comunidades
description: Os membros da comunidade interagem com outros membros por email
seo-description: Os membros da comunidade interagem com outros membros por email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Subscrições de comunidades {#communities-subscriptions}

## Visão geral {#overview}

A partir do [FP1](deploy-communities.md#latestfeaturepack)das Comunidades, os membros da comunidade podem interagir com a comunidade por email usando um recurso chamado subscrição.

As subscrições são semelhantes às [notificações](notifications.md) , pois os membros podem se inscrever ao seguir artigos de blog, tópicos do fórum ou perguntas de QnA.

O que distingue as subscrições das notificações é:

* Os membros não podem subscrever se estiverem a seguir outros membros.
* A única ação a ser tomada pelos membros é selecionar `Email Subscriptions` ao seguir.
* Quando a resposta por e-mail é configurada, os membros podem efetivamente postar o conteúdo simplesmente respondendo ao e-mail recebido.

### Requisitos {#requirements}

**Configurar email**

O email deve ser configurado para que as subscrições estejam funcionais e para que os membros respondam por email.

Para obter instruções sobre como configurar e-mail, consulte [Configuração de e-mail](email.md).

**Ativar Subscrições e seguir**

Os componentes devem ser configurados para ativar o subscrição *e* os seguintes itens. Os recursos que permitem o subscrição são [blog](blog-feature.md), [fórum](forum.md) e [QnA](working-with-qna.md).

## Subscrições a partir de {#subscriptions-from-following}

![subscrição seguinte](assets/subscription-following.png)

O botão **Seguir** fornece um meio de seguir entradas como atividades, subscrições e/ou notificações. Cada vez que o botão **Seguir** é selecionado, é possível ativar ou desativar uma seleção.

Se algum método de seguir for selecionado, o texto do botão mudará para **Seguinte**. Para sua conveniência, é possível selecionar `Unfollow All` alternar todos os métodos.

O botão **Seguir** incluirá a `Email Subscriptions` opção somente quando um fórum, QnA ou blog estiver configurado para ativar subscrições por email. Este botão será exibido:

* Na página principal de recursos do fórum habilitado, QnA ou blog Enviará um email para todas as atividades sob esse recurso.

* Para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog Enviará um email quando houver atividade para essa entrada específica.

## Responder por email {#reply-by-email}

Quando o email for [configurado para resposta por email](email.md#configure-polling-importer), o membro que se inscreveu receberá um email com o conteúdo publicado e um link para o conteúdo online.

Se eles responderem ao email, o conteúdo digitado na resposta será exibido como conteúdo online.

![email-reply](assets/email-reply.png)

O tempo necessário para uma resposta ser postada é controlado pelo intervalo [de atualização do importador da](email.md#configure-polling-importer)pesquisa.

![QA](assets/qa.png)

