---
title: Fundamentos Tally
description: Saiba como Tally é uma classe abstrata que fornece um método padrão de coletar feedback dos membros sobre como eles valorizam produtos e serviços específicos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Fundamentos Tally {#tally-essentials}

Tally é uma classe abstrata que fornece um método padrão de coletar feedback dos membros sobre como eles valorizam produtos e serviços específicos. Não há suporte para comentários anônimos. Os visitantes do site devem se registrar e fazer logon para participar e fazer logon para alterar seus comentários. O requisito para fazer logon facilita a moderação e aumenta o valor do feedback, evitando várias publicações.

Um componente tally personalizado pode ser criado estendendo a classe tally abstrata.

[Curtir](essentials-liking.md) é uma implementação de tally que é uma forma simples de expressar uma opinião positiva.

[Votação](essentials-voting.md) é uma implementação de tally que é uma forma simples de expressar uma opinião positiva ou negativa.

[Classificação](rating-basics.md) é uma implementação do tally que usa um sistema estelar para expressar uma variedade de opiniões, de positivas a negativas.

A partir do AEM 6.1, o componente de pesquisa não está mais disponível.

[Resenhas](reviews-basics.md) é um componente SCF híbrido de [comentários](essentials-comments.md) e [avaliação](rating-basics.md).

## Essentials para o lado do cliente {#essentials-for-client-side}

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [APIs Tally](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Endpoints Tally](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acessar tabelas publicadas (UGC) {#accessing-posted-tallies-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir do AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
