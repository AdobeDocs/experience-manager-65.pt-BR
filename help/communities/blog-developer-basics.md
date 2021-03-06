---
title: Blog Essentials
seo-title: Blog Essentials
description: Visão geral do blog
seo-description: Visão geral do blog
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Blog Essentials {#blog-essentials}

Desde AEM 6.1 Communities, um blog é uma atividade comunitária. Os artigos de blog agora são publicados a partir do ambiente de publicação, onde anteriormente os artigos de blog só podiam ser criados no ambiente do autor e publicados.

Os artigos de blog agora podem ser criados por qualquer membro da comunidade, a menos que restritos a membros privilegiados.

Esta página fornece as informações essenciais para trabalhar com o recurso de blog.

>[!NOTE]
>
>A infraestrutura subjacente do recurso de blog é o recurso do journal.

## Essentials for Client-Side {#essentials-for-client-side}

O recurso de blog é composto de dois componentes principais que estão disponíveis ao adicionar a [função de blog](/help/communities/functions.md#blog-function) ou ao adicionar os componentes a uma página no modo de edição do autor.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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
| [**inclusivo**](/help/communities/scf.md#add-or-include-a-communities-component) | Não |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **modelos** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propriedades** | consulte [Recurso de blog](/help/communities/blog-feature.md) |

* [Personalizações do cliente](/help/communities/client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API do blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Pontos de extremidade do blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizações do servidor](/help/communities/server-customize.md)

### Função do blog {#blog-function}

Uma estrutura de site da comunidade que inclui a [função Blog](/help/communities/functions.md#blog-function) terá os componentes `Blog` e `Blog Sidebar` configurados. A função Blog suporta a identificação de um [grupo de usuários membro privilegiado](/help/communities/users.md#privileged-members-group).

### Acesso às entradas do blog (UGC) {#accessing-blog-entries-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

A partir AEM Comunidades 6.1, o uso de uma [loja comum](/help/communities/working-with-srp.md) para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte :

* [Visão geral](/help/communities/srp.md)  do provedor de recursos do armazenamento - introdução e visão geral do uso do repositório.
* [SRP e UGC Essentials](/help/communities/srp-and-ugc.md)  - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com diretrizes de codificação do SRP](/help/communities/accessing-ugc-with-srp.md) .
* [Refatoração](/help/communities/socialutils.md)  do SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

## Editor principal {#primary-publisher}

Quando a implantação for um farm de publicação, será necessário identificar um editor principal que pesquisará artigos programados para publicação.

Consulte [Editor principal](/help/communities/deploy-communities.md#primary-publisher) para obter mais detalhes.

## Permitir mídia avançada {#allowing-rich-media}

A plataforma AEM bloqueia links de outros sites para impedir ataques XSS, conforme descrito em

* [Protect contra script entre sites (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partir do AEM 6.2, as modificações anteriormente necessárias para serem feitas manualmente são incluídas no arquivo de configuração padrão do AntiSamy.

A mídia avançada é incorporada em um artigo de blog selecionando o ícone `Embed Media from External Sites` :

![media](assets/media-icon.png)

