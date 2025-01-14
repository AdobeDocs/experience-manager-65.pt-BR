---
title: Console de relatórios
description: Saiba como usar vários relatórios que você pode acessar de várias maneiras do ambiente de autor do Adobe Experience Manager.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# Console de relatórios {#reports-console}

## Visão geral {#overview}

Para o AEM Communities, há vários relatórios que podem ser acessados de várias maneiras no ambiente de criação.

Em geral, os vários relatórios são:

* [Relatório de modos de exibição](#views-report)

  Fornece um gráfico de exibições de conteúdo por membros da comunidade e visitantes do site para qualquer site da comunidade.

* [Relatório de postagens](#posts-report)

  Fornece um gráfico de vários tipos de publicações de membros da comunidade para qualquer site da comunidade.

Os relatórios tabulares podem ser exportados no formato .csv para processamento subsequente.

## Consoles de relatórios {#reporting-consoles}

### Relatórios para sites da comunidade {#reports-for-community-sites}

* Da navegação global: **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Relatórios]**

* Escolher de:

   * **[!UICONTROL Relatório de atribuições]**

      * Gere um relatório para o site da comunidade, usuário ou grupo selecionado e atribuição.

   * **[!UICONTROL Relatório de postagens]**

      * Gerar um relatório para o site da comunidade, tipo de conteúdo e período de tempo selecionados.

   * **[!UICONTROL Relatório de modos de exibição]**

      * gere um relatório para o Site da comunidade, Tipo de conteúdo e Período selecionados.

![relatórios](assets/reports1.png)

## Relatório de exibições {#views-report}

O console Exibições permite que os relatórios sejam gerados em exibições de página pelos recursos da comunidade por um determinado período de tempo.

![exibir-relatório](assets/view-report.png)

Selecione os critérios para o relatório:

* **[!UICONTROL Site]**

  Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

  Pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site.

* **[!UICONTROL Intervalo de tempo]**

  Selecione um de:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **[!UICONTROL Gerar]** para criar o relatório.

![generate-views](assets/generate-views.png)

## Relatório de publicações {#posts-report}

O console Postagens permite gerar relatórios sobre o número de postagens para recursos da comunidade em um determinado período de tempo.

![relatório de postagens](assets/posts-report.png)

Selecione os critérios para o relatório:

* **[!UICONTROL Site]**

  Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

  Pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site.

* **[!UICONTROL Intervalo de tempo]**

  Selecione um de:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecione **[!UICONTROL Gerar]** para criar o relatório.

![gerar-relatório](assets/generate-posts-report.png)

## Resolução de problemas {#troubleshooting}

### Nenhum site da comunidade listado {#no-community-sites-listed}

Se nenhum site da comunidade estiver listado, verifique se o Adobe Analytics foi ativado para um site. Se escolher relatórios sobre atribuições, certifique-se de que a função de atribuições esteja na estrutura do site da comunidade.

### Os relatórios não são exibidos na instância do autor do AEM {#reports-do-not-show-in-aem-author-instance}

Se os relatórios não forem exibidos na instância do Autor AEM, verifique as personalizações, como o mapeamento de URL na instância do Publish. Se o mapeamento de URL for feito somente na instância AEM Publish do site de comunidades, verifique se o mesmo foi configurado na instância AEM Author na configuração **Site Trend Report Social Component Fatory**.

![Mapeamento de URL no Autor do AEM](assets/sitetrend.png)
