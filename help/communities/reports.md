---
title: Console de relatórios
seo-title: Reports Console
description: Saiba como acessar relatórios
seo-description: Learn how to access reports
uuid: 7bb15a15-077b-4bfb-aaf4-50fddc67f237
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: fde053ff-b671-456b-869c-81f16ea1f1be
docset: aem65
role: Admin
exl-id: 2aff2ffe-ba6f-4cc9-a126-40fc2a1161e2
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# Console de relatórios {#reports-console}

## Visão geral {#overview}

Para o AEM Communities, há vários relatórios que podem ser acessados de várias maneiras no ambiente de criação.

Em geral, os vários relatórios são:

* [Relatório de exibições](#views-report)

   Fornece um gráfico de exibições de conteúdo por membros da comunidade e visitantes do site para qualquer site da comunidade.

* [Relatório de publicações](#posts-report)

   Fornece um gráfico de vários tipos de publicações de membros da comunidade para qualquer site da comunidade.

Os relatórios tabulares podem ser exportados no formato .csv para processamento subsequente.

## Consoles de relatórios {#reporting-consoles}

### Relatórios para sites da comunidade {#reports-for-community-sites}

* Na navegação global: **[!UICONTROL Navegação]** > **[!UICONTROL Communities]** >  **[!UICONTROL Relatórios]**

* Escolher de:

   * **[!UICONTROL Relatório de atribuições]**

      * Gere um relatório para o site da comunidade, usuário ou grupo selecionado e atribuição.
   * **[!UICONTROL Relatório de publicações]**

      * Gerar um relatório para o site da comunidade, tipo de conteúdo e período de tempo selecionados.
   * **[!UICONTROL Relatório de exibições]**

      * gere um relatório para o Site da comunidade, Tipo de conteúdo e Período selecionados.



![relatórios](assets/reports1.png)

## Relatório de exibições {#views-report}

O console Exibições permite que os relatórios sejam gerados nas exibições de página pelos recursos da comunidade por um determinado período de tempo.

![exibir-relatório](assets/view-report.png)

Selecione os critérios para o relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site.

* **[!UICONTROL Período de tempo]**

   Selecione um de:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecionar **[!UICONTROL Gerar]** para criar o relatório.

![generate-views](assets/generate-views.png)

## Relatório de publicações {#posts-report}

O console de Publicações permite que os relatórios sejam gerados sobre o número de publicações para os recursos da comunidade por um determinado período de tempo.

![post-report](assets/posts-report.png)

Selecione os critérios para o relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todo o conteúdo ou selecionar um dos recursos presentes no site.

* **[!UICONTROL Período de tempo]**

   Selecione um de:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecionar **[!UICONTROL Gerar]** para criar o relatório.

![generate-report](assets/generate-posts-report.png)

## Resolução de problemas {#troubleshooting}

### Nenhum site da comunidade listado {#no-community-sites-listed}

Se nenhum site da comunidade estiver listado, verifique se o Adobe Analytics foi ativado para um site. Se escolher relatórios sobre atribuições, certifique-se de que a função de atribuições esteja na estrutura do site da comunidade.

### Os relatórios não são exibidos na instância do autor do AEM {#reports-do-not-show-in-aem-author-instance}

Se os relatórios não forem exibidos na instância do AEM Author, verifique as personalizações, como o mapeamento de URL na instância de Publicação. Se o mapeamento de URL for feito somente na instância de publicação do AEM do site das comunidades, verifique se o mesmo foi configurado na instância de autor do AEM no **Fatory do Componente Social do Relatório de Tendências do Site** configuração.

![Mapeamento de URL no AEM Author](assets/sitetrend.png)
