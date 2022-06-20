---
title: Insights de ativos
description: Saiba como o recurso Insights do Assets permite que você acompanhe as classificações do usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas do Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 7%

---

# Insights de ativos {#asset-insights}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/touch-ui-configuring-asset-insights.html?lang=en) |

O Assets Insights permite que você rastreie as estatísticas de classificação e uso de imagens usadas em campanhas de marketing de terceiros e nas soluções criativas de sites do Adobe. Ajuda a obter insights sobre seu desempenho e sua popularidade.

[!DNL Assets] Os insights capturam detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para [!DNL Assets] Insights para capturar estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Assets Insights exiba as estatísticas de uso dos ativos, primeiro configure o recurso para buscar dados de relatório do Adobe Analytics. Para obter detalhes, consulte [Configurar o Assets Insights](/help/assets/configure-asset-insights.md). Para usar esse recurso em uma instalação local, compre [!DNL Adobe Analytics] licença separadamente. Clientes em [!DNL Managed Services] receive [!DNL Analytics] licença fornecida com [!DNL Experience Manager]. Consulte [Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

## Exibir estatísticas de uma imagem {#viewing-statistics-for-an-image}

Você pode exibir as pontuações do Assets Insights da página de metadados.

1. No [!DNL Assets] interface do usuário (UI), selecione a imagem e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades , clique no botão **[!UICONTROL Insights]** guia .
1. Revise os detalhes de uso do ativo na **[!UICONTROL Insights]** guia . O **[!UICONTROL Pontuação]** descreve o uso total de ativos e as funções de desempenho de um ativo .

   A pontuação de uso descreve a quantidade de vezes que o ativo é usado em várias soluções.

   O **[!UICONTROL Impressões]** pontuação é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Cliques]** é o número de vezes em que o ativo é clicado.

1. Revise o **[!UICONTROL Estatísticas de uso]** seção para saber quais entidades o ativo fez parte e quais soluções criativas o usaram recentemente. Quanto maior for o uso, maior será a probabilidade de o ativo ser popular entre os usuários. Os dados de uso são exibidos abaixo dos seguintes cabeçalhos:

   * **Ativo**: O número de vezes que o ativo fez parte de uma coleção ou de um ativo composto
   * **Web e móvel**: O número de vezes que o ativo foi parte de sites e aplicativos
   * **Social**: O número de vezes que o ativo foi usado em soluções, como Adobe Social e Adobe Campaign
   * **Email**: O número de vezes que o ativo foi usado em campanhas de email

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso Assets Insights normalmente busca os dados das Soluções da Adobe Analytics de maneira periódica, a seção Soluções pode não exibir os dados mais recentes. O período de tempo para o qual os dados são exibidos depende da programação da operação de busca executada pelo Assets Insights para recuperar os dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções , a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado do ativo que você inclui nos sites para obter dados de desempenho, clique em **[!UICONTROL Obter código incorporado]** abaixo da miniatura do ativo. Para obter mais informações sobre como incluir o código Incorporado em páginas da Web de terceiros, consulte [Usar o rastreador de página e incorporar código em páginas da Web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Exibir estatísticas agregadas de imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. No [!DNL Assets] na interface do usuário, navegue até a pasta que contém os ativos para os quais deseja exibir insights.
1. Clique em Layout na barra de ferramentas e escolha **[!UICONTROL Exibição de insights]**.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

## Agendar tarefa em segundo plano {#scheduling-background-job}

O Assets Insights busca dados de uso de ativos dos conjuntos de relatórios do Adobe Analytics de maneira periódica. Por padrão, o Assets Insights executa um trabalho em segundo plano a cada 24 horas às 2:00 AM para buscar dados. No entanto, você pode modificar a frequência e o tempo configurando a variável **[!UICONTROL Trabalho de sincronização de relatórios de desempenho de ativos do Adobe CQ DAM]** do console da Web.

1. Clique no botão [!DNL Experience Manager] logotipo e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Abra o **[!UICONTROL Trabalho de sincronização de relatórios de desempenho de ativos do Adobe CQ DAM]** configuração de serviço.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique a frequência do agendador desejada e a hora de início da tarefa na expressão do agendador de propriedades. Salve as alterações.
