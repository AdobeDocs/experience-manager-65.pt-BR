---
title: Sobrepor componentes das comunidades
description: Saiba mais sobre como sobrepor um componente padrão para que você possa alterar a aparência ou o comportamento de um componente globalmente, para todas as referências relativas ao componente.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 18376805-c2ed-439a-abc7-e9657afe8baf
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%
---
# Sobrepor componentes das comunidades {#overlay-communities-components}

A intenção de [sobrepor](/help/communities/client-customize.md#overlays) um componente padrão é alterar a aparência ou o comportamento de um componente globalmente, para todas as referências relativas ao componente. Depende da natureza do sling para resolver para a pasta /apps antes de pesquisar na pasta /libs. Assim, o caminho para o componente é idêntico ao caminho para o componente padrão, exceto que está na pasta /apps e não na pasta /libs.

## Exemplo {#example}

**Componente de comentários de sobreposição**

Suponha que você deseje modificar o recurso de comentário para que ele corresponda ao design do seu site, alterando o cabeçalho do comentário para que ele não exiba mais o avatar de nenhum comentário. As soluções para ocultar o avatar são usar o CSS ou, como descrito aqui, sobrepor o header.jsp na pasta de aplicativos para que o HTML que contém o avatar nunca seja enviado ao cliente.

Para sobrepor comentários, você deve:

1. [Criar página de comentários](/help/communities/overlay-create-comments-page.md)
1. [Criar nós](/help/communities/overlay-create-nodes.md)
1. [Alterar a aparência](/help/communities/overlay-alter-appearance.md)

**Sobrepor emails de notificações**

Suponha que você deseja personalizar a mensagem de notificações por email, você pode fazer isso [sobrepondo](/help/communities/client-customize.md#overlays) os modelos em `/libs/settings/community/templates/email/html`.

Por exemplo, suponha que você queira editar as menções notificações por email (para um componente das Comunidades específico onde o UGC é criado). Nesses casos, adicione uma condição **if** para o verbo **mention** nos modelos dos componentes para os quais você habilitou o suporte **@mentions**.

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

Para modificar o modelo de notificações por email para @mention em comentários de blog, coloque o modelo pronto para uso em: `/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en`
