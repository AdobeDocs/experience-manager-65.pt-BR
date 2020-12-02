---
title: Notificações de comunidades
seo-title: Notificações de comunidades
description: A AEM Communities tem notificações que exibem eventos de interesse para o membro da comunidade conectado
seo-description: A AEM Communities tem notificações que exibem eventos de interesse para o membro da comunidade conectado
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 5d196d1f6d5f94f2d3ef0d4461cfe38562f8ba8c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# Notificações de comunidades {#communities-notifications}

## Visão geral {#overview}

A AEM Communities fornece uma seção de notificações que exibe eventos de interesse para o membro da comunidade conectado.

As notificações são semelhantes a [atividade](/help/communities/essentials-activities.md) e [subscrição](/help/communities/subscriptions.md), uma vez que podem resultar de:

* O conteúdo de publicação do membro.
* O membro que escolheu seguir outro membro.
* O membro optou por seguir tópicos específicos, artigos e outros segmentos de conteúdo.
* A marcação de membro (@menção) de outro membro da comunidade em um conteúdo gerado pelo usuário.

O que distingue as notificações do atividade e do subscrição é:

* Um link para a seção de notificações está sempre presente no cabeçalho do site da comunidade:

   * O Atividade exige que [função de fluxo de atividade](/help/communities/functions.md#activity-stream-function) seja incluída na estrutura do site da comunidade.
   * O Subscrição exige [configuração de email](/help/communities/email.md).

* A implementação de notificações é feita por meio de canais escaláveis e conectáveis:

   * As atividades só estão disponíveis na Web.
   * As subscrições só estão disponíveis por email.

A partir de Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack), os canais de notificação disponíveis são:

* O canal da Web, acessado usando o link `Notifications`.
* O canal de email, disponível quando o email está configurado corretamente.

Os futuros canais são móveis e desktops.

### Requisitos {#requirements}

**Configurar email**

O e-mail deve ser configurado para que o canal de e-mail possa receber notificações.

Para obter instruções sobre como configurar o email, consulte [Configuração do Email](/help/communities/analytics.md).

**Habilitar Seguir**

Os componentes devem ser configurados para permitir o seguinte. Os recursos que permitem o seguinte são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) e [comentários](/help/communities/comments.md).

**Nota**:

* Os componentes usados nos [modelos de site da comunidade](/help/communities/sites.md) e [modelos de grupo](/help/communities/tools-groups.md) já podem estar configurados para seguir.

* Os perfis membros já estão configurados para permitir que outros membros sigam.

## Notificações do seguinte {#notifications-from-following}

![notificações](assets/notifications.png)

O botão **[!UICONTROL Seguir]** fornece um meio de seguir as entradas como atividades, subscrições e/ou notificações. Sempre que o botão **[!UICONTROL Seguir]** for selecionado, é possível ativar ou desativar uma seleção. A seleção `Email Subscriptions` só está presente quando configurada.

Se algum método do seguinte for selecionado, o texto do botão mudará para **[!UICONTROL Seguindo]**. Para conveniência, é possível selecionar `Unfollow All` para desativar todos os métodos.

O botão **[!UICONTROL Seguir]** será exibido:

* Ao exibir o perfil de outro membro.
* Em uma página principal do recurso, como fóruns, QnA e blogs:

   * Segue toda a atividade desse recurso geral.

* Para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog:

   * Segue toda a atividade para essa entrada específica.

## Gerenciando configurações de notificação {#managing-notification-settings}

Ao selecionar o link Configurações de notificação na página Notificações, é possível que cada membro gerencie como as notificações são recebidas.

O canal da Web está sempre ativado.

![notifications14](assets/notifications1.png)

O canal de e-mail, que depende da [configuração adequada do e-mail](/help/communities/email.md), fornece as mesmas configurações do canal da Web.

O canal de email está desativado por padrão.

![notifications2](assets/notifications2.png)

Pode ser ativado por um membro, mas ainda depende do email que está sendo configurado.

![notifications3](assets/notifications3.png)

## Visualizar notificações {#viewing-notifications}

### Notificações da Web {#web-notifications}

Um [assistente criou o site da comunidade](/help/communities/sites-console.md) agora inclui um link para o recurso `Notifications` na barra de cabeçalho do site acima do banner. Ao contrário das mensagens, as notificações são criadas para cada site da comunidade, enquanto as mensagens devem ser ativadas durante o processo de criação do site.

Ao visitar o site publicado, selecionar o link `Notifications` exibirá todas as notificações do membro.

![notificações4](assets/notifications4.png)

### Notificações por email {#email-notifications}

Quando o canal de email é ativado, o membro recebe um email que contém um link para o conteúdo da Web.

![notificações5](assets/notifications5.png)

## Personalizar notificações por email {#customize-email-notifications}

As organizações podem personalizar as notificações por email ao sobrepor[os modelos em **/libs/settings/community/models/email/html**.](/help/communities/client-customize.md#overlays)

Por exemplo, para modificar as notificações de menções por e-mail (para um componente de comunidades) adicione uma condição **if** para o verbo **menção** nos modelos dos componentes para os quais você ativou o suporte a **@menções**.

Para modificar o modelo de notificações por e-mail para @menção nos comentários do blog, coloque-o fora da caixa em: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

