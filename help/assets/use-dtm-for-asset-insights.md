---
title: Ativar o Assets Insights por meio do DTM
description: Saiba como usar o Gerenciamento dinâmico de tags (DTM) do Adobe para ativar o Assets Insights.
contentOwner: AG
role: User, Admin
feature: Insights de ativos,Relatórios de ativos
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Ativar o Assets Insights por meio do DTM {#enable-asset-insights-through-dtm}

O Adobe Dynamic Tag Management é uma ferramenta que ativa suas ferramentas de marketing digital. É fornecido gratuitamente para os clientes da Adobe Analytics. Você pode personalizar o código de rastreamento para permitir que soluções de CMS de terceiros usem o Assets Insights ou usar o DTM para inserir tags do Assets Insights. Os insights são suportados e fornecidos apenas para imagens.

>[!CAUTION]
>
>O DTM do Adobe está obsoleto em favor de [!DNL Adobe Experience Platform Launch] e em breve chegará ao [fim da vida útil](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). O Adobe recomenda [usar [!DNL Launch] para insights de ativos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Execute essas etapas para ativar o Assets Insights por meio do DTM.

1. Clique no logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração do Insights]**.
1. [Configurar a implantação do Experience Manager com o Cloud Service do DTM](/help/sites-administering/dtm.md)

   O token da API deve estar disponível assim que você fizer logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e visitar **[!UICONTROL Configurações da conta]** no Perfil do usuário. Essa etapa não é necessária do ponto de vista do Assets Insights, pois a integração do Experience Manager Sites com o Assets Insights ainda está em funcionamento.

1. Faça logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e selecione uma empresa, conforme apropriado.
1. Criar ou abrir uma propriedade da Web existente

   * Selecione a guia **[!UICONTROL Propriedades da Web]** e clique em **[!UICONTROL Adicionar Propriedade]**.

   * Atualize os campos conforme apropriado e clique em **[!UICONTROL Criar propriedade]**. Consulte [documentação](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html).

   ![Criar propriedade da Web de edição](assets/Create-edit-web-property.png)

1. Na guia **[!UICONTROL Rules]**, selecione **[!UICONTROL Regras de carregamento de página]** no painel de navegação e clique em **[!UICONTROL Criar nova regra]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expanda **[!UICONTROL JavaScript /Tags de terceiros]**. Em seguida, clique em **[!UICONTROL Adicionar novo script]** na guia **[!UICONTROL HTML sequencial]** para abrir a caixa de diálogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Clique no logotipo do Experience Manager e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.
1. Clique em **[!UICONTROL Insights Page Tracker]**, copie o código do rastreador e, em seguida, cole na caixa de diálogo Script aberta na etapa 6. Salve as alterações.

   >[!NOTE]
   >
   >* `AppMeasurement.js` for removido. Ela deve estar disponível por meio da ferramenta Adobe Analytics do DTM.
   >* A chamada para `assetAnalytics.dispatcher.init()` é removida. Espera-se que a função seja chamada assim que a ferramenta Adobe Analytics do DTM terminar o carregamento.
   >* Dependendo de onde o Rastreador de página do Assets Insights está hospedado (por exemplo, Experience Manager, CDN e assim por diante), a origem da origem do script pode exigir alterações.
   >* Para o Rastreador de página hospedado no Experience Manager, a origem deve apontar para uma instância de publicação usando o nome do host da instância do dispatcher.


1. Acesso `https://dtm.adobe.com`. Clique em **[!UICONTROL Visão geral]** na propriedade da Web e clique em **[!UICONTROL Adicionar ferramenta]** ou abra uma ferramenta Adobe Analytics existente. Ao criar a ferramenta, você pode definir **[!UICONTROL Método de configuração]** como **[!UICONTROL Automático]**.

   ![Adicionar a ferramenta Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Selecione Conjuntos de relatórios de preparo/produção, conforme apropriado.

1. Expanda **[!UICONTROL Gerenciamento de biblioteca]** e verifique se **[!UICONTROL Carregar biblioteca em]** está definido como **[!UICONTROL Início da página]**.

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

   * A regra de carregamento de página no DTM inclui apenas o código `pagetracker.js` . Todos os campos `assetAnalytics` são considerados substituições de valores padrão. Elas não são exigidas por padrão.
   * O código chama `assetAnalytics.dispatcher.init()` depois de garantir que `_satellite.getToolsByType('sc')[0].getS()` seja inicializado e `assetAnalytics,dispatcher.init` esteja disponível. Portanto, você pode ignorar a adição na etapa 11.
   * Conforme indicado nos comentários no código do Rastreador de página do Insights (**[!UICONTROL Ferramentas > Ativos > Rastreador de página do Insights]**), quando o Rastreador de página não cria um objeto `AppMeasurement`, os três primeiros argumentos (RSID, Servidor de rastreamento e Namespace do visitante) são irrelevantes. Strings vazias são passadas para realçar isso.\
      Os argumentos restantes correspondem ao que está configurado na página Configuração do Insights (**[!UICONTROL Ferramentas > Ativos > Configuração do Insights]**).
   * O objeto AppMeasurement é recuperado consultando `satelliteLib` para todos os mecanismos de SiteCatalyst disponíveis. Se várias tags estiverem configuradas, altere o índice do seletor de matriz apropriadamente. As entradas no array são solicitadas de acordo com as ferramentas do SiteCatalyst disponíveis na interface do DTM.

1. Salve e feche a janela Editor de código e salve as alterações na configuração da Ferramenta.
1. Na guia **[!UICONTROL Approvals]** , aprove as duas aprovações pendentes. A tag do DTM está pronta para inserção na página da Web. Para obter detalhes sobre como inserir tags do DTM em páginas da Web, consulte [Integrar DTM em modelos de página personalizados](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/).
