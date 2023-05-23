---
title: Insights de ativos
description: Saiba como o recurso de insights do Assets permite rastrear as classificações de usuário e as estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas de Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 7%

---

# Insights de ativos {#asset-insights}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Este artigo |

O recurso Insights do Assets permite rastrear classificações de usuários e estatísticas de uso de imagens usadas em sites de terceiros, campanhas de marketing e soluções criativas de Adobe. Ele ajuda a obter insights sobre seu desempenho e popularidade.

[!DNL Assets] O Insights captura detalhes da atividade do usuário, como o número de vezes que uma imagem é classificada, clicada e impressões (número de vezes que uma imagem é carregada no site). Ele atribui pontuações a imagens com base nessas estatísticas. Você pode usar as pontuações e as estatísticas de desempenho para selecionar imagens populares para inclusão em catálogos, campanhas de marketing e assim por diante. Você pode até mesmo formular políticas de arquivamento e renovação de licença com base nessas estatísticas.

Para [!DNL Assets] Insights para capturar estatísticas de uso de imagens de um site, você deve incluir o código incorporado da imagem no código do site.

Para permitir que o Assets Insights exiba estatísticas de uso de ativos, primeiro configure o recurso para buscar dados de relatórios do Adobe Analytics. Para obter detalhes, consulte [Configurar insights do Assets](/help/assets/configure-asset-insights.md). Para usar esse recurso em uma instalação no local, adquira [!DNL Adobe Analytics] licença separadamente. Clientes em [!DNL Managed Services] receber [!DNL Analytics] licença fornecida com [!DNL Experience Manager]. Consulte [Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Os insights só são aceitos e fornecidos para imagens.

## Exibir estatísticas de uma imagem {#viewing-statistics-for-an-image}

Você pode exibir as pontuações dos Insights do Assets na página de metadados.

1. No [!DNL Assets] (UI), selecione a imagem e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Na página Propriedades, clique na guia **[!UICONTROL Insights]** guia.
1. Revise os detalhes de uso do ativo no **[!UICONTROL Insights]** guia. A variável **[!UICONTROL Pontuação]** A seção descreve o uso total de ativos e os repositórios de desempenho de um ativo.

   A pontuação de uso descreve o número de vezes que o ativo é usado em várias soluções.

   A variável **[!UICONTROL Impressões]** pontuação é o número de vezes que o ativo é carregado no site. O número exibido em **[!UICONTROL Cliques]** é o número de vezes em que o ativo é clicado.

1. Revise o **[!UICONTROL Estatísticas de uso]** para saber de quais entidades o ativo fazia parte e quais soluções criativas o usaram recentemente. Quanto maior for o uso, maior será a probabilidade de o ativo ser popular entre os usuários. Os dados de uso são exibidos abaixo dos seguintes cabeçalhos:

   * **Ativo**: o número de vezes que o ativo fez parte de uma coleção ou de um ativo composto
   * **Web e móvel**: o número de vezes que o ativo fez parte de sites e aplicativos
   * **Social**: o número de vezes que o ativo foi usado em soluções, como Adobe Social e Adobe Campaign
   * **E-mail**: o número de vezes que o ativo foi usado em campanhas de email

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Como o recurso de insights do Assets normalmente busca os dados de Soluções da Adobe Analytics periodicamente, a seção Soluções pode não exibir os dados mais recentes. O período para o qual os dados são exibidos depende do agendamento da operação de busca que o Assets Insights executa para recuperar os dados do Analytics.

1. Para exibir estatísticas de desempenho do ativo graficamente durante um período de tempo, selecione o período na seção **[!UICONTROL Estatísticas de desempenho]**. Detalhes, incluindo cliques e impressões, são exibidos como linhas de tendência de um gráfico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >Ao contrário dos dados na seção Soluções, a seção Estatísticas de desempenho exibe os dados mais recentes.

1. Para obter o código incorporado para o ativo incluído em sites para obter dados de desempenho, clique em **[!UICONTROL Obter código de inserção]** abaixo da miniatura do ativo. Para obter mais informações sobre como incluir seu código incorporado em páginas da Web de terceiros, consulte [Uso do Rastreador de páginas e código incorporado em páginas da Web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Exibir estatísticas agregadas para imagens {#viewing-aggregate-statistics-for-images}

Exiba pontuações de todos os ativos em uma pasta simultaneamente usando a **[!UICONTROL Exibição do Insights]**.

1. No [!DNL Assets] navegue até a pasta que contém os ativos para os quais deseja exibir insights.
1. Clique em Layout na barra de ferramentas e escolha **[!UICONTROL Visualização de insights]**.
1. A página exibe as pontuações de uso dos ativos. Compare as classificações dos vários ativos e obtenha insights.

## Agendar trabalho em segundo plano {#scheduling-background-job}

O Assets Insights busca dados de uso de ativos dos conjuntos de relatórios do Adobe Analytics periodicamente. Por padrão, o Assets Insights executa um trabalho em segundo plano a cada 24 horas às 2:00 AM para buscar dados. No entanto, você pode modificar a frequência e o tempo, configurando o **[!UICONTROL Trabalho de sincronização do relatório de desempenho do ativo Adobe CQ DAM]** no console da web.

1. Clique em [!DNL Experience Manager] e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Abra o **[!UICONTROL Trabalho de sincronização do relatório de desempenho do ativo Adobe CQ DAM]** configuração do serviço.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Especifique a frequência do scheduler desejada e a hora de início do trabalho na expressão do scheduler de propriedade. Salve as alterações.
