---
title: Fundamentos do blog
description: Saiba como adicionar o recurso Blog a uma página para que os membros da comunidade conectados possam postar artigos no blog.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 2%

---

# Fundamentos do blog {#blog-essentials}

Desde o AEM 6.1 Communities, um blog é uma atividade comunitária. Agora os artigos de blog são publicados a partir do ambiente de publicação, onde anteriormente os artigos de blog só podiam ser criados no ambiente de criação e publicados.

Artigos de blog agora podem ser criados por qualquer membro da comunidade, a menos que restritos a membros privilegiados.

Esta página fornece as informações essenciais para trabalhar com o recurso de blog.

>[!NOTE]
>
>A infraestrutura subjacente do recurso de blog é o recurso de diário.

## Essentials para o lado do cliente {#essentials-for-client-side}

O recurso de blog é composto por dois componentes principais que estão disponíveis ao adicionar a [função de Blog](/help/communities/functions.md#blog-function) ou ao adicionar os componentes a uma página no modo de edição do autor.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>consulte <a href="/help/communities/blog-feature.md">Recurso de Blog</a></td>
  </tr>
 </tbody>
</table>

### Barra lateral do blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**incluível**](/help/communities/scf.md#add-or-include-a-communities-component) | Não |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **modelos** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propriedades** | consulte [Recurso de Blog](/help/communities/blog-feature.md) |

* [Personalizações do lado do cliente](/help/communities/client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do blog](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Pontos de Extremidade do Blog](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](/help/communities/server-customize.md)

### Função do blog {#blog-function}

Uma estrutura de site de comunidade que inclui a [função de Blog](/help/communities/functions.md#blog-function) tem os componentes `Blog` e `Blog Sidebar` configurados. A função Blog dá suporte à identificação de um [grupo de usuários membro privilegiado](/help/communities/users.md#privileged-members-group).

### Acessar entradas do blog (UGC) {#accessing-blog-entries-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderando Conteúdo Gerado por Usuário](/help/communities/moderate-ugc.md).

Desde o AEM 6.1 Communities, o uso de um [armazenamento comum](/help/communities/working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](/help/communities/srp.md) - introdução e visão geral do uso do repositório.
* [Fundamentos do SRP e do UGC](/help/communities/srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](/help/communities/accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração de SocialUtils](/help/communities/socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.

## Editor primário {#primary-publisher}

Quando a implantação é um farm de publicação, é necessário identificar um publicador principal que pesquisa os artigos agendados para publicação.

Consulte [Publicador principal](/help/communities/deploy-communities.md#primary-publisher) para obter mais detalhes.

## Permitir mídia avançada {#allowing-rich-media}

A plataforma AEM bloqueia links de outros sites para impedir ataques XSS, conforme descrito em

* [Protect contra Scripts entre sites (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partir do AEM 6.2, as modificações que anteriormente precisavam ser feitas manualmente estão incluídas no arquivo de configuração padrão do AntiSamy.

A mídia avançada está incorporada em um artigo de blog ao selecionar o ícone `Embed Media from External Sites`:

![mídia](assets/media-icon.png)
