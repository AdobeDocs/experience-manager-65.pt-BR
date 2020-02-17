---
title: Assinaturas de comunidades
seo-title: Assinaturas de comunidades
description: Os membros da comunidade interagem com outros membros por email
seo-description: Os membros da comunidade interagem com outros membros por email
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Assinaturas de comunidades {#communities-subscriptions}

## Visão geral {#overview}

A partir do [FP1](deploy-communities.md#latestfeaturepack)das Comunidades, os membros da comunidade podem interagir com a comunidade por email usando um recurso chamado de assinaturas.

As assinaturas são semelhantes às [notificações](notifications.md) , pois os membros podem se inscrever ao seguir artigos de blog, tópicos do fórum ou perguntas de QnA.

O que distingue as assinaturas das notificações é:

* Os membros não podem subscrever quando seguirem outros membros
* A única ação a ser tomada pelos membros é selecionar `Email Subscriptions` ao seguir
* Quando a resposta por e-mail é configurada, os membros podem efetivamente postar conteúdo simplesmente respondendo ao e-mail recebido

### Requisitos {#requirements}

**Configurar email**

O email deve ser configurado para que as assinaturas sejam funcionais e para que os membros respondam por email.

Para obter instruções sobre como configurar o email, consulte [Configuração do email](email.md).

**Ativar assinaturas e seguir**

Os componentes devem ser configurados para permitir assinaturas *e* seguintes. Os recursos que permitem assinaturas são [blog](blog-feature.md), [fórum](forum.md) e [QnA](working-with-qna.md).

## Assinaturas dos seguintes {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

O botão **Seguir** fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Sempre que o botão **Seguir** é selecionado, é possível ativar ou desativar uma seleção.

Se algum método de seguir for selecionado, o texto do botão mudará para **Seguinte**. Para sua conveniência, é possível optar por desativar todos os métodos `Unfollow All` .

O botão **Seguir** incluirá a `Email Subscriptions` opção somente quando um fórum, QnA ou blog estiver configurado para ativar assinaturas por email. Este botão será exibido

* Na página principal de recursos do fórum habilitado, QnA ou blog

   * Enviará um email para todas as atividades do recurso

* Para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog

   * Enviará um email quando houver atividade para essa entrada específica

## Responder por email {#reply-by-email}

Quando o email for [configurado para resposta por email](email.md#configure-polling-importer), o membro que se inscreveu receberá um email com o conteúdo publicado e um link para o conteúdo online.

Se eles responderem ao email, o conteúdo digitado na resposta será exibido como conteúdo online.

![chlimage_1-6](assets/chlimage_1-6.png)

O tempo necessário para uma resposta ser postada é controlado pelo intervalo [de atualização do importador da](email.md#configure-polling-importer)pesquisa.

![chlimage_1-7](assets/chlimage_1-7.png)

