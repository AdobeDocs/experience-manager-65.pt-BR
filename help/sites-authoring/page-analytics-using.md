---
title: Visualizar dados de análise de página
seo-title: Seeing Page Analytics Data
description: Use dados de análise de página para avaliar a eficácia do conteúdo da página
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 86%

---

# Visualizar dados de análise de página{#seeing-page-analytics-data}

Use dados de análise de página para avaliar a eficácia do conteúdo da página.

## Análise visível do console {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

Dados de análise de página são exibidos na [Visualização de lista](/help/sites-authoring/basic-handling.md#list-view) do console Sites. Quando as páginas são exibidas em formato de lista, as seguintes colunas estão disponíveis por padrão:

* Exibições da página
* Visitantes únicos
* Tempo na página

Cada coluna mostra um valor para o período de relatório atual e também indica se o valor aumentou ou diminuiu em relação ao período do relatório anterior. Os dados exibidos são atualizados a cada 12 horas.

>[!NOTE]
>
>Para alterar o período de atualização, [configure o intervalo de importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra o **Sites** console; por exemplo [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. Na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone para selecionar **Visualização de lista** (o ícone mostrado dependerá da [visualização atual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Novamente, na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone e selecione **Configurações de exibição**. A caixa de diálogo **Configurar colunas** será aberta. Faça as alterações necessárias e confirme com **Atualizar**.

   ![spad-02](assets/spad-02.png)

### Seleção do período de relatório {#selecting-the-reporting-period}

Selecione o período de relatório para o qual os dados de Analítica devem aparecer no console Sites:

* Dados dos últimos 30 dias
* Dados dos últimos 90 dias
* Dados deste ano

O período do relatório atual aparece na barra de ferramentas do console Sites (à direita da barra de ferramentas superior). Use o menu suspenso para selecionar o período de relatório necessário.

![aa-05](assets/aa-05.png)

### Configurar colunas de dados disponíveis {#configuring-available-data-columns}

Os membros do grupo de usuários análise-administradores podem configurar o console Sites para permitir que os autores vejam colunas de análise adicionais.

>[!NOTE]
>
>Quando uma árvore de páginas contém páginas secundárias associadas a diferentes configurações de nuvem do Adobe Analytics, você não pode configurar as colunas de dados disponíveis para as páginas.

1. Na Exibição de lista, use os seletores de exibição (à direita da barra de ferramentas), selecione **Exibir configurações** e depois **Adicionar dados personalizados do Analytics**.

   ![spad-03](assets/spad-03.png)

1. Selecione as métricas que deseja expor aos autores do console Sites e clique em **Adicionar**.

   As colunas que aparecem são recuperadas do Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrir Content Insight do Sites {#opening-content-insights-from-sites}

Abrir [Content Insight](/help/sites-authoring/content-insights.md) no console Sites para investigar ainda mais a eficácia da página.

1. No console Sites, selecione a página para da qual você deseja ver os Content Insights.
1. Na barra de ferramentas, clique no ícone Analytics e Recomendações.

   ![](do-not-localize/chlimage_1-14.png)

## Análise visível do Editor de página (Mapa de atividades) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>Devido a alterações de segurança na API do Adobe Analytics, não é mais possível usar a versão do Activity Map incluída no AEM.
>
>O [Plug-in do Activity Map fornecido pelo Adobe Analytics](https://docs.adobe.com/content/help/pt-BR/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) deve ser usada.
