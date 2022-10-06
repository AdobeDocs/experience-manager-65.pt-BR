---
title: Integração ao Adobe Analytics
seo-title: Integrating with Adobe Analytics
description: Saiba como integrar o AEM com o Adobe Analytics.
seo-description: Learn how to integrate AEM with Adobe Analytics.
uuid: d8548263-6ac5-45fb-8c70-52ecd4161bbb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 444c522e-2f33-4f41-846c-8d317e799659
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 73%

---

# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

A integração do Adobe Analytics e do AEM permite rastrear a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM faça autenticação com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem página e dados do usuário; por exemplo:

* dados que os componentes do AEM coletam
* cliques em links
* informações de uso de vídeo
* o número de visitas à página do Adobe Analytics

As seguintes páginas ajudam a configurar a integração:

* [Conectar ao Adobe Analytics e Criar Frameworks](/help/sites-administering/adobeanalytics-connect.md)
* [Configuração do rastreamento de links para o Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mapeamento de dados do componente com propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuração do rastreamento de vídeo para o Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificações do Adobe](/help/sites-administering/adobeanalytics-classifications.md)

Também é possível usar a variável [Assistente de opt-in](/help/sites-administering/opt-in.md) para realizar facilmente a integração.

>[!NOTE]
>
>Consulte também o artigo de instruções: [Integração de AEM com o Adobe Target e o Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Informações adicionais {#further-information}

Consulte:

* [Estender a integração do Adobe Analytics](/help/sites-developing/extending-analytics.md) para obter informações sobre o desenvolvimento de componentes que coletam dados do usuário e personalização da estrutura do Adobe Analytics.
* O artigo da base de conhecimento, [Integração do Adobe Analytics - solução de problemas](https://helpx.adobe.com/br/experience-manager/kb/sitecatalystintegrationtroubleshooting.html), para obter informações sobre como solucionar problemas de integração com o Adobe Analytics.

>[!NOTE]
>
>Se estiver usando o Adobe Analytics com uma configuração de proxy personalizada, precisará [configurar dois pacotes OSGi](/help/sites-deploying/configuring-osgi.md) (por exemplo, com o console da Web) necessários para as configurações de proxy do **Apache HTTP Client**. Ambos são necessários, pois algumas funcionalidades do AEM usam as APIs 3.x, enquanto outros usam as APIs 4.x. Configurar o:
>
>* **Day Commons HTTP Client 3.1** para configurar a API 3.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Configuração de proxy de componentes HTTP do Apache** para configurar a API 4.x;
   >  por exemplo, [https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

