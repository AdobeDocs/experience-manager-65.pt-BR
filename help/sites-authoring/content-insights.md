---
title: Content Insight
description: O Insight de conteúdo fornece informações sobre o desempenho da página usando a análise da Web e a recomendação de SEO
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---

# Content Insight{#content-insight}

O Insight de conteúdo fornece informações sobre o desempenho da página usando análises da Web e recomendações de SEO. Use o Insight de conteúdo para tomar decisões sobre como modificar páginas ou saber como as alterações anteriores alteraram o desempenho. Para cada página criada, você pode abrir o Insight de conteúdo para analisar a página.

![chlimage_1-311](assets/chlimage_1-311.png)

O layout da página Insight de conteúdo é alterado para se adequar às dimensões e à orientação da tela do dispositivo que você está usando.

## Dados do relatório

A página Insight de conteúdo inclui relatórios que usam dados do Adobe SiteCatalyst, Adobe Target, Adobe Social e BrightEdge:

* SiteCatalyst: estão disponíveis relatórios para as seguintes métricas:

   * Exibições da página
   * Tempo médio gasto na página
   * Fontes

* Target: relatórios sobre as atividades de campanha para as quais a página inclui ofertas.
* BrightEdge: Relatórios sobre os recursos da página que melhoram a visibilidade da página para os mecanismos de pesquisa e recomenda os recursos que devem ser implementados.

Consulte [Abrindo o Analytics e o Recommendations para uma Página](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page).

## Período da geração de relatórios

Os relatórios mostram dados de um período de tempo que você controla. Quando você ajusta o período do relatório, os relatórios são atualizados automaticamente com os dados desse período. As dicas visuais indicam o tempo em que as versões da página foram alteradas, para que você possa comparar o desempenho de cada versão.

>[!NOTE]
>
>A linha do tempo do painel Insight de Conteúdo está em `GMT`.

Você também pode especificar a granularidade dos dados relatados, por exemplo, ver dados diários, semanais, mensais ou anuais.

Consulte [Alterando o Período do Relatório](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period).

>[!NOTE]
>
>Os relatórios de Insights de conteúdo exigem que o administrador tenha integrado o AEM ao SiteCatalyst, Target e BrightEdge. Consulte [Integração com o SightCatalyst](/help/sites-administering/adobeanalytics.md), [Integração com o Adobe Target](/help/sites-administering/target.md) e [Integração com o BrightEdge](/help/sites-administering/brightedge.md).

## O Relatório de Visões {#the-views-report}

O relatório Exibições inclui os seguintes recursos para avaliar o tráfego da página:

* O número total de exibições de uma página para o período do relatório.
* Um gráfico do número de exibições no período do relatório:

   * Total de visualizações.
   * Visitantes únicos.

![chlimage_1-312](assets/chlimage_1-312.png)

## O relatório Envolvido médio da página {#the-page-average-engaged-report}

O relatório Média de página ativada inclui os seguintes recursos para avaliar a eficácia da página:

* O tempo médio pelo qual a página permanece aberta durante todo o período do relatório.
* Um gráfico do comprimento médio de uma exibição de página no período do relatório.

![chlimage_1-313](assets/chlimage_1-313.png)

## O relatório de Fontes {#the-sources-report}

O relatório Fontes indica como os usuários navegaram para a página, por exemplo, a partir dos resultados do mecanismo de pesquisa ou usando o URL conhecido.

![chlimage_1-314](assets/chlimage_1-314.png)

## O relatório Rejeições {#the-bounces-report}

O relatório Rejeições inclui um gráfico que mostra o número de rejeições ocorridas para uma página durante o período do relatório selecionado.

![chlimage_1-315](assets/chlimage_1-315.png)

## O relatório de atividades de campanha {#the-campaign-activity-report}

Para cada campanha para a qual a página está ativa, aparece um relatório chamado *Nome da campanha* Atividade. O relatório mostra as impressões de página e as conversões de cada segmento para o qual uma oferta é fornecida.

![chlimage_1-316](assets/chlimage_1-316.png)

## O Relatório de Recomendações da SEO {#the-seo-recommendations-report}

O relatório Recomendações de SEO contém os resultados da análise do BrightEdge para a página. O relatório é uma lista de verificação de recursos da página que indica quais recursos a página inclui ou não para maximizar a localizabilidade usando mecanismos de pesquisa.

O relatório permite criar tarefas para que sejam feitos aprimoramentos a fim de melhorar a localização da página. As recomendações indicam que foram criadas tarefas para implementá-las. Consulte [Atribuição de Tarefas para Recomendações de SEO](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations).

![chlimage_1-317](assets/chlimage_1-317.png)
