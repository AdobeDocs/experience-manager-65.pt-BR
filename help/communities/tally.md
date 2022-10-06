---
title: Tally Essentials
seo-title: Tally Essentials
description: Visão geral da classe Tally
seo-description: Tally class overview
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Tally Essentials {#tally-essentials}

Tally é uma classe abstrata que fornece um método padrão para coletar feedback dos membros sobre como eles valorizam produtos e serviços específicos. Não há suporte para feedback anônimo. O visitante do site deve se registrar e fazer logon para participar e fazer logon para alterar seus comentários. O requisito para fazer logon facilita a moderação e melhora o valor do feedback, impedindo várias publicações.

Um componente tally personalizado pode ser criado ao estender a classe tally abstrata.

[Curtir](essentials-liking.md) é uma implementação da tally que é uma forma simples de expressar uma opinião positiva.

[Votação](essentials-voting.md) é uma implementação de uma tally que é uma forma simples de expressar uma opinião positiva ou negativa.

[Classificação](rating-basics.md) é uma implementação de uma contagem que utiliza um sistema estelar para expressar uma gama de opiniões de positiva para negativa.

A partir do AEM 6.1, o componente de pesquisa não estará mais disponível.

[Resenhas](reviews-basics.md) é um componente do SCF que é híbrido de [comentários](essentials-comments.md) e [classificação](rating-basics.md).

## Fundamentos para o lado do cliente {#essentials-for-client-side}

* [Personalizações do lado do cliente](client-customize.md)

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [Tally APIs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoints Tally](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acesso a Listas Publicadas (UGC) {#accessing-posted-tallies-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM 6.1 Comunidades, uso de um [loja comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Princípios básicos de SRP e UGC](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais.
