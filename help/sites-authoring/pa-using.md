---
title: Visualização dos dados de análise da página para medir a eficácia do conteúdo da página
description: Usar dados de análise de página para medir a eficácia do conteúdo da página
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 4%

---

# Visualização de dados de análise de página{#seeing-page-analytics-data}

Use os dados de análise da página para medir a eficácia do conteúdo da página.

## Analytics visível no Console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Os dados de análise de página são exibidos na [Exibição de lista](/help/sites-authoring/basic-handling.md#list-view) do console Sites. Quando as páginas são exibidas no formato de lista, as seguintes colunas estão disponíveis por padrão:

* Visualizações de página
* Visitantes únicos
* Tempo na página

Cada coluna mostra um valor para o período de relatório atual e também indica se o valor aumentou ou diminuiu desde o período de relatório anterior. Os dados exibidos são atualizados a cada 12 horas.

>[!NOTE]
>
>Para alterar o período de atualização, [configure o intervalo de importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra o console **Sites**; por exemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Na extremidade direita da barra de ferramentas (canto superior direito), clique no ícone para selecionar **Exibição em lista** (o ícone mostrado dependerá da [exibição atual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Novamente, na extremidade direita da barra de ferramentas (canto superior direito), clique no ícone e selecione **Exibir configurações**. A caixa de diálogo **Configurar Colunas** é aberta. Faça as alterações necessárias e confirme com **Atualizar**.

   ![aa-04](assets/aa-04.png)

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

1. Na Exibição de Lista, use os seletores de exibição (à direita da barra de ferramentas), selecione **Exibir Configurações** e **Adicionar Dados Personalizados do Analytics**.

   ![aa-15](assets/aa-15.png)

1. Selecione as métricas que deseja expor aos autores no console Sites e clique em **Adicionar**.

   As colunas exibidas são recuperadas do Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrindo insights de conteúdo em sites {#opening-content-insights-from-sites}

Abra o [Content Insight](/help/sites-authoring/content-insights.md) do console Sites para investigar mais a eficácia da página.

1. No console do Sites, selecione a página da qual deseja ver os Insights de conteúdo.
1. Na barra de ferramentas, clique no ícone Analytics e Recommendations.

   ![Ícone do Analytics e do Recommendations](do-not-localize/chlimage_1-16a.png)

## Análises visíveis no Editor de páginas (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Isto é mostrado se o [Activity Map foi configurado](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) para o seu site.

>[!NOTE]
>
>Os dados da Activity Map são obtidos do Adobe Analytics.

Quando seu site tiver sido [configurado para Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), você poderá usar o [Activity Map de modo](/help/sites-authoring/author-environment-tools.md#page-modes) para exibir dados relevantes. Por exemplo:

![aa-07](assets/aa-07.png)

### Acessar o Activity Map {#accessing-the-activity-map}

Após selecionar o modo [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes), você será solicitado a inserir suas credenciais do Adobe Analytics.

![aa-03](assets/aa-03.png)

A barra de ferramentas flutuante do **Analytics** é exibida; aqui você pode:

* alterar o formato da barra de ferramentas usando as setas duplas (**>>**)
* Alternar Detalhes da página (ícone de olho)
* Defina as configurações de Activity Map ( ícone cog)
* Selecione a análise que será exibida (vários seletores suspensos)
* Saia do Activity Map e feche a barra de ferramentas (x)

![aa-09](assets/aa-09.png)

### Selecionar o Analytics para mostrar {#selecting-the-analytics-to-show}

Você pode selecionar os dados analíticos a serem mostrados e como eles devem ser exibidos, usando os vários critérios:

* **Padrão**/**Ao Vivo**

* tipo de evento
* grupo de usuários
* **Bolhas**/**Gradiente**/**Ganhadores e Perdedores**/**Desativado**

* período a ser exibido

![aa-13](assets/aa-13.png)

### Configuração do Activity Map {#configuring-the-activity-map}

Use o ícone **Mostrar Configurações** para abrir a caixa de diálogo **Configurações de Activity Map**.

![aa-04-1](assets/aa-04-1.png)

A caixa de diálogo **Configurações de Activity Map** fornece um intervalo de opções em três guias:

![aa-06](assets/aa-06.png)

* Geral

   * Conjunto de relatórios
   * Nome da Página
   * Idioma
   * Sobreposições de Rótulo com
   * Tamanho da fonte do rótulo
   * Cor do gradiente
   * Cor da bolha
   * Gradiente colorido com base em
   * Transparência do gradiente

* Padrão

   * Exibição (tipo e número de links)
   * Ocultar as sobreposições para links que não receberam visitas

* Em tempo real

   * Exibir os principais (ganhadores ou perdedores)
   * Excluir % inferior
   * Atualização automática (dados e período)
