---
title: 'Informações de ativos '
description: Saiba como o recurso Asset Insights permite rastrear as classificações de usuários e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 7%

---


# Informações de ativos {#asset-insights}

O recurso Asset Insights permite que você rastreie as classificações de usuários e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas da Adobe. Ajuda a obter insights sobre o desempenho e a popularidade deles.

O Assets Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as estatísticas de pontuação e desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para que o Assets Insights capture as estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Asset Insights exiba estatísticas de uso de ativos, configure primeiro o recurso para buscar dados de relatórios da Adobe Analytics. Para obter detalhes, consulte [Configurar insights](/help/assets/touch-ui-configuring-asset-insights.md)de ativos.

>[!NOTE]
>
>Os insights só são suportados e fornecidos para imagens.

## Estatísticas de Visualização para uma imagem {#viewing-statistics-for-an-image}

Você pode visualização as pontuações do Asset Insights na página de metadados.

1. Na interface do usuário do Assets (UI), selecione a imagem e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades, clique na guia **[!UICONTROL Insights]** .
1. Revise os detalhes de uso do ativo na guia **[!UICONTROL Insights]** . A seção **[!UICONTROL Pontuação]** descreve o uso total de ativos e as funções de desempenho de um ativo.

   A pontuação de uso descreve o número de vezes que o ativo é usado em várias soluções.

   A pontuação de **[!UICONTROL impressões]** é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Cliques]** é o número de vezes que o ativo é clicado.

1. Revise a seção Estatísticas **[!UICONTROL de]** uso para saber de quais entidades o ativo fazia parte e quais soluções criativas o utilizaram recentemente. Quanto maior o uso, maiores as chances de que o ativo seja popular entre os usuários. Os dados de uso são exibidos sob os seguintes cabeçalhos:

   * **Ativo**: O número de vezes que o ativo fez parte de uma coleção ou de um ativo composto
   * **Web e dispositivos móveis**: O número de vezes que o ativo fez parte de sites e aplicativos
   * **Social**: O número de vezes que o ativo foi usado em soluções, como o Adobe Social e o Adobe Campaign
   * **Email**: O número de vezes que o ativo foi usado em campanhas de email
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Asset Insights normalmente obtém os dados de Soluções da Adobe Analytics de forma periódica, a seção Soluções pode não exibir os dados mais recentes. O período de tempo para o qual os dados são exibidos depende da programação da operação de busca executada pelo Asset Insights para recuperar dados da Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções, a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado para o ativo que você inclui em sites para obter dados de desempenho, clique em **[!UICONTROL Obter código]** incorporado abaixo da miniatura do ativo. Para obter mais informações sobre como incluir o código Incorporado em páginas da Web de terceiros, consulte [Uso do rastreador de páginas e o código incorporado em páginas](/help/assets/touch-ui-using-page-tracker.md)da Web.

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Estatísticas de agregação de Visualizações para imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. Na interface do usuário dos Ativos, navegue até a pasta que contém os ativos para os quais você deseja visualização insights.
1. Clique em Layout na barra de ferramentas e escolha **[!UICONTROL Visualização]** Insights.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

## Agendar tarefa em segundo plano {#scheduling-background-job}

O Asset Insights busca os dados de uso de ativos dos conjuntos de relatórios da Adobe Analytics de forma periódica. Por padrão, o Asset Insights executa uma tarefa em segundo plano a cada 24 horas às 2 horas da manhã para obter dados. No entanto, você pode modificar a frequência e a hora configurando o serviço Trabalho **[!UICONTROL de sincronização de relatório de desempenho de ativos do]** Adobe CQ DAM no console da Web.

1. Click the Experience Manager logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Abra a configuração do serviço **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** .

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique a frequência de scheduler desejada e a hora de start para o trabalho na expressão de scheduler de propriedade. Salve as alterações.
