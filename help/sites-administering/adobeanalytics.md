---
title: Integração com o Adobe Analytics
seo-title: Integração com o Adobe Analytics
description: Saiba como integrar o AEM ao Adobe Analytics.
seo-description: Saiba como integrar o AEM ao Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
translation-type: tm+mt
source-git-commit: ca25e66b280db479f69c487753a557b0240233da

---


# Integração com o Adobe Analytics{#integrating-with-adobe-analytics}

A integração do Adobe Analytics e do AEM permite rastrear a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM se autentique com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem dados da página e do utilizador; por exemplo:

* dados que os componentes do AEM coletam
* cliques em links
* informações de uso do vídeo
* o número de visitas de página do Adobe Analytics

As páginas a seguir ajudam a configurar a integração:

* [Conexão com o Adobe Analytics e criação de estruturas](/help/sites-administering/adobeanalytics-connect.md)
* [Configuração do rastreamento de links para o Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mapeamento de dados de componentes com as propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuração do rastreamento de vídeo para o Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificações da Adobe](/help/sites-administering/adobeanalytics-classifications.md)

Você também pode usar o assistente [de](/help/sites-administering/opt-in.md) aceitação para executar facilmente a integração.

>[!NOTE]
>
>Consulte também o artigo de instruções: [Integração do AEM com o Adobe Target e o Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Informações adicionais {#further-information}

Consulte:

* [Extensão da integração](/help/sites-developing/extending-analytics.md) do Adobe Analytics para obter informações sobre o desenvolvimento de componentes que coletam dados de usuários e personalizam a estrutura do Adobe Analytics.
* O artigo da base de conhecimento, Integração do [Adobe Analytics - solução de problemas](https://helpx.adobe.com/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas de integração do Adobe Analytics.

>[!NOTE]
>
>Se você estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes](/help/sites-deploying/configuring-osgi.md) OSGi (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client** . Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
   >
   >
* **Configuração** de proxy de componentes HTTP Apache para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



