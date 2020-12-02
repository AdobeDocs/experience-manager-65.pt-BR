---
title: Visualizar dados de análise de página
seo-title: Visualizar dados de análise de página
description: Use dados de análise de página para avaliar a eficácia do conteúdo da página
seo-description: Use dados de análise de página para avaliar a eficácia do conteúdo da página
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
translation-type: tm+mt
source-git-commit: e3683f6254295e606e9d85e88979feaaea76c42e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 93%

---


# Visualizar dados de análise de página{#seeing-page-analytics-data}

Use dados de análise de página para avaliar a eficácia do conteúdo da página.

## Análise visível do console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Dados de análise de página são exibidos na [Visualização de lista](/help/sites-authoring/basic-handling.md#list-view) do console Sites. Quando as páginas são exibidas em formato de lista, as seguintes colunas estão disponíveis por padrão:

* Exibições da página
* Visitantes únicos
* Tempo na página

Cada coluna mostra um valor para o período de relatório atual e também indica se o valor aumentou ou diminuiu em relação ao período do relatório anterior. Os dados exibidos são atualizados a cada 12 horas.

>[!NOTE]
>
>Para alterar o período de atualização, [configure o intervalo de importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra o console **Sites**, por exemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone para selecionar **Visualização de lista** (o ícone mostrado dependerá da [visualização atual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Novamente, na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone e selecione **Configurações de exibição**. A caixa de diálogo **Configurar colunas** será aberta. Faça as alterações necessárias e confirme com **Atualizar**.

   ![aa-04](assets/aa-04.png)

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

1. Na Visualização da Lista, use os seletores de visualização (à direita da barra de ferramentas), selecione **Configurações de Visualização** e **Adicionar dados personalizados do Analytics**.

   ![aa-15](assets/aa-15.png)

1. Selecione as métricas que deseja expor aos autores do console Sites e clique em **Adicionar**.

   As colunas que aparecem são recuperadas do Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrir Content Insight do Sites {#opening-content-insights-from-sites}

Abra [Content Insight](/help/sites-authoring/content-insights.md) no console Sites para investigar a eficácia da página.

1. No console Sites, selecione a página para da qual você deseja ver os Content Insights.
1. Na barra de ferramentas, clique no ícone Analytics e Recomendações.

   ![](do-not-localize/chlimage_1-16a.png)

## Análise visível do Editor de página (Mapa de atividades)  {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Isso será mostrado se o [Mapa de atividades tiver sido configurado](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) para seu site.

>[!NOTE]
>
>Os dados do Mapa de atividades são retirados do Adobe Analytics.

Quando seu site tiver sido [configurado para o Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), você poderá usar o [mapa de atividades do modo](/help/sites-authoring/author-environment-tools.md#page-modes) para exibir dados relevantes. Por exemplo:

![aa-07](assets/aa-07.png)

### Acessar o mapa de atividades {#accessing-the-activity-map}

Após selecionar o modo de [Mapa de atividades](/help/sites-authoring/author-environment-tools.md#page-modes), você será solicitado a inserir suas credenciais do Adobe Analytics.

![aa-03](assets/aa-03.png)

A barra de ferramentas flutuante do **Analytics** é mostrada; aqui você pode:

* alterar o formato da barra de ferramentas usando as setas duplas (**>>**)
* Alternar detalhes da página (ícone de olhos)
* Configurar as configurações do Mapa de atividades (ícone cog)
* Selecionar a análise a ser mostrada (vários seletores suspensos)
* Saia do Mapa de atividades e feche a barra de ferramentas (x)

![aa-09](assets/aa-09.png)

### Selecionar a análise a ser exibida {#selecting-the-analytics-to-show}

Você pode selecionar os dados analíticos a serem exibidos e como eles devem ser exibidos, usando os vários critérios:

* **Padrão**/**Em tempo real**

* tipo de evento
* grupo de usuários
* **Bolhas**/**Gradiente**/**Ganhos e perdas**/**Desligado**

* período a ser mostrado

![aa-13](assets/aa-13.png)

### Configurar o mapa de atividades {#configuring-the-activity-map}

Use o ícone **Mostrar configurações** para abrir a caixa de diálogo **Configurações do Mapa de atividades**.

![aa-04-1](assets/aa-04-1.png)

A caixa de diálogo **Configurações do Mapa de atividades** fornece uma variedade de opções em três guias:

![aa-06](assets/aa-06.png)

* Geral

   * Conjunto de relatórios
   * Nome da Página
   * Idioma
   * Sobreposições de rótulo com
   * Tamanho da fonte do rótulo
   * Cor do gradiente
   * Cor da bolha
   * Gradiente colorido com base em
   * Transparência do gradiente

* Padrão

   * Exibir (tipo e número de links)
   * Ocultar as sobreposições de links que não receberam visitas

* Online

   * Exibir superiores (Ganhos ou perdas)
   * Excluir os inferiores %
   * Atualização automática (dados e período)

