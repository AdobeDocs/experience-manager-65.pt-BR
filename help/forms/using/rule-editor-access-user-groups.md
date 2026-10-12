---
title: Conceder acesso ao editor de regras para grupos de usuários selecionados
description: Conceda acesso restrito ao editor de regras para grupos de usuários selecionados.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: a1a2b277-3133-404b-a7fc-337cedddb12c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 7%
---
# Conceder acesso ao editor de regras para grupos de usuários selecionados{#grant-rule-editor-access-to-select-user-groups}

A Adobe <span class="preview"> recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve uma abordagem mais antiga para a criação do Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

Você pode ter diferentes tipos de usuários com habilidades variadas que trabalham com o Adaptive Forms. Embora os usuários especialistas possam ter o conhecimento certo para trabalhar com scripts e regras complexas, pode haver usuários de nível básico que precisam trabalhar somente com o layout e as propriedades básicas dos formulários adaptáveis.

O AEM Forms permite limitar o acesso do editor de regras aos usuários com base em sua função. Nas definições do Serviço de Configuração do Forms Adaptive, você pode especificar os [grupos de usuários](/help/sites-administering/security.md) que podem exibir e acessar o editor de regras.

## Especificar grupos de usuários que podem acessar o editor de regras {#specify-user-groups-that-can-access-rule-editor}

1. Faça logon no AEM Forms como administrador.
1. Na instância do autor, clique em ![adobeexperiencemanager](assets/adobeexperiencemanager.png)Adobe Experience Manager > Ferramentas ![martelo](assets/hammer.png) > Operações > Console da Web. O Console da Web é aberto em uma nova janela.

   ![1-2](assets/1-2.png)

1. Na janela Console da Web, localize e clique em **[!UICONTROL Configuração do canal da Web de formulário adaptável e comunicação interativa]**. A caixa de diálogo **[!UICONTROL Configuração do canal da Web de formulário adaptável e comunicação interativa]** é exibida. Não altere nenhum valor e clique em **Salvar**.

   Ele cria um arquivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config no repositório do CRX.

1. Faça logon no CRXDE como administrador. Abra o arquivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config para edição.
1. Use a propriedade a seguir para especificar o nome de um grupo que possa acessar o editor de regras (por exemplo, RuleEditorsUserGroup) e clique em **Salvar Tudo**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar o acesso para vários grupos, especifique uma lista de valores separados por vírgula:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Criar Usuário](assets/create_user_new.png)

   Agora, quando um usuário que não faz parte do grupo de usuários especificado (aqui RuleEditorsUserGroup) toca em um campo, o ícone Editar regra ( ![edit-rules1](assets/edit-rules1.png)) não está disponível para ele na barra de ferramentas dos componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de ferramentas Componentes visível para um usuário com acesso ao editor de regras

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de ferramentas Componentes conforme visível para um usuário sem acesso ao editor de regras

   Para obter instruções sobre como adicionar usuários a grupos, consulte [Administração e Segurança do Usuário](/help/sites-administering/security.md).
