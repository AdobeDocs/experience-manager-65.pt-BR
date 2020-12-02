---
title: Ativação de componentes do portal de formulários
seo-title: Ativação de componentes do portal de formulários
description: Os componentes do Forms Portal estão desativados. Ative os serviços do Documento e os grupos Previsões de serviços do Documento para ativar os componentes do Forms Portal.
seo-description: Os componentes do Forms Portal estão desativados. Ative os serviços do Documento e os grupos Previsões de serviços do Documento para ativar os componentes do Forms Portal.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Habilitar componentes do portal de formulários {#enabling-forms-portal-components}

Os componentes do portal de formulários não estão disponíveis para uso. Para que os componentes apareçam na lista dos componentes disponíveis AEM sidekick, execute as seguintes etapas:

1. Faça logon na instância do autor do site e abra uma página do AEM Sites.

1. Para as páginas que usam um modelo estático, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![menu suspenso](assets/canvas-drop-down.png) > **Design** para abrir a página no modo Design.
   1. Toque em qualquer componente (com uma borda azul) e, em seguida, toque em ![field-level](assets/field-level.png) para selecionar o sistema de parágrafo que contém o componente atual.
   1. No sistema de parágrafo, toque em ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar para o sistema de parágrafo.
   1. Na lista de **[!UICONTROL Componentes permitidos]**, ative as caixas de seleção para os componentes **[!UICONTROL Documento Services]** e **[!UICONTROL Documento Services Predicates]**. Toque em **[!UICONTROL OK]**.

1. Para as páginas que usam um modelo dinâmico, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![propriedades](assets/properties.png) > **Editar modelo** para abrir o modelo da página.
   1. Toque em **Container de layout** e toque em ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Na guia **Componentes permitidos**, ative as opções **Predicados de serviços de Documento e serviços de Documento** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Você também pode ativar componentes específicos dessas categorias selecionando os componentes. Para obter mais informações sobre os componentes e seu uso, consulte [Criação de uma página do portal de formulários](/help/forms/using/creating-form-portal-page.md) e [Incorporação do componente de link em uma página](/help/forms/using/embedding-link-component-page.md).

Agora, os Serviços do Documento e os Previsões de serviços do Documento estão disponíveis no navegador de componentes. Os componentes são ativados para todas as páginas que usam o mesmo modelo.

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Lista de formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
