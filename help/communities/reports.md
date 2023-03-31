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

Para o AEM Communities, há vários relatórios que podem ser acessados de várias maneiras do ambiente de criação.

Em geral, os diversos relatórios são:

* [Relatório de exibições](#views-report)

   Fornece um gráfico de visualizações de conteúdo por membros da comunidade e visitantes do site para qualquer site da comunidade.

* [Relatório de publicações](#posts-report)

   Fornece um gráfico de vários tipos de postagens por membros da comunidade para qualquer site da comunidade.

Os relatórios tabulares podem ser exportados no formato .csv para processamento subsequente.

## Consoles de relatórios {#reporting-consoles}

### Relatórios para sites da comunidade {#reports-for-community-sites}

* Na navegação global: **[!UICONTROL Navegação]** > **[!UICONTROL Comunidades]** >  **[!UICONTROL Relatórios]**

* Escolha entre:

   * **[!UICONTROL Relatório de atribuições]**

      * Gere um relatório para o Site da Comunidade, Usuário ou Grupo e Atribuição selecionados.
   * **[!UICONTROL Relatório de publicações]**

      * Gere um relatório para o Site da comunidade, Tipo de conteúdo e Período selecionado.
   * **[!UICONTROL Relatório de exibições]**

      * gerar um relatório para o Site da comunidade, Tipo de conteúdo e Período.



![relatórios](assets/reports1.png)

## Relatório de exibições {#views-report}

O console Exibições permite que os relatórios sejam gerados nas exibições de página por recursos da comunidade por um determinado período.

![exibir relatório](assets/view-report.png)

Selecione os critérios do relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todos os conteúdos ou selecionar um dos recursos existentes no site.

* **[!UICONTROL Intervalo de tempo]**

   Selecione um dos seguintes:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecionar **[!UICONTROL Gerar]** para criar o relatório.

![generate-views](assets/generate-views.png)

## Relatório de publicações {#posts-report}

O console Publicações permite que os relatórios sejam gerados no número de publicações para recursos da comunidade por um determinado período.

![relatório de postagens](assets/posts-report.png)

Selecione os critérios do relatório:

* **[!UICONTROL Site]**

   Selecione um site da comunidade.

* **[!UICONTROL Tipo de conteúdo]**

   Pode escolher Todos os conteúdos ou selecionar um dos recursos existentes no site.

* **[!UICONTROL Intervalo de tempo]**

   Selecione um dos seguintes:

   * Últimos 7 dias
   * Últimos 30 dias
   * Últimos 90 dias
   * Ano anterior

Selecionar **[!UICONTROL Gerar]** para criar o relatório.

![gerar relatório](assets/generate-posts-report.png)

## Resolução de problemas {#troubleshooting}

### Nenhum site da comunidade listado {#no-community-sites-listed}

Se nenhum site da comunidade estiver listado, verifique se o Adobe Analytics foi ativado para um site. Se você escolher relatórios em atribuições, verifique se a função de atribuições está na estrutura do site da comunidade.

### Os relatórios não são exibidos na instância do autor do AEM {#reports-do-not-show-in-aem-author-instance}

Se os relatórios não forem exibidos na instância do autor do AEM, verifique as personalizações, como o mapeamento de URL na instância de publicação. Se o mapeamento de URL for feito somente na instância de publicação do AEM do site de comunidades, verifique se o mesmo foi configurado na instância de autor do AEM em **Relatório de tendência do site - Fábrica do componente social** configuração.

![Mapeamento de URL no autor do AEM](assets/sitetrend.png)
