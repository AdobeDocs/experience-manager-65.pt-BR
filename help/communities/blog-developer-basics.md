---
title: Fundamentos do blog
seo-title: Blog Essentials
description: Visão geral do blog
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
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

O recurso de blog é composto por dois componentes principais que estão disponíveis ao adicionar o [Função de blog](/help/communities/functions.md#blog-function) ou adicionando os componentes a uma página no modo de edição do autor.

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
   <td>consulte <a href="/help/communities/blog-feature.md">Recurso de blog</a></td>
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
| **propriedades** | consulte [Recurso de blog](/help/communities/blog-feature.md) |

* [Personalizações do lado do cliente](/help/communities/client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Endpoints do blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](/help/communities/server-customize.md)

### Função do blog {#blog-function}

Uma estrutura de site da comunidade que inclui o [Função de blog](/help/communities/functions.md#blog-function) terá configurado `Blog` e `Blog Sidebar` componentes. A função Blog suporta a identificação de um [grupo de usuários membro privilegiado](/help/communities/users.md#privileged-members-group).

### Acessar entradas do blog (UGC) {#accessing-blog-entries-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

A partir do AEM 6.1 Communities, o uso de um [armazenamento comum](/help/communities/working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte :

* [Visão geral do provedor de recursos de armazenamento](/help/communities/srp.md) - introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](/help/communities/srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acesso ao UGC com SRP](/help/communities/accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração de SocialUtils](/help/communities/socialutils.md) - mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.

## Editor primário {#primary-publisher}

Quando a implantação é um farm de publicação, é necessário identificar um editor principal que sondará os artigos agendados para publicação.

Consulte [Editor primário](/help/communities/deploy-communities.md#primary-publisher) para obter mais detalhes.

## Permitir mídia avançada {#allowing-rich-media}

A plataforma AEM bloqueia links de outros sites para impedir ataques XSS, conforme descrito em

* [Protect contra Scripts entre sites (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partir do AEM 6.2, as modificações que anteriormente precisavam ser feitas manualmente estão incluídas no arquivo de configuração padrão do AntiSamy.

A mídia avançada é incorporada em um artigo de blog ao selecionar o `Embed Media from External Sites` ícone:

![mídia](assets/media-icon.png)
