---
title: Invalidar o cache CDN por meio do Dynamic Media
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pelo Dynamic Media, em vez de aguardar a expiração do cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# Invalidar o cache CDN por meio do Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Os ativos de Mídia dinâmica são armazenados em cache pelo CDN (Content Delivery Network) para delivery rápido aos seus clientes. No entanto, ao fazer atualizações nesses ativos, você pode desejar que essas alterações entrem em vigor imediatamente em seu site. Limpar ou invalidar o cache de CDN permite que você atualize rapidamente os ativos entregues pelo Dynamic Media. Em vez de esperar que o cache expire usando um valor TTL (Time To Live) (o padrão é 10 horas), você pode enviar uma solicitação do Dynamic Media para que o cache expire imediatamente.

>[!IMPORTANT]
>
>Estas etapas aplicam-se somente ao modo Dynamic Media - Scene7 no AEM 6.5, Service Pack 6 ou posterior. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

Consulte também Visão geral do [cache no Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o conteúdo em cache CDN para ativos de Dynamic Media:**

1. No AEM 6.5.6 ou posterior, toque em **[!UICONTROL Ferramentas > Ativos > Invalidação de CDN.]**

   ![Recurso de validação CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Na página de Invalidação de CDN, defina as opções desejadas:

   | Opção | Descrição |
   | --- | --- |
   | **[!UICONTROL Invalidar predefinições de imagem associadas a ativos na CDN]** | Ao marcar essa opção, você pode selecionar um ou mais ativos do Dynamic Media, independentemente do tipo MIME, e suas predefinições de imagens associadas para a invalidação do cache.<br>Embora você possa selecionar uma ou mais pastas que contêm ativos, o Adobe não recomenda essa abordagem. Em vez disso, você deve selecionar arquivos de ativos individuais.<br>Vá para a próxima etapa. |
   | **[!UICONTROL Invalidação com base no modelo]** | Ao marcar essa opção, você pode selecionar ativos de Mídia dinâmica e o modelo de Invalidação criados anteriormente. Use esta opção com |
   | **[!UICONTROL Adicionar ativos]** | Blá |
   | **[!UICONTROL Adicionar URL]** | Adicione manualmente caminhos de URL completos aos ativos do Dynamic Media cujo cache você deseja invalidar. |

1. 
1. Toque em **[!UICONTROL Avançar.]**
1. 
