---
title: Personalização e direcionamento de conteúdo
seo-title: Personalization and Content Targeting
description: Saiba como o AEM pode criar conteúdo personalizado
seo-description: Learn how AEM can create personalized content
uuid: 3a1aaa3d-5f57-4fb7-a4be-523f0d274b79
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 850da0da-f7c3-4dd7-bb06-404c14a2a791
exl-id: be34760a-875b-419d-9fa4-2359b314a3b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 87%

---

# Personalização e direcionamento de conteúdo {#personalization}

## Personalização e direcionamento de conteúdo {#personalization-and-content-targeting}

O AEM fornece uma estrutura de ferramentas para criar conteúdo direcionado e apresentar experiências personalizadas.

## Modo Direcionar {#targeting-mode}

[Crie conteúdo direcionado usando o modo Direcionar do AEM. ](/help/sites-authoring/content-targeting-touch.md) O modo de direcionamento e o componente do Target fornecem ferramentas para criar conteúdo para as experiências das suas atividades de marketing.

## Atividades {#activities}

Atividades definem e organizam seus esforços de marketing. Elas abrangem os públicos que você está direcionando e o período em que a o direcionamento é aplicado.

Por exemplo, o catálogo de produtos We.Retail inclui teasers que focalizam a atenção em produtos sazonais. A atividade Esportes de verão define os segmentos de marketing direcionados pelos teasers durante os meses de verão.

Atividades também identificam o [mecanismo de direcionamento](/help/sites-authoring/personalization.md#targeting-engine) usado por suas páginas.

Use o [console Atividades](/help/sites-authoring/activitylib.md) para criar e gerenciar as atividades das suas marcas. Você também pode criar atividades ao [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md).

## Experiências {#experiences}

Para cada atividade, você define uma ou mais experiências que identificam os públicos que estão sendo direcionados. O AEM permite que você controle o conteúdo que compreende cada experiência.

Os públicos se baseiam em segmentos de marketing criados no AEM ou no Adobe Target. Quando um visitante abre uma página da Web, a lógica da página determina o público ao qual ele pertence e exibe o conteúdo que você criou para esse público.

Por exemplo, uma atividade define experiências para dois públicos separados: mulheres com mais de 30 anos e mulheres com menos de 30 anos. A página Women&#39;s do site We.Retail exibe produtos diferentes para cada experiência.

Você define experiências para uma atividade. É possível usar o [console Atividades](/help/sites-authoring/activitylib.md#adding-editing-an-activity-using-the-activities-console) ou o [modo Direcionar](/help/sites-authoring/content-targeting-touch.md#adding-and-removing-experiences-using-targeting-mode) para adicionar experiências a uma atividade.

## Ofertas {#offers}

Uma oferta é um conteúdo que aparece em uma localização em uma página para uma experiência. Use ofertas diferentes para experiências diferentes para maximizar a eficácia do conteúdo para os seus públicos.

Por exemplo, a página Women&#39;s do site de exemplo We.Retail pode usar ofertas como a imagem de teaser que aparece na parte superior da página. Uma oferta diferente é usada como teaser para a experiência Mulheres acima de 30 anos e para a experiência Mulheres com menos de 30 anos.

Use o [console Ofertas](/help/sites-authoring/offerlib.md) para criar ofertas que você possa usar em várias experiências. Crie ofertas de uso único ou adicione ofertas de uma biblioteca de ofertas ao [criar conteúdo direcionado](/help/sites-authoring/content-targeting-touch.md).

## Mecanismo de direcionamento {#targeting-engine}

O mecanismo de direcionamento é o mecanismo que orienta a lógica do conteúdo segmentado. [Atividades](/help/sites-authoring/activitylib.md) são configuradas para usar um dos dois mecanismos de segmentação disponíveis: AEM e Adobe Target.

### AEM {#aem}

O AEM fornece um mecanismo de direcionamento integrado que processa solicitações de página e determina o conteúdo a ser exibido. Ao usar o mecanismo de direcionamento do AEM, você está limitado a usar segmentos criados no AEM para definir os públicos das suas experiências.

### Adobe Target {#adobe-target}

O mecanismo de direcionamento do Adobe Target faz com que as informações coletadas das visitas às páginas sejam rastreadas no Adobe Target.

* Ao usar esse mecanismo de direcionamento, você usa segmentos importados do Adobe Target para definir os públicos das suas experiências.
* As atividades que usam o mecanismo do Adobe Target são [sincronizadas com o Target](/help/sites-authoring/activitylib.md#synchronizing-activities-with-adobe-target).

Você pode usar esse mecanismo quando tiver [integrado ao Adobe Target](/help/sites-administering/opt-in.md).
