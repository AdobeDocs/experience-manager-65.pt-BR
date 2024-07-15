---
title: Como criar um formulário adaptável?
description: Saiba como criar um Formulário adaptável usando o  [!DNL Experience Manager Forms]. Os Forms adaptáveis são formulários de HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um Formulário adaptável com base em um Modelo de dados de formulário e um esquema XML ou JSON.
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 23%

---

# Criar componentes principais com base no Forms adaptável {#creating-an-adaptive-form-core-components}


O Adobe <span class="preview"> recomenda usar os Componentes Principais para [adicionar o Adaptive Forms a uma Página do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) ou para [criar o Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) independente. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

Formulários adaptáveis permitem criar formulários envolventes, responsivos, dinâmicos e adaptáveis. O AEM Forms fornece uma interface de usuário empresarial fácil de usar para criar rapidamente o Adaptive Forms. A interface do usuário oferece navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um Formulário adaptável.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais de formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes oferecem recursos de personalização, redução do tempo de desenvolvimento e dos custos de manutenção para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. A Adobe recomenda o uso desses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Componentes de fundamentais de formulários adaptáveis](creating-adaptive-form.md): esses são componentes clássicos (antigos) de captura de dados. Você pode continuar usando-os para editar seus componentes fundamentais já existentes com base no formulário adaptável. Se você estiver criando formulários, a Adobe recomenda o uso dos [Componentes principais do Adaptive Forms](/help/forms/using/create-adaptive-form.md) para criar um Adaptive Forms.

## Pré-requisitos

Você precisará do seguinte para criar um formulário adaptável:

* **Habilitar os Componentes Principais do Forms Adaptive para seu ambiente**: o projeto AEM Archetype versão 41 ou posterior é necessário para [habilitar os Componentes Principais para seu ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Ao habilitar os Componentes principais para o seu ambiente, o modelo **Forms adaptável (Componente principal)** e o tema da Tela são adicionados ao seu ambiente.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência, e a ação de envio define a ação a ser executada no envio de um formulário adaptável. Você também pode implantar [modelos de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) em seu ambiente. Isso o ajuda a começar a criar formulários rapidamente.

  >[!NOTE]
  >
  > Se você não tiver o modelo **Formulários adaptáveis (componente principal)** em seu ambiente, [Habilite os Componentes principais dos formulários adaptáveis para o seu ambiente](/help/forms/using/enable-adaptive-forms-core-components.md). Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** será adicionado ao seu ambiente.

* **Um tema de formulários adaptáveis**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes.  O tema `Canvas` é adicionado por padrão quando você habilita os componentes principais para o seu ambiente. Você pode [baixar e personalizar os temas padrão](create-or-customize-themes-for-adaptive-forms-core-components.md). Para **temas prontos**, você pode implantar [temas de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) em seu ambiente. Isso o ajuda a começar a estilizar seus formulários e a fornecer uma estrutura básica para criar ou personalizar um tema de acordo com os requisitos da empresa.

* **Permissões**: adicionar usuários ao grupo [!DNL forms-users]. Os membros do grupo [!DNL forms-users] tem permissões para criar formulários adaptáveis. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Criação de um Formulário adaptável {#create-an-adaptive-form}

1. Faça logon na [instância de autor do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=en#author-and-publish-installs) local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Criar Forms Adaptável]**.

1. Selecione um modelo dos Componentes principais adaptáveis do Forms e clique em **[!UICONTROL Avançar]**.

1. A opção **[!UICONTROL Adicionar propriedades]** é exibida. Especifique os valores para os seguintes campos de propriedade. Os campos Título e Nome são obrigatórios:

   * **[!UICONTROL Título:]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário do [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** especifica o nome do formulário. Um nó com o nome especificado será criado no repositório. Ao começar a digitar um título, o valor do campo de nome é gerado automaticamente. É possível alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados.
   * **[!UICONTROL Descrição:]** Especifica as informações detalhadas sobre o formulário.
   * **[!UICONTROL Biblioteca de Temas de Cliente]:** Especifica o tema para um Formulário Adaptável. Por padrão, o tema `adaptiveform.theme.canvas3` é selecionado. Você também pode escolher um tema diferente do menu suspenso **[!UICONTROL Biblioteca de Temas do Cliente]**.
   * **[!UICONTROL Contêiner de Configuração:]** Define um local onde os arquivos de configuração do Adaptive Forms são armazenados. Esses arquivos de configuração contêm configurações e propriedades relacionadas ao comportamento e à aparência do Forms adaptável.
   * **[!UICONTROL Marcas:]** especifica as marcas para identificar exclusivamente o Formulário adaptável. A ajuda das tags na pesquisa do formulário. Para criar marcas, digite novos nomes de marcas na caixa **[!UICONTROL Marcas]**.
1. Selecione **[!UICONTROL Criar]**. Um formulário adaptável é criado e uma caixa de diálogo para abrir o formulário para edição é exibida.


1. Selecione **[!UICONTROL Editar]** para abrir o formulário recém-criado em uma nova guia. O formulário é aberto para edição e exibe o conteúdo disponível no template. Ele também exibe a barra lateral para personalizar o formulário recém-criado.


## Usar os Componentes principais adaptáveis do Forms para criar seu formulário

Depois de abrir o formulário para edição, você pode usar os Componentes principais do Adaptive Forms disponíveis para adicionar campos de formulário ao formulário. Você pode arrastar e soltar ou usar a opção + [inserir componente] para adicionar esses componentes a um formulário. Consulte a documentação dos Componentes principais do AEM para saber mais sobre os [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR#components). Você também pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação.

## Configurar a ação enviar para um formulário adaptável {#configure-submit-action-for-form}

Uma ação enviar permite escolher o destino dos dados capturados por meio de um formulário adaptável. É acionado quando um usuário clica no botão Enviar em um Formulário adaptável. Os formulários adaptáveis incluem algumas ações de envio prontas para uso. Você também pode estender ações de envio padrão para criar sua própria ação de envio personalizada. Para configurar uma Ação de envio para o formulário:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/using/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.

1. Clique na guia **[!UICONTROL Envio]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar uma ação de envio](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. Selecione e configure uma **[!UICONTROL Ação de envio]**, com base em suas necessidades. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de Envio do Formulário Adaptável](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redirecionar o usuário para uma página ou mostrar uma mensagem de agradecimento no envio do formulário

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou uma mensagem. Para redirecionar o usuário ou configurar a mensagem de agradecimento:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/using/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Envio]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável e configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * Para configurar uma URL de Redirecionamento, para a opção Enviar, selecione a opção **[!UICONTROL Redirecionar para URL]** e procure e selecione uma página do AEM Sites ou forneça a URL de uma página externa.

   * Para configurar uma mensagem personalizada ou de agradecimento, para a opção Enviar, selecione a opção **[!UICONTROL Mostrar Mensagem]** e forneça uma mensagem na caixa **[!UICONTROL Conteúdo da Mensagem]**. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.

## Configurar um esquema ou modelo de dados de formulário para um formulário adaptável {#configure-schema-or-data-model-for-form}

Você pode usar o modelo de dados do formulário e conectar um formulário a uma fonte de dados para enviar e receber dados com base nas ações do usuário. Também é possível conectar um formulário a um esquema JSON para receber os dados enviados em um formato predefinido. De acordo com os requisitos, conecte o formulário a um esquema JSON ou modelo de dados do formulário:

* [Criar um esquema JSON e carregar para o seu ambiente](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [Criar um modelo de dados de formulário](/help/forms/using/create-form-data-models.md)

### Configurar um esquema JSON ou um modelo de dados de formulário para o formulário

Para configurar um Esquema JSON ou um Modelo de dados de formulário para seu formulário:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/using/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Modelo de Dados]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável e configurar um esquema JSON ou modelo de dados de formulário](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Selecione e configure um esquema JSON ou um modelo de dados de formulário, com base em seus requisitos:

   * Ao selecionar a opção **[!UICONTROL Modelo de formulário]**, use a opção **[!UICONTROL Selecionar modelo de dados de formulário]** para selecionar um modelo de dados de formulário pré-configurado.
   * Ao selecionar a opção **[!UICONTROL Esquema]**, use a opção **[!UICONTROL Esquema]** para selecionar um esquema JSON para o formulário.

1. Clique em **[!UICONTROL Concluído]**.

>[!NOTE]
>
> Você pode editar o esquema JSON ou o modelo de dados de formulário para um formulário adaptável usando as propriedades do Contêiner do guia.

## Configurar um serviço de preenchimento  {#configure-prefill-service-for-form}

Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. É possível:

* [Criar um serviço de preenchimento prévio personalizado](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [Usar o serviço de preenchimento do modelo de dados de formulário](#fdm-prefill-service)

### Usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável {#fdm-prefill-service}

Você pode usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável usando um modelo de dados de formulário ou um serviço de preenchimento prévio personalizado. O serviço de Preenchimento de Modelo de Dados de Formulário usa o [Obter Serviço do Modelo de Dados de Formulário](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) configurado para recuperar dados. Para usar o serviço de Preenchimento de modelo de dados de formulário para um Formulário adaptável:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/using/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/using/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável e configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. Selecione um modelo de dados de formulário. Abra a guia **[!UICONTROL Básico]**. No serviço de preenchimento, selecione **[!UICONTROL Serviço de Preenchimento de Modelo de Dados de Formulário]**.
1. Clique em **[!UICONTROL Concluído]**. O formulário adaptável agora está configurado para usar o Preenchimento prévio do modelo de dados de formulário. Agora você pode usar o [editor de regras](rule-editor.md) para criar regras e preencher previamente os campos do formulário.

## Como renomear um formulário adaptável para AEM?{#rename-an-AEM-Adaptive-Form}

Para renomear um formulário adaptável, execute as seguintes etapas:

1. Selecione um formulário adaptável na interface do usuário do AEM Forms.
1. Clique nas **Propriedades** localizadas no painel superior.

   ![Propriedades](/help/forms/using/assets/rename-form-properties.png)

1. Altere o nome do formulário na guia **Título**, conforme mostrado na imagem abaixo.
1. Clique em **Salvar e fechar**.

   ![Renomear um Formulário adaptável de AEM](/help/forms/using/assets/rename-form-title.png)


<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## O que vem a seguir

* [Usar o editor de regras para adicionar comportamento dinâmico ao formulário](rule-editor.md)
* [Criar ou personalizar temas para Componentes principais com base no Forms adaptável](create-or-customize-themes-for-adaptive-forms-core-components.md)


## Consulte também:

* [Criar um formulário adaptável baseado nos Componentes principais](create-an-adaptive-form-core-components.md)
* [Criar ou adicionar um formulário adaptável a uma página do AEM Sites ou a um fragmento de experiência](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Modelos de temas de exemplo e modelos de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
