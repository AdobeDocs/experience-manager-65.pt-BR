---
title: Criação de um modelo de página AEM personalizado com componentes de formulário do Adobe Campaign
description: Criar um modelo de página personalizado que use componentes do Adobe Campaign Form
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ad8f849384e58511de97611d1b26c4fc96022062
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Criação de um modelo de página AEM personalizado com componentes de formulário do Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

Esta página explica como criar um modelo de página personalizado que usa componentes do [Formulário do Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) examinando como o modelo Geometrixx-outdoors (`/apps/geometrixx-outdoors/components/page_campaign_profile`) é implementado e aponta para informações importantes que você pode precisar ao criar seu próprio modelo personalizado.

>[!NOTE]
>
>[Amostras de email e formulário só estão disponíveis em Geometrixx](/help/sites-developing/we-retail.md). Baixe o conteúdo de Geometrixx de amostra do Compartilhamento de pacotes.

>[!CAUTION]
>
>Os componentes de email do AEM foram descontinuados. Devido à natureza do email, que mescla conteúdo e estilo, os componentes de email fornecidos prontos para uso pelo AEM tornam-se de reutilização limitada para os clientes, devido à necessidade de implementar estilos personalizados em quaisquer componentes que sejam necessários para projetos.
>
>Os componentes de email podem ser implementados no nível do projeto, e os componentes de email do AEM obsoletos ilustram como isso pode ser feito. No entanto, não use esses componentes obsoletos em projetos.


Para criar um modelo de página do AEM personalizado usando componentes do Adobe Campaign Form, verifique se você tem o seguinte:

1. **Corrigir resourceSuperType**

   Verifique se o componente de página herda de `mcm/campaign/components/profile`.

   Isso é necessário para que os servlets obtenham e salvem informações

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Configurações do ClientContext**

   Ao examinar as configurações de clientcontext ( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`), você verá as seguintes configurações:

   * O ClientContext aponta para `/etc/clientcontext/campaign`
   * Também há um nó *config* extra.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   Em **head.jsp**, você verá as seguintes linhas que usam o **clientcontext-config** e o **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   Em **body.jsp**, os serviços em nuvem são carregados na parte inferior da página:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propriedades da página de campanha**

   Para poder selecionar um modelo de Adobe Campaign, as propriedades de página são estendidas com a guia **Campanha**:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Configurações do modelo**.

   No modelo ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) você verá os seguintes valores padrão:

   | **acMapping** | mapRecipient (para Adobe Campaign 6.1), perfil (para Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | email |

   ![chlimage_1-204](assets/chlimage_1-204.png)
