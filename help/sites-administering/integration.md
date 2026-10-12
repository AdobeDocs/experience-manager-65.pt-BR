---
title: Integração de soluções
description: Saiba mais sobre como integrar o Adobe Experience Manager (AEM) com outros serviços da Adobe ou de terceiros.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ee5e8ebb-773f-4aa6-9c3e-2cc3bf4a3bbd
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 10%
---
# Integração de soluções{#solutions-integration}

* [Integração com a Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md)
* [Integração com serviços de terceiros](/help/sites-administering/third-party-services.md)
* [Analytics com provedores externos](/help/sites-administering/external-providers.md)
* [Produtor do catálogo](/help/sites-administering/catalog-producer.md)
* [Entender, aplicar e preparar Tags inteligentes](/help/assets/enhanced-smart-tags.md)

As seguintes informações estão disponíveis sobre a integração do AEM com outros serviços da Adobe ou de terceiros:

>[!NOTE]
>
>Se estiver usando uma configuração de proxy personalizada juntamente com sua integração, você deve definir ambas as configurações de proxy do HTTP Client, pois algumas funcionalidades do AEM estão usando as APIs 3.x e algumas outras as APIs 4.x:
>
>* A 3.x está configurada com [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x está configurado com [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
