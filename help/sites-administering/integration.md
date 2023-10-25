---
title: Integração de soluções
description: Saiba mais sobre como integrar o Adobe Experience Manager (AEM) a outros serviços da Adobe ou de terceiros.
uuid: 3bf56b1b-284d-4f14-8974-0a595ece5028
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b5ff918d-08ab-4307-a807-693468fc083b
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 25%

---

# Integração de soluções{#solutions-integration}

* [Integração com a Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md)
* [Integração com serviços de terceiros](/help/sites-administering/third-party-services.md)
* [Analytics com provedores externos](/help/sites-administering/external-providers.md)
* [Produtor do catálogo](/help/sites-administering/catalog-producer.md)
* [SharePoint Connector](/help/sites-administering/sharepoint-connector.md)
* [Entender, aplicar e preparar Tags inteligentes](/help/assets/enhanced-smart-tags.md)

As seguintes informações estão disponíveis sobre a integração do AEM com outros serviços de Adobe ou de terceiros:

>[!NOTE]
>
>Se estiver usando uma configuração de proxy personalizada juntamente com sua integração, você deverá definir ambas as configurações de proxy do HTTP Client, pois algumas funcionalidades do AEM estão usando as APIs 3.x e algumas outras as APIs 4.x:
>
>* A 3.x está configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* A 4.x está configurada com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
