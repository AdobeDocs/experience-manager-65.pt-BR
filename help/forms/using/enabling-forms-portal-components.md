---
title: Habilitar componentes do portal de formulários
description: Por padrão, os componentes do Forms Portal são desativados. Habilite os grupos Serviços de documento e Predicados de serviços de documento para habilitar os componentes do Portal do Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 5%

---

# Habilitar componentes do portal de formulários {#enabling-forms-portal-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Pronto para uso, os componentes do portal de formulários não estão disponíveis para uso. Para fazer os componentes aparecerem na lista de componentes disponíveis no sidekick AEM, execute as seguintes etapas:

1. Faça logon na instância de autor do site e abra uma página do AEM Sites.

1. Para as páginas que usam um modelo estático, execute as seguintes etapas:

   1. No cabeçalho da página, selecione ![tela suspensa](assets/canvas-drop-down.png) > **Design** para abrir a página no modo Design.
   1. Selecione qualquer componente (com uma borda azul) e selecione ![nível de campo](assets/field-level.png) para selecionar o sistema de parágrafo que contém o componente atual.
   1. No sistema de parágrafos, selecione ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar do sistema de parágrafos.
   1. Na lista de **[!UICONTROL Componentes Permitidos]**, habilite as caixas de seleção para **[!UICONTROL Serviços de Documento]** e **[!UICONTROL Predicados de Serviços de Documento]** componentes. Selecione **[!UICONTROL OK]**.

1. Para as páginas que usam um modelo dinâmico, execute as seguintes etapas:

   1. No cabeçalho da página, selecione ![propriedades](assets/properties.png) > **Editar modelo** para abrir o modelo da página.
   1. Selecione **Contêiner de layout** e selecione ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Na guia **Componentes Permitidos**, habilite as opções **Serviços de Documentos e Predicados de Serviços de Documentos** e selecione ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Você também pode ativar componentes específicos nessas categorias selecionando os componentes. Para obter mais informações sobre os componentes e seu uso, consulte [Criando uma página do portal de formulários](/help/forms/using/creating-form-portal-page.md) e [Incorporando componente de link em uma página](/help/forms/using/embedding-link-component-page.md).

Agora, as categorias de componentes Serviços de documento e Predicados de serviços de documento estão disponíveis no navegador de componentes. Os componentes são ativados para todas as páginas que usam o mesmo modelo.

## Artigos relacionados

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
