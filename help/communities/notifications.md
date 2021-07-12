---
title: Notificações de comunidades
seo-title: Notificações de comunidades
description: A AEM Communities tem notificações que exibem eventos de interesse para o membro da comunidade que fez logon
seo-description: A AEM Communities tem notificações que exibem eventos de interesse para o membro da comunidade que fez logon
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---

# Notificações de comunidades {#communities-notifications}

## Visão geral {#overview}

O AEM Communities fornece uma seção de notificações que exibe eventos de interesse para o membro da comunidade com logon assinado.

As notificações são semelhantes a [atividades](/help/communities/essentials-activities.md) e [assinaturas](/help/communities/subscriptions.md), pois podem resultar de:

* O conteúdo de publicação do membro.
* O membro que escolheu seguir outro membro.
* O membro opta por seguir tópicos específicos, artigos e outros threads de conteúdo.
* A marcação de membro (@menção) de outro membro da comunidade em um conteúdo gerado pelo usuário.

O que distingue notificações de atividades e assinaturas é:

* Um link para a seção de notificações está sempre presente no cabeçalho de um site da comunidade:

   * As atividades exigem que a [função de fluxo de atividade](/help/communities/functions.md#activity-stream-function) seja incluída na estrutura do site da comunidade.
   * As assinaturas exigem [configuração de email](/help/communities/email.md).

* A implementação das notificações é por meio de canais escaláveis e conectáveis:

   * As atividades só estão disponíveis na Web.
   * As assinaturas só estão disponíveis por email.

A partir das Comunidades [FP1](/help/communities/deploy-communities.md#latestfeaturepack), os canais de notificação disponíveis são:

* O canal da Web, acessado usando o link `Notifications`.
* O canal de email, disponível quando o email está configurado corretamente.

Os canais futuros são dispositivos móveis e desktop.

### Requisitos {#requirements}

**Configurar Email**

O email deve ser configurado para que o canal de email das notificações funcione.

Para obter instruções sobre como configurar o email, consulte [Configuração do email](/help/communities/analytics.md).

**Habilitar Seguir**

Os componentes devem ser configurados para ativar o seguinte. Os recursos que permitem o seguinte são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca de arquivos](/help/communities/file-library.md) e [comentários](/help/communities/comments.md).

**Nota**:

* Os componentes usados na comunidade [modelos de site](/help/communities/sites.md) e [modelos de grupo](/help/communities/tools-groups.md) podem já estar configurados para serem seguidos.

* Os perfis de membro já estão configurados para permitir que outros membros sigam.

## Notificações do seguinte {#notifications-from-following}

![notificações](assets/notifications.png)

O botão **[!UICONTROL Follow]** fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Sempre que o botão **[!UICONTROL Follow]** é selecionado, é possível ativar ou desativar uma seleção. A seleção `Email Subscriptions` só está presente quando configurada.

Se qualquer método do seguinte for selecionado, o texto do botão será alterado para **[!UICONTROL Seguindo]**. Para maior comodidade, é possível selecionar `Unfollow All` para desligar todos os métodos.

O botão **[!UICONTROL Follow]** será exibido:

* Ao visualizar o perfil de outro membro.
* Em uma página principal do recurso, como fóruns, QnA e blogs:

   * Segue todas as atividades para esse recurso geral.

* Para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog:

   * Segue todas as atividades da entrada específica.

## Gerenciando configurações de notificação {#managing-notification-settings}

Ao selecionar o link Configurações de notificação na página Notificações , é possível que cada membro gerencie como as notificações são recebidas.

O canal da Web é sempre ativado.

![notificações14](assets/notifications1.png)

O canal de email, que depende da [configuração adequada do email](/help/communities/email.md), fornece as mesmas configurações do canal da Web.

O canal de email está desativado por padrão.

![notifications2](assets/notifications2.png)

Ele pode ser ativado por um membro, mas ainda depende da configuração do email.

![notifications3](assets/notifications3.png)

## Visualizar notificações {#viewing-notifications}

### Notificações da Web {#web-notifications}

Um [assistente criado no site da comunidade](/help/communities/sites-console.md) agora inclui um link para o recurso `Notifications` na barra de cabeçalho do site acima do banner. Ao contrário das mensagens, as notificações são criadas para cada site da comunidade, enquanto as mensagens devem ser ativadas durante o processo de criação do site.

Ao visitar o site publicado, selecionar o link `Notifications` exibirá todas as notificações do membro.

![notificações4](assets/notifications4.png)

### Notificações por email {#email-notifications}

Quando o canal de email está ativado, o membro recebe um email que contém um link para o conteúdo na Web.

![notificações5](assets/notifications5.png)

## Personalizar notificações por email {#customize-email-notifications}

As organizações podem personalizar as notificações por email ao [sobrepor](/help/communities/client-customize.md#overlays) os modelos em **/libs/settings/community/templates/email/html**.

Por exemplo, para modificar as menções e-mails de notificações (para um componente de comunidades), adicione uma condição **if** para verbo **mention** nos modelos dos componentes para os quais você ativou o suporte **@menções**.

Para modificar o modelo de notificações por email para @mention em comentários do blog, coloque o modelo pronto para uso em: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
