---
title: 'Informações de ativos '
description: Saiba como o recurso Asset Insights permite que você acompanhe as classificações do usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas do Adobe.
contentOwner: AG
role: Profissional de negócios, Administrador
feature: Insights de ativos,Relatórios de ativos
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---


# Informações de ativos {#asset-insights}

O Asset Insights permite que você rastreie as estatísticas de classificações e uso de imagens usadas em campanhas de marketing de terceiros e nas soluções criativas de sites do Adobe. Ajuda a obter insights sobre seu desempenho e sua popularidade.

[!DNL Assets] Os insights capturam detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para [!DNL Assets] insights para capturar estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Asset Insights exiba estatísticas de uso de ativos, primeiro configure o recurso para buscar dados de relatório do Adobe Analytics. Para obter detalhes, consulte [Configurar Asset Insights](/help/assets/configure-asset-insights.md).

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

## Exibir estatísticas de uma imagem {#viewing-statistics-for-an-image}

Você pode exibir as pontuações do Asset Insights da página de metadados.

1. Na interface do usuário [!DNL Assets] (UI), selecione a imagem e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades , clique na guia **[!UICONTROL Insights]**.
1. Revise os detalhes de uso do ativo na guia **[!UICONTROL Insights]**. A seção **[!UICONTROL Pontuação]** descreve o uso total de ativos e as funções de desempenho de um ativo .

   A pontuação de uso descreve a quantidade de vezes que o ativo é usado em várias soluções.

   A pontuação **[!UICONTROL Impressões]** é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Clicks]** é o número de vezes que o ativo é clicado.

1. Revise a seção **[!UICONTROL Estatísticas de uso]** para saber quais entidades o ativo fazia parte e quais soluções criativas o usaram recentemente. Quanto maior for o uso, maior será a probabilidade de o ativo ser popular entre os usuários. Os dados de uso são exibidos abaixo dos seguintes cabeçalhos:

   * **Ativo**: O número de vezes que o ativo fez parte de uma coleção ou de um ativo composto
   * **Web e móvel**: O número de vezes que o ativo foi parte de sites e aplicativos
   * **Social**: O número de vezes que o ativo foi usado em soluções, como Adobe Social e Adobe Campaign
   * **Email**: O número de vezes que o ativo foi usado em campanhas de email

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Asset Insights normalmente busca os dados de Soluções da Adobe Analytics de maneira periódica, a seção Soluções pode não exibir os dados mais recentes. O período de tempo para o qual os dados são exibidos depende do agendamento da operação de busca executada pelo Asset Insights para recuperar dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções , a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado do ativo que você inclui nos sites para obter dados de desempenho, clique em **[!UICONTROL Obter código incorporado]** abaixo da miniatura do ativo. Para obter mais informações sobre como incluir o código Incorporado em páginas da Web de terceiros, consulte [Usar o rastreador de páginas e incorporar o código em páginas da Web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Exibir estatísticas agregadas de imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. Na interface do usuário [!DNL Assets], navegue até a pasta que contém os ativos para os quais deseja exibir insights.
1. Clique em Layout na barra de ferramentas e escolha **[!UICONTROL Exibição do Insights]**.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

## Agendar tarefa em segundo plano {#scheduling-background-job}

O Asset Insights busca dados de uso de ativos dos conjuntos de relatórios do Adobe Analytics de maneira periódica. Por padrão, o Asset Insights executa um trabalho em segundo plano a cada 24 horas às 2:00 AM para buscar dados. No entanto, você pode modificar a frequência e o tempo configurando o serviço **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** do console da Web.

1. Clique no logotipo [!DNL Experience Manager] e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Abra a configuração do serviço **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]**.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique a frequência do agendador desejada e a hora de início da tarefa na expressão do agendador de propriedades. Salve as alterações.
