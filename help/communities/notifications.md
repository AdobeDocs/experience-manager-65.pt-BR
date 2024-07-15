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

As notificações são semelhantes a [atividades](/help/communities/essentials-activities.md) e [assinaturas](/help/communities/subscriptions.md), pois podem resultar de:

* O conteúdo de postagem do membro.
* O membro que escolhe seguir outro membro.
* O membro optou por seguir tópicos, artigos e outras threads de conteúdo específicos.
* A marcação de membro (@mention) de outro membro da comunidade em um conteúdo gerado pelo usuário.

O que distingue as notificações das atividades e assinaturas é:

* Um link para a seção de notificações está sempre presente no cabeçalho de um site da comunidade:

   * As atividades exigem que a [função de fluxo de atividades](/help/communities/functions.md#activity-stream-function) seja incluída na estrutura do site da comunidade.
   * As assinaturas exigem [configuração de email](/help/communities/email.md).

* A implementação de notificações é feita por meio de canais dimensionáveis e conectáveis:

   * As atividades só estão disponíveis na Web.
   * As assinaturas só estão disponíveis por email.

A partir das Comunidades [FP1](/help/communities/deploy-communities.md#latestfeaturepack), os canais de notificação disponíveis são:

* O canal da Web, acessado usando o link `Notifications`.
* O canal de email, disponível quando o email é configurado corretamente.

Os canais futuros são móvel e desktop.

### Requisitos {#requirements}

**Configurar Email**

O email deve ser configurado para que o canal de email funcione.

Para obter instruções sobre como configurar emails, consulte [Configurando Email](/help/communities/analytics.md).

**Habilitar Seguimento**

Os componentes devem ser configurados para permitir o acompanhamento. Os recursos que permitem os seguintes itens são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca de arquivos](/help/communities/file-library.md) e [comentários](/help/communities/comments.md).

**Nota**:

* Os componentes usados na comunidade [modelos de site](/help/communities/sites.md) e [modelos de grupo](/help/communities/tools-groups.md) podem já estar configurados para seguir.

* Os perfis de membro já estão configurados para permitir que outros membros sigam.

## Notificações do Seguinte {#notifications-from-following}

![notificações](assets/notifications.png)

O botão **[!UICONTROL Seguir]** fornece um meio de seguir entradas como atividades, assinaturas e/ou notificações. Sempre que o botão **[!UICONTROL Seguir]** é selecionado, é possível ativar ou desativar uma seleção. A seleção `Email Subscriptions` está presente somente quando configurada.

Se qualquer método de acompanhamento for selecionado, o texto do botão será alterado para **[!UICONTROL Seguinte]**. Para maior comodidade, é possível selecionar `Unfollow All` para desligar todos os métodos.

O botão **[!UICONTROL Seguir]** será exibido:

* Ao exibir o perfil de outro membro.
* Em uma página principal de recursos, como fóruns, QnA e blogs:

   * Segue todas as atividades desse recurso geral.

* Para uma entrada específica, como um tópico do fórum, pergunta QnA ou artigo de blog:

   * Segue todas as atividades dessa entrada específica.

## Gerenciar configurações de notificação {#managing-notification-settings}

Ao selecionar o link Definições de Notificação na página Notificações, é possível que cada membro gerencie como as notificações são recebidas.

O canal da Web está sempre habilitado.

![notificações14](assets/notifications1.png)

O canal de email, que depende da [configuração adequada do email](/help/communities/email.md), fornece as mesmas configurações do canal Web.

O canal de email está desativado por padrão.

![notificações2](assets/notifications2.png)

Ela pode ser ativada por um membro, mas ainda depende do email estar configurado.

![notificações3](assets/notifications3.png)

## Visualizar notificações {#viewing-notifications}

### Notificações da Web {#web-notifications}

Um [site de comunidade criado pelo assistente](/help/communities/sites-console.md) agora inclui um link para o recurso `Notifications` na barra de cabeçalho do site acima do banner. Diferentemente das mensagens, as notificações são criadas para cada site da comunidade, enquanto as mensagens devem ser ativadas durante o processo de criação do site.

Ao visitar o site publicado, selecionar o link `Notifications` exibirá todas as notificações para o membro.

![notificações4](assets/notifications4.png)

### Notificações por email {#email-notifications}

Quando o canal de email está ativado, o membro recebe um email que contém um link para o conteúdo na Web.

![notificações5](assets/notifications5.png)

## Personalizar notificações por email {#customize-email-notifications}

As organizações podem personalizar as notificações por email [sobrepondo](/help/communities/client-customize.md#overlays) os modelos em **/libs/settings/community/templates/email/html**.

Por exemplo, para modificar as notificações por email de menções (para um componente de comunidades), adicione uma condição **if** para o verbo **mention** nos modelos dos componentes para os quais você habilitou o suporte **@mentions**.

Para modificar o modelo de notificações por email para @mention nos comentários do blog, coloque o modelo pronto para uso em: **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
