---
title: Componentes de comunidades de sobreposição
seo-title: Overlay communities components
description: Componentes de comunidades de sobreposição
seo-description: Overlay communities components
uuid: 872f7006-959a-49d2-b025-3a5abb7c6dca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 502c0916-6c54-440c-be8c-eae56001fa26
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Componentes de comunidades de sobreposição {#overlay-communities-components}

A intenção de [sobreposição](/help/communities/client-customize.md#overlays) um componente padrão é alterar a aparência ou o comportamento de um componente globalmente, para todas as referências relativas ao componente. Ele depende da natureza do sling para resolver para a pasta /apps antes de pesquisar na pasta /libs. Assim, o caminho para o componente é idêntico ao caminho para o componente padrão, exceto que está na pasta /apps e não na pasta /libs.

## Exemplo {#example}

**Componente sobrepor comentários**

Suponha que você gostaria de modificar o recurso de comentário para que ele corresponda ao design do seu site, alterando o cabeçalho do comentário para que ele não exiba mais o avatar para qualquer comentário. As soluções para ocultar o avatar estão usando o CSS ou, conforme descrito aqui, sobrepondo o header.jsp na pasta de aplicativos para que o HTML contendo o avatar nunca seja enviado ao cliente.

Para sobrepor comentários, você precisará:

1. [Página Comentários](/help/communities/overlay-create-comments-page.md)
1. [Criar nós](/help/communities/overlay-create-nodes.md)
1. [Alterar a aparência](/help/communities/overlay-alter-appearance.md)

**Emails de notificações de sobreposição**

Suponha que você deseja personalizar a mensagem das notificações por email, e pode fazer isso [sobreposição](/help/communities/client-customize.md#overlays) os modelos em **/libs/settings/community/templates/email/html**.

Por exemplo, para modificar as notificações de e-mail das menções (para um componente de comunidades específicas onde o ugc é criado), adicione um **if** condição para verbo **menção** nos modelos dos componentes para os quais você ativou a variável **@menções** suporte.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar o modelo de notificações por email para @mention em comentários do blog, coloque o modelo pronto para uso em: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
