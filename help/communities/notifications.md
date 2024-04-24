---
title: Notificações das comunidades
description: O AEM Communities tem notificações que exibem eventos de interesse para o membro da comunidade conectado
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Notificações das comunidades {#communities-notifications}

## Visão geral {#overview}

O AEM Communities fornece uma seção de notificações que exibe eventos de interesse para o membro da comunidade conectado.

As notificações são semelhantes a [atividades](/help/communities/essentials-activities.md) e [assinaturas](/help/communities/subscriptions.md) como podem resultar de:

* O conteúdo de postagem do membro.
* O membro que escolhe seguir outro membro.
* O membro optou por seguir tópicos, artigos e outras threads de conteúdo específicos.
* A marcação de membro (@mention) de outro membro da comunidade em um conteúdo gerado pelo usuário.

O que distingue as notificações das atividades e assinaturas é:

* Um link para a seção de notificações está sempre presente no cabeçalho de um site da comunidade:

   * As atividades exigem o [função de fluxo de atividade](/help/communities/functions.md#activity-stream-function) para ser incluído na estrutura do site da comunidade.
   * As assinaturas exigem [configuração de email](/help/communities/email.md).

* A implementação de notificações é feita por meio de canais dimensionáveis e conectáveis:

   * As atividades só estão disponíveis na Web.
   * As assinaturas só estão disponíveis por email.

A partir das comunidades [FP1](/help/communities/deploy-communities.md#latestfeaturepack), os canais de notificação disponíveis são:

* O canal da Web, acessado por meio do `Notifications` link.
* O canal de email, disponível quando o email é configurado corretamente.

Os canais futuros são móvel e desktop.

### Requisitos {#requirements}

**Configurar email**

O email deve ser configurado para que o canal de email funcione.

Para obter instruções sobre como configurar o email, consulte [Configuração de email](/help/communities/analytics.md).

**Ativar Seguir**

Os componentes devem ser configurados para permitir o acompanhamento. Os recursos que permitem seguir são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md), e [comentários](/help/communities/comments.md).

**Nota**:

* Componentes usados na comunidade [modelos de site](/help/communities/sites.md) e [modelos de grupo](/help/communities/tools-groups.md) pode já estar configurado para seguir.

* Os perfis de membro já estão configurados para permitir que outros membros sigam.

## Notificações do Seguinte {#notifications-from-following}

![notificações](assets/notifications.png)

A variável **[!UICONTROL Seguir]** O botão fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Cada vez que a variável **[!UICONTROL Seguir]** for selecionada, é possível ativar ou desativar uma seleção. A variável `Email Subscriptions` a seleção está presente somente quando configurada.

Se qualquer método de seguir for selecionado, o texto do botão será alterado para **[!UICONTROL Seguindo]**. Por conveniência, é possível selecionar `Unfollow All` para desativar todos os métodos.

A variável **[!UICONTROL Seguir]** aparecerá:

* Ao exibir o perfil de outro membro.
* Em uma página principal de recursos, como fóruns, QnA e blogs:

   * Segue todas as atividades desse recurso geral.

* Para uma entrada específica, como um tópico do fórum, pergunta QnA ou artigo de blog:

   * Segue todas as atividades dessa entrada específica.

## Gerenciar configurações de notificação {#managing-notification-settings}

Ao selecionar o link Definições de Notificação na página Notificações, é possível que cada membro gerencie como as notificações são recebidas.

O canal da Web está sempre habilitado.

![notificações14](assets/notifications1.png)

O canal de email, que depende da [configuração de email](/help/communities/email.md), fornece as mesmas configurações do canal Web.

O canal de email está desativado por padrão.

![notificações2](assets/notifications2.png)

Ela pode ser ativada por um membro, mas ainda depende do email estar configurado.

![notificações3](assets/notifications3.png)

## Visualizar notificações {#viewing-notifications}

### Notificações da Web {#web-notifications}

A [o assistente criou o site da comunidade](/help/communities/sites-console.md) agora inclui um link para a variável `Notifications` recurso na barra de cabeçalho do site acima do banner. Diferentemente das mensagens, as notificações são criadas para cada site da comunidade, enquanto as mensagens devem ser ativadas durante o processo de criação do site.

Ao visitar o site publicado, selecione o `Notifications` exibirá todas as notificações do membro.

![notificações4](assets/notifications4.png)

### Notificações por email {#email-notifications}

Quando o canal de email está ativado, o membro recebe um email que contém um link para o conteúdo na Web.

![notificações5](assets/notifications5.png)

## Personalizar notificações por email {#customize-email-notifications}

As organizações podem personalizar as notificações por email [sobreposição](/help/communities/client-customize.md#overlays) os modelos em **/libs/settings/community/templates/email/html**.

Por exemplo, para modificar as menções notificações por email (para um componente de comunidades), adicione uma **se** condição para verbo **menção** nos modelos dos componentes para os quais você ativou a variável **@mentions** suporte.

Para modificar o modelo de notificações por email para @mention em comentários de blog, coloque o modelo pronto para uso em: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/br**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
