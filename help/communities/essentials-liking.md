---
title: Noções básicas sobre curtir
seo-title: Noções básicas sobre curtir
description: Visão geral do componente de curtir
seo-description: Visão geral do componente de curtir
uuid: 89f16859-c901-4090-8e16-363b95c508de
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f176c42b-b16b-42c9-af22-4b6421de5a90
pagetitle: Liking Essentials
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---


# Como curtir o Essentials {#liking-essentials}

O componente de curtir, uma subclasse [tally](tally.md), é uma ferramenta útil que permite que os membros expressem uma opinião positiva sobre um determinado conteúdo simplesmente selecionando o ícone do coração.

É permitido colocar várias instâncias de um componente de curtir na mesma página; cada instância deve ser configurada com uma propriedade exclusiva `tally name`.

Não há suporte para a publicação anônima de um curtir. Os visitantes do site devem se registrar e fazer logon para participar do curtidas. O visitante conectado (membro) pode alternar como ligado e desligado a qualquer momento.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/curtir</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Sim - as propriedades são editáveis no modo <i>design </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.liking</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td><p> /libs/social/tally/components/hbs/liking/liking.hbs<br /> /libs/social/tally/components/hbs/liking/activity-icon.hbs<br /> /libs/social/tally/components/hbs/liking/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/liking/clientlibs/likingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td><p>Consulte <a href="liking.md">Usando Curtir</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [Tally APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Pontos de extremidade totais](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Acessando a Votação Publicada (UGC) {#accessing-posted-voting-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM Comunidades 6.1, o uso de uma [loja comum](working-with-srp.md) para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md)  do provedor de recursos do armazenamento - introdução e visão geral do uso do repositório.
* [SRP e UGC Essentials](srp-and-ugc.md)  - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com diretrizes de codificação do SRP](accessing-ugc-with-srp.md) .
* [Refatoração](socialutils.md)  do SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

