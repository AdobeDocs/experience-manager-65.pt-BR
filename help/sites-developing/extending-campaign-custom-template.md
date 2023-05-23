---
title: Criação de um modelo de página AEM personalizado com componentes de formulário do Adobe Campaign
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: Criar um modelo de página personalizado que use componentes do Adobe Campaign Form
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Criação de um modelo de página AEM personalizado com componentes de formulário do Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

Esta página explica como criar um modelo de página personalizado que usa o [Formulário do Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) Geometrixx examinando o modo como o modelo para atividades no exterior ( `/apps/geometrixx-outdoors/components/page_campaign_profile`) é implementada e aponta para informações importantes que podem ser necessárias ao criar seu próprio modelo personalizado.

>[!NOTE]
>
>[O email e os exemplos de formulário estão disponíveis somente no Geometrixx](/help/sites-developing/we-retail.md). Baixe o conteúdo de Geometrixx de amostra do Compartilhamento de pacotes.

Para criar um modelo de página do AEM personalizado usando componentes do Adobe Campaign Form, verifique se você tem o seguinte:

1. **Corrigir resourceSuperType**

   Verifique se o componente de página herda de `mcm/campaign/components/profile`.

   Isso é necessário para que os servlets obtenham e salvem informações

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Configurações do ClientContext**

   Ao observar as configurações de clientcontext ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`) você verá as seguintes configurações:

   * O ClientContext aponta para `/etc/clientcontext/campaign`
   * Há também uma *config* nó.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   Entrada **head.jsp**, você verá as seguintes linhas que usam a variável **clientcontext-config** e a variável **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   Entrada **body.jsp**, os serviços em nuvem são carregados na parte inferior da página:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propriedades da página de campanha**

   Para poder selecionar um modelo Adobe Campaign, as propriedades da página são estendidas com o **Campaign** guia:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Configurações do modelo**.

   No modelo ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) você verá os seguintes valores padrão:

   | **acMapping** | mapRecipient (para Adobe Campaign 6.1), perfil (para Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | email |

   ![chlimage_1-204](assets/chlimage_1-204.png)
