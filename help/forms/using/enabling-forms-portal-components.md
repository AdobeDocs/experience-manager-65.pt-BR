---
title: Ativar componentes do portal de formulários
seo-title: Enabling forms portal components
description: Pronto para uso, os componentes do Portal Forms são desativados. Ative os grupos de Predicados de Serviços de Documento e Serviços de Documento para ativar os componentes do Portal do Forms.
seo-description: Out of the box, Forms Portal components are disabled. Enable Document Services and Document Services Predicates groups to enable Forms Portal components.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Ativar componentes do portal de formulários {#enabling-forms-portal-components}

Pronto para uso, os componentes do portal de formulários não estão disponíveis para uso. Para fazer com que os componentes apareçam na lista de componentes disponíveis AEM sidekick, execute as seguintes etapas:

1. Faça logon na instância do autor do site e abra uma página do AEM Sites.

1. Para as páginas que usam um modelo estático, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![lista suspensa de tela](assets/canvas-drop-down.png) > **Design** para abrir a página no modo Design.
   1. Toque em qualquer componente (com uma borda azul) e toque em ![nível de campo](assets/field-level.png) para selecionar o sistema de parágrafo que contém o componente atual.
   1. No sistema de parágrafo, toque em ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar no sistema de parágrafo.
   1. Na lista de **[!UICONTROL Componentes permitidos]**, ativar caixas de seleção para **[!UICONTROL Serviços de documento]** e **[!UICONTROL Predicados dos serviços de documento]** componentes. Toque **[!UICONTROL OK]**.

1. Para as páginas que usam um modelo dinâmico, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![propriedades](assets/properties.png) > **Editar modelo** para abrir o modelo da página.
   1. Toque **Contêiner de layout** e tocar ![FeedManagement](/help/forms/using/assets/feedmanagement.png). No **Componentes permitidos** , ative a **Predicados de serviços de documentos e serviços de documentos** opções e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Você também pode ativar componentes específicos dessas categorias selecionando os componentes. Para obter mais informações sobre os componentes e seu uso, consulte [Criação de uma página de portal de formulário](/help/forms/using/creating-form-portal-page.md) e [Como incorporar o componente de link em uma página](/help/forms/using/embedding-link-component-page.md).

Agora, as categorias de componentes Serviços de documento e Predicados de serviços de documento estão disponíveis no navegador de componentes. Os componentes são habilitados para todas as páginas que usam o mesmo modelo.

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e Envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
