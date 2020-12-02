---
title: Ativar insights de ativos por meio do DTM
description: Saiba como usar o Gerenciamento dinâmico de tags do Adobe (DTM) para ativar o Asset Insights.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Ativar insights de ativos por meio do DTM {#enable-asset-insights-through-dtm}

O Gerenciamento dinâmico de tags do Adobe é uma ferramenta que ativa suas ferramentas de marketing digital. Ele é fornecido gratuitamente aos clientes da Adobe Analytics. Você pode personalizar seu código de rastreamento para permitir que soluções de CMS de terceiros usem o Asset Insights ou usar o DTM para inserir tags do Asset Insights. Os insights só são suportados e fornecidos para imagens.

>[!CAUTION]
>
>O DTM do Adobe está obsoleto em favor de [!DNL Adobe Experience Platform Launch] e em breve chegará ao [fim da vida](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). O Adobe recomenda que você [use [!DNL Launch] para obter insights de ativos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Execute essas etapas para ativar os Asset Insights por meio do DTM.

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração do Insights]**.
1. [Configurar a implantação do Experience Manager com o Cloud Service DTM](/help/sites-administering/dtm.md)

   O token da API deve estar disponível assim que você fizer logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e visitar **[!UICONTROL Configurações da conta]** no Perfil do usuário. Essa etapa não é necessária do ponto de vista Asset Insights, pois a integração dos Experience Manager Sites com Asset Insights ainda está em andamento.

1. Faça logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e selecione uma empresa, conforme apropriado.
1. Criar ou abrir uma propriedade da Web existente

   * Selecione a guia **[!UICONTROL Propriedades da Web]** e clique em **[!UICONTROL Adicionar propriedade]**.

   * Atualize os campos conforme apropriado e clique em **[!UICONTROL Criar propriedade]**. Consulte [documentação](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Criar propriedade da Web de edição](assets/Create-edit-web-property.png)

1. Na guia **[!UICONTROL Regras]**, selecione **[!UICONTROL Regras de carregamento de página]** no painel de navegação e clique em **[!UICONTROL Criar nova regra]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expanda **[!UICONTROL JavaScript /Tags de terceiros]**. Em seguida, clique em **[!UICONTROL Adicionar novo script]** na guia **[!UICONTROL HTML sequencial]** para abrir a caixa de diálogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.
1. Clique em **[!UICONTROL Controlador de página do Insights]**, copie o código do rastreador e cole-o na caixa de diálogo Script aberta na etapa 6. Salve as alterações.

   >[!NOTE]
   >
   >* `AppMeasurement.js` for removido. Ela deve estar disponível por meio da ferramenta Adobe Analytics do DTM.
   >* A chamada para `assetAnalytics.dispatcher.init()` foi removida. Espera-se que a função seja chamada assim que a ferramenta Adobe Analytics do DTM terminar o carregamento.
   >* Dependendo de onde o Asset Insights Page Tracker estiver hospedado (por exemplo, Experience Manager, CDN e assim por diante), a origem da fonte do script pode exigir alterações.
   >* Para o Controlador de página hospedado no Experience Manager, a origem deve apontar para uma instância de publicação usando o nome de host da instância do dispatcher.


1. Acesso `https://dtm.adobe.com`. Clique em **[!UICONTROL Visão geral]** na propriedade da Web e clique em **[!UICONTROL Adicionar ferramenta]** ou abra uma ferramenta Adobe Analytics existente. Ao criar a ferramenta, você pode definir **[!UICONTROL Método de configuração]** como **[!UICONTROL Automático]**.

   ![Adicionar ferramenta Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Selecione Conjuntos de relatórios de armazenamento temporário/produção, conforme apropriado.

1. Expanda **[!UICONTROL Gerenciamento de biblioteca]** e certifique-se de que **[!UICONTROL Carregar biblioteca em]** esteja definido como **[!UICONTROL Topo da página]**.

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. Expanda **[!UICONTROL Personalizar código de página]** e clique em **[!UICONTROL Abrir editor]**.

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. Cole o seguinte código na janela:

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * A regra de carregamento de página no DTM inclui apenas o código `pagetracker.js`. Quaisquer campos `assetAnalytics` são considerados substituições para valores padrão. Elas não são obrigatórias por padrão.
   * O código chama `assetAnalytics.dispatcher.init()` depois de verificar se `_satellite.getToolsByType('sc')[0].getS()` está inicializado e `assetAnalytics,dispatcher.init` está disponível. Portanto, você pode ignorar a adição na etapa 11.
   * Conforme indicado nos comentários no código do Controlador de página do Insights (**[!UICONTROL Ferramentas > Ativos > Controlador de página do Insights]**), quando o Controlador de página não cria um objeto `AppMeasurement`, os três primeiros argumentos (RSID, Servidor de rastreamento e Namespace de Visitante) são irrelevantes. Strings vazias são passadas para realçar isso.\
      Os argumentos restantes correspondem ao que está configurado na página Configuração do Insights (**[!UICONTROL Ferramentas > Ativos > Configuração do Insights]**).
   * O objeto AppMeasurement é recuperado consultando `satelliteLib` para todos os mecanismos de SiteCatalyst disponíveis. Se várias tags estiverem configuradas, altere o índice do seletor de matriz adequadamente. As entradas no storage são ordenadas de acordo com as ferramentas de SiteCatalyst disponíveis na interface do DTM.

1. Salve e feche a janela Editor de código e salve as alterações na configuração da ferramenta.
1. Na guia **[!UICONTROL Aprovações]**, aprove as duas aprovações pendentes. A tag do DTM está pronta para ser inserida na sua página da Web. Para obter detalhes sobre como inserir tags do DTM em páginas da Web, consulte [Integrar o DTM em modelos de página personalizados](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
