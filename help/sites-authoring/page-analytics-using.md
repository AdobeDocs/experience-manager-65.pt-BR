---
title: Visualização dos dados de análise da página para medir a eficácia do conteúdo da página
seo-title: Seeing Page Analytics Data
description: Usar dados de análise de página para medir a eficácia do conteúdo da página
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
source-git-commit: 75c6bb87bb06c5ac9378ccebf193b5416c080bb1
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 11%

---

# Visualização de dados de análise de página{#seeing-page-analytics-data}

Use os dados de análise da página para medir a eficácia do conteúdo da página.

## Analytics visível no Console {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

Os dados de análise da página são exibidos em [Exibição de lista](/help/sites-authoring/basic-handling.md#list-view) do console Sites. Quando as páginas são exibidas no formato de lista, as seguintes colunas estão disponíveis por padrão:

* Exibições da página
* Visitantes únicos
* Tempo na página

Cada coluna mostra um valor para o período de relatório atual e também indica se o valor aumentou ou diminuiu desde o período de relatório anterior. Os dados exibidos são atualizados a cada 12 horas.

>[!NOTE]
>
>Para alterar o período de atualização, [configurar o intervalo de importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra o **Sites** console; por exemplo [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. Na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone para selecionar **Exibição de lista** (o ícone mostrado dependerá do [exibição atual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Novamente, na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone e selecione **Configurações de exibição**. A variável **Configurar colunas** será aberta. Faça as alterações necessárias e confirme com **Atualizar**.

   ![spad-02](assets/spad-02.png)

### Seleção do Período de Geração de Relatórios {#selecting-the-reporting-period}

Selecione o período do relatório para o qual os dados do Analytics aparecem no console Sites:

* Dados dos últimos 30 dias
* Dados dos últimos 90 dias
* Dados deste ano

O período atual do relatório aparece na barra de ferramentas do console Sites (à direita da barra de ferramentas superior). Use o menu suspenso para selecionar o período de relatório necessário.

![aa-05](assets/aa-05.png)

### Configuração de Colunas de Dados Disponíveis {#configuring-available-data-columns}

Os membros do grupo de usuários de administradores de análises podem configurar o console Sites para permitir que os autores vejam colunas adicionais do Analytics.

>[!NOTE]
>
>Quando uma árvore de páginas contém páginas secundárias associadas a diferentes configurações de nuvem do Adobe Analytics, não é possível definir colunas de dados disponíveis para as páginas.

1. Na Exibição em lista, use os seletores de exibições (à direita da barra de ferramentas) e selecione **Configurações de exibição** e depois **Adicionar dados personalizados do Analytics**.

   ![spad-03](assets/spad-03.png)

1. Selecione as métricas que deseja expor aos autores no console Sites e clique em **Adicionar**.

   As colunas exibidas são recuperadas do Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrindo insights de conteúdo em sites {#opening-content-insights-from-sites}

Abertura [Content Insight](/help/sites-authoring/content-insights.md) no console Sites para investigar mais a eficácia da página.

1. No console do Sites, selecione a página da qual deseja ver os Insights de conteúdo.
1. Na barra de ferramentas, clique no ícone Analytics e Recommendations.

   ![Ícone do Analytics e do Recommendations](do-not-localize/chlimage_1-14.png)

## Análises visíveis no Editor de páginas (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>A variável [Plug-in do ActivityMap fornecido pela Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=pt-BR) deve ser usada.
