---
title: Componentes de comunidades de sobreposição
seo-title: Componentes de comunidades de sobreposição
description: Componentes de comunidades de sobreposição
seo-description: Componentes de comunidades de sobreposição
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Componentes de comunidades de sobreposição {#overlay-communities-components}

A intenção de [sobrepor](/help/communities/client-customize.md#overlays) um componente padrão é alterar a aparência ou o comportamento de um componente globalmente, para todas as referências relativas ao componente. Ele depende da natureza do sling para resolver a pasta /apps antes de pesquisar na pasta /libs. Assim, o caminho para o componente é idêntico ao caminho para o componente padrão, exceto que está na pasta /apps e não na pasta /libs.

## Exemplo {#example}

**Componente de comentários de sobreposição**

Suponha que você queira modificar o recurso de comentário para que ele corresponda ao design do seu site, alterando o cabeçalho do comentário para que ele não exiba mais o avatar para qualquer comentário. As soluções para ocultar o avatar estão usando o CSS ou, conforme descrito aqui, sobrepondo o header.jsp na pasta de aplicativos para que o HTML que contém o avatar nunca seja enviado para o cliente.

Para sobrepor comentários, você precisará:

1. [Página de comentários](/help/communities/overlay-create-comments-page.md)
1. [Criar nós](/help/communities/overlay-create-nodes.md)
1. [Alterar a aparência](/help/communities/overlay-alter-appearance.md)

**E-mails de notificações de sobreposição**

Suponha que você queira personalizar a mensagem das notificações por email, você pode fazer isso [sobrepondo](/help/communities/client-customize.md#overlays) os modelos em **/libs/settings/community/models/email/html**.

Por exemplo, para modificar as notificações por e-mail de menções (para um componente de comunidades específicas onde o ugc é criado), adicione uma condição **if** para a **menção** verbo nos modelos dos componentes para os quais você habilitou o suporte a **@menções** .

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar o modelo de notificações por e-mail para @menção nos comentários do blog, coloque-o fora da caixa em: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
