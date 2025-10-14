---
title: Personalização e direcionamento de conteúdo
description: Saiba como o Adobe Experience Manager 6.5 pode criar conteúdo personalizado.
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 36%

---

# Personalização e direcionamento de conteúdo {#personalization}

## Personalização e direcionamento de conteúdo {#personalization-and-content-targeting}

O AEM fornece uma estrutura de ferramentas para a criação de conteúdo direcionado e a apresentação de experiências personalizadas.

## Modo de direcionamento {#targeting-mode}

[Crie conteúdo direcionado usando o modo Direcionar do AEM. &#x200B;](/help/sites-authoring/content-targeting-touch.md) O modo de direcionamento e o componente do Target fornecem ferramentas para criar conteúdo para as experiências das suas atividades de marketing.

## Atividades {#activities}

As atividades definem e organizam seus esforços de marketing. As atividades abrangem os públicos que você está direcionando e o período em que o direcionamento é aplicado.

Por exemplo, o catálogo de produtos We.Retail inclui teasers que chamam a atenção para produtos sazonais. A atividade Esportes de verão define os segmentos de marketing aos quais os teasers se destinam durante os meses de verão.

As atividades também identificam o [mecanismo de direcionamento](/help/sites-authoring/personalization.md#targeting-engine) que suas páginas usam.

Use o [console de Atividades](/help/sites-authoring/activitylib.md) para criar e gerenciar as atividades das suas marcas. Você também pode criar atividades ao [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md).

## Experiências {#experiences}

Para cada atividade, você define uma ou mais experiências que identificam os públicos que estão sendo direcionados. O AEM permite que você controle o conteúdo que compreende cada experiência.

Os públicos-alvo são baseados em segmentos de marketing criados no AEM ou no Adobe Target. Quando um visitante abre uma página da Web, a lógica da página determina o público-alvo ao qual ele pertence e exibe o conteúdo que você criou para esse público-alvo.

Por exemplo, uma atividade define experiências para dois públicos separados: mulheres com mais de 30 anos e mulheres com menos de 30 anos. A página Feminino do site We.Retail exibe produtos diferentes para cada experiência.

Você define experiências para uma atividade. Você pode usar o [console de Atividades](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) ou o [modo de Direcionamento](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) para adicionar experiências a uma atividade.

## Ofertas {#offers}

Uma oferta é um conteúdo que aparece em um local em uma página para uma experiência. Use diferentes ofertas para experiências diferentes para maximizar a eficácia do conteúdo para seus públicos-alvo.

Por exemplo, a página Feminino do site de amostra We.Retail pode usar ofertas como a imagem do teaser que aparece na parte superior da página. Uma oferta diferente é usada como teaser para a experiência Feminino acima de 30 e para a experiência Feminino abaixo de 30.

Use o [Console de ofertas](/help/sites-authoring/offerlib.md) para criar ofertas que você possa usar em várias experiências. Crie ofertas de uso único ou adicione ofertas de uma biblioteca de ofertas ao [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md).

## Mecanismo de direcionamento {#targeting-engine}

O mecanismo de direcionamento é o mecanismo que orienta a lógica do conteúdo direcionado. [Atividades](/help/sites-authoring/activitylib.md) são configuradas para usar um dos dois mecanismos de segmentação disponíveis: AEM e Adobe Target.

### AEM {#aem}

O AEM fornece um mecanismo de direcionamento integrado que processa solicitações de página e determina o conteúdo a ser exibido. Ao usar o mecanismo de direcionamento do AEM, você está limitado a usar segmentos criados no AEM para definir os públicos das suas experiências.

### Adobe Target {#adobe-target}

O mecanismo de direcionamento do Adobe Target faz com que as informações coletadas das visitas às páginas sejam rastreadas no Adobe Target.

* Ao usar esse mecanismo de direcionamento, você utilizará os segmentos importados do Adobe Target para definir os públicos-alvo das suas experiências.
* As atividades que usam o mecanismo do Adobe Target são [sincronizadas com o Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Você pode usar esse mecanismo quando tiver [integrado com o Adobe Target](/help/sites-administering/opt-in.md).
