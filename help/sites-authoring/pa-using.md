---
title: Visualização de dados de análise de página para medir a eficácia do conteúdo da página
description: Usar dados de análise de página para medir a eficácia do conteúdo da página
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# Visualizar dados de análise da página{#seeing-page-analytics-data}

Use os dados de análise da página para medir a eficácia do conteúdo da página.

## Análise visível do console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

Os dados de análise da página são exibidos em [Exibição de lista](/help/sites-authoring/basic-handling.md#list-view) do console Sites . Quando as páginas são exibidas em formato de lista, as seguintes colunas estão disponíveis por padrão:

* Exibições da página
* Visitantes únicos
* Tempo na página

Cada coluna mostra um valor para o período de relatório atual e também indica se o valor aumentou ou diminuiu em relação ao período de relatório anterior. Os dados exibidos são atualizados a cada 12 horas.

>[!NOTE]
>
>Para alterar o período de atualização, [configurar o intervalo de importação](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Abra o **Sites** console; por exemplo [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. Na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone para selecionar **Exibição de lista** (o ícone mostrado dependerá do [exibição atual](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Novamente, na extremidade direita da barra de ferramentas (canto superior direito), clique ou toque no ícone e selecione **Exibir configurações**. O **Configurar colunas** será aberta. Faça as alterações necessárias e confirme com **Atualizar**.

   ![aa-04](assets/aa-04.png)

### Selecionar o período de relatório {#selecting-the-reporting-period}

Selecione o período de relatório para o qual os dados do Analytics aparecem no console Sites :

* Dados dos últimos 30 dias
* Dados dos últimos 90 dias
* Dados deste ano

O período de relatório atual aparece na barra de ferramentas do console Sites (à direita da barra de ferramentas superior). Use o menu suspenso para selecionar o período de relatório necessário.
![aa-05](assets/aa-05.png)

### Configuração das colunas de dados disponíveis {#configuring-available-data-columns}

Os membros do grupo de usuários analytics-administrators podem configurar o console Sites para permitir que os autores vejam colunas adicionais do Analytics.

>[!NOTE]
>
>Quando uma árvore de páginas contém páginas filhas associadas a diferentes configurações de nuvem do Adobe Analytics, você não pode configurar as colunas de dados disponíveis para as páginas.

1. Na Exibição de lista, use os seletores de exibição (à direita da barra de ferramentas), selecione **Exibir configurações** e depois **Adicionar dados personalizados do Analytics**.

   ![aa-15](assets/aa-15.png)

1. Selecione as métricas que deseja expor aos autores no console Sites e clique em **Adicionar**.

   As colunas que aparecem são recuperadas do Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Abrir Content Insights de Sites {#opening-content-insights-from-sites}

Abrir [Content Insight](/help/sites-authoring/content-insights.md) no console Sites para investigar ainda mais a eficácia da página.

1. No console Sites , selecione a página na qual deseja visualizar os Content Insights.
1. Na barra de ferramentas, clique no ícone Analytics e Recommendations .

   ![](do-not-localize/chlimage_1-16a.png)

## Analytics visível do Editor de páginas (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Isso será mostrado se a variável [Activity Map foi configurado](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) para o seu site.

>[!NOTE]
>
>Os dados do Activity Map são retirados do Adobe Analytics.

Quando seu site tiver sido [configurado para Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), você pode usar o [Activity Map de modo](/help/sites-authoring/author-environment-tools.md#page-modes) para visualizar os dados relevantes. Por exemplo:

![aa-07](assets/aa-07.png)

### Acesso ao Activity Map {#accessing-the-activity-map}

Depois de selecionar o [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) , você será solicitado a inserir suas credenciais do Adobe Analytics.

![aa-03](assets/aa-03.png)

O **Analytics** a barra de ferramentas flutuante é exibida; aqui você pode:

* altere o formato da barra de ferramentas usando as setas duplas (**>>**)
* Alternar detalhes da página (ícone de olhos)
* Defina as configurações do Activity Map (ícone de engrenagem)
* Selecione a análise a ser mostrada (vários seletores suspensos)
* Sair do Activity Map e fechar a barra de ferramentas (x)

![aa-09](assets/aa-09.png)

### Seleção do Analytics para mostrar {#selecting-the-analytics-to-show}

Você pode selecionar os dados analíticos a serem exibidos e como eles devem ser exibidos, usando os vários critérios:

* **Padrão**/**Ao vivo**

* tipo de evento
* grupo de usuários
* **Bolhas**/**Gradiente**/**Ganhadores e perdedores**/**Desligado**

* período a ser mostrado

![aa-13](assets/aa-13.png)

### Configuração do Activity Map {#configuring-the-activity-map}

Use o **Mostrar configurações** ícone para abrir o **Configurações do Activity Map** caixa de diálogo.

![aa-04-1](assets/aa-04-1.png)

O **Configurações do Activity Map** A caixa de diálogo fornece uma variedade de opções em três guias:

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

   * Exibição (tipo e número de links)
   * Ocultar as sobreposições para links que não receberam visitas

* Online

   * Exibir principais (ganhadores ou perdedores)
   * Excluir os inferiores %
   * Atualização automática (dados e período)
