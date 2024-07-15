---
title: Integração ao Adobe Analytics
description: Saiba como integrar o Adobe Experience Manager (AEM) ao Adobe Analytics.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 0a87ece4-57ed-4022-a78a-264c1edf4b4e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 58%

---

# Integração ao Adobe Analytics{#integrating-with-adobe-analytics}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/integrating-adobe-analytics.html) |
| AEM 6.5 | Este artigo |


Integrar o Adobe Analytics e o AEM permite rastrear a atividade da página da Web:

* Uma configuração do Adobe Analytics permite que o AEM faça autenticação com o Adobe Analytics.
* Uma estrutura identifica os dados enviados para o conjunto de relatórios do Adobe Analytics.

Os dados incluem página e dados do usuário; por exemplo:

* dados que os componentes do AEM coletam
* cliques em links
* informações de uso de vídeo
* o número de visitas à página do Adobe Analytics

As seguintes páginas ajudam a configurar a integração:

* [Conexão com o Adobe Analytics e criação de estruturas](/help/sites-administering/adobeanalytics-connect.md)
* [Configuração do rastreamento de links para o Adobe Analytics](/help/sites-administering/adobeanalytics-link.md)
* [Mapeamento de dados do componente com propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md)
* [Configuração do rastreamento de vídeo para o Adobe Analytics](/help/sites-administering/adobeanalytics-video.md)
* [Classificações de Adobe](/help/sites-administering/adobeanalytics-classifications.md)

Você também pode usar o [Assistente de aceitação](/help/sites-administering/opt-in.md) para fazer a integração facilmente.

>[!NOTE]
>
>Consulte também o artigo de instruções: [Integração do AEM com o Adobe Target e o Adobe Analytics usando o DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

## Informações adicionais {#further-information}

Consulte:

* [Estendendo a Integração do Adobe Analytics](/help/sites-developing/extending-analytics.md) para obter informações sobre o desenvolvimento de componentes que coletam dados do usuário e personalização da estrutura do Adobe Analytics.
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
