---
title: Tally Essentials
seo-title: Tally Essentials
description: Visão geral da classe Tally
seo-description: Visão geral da classe Tally
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally é uma classe abstrata que fornece um método padrão para coletar feedback dos membros sobre como eles valorizam produtos e serviços específicos. Não há suporte para feedback anônimo. O visitante do site deve se registrar e fazer logon para participar e fazer logon para alterar seus comentários. O requisito para fazer logon facilita a moderação e aumenta o valor do feedback, evitando várias publicações.

Um componente tally personalizado pode ser criado ao estender a classe tally abstrata.

[](essentials-liking.md) Provavelmente, é uma implementação de uma aliança que é uma forma simples de expressar uma opinião positiva.

[A ](essentials-voting.md) Votingança é uma implementação do tally que é uma forma simples de expressar uma opinião positiva ou negativa.

[A ](rating-basics.md) Ratingis é uma implementação do tally que usa um sistema de estrelas para expressar uma gama de opiniões de positivas a negativas.

A partir do AEM 6.1, o componente de pesquisa não estará mais disponível.

[A ](reviews-basics.md) Reviews é um componente do SCF que é um híbrido de  [](essentials-comments.md) comentários e  [classificações](rating-basics.md).

## Essentials for Client-Side {#essentials-for-client-side}

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [Tally APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Pontos de extremidade totais](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Acessar Conversas Publicadas (UGC) {#accessing-posted-tallies-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM Comunidades 6.1, o uso de uma [loja comum](working-with-srp.md) para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md)  do provedor de recursos do armazenamento - Introdução e visão geral do uso do repositório.
* [SRP e UGC Essentials](srp-and-ugc.md)  - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com diretrizes de codificação SRP](accessing-ugc-with-srp.md) .
* [Refatoração](socialutils.md)  do SocialUtils - mapeamento de métodos de utilitário obsoletos para os métodos atuais do utilitário SRP.

