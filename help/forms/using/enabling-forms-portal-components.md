---
title: Ativar componentes do portal de formulários
seo-title: Ativar componentes do portal de formulários
description: Pronto para uso, os componentes do Portal Forms são desativados. Ative os grupos de Predicados de Serviços de Documento e Serviços de Documento para ativar os componentes do Portal do Forms.
seo-description: Pronto para uso, os componentes do Portal Forms são desativados. Ative os grupos de Predicados de Serviços de Documento e Serviços de Documento para ativar os componentes do Portal do Forms.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
feature: Portal do Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Ativar componentes do portal de formulários {#enabling-forms-portal-components}

Pronto para uso, os componentes do portal de formulários não estão disponíveis para uso. Para fazer com que os componentes apareçam na lista de componentes disponíveis AEM sidekick, execute as seguintes etapas:

1. Faça logon na instância do autor do site e abra uma página do AEM Sites.

1. Para as páginas que usam um modelo estático, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![tela suspensa](assets/canvas-drop-down.png) > **Design** para abrir a página no modo Design.
   1. Toque em qualquer componente (com uma borda azul) e toque em ![nível de campo](assets/field-level.png) para selecionar o sistema de parágrafo que contém o componente atual.
   1. No sistema de parágrafo, toque em ![settings_icon](assets/settings_icon.png) para abrir a caixa de diálogo Editar para o sistema de parágrafo.
   1. Na lista de **[!UICONTROL Componentes permitidos]**, ative as caixas de seleção para os componentes **[!UICONTROL Serviços de Documento]** e **[!UICONTROL Predicados de Serviços de Documento]**. Toque em **[!UICONTROL OK]**.

1. Para as páginas que usam um modelo dinâmico, execute as seguintes etapas:

   1. No cabeçalho da página, toque em ![properties](assets/properties.png) > **Edit Template** para abrir o modelo da página.
   1. Toque em **Contêiner de layout** e toque em ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Na guia **Componentes permitidos**, ative as opções **Serviços de Documento e Predicados de Serviços de Documento** e toque em ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Você também pode ativar componentes específicos dessas categorias selecionando os componentes. Para obter mais informações sobre os componentes e seu uso, consulte [Criação de uma página do portal de formulários](/help/forms/using/creating-form-portal-page.md) e [Incorporação do componente de link em uma página](/help/forms/using/embedding-link-component-page.md).

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
