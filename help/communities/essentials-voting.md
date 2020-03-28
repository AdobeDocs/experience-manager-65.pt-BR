---
title: Essenciais de votação
seo-title: Essenciais de votação
description: Visão geral do componente de votação
seo-description: Visão geral do componente de votação
uuid: ed0a771d-1c14-4fbf-ab6a-a028e5ee2e2a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 1a947a06-6a5c-4be9-b2fa-e5fa809ff3b8
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Essenciais de votação {#voting-essentials}

O componente de votação, uma subclasse [tally](tally.md) , é uma ferramenta útil que permite que os membros classifiquem um conteúdo específico simplesmente selecionando setas para cima ou para baixo para indicar sua opinião.

É permitido colocar várias instâncias de um componente de votação na mesma página; cada instância deve ser configurada com uma `tally name` propriedade exclusiva.

Não se apoia o envio anônimo de uma votação. Os visitantes do site devem se registrar e fazer logon para participar da votação apenas uma vez. Os visitantes conectados (membros) podem alterar seus votos a qualquer momento.

## Essenciais para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/votação</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Sim - as propriedades são editáveis no <i>modo </i>de design</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.vote</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td><p>Consulte, <a href="voting.md">Usando Votação</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [Tally APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Pontos de extremidade totais](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Acessar a votação publicada (UGC) {#accessing-posted-voting-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo](moderate-ugc.md)gerado pelo usuário.

A partir das comunidades do AEM 6.1, o uso de uma loja [](working-with-srp.md) comum para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md) do provedor de recursos do Armazenamento - introdução e visão geral do uso do repositório
* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos de utilitários SRP
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação
* [Refatoração](socialutils.md) do SocialUtils - mapeamento de métodos de utilitário obsoletos para os métodos atuais do utilitário SRP

