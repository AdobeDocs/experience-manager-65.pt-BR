---
title: Ativar o Assets Insights por meio do DTM
description: Saiba como usar o Adobe Dynamic Tag Management (DTM) para ativar o Assets Insights.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Ativar o Assets Insights por meio do DTM {#enable-asset-insights-through-dtm}

O Adobe Dynamic Tag Management é uma ferramenta que ativa as ferramentas de marketing digital. Ele é fornecido gratuitamente para clientes do Adobe Analytics. Você pode personalizar seu código de rastreamento para permitir que soluções de CMS de terceiros usem o Assets Insights ou usar o DTM para inserir tags do Assets Insights. Os insights só são aceitos e fornecidos para imagens.

>[!CAUTION]
>
>O DTM do Adobe foi descontinuado em favor do [!DNL Adobe Experience Platform] e logo chegará ao [fim da vida útil](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f). A Adobe recomenda que você [use [!DNL Adobe Experience Platform] para insights de ativos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html).

Execute essas etapas para ativar o Assets Insights por meio do DTM.

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Configuração do Insights]**.
1. [Configurar a implantação do Experience Manager com o Cloud Service do DTM](/help/sites-administering/dtm.md)

   O token da API deve estar disponível depois que você fizer logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e visitar **[!UICONTROL Configurações de Conta]** no Perfil do usuário. Essa etapa não é necessária do ponto de vista do Assets Insights, pois a integração do Experience Manager Sites com o Assets Insights ainda está em andamento.

1. Faça logon em [https://dtm.adobe.com](https://dtm.adobe.com/) e selecione uma empresa, conforme apropriado.
1. Criar ou abrir uma Propriedade da Web existente

   * Selecione a guia **[!UICONTROL Propriedades da Web]** e clique em **[!UICONTROL Adicionar Propriedade]**.

   * Atualize os campos conforme apropriado e clique em **[!UICONTROL Criar Propriedade]**. Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR).

   ![Criar propriedade da Web de edição](assets/Create-edit-web-property.png)

1. Na guia **[!UICONTROL Regras]**, selecione **[!UICONTROL Regras de carregamento de página]** no painel de navegação e clique em **[!UICONTROL Criar nova regra]**.

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. Expanda **[!UICONTROL JavaScript /Marcas de Terceiros]**. Em seguida, clique em **[!UICONTROL Adicionar novo script]** na guia **[!UICONTROL HTML sequencial]** para abrir a caixa de diálogo Script.

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. Clique no logotipo do Experience Manager e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**.
1. Clique em **[!UICONTROL Rastreador de páginas do Insights]**, copie o código do rastreador e cole-o na caixa de diálogo de Script que você abriu na etapa 6. Salve as alterações.

   >[!NOTE]
   >
   >* `AppMeasurement.js` foi removido. Espera-se que esteja disponível por meio da ferramenta Adobe Analytics do DTM.
   >* A chamada para `assetAnalytics.dispatcher.init()` foi removida. Espera-se que a função seja chamada assim que a ferramenta Adobe Analytics do DTM terminar de carregar.
   >* Dependendo de onde o Rastreador de páginas do Assets Insights estiver hospedado (por exemplo, Experience Manager, CDN e assim por diante), a origem da origem do script pode exigir alterações.
   >* Para o Rastreador de páginas hospedado no Experience Manager, a origem deve apontar para uma instância de publicação usando o nome de host da instância do Dispatcher.

1. Acessar `https://dtm.adobe.com`. Clique em **[!UICONTROL Visão geral]** na propriedade da Web e clique em **[!UICONTROL Adicionar ferramenta]** ou abra uma Ferramenta do Adobe Analytics existente. Ao criar a ferramenta, você pode definir o **[!UICONTROL Método de Configuração]** como **[!UICONTROL Automático]**.

   ![Adicionar ferramenta do Adobe Analytics](assets/Add-Adobe-Analytics-Tool.png)

   Selecione Conjuntos de relatórios de Preparo/Produção, conforme apropriado.

1. Expanda **[!UICONTROL Gerenciamento de Biblioteca]** e certifique-se de que **[!UICONTROL Carregar Biblioteca em]** esteja definido como **[!UICONTROL Topo da Página]**.

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * A regra de carregamento de página no DTM inclui apenas o código `pagetracker.js`. Quaisquer campos `assetAnalytics` são considerados substituições para valores padrão. Elas não são exigidas por padrão.
   * O código chama `assetAnalytics.dispatcher.init()` depois de verificar se `_satellite.getToolsByType('sc')[0].getS()` foi inicializado e se `assetAnalytics,dispatcher.init` está disponível. Portanto, você pode pular a adição na etapa 11.
   * Conforme indicado em comentários no código do Rastreador de Páginas do Insights (**[!UICONTROL Ferramentas > Assets > Rastreador de Páginas do Insights]**), quando o Rastreador de Páginas não cria um objeto `AppMeasurement`, os três primeiros argumentos (RSID, Servidor de Rastreamento e Namespace do Visitante) são irrelevantes. Cadeias de caracteres vazias são passadas para realçar isso.\
     Os argumentos restantes correspondem ao que está configurado na página Configuração de Insights (**[!UICONTROL Ferramentas > Assets > Configuração de Insights]**).
   * O objeto de AppMeasurement é recuperado consultando `satelliteLib` para todos os mecanismos de SiteCatalyst disponíveis. Se várias tags estiverem configuradas, altere o índice do seletor de matriz apropriadamente. As entradas no storage são ordenadas de acordo com as ferramentas do SiteCatalyst disponíveis na interface do DTM.

1. Salve e feche a janela Editor de códigos e salve as alterações na configuração da Ferramenta.
1. Na guia **[!UICONTROL Aprovações]**, aprove as duas aprovações pendentes. A tag do DTM está pronta para ser inserida na página da Web.
